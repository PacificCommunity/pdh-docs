---
description: >-
  Pacific Data Hub .Stat API. Access macrodata datasets about the Pacific
  region. Data is available in XML, JSON and CSV formats.
---

# Interface

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
An example API request for all of the agency schemes \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/agencyscheme"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:29:21 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=db72583daabc6da0e4d2c1bc99b03cc8e1602844161; expires=Sun, 15-Nov-20 10:29:21 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e3119271ed3e9bf-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d28e0c6d0000e9bf2db16000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11299</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:29:21.2419081+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:OrganisationSchemes>
      <structure:AgencyScheme id="AGENCIES" agencyID="SPC" version="1.0" isFinal="false">
        <common:Name xml:lang="en">SPC agency scheme</common:Name>
        <structure:Agency id="SPC">
          <common:Name xml:lang="en">Pacific Community (SPC)</common:Name>
          <common:Name xml:lang="fr">Communauté du Pacifique (CPS)</common:Name>
        </structure:Agency>
      </structure:AgencyScheme>
    </structure:OrganisationSchemes>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for the currencies category \(CAT\_CURRENCIES\) used by dataflows \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/categorisation/SPC/CAT_CURRENCIES"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:35:42 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d500d33b55d0c10297ba7dfceedc660bd1602844542; expires=Sun, 15-Nov-20 10:35:42 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e312278b818329b-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d293df750000329b46976000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11306</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:35:42.9540952+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:Categorisations>
      <structure:Categorisation id="CAT_CURRENCIES" agencyID="SPC" version="2.0" isFinal="false">
        <common:Name xml:lang="en">Categorisation for the Currencies dataflow</common:Name>
        <structure:Source>
          <Ref id="DF_CURRENCIES" version="2.0" agencyID="SPC" package="datastructure" class="Dataflow" />
        </structure:Source>
        <structure:Target>
          <Ref id="ECO" maintainableParentID="CAS_COM_TOPIC" maintainableParentVersion="1.0" agencyID="SPC" package="categoryscheme" class="Category" />
        </structure:Target>
      </structure:Categorisation>
    </structure:Categorisations>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for all category schemes \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/categoryscheme"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:38:25 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d70f61bc721dfb8d40bcaadbb1ff2b1281602844705; expires=Sun, 15-Nov-20 10:38:25 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e31266fb85532a4-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d29659d7000032a46a2a7000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11309</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:38:25.3660767+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:CategorySchemes>
      <structure:CategoryScheme id="CAS_COM_DEV" agencyID="SPC" version="1.0" isFinal="false">
        <common:Name xml:lang="en">Development indicators</common:Name>
        <common:Name xml:lang="fr">Indicateurs de développement</common:Name>
        <structure:Category id="SDG">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">10</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">10</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Sustainable Development Goals</common:Name>
          <common:Name xml:lang="fr">Objectifs de Développement Durable</common:Name>
        </structure:Category>
        <structure:Category id="NMDI">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">20</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">20</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">National Minimum Development Indicators</common:Name>
          <common:Name xml:lang="fr">Indicateurs Minima du Développement National</common:Name>
        </structure:Category>
      </structure:CategoryScheme>
      <structure:CategoryScheme id="CAS_COM_TOPIC" agencyID="SPC" version="1.0" isFinal="false">
        <common:Name xml:lang="en">Topic</common:Name>
        <common:Name xml:lang="fr">Thème</common:Name>
        <structure:Category id="ECO">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">10</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">10</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Economy</common:Name>
          <common:Name xml:lang="fr">Économie</common:Name>
        </structure:Category>
        <structure:Category id="ENV">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">20</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">20</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Environment</common:Name>
          <common:Name xml:lang="fr">Environnement</common:Name>
        </structure:Category>
        <structure:Category id="HEA">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">30</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">30</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Health</common:Name>
          <common:Name xml:lang="fr">Santé</common:Name>
        </structure:Category>
        <structure:Category id="IND">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">40</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">40</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Industry and Services</common:Name>
          <common:Name xml:lang="fr">Industrie et services</common:Name>
        </structure:Category>
        <structure:Category id="POP">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">50</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">50</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Population</common:Name>
          <common:Name xml:lang="fr">Population</common:Name>
        </structure:Category>
        <structure:Category id="SOC">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">60</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">60</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Social</common:Name>
          <common:Name xml:lang="fr">Social</common:Name>
        </structure:Category>
        <structure:Category id="XDO">
          <common:Annotations>
            <common:Annotation>
              <common:AnnotationType>ORDER</common:AnnotationType>
              <common:AnnotationText xml:lang="en">70</common:AnnotationText>
              <common:AnnotationText xml:lang="fr">70</common:AnnotationText>
            </common:Annotation>
          </common:Annotations>
          <common:Name xml:lang="en">Multi-domain</common:Name>
          <common:Name xml:lang="fr">Multi-domaine</common:Name>
        </structure:Category>
      </structure:CategoryScheme>
    </structure:CategorySchemes>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for the codelist for units of measure \(CL\_COM\_UNIT\_MEASURE\) \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/codelist/SPC/CL_COM_UNIT_MEASURE"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:46:51 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d0b3b57cd40f3e51c8b6a36f754e8add81602845211; expires=Sun, 15-Nov-20 10:46:51 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e3132ca49a9e9b3-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d29e126e0000e9b3a631c000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11312</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:46:51.3717248+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:Codelists>
      <structure:Codelist id="CL_COM_UNIT_MEASURE" agencyID="SPC" version="1.0" isFinal="false">
        <common:Name xml:lang="en">Common codelist for units of measure</common:Name>
        <common:Name xml:lang="fr">Liste de codes commune pour les unités de mesure</common:Name>
        <structure:Code id="N">
          <common:Name xml:lang="en">units</common:Name>
          <common:Name xml:lang="fr">unités</common:Name>
        </structure:Code>
        <structure:Code id="PERCENT">
          <common:Name xml:lang="en">percent</common:Name>
          <common:Name xml:lang="fr">pourcents</common:Name>
        </structure:Code>
        <structure:Code id="KM2">
          <common:Name xml:lang="en">square kilometre</common:Name>
          <common:Name xml:lang="fr">kilomètre carré</common:Name>
        </structure:Code>
        <structure:Code id="POP_KM2">
          <common:Name xml:lang="en">persons per square kilometre</common:Name>
          <common:Name xml:lang="fr">personnes par kilomètre carré</common:Name>
        </structure:Code>
        <structure:Code id="RATIO_POP">
          <common:Name xml:lang="en">ratio to total population</common:Name>
          <common:Name xml:lang="fr">rapport à la population totale</common:Name>
        </structure:Code>
        <structure:Code id="INDEX">
          <common:Name xml:lang="en">index</common:Name>
          <common:Name xml:lang="fr">indice</common:Name>
        </structure:Code>
        <structure:Code id="PER_100000_LIVE_BIRTHS">
          <common:Name xml:lang="en">per 100,000 live births</common:Name>
          <common:Name xml:lang="fr">pour 100 000 naissances vivantes</common:Name>
        </structure:Code>
        <structure:Code id="PER_100000_POP">
          <common:Name xml:lang="en">per 100,000 population</common:Name>
          <common:Name xml:lang="fr">pour 100 000 habitants</common:Name>
        </structure:Code>
        <structure:Code id="PER_1000_POP">
          <common:Name xml:lang="en">per 1,000 population</common:Name>
          <common:Name xml:lang="fr">pour 1000 habitants</common:Name>
        </structure:Code>
        <structure:Code id="LITRES_PURE_ALCOHOL">
          <common:Name xml:lang="en">litres pure alcohol</common:Name>
          <common:Name xml:lang="fr">litres d'alcool pur</common:Name>
        </structure:Code>
        <structure:Code id="PER_100_POP">
          <common:Name xml:lang="en">per 100 population</common:Name>
          <common:Name xml:lang="fr">pour 100 habitants</common:Name>
        </structure:Code>
        <structure:Code id="USD_MILLIONS">
          <common:Name xml:lang="en">usd in millions</common:Name>
          <common:Name xml:lang="fr">usd en millions</common:Name>
        </structure:Code>
        <structure:Code id="USD">
          <common:Name xml:lang="en">USD</common:Name>
          <common:Name xml:lang="fr">USD</common:Name>
        </structure:Code>
        <structure:Code id="T">
          <common:Name xml:lang="en">metric tons</common:Name>
          <common:Name xml:lang="fr">tonnes métriques</common:Name>
        </structure:Code>
        <structure:Code id="CUR_LCU">
          <common:Name xml:lang="en">local currency</common:Name>
          <common:Name xml:lang="fr">monnaie locale</common:Name>
        </structure:Code>
        <structure:Code id="USDBBL">
          <common:Name xml:lang="en">$/bbl</common:Name>
          <common:Name xml:lang="fr">$/bbl</common:Name>
        </structure:Code>
        <structure:Code id="USDMT">
          <common:Name xml:lang="en">$/mt</common:Name>
          <common:Name xml:lang="fr">$/mt</common:Name>
        </structure:Code>
        <structure:Code id="USDMMBTU">
          <common:Name xml:lang="en">$/mmbtu</common:Name>
          <common:Name xml:lang="fr">$/mmbtu</common:Name>
        </structure:Code>
        <structure:Code id="BASE2010">
          <common:Name xml:lang="en">2010=100</common:Name>
          <common:Name xml:lang="fr">2010=100</common:Name>
        </structure:Code>
        <structure:Code id="USDKG">
          <common:Name xml:lang="en">$/kg</common:Name>
          <common:Name xml:lang="fr">$/kg</common:Name>
        </structure:Code>
        <structure:Code id="USDCM">
          <common:Name xml:lang="en">$/cubic meter</common:Name>
          <common:Name xml:lang="fr">$/cubic meter</common:Name>
        </structure:Code>
        <structure:Code id="USHSHEET">
          <common:Name xml:lang="en">¢/sheet</common:Name>
          <common:Name xml:lang="fr">¢/sheet</common:Name>
        </structure:Code>
        <structure:Code id="USDDMTU">
          <common:Name xml:lang="en">$/dmtu</common:Name>
          <common:Name xml:lang="fr">$/dmtu</common:Name>
        </structure:Code>
        <structure:Code id="USDTROYOZ">
          <common:Name xml:lang="en">$/troy oz</common:Name>
          <common:Name xml:lang="fr">$/troy oz</common:Name>
        </structure:Code>
        <structure:Code id="BASE2005">
          <common:Name xml:lang="en">2005=100</common:Name>
          <common:Name xml:lang="fr">2005=100</common:Name>
        </structure:Code>
        <structure:Code id="CENTSKG">
          <common:Name xml:lang="en">cents/kg</common:Name>
          <common:Name xml:lang="fr">cents/kg</common:Name>
        </structure:Code>
        <structure:Code id="NZD">
          <common:Name xml:lang="en">New Zealand Dollar</common:Name>
          <common:Name xml:lang="fr">Dollar néo-zélandais</common:Name>
        </structure:Code>
        <structure:Code id="FJD">
          <common:Name xml:lang="en">Fiji Dollar</common:Name>
          <common:Name xml:lang="fr">Dollar fidjien</common:Name>
        </structure:Code>
        <structure:Code id="AUD">
          <common:Name xml:lang="en">Australian Dollar</common:Name>
          <common:Name xml:lang="fr">Dollar australien</common:Name>
        </structure:Code>
        <structure:Code id="XPF">
          <common:Name xml:lang="en">CFP Franc</common:Name>
          <common:Name xml:lang="fr">Franc CFP</common:Name>
        </structure:Code>
        <structure:Code id="PGK">
          <common:Name xml:lang="en">Kina</common:Name>
          <common:Name xml:lang="fr">Kina</common:Name>
        </structure:Code>
        <structure:Code id="SBD">
          <common:Name xml:lang="en">Solomon Islands Dollar</common:Name>
          <common:Name xml:lang="fr">Dollar des Îles Salomon</common:Name>
        </structure:Code>
        <structure:Code id="TOP">
          <common:Name xml:lang="en">Pa’anga</common:Name>
          <common:Name xml:lang="fr">Pa’anga</common:Name>
        </structure:Code>
        <structure:Code id="VUV">
          <common:Name xml:lang="en">Vatu</common:Name>
          <common:Name xml:lang="fr">Vatu</common:Name>
        </structure:Code>
        <structure:Code id="WST">
          <common:Name xml:lang="en">Tala</common:Name>
          <common:Name xml:lang="fr">Tala</common:Name>
        </structure:Code>
        <structure:Code id="USD_POP">
          <common:Name xml:lang="en">USD per person</common:Name>
          <common:Name xml:lang="fr">USD par personne</common:Name>
        </structure:Code>
        <structure:Code id="NZD_POP">
          <common:Name xml:lang="en">New Zealand Dollar per person</common:Name>
          <common:Name xml:lang="fr">Dollar néo-zélandais par personne</common:Name>
        </structure:Code>
        <structure:Code id="FJD_POP">
          <common:Name xml:lang="en">Fiji Dollar per person</common:Name>
          <common:Name xml:lang="fr">Dollar fidjien par personne</common:Name>
        </structure:Code>
        <structure:Code id="AUD_POP">
          <common:Name xml:lang="en">Australian Dollar per person</common:Name>
          <common:Name xml:lang="fr">Dollar australien par personne</common:Name>
        </structure:Code>
        <structure:Code id="XPF_POP">
          <common:Name xml:lang="en">CFP Franc per person</common:Name>
          <common:Name xml:lang="fr">Franc CFP par personne</common:Name>
        </structure:Code>
        <structure:Code id="PGK_POP">
          <common:Name xml:lang="en">Kina per person</common:Name>
          <common:Name xml:lang="fr">Kina par personne</common:Name>
        </structure:Code>
        <structure:Code id="SBD_POP">
          <common:Name xml:lang="en">Solomon Islands Dollar per person</common:Name>
          <common:Name xml:lang="fr">Dollar des Îles Salomon par personne</common:Name>
        </structure:Code>
        <structure:Code id="TOP_POP">
          <common:Name xml:lang="en">Pa’anga per person</common:Name>
          <common:Name xml:lang="fr">Pa’anga par personne</common:Name>
        </structure:Code>
        <structure:Code id="VUV_POP">
          <common:Name xml:lang="en">Vatu per person</common:Name>
          <common:Name xml:lang="fr">Vatu par personne</common:Name>
        </structure:Code>
        <structure:Code id="WST_POP">
          <common:Name xml:lang="en">Tala per person</common:Name>
          <common:Name xml:lang="fr">Tala par personne</common:Name>
        </structure:Code>
        <structure:Code id="GY">
          <common:Name xml:lang="en">Growth Rate, Over 1 Year</common:Name>
          <common:Name xml:lang="fr">Taux de croissance, sur 1 an</common:Name>
        </structure:Code>
        <structure:Code id="USD_R_POP">
          <common:Name xml:lang="en">Per Capita, US $, Exchange Rates Converted</common:Name>
          <common:Name xml:lang="fr">Par habitant, US $, taux de change convertis</common:Name>
        </structure:Code>
        <structure:Code id="PERCENT_GDP">
          <common:Name xml:lang="en">As a % of GDP</common:Name>
          <common:Name xml:lang="fr">En% du PIB</common:Name>
        </structure:Code>
        <structure:Code id="YR">
          <common:Name xml:lang="en">Years</common:Name>
          <common:Name xml:lang="fr">Années</common:Name>
        </structure:Code>
        <structure:Code id="PER_1000_LIVE_BIRTHS">
          <common:Name xml:lang="en">per 1,000 live births</common:Name>
          <common:Name xml:lang="fr">pour 1000 naissances vivantes</common:Name>
        </structure:Code>
        <structure:Code id="RF">
          <common:Name xml:lang="en">Relative frequency (% of total)</common:Name>
          <common:Name xml:lang="fr">Fréquence relative (% du total)</common:Name>
        </structure:Code>
        <structure:Code id="g">
          <common:Name xml:lang="en">g</common:Name>
          <common:Name xml:lang="fr">g</common:Name>
        </structure:Code>
        <structure:Code id="kcal">
          <common:Name xml:lang="en">kcal</common:Name>
          <common:Name xml:lang="fr">kcal</common:Name>
        </structure:Code>
        <structure:Code id="kj">
          <common:Name xml:lang="en">kj</common:Name>
          <common:Name xml:lang="fr">kj</common:Name>
        </structure:Code>
        <structure:Code id="mg">
          <common:Name xml:lang="en">mg</common:Name>
          <common:Name xml:lang="fr">mg</common:Name>
        </structure:Code>
        <structure:Code id="YEAR">
          <common:Name xml:lang="en">years</common:Name>
          <common:Name xml:lang="fr">années</common:Name>
        </structure:Code>
        <structure:Code id="BOOL">
          <common:Name xml:lang="en">Boolean or binary measure</common:Name>
          <common:Name xml:lang="fr">Mesure booléenne ou binaire</common:Name>
        </structure:Code>
        <structure:Code id="CON_USD">
          <common:Name xml:lang="en">Constant USD</common:Name>
          <common:Name xml:lang="fr">USD constant</common:Name>
        </structure:Code>
        <structure:Code id="HA">
          <common:Name xml:lang="en">Hectares</common:Name>
          <common:Name xml:lang="fr">Hectares</common:Name>
        </structure:Code>
        <structure:Code id="MJ_PER_GDP_CON_PPP_USD">
          <common:Name xml:lang="en">Megajoules per USD constant PPP GDP</common:Name>
          <common:Name xml:lang="fr">Mégajoules par USD PIB PPA constant</common:Name>
        </structure:Code>
        <structure:Code id="PER_10000_POP">
          <common:Name xml:lang="en">per 10,000 population</common:Name>
          <common:Name xml:lang="fr">pour 10 000 habitants</common:Name>
        </structure:Code>
      </structure:Codelist>
    </structure:Codelists>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for common SPC concepts \(CS\_COMMON\) \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/conceptscheme/SPC/CS_COMMON"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:50:17 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d41d0f238e6803e89c514864a5c216f701602845417; expires=Sun, 15-Nov-20 10:50:17 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e3137d138e732a0-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d2a136c5000032a0f187d000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11315</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:50:17.3118345+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:Concepts>
      <structure:ConceptScheme id="CS_COMMON" agencyID="SPC" version="2.0" isFinal="false">
        <common:Name xml:lang="en">Common concepts for SPC .Stat data</common:Name>
        <common:Name xml:lang="fr">Concepts communs pour les données .Stat de la CPS</common:Name>
        <structure:Concept id="TIME_PERIOD">
          <common:Name xml:lang="en">Time</common:Name>
          <common:Name xml:lang="fr">Période</common:Name>
        </structure:Concept>
        <structure:Concept id="FREQ">
          <common:Name xml:lang="en">Frequency</common:Name>
          <common:Name xml:lang="fr">Fréquence</common:Name>
        </structure:Concept>
        <structure:Concept id="OBS_VALUE">
          <common:Name xml:lang="en">Observation value</common:Name>
          <common:Name xml:lang="fr">Valeur observée</common:Name>
        </structure:Concept>
        <structure:Concept id="OBS_SATUS">
          <common:Name xml:lang="en">Observation Status</common:Name>
          <common:Name xml:lang="fr">Statut de l'observation</common:Name>
        </structure:Concept>
        <structure:Concept id="CONF_STATUS">
          <common:Name xml:lang="en">Confidentiality status</common:Name>
          <common:Name xml:lang="fr">Confidentialité</common:Name>
        </structure:Concept>
        <structure:Concept id="UNIT_MEASURE">
          <common:Name xml:lang="en">Unit of measure</common:Name>
          <common:Name xml:lang="fr">Unité de mesure</common:Name>
        </structure:Concept>
        <structure:Concept id="UNIT_MULT">
          <common:Name xml:lang="en">Unit multiplier</common:Name>
          <common:Name xml:lang="fr">Multiplicateur d'unités</common:Name>
        </structure:Concept>
        <structure:Concept id="COMMENT">
          <common:Name xml:lang="en">Comment</common:Name>
          <common:Name xml:lang="fr">Commentaire</common:Name>
        </structure:Concept>
        <structure:Concept id="DECIMALS">
          <common:Name xml:lang="en">Decimals</common:Name>
          <common:Name xml:lang="fr">Décimales</common:Name>
        </structure:Concept>
        <structure:Concept id="GEO_AREA">
          <common:Name xml:lang="en">Geographical area</common:Name>
          <common:Name xml:lang="fr">Zone géographique</common:Name>
        </structure:Concept>
        <structure:Concept id="GEO_PICT">
          <common:Name xml:lang="en">Pacific Island Countries and territories</common:Name>
          <common:Name xml:lang="fr">Pays et territoires insulaires du Pacifique</common:Name>
        </structure:Concept>
        <structure:Concept id="SEX">
          <common:Name xml:lang="en">Sex</common:Name>
          <common:Name xml:lang="fr">Sexe</common:Name>
        </structure:Concept>
        <structure:Concept id="AGE">
          <common:Name xml:lang="en">Age</common:Name>
          <common:Name xml:lang="fr">Âge</common:Name>
        </structure:Concept>
        <structure:Concept id="CURRENCY">
          <common:Name xml:lang="en">Currency</common:Name>
          <common:Name xml:lang="fr">Devise</common:Name>
        </structure:Concept>
        <structure:Concept id="DATA_SOURCE">
          <common:Name xml:lang="en">Data source</common:Name>
          <common:Name xml:lang="fr">Source de données</common:Name>
        </structure:Concept>
        <structure:Concept id="INDICATOR">
          <common:Name xml:lang="en">Indicator</common:Name>
          <common:Name xml:lang="fr">Indicateur</common:Name>
        </structure:Concept>
        <structure:Concept id="COMMODITY">
          <common:Name xml:lang="en">Commodity</common:Name>
          <common:Name xml:lang="fr">Marchandise</common:Name>
        </structure:Concept>
        <structure:Concept id="URBANIZATION">
          <common:Name xml:lang="en">Urbanization</common:Name>
          <common:Name xml:lang="fr">Urbanisation</common:Name>
        </structure:Concept>
        <structure:Concept id="EDUCATION">
          <common:Name xml:lang="en">Education level</common:Name>
          <common:Name xml:lang="fr">Niveau d'éducation</common:Name>
        </structure:Concept>
        <structure:Concept id="OCCUPATION">
          <common:Name xml:lang="en">Occupation</common:Name>
          <common:Name xml:lang="fr">Profession</common:Name>
        </structure:Concept>
        <structure:Concept id="DISABILITY">
          <common:Name xml:lang="en">Disability</common:Name>
          <common:Name xml:lang="fr">Invalidité</common:Name>
        </structure:Concept>
        <structure:Concept id="INCOME">
          <common:Name xml:lang="en">Income</common:Name>
          <common:Name xml:lang="fr">Revenu</common:Name>
        </structure:Concept>
        <structure:Concept id="COMPOSITE_BREAKDOWN">
          <common:Name xml:lang="en">Composite breakdown</common:Name>
          <common:Name xml:lang="fr">Ventilation composite</common:Name>
        </structure:Concept>
        <structure:Concept id="ECONOMIC_SECTOR">
          <common:Name xml:lang="en">Economic sector</common:Name>
          <common:Name xml:lang="fr">Secteur économique</common:Name>
        </structure:Concept>
        <structure:Concept id="LABOUR_FORCE_STATUS">
          <common:Name xml:lang="en">Labour force status</common:Name>
          <common:Name xml:lang="fr">Statut d'activité professionnelle</common:Name>
        </structure:Concept>
        <structure:Concept id="EMPLOYMENT_STATUS">
          <common:Name xml:lang="en">Employment status</common:Name>
          <common:Name xml:lang="fr">Statut d'emploi</common:Name>
        </structure:Concept>
        <structure:Concept id="BASE_PER">
          <common:Name xml:lang="en">Base period</common:Name>
          <common:Name xml:lang="fr">Période de base</common:Name>
        </structure:Concept>
        <structure:Concept id="TIME_FORMAT">
          <common:Name xml:lang="en">Time format</common:Name>
          <common:Name xml:lang="fr">Format termporel</common:Name>
        </structure:Concept>
        <structure:Concept id="LABEMP_STATUS">
          <common:Name xml:lang="en">Labour and employment status</common:Name>
          <common:Name xml:lang="fr">Statut d'activité professionnelle et d'emploi</common:Name>
        </structure:Concept>
        <structure:Concept id="BUDGET">
          <common:Name xml:lang="en">Budget</common:Name>
          <common:Name xml:lang="fr">Budget</common:Name>
        </structure:Concept>
      </structure:ConceptScheme>
    </structure:Concepts>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for the list of constraints for the NMDI dataflow \(CON\_NMDI\) \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/contentconstraint/SPC/CON_NMDI"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 10:54:45 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d5897a1c29f59bca34e2c0f1fff906f991602845685; expires=Sun, 15-Nov-20 10:54:45 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e313e5dfbfd32a5-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d2a54ebf000032a5ce1e2000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11318</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T10:54:45.5537897+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:Constraints>
      <structure:ContentConstraint id="CON_NMDI" agencyID="SPC" version="1.0" isFinal="false" type="Allowed">
        <common:Name xml:lang="en">Consraint in list of indicators for NMDI</common:Name>
        <structure:ConstraintAttachment>
          <structure:Dataflow>
            <Ref id="DF_NMDI" version="1.0" agencyID="SPC" package="datastructure" class="Dataflow" />
          </structure:Dataflow>
        </structure:ConstraintAttachment>
        <structure:CubeRegion include="true">
          <common:KeyValue id="GEO_PICT">
            <common:Value>AS</common:Value>
            <common:Value>CK</common:Value>
            <common:Value>FJ</common:Value>
            <common:Value>FM</common:Value>
            <common:Value>GU</common:Value>
            <common:Value>KI</common:Value>
            <common:Value>MH</common:Value>
            <common:Value>MP</common:Value>
            <common:Value>NC</common:Value>
            <common:Value>NR</common:Value>
            <common:Value>NU</common:Value>
            <common:Value>PF</common:Value>
            <common:Value>PG</common:Value>
            <common:Value>PN</common:Value>
            <common:Value>PW</common:Value>
            <common:Value>SB</common:Value>
            <common:Value>TK</common:Value>
            <common:Value>TO</common:Value>
            <common:Value>TV</common:Value>
            <common:Value>VU</common:Value>
            <common:Value>WF</common:Value>
            <common:Value>WS</common:Value>
          </common:KeyValue>
          <common:KeyValue id="INDICATOR">
            <common:Value>AG_LND_FRST</common:Value>
            <common:Value>AG_PRD_ORTIND</common:Value>
            <common:Value>BX_TRF_PWKR</common:Value>
            <common:Value>DC_FTA_TOTAL</common:Value>
            <common:Value>DC_ODA_LDCG</common:Value>
            <common:Value>DC_TOF_INFRAL</common:Value>
            <common:Value>DC_TOF_TRDCMDL</common:Value>
            <common:Value>DC_TRF_TOTDL</common:Value>
            <common:Value>DEV</common:Value>
            <common:Value>DT_TDS_DECT</common:Value>
            <common:Value>EDU</common:Value>
            <common:Value>EG_ACS_ELEC</common:Value>
            <common:Value>EG_FEC_RNEW</common:Value>
            <common:Value>EN_LND_SLUM</common:Value>
            <common:Value>EN_REF_COLDIS</common:Value>
            <common:Value>ER_CBD_ABSCLRHS</common:Value>
            <common:Value>ER_GRF_ANIMKPT</common:Value>
            <common:Value>ER_H2O_FISHFEXP</common:Value>
            <common:Value>ER_MRN_MARIN</common:Value>
            <common:Value>ER_PTD_FRHWTR</common:Value>
            <common:Value>ER_PTD_TERR</common:Value>
            <common:Value>ER_PTD_TOT</common:Value>
            <common:Value>ER_RSK_LST</common:Value>
            <common:Value>FB_BNK_ACCSS</common:Value>
            <common:Value>FIS</common:Value>
            <common:Value>HEA</common:Value>
            <common:Value>IC_GEN_MGTL</common:Value>
            <common:Value>INF</common:Value>
            <common:Value>IT_MOB_2GNTWK</common:Value>
            <common:Value>IT_MOB_OWN</common:Value>
            <common:Value>IT_NET_BBND</common:Value>
            <common:Value>IT_USE_ii99</common:Value>
            <common:Value>NMDI0001</common:Value>
            <common:Value>NMDI0002</common:Value>
            <common:Value>NMDI0003</common:Value>
            <common:Value>NMDI0004</common:Value>
            <common:Value>NMDI0011</common:Value>
            <common:Value>NMDI0013</common:Value>
            <common:Value>NMDI0014</common:Value>
            <common:Value>NMDI0016</common:Value>
            <common:Value>NMDI0018</common:Value>
            <common:Value>NMDI0019</common:Value>
            <common:Value>NMDI0020</common:Value>
            <common:Value>NMDI0021</common:Value>
            <common:Value>NMDI0022</common:Value>
            <common:Value>NMDI0033</common:Value>
            <common:Value>NMDI0034</common:Value>
            <common:Value>NMDI0035</common:Value>
            <common:Value>NMDI0036</common:Value>
            <common:Value>NMDI0038</common:Value>
            <common:Value>NMDI0047</common:Value>
            <common:Value>NMDI0051</common:Value>
            <common:Value>NMDI0052</common:Value>
            <common:Value>NMDI0054</common:Value>
            <common:Value>NMDI0057</common:Value>
            <common:Value>NMDI0059</common:Value>
            <common:Value>NMDI0081</common:Value>
            <common:Value>NMDI0087</common:Value>
            <common:Value>NMDI0088</common:Value>
            <common:Value>NMDI0091</common:Value>
            <common:Value>NMDI0099</common:Value>
            <common:Value>NMDI0100</common:Value>
            <common:Value>NMDI0102</common:Value>
            <common:Value>NMDI0103</common:Value>
            <common:Value>NMDI0116</common:Value>
            <common:Value>NMDI0118</common:Value>
            <common:Value>NMDI0129</common:Value>
            <common:Value>NMDI0131</common:Value>
            <common:Value>NMDI0132</common:Value>
            <common:Value>NMDI0133</common:Value>
            <common:Value>NMDI0134</common:Value>
            <common:Value>NMDI0137</common:Value>
            <common:Value>NMDI0138</common:Value>
            <common:Value>NMDI0139</common:Value>
            <common:Value>NMDI0145</common:Value>
            <common:Value>NMDI0146</common:Value>
            <common:Value>NMDI0149</common:Value>
            <common:Value>NMDI0165</common:Value>
            <common:Value>NMDI0167</common:Value>
            <common:Value>NMDI0193</common:Value>
            <common:Value>NMDI0225</common:Value>
            <common:Value>NMDI0226</common:Value>
            <common:Value>NMDI0264</common:Value>
            <common:Value>NMDI0265</common:Value>
            <common:Value>NMDI0293</common:Value>
            <common:Value>NMDI0294</common:Value>
            <common:Value>NMDI0295</common:Value>
            <common:Value>NMDI0296</common:Value>
            <common:Value>NMDI0303</common:Value>
            <common:Value>NMDI0419</common:Value>
            <common:Value>NMDI0420</common:Value>
            <common:Value>NMDI0421</common:Value>
            <common:Value>NMDI0426</common:Value>
            <common:Value>NMDI0428</common:Value>
            <common:Value>NMDI0429</common:Value>
            <common:Value>NMDI0431</common:Value>
            <common:Value>NY_GDP_PCAP</common:Value>
            <common:Value>OTH</common:Value>
            <common:Value>POP</common:Value>
            <common:Value>SE_ACS_ELECT</common:Value>
            <common:Value>SE_ADT_EDUCTRN</common:Value>
            <common:Value>SE_GC_TCAQ</common:Value>
            <common:Value>SE_PRE_PARTN</common:Value>
            <common:Value>SE_TOT_GPI</common:Value>
            <common:Value>SE_TOT_PRFL</common:Value>
            <common:Value>SG_DSR_LEGREG</common:Value>
            <common:Value>SG_GEN_PARL</common:Value>
            <common:Value>SG_HAZ_CMRBASEL</common:Value>
            <common:Value>SG_INF_ACCSS</common:Value>
            <common:Value>SG_INT_MBR</common:Value>
            <common:Value>SG_PLN_MSTKSDG</common:Value>
            <common:Value>SG_PLN_PRVNDI</common:Value>
            <common:Value>SG_REG_BRTH</common:Value>
            <common:Value>SG_REG_BRTH90</common:Value>
            <common:Value>SG_STT_CAPTY</common:Value>
            <common:Value>SG_STT_FPOS</common:Value>
            <common:Value>SG_STT_NSDSFDDNR</common:Value>
            <common:Value>SH_ALC_CONSPT</common:Value>
            <common:Value>SH_DTH_NCD</common:Value>
            <common:Value>SH_DYN_IMRT</common:Value>
            <common:Value>SH_DYN_NMRT</common:Value>
            <common:Value>SH_FPL_INFM</common:Value>
            <common:Value>SH_FPL_MTMM</common:Value>
            <common:Value>SH_H2O_SAFE</common:Value>
            <common:Value>SH_IHR_CAPPRD</common:Value>
            <common:Value>SH_MED_DEN</common:Value>
            <common:Value>SH_PRV_SMOK</common:Value>
            <common:Value>SH_SAN_DEFECT</common:Value>
            <common:Value>SH_STA_BRTC</common:Value>
            <common:Value>SH_STA_MALR</common:Value>
            <common:Value>SH_STA_MORT</common:Value>
            <common:Value>SH_STA_STNT</common:Value>
            <common:Value>SH_STA_WASH</common:Value>
            <common:Value>SH_STA_WAST</common:Value>
            <common:Value>SH_TBS_INCD</common:Value>
            <common:Value>SH_TRP_INTVN</common:Value>
            <common:Value>SI_COV_BENFTS</common:Value>
            <common:Value>SI_HEI_TOTL</common:Value>
            <common:Value>SI_POV_DAY1</common:Value>
            <common:Value>SI_POV_NAHC</common:Value>
            <common:Value>SI_RMT_COST</common:Value>
            <common:Value>SL_DOM_TSPD</common:Value>
            <common:Value>SL_EMP_EARN</common:Value>
            <common:Value>SL_EMP_GTOTL</common:Value>
            <common:Value>SL_ISV_IFRM</common:Value>
            <common:Value>SL_TLF_MANF</common:Value>
            <common:Value>SL_TLF_NEET</common:Value>
            <common:Value>SL_TLF_UEM</common:Value>
            <common:Value>SN_ITK_DEFC</common:Value>
            <common:Value>SP_DYN_ADKL</common:Value>
            <common:Value>SP_DYN_MRBF</common:Value>
            <common:Value>SPC_1_2_2</common:Value>
            <common:Value>SPC_1_4_1</common:Value>
            <common:Value>SPC_10_2_1</common:Value>
            <common:Value>SPC_10_7_2</common:Value>
            <common:Value>SPC_11_b_2</common:Value>
            <common:Value>SPC_12_4_2</common:Value>
            <common:Value>SPC_12_5_1</common:Value>
            <common:Value>SPC_12_b_1</common:Value>
            <common:Value>SPC_13_2_1</common:Value>
            <common:Value>SPC_13_3_1</common:Value>
            <common:Value>SPC_13_a_1</common:Value>
            <common:Value>SPC_13_b_1</common:Value>
            <common:Value>SPC_14_1_1</common:Value>
            <common:Value>SPC_14_2_1</common:Value>
            <common:Value>SPC_14_3_1</common:Value>
            <common:Value>SPC_14_6_1</common:Value>
            <common:Value>SPC_14_7_1</common:Value>
            <common:Value>SPC_14_a_1</common:Value>
            <common:Value>SPC_14_b_1</common:Value>
            <common:Value>SPC_15_7_1</common:Value>
            <common:Value>SPC_15_8_1</common:Value>
            <common:Value>SPC_16_1_3</common:Value>
            <common:Value>SPC_16_3_1</common:Value>
            <common:Value>SPC_16_6_1</common:Value>
            <common:Value>SPC_16_7_1</common:Value>
            <common:Value>SPC_16_7_2</common:Value>
            <common:Value>SPC_17_1_1</common:Value>
            <common:Value>SPC_17_1_2</common:Value>
            <common:Value>SPC_17_14_1</common:Value>
            <common:Value>SPC_17_17_1</common:Value>
            <common:Value>SPC_17_3_1</common:Value>
            <common:Value>SPC_17_7_1</common:Value>
            <common:Value>SPC_2_3_2</common:Value>
            <common:Value>SPC_2_4_1</common:Value>
            <common:Value>SPC_3_8_1</common:Value>
            <common:Value>SPC_4_6_1</common:Value>
            <common:Value>SPC_4_7_1</common:Value>
            <common:Value>SPC_5_1_1</common:Value>
            <common:Value>SPC_5_2_2</common:Value>
            <common:Value>SPC_5_a_2</common:Value>
            <common:Value>SPC_5_c_1</common:Value>
            <common:Value>SPC_6_3_1</common:Value>
            <common:Value>SPC_7_a_1</common:Value>
            <common:Value>SPC_8_9_1</common:Value>
            <common:Value>SPC_8_9_2</common:Value>
            <common:Value>VC_DSR_AALG</common:Value>
            <common:Value>VC_DSR_AFFCT</common:Value>
            <common:Value>VC_DSR_MISS</common:Value>
            <common:Value>VC_DSR_MORT</common:Value>
            <common:Value>VC_VAW_MARR</common:Value>
          </common:KeyValue>
        </structure:CubeRegion>
      </structure:ContentConstraint>
    </structure:Constraints>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
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
An example API request for the data structure definition of Commodity Prices \(DSD\_COMMODITY\_PRICES\) \(returned as XML\): `curl -v -X GET "https://stats-nsi-stable.pacificdata.org/rest/datastructure/SPC/DSD_COMMODITY_PRICES"`
{% endapi-method-response-example-description %}

