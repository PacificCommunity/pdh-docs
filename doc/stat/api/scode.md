---
description: >-
  Here are some worked examples of the PDH .Stat API being used for various
  reasons. Full details of each implementation are available in the provided
  Github links.
---

# Sample Code

## **Get all dataflow IDs from PDH .Stat API**

This python script returns a list of all existing dataflowIDs. This can be useful for applications which need to check for new/updated dataflows.

```python
import requests
from bs4 import BeautifulSoup

base_url = 'https://sdd-dotstat-api-gateway.azure-api.net/'
key = str(input('Enter subscription key: '))

def get_endpoints(base_url, key):
  """
  Get the dataflowIDs of all existing dataflows in PDH .Stat API
        :param base_url: the API's base URL
        :param key: your subscription key
        :return: list of strings
  """
  endpoints = []
  resources_url = base_url + 'dataflow/all/all/latest?detail=full'
  headers = {'Ocp-Apim-Subscription-Key': key}
  resp = requests.get(resources_url, headers=headers, verify=False)
  soup = BeautifulSoup(resp.text, 'xml')
  for name in soup.findAll('Dataflow'):
    endpoints.append(name['id'])
  return endpoints

df_ids = get_endpoints(base_url, key)
print(df_ids)
# Output: ['DF_CPI', 'DF_IMTS', 'DF_POCKET', 'DF_POP_SUM', 'DF_SDG']
```

## **Get basic metadata about a dataflow from PDH .Stat API**

This python script returns a dictionary with the title, agencyId, version for a given dataflowId. This can be useful for applications which harvest from PDH .Stat or simply need to display information about a dataset/dataflow. The function can be used iteratively for information on more than one dataflow.

```python
import requests
from bs4 import BeautifulSoup

base_url = 'https://sdd-dotstat-api-gateway.azure-api.net/'
df = str(input('Enter dataflow ID: '))
# Or hard-code an example dataflow
# df = 'DF_SDG'
key = str(input('Enter subscription key: '))
# Or hard-code your key
# key = 'your key'

def basic_metadata(base_url, df, key):
  """
  Get some basic metadata on a dataflow in PDH .Stat API
        :param base_url: the API's base URL (string)
        :param df: the dataflow ID (string) e.g. 'DF_SDG'
        :param key: your subscription key (string)
        :return: dictionary of metadata key, value pairs
  """
  meta_suffix = 'latest/?references=all&detail=referencepartial'
  meta_url = '{}dataflow/all/{}/{}'.format(base_url, df, meta_suffix)
  headers = {'Ocp-Apim-Subscription-Key': key}
  meta = requests.get(meta_url, headers=headers, verify=False)
  soup = BeautifulSoup(meta.text, 'xml')
  structure = soup.find('Dataflow', attrs= {'id': df})
  meta_dict = {'dataflowId' : df}
  meta_dict['title'] = structure.find('Name').text
  meta_dict['agencyId'] = structure['agencyID']
  meta_dict['version'] = structure['version']
  return meta_dict

dict = basic_metadata(base_url, df, key)
print(dict)
# Output (assuming :param df is 'DF_SDG')
# {'dataflowId': 'DF_SDG', 'title': 'Sustainable Development Indicators', 'agencyId': 'SPC', 'version': '1.0'}
```

## **Plot time series population data \(CSV format\) from PDH .Stat API**

This python script makes a request for CSV-formatted population data over time, for a specified number of countries. It then manipulates the data and plots the results as a time series chart. It is designed to work for any number of countries, over any time period \(within API's constraints\). It could be adapted to handle other time series data.

![](../../../.gitbook/assets/population_time_series.png)

```python
import requests
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# This query requests CSV data with population data for New Caledonia, Fiji, American Samoa, from 1969 to 2015
query_url = 'https://sdd-dotstat-api-gateway.azure-api.net/data/DF_POP_SUM/NC+FJ+AS./all?startPeriod=1969&endPeriod=2015&format=csv'

key = str(input('Enter subscription key: '))
# Or hard-code your key
#key = 'your-key'

def plot_time_series(query_url, key):
  """
  Plot time series population data from a CSV-formatted API GET response
        :param query_url: the API request URL (string)
        :param key: your API subscription key (string)
        :return: time series plot
  """
  headers = {'Ocp-Apim-Subscription-Key': key}
  csv_data = requests.get(query_url, headers=headers, verify=False)
  # Make a dataframe from the csv-formatted text
  csv_df = pd.DataFrame([x.split(',') for x in csv_data.text.split('\n')])
  csv_df.columns = csv_df.iloc[0]
  # Find unique country names
  countries = filter(None, list(csv_df.SPC_AREA.unique()))
  countries = [y for y in countries if (len(y) == 2)]
  # Find the timeline
  time = filter(None, list(csv_df.TIME_PERIOD.unique()))
  time = [z for z in time if (len(z) == 4)]
  # Store max values, for sizing of chart
  maxvals = []
  # Plot data over time for each country
  for code in countries:
      data = csv_df[csv_df['SPC_AREA'] == code]
      vals = [int(m) for m in data['OBS_VALUE'].tolist()]
      maxvals.append(max(vals))
      plt.plot(time, vals, label=code)
  # Set up the plot
  plt.legend()
  plt.title('Population growth over time')
  plt.xlabel('Year')
  plt.ylabel('Population')
  plt.yticks(np.arange(0, max(maxvals)+10000, 100000))

  return plt.show()

plot_time_series(query_url, key)
```

