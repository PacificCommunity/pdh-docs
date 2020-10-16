---
description: >-
  Pacific Data Hub .Stat API. Access macrodata datasets about the Pacific
  region. Data is available in XML, JSON and CSV formats.
---

# API

## Data queries

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" %}
{% api-method-summary %}
Get data
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves the data observations for a dataflow, based on various filters.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="flow" type="string" required=true %}
The **statistical domain** \(dataflow\) of the data to be returned.  
Examples:  
`DF_SDG`: The ID for Sustainable Development Goals dataflow  
`DF_CPI`: The ID for Consumer Price Index dataflow  
`DF_POCKET`: The ID for Pocket Summary dataflow  
`DF_POP_SUM`: The ID for Population dataflow  
`DF_IMTS`: The ID for International Merchandise Trade Statistics dataflow
{% endapi-method-parameter %}

{% api-method-parameter name="key" type="string" required=true %}
The \(possibly partial\) **key identifying the data to be returned**.  
The keyword `all` can be used to indicate that all data belonging to the specified dataflow and provided by the specified provider must be returned. The allowable values for key will change depending on the selected dataflow. In general, it is a series of parameters separated by the `.` sign. Where there are 2 points in a row, it indicates a "wildcard" for that parameter. To select several values as a parameter, separate them with a `+` sign.
{% endapi-method-parameter %}

{% api-method-parameter name="provider" type="string" required=true %}
The agency maintaining the artefact to be returned \(i.e. `SPC`\).   
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="startPeriod" type="string" required=false %}
The start of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.  
Examples:  
`2000`: Year \(ISO 8601\)  
`2000-01`: Month \(ISO 8601\)  
`2000-01-01`: Date \(ISO 8601\)  
`2000-Q1`: Quarter \(SDMX\)  
`2000-W01`: Week\(SDMX\)
{% endapi-method-parameter %}

{% api-method-parameter name="endPeriod" type="string" required=false %}
The end of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.  
Examples:  
`2000`: Year \(ISO 8601\)  
`2000-01`: Month \(ISO 8601\)  
`2000-01-01`: Date \(ISO 8601\)  
`2000-Q1`: Quarter \(SDMX\)  
`2000-W001`: Week \(SDMX\)
{% endapi-method-parameter %}

{% api-method-parameter name="dimensionAtObservation" type="string" required=false %}
Indicates **how the data should be packaged**.  
The options are:  
`TIME_PERIOD`: A timeseries view  
The ID of any other dimension: A cross-sectional view of the data  
`AllDimensions`: A flat view of the data
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The **amount of information** to be returned.  
Possible options are:  
`full`: All data and documentation  
`dataonly`: Everything except attributes  
`serieskeysonly`: The series keys. This is useful to return the series that match a certain query, without returning the actual data \(e.g. overview page\)  
`nodata`: The series, including attributes and annotations, without observations
{% endapi-method-parameter %}

{% api-method-parameter name="format" type="string" required=false %}
The **data format** to be returned.  
Possible options are:  
`jsondata`  
`csv`  
`genericdata`  
`structure`  
`structurespecificdata`
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept-Language" type="string" required=false %}
Specifies the client's preferred language.
{% endapi-method-parameter %}

{% api-method-parameter name="If-Modified-Since" type="string" required=false %}
Takes a date-time \(RFC3339 format\) as input and returns the content matching the query only if it has changed since the supplied timestamp.
{% endapi-method-parameter %}

{% api-method-parameter name="Accept" type="string" required=false %}
Specifies the format of the API response.  
Possible options are:  
`application/vnd.sdmx.genericdata+xml;version=2.1`: returns SDMX-XML format  
`application/vnd.sdmx.data+json;version=2.1`: returns SDMX-JSON format  
`application/vnd.sdmx.data+csv;version=2.1`: returns SDMX-CSV format
{% endapi-method-parameter %}

