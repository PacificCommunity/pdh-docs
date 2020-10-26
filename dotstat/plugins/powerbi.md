---
description: Produce reports and dashboards with Power BI using a PowerQuery template
---

# Power BI

![](../../.gitbook/assets/image%20%2850%29.png)

Get the API query corresponding to the data to be imported using the Data Explorer as explained [here](https://app.gitbook.com/@pacific-community-spc/s/pacific-data-hub/dotstat/de#get-api-queries-corresponding-to-the-data-selection).

Create a new data source in Power BI: Data &gt; Get Data &gt; Web &gt; Paste the API query URL

Rename the data source created by right-clicking on it and sleecting "properties"

Replace the PowerQuery with the template provided below:

* Right-click on the data source and select "advanced editor"
* Copy-paste the PowerQuery template below into the editor
* Adapt the "Source" variable from the query \(line 4 below\) by replacing the URL with the one obtained from PDH.stat Data Explorer, save and run

Labels corresponding to codes used in the dataset can be collected using the “structure query” available from the Data Exporer or possibly from the metadata file attached to the dataset, accessible in the Data Explorer has explained [here](https://app.gitbook.com/@pacific-community-spc/s/pacific-data-hub/~/drafts/-MKHVBJLfZGUkh7nHeLU/dotstat/de#link-to-metadata).

```text

let

    Source = Xml.Tables(Web.Contents("https://stats-nsi-stable.pacificdata.org/rest/data/SPC,DF_POCKET,2.0/.A..?startPeriod=2018&endPeriod=2018&dimensionAtObservation=AllDimensions")),

    Table = Source{1}[Table],
    T01 = Table.TransformColumnTypes(Table,{{"Attribute:action", type text}, {"Attribute:structureRef", type text}}),
    T02 = T01{0}[#"http://www.sdmx.org/resources/sdmxml/schemas/v2_1/data/generic"],
    T03 = T02{0}[Obs],
    T04 = Table.AddIndexColumn(T03, "Index", 1, 1),
    T05 = Table.ExpandTableColumn(T04, "ObsValue", {"Attribute:value"}, {"ObsValue.Attribute:value"}),
    T06 = Table.ExpandTableColumn(T05, "ObsKey", {"Value"}, {"ObsKey.Value"}),

    D01 = Table.RemoveColumns(T06,{"ObsValue.Attribute:value", "Attributes"}),
    D02 = Table.ExpandTableColumn(D01, "ObsKey.Value", {"Attribute:id", "Attribute:value"}, {"ObsKey.Value.Attribute:id", "ObsKey.Value.Attribute:value"}),
    DIM = Table.Pivot(D02, List.Distinct(D02[#"ObsKey.Value.Attribute:id"]), "ObsKey.Value.Attribute:id", "ObsKey.Value.Attribute:value"),

    A01 = Table.RemoveColumns(T06,{"ObsKey.Value", "ObsValue.Attribute:value"}),
    A02 = Table.ExpandTableColumn(A01, "Attributes", {"Value"}, {"Attributes.Value"}),
    A03 = Table.ExpandTableColumn(A02, "Attributes.Value", {"Attribute:id", "Attribute:value"}, {"Attributes.Value.Attribute:id", "Attributes.Value.Attribute:value"}),
    A04 = Table.ReplaceValue(A03,null,"",Replacer.ReplaceValue,{"Attributes.Value.Attribute:id"}),
    A05 = Table.Pivot(A03, List.Distinct(A04[#"Attributes.Value.Attribute:id"]), "Attributes.Value.Attribute:id", "Attributes.Value.Attribute:value"),
    ATT = Table.RemoveColumns(A05,{""},1),
    
    O01 = Table.ExpandTableColumn(T05, "ObsKey", {"Value"}, {"ObsKey.Value"}),
    OBS = Table.RemoveColumns(O01,{"ObsKey.Value", "Attributes"}),
    
    DIMOBS01 = Table.NestedJoin(DIM, {"Index"}, OBS, {"Index"}, "OBS", JoinKind.Inner),
    DIMOBS02 = Table.ExpandTableColumn(DIMOBS01, "OBS", {"ObsValue.Attribute:value"}, {"OBS.ObsValue.Attribute:value"}),    
    DIMOBS03 = Table.RenameColumns(DIMOBS02,{{"OBS.ObsValue.Attribute:value", "OBS_VALUE"}}),
    DIMOBS   = Table.ReplaceValue(DIMOBS03,null,"",Replacer.ReplaceValue,{"OBS_VALUE"}),
     
    DIMOBSATT01 = Table.NestedJoin(DIMOBS, {"Index"}, ATT, {"Index"}, "ATT", JoinKind.Inner),
    DIMOBSATT = Table.ExpandTableColumn(DIMOBSATT01, "ATT", {"OBS_COMMENT"}, {"ATT.OBS_COMMENT"}),

    SDMX=Table.TransformColumnTypes(DIMOBSATT,{{"OBS_VALUE", type number}}, "us-EN")

in
    SDMX

```

