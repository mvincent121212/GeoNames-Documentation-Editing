---
title: 'Before You Start'

layout: null
---

### Account Set Up

To get access to the GeoNames Web Services API, you must make an account with the GeoNames website.
1. Navigate to the [GeoNames Website](https://www.geonames.org/){:target="_blank}.
2. Click **login** in the top right.
3. Create a new account.
4. Verify your account with the email GeoNames sends (check your spam folder if you do not see it).
5. Navigate to [Manage Account](https://www.geonames.org/manageaccount){:target="_blank} and enable web services under **Free Web Services**.

### Send a Request

To make a request, you must add your GeoNames username as a parameter to your request. The **base url** for all services is `api.geonames.org`

Example: `api.geonames.org/postalCodeSearch?postalcode=10001&username={username}`

### Important Considerations

* String parameters require [url encoding](https://forum.geonames.org/gforum/posts/list/8.page){:target="_blank}.
* If using Javascript, refer to [JSON webservices](https://www.geonames.org/export/JSON-webservices.html) (as most browsers do not call XML services from another server).
* Secure endpoints are available at secure.geonames.org.
* Service Level Agreement is available under [commercial web services](https://www.geonames.org/commercial-webservices.html){:target="_blank}.

### Additional Resources

* [Client Libraries](https://www.geonames.org/export/client-libraries.html){:target="_blank}
* [Credits Per Request](https://www.geonames.org/export/credits.html){:target="_blank}
* [Webservice Exception](https://www.geonames.org/export/webservice-exception.html){:target="_blank}