{% api-method-parameter name="Accept-Encoding" type="string" required=false %}
Specifies whether the response should be compressed and how.  
`identity` \(the default\) indicates that no compression will be performed.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
An example API request for data on Fiji's population projection \(DF\_POP\_PROJ\) from 2015 to 2020 \(returned as XML\): `curl -v -X GET   
"https://stats-nsi-stable.pacificdata.org/rest/data/SPC,DF_POP_PROJ,3.0/A.FJ._T._T.MIDYEARPOPEST?startPeriod=2015&endPeriod=2020&dimensionAtObservation=AllDimensions"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 05:36:49 GMT
Content-Type: application/vnd.sdmx.genericdata+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d5be5dfdd90fc5940bf06bc555017cc891602826609; expires=Sun, 15-Nov-20 05:36:49 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e2f6ca67a10e9b3-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Content-Disposition: attachment; filename= "SPC-DF_POP_PROJ-3.0-A.FJ._T._T.MIDYEARPOPEST.csv"
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d1823c0b0000e9b3ab23d000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:GenericData xmlns:footer="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message/footer" xmlns:generic="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/data/generic" xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xml="http://www.w3.org/XML/1998/namespace">
<message:Header>
<message:ID>IREF0919307a49a947be8b3b0ad3ed78de70</message:ID>
<message:Test>true</message:Test>
<message:Prepared>2020-10-16T05:36:49</message:Prepared>
<message:Sender id="Stable - DotStat v8" />
<message:Structure structureID="SPC_DF_POP_PROJ_3_0" dimensionAtObservation="AllDimensions">
<common:StructureUsage><Ref agencyID="SPC" id="DF_POP_PROJ" version="3.0" />
</common:StructureUsage>
</message:Structure>
<message:DataSetAction>Information</message:DataSetAction>
</message:Header>
<message:DataSet action="Information" structureRef="SPC_DF_POP_PROJ_3_0">
<generic:Obs><generic:ObsKey><generic:Value id="TIME_PERIOD" value="2017" />
<generic:Value id="FREQ" value="A" />
<generic:Value id="GEO_PICT" value="FJ" />
<generic:Value id="SEX" value="_T" />
<generic:Value id="AGE" value="_T" />
<generic:Value id="INDICATOR" value="MIDYEARPOPEST" />
</generic:ObsKey><generic:ObsValue value="883270" />
<generic:Attributes><generic:Value id="UNIT_MEASURE" value="N" />
<generic:Value id="UNIT_MULTIPLIER" value="0" />
<generic:Value id="OBS_STATUS" value="E" />
<generic:Value id="OBS_COMMENT" value="The difference between this value and the sum of male and female populations is due to rounding errors in lower-level estimates." />
</generic:Attributes></generic:Obs>
<generic:Obs>
<generic:ObsKey>
<generic:Value id="TIME_PERIOD" value="2018" />
<generic:Value id="FREQ" value="A" />
<generic:Value id="GEO_PICT" value="FJ" />
<generic:Value id="SEX" value="_T" />
<generic:Value id="AGE" value="_T" />
<generic:Value id="INDICATOR" value="MIDYEARPOPEST" />
</generic:ObsKey><generic:ObsValue value="887394" />
<generic:Attributes><generic:Value id="UNIT_MEASURE" value="N" />
<generic:Value id="UNIT_MULTIPLIER" value="0" />
<generic:Value id="OBS_STATUS" value="E" />
<generic:Value id="OBS_COMMENT" value="The difference between this value and the sum of male and female populations is due to rounding errors in lower-level estimates." />
</generic:Attributes>
</generic:Obs>
<generic:Obs>
<generic:ObsKey>
<generic:Value id="TIME_PERIOD" value="2019" />
<generic:Value id="FREQ" value="A" />
<generic:Value id="GEO_PICT" value="FJ" />
<generic:Value id="SEX" value="_T" />
<generic:Value id="AGE" value="_T" />
<generic:Value id="INDICATOR" value="MIDYEARPOPEST" />
</generic:ObsKey>
<generic:ObsValue value="891296" />
<generic:Attributes>
<generic:Value id="UNIT_MEASURE" value="N" />
<generic:Value id="UNIT_MULTIPLIER" value="0" />
<generic:Value id="OBS_STATUS" value="F" />
</generic:Attributes>
</generic:Obs>
<generic:Obs>
<generic:ObsKey>
<generic:Value id="TIME_PERIOD" value="2020" />
<generic:Value id="FREQ" value="A" />
<generic:Value id="GEO_PICT" value="FJ" />
<generic:Value id="SEX" value="_T" />
<generic:Value id="AGE" value="_T" />
<generic:Value id="INDICATOR" value="MIDYEARPOPEST" />
</generic:ObsKey><generic:ObsValue value="894961" />
<generic:Attributes><generic:Value id="UNIT_MEASURE" value="N" />
<generic:Value id="UNIT_MULTIPLIER" value="0" />
<generic:Value id="OBS_STATUS" value="F" />
<generic:Value id="OBS_COMMENT" value="The difference between this value and the sum of male and female populations is due to rounding errors in lower-level estimates." />
</generic:Attributes>
</generic:Obs>
</message:DataSet>
</message:GenericData>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
An example response for when the request seeks a dataflow which doesn't exist.
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 05:48:01 GMT
Content-Type: text/plain
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=dca6803be6c4a37ae70765f99c6149ca71602827281; expires=Sun, 15-Nov-20 05:48:01 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e2f7d0b38a5329b-BNE
Cache-Control: no-cache
Expires: -1
CF-Cache-Status: DYNAMIC
cf-request-id: 05d18c7b050000329b542c0000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

