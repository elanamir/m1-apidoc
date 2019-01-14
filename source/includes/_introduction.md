# Introduction

The MeasureOne API is organized around REST. Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients. We support cross-origin resource sharing, allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code). JSON is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.

To make the API as explorable as possible, accounts have test mode and live mode API keys. There is no "switch" for changing between modes, just use the appropriate key to perform a live or test transaction. Requests made with test mode credentials never hit the banking networks and incur no cost.


# API libraries
Official libraries for the Stripe API are available in several languages. Community-supported libraries are also available for additional languages.

https://api.stripe.com

# Authentication
```shell 
curl https://api.measureone.com/v1/transcripts \
  -u <YOUR API KEY HERE>:
```

Authenticate your account by including your secret key in API requests.  Authentication to the API is performed via HTTP Basic Auth. Provide your API key as the basic auth username value. You do not need to provide a password.  All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

# Errors
MeasureOne uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.). Codes in the 5xx range indicate an error with MeasureOne's servers.

Some 4xx errors that could be handled programmatically include an error code that briefly explains the error reported.


# ATTRIBUTES
 type
string
The type of error returned. One of api_connection_error, api_error, authentication_error, card_error, idempotency_error, invalid_request_error, or rate_limit_error

 charge
string
For card errors, the ID of the failed charge.

 code
string
For some errors that could be handled programmatically, a short string indicating the error code reported.

 decline_code
string
For card errors resulting from a card issuer decline, a short string indicating the card issuer’s reason for the decline if they provide one.

 doc_url
string
A URL to more information about the error code reported.

 message
string
A human-readable message providing more details about the error. For card errors, these messages can be shown to your users.

 param
string
If the error is parameter-specific, the parameter related to the error. For example, you can use this to display a message near the correct form field.

 source
hash
The source object for errors returned on a request involving a source.

## HTTP status code summary
Code | Description
-----| --------------------
200 | OK	Everything worked as expected.
400 | Bad Request	The request was unacceptable, often due to missing a required parameter.
401 | Unauthorized	No valid API key provided.
402 | Request Failed	The parameters were valid but the request failed.
404 |  Not Found	The requested resource doesn't exist.
409 |  Conflict	The request conflicts with another request (perhaps due to using the same idempotent key).
429 |  Too Many Requests	Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.
500, 502, 503, 504 | Server Errors	Something went wrong on MeasureOne's end.

The error reponse will have the following attributes:



