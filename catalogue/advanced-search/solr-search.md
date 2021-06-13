---
description: Searching for data using Solr search syntax
---

# Solr Search Queries

By enabling the advanced search feature, you can take advantage of Solr's flexible search syntax to analyze your data. For example, you can search for data that contains the terms 'Climate' and 'Financing' in close proximity to each other, or search for data or dates that fall within a specific range.

{% hint style="info" %}
You can add SOLR search syntax search enabling 'Advanced search' under the search bar, then checking the 'Add query syntax to search' check box.
{% endhint %}

![Enbaling advanced search](../../.gitbook/assets/image%20%2889%29.png)

![Enabling SOLR search](../../.gitbook/assets/image%20%2888%29.png)

### Searching for keywords and search phrases

The following are examples of searches for a specific keyword or search phrase.

| Task | Example | Syntax   |
| :--- | :--- | :--- |
| Search for a keyword in a specific field | Search for the keyword `AccessLog` in the title field | `title:AccessLog` |
| Search for a phrase in a specific field | Search for the phrase `Code 1918` in the title field | `title:"Code 1918"` |
| Search for a phrase in one field and a second phrase in another field | Search for `Error 401` in the title field and `Authorization is denied` in the body field | `title:"Error 401" AND body:"Authorization is denied"` |
| Combine searches for multiple phrases or keywords using operators such as AND or OR | Search for `Error 401` in the title field AND `Authorization is denied` in the body field, or search for `Password` in the title field. | `(title:"Error 401" AND body:"Authorization is denied") OR title:Password` |
| Search for a keyword in a specific field, excluding search results with another keyword in the same field | Search for `401` but not `404` in the title field | `title:401 -title:404` |
| Search for data in which a field does not contain a specific value | Search for data where the inStock field is not false | `-inStock:false`  |
| Search for values in a specified range | Search for values from `20020101` to `20030101` in the mod\_date field | `mod_date:[20020101 TO 20030101]` |

### Searching using wildcards

You can use the wildcard character \(\*\) to search for results that are not exact matches. Solr search syntax does not support using a wildcard symbol as the first character of a search.

| Task | Example | Syntax |
| :--- | :--- | :--- |
| Search for words starting with a string of characters | Search for any word that starts with `En` in the title field | `title:En*` |
| Search for words starting and ending with specific strings of characters | Search for any word that starts with `En` and ends with `ed` in the title field | `title:En*ed` |
| Search for values in a field that are less than or equal to a specified numeric value | Search for values in the code field that are less than or equal to 100 | `code:[* TO 100]` |
| Search for values in a field that are greater than or equal to a specified numeric value | Search for values in the code field that are greater than or equal to 100 | `code:[100 TO *]` |
| Search for data that contains a specific field | Find data that includes the message field | `message:[* TO *]` |
| Search for data that does not contain a specific field | Find data that does not have a message field | `-message:[* TO *]` |

#### Searching using additional search options

You can search for terms that are a given number of words away from each other \(called a proximity search\).

| Task | Example | Syntax |
| :--- | :--- | :--- |
| Search for keywords that are a specific number of words away from each other | Search for `log analysis` within 4 words from each other | `"log analysis"~4` |
| Search for transposed words | Search for `log analysis` or `analysis log` | `"log analysis"~1` |

You can approximate a search for multiple keywords \(for example, a search for business AND analysis\) using a search with a large proximity value, such as `"business analysis"~10000000`. For practical purposes, this returns the same group of results as searching for business AND analysis. Unlike a search for business AND analysis, however, results in which business and analysis are closer together are regarded as having a higher search relevance. However, the proximity search also requires more time and system resources to perform.

You can determine which parts of a search query are treated as more important by providing a numeric boost factor. For example, the following query assigns higher importance to matches in the title field than matches in the body field: `(title:MicroStrategy OR title:Analytics)^1.5 (body:Intelligence OR body:Server)`.

For a detailed overview of Solr query syntax, including information about creating queries that take advantage of functions, nested queries, boost factors, and more, see the [official documentation for the query parser syntax](http://lucene.apache.org/java/3_5_0/queryparsersyntax.html). In most cases, Solr uses the standard Lucene query syntax to perform searches. For a list of exceptions, see the [Solr wiki](http://wiki.apache.org/solr/SolrQuerySyntax).