Could not find Dataflow and/or DSD related with this data request* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Code samples

{% tabs %}
{% tab title="Curl" %}
```java
@ECHO OFF

curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}?startPeriod={string}&endPeriod={string}&dimensionAtObservation=TIME_PERIOD&detail=full&format={string}"
-H "Accept-Encoding: "
-H "Accept-Language: "
-H "If-Modified-Since: "
-H "Accept: "

--data-ascii "{body}" 
```
{% endtab %}

{% tab title="C\#" %}
```csharp
using System;
using System.Net.Http.Headers;
using System.Text;
using System.Net.Http;
using System.Web;

namespace CSHttpClientSample
{
    static class Program
    {
        static void Main()
        {
            MakeRequest();
            Console.WriteLine("Hit ENTER to exit...");
            Console.ReadLine();
        }
        
        static async void MakeRequest()
        {
            var client = new HttpClient();
            var queryString = HttpUtility.ParseQueryString(string.Empty);

            // Request headers
            client.DefaultRequestHeaders.AcceptEncoding.Add(StringWithQualityHeaderValue.Parse(""));
            client.DefaultRequestHeaders.AcceptLanguage.Add(StringWithQualityHeaderValue.Parse(""));
            client.DefaultRequestHeaders.IfModifiedSince = DateTimeOffset.Parse("");

            client.DefaultRequestHeaders.Accept.Add(MediaTypeWithQualityHeaderValue.Parse(""));
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "{subscription key}");

            // Request parameters
            queryString["startPeriod"] = "{string}";
            queryString["endPeriod"] = "{string}";
            queryString["dimensionAtObservation"] = "TIME_PERIOD";
            queryString["detail"] = "full";
            queryString["format"] = "{string}";
            var uri = "https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}?" + queryString;

            var response = await client.GetAsync(uri);
        }
    }
}	
Pacific Data Hub Home

PDH.Stat Data Explorer
```
{% endtab %}

{% tab title="Java" %}
```java
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
import java.net.URI;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

public class JavaSample 
{
    public static void main(String[] args) 
    {
        HttpClient httpclient = HttpClients.createDefault();

        try
        {
            URIBuilder builder = new URIBuilder("https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}");

            builder.setParameter("startPeriod", "{string}");
            builder.setParameter("endPeriod", "{string}");
            builder.setParameter("dimensionAtObservation", "TIME_PERIOD");
            builder.setParameter("detail", "full");
            builder.setParameter("format", "{string}");

            URI uri = builder.build();
            HttpGet request = new HttpGet(uri);
            request.setHeader("Accept-Encoding", "");
            request.setHeader("Accept-Language", "");
            request.setHeader("If-Modified-Since", "");
            request.setHeader("Accept", "");
            request.setHeader("Ocp-Apim-Subscription-Key", "{subscription key}");


            // Request body
            StringEntity reqEntity = new StringEntity("{body}");
            request.setEntity(reqEntity);

            HttpResponse response = httpclient.execute(request);
            HttpEntity entity = response.getEntity();

            if (entity != null) 
            {
                System.out.println(EntityUtils.toString(entity));
            }
        }
        catch (Exception e)
        {
            System.out.println(e.getMessage());
        }
    }
}

Pacific Data Hub Home

PDH.Stat Data Explorer
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
<!DOCTYPE html>
<html>
<head>
    <title>JSSample</title>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>
</head>
<body>

<script type="text/javascript">
    $(function() {
        var params = {
            // Request parameters
            "startPeriod": "{string}",
            "endPeriod": "{string}",
            "dimensionAtObservation": "TIME_PERIOD",
            "detail": "full",
            "format": "{string}",
        };
      
        $.ajax({
            url: "https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}?" + $.param(params),
            beforeSend: function(xhrObj){
                // Request headers
                xhrObj.setRequestHeader("Accept-Encoding","");
                xhrObj.setRequestHeader("Accept-Language","");
                xhrObj.setRequestHeader("If-Modified-Since","");
                xhrObj.setRequestHeader("Accept","");
                xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key","{subscription key}");
            },
            type: "GET",
            // Request body
            data: "{body}",
        })
        .done(function(data) {
            alert("success");
        })
        .fail(function() {
            alert("error");
        });
    });
</script>
</body>
</html>
```
{% endtab %}