Error types
api_connection_error	Failure to connect to Stripe's API.
api_error	API errors cover any other type of problem (e.g., a temporary problem with Stripe's servers), and are extremely uncommon.
authentication_error	Failure to properly authenticate yourself in the request.
card_error	Card errors are the most common type of error you should expect to handle. They result when the user enters a card that can't be charged for some reason.
idempotency_error	Idempotency errors occur when an Idempotency-Key is re-used on a request that does not match the first request's API endpoint and parameters.
invalid_request_error	Invalid request errors arise when your request has invalid parameters.
rate_limit_error	Too many requests hit the API too quickly.
validation_error	Errors triggered by our client-side libraries when failing to validate fields (e.g., when a card number or expiration date is invalid or incomplete).

# Handling errors
Our API libraries raise exceptions for many reasons, such as a failed charge, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

Attribute | Type | Description
----------|------|---------
type | string | the type of error returned.   One of XXX.
codes | string | short string indicating the code looking
message | human readable message providing more details about the error
param | string | error specific parameter


# Metadata
```shell
curl https://api.stripe.com/v1/charges \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -d amount=2000 \
  -d currency=usd \
  -d source=tok_visa \
  -d metadata[order_id]=6735
{
  "id": "ch_1DmMda2eZvKYlo2CkeESaJO5",
  "object": "charge",
  "amount": 100,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "balance_transaction": "txn_19XJJ02eZvKYlo2ClwuJ1rbA",
  "captured": false,
  "created": 1546008514,
  "currency": "usd",
  "customer": null,
  "description": "My First Test Charge (created for API docs)",
  "destination": null,
  "dispute": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {
  },
  "invoice": null,
  "livemode": false,
  "metadata": {
    "order_id": "6735"
  },
  "on_behalf_of": null,
  "order": null,
  "outcome": null,
  "paid": true,
  "payment_intent": null,
  "receipt_email": null,
  "receipt_number": null,
  "refunded": false,
  "refunds": {
    "object": "list",
    "data": [

    ],
    "has_more": false,
    "total_count": 0,
    "url": "/v1/charges/ch_1DmMda2eZvKYlo2CkeESaJO5/refunds"
  },
  "review": null,
  "shipping": null,
  "source": {
    "id": "card_1DmMdY2eZvKYlo2CQ8USc474",
    "object": "card",
    "address_city": null,
    "address_country": null,
    "address_line1": null,
    "address_line1_check": null,
    "address_line2": null,
    "address_state": null,
    "address_zip": null,
    "address_zip_check": null,
    "brand": "MasterCard",
    "country": "US",
    "customer": null,
    "cvc_check": null,
    "dynamic_last4": null,
    "exp_month": 12,
    "exp_year": 2019,
    "fingerprint": "7a9bk9ncM08SXfua",
    "funding": "credit",
    "last4": "4444",
    "metadata": {
    },
    "name": null,
    "tokenization_method": null
  },
  "source_transfer": null,
  "statement_descriptor": null,
  "status": "succeeded",
  "transfer_group": null
}
```
Updateable Stripe objects—including Account, Charge, Customer, Refund, Subscription, and Transfer—have a metadata parameter. You can use this parameter to attach key-value data to these Stripe objects.

Metadata is useful for storing additional, structured information on an object. As an example, you could store your user's full name and corresponding unique identifier from your system on a Stripe Customer object. Metadata is not used by Stripe—for example, not used to authorize or decline a charge—and won't be seen by your users unless you choose to show it to them.

Some of the objects listed above also support a description parameter. You can use the description parameter to annotate a charge—with, for example, a human-readable description like 2 shirts for test@example.com. Unlike metadata, description is a single string, and your users may see it (e.g., in email receipts Stripe sends on your behalf).

Do not store any sensitive information (personally identifiable information, card details, etc.) as metadata or in the description parameter.

Note: You can specify up to 20 keys, with key names up to 40 characters long and values up to 500 characters long.

Was this section helpful?YesNo
SAMPLE METADATA USE CASES
Link IDs
Attach your system's unique IDs to a Stripe object, for easy lookups. For example, add your order number to a charge, your user ID to a customer or recipient, or a unique receipt number to a transfer.

Refund papertrails
Store information about why a refund was created, and by whom.

Customer details
Annotate a customer by storing an internal ID for your later use.



# Pagination

```shell
curl https://api.stripe.com/v1/customers?limit=3 \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -G
{
  "object": "list",
  "url": "/v1/customers",
  "has_more": false,
  "data": [
    {
      "id": "cus_EHIlrwhRLoczh3",
      "object": "customer",
      "account_balance": 0,
      "created": 1546575592,
      "currency": "usd",
      "default_source": null,
      "delinquent": false,
      "description": null,
      "discount": null,
      "email": null,
      "invoice_prefix": "81551D9",
      "livemode": false,
      "metadata": {
      },
      "shipping": null,
      "sources": {
        "object": "list",
        "data": [
    
        ],
        "has_more": false,
        "total_count": 0,
        "url": "/v1/customers/cus_EHIlrwhRLoczh3/sources"
      },
      "subscriptions": {
        "object": "list",
        "data": [
    
        ],
        "has_more": false,
        "total_count": 0,
        "url": "/v1/customers/cus_EHIlrwhRLoczh3/subscriptions"
      },
      "tax_info": null,
      "tax_info_verification": null
    },
    {...},
    {...}
  ]
}
```

All top-level API resources have support for bulk fetches via "list" API methods. For instance, you can list charges, list customers, and list invoices. These list API methods share a common structure, taking at least these three parameters: limit, starting_after, and ending_before.

Stripe utilizes cursor-based pagination via the starting_after and ending_before parameters. Both parameters take an existing object ID value (see below) and return objects in reverse chronological order. The ending_before parameter returns objects listed before the named object. The starting_after parameter returns objects listed after the named object. If both parameters are provided, only ending_before is used.

Was this section helpful?YesNo
ARGUMENTS
 limit
optional, default is 10
A limit on the number of objects to be returned, between 1 and 100.

 starting_after
optional
A cursor for use in pagination. starting_after is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, ending with obj_foo, your subsequent call can include starting_after=obj_foo in order to fetch the next page of the list.

 ending_before
optional
A cursor for use in pagination. ending_before is an object ID that defines your place in the list. For instance, if you make a list request and receive 100 objects, starting with obj_bar, your subsequent call can include ending_before=obj_bar in order to fetch the previous page of the list.

LIST RESPONSE FORMAT
 object
string, value is "list"
A string describing the object type returned.

 data
array
An array containing the actual response elements, paginated by any request parameters.

 has_more
boolean
Whether or not there are more elements available after this set. If false, this set comprises the end of the list.

 url
string
The URL for accessing this list.

## Auto-pagination
```shell
curl https://api.stripe.com/v1/customers \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -D "-" \
  -X POST
````
Most of our libraries support auto-pagination. This feature easily handles fetching large lists of resources without having to manually paginate results and perform subsequent requests.

Since curl simply emits raw HTTP requests, it doesn't support auto-pagination.

The auto-pagination feature is specific to Stripe's libraries and cannot
be used directly with curl.
Request IDs
Each API request has an associated request identifier. You can find this value in the response headers, under Request-Id. You can also find request identifiers in the URLs of individual request logs in your Dashboard. If you need to contact us about a specific request, providing the request identifier will ensure the fastest possible resolution.

Was this section helpful?YesNo


# Versioning
```shell
curl https://api.stripe.com/v1/charges \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -H "Stripe-Version: 2018-11-08"
```
When we make backwards-incompatible changes to the API, we release new, dated versions. The current version is 2018-11-08. Read our API upgrades guide to see our API changelog and to learn more about backwards compatibility.

All requests will use your account API settings, unless you override the API version. The changelog lists every available version. Note that events generated by API requests will always be structured according to your account API version.

To set the API version on a specific request, send a Stripe-Version header.

You can visit your Dashboard to upgrade your API version. As a precaution, use API versioning to test a new API version before committing to an upgrade.

Was this section helpful?YesNo
