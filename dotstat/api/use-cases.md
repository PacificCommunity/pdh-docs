---
description: >-
  The PDH.stat API is an efficient way of accessing Pacific data for a variety
  of use cases.
---

# Use cases

Here we outline a few different types of use cases, so that you can learn how to best leverage the API's functionality for your need.

* [Query building with Data Explorer](use-cases.md#query-building-with-data-explorer)
* [Making a data request](use-cases.md#making-a-data-request)
* [Making a data request for a specific response format](use-cases.md#making-a-data-request-for-a-specific-format)
* [Making a dataflow request \(retrieving information on existing datasets\)](use-cases.md#discovering-dataflows)

## Query building with Data Explorer

If you're making a "one-off" data request about a certain topic, the [PDH.stat Data Explorer](https://stats.pacificdata.org/data-explorer/#/) may be the easiest way to go about it. The intuitive interface allows you to choose a dataset, adjust filters and view the results in a table or chart. You can then produce the API request URL for the actual SDMX data you've accessed. This makes it useful for API query building.

Visit the Data Explorer [here](https://stats.pacificdata.org/data-explorer/#/).

## Making a data request

If you're wanting to access specific data for use in a web application, for producing a "live" chart, or for some other reason, you will want to construct an API request.

In general, you will use the `HTTP GET` method with the `data` endpoint to request a dataflow \(i.e. dataset\). You'll use the API's path and query parameters to define the exact data you want, the time period, the response format, and so on.

The basic template for the API data request URL is defined below.

```text
https://stats-nsi-stable.pacificdata.org/rest/data/flowID/key?queryparameters
```

**The key parameter**

The `key` parameter is the primary way of filtering the exact data you're looking for in a dataflow \(dataset\). The keyword `all` can be used to indicate that all data should be returned. The allowable values for key will change depending on the selected dataflow. In general it is a series of parameters separated by the `.` symbol. Where there are 2 points in a row, it indicates a wildcard for that parameter. To select several values as a parameter, separate them with a `+` sign.

**Note: building the key parameter can be difficult, so the Data Explorer can be used to visually select/filter data, and then see the matching API request URL. This can make key-building much easier. See it** [**here**](https://stats.pacificdata.org/data-explorer/#/)**.**

Examples of `key` parameter for different dataflows:

* `FJ+KI.A`: \(Population dataflow\) Annual population figures for Fiji and Kiribati
* `AG_LND_TOTL..GU.KM2`: \(Pocket Summary dataflow\) Land area in kilometres squared in Guam

**Example: Retrieving population data for two countries**

In this example, we want data on population estimates of Fiji and New Caledonia over time \(1970 to 2018\). The following API request will return the SDMX data we're after:

```text
https://stats-nsi-stable.pacificdata.org/rest/data/DF_POP_PROJ/A.NC+FJ...?startPeriod=1970&endPeriod=2018
```

* Path Parameters
* **data** : indicates that we want to access a given "dataflow"
* **DF\_POP\_PROJ** : `flowID` parameter, uniquely identifies the SDMX "dataflow" \("Population Projections" in this case\)
* **A.NC+FJ...** : `key` parameter, filters results to get Annual data about New Caledonia \(NC\) and Fiji \(FJ\). The points represent "wildcards" for other optional filters \(such as sex, age, and type of population indicator\), meaning that we will get data on all of those options.
* Query Parameters
* **startPeriod=1970** : `startPeriod` parameter, gets data starting from 1970
* **endPeriod=2018** : `endPeriod` parameter, gets data up until 2018

## **Making a data request for a specific format**

Data requests can specify what the response data format should be: json, csv, SDMX etc. In this example, we will get the same population data as in the above example, but we want the response in a JSON format. The following API request will return the JSON data we're after:

```text
https://stats-nsi-stable.pacificdata.org/rest/data/DF_POP_PROJ/A.NC+FJ...?startPeriod=1970&endPeriod=2018&format=jsondata
```

* Path Parameters
* **data** : indicates that we want to access a given "dataflow"
* **DF\_POP\_PROJ** : `flowID` parameter, uniquely identifies the SDMX "dataflow" \("Population Summary" in this case\)
* **A.NC+FJ...** : `key` parameter, filters results to get Annual data about New Caledonia \(NC\) and Fiji \(FJ\). The points represent "wildcards" for other optional filters \(such as sex, age, and type of population indicator\), meaning that we will get data on all of those options.
* Query Parameters
* **startPeriod=1970** : `startPeriod` parameter, gets data starting from 1969
* **endPeriod=2018** : `endPeriod` parameter, gets data up until 2018
* **format=jsondata** : `format` parameter, defines the desired response format: jsondata, csv, genericdata etc.

**Sample Code**

For detailed implementations of API use, see [Sample Code](scode.md).

## Discovering dataflows

Depending on your application's needs, you may want to retrieve information on all existing dataflows. The `HTTP GET` method is used with the `dataflow` endpoint to get this type of information.

The basic template for the API dataflow request URL is defined below.

```text
https://stats-nsi-stable.pacificdata.org/rest/dataflow/agencyID/resourceID/version?queryparameters
```

**Example: Retrieve all dataflows for a specific agency**

In this example, we want to know all existing dataflows maintained by SPC, and details about those dataflows. The following API request will return the SDMX data we're after:

```text
https://stats-nsi-stable.pacificdata.org/rest/dataflow/SPC/all/latest?detail=full
```

* Path Parameters
* **dataflow** : indicates that we want information on dataflows
* **SPC** : `agencyID` parameter, uniquely identifies the agency whose dataflows we want to request
* **all** : `resourceID` parameter, retrieves 'all' resources
* **latest** : `version` parameter, gets the latest version of the resource
* Query Parameters
* **detail=full** : `detail` parameter, determines what sort of information about resources is returned

**Sample Code**

For example code which retrieves all dataflowIds, see [Sample Code](scode.md).