{% tab title="ObjC" %}
```objectivec
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];
    
    NSString* path = @"https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}";
    NSArray* array = @[
                         // Request parameters
                         @"entities=true",
                         @"startPeriod={string}",
                         @"endPeriod={string}",
                         @"dimensionAtObservation=TIME_PERIOD",
                         @"detail=full",
                         @"format={string}",
                      ];
    
    NSString* string = [array componentsJoinedByString:@"&"];
    path = [path stringByAppendingFormat:@"?%@", string];

    NSLog(@"%@", path);

    NSMutableURLRequest* _request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:path]];
    [_request setHTTPMethod:@"GET"];
    // Request headers
    [_request setValue:@"" forHTTPHeaderField:@"Accept-Encoding"];
    [_request setValue:@"" forHTTPHeaderField:@"Accept-Language"];
    [_request setValue:@"" forHTTPHeaderField:@"If-Modified-Since"];
    [_request setValue:@"" forHTTPHeaderField:@"Accept"];
    [_request setValue:@"{subscription key}" forHTTPHeaderField:@"Ocp-Apim-Subscription-Key"];
    // Request body
    [_request setHTTPBody:[@"{body}" dataUsingEncoding:NSUTF8StringEncoding]];
    
    NSURLResponse *response = nil;
    NSError *error = nil;
    NSData* _connectionData = [NSURLConnection sendSynchronousRequest:_request returningResponse:&response error:&error];

    if (nil != error)
    {
        NSLog(@"Error: %@", error);
    }
    else
    {
        NSError* error = nil;
        NSMutableDictionary* json = nil;
        NSString* dataString = [[NSString alloc] initWithData:_connectionData encoding:NSUTF8StringEncoding];
        NSLog(@"%@", dataString);
        
        if (nil != _connectionData)
        {
            json = [NSJSONSerialization JSONObjectWithData:_connectionData options:NSJSONReadingMutableContainers error:&error];
        }
        
        if (error || !json)
        {
            NSLog(@"Could not parse loaded json with error:%@", error);
        }
        
        NSLog(@"%@", json);
        _connectionData = nil;
    }
    
    [pool drain];

    return 0;
}
Pacific Data Hub Home

PDH.Stat Data Explorer
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new Http_Request2('https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Accept-Encoding' => '',
    'Accept-Language' => '',
    'If-Modified-Since' => '',
    'Accept' => '',
    'Ocp-Apim-Subscription-Key' => '{subscription key}',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
    'startPeriod' => '{string}',
    'endPeriod' => '{string}',
    'dimensionAtObservation' => 'TIME_PERIOD',
    'detail' => 'full',
    'format' => '{string}',
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_GET);

// Request body
$request->setBody("{body}");

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>
Pacific Data Hub Home

PDH.Stat Data Explorer
```
{% endtab %}

