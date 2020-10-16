# Power BI

Copy the data query and replace the bit in yellow below. Then copy all the code and add to a new query window in Power BI. This will extract the dataset. We still need to refine the code a little bit to neaten things up but with a little transformation you should be able to get some great examples.

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