```markup
Date: Fri, 16 Oct 2020 11:01:34 GMT
Content-Type: application/vnd.sdmx.structure+xml; version=2.1; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Set-Cookie: __cfduid=d59a104a71be634615a1cf4fac9207a8a1602846094; expires=Sun, 15-Nov-20 11:01:34 GMT; path=/; domain=.pacificdata.org; HttpOnly; SameSite=Lax
CF-Ray: 5e31485aea5432a1-BNE
Accept-Ranges: values
Cache-Control: no-store,no-cache
Vary: Accept, Accept-Encoding
CF-Cache-Status: DYNAMIC
cf-request-id: 05d2ab8cd1000032a1a2306000000001
Expect-CT: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Pragma: no-cache
Server: cloudflare

<?xml version="1.0" encoding="utf-8"?>
<!--NSI Web Service v7.13.0.0-->
<message:Structure xmlns:message="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/message" xmlns:structure="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/structure" xmlns:common="http://www.sdmx.org/resources/sdmxml/schemas/v2_1/common">
  <message:Header>
    <message:ID>IDREF11321</message:ID>
    <message:Test>false</message:Test>
    <message:Prepared>2020-10-16T11:01:34.6619601+00:00</message:Prepared>
    <message:Sender id="Unknown" />
    <message:Receiver id="Unknown" />
  </message:Header>
  <message:Structures>
    <structure:DataStructures>
      <structure:DataStructure id="DSD_COMMODITY_PRICES" agencyID="SPC" version="1.0" isFinal="false">
        <common:Name xml:lang="en">DSD for commodity prices</common:Name>
        <structure:DataStructureComponents>
          <structure:DimensionList id="DimensionDescriptor">
            <structure:Dimension id="FREQ" position="1">
              <structure:ConceptIdentity>
                <Ref id="FREQ" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:Enumeration>
                  <Ref id="CL_COM_FREQ" version="1.0" agencyID="SPC" package="codelist" class="Codelist" />
                </structure:Enumeration>
              </structure:LocalRepresentation>
            </structure:Dimension>
            <structure:Dimension id="COMMODITY" position="2">
              <structure:ConceptIdentity>
                <Ref id="COMMODITY" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:Enumeration>
                  <Ref id="CL_COMMODITY_PRICES" version="1.0" agencyID="SPC" package="codelist" class="Codelist" />
                </structure:Enumeration>
              </structure:LocalRepresentation>
            </structure:Dimension>
            <structure:Dimension id="INDICATOR" position="3">
              <structure:ConceptIdentity>
                <Ref id="INDICATOR" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:Enumeration>
                  <Ref id="CL_COMMODITY_PRICES_INDICATORS" version="1.0" agencyID="SPC" package="codelist" class="Codelist" />
                </structure:Enumeration>
              </structure:LocalRepresentation>
            </structure:Dimension>
            <structure:TimeDimension id="TIME_PERIOD" position="4">
              <structure:ConceptIdentity>
                <Ref id="TIME_PERIOD" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:TextFormat textType="ObservationalTimePeriod" />
              </structure:LocalRepresentation>
            </structure:TimeDimension>
          </structure:DimensionList>
          <structure:AttributeList id="AttributeDescriptor">
            <structure:Attribute id="DATA_SOURCE" assignmentStatus="Conditional">
              <structure:ConceptIdentity>
                <Ref id="DATA_SOURCE" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:TextFormat textType="String" />
              </structure:LocalRepresentation>
              <structure:AttributeRelationship>
                <structure:Dimension>
                  <Ref id="FREQ" />
                </structure:Dimension>
                <structure:Dimension>
                  <Ref id="COMMODITY" />
                </structure:Dimension>
                <structure:Dimension>
                  <Ref id="INDICATOR" />
                </structure:Dimension>
              </structure:AttributeRelationship>
            </structure:Attribute>
            <structure:Attribute id="UNIT_MEASURE" assignmentStatus="Conditional">
              <structure:ConceptIdentity>
                <Ref id="UNIT_MEASURE" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:Enumeration>
                  <Ref id="CL_COM_UNIT_MEASURE" version="1.0" agencyID="SPC" package="codelist" class="Codelist" />
                </structure:Enumeration>
              </structure:LocalRepresentation>
              <structure:AttributeRelationship>
                <structure:Dimension>
                  <Ref id="COMMODITY" />
                </structure:Dimension>
                <structure:Dimension>
                  <Ref id="INDICATOR" />
                </structure:Dimension>
              </structure:AttributeRelationship>
            </structure:Attribute>
            <structure:Attribute id="OBS_COMMENT" assignmentStatus="Conditional">
              <structure:ConceptIdentity>
                <Ref id="COMMENT" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
              <structure:LocalRepresentation>
                <structure:TextFormat textType="String" />
              </structure:LocalRepresentation>
              <structure:AttributeRelationship>
                <structure:PrimaryMeasure>
                  <Ref id="OBS_VALUE" />
                </structure:PrimaryMeasure>
              </structure:AttributeRelationship>
            </structure:Attribute>
          </structure:AttributeList>
          <structure:MeasureList id="MeasureDescriptor">
            <structure:PrimaryMeasure id="OBS_VALUE">
              <structure:ConceptIdentity>
                <Ref id="OBS_VALUE" maintainableParentID="CS_COMMON" maintainableParentVersion="2.0" agencyID="SPC" package="conceptscheme" class="Concept" />
              </structure:ConceptIdentity>
            </structure:PrimaryMeasure>
          </structure:MeasureList>
        </structure:DataStructureComponents>
      </structure:DataStructure>
    </structure:DataStructures>
  </message:Structures>
</message:Structure>* Connection #0 to host stats-nsi-stable.pacificdata.org left intact
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}

{% endhint %}