{% tab title="Python" %}
```python
########### Python 2.7 #############
import httplib, urllib, base64

headers = {
    # Request headers
    'Accept-Encoding': '',
    'Accept-Language': '',
    'If-Modified-Since': '',
    'Accept': '',
    'Ocp-Apim-Subscription-Key': '{subscription key}',
}

params = urllib.urlencode({
    # Request parameters
    'startPeriod': '{string}',
    'endPeriod': '{string}',
    'dimensionAtObservation': 'TIME_PERIOD',
    'detail': 'full',
    'format': '{string}',
})

try:
    conn = httplib.HTTPSConnection('sdd-dotstat-api-gateway.azure-api.net')
    conn.request("GET", "/data/{flow}/{key}/{provider}?%s" % params, "{body}", headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################

########### Python 3.2 #############
import http.client, urllib.request, urllib.parse, urllib.error, base64

headers = {
    # Request headers
    'Accept-Encoding': '',
    'Accept-Language': '',
    'If-Modified-Since': '',
    'Accept': '',
    'Ocp-Apim-Subscription-Key': '{subscription key}',
}

params = urllib.parse.urlencode({
    # Request parameters
    'startPeriod': '{string}',
    'endPeriod': '{string}',
    'dimensionAtObservation': 'TIME_PERIOD',
    'detail': 'full',
    'format': '{string}',
})

try:
    conn = http.client.HTTPSConnection('sdd-dotstat-api-gateway.azure-api.net')
    conn.request("GET", "/data/{flow}/{key}/{provider}?%s" % params, "{body}", headers)
    response = conn.getresponse()
    data = response.read()
    print(data)
    conn.close()
except Exception as e:
    print("[Errno {0}] {1}".format(e.errno, e.strerror))

####################################
Pacific Data Hub Home

PDH.Stat Data Explorer
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require 'net/http'

uri = URI('https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}')

query = URI.encode_www_form({
    # Request parameters
    'startPeriod' => '{string}',
    'endPeriod' => '{string}',
    'dimensionAtObservation' => 'TIME_PERIOD',
    'detail' => 'full',
    'format' => '{string}'
})
if query.length > 0
  if uri.query && uri.query.length > 0
    uri.query += '&' + query
  else
    uri.query = query
  end
end

request = Net::HTTP::Get.new(uri.request_uri)
# Request headers
request['Accept-Encoding'] = ''
# Request headers
request['Accept-Language'] = ''
# Request headers
request['If-Modified-Since'] = ''
# Request headers
request['Accept'] = ''
# Request headers
request['Ocp-Apim-Subscription-Key'] = '{subscription key}'
# Request body
request.body = "{body}"

response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|
    http.request(request)
end

puts response.body
```
{% endtab %}
{% endtabs %}

