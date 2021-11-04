---
description: The user-friendly interface to Pacific data
---

# Data Explorer

For an introduction on how to use the Data Explorer see this video :

{% embed url="https://youtu.be/mbY7nAJvQ8c" %}

## Access the PDH.stat Data Explorer

### Via PDH.stat URL

PDH.stat Data Explorer is directly accessible via the following URL:

[https://stats.pacificdata.org/](https://stats.pacificdata.org)

### From the Data Catalogue

The application is also accessible in several ways from the [Data Catalogue](../catalogue/):

A link is available from the "Tools" menu:

![](<../.gitbook/assets/image (27).png>)

PDH Data Catalogue entries have a link to visualize the data in the Data Explorer as a source:

![](<../.gitbook/assets/image (30).png>)

## Find data

### Using predefined topics or textual search

From the welcome page of the Data Explorer data can be searched using predefined topics or using textual search.

![](<../.gitbook/assets/image (31).png>)

Textual search will not only return datasets mentionning serch text in their name or description but also datasets containing occurence of the text in code labels or comments used in the data.

![](<../.gitbook/assets/image (32).png>)

### Faceted search

The research results page implements what is called a "faceted search" allowing search criteria to be refined in a second step using a filtering panel on the left side of the screen.

![](<../.gitbook/assets/image (33).png>)

### From the Data Calalogue

&#x20;PDH.stat data is registered in the Data Catalogue and can also be found using its various different functionnalities. For more information see [dedicated section on the use of the Data Catalogue](../catalogue/).

## View the data

Datasets are first displayed according to a predefined default view.

Filters applied to the default view are visible in the filtering panel on the left side of the screen,&#x20;

![](<../.gitbook/assets/image (35).png>)

A maximum number of observations will be displayed in the Data Explorer to prevserve user experience. If this limit is exceeded the dataset will be trucated and a warning message will be displayed at the top of the table.

![](<../.gitbook/assets/image (36).png>)

## Refine selection

Filters can be managed from the filtering panel on the left of the data table.&#x20;

* The upper side of the panel shows applied filters and allow to easilty clear filters (remove one category, remove all categories selected for a given dimension, clear all filters)
* The lower side of the panel shows available filters and allows defining filters (add or remove individual categories for each dimension)

![](<../.gitbook/assets/image (38).png>)

* To remove a category click on the cross next to the category&#x20;
* To remove all selected categories for a given dimension click on the cross next to the dimension label
* To clear all filters appalied to the dataset click on the cross next to the dimension label

![](<../.gitbook/assets/image (41).png>)

To define filters the lower part of the filtering panel can be used to add or remove categoires from the data selection for each dimension.

![](<../.gitbook/assets/image (42).png>)

* Selectect categories are highlighted,&#x20;
  * Clicking on an unselected category ads it to the selection
  * Clikcing on a selected category removes it from the selection
* When no catgory is selected for a dimension all categories are part of the selection
* The presence of a chevron to the right of the category label indicates that subcategories are available, clicking on the chevron symbol will display sub-categories
* The numbers in the green rectangle next to dimension labels inidicate how many categories are selected from the total number of categories available for the dimension

## Reshape the table

In the Data Explorer dimensions may be displayed as row section, row or column.

![](<../.gitbook/assets/image (43).png>)

Table layout can be customized using the "customize" functionnality available by clicking the appropriate item on ribbon above the data table.

![](<../.gitbook/assets/image (14).png>)

Dimensions can be dragged between columns, row sections and rows.

![](<../.gitbook/assets/image (44).png>)

The new table view is applied once the "apply layout" button is clicked.

At least one dimension must set for rows.

When multiple dimensions are set as columns, row section or row the order in which they are mentionned is significant and corresponds to the order in which they will be nested in the table view. Dimensions can be re-ordred using drag and drop.

## Share by e-mail

A share functionnality allows sending a link to the data currenlty displayed in the Data Explorer per e-mail.

To access this functionnality the "Share" item from the top menu must be clicked.

![](<../.gitbook/assets/image (15).png>)

Data can be shared in 2 ways :

* As a snapshot of data meaning that data will not change even if updated on the site
* As a view of latest data available meaning that latest available data will always be shown when the shared link is clicked

![](<../.gitbook/assets/image (25).png>)

The email address to which a link will be sent must be provided. The first time an email is sent the address must be validated by clicking the "valide email link" in the message received from the Data Explorer.

![](<../.gitbook/assets/image (26).png>)

## Export data

![](<../.gitbook/assets/image (16).png>)

![](<../.gitbook/assets/image (22).png>)

Data can be downloaded as Excel or as CSV, for CSV files it is possible to export only data currently dispalyed considering filters applied or to export the entire dataset whithout any filtering.

## Link to metadata

When a metadata document is available it will be accessible from the "Download" menu by clicking the "Metadata" link next to a blue "i" icon.

![](<../.gitbook/assets/image (16).png>)

![](<../.gitbook/assets/image (21).png>)

Metadata documents comprise a first section with reference metadata (data description, data source, processing, coverage, ...) and a second section with information on the data structure (columns and codelists).

![](<../.gitbook/assets/image (20).png>)

## Get API queries corresponding to the data selection

API queries corresponding to the data view currentlty displayed in the Data Explorer can be accessed using the "More" menu.

![](<../.gitbook/assets/image (18).png>)

Separate API queries are provided for data and for structural metadata.

![](<../.gitbook/assets/image (23).png>)

For more information see [dedicated section on the use of the API](api/).
