---
description: Produce reports and dashboards with Power BI using a PowerQuery template
---

# Power BI

![](<../../.gitbook/assets/image (50).png>)

The OECD has developed a plugin to connect an SDMX data source directly to Power BI, you can find the [documentation to install it here](https://sis-cc.gitlab.io/sdmx-tools/documentation/using-sdmx-powerbi-connector/installation-instructions/). Because this plugin is free and open source, its code is publicly available in its [repository](https://gitlab.com/sis-cc/sdmx-tools/sdmx-power-bi).

To import a dataset you will need the API query corresponding to the data to be imported using the Data Explorer as [explained here](https://docs.pacificdata.org/dotstat/de#get-api-queries-corresponding-to-the-data-selection).

Then you can create a new data source in Power BI: Data > Get Data > SDMX. For importation mode, you can choose between labels only, codes only or both. [(Official plugin documentation)](https://sis-cc.gitlab.io/sdmx-tools/documentation/using-sdmx-powerbi-connector/how-to-use/)

![Plugin configuration window](<../../.gitbook/assets/image (93).png>)

When the data is imported you can transform it with Power Query ("Transform Data" button) to remove useless columns, clean some fields or anything else.

![Imported Data](<../../.gitbook/assets/image (95).png>)

The next screenshot shows a Power Query with the previously imported data, transformed with some steps.

![Data transformations with Power Query](<../../.gitbook/assets/image (96).png>)

Finally, your data is now imported and transformed, you can use it to do some visualisations.

![Visualisation Example](<../../.gitbook/assets/image (97).png>)
