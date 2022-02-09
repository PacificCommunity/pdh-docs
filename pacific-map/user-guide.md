# User Guide

For an introduction on how to use Pacific map see this video:

{% embed url="https://youtu.be/drsCpfCF27M" %}

### How to get started with PacificMap

* You can access PacificMap either from the Pacific Data Hub main page or by using the URL [https://map.pacificdata.org/](https://map.pacificdata.org).

![](<../.gitbook/assets/image (60).png>)

* In the left-hand panel click the **Explore map data** button to launch the Data Catalogue.

![](<../.gitbook/assets/image (61).png>)

* Browse through the Data Catalogue to find a data set of interest. Click on the title of your preferred data set to get a preview of that data, along with a description and other relevant metadata. To view your selected data set on the main map, click the **Add to the Map** button. The spatial data will be immediately displayed in the map view, and a visual legend for that data will appear in the Data Workbench, located on the left-hand side of the page.

![](<../.gitbook/assets/image (62).png>)

* To locate the loaded data on the map, go to the Data Workbench (positioned on the left-hand side of the page), and click the **Ideal Zoom** link for your desired data set. From here you can also click **About data** to get more information about your selected data set.

![](<../.gitbook/assets/image (63).png>)

* To add additional datasets to the map, simply click **Explore map data** again in the left-hand panel to relaunch the Data Catalogue.
* Zoom manually by moving your mouse pointer over the map and using your mouse wheel to zoom in or out further.
* Click and drag the map to further show the region in which you are interested.
* Click on a feature (that is, directly on a point or line, or within a region) to show data about the individual feature.

### How to find out about a displayed feature

* Click on the feature which is displayed on the map. You can click on points, lines or within regions to see a display of the information available from the spatial data provider for that particular feature.
* For points and lines, you need to click quite accurately to identify the feature. For Regions, clicking on the boundary will give ambiguous results. Click within the region.

![](<../.gitbook/assets/image (64).png>)

Note: You cannot find out further information about the features which are part of the base maps.

### How to configure map settings

* In the top-right corner click on **Map Settings.**

![](<../.gitbook/assets/image (66).png>)

* In the **Map View** section you can select whether to display data using **3D Terrain**, **3D Smooth** or **2D.**

![](<../.gitbook/assets/image (67).png>)

* In the **Base Map** section you can select the most appropriate option for the type of dataset you are working with.

![](<../.gitbook/assets/image (69).png>)

* The **Image Optimisation** slide control will help you to prioritize between quality or performance. In cases where yourcomputer is not powerful enough or the bandwidth is limited, you should move the control to the right in order to make the app faster and more reactive. &#x20;

### How to display my own spreadsheet or spatial data

PacificMap can display two kinds of spreadsheets:

1. Spreadsheets with a **point location (latitude and longitude)** for each row, expressed as two columns: `lat` and `lon`. These will be displayed as points (circles).
2. Spreadsheets where each row refers to a **region** such as a local government area or divisions. Columns must be named according to the [csv-geo-pacific](https://github.com/PacificCommunity/csv-geo-pacific) standard. These will be displayed as regions, highlighting the actual shape of each area.

Spreadsheets must be saved as CSV (comma-separated values).

Standard spatial formats such as GeoJSON and KML are also supported.

There are two ways to load your data:

* Drag your data file onto the PacificMap map view. The format of the data file will be auto-detected.
* Click on the **Upload** button in the left-hand panel. This will launch the Data Catalogue. Select the **My Data** tab at the top of the modal window and follow the provided instructions.

![](<../.gitbook/assets/image (70).png>)

As with datasets which are already part of the Pacific Data Hub, you can click on regions or points to see the available data for a given feature. If the file is a CSV, data from all columns will be shown in the feature information dialogue when you click.

You can also use all of the features of the [Data Workbench](https://map.pacificdata.org/help/data-workbench.html) on your dataset.

To share a view of your data with others, you must first upload the dataset to the Pacific Data Hub Catalogue.&#x20;

### How to share my PacificMap view with others

* In the top right corner click on **Share/Print.**

![](<../.gitbook/assets/image (71).png>)

There are three ways of sharing your map view:

* **Share URL.** Copy the given URL (shown in the first text box) to the clipboard and paste it into an email which you send to the recipient. They can click on it in the email or paste it into their browser to see the same view as you.
* **Print Map.** Generates a static map that can be shared using different formats. Note that this option is the only one that will show data loaded from a local file or URL.
* **Advanced Options.** Create a code to embed the map into a web page.

![](<../.gitbook/assets/image (72).png>)

### How to contribute Data Sets to PacificMap

PacificMap encourages data providers to publish their spatial data using this platform. There are two routes you can take to publishing.

* Any spatial data which is added to [Pacific Data Hub](https://pacificdata.org) using a protocol or format supported by the PacificMap (such as WMS) will automatically appear in the **PacificDataHub** section of the **Data Catalogue** tab for the PacificMap.
* If you require your data set to appear under a separate category of the PacificMap Data Catalogue, you will need to contact  [datahub@spc.int](mailto:datahub@spc.int) for more information.&#x20;

### How to visualize Geographic data stored in the Pacific Data Hub Catalogue&#x20;

Datasets in the Pacific Data Hub containing geographic data will be tagged with the **Geographic data** label

![](<../.gitbook/assets/image (73).png>)

The resources within the dataset containing geographic data come with the **PacificMap** label&#x20;

![](<../.gitbook/assets/image (74).png>)

* When opening one of the files containing geographic data, three map preview options are made available.

![](<../.gitbook/assets/image (75).png>)

* Select **PacificMap** option and the geospatial dataset will be displayed on an embed frame.
* Click on **Open in PacificMap** if you want to open your the dataset on a PacificMap instance independent from the Pacific Data Hub Catalogue

![](<../.gitbook/assets/image (79).png>)
