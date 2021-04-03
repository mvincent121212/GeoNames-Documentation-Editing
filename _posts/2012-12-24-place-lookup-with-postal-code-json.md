---
category: Webservices
url_path: '/postalCodeLookupJSON?'
title: 'Postal code lookup in JSON'
type: 'GET'

layout: null
---

Find place names within a particular postal code. The response is in JSON format, sorted by postalcode and place name.

## Parameters

### Required

| Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description 
| :----- | :---------- | :----------- 
|
|postalcode|String|Exception Values: For Canada, Ireland, and Malta use the first letters of the full postal codes. For Argentina, use the 4-digit postal codes used before 1999. For Brazil, only major postal codes ending with 000 and the major code per municipality are available.
|

### Optional

| Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Type&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description 
| :----- | :---------- | :----------- 
|
|country|String|Values are [ISO-3166 country codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes){:target=_blank} i.e. country=FR. Default is all countries. Can occur more than once, i.e. country=FR&country=GP.
|
|maxRows|Integer|Max number of rows returned. Default is 20, max is 1000.
|
|callback|String|Give this parameter a value 'formatted=true' to format the output with linefeeds and indentation. This parameter can be useful to view the JSON result in a browser, but should not be used in production due to waste of bandwidth.
|
|charset|String|Defines the encoding used for the response document. Default is 'UTF8'.
|

### Request

Below is an example URL of a request and its usage.

|Usage|URL|
|:-----|:----
|
|Return place names within postal code 6600 in Austria.| http://api.geonames.org/postalCodeLookupJSON?postalcode=6600&country=AT&username=demo
|

### Example cURL Request
```
curl --location --request GET 'http://api.geonames.org/postalCodeLookupJSON?postalcode=6600&country=AT&username=mvincent1212'
```

## Response

### Return Values

The response turns an array of objects called postalcodes.

Within each object are the following return values in this order:
* adminCode2 - the code of an administrative subdivision of the place name.
* adminCode3 - this code is a subdivision within adminCode2.
* adminName3 - the name of the place corresponding to adminCode3.
* adminCode1 - this code is a subdivision that includes both adminCode2 and adminCode3.
* adminName2
* lng - the longitude of the place.
* countryCode
* postalcode
* adminName1
* placeName
* lat - the latitude of the place.

### Example Response
```
{
    "postalcodes": [
        {
            "adminCode2": "708",
            "adminCode3": "70805",
            "adminName3": "Breitenwang",
            "adminCode1": "07",
            "adminName2": "Politischer Bezirk Reutte",
            "lng": 10.7333333,
            "countryCode": "AT",
            "postalcode": "6600",
            "adminName1": "Tirol",
            "placeName": "Breitenwang",
            "lat": 47.4833333
        },
        {
            "adminCode2": "708",
            "adminCode3": "70820",
            "adminName3": "Lechaschau",
            "adminCode1": "07",
            "adminName2": "Politischer Bezirk Reutte",
            "lng": 10.706520080566406,
            "countryCode": "AT",
            "postalcode": "6600",
            "adminName1": "Tirol",
            "placeName": "Lechaschau",
            "lat": 47.488035007826824
        }
    ]
}
```
