# User Guide

For an introduction on how to use Pacific map see this video:

{% embed url="https://youtu.be/drsCpfCF27M" %}

### Introduction

[**PacificMap** ](https://map.pacificdata.org)is typically accessing the data directly from the [**Pacific Data Hub**](https://pacificdata.org/data) catalogue or the organizations who are the custodians of that data.

The **PacificMap:**

* provides easy access to authoritative and other spatial data to government, business and the public from the Pacific
* facilitates the opening of data by international and regional development agencies, research and academic institutions, and local government bodies
* provides an open framework of geospatial data services that supports commercial and community innovation

### How to get started with PacificMap

* You can access PacificMap either from the Pacific Data Hub main page or by using the URL [https://map.pacificdata.org/](https://map.pacificdata.org/).

![](../.gitbook/assets/image%20%2860%29.png)

* In the left-hand panel click the **Explore map data** button to launch the Data Catalogue.

![](../.gitbook/assets/image%20%2874%29.png)

* Browse through the Data Catalogue to find a data set of interest. Click on the title of your preferred data set to get a preview of that data, along with a description and other relevant metadata. To view your selected data set on a larger map, click the **Add to the Map** button. The spatial data will be immediately displayed in the map view, and a visual legend for that data will appear in the Data Workbench, located on the left-hand side of the page.

![](../.gitbook/assets/image%20%2868%29.png)

* To locate the loaded data on the map, go to the Data Workbench \(positioned on the left-hand side of the page\), and click the **Ideal Zoom** link for your desired data set. From here you can also click **About data** to get more information about your selected data set.

![](../.gitbook/assets/image%20%2865%29.png)

* To add additional data sets to the map, simply click **Explare map data** again in the left-hand panel to relaunch the Data Catalogue.
* Zoom manually by moving your mouse pointer over the map and using your mouse wheel to zoom in or out further.
* Click and drag the map to further show the region in which you are interested.
* Click on a feature \(that is, directly on a point or line, or within a region\) to show data about the individual feature.

### How to find out about a displayed feature

* Click on the feature which is displayed on the map. You can click on Points, on Lines or within Regions to see a display of the information available from the spatial data provider for that particular feature.
* For Points and Lines, you need to click quite accurately to identify the feature. For Regions, clicking on the boundary will give ambiguous results. Click within the region.

![](../.gitbook/assets/image%20%2857%29.png)

* You cannot find out further information about the features which are part of the base maps.

### How to configure map settings

* On the top right corner click on **Map Settings.**

![](../.gitbook/assets/image%20%2856%29.png)

* In **Map View** section you can select the way to display data among **3D Terrain**, **3D Smooth** or **2D options.**

![](../.gitbook/assets/image%20%2859%29.png)

* In **Base Map** section you can select the most appropriate option for the type of dataset you are working with.

![](../.gitbook/assets/image%20%2863%29.png)

* The Image Optimisation slide control will help you to prioritize between quality or performance. In cases where the computer is not powerful enough or the bandwidth is limited, you should move the control to the right in order to make the app faster and more reactive.  

### How to display my own spreadsheet or spatial data

PacificMap can display two kinds of spreadsheets:

1. Spreadsheets with a **point location \(latitude and longitude\)** for each row, expressed as two columns: `lat` and `lon`. These will be displayed as points \(circles\).
2. Spreadsheets where each row refers to a **region** such as a local government area or divisions. Columns must be named according to the [csv-geo-pacific](https://github.com/PacificCommunity/csv-geo-pacific) standard. These will be displayed as regions, highlighting the actual shape of each area.

Spreadsheets must be saved as CSV \(comma-separated values\).

Standard spatial formats such as GeoJSON and KML are also supported.

There are two ways to load your data:

* Drag your data file onto the PacificMap map view. The format of the data file will be auto-detected.
* Click on the **Upload** button in the left-hand panel. This will launch the Data Catalogue. Select the **My Data** tab at the top of the modal window and follow the provided instructions.

![](../.gitbook/assets/image%20%2862%29.png)

As for PacificMap data sets, you can click on the regions or points to see the data available for that location. If the file is a CSV file, the data from all columns will be shown in the feature information dialogue when you click.

You can also use all of the features of the [Data Workbench](https://map.pacificdata.org/help/data-workbench.html) on the data you have loaded as well.

To share a view of your data with others, you must first publish it to the web somewhere with a URL, and then load it from there.

### How to share my PacificMap view with others

* In the top right corner click on **Share/Print.**

![](../.gitbook/assets/image%20%2861%29.png)

There are three ways of sharing your map view:

* **Share URL.** Copy the given URL \(shown in the first text box\) to the clipboard and paste it into an email which you send to the recipient. They can click on it in the email or paste it into their browser to see the same view as you.
* **Print Map.** Generates a static map that can be shared using different formats. Note that this option is the only one that will show data loaded from a local file or URL.
* **Advanced Options.** Creates a code to embed the map into an HTML document.

![](../.gitbook/assets/image%20%2873%29.png)

### How to contribute Data Sets to PacificMap

The PacificMap encourages data providers to publish their spatial data using this platform. There are two routes you can take to publishing.

* Any spatial data which is added to [Pacific Data Hub](https://pacificdata.org/) using a protocol or format supported by the PacificMap \(such as WMS\) will automatically appear in the **PacificDataHub** section of the **Data Catalogue** tab for the PacificMap.
* If you require your data set to appear under a separate category of the PacificMap Data Catalogue, you will need to contact the support for PacificMap by emailing to [datahub@spc.int](mailto:datahub@spc.int) for more information. You will need to provide an internet accessible service in a standard protocol to access your data set on the internet and appropriate references must be added to the PacificMap configuration.

### How to visualize Geographic data stored in the Pacific Data Hub Catalogue 

Datasets in the Pacific Data Hub containing geographic data come tagged with the **Geographic data** label

![](../.gitbook/assets/image%20%2866%29.png)

The resources within the dataset containing geographic data come with the **PacificMap** label 

![](../.gitbook/assets/image%20%2867%29.png)

* When opening one of the files containing geographic data, three map preview options are made available.

![](../.gitbook/assets/image%20%2855%29.png)

* Select **PacificMap** option and the geospatial dataset will be displayed on an embed frame.
* Click on **Open in PacificMap** if you want to open your the dataset on a PacificMap instance independent from the Pacific Data Hub Catalogue

![](../.gitbook/assets/image%20%2869%29.png)