## Structure queries

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/dataflow/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get dataflow
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves a dataflow \(or many dataflows\), and the associated metadata, including the name, description, and metadata dictionary.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. SPC\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.  
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned.  
Possible values are:  
`none`: No references will be returned  
parents: Returns the artefacts that use the artefact matching the query  
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of `parentsandsiblings` and `descendants`  
In addition, a concrete type of resource may also be used \(e.g. `codelist`\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.  
Possible values are:  
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to `true`  
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information  
`full`: All available information for all artefacts should be returned  
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
An example request for the Consumer Price Index dataflow \(DF\_CPI\), specifying `allstubs` as the detail parameter to return a simplified view of the dataflow: `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/dataflow/SPC/DF_CPI/3.0?references=all&detail=allstubs"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 06:35:59 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=dfd97cf769efd84d0ccd013362e8a84241602830158; expires=Sun, 15-Nov-20 06:35:58 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e2fc34cde53e9bf-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d1b8640b0000e9bf31346000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11282</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T06:35:59.0586706+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:Dataflows>
      <structure:Dataflow id="DF_CPI" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Dataflow/SPC/DF_CPI/3.0">
        <common:Annotations>
          <common:Annotation>
            <common:AnnotationType>NonProductionDataflow</common:AnnotationType>
            <common:AnnotationText xml:lang="en">true</common:AnnotationText>
          </common:Annotation>
        </common:Annotations>
        <common:Name xml:lang="en">Inflation rates</common:Name>
        <common:Name xml:lang="fr">Taux d'inflation</common:Name>
      </structure:Dataflow>
    </structure:Dataflows>
    <structure:CategorySchemes>
      <structure:CategoryScheme id="CAS_COM_TOPIC" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/CategoryScheme/SPC/CAS_COM_TOPIC/1.0">
        <common:Name xml:lang="en">Topic</common:Name>
        <common:Name xml:lang="fr">Thème</common:Name>
      </structure:CategoryScheme>
    </structure:CategorySchemes>
    <structure:Categorisations>
      <structure:Categorisation id="CAT_CPI" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://need/to/changeit">
        <common:Name xml:lang="en">Categorisation of dataflow DF_CPI to category ECO of categrory scheme CAS_COM_TOPIC</common:Name>
      </structure:Categorisation>
    </structure:Categorisations>
    <structure:Codelists>
      <structure:Codelist id="CL_COM_FREQ" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_FREQ/1.0">
        <common:Name xml:lang="en">Common codelist for data frequencies</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour la fréquence des données</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_COM_GEO_PICT" agencyID="SPC" version="2.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_GEO_PICT/2.0">
        <common:Name xml:lang="en">Common hierarchical codelist for PICTs</common:Name>
        <common:Name xml:lang="fr">Liste hiérarchique de codes commune pour les PICTs</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_COM_OBS_STATUS" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_OBS_STATUS/1.0">
        <common:Name xml:lang="en">Common codelist for observation statuses</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour le statut des observations</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_COM_PACCOICOP20" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_PACCOICOP20/1.0">
        <common:Name xml:lang="en">Common codelist for PACCOICOP 2020</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour PACCOICOP 2020</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_COM_UNIT_MEASURE" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_UNIT_MEASURE/1.0">
        <common:Name xml:lang="en">Common codelist for units of measure</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour les unités de mesure</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_COM_UNIT_MULT" agencyID="SPC" version="1.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_COM_UNIT_MULT/1.0">
        <common:Name xml:lang="en">Common codelist for unit multipliers</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour les mulltiplicateurs d'unité</common:Name>
      </structure:Codelist>
      <structure:Codelist id="CL_CPI_INDICATORS" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/Codelist/SPC/CL_CPI_INDICATORS/3.0">
        <common:Name xml:lang="en">Codelist for consumer prices indicators</common:Name>
        <common:Name xml:lang="fr">Liste de codes pour les indicateurs des prix à la consommation</common:Name>
      </structure:Codelist>
    </structure:Codelists>
    <structure:Concepts>
      <structure:ConceptScheme id="CS_COMMON" agencyID="SPC" version="2.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/ConceptScheme/SPC/CS_COMMON/2.0">
        <common:Name xml:lang="en">Common concepts for SPC .Stat data</common:Name>
        <common:Name xml:lang="fr">Concepts communs pour les données .Stat de la CPS</common:Name>
      </structure:ConceptScheme>
    </structure:Concepts>
    <structure:DataStructures>
      <structure:DataStructure id="DSD_CPI" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/DataStructure/SPC/DSD_CPI/3.0">
        <common:Name xml:lang="fr">Définition de la structure des données pour les prix à la consommation</common:Name>
        <common:Name xml:lang="en">Data structure definition for consummer prices</common:Name>
      </structure:DataStructure>
    </structure:DataStructures>
    <structure:Constraints>
      <structure:ContentConstraint id="CON_CPI" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/ContentConstraint/SPC/CON_CPI/3.0" type="Actual">
        <common:Name xml:lang="en">Content constraint for DF_CPI</common:Name>
      </structure:ContentConstraint>
      <structure:ContentConstraint id="CR_A_DF_CPI" agencyID="SPC" version="3.0" isExternalReference="true" isFinal="false" structureURL="http://stats-nsi-stable.pacificdata.org/rest/ContentConstraint/SPC/CR_A_DF_CPI/3.0" type="Actual">
        <common:Name xml:lang="en">Availability (A) for DF_CPI</common:Name>
      </structure:ContentConstraint>
    </structure:Constraints>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/agencyscheme/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get agency schemes
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves information about agencies associated with the .Stat instance. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. SPC\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.   
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).   
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).   
The keyword `all` can be used to return all version of the matching resource.   
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned. Possible values are:  
`none`: No references will be returned   
`parents`: Returns the artefacts that use the artefact matching the query  
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.   
Possible values are:   
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name   
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to `true`   
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information   
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information   
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/categorisation/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get categorisations
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves information about categories used by dataflows.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. SPC\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.   
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).   
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.   
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).   
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned. Possible values are:  
`none`: No references will be returned parents: Returns the artefacts that use the artefact matching the query   
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned   
`descendants`: References of references, up to any level, will be returned   
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.   
Possible values are:   
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name   
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name   
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true   
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information   
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information   
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/categoryscheme/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get category schemes
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves information about category schemes used by dataflows.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. SPC\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.   
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned. Possible values are:  
`none`: No references will be returned parents: Returns the artefacts that use the artefact matching the query   
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts   
`children`: Returns the artefacts referenced by the artefact to be returned   
`descendants`: References of references, up to any level, will be returned   
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.   
Possible values are:   
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name   
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name   
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true   
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information   
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/codelist/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get codelists
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves the codelists associated with a dataflow.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. `SPC`\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.  
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned. Possible values are:   
`none`: No references will be returned parents: Returns the artefacts that use the artefact matching the query   
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.  
Possible values are:  
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true  
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information  
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/conceptscheme/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get concept schemes
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves information about concept schemes used by dataflows.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. `SPC`\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.  
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned.   
Possible values are:  
`none`: No references will be returned  
`parents`: Returns the artefacts that use the artefact matching the query  
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.  
Possible values are:  
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true  
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information  
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/contentconstraint/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get content constraints
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves content constraints for a dataflow.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. `SPC`\).  
It is possible to set more than one agency, using `+` as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.  
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned.   
Possible values are:  
`none`: No references will be returned parents: Returns the artefacts that use the artefact matching the query   
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.  
Possible values are:  
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true  
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information  
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest" path="/datastructure/{agencyID}/{resourceID}/{version}\[?references\]\[&detail\]" %}
{% api-method-summary %}
Get data structures
{% endapi-method-summary %}

{% api-method-description %}
This method retrieves a data structure definition.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="agencyID" type="string" required=false %}
The agency maintaining the artefact to be returned \(i.e. `SPC`\).  
It is possible to set more than one agency, using + as separator \(e.g. `SPC+ECB`\).  
The keyword `all` can be used to indicate that artefacts maintained by any maintenance agency should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="resourceID" type="string" required=false %}
The ID of the artefact to be returned.  
It is possible to set more than one ID, using `+` as separator \(e.g. `CL_FREQ+CL_CONF_STATUS`\).  
The keyword `all` can be used to indicate that any artefact of the specified resource type should be returned.
{% endapi-method-parameter %}

{% api-method-parameter name="version" type="string" required=false %}
The version of the artefact to be returned.  
It is possible to set more than one version, using `+` as separator \(e.g. `1.0+2.1`\).  
The keyword `all` can be used to return all version of the matching resource.  
The keyword `latest` can be used to return the latest production version of the matching resource.
{% endapi-method-parameter %}

{% api-method-parameter name="references" type="string" required=false %}
Instructs the web service to return \(or not return\) the artefacts referenced by the artefact to be returned.   
Possible values are:   
`none`: No references will be returned  
`parents`: Returns the artefacts that use the artefact matching the query  
`parentsandsiblings`: Returns the artefacts that use the artefact matching the query, as well as the artefacts referenced by these artefacts  
`children`: Returns the artefacts referenced by the artefact to be returned  
`descendants`: References of references, up to any level, will be returned  
`all`: The combination of parentsandsiblings and descendants In addition, a concrete type of resource may also be used \(e.g. codelist\)
{% endapi-method-parameter %}

{% api-method-parameter name="detail" type="string" required=false %}
The amount of information to be returned. `referencepartial` is a common value.  
Possible values are:  
`allstubs`: All artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencestubs`: Referenced artefacts should be returned as stubs, containing only identification information, as well as the artefacts' name  
`referencepartial`: Referenced item schemes should only include items used by the artefact to be returned. For example, a concept scheme would only contain the concepts used in a DSD, and its isPartial flag would be set to true  
`allcompletestubs`: All artefacts should be returned as complete stubs, containing identification information, the artefacts' names, descriptions, annotations and isFinal information  
`referencecompletestubs`: Referenced artefacts should be returned as complete stubs, containing identification information, the artefacts' name, description, annotations and isFinal information  
`full`: All available information for all artefacts should be returned
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
See API change history.
{% endhint %}

{% page-ref page="api-history.md" %}



