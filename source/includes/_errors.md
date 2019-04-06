# Errors
<a href='error'></a>

MeasureOne uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted). Codes in the 5xx range indicate an error with MeasureOne's servers.

### HTTP Status Codes

The following table details the possible HTTP status codes:

<a href='httpcode'></a>

Code | Name | Description 
-----| ---------- | ---------------------------------------------------------------------
200 | OK	| Everything worked as expected.
400 | Bad Request	| The request was unacceptable, often due to missing a required parameter.
401 | Unauthorized	| No valid API key provided.
402 | Request Failed	| The parameters were valid but the request failed.
404 |  Not Found	| The requested resource doesn't exist.
429 |  Too Many Requests	| Too many requests hit the API too quickly.
500, 502, 503, 504 | Server Errors	| Something went wrong on MeasureOne's end.


> Example Error Response 

```json
{
  "error_code": "DUPLICATE_VALUE",
  "http_code": 409,
  "request_id": "req_1J4BuZp4WloNlsk4JE8MxGPgJ02",
  "error_message": "john.doe@example.com already exists",
  "display_message": "The user with email jon.doe@example.com already exists"
}
```

### Error Payload

Error payload response reference

|Name|Type|Description|
-----|----|------------|
|error_code|string|The error code as defined [here](#errorcode) |
|http_code|integer|The HTTP code as defined [here](#httpcode)
|request_id|string|A unique request id to reference this message|
|error_message|string|Developer friendly message|
|display_message|string|User-friendly message|

<a href='errorcode'></a>
### Error Codes
The `error_code` attribute can take on one of the values in the following table:

|Error Code|Description|
|----------|------------|
|INVALID_FIELDS| Invalid value type for attribute | 
|MISSING_FIELDS| Missing required attrbute | 
|UNKNOWN_FIELDS| Unknown attribute in payload |
|INVALID_BODY| Bad payload bady | 
|INVALID_HEADERS| Bad header format |
|NOT_FOUND| Bad object ID | 
|INVALID_CREDENTIALS| Invalid API keys or other credentials for the requested operations | 
|SANDBOX_ONLY| Non-sandbox operations attempted in sandbox | 
|DUPLICATE_VALUES| Attempt to perform a create operation on a resource that already exists | 
|API_ERROR| Other API Error | 
