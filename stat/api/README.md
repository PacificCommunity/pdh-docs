---
description: >-
  Pacific Data Hub .Stat API. Access macrodata datasets about the Pacific
  region. Data is available in XML, JSON and CSV formats.
---

# API

## Data queries

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}
Get Data
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
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```
{    "name": "Cake's name",    "recipe": "Cake's recipe name",    "cake": "Binary cake"}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```
{    "message": "Ain't no cake like that."}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
application/vnd.sdmx.genericdata+xml;version=2.1
{% endapi-method-parameter %}
{% endapi-method-headers %}
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

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="endPeriod" type="string" required=false %}
The end of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.
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

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="endPeriod" type="string" required=false %}
The end of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.
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

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="endPeriod" type="string" required=false %}
The end of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.  
Examples:  
`2000`: Year \(ISO 8601\)  
`2000-01`: Month \(ISO 8601\)  
`2000-01-01`: Date \(ISO 8601\)  
`2000-S1`: Semester \(SDMX\)  
`2000-D001`: Day \(SDMX\)
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

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="endPeriod" type="string" required=false %}
The end of the period for which results should be supplied \(inclusive\). Can be expressed using 8601 dates or SDMX reporting periods.  
Examples:  
`2000`: Year \(ISO 8601\)  
`2000-01`: Month \(ISO 8601\)  
`2000-01-01`: Date \(ISO 8601\)  
`2000-S1`: Semester \(SDMX\)  
`2000-D001`: Day \(SDMX\)
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

{% api-method method="get" host="https://stats-nsi-stable.pacificdata.org/rest/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="key" type="string" required=false %}
indicate
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
indicate
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

curl -v -X GET "https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}?startPeriod={string}&endPeriod={string}&dimensionAtObservation=TIME_PERIOD&detail=full&format={string}"
-H "Accept-Encoding: "
-H "Accept-Language: "
-H "If-Modified-Since: "
-H "Accept: "
-H "Ocp-Apim-Subscription-Key: {subscription key}"

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get agency schemes
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get categorisations
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get category schemes
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get codelists
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get concept schemes
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get content constraints
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get data structures
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
Get dataflows
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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



