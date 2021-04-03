---
category: Webservices
url_path: '/postalCodeSearch?'
title: 'Search by postal code'
type: 'GET'

layout: null
---

Search for a list of places based on a postal code parameter.

The default response is in XML. If you want a JSON formatted response, use endpoint `/postalCodeSearchJSON?`

## Parameters

### Required
One of postalcode or placename are required.


| Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description 
| :----- | :---------- | :----------- 
|
|postalcode|String|Exception Values: For Canada, Ireland, and Malta use the first letters of the full postal codes. For Argentina, use the 4-digit postal codes used before 1999. For Brazil, only major postal codes ending with 000 and the major code per municipality are available.
|
|placename|String|All fields for values: placename, postal code, country, admin name. Is [urlencoded utf8](https://forum.geonames.org/gforum/posts/list/8.page){:target=_blank}.
|

### Optional

| Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description 
| :----- | :---------- | :----------- 
|
|postalcode_startsWith|String|The first characters or letters of a postal code.
|
|placename_startsWith|String|The first characters of a place name.
|
|country|String|Values are [ISO-3166 country codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes){:target=_blank} i.e. country=FR. Default is all countries. Can occur more than once, i.e. country=FR&country=GP.
|
|countryBias|String|Country values listed as a countryBias are listed first in the response.
|
|maxRows|Integer|Max number of rows returned. Default is 100, max is 1000.
|
|style|String|Values are 'SHORT', 'MEDIUM', 'LONG', and 'FULL'. Specifies the verbosity of the response document. Default is MEDIUM.
|
|operator|String|Possible values are 'AND' or 'OR'. The default is 'AND', specifying that all search terms need to match the response. If set to 'OR', not all search terms need to match the response.
|
|charset|String|Defines the encoding used for the response document. Default is 'UTF8'.
|
|isReduced|Boolean| When set to true, only UK outer codes and NL 4-digit codes are returned. Default is false, but default is true for commercial servers.
|
|east,west,north,south|Float|Use this parameter when you want to create a [bounding box](https://wiki.openstreetmap.org/wiki/Bounding_Box){:target="_blank"} for your search results. One example for this parameter is south=0&north=70&west=-120&east=-10.
|

## Request

Below are some example uses of the postalCodeSearch request and their corresponding URL's. Replace the username parameter 'demo' with your GeoNames account username.

|Usage|URL|
|:-----|:----
|
|Find the first ten locations that have the postal code 9011.| http://api.geonames.org/postalCodeSearch?postalcode=9011&maxRows=10&username=demo
|
|Find the first ten locations that have the postal code 9011. List Switzerland locations first.|api.geonames.org/postalCodeSearch?postalcode=9011&username=demo&maxRows=10&countryBias=CH
|
Find the first ten locations that have the postal code 9011. Return a JSON formatted response.|http://api.geonames.org/postalCodeSearchJSON?postalcode=9011&maxRows=10&username=demo
|

### Example cURL Request

```
curl --location --request GET 'api.geonames.org/postalCodeSearch?postalcode=9011&username=mvincent1212&maxRows=10'
```
## Response

### Return Values

All search results are wrapped in the value geonames.

Within geonames, the return values are the following:
* totalResultsCount - the total number of search results found for your query.
* code - each search result is wrapped in this result.

Within each code and with the default style (MEDIUM), the following results are found:
* postalcode
* name
* countryCode
* lat - the latitude of the postal code.
* lng - the longitude of the postal code.
* adminCode1 - the code of an administrative subdivision of the postal code.
* adminName1 - the name corresponding to adminCode1.
* adminCode2 - the code is a subdivision within adminCode1.
* adminName2
* adminCode3 - the code is a subdivision within adminCode2.
* adminName3 

style=SHORT removes all adminCodes and adminNames.

Style=LONG and Style=FULL are equivalent to Style=MEDIUM.

### Example Response

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<geonames>
    <totalResultsCount>62</totalResultsCount>
    <code>
        <postalcode>L-9011</postalcode>
        <name>Ettelbruck</name>
        <countryCode>LU</countryCode>
        <lat>49.84751</lat>
        <lng>6.09171</lng>
        <adminCode1 ISO3166-2="DI">DI</adminCode1>
        <adminName1>Diekirch</adminName1>
        <adminCode2>07</adminCode2>
        <adminName2>Ettelbruck</adminName2>
        <adminCode3/>
        <adminName3/>
    </code>
    <code>
        <postalcode>9011</postalcode>
        <name>Tromsø</name>
        <countryCode>NO</countryCode>
        <lat>69.6489</lat>
        <lng>18.95508</lng>
        <adminCode1 ISO3166-2="54">54</adminCode1>
        <adminName1>Troms og Finnmark</adminName1>
        <adminCode2>5401</adminCode2>
        <adminName2>Tromsø</adminName2>
        <adminCode3/>
        <adminName3/>
    </code>
</geonames>
```
