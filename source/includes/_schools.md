# Schools

The Schools interface enables developers to access the list of schools for which MeasureOne maintains a library of transcript portal URLs.    This list is used to power the MeasureOne Transcript Portal.   By accessing this list, developers can implement their own access portal experiences.

## Retrieve Schools Request
`POST /schools/get`

Request payload reference: Empty

## Retrieve Schools Response

> Example Retrieve Schools Response

```json
[
	{
		"id": string,
		"school_name":	string,
		"unit_id": string,
		"opeid":	string,
		"school_state": string,
		"school_city":	string,
		"sis_url":	string,
		"school_address_1":	string,
		"school_address_2":	string,
		"school_zipcode":	string,
		"school_logo_url": string($url),
		"short_code": string
	},
	...
]
```

The response will return a list or school objects as defined the the following table.   

<h3>Attribute Reference</h3>
<a href="schoolobj"></a>

|Name|Type|Description|
-----|----|------------|
id|string|Unique object ID|
school_name|string|School Name|
unit_id|string|
opeid|string|The school OPEID|
school_state|string|State|
school_city|string|City|
sis_url|string|URL of transcript portal|
school_address1|string|Street address field 1|
school_address2|string|Street address field 2|
school_zipcode|string|Zipcode|
school_logo_url|string|URL of school logo|
short_code|string|3 letter short code for school name|

## Retrieve School by ID Request

> Example Retrieve School by ID Request

```json
{
	"id": "sch_1J4BlTgxKA1Mtvjel8rtVkSq5ki"
}
```

`POST /schools/get_by_id`

Request payload Reference: a school object id.

<h3>Attribute Reference</h3>
<a href="school-get-by-id-request"></a>

|Name|Type|Description|
-----|----|------------|
id|string|Unique object ID|

## Retrieve School by ID Response

> Example Retrieve School by ID Response

```json
{
	"id": "sch_1J4BlTgxKA1Mtvjel8rtVkSq5ki"
	...

}
```


Response payload reference: the school object referenced by the requested id, as defined [above](#schoolobj).  

In the event of an error, the API will return an Error object as the value of the id causing the error.   See the [Error](#error) section for more details.




