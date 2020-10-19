---
description: The user-friendly interface to Pacific data
---

# Data Explorer

For an introduction on how to use the Data Explorer see this video :

{% embed url="https://youtu.be/65-ETNfFMBk" %}

## Access the Data Explorer

PDH.stat Data Explorer is accessible direclty using the following URL: [https://stats.pacificdata.org/](https://stats.pacificdata.org/)

The application is also accessible in several ways from the [Data Catalogue](https://pacificdata.org/):

* a link is available from the "Tools" menu:

![](../.gitbook/assets/image%20%2824%29.png)

* PDH Data Catalogue entries have a link to visualize the data in the Data Explorer as a source:

![](../.gitbook/assets/image%20%2841%29.png)

## Find data

From the welcome page of the Data Explorer data can be searched using predefined topics or textual search.

![](../.gitbook/assets/image%20%2843%29.png)

Textual search will not only return datasets mentionning serch text in their name or description but also datasets containing occurence of the text in code labels or comments used in the data.

![](../.gitbook/assets/image%20%2839%29.png)

The research results page implements what is called a "faceted search" allowing search criteria to be refined in a second step using a filtering panel on the left side of the screen.

![](../.gitbook/assets/image%20%2827%29.png)

 PDH.stat data can also be found from the Data Catalogue using its various different functionnalities. For more information see [dedicated section on the use of the Data Catalogue](https://app.gitbook.com/@pacific-community-spc/s/pacific-data-hub/~/drafts/-MJz0A5FvX84FSq5yBMJ/catalogue).

## View the data

Datasets are first displayed according to a predefined default view.

Filters applied to the default view are visible in the filtering panel on the left side of the screen, 

![](../.gitbook/assets/image%20%2820%29.png)

A maximum number of observations will be displayed in the Data Explorer to prevserve user experience. If this limit is exceeded the dataset will be trucated and a warning message will be displayed at the top of the table.

![](../.gitbook/assets/image%20%2819%29.png)

## Refine selection

Filters can be managed from the filtering panel on the left of the data table. 

* The upper side of the panel shows applied filters and allow to easilty clear filtering \(remove one category, remove all categories selected for a given dimension, clear all filters\)
* The lower side of the panel shows available filters and allows defining filters \(add or remove individual categories for each dimension\)

![](../.gitbook/assets/image%20%2829%29.png)

* To remove a category click on the cross next to the catgory 
* To remove all selected category for a given dimension click on the cross next to the dimension label
* To clear all filters click on the cross next to the dimension label

![](../.gitbook/assets/image%20%2821%29.png)

To define filters the lower part of the filtering panel can be used to add or remove categores from the data selection for each dimension.

![](../.gitbook/assets/image%20%2840%29.png)

* Selecting category adds the category to the selection
* Selecting category adds the category to the selection
* When no catgory is selected for a dimension all categories are part of the selection
* The presence of a chevron to the right of the category label indicates that subcategories are available, clickijng the chevron symbol will display sub-categories
* The numbers in the greenrectangle inidcate how many ctagoriesare selected from the total number of categories

## Reshape the table

In the Data Explorer dimensions may be displayed as row section, row or column.

![](../.gitbook/assets/image%20%2823%29.png)

ustomize menu item on the top bar

![](../.gitbook/assets/image%20%2837%29.png)

Dimensions can be dragged between columns, row sections and rows.

![](../.gitbook/assets/image%20%2834%29.png)

The "apply layout" button must be clivked in order to have the new table view applied.

At least one dimension must set for rows.

When multiple dimensions are set as row section, row or column the order in chich they ae mentionned is the order in which they will be nested in the table view. Dimensions can be re-ordred using drag and drop.

## Share by e-mail

A share functionnality allows sending a link to the data currenlty displayed in the Data Explorer per e-mail.

To access this functionnality the "Share" item from the top menu must be clicked.

![](../.gitbook/assets/image%20%2830%29.png)

Data can be shared in 2 ways :

* As a snapshot of data meaning that data will not change even if updated on the site
* As a view of latest data available meaning that latest avaiable data will always be shown when the shared link is clicked

![](../.gitbook/assets/image%20%2816%29.png)

The e-mail address to which a link will be sent must be provided. The first time an email is sent e-mailmust be validated simply b y clicking the "valide email link" in the message received from the Data Explorer.

![](../.gitbook/assets/image%20%2828%29.png)

## Export data

![](../.gitbook/assets/image%20%2815%29.png)

![](../.gitbook/assets/image%20%2844%29.png)

Data can be downloaded as Excel or as CSV, for CSV files a use may choose to export only data currenclty dispalyed by application of filters or to export the entire dataset.

## Link to metadata

When a metadata document it will be availble from the "Download" menu next to a blue "i" icon.

![](../.gitbook/assets/image%20%2815%29.png)

![](../.gitbook/assets/image%20%2817%29.png)

Metadata documents comprise a first section with reference metadata \(data description, data source, processing, coverage, ...\) and a secopnd section providing information on the data structure \(columns and codelists\).

![](../.gitbook/assets/image%20%2835%29.png)

## Get API queries corresponding to the data selection

API queries corresponding to the data view currentlty displayed in the Data Explorer can be accessed using the "More" menu.

![](../.gitbook/assets/image%20%2838%29.png)

Separate API queries are provided for data and for structural metadata.

![](../.gitbook/assets/image%20%2826%29.png)

For more information see [dedicated section on the use of the API](https://app.gitbook.com/@pacific-community-spc/s/pacific-data-hub/~/drafts/-MJz0A5FvX84FSq5yBMJ/dotstat/api).

