# Sandbox Environment

The MeasureOne sandbox environment provides a way to test the API and your application against fake data.   Access to sandbox is determined by using a sanbox API Key.

## Endpoints

The sandbox environment provides the same endpoints as the production environment.    It adds one more endpoint: 

`POST /sandbox/init`

that initializes the sandbox and deletes all the data in it.

## Sandbox Transcript Data
The biggest difference between the production and sandbox environments is that the sandbox only accepts and operates on fake data.   Transcript data submitted to the sandbox must originate from a specific set of data as detailed in the table below.   Each of these fake transcripts will be accepted by the sandbox and processed.   Specfically, the `source_data` in the `/transcript/new` endpoint must include one of these documents, with the type and base64 encoding as detailed in the document.  Any other content will be rejected.


Each test transcript has a document-specific processing behavior associated with it.   This enables testing of synchronous vs. webhook-driven asynchronous communication.  


Transcript Number|Raw Document link | Type | Base64 Document link | Processing behavior | 
-----------------|------------------|------|----------------------|---------------------|

 