---
description: >-
  Pacific Data Hub .Stat API. Access macrodata datasets about the Pacific
  region. Data is available in XML, JSON and CSV formats.
---

# API

## Data queries

{% api-method method="get" host="https://sdd-dotstat-api-gateway.azure-api.net/data/{flow}/{key}/{provider}\[?startPeriod\]\[&endPeriod\]\[&dimensionAtObservation\]\[&detail\]\[&format\]" path="" %}
{% api-method-summary %}
Get Data
{% endapi-method-summary %}

{% api-method-description %}
Explain what method does
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="flow" type="string" %}
The **statistical domain** \(aka dataflow\) of the data to be returned.   
Examples:  
`DF_SDG`: The ID for Sustainable Development Goals dataflow  
 `DF_CPI`: The ID for Consumer Price Index dataflow  
 `DF_POCKET`: The ID for Pocket Summary dataflow  
 `DF_POP_SUM`: The ID for Population dataflow  
 `DF_IMTS`: The ID for International Merchandise Trade Statistics dataflow
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Authentication token to track down who is emptying our stocks.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="recipe" type="string" %}
The API will do its best to find a cake matching the provided recipe.
{% endapi-method-parameter %}

{% api-method-parameter name="gluten" type="boolean" %}
Whether the cake should be gluten-free or not.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
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



