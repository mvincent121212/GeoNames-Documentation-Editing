---
category: Webservices
url_path: '/findNearbyPostalCodes?'
title: 'Find nearby postal codes'
type: 'GET'

layout: null
---

Finds nearby postal codes to a location by specifying either a longitude and latitude or a postal code/place name.

The default response is in XML. If you want a JSON formatted response, use endpoint `/findNearbyPostalCodesJSON?`.

## Parameters

### Required
Specify one of either lat and lng, postalcode, or placename.


|Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Description 
| :----- | :---------- | :----------- 
|
|lat|Float|The latitude of your location. Ranges from -90 to 90.
|
|lng|Float|The longitude of your location. Ranges from -180 to 180.
|
|postalcode|String|Exception Values: For Canada, Ireland, and Malta use the first letters of the full postal codes. For Argentina, use the 4-digit postal codes used before 1999. For Brazil, only major postal codes ending with 000 and the major code per municipality are available.
|
|placename|String|All fields for values: placename, postal code, country, admin name. Is [urlencoded utf8](https://forum.geonames.org/gforum/posts/list/8.page){:target=_blank}.
|

### Optional

If you specify lat and lng, the following parameters can be used. If you specify postalcode or placename, use the parameters country, radius, or maxRows from the following:

|Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Description 
| :----- | :---------- | :----------- 
|
|radius|Integer|Value is in km. Max value is 30 for free services and 160km for premium services.
|
|maxRows|Integer|Max number of rows returned. Default is 5 rows, max is 500 for free services and 2500 for premium services.
|
|style|String|Values are 'SHORT', 'MEDIUM', 'LONG', and 'FULL'. Specifies the verbosity of the response document. Default is MEDIUM.
|
|country|String|Values are [ISO-3166 country codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes){:target=_blank} i.e. country=FR. Default is all countries. Can occur more than once, i.e. country=FR&country=GP.
|
|localCountry|Boolean|If this value is set to true, the parameter will restrict the search to only the local country of your search and no bordering countries.
|
|isReduced|Boolean| When set to true, only UK outer codes and NL 4-digit codes are returned. Default is false, but default is true for commercial servers.
|

## Request

Below are some example uses of the findNearbyPostalCodes request and their corresponding URL's. Replace the username parameter 'demo' with your GeoNames account username.

|Usage|URL|
|:-----|:----
|
|Find nearby postal codes to a location with latitude 47 and longitude 9.|http://api.geonames.org/findNearbyPostalCodes?lat=47&lng=9&username=demo
|
|Find nearby postal codes to postal code 8775 in Switzerland within 10km.|api.geonames.org/findNearbyPostalCodes?postalcode=8775&country=CH&radius=10&username=demo
|
|Find nearby postal codes to postal code 8775 in Switzerland within 10km. Return a JSON formatted response.|api.geonames.org/findNearbyPostalCodesJSON?postalcode=8775&country=CH&radius=10&username=demo
|

### Example cURL Request
```
curl --location --request GET 'http://api.geonames.org/findNearbyPostalCodes?lat=47&lng=9&username=demo'
```

## Response

### Return Values

The response is equivalent to the response from endpoint `/postalCodeSearch?`

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
    <code>
        <postalcode>8759</postalcode>
        <name>Netstal</name>
        <countryCode>CH</countryCode>
        <lat>47.021</lat>
        <lng>8.97896</lng>
        <adminCode1>GL</adminCode1>
        <adminName1>Kanton Glarus</adminName1>
        <adminCode2>800</adminCode2>
        <adminName2>Glarus</adminName2>
        <adminCode3>1632</adminCode3>
        <adminName3>Glarus</adminName3>
        <distance>2.82791</distance>
    </code>
    <code>
        <postalcode>8750</postalcode>
        <name>Riedern</name>
        <countryCode>CH</countryCode>
        <lat>47.02536</lat>
        <lng>9.0055</lng>
        <adminCode1>GL</adminCode1>
        <adminName1>Kanton Glarus</adminName1>
        <adminCode2>800</adminCode2>
        <adminName2>Glarus</adminName2>
        <adminCode3>1632</adminCode3>
        <adminName3>Glarus</adminName3>
        <distance>2.84987</distance>
    </code>
</geonames>
```


