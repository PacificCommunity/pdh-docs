# Concepts

## Data structures

In the Pacific Data Hub .Stat API, datasets are specified by a 'data structure.' You can request all available data structures with:

**.../datastructure/SPC/all/?references=none&detail=allstubs**

## Data Flows

The data within a data structure is accessed via a 'dataflow.' One data structure may have multiple dataflows to return different views of the same underlying data. You can request all available dataflows with:

**…/dataflow/SPC/all/?references=none&detail=allstubs**

You can request all dataflows for a specific data structure with:

**…/datastructure/SPC/`structureId`/?references=dataflow&detail=allstubs**

## Codelists and Key

Data structures are built from 'codelists' \(eg. Age Breakdown, Occupation Breakdown\). You can request all codelists for a specific data structure with:

**.../datastructure/SPC/`structureId`/?references=codelist&detail=full**

The codes from a codelist are specified in the `key` API query parameter when requesting data.

**.../data/SPC/`flowId`key/**

## SDMX

The API returns data in SDMX 2.1 \(Statistical Data and Metadata eXchange\). More information about the SDMX standard is available at: [https://sdmx.org](https://sdmx.org/)/

* **SDMX-JSON**: [https://github.com/sdmx-twg/sdmx-json](https://github.com/sdmx-twg/sdmx-json/blob/master/data-message/docs/1-sdmx-json-field-guide.md)
* **SDMX-CSV**: [https://github.com/sdmx-twg/sdmx-csv](https://github.com/sdmx-twg/sdmx-csv/blob/master/data-message/docs/sdmx-csv-field-guide.md)

\*\*\*\*

\*\*\*\*





