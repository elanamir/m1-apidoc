# Overview

Welcome to the MeasureOne API!   Our API provides a modern, developer-friendly RESTful interface to the MeasureOne platform.   Our focus is on simplicity, predictability, and consistency of behavior so that you the developer can easily integrate our capabilities into your application.     


## Authentication
```shell 
curl https://prod.measureone.com/v1/transcripts \
  -u <YOUR API KEY HERE>:
```

Authenticate your account by including your secret key in API requests.  Authentication to the API is performed via HTTP Basic Auth. Provide your API key as the basic auth username value. You do not need to provide a password.  All API requests must be made over HTTPS with TLS versions 1.1+.  TLS versions below 1.1 are not supported.   Calls made over plain HTTP will fail. API requests without authentication will also fail.


## HTTP Protocol
The MeasureOne API exclusively uses POST requests to communicate and HTTP response codes to indicate status and errors. All responses come in standard JSON. All requests must include a Content-Type of `application/json` and the body must be valid JSON.

## API Servers
Environment | Hostname 
---------| ------------------------------- 
Sandbox | `sandbox.measureone.com` 
Development | `dev.measureone.com` 
Production | `prod.measureone.com` 

The Sandbox environment provides full API capabilities with a set of test data.   For more details on the test data please see the MeasureOne Development Guide.   The Development environment provides support of the test data as well as up to 50 live transcripts.   The Production environment provides full production capabilities.


## Versioning
```shell
curl https://prod.measureone.com/v1/ \
  -u m1_1J4C7gNPCXbkdbKfOT1JFes3HB5: \
  -H "MeasureOne-Version: 2019-03-13"
```
The current major version of the measureone API is `v1`.   When we make backwards-incompatible changes to the API, we release new, dated versions. The current version is `2019-03-13`.    

All requests will use your account API settings, unless you override the API version.   To set the API version on a specific request, send it in a `MeasureOne-Version` header.


