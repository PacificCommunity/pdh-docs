# User Guide

### How to get started with PacificMap

To launch PacificMap and display some basic data follow these steps.

* Display the PacificMap by using the URL [https://map.pacificdata.org/](https://map.pacificdata.org/).
* In the left-hand panel click the **Add Data** button to launch the Data Catalogue.
* Browse through the Data Catalogue to find a data set of interest. Click on the title of your prefered data set to get a preview of that data, along with a description and other relevant metadata. To view your selected data set on a larger map, click the **Add to the Map** button. The spatial data will be immediately displayed in the map view, and a visual legend for that data will appear in the Data Workbench, located on the left-hand side of the page.
* Note that it may not be immediately obvious where your selected spatial data has loaded on the map if it only covers a small area of the Pacific. To locate the loaded data on the map, go to the Data Workbench \(positioned on the left-hand side of the page\), and click the **Zoom to extent** link for your desired data set. From here you can also click **About this data** to get more information about your selected data set.
* To add additional data sets to the map, simply click **Add Data** again in the left-hand panel to relaunch the Data Catalogue.
* Zoom manually by moving your mouse pointer over the map and using your mouse wheel to zoom in or out further.
* Click and drag the map to further show the region in which you are interested.
* Click on a feature \(that is, directly on a point or line, or within a region\) to show data about the individual feature.

You can perform these steps in any order as required to tune your display of spatial data.

### How to find out about a displayed feature

Click on the feature which is displayed on the map. You can click on Points, on Lines or within Regions to see a display of the information available from the spatial data provider for that particular feature.

For Points and Lines, you need to click quite accurately to identify the feature. For Regions, clicking on the boundary will give ambiguous results. Click within the region.

You cannot find out further information about the features which are part of the base maps.

### How to display my own spreadsheet or spatial data

PacificMap can display two kinds of spreadsheets:

1. Spreadsheets with a **point location \(latitude and longitude\)** for each row, expressed as two columns: `lat` and `lon`. These will be displayed as points \(circles\).
2. Spreadsheets where each row refers to a **region** such as a local government area or divisions. Columns must be named according to the [csv-geo-pacific](https://github.com/PacificCommunity/csv-geo-pacific) standard. These will be displayed as regions, highlighting the actual shape of each area.

Spreadsheets must be saved as CSV \(comma-separated values\).

Other standard spatial data types such as GeoJSON and KML are also supported.

There are two ways to load your data:

* Drag your data file onto the PacificMap map view. The format of the data file will be auto-detected.
* Click on the **Add Data** button in the left-hand panel. This will launch the Data Catalogue. Select the **My Data** tab at the top of the modal window and follow the provided instructions.

As for PacificMap data sets, you can click on the regions or points to see the data available for that location. If the file is a CSV file, the data from all columns will be shown in the feature information dialogue when you click.

You can also use all of the features of the [Data Workbench](https://map.pacificdata.org/help/data-workbench.html) on the data you have loaded as well.

To share a view of your data with others, you must first publish it to the web somewhere with a URL, and then load it from there.

### How to share my PacificMap view with others

There are three ways:

* Click the Share button, copy the given URL \(shown in the first text box\) to the clipboard and paste it into an email which you send to the recipient. They can click on it in the email or paste it into their browser to see the same view as you.
* Click the Share button, copy the HTML fragment \(shown in the second text box\) and paste it into an HTML file, which you then make available to the recipients. When the recipients display your web page, they will see the PacificMap view within that web page.
* Take a screenshot and email it as an image \(see your OS instructions on how to take a screenshot\). This will share all information, even if loaded from a local file or URL.

**Note that only the third method will show the data you have loaded from a local file**.

### How to contribute Data Sets to PacificMap

The PacificMap encourages data providers to publish their spatial data using this platform. There are two routes you can take to publishing.

* Any spatial data which is added to [PacificDataHub](https://pacificdata.org/) using a protocol or format supported by the PacificMap \(such as WMS\) will automatically appear in the **PacificDataHub** section of the **Data Catalogue** tab for the PacificMap.
* If you require your data set to appear under a separate category of the PacificMap Data Catalogue, you will need to contact the support for PacificMap by emailing to [datahub@spc.int](mailto:datahub@spc.int) for more information. You will need to provide an internet accessible service in a standard protocol to access your data set on the internet and appropriate references must be added to the PacificMap configuration.

