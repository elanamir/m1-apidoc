# Sandbox Environment

The MeasureOne sandbox environment provides an easy way to test the API and your application against fake data.   Access to sandbox is determined by using a sandbox API Key.


The sandbox environment provides the same endpoints as the production environment.   
The biggest difference between the production and sandbox environments is that the sandbox only accepts and operates on fake data.   Transcript data submitted to the sandbox must originate from a specific set of data as detailed in the table below.   Each of these fake transcripts will be accepted by the sandbox and processed.   Specfically, the `source_data` in the `/transcript/new` endpoint must include one of these documents, with the type and encoding as detailed below.  Any other content will be rejected.


Each test transcript has a document-specific processing behavior associated with it.   This enables testing of synchronous vs. webhook-driven asynchronous communication.     


|Transcript Number|Document Link | Type | Processing Behavior | 
-----------------|------------------|------|----------------------|
||||||
 
 
### Posting to the Sandbox

The easiest way to post a new transcript to the sandbox is to set the `document_link` attribute in the `source_data` object of the Transcript object as follows:

* Set the `document_link` to the Document Link value in the table above
* Set the `type` to the Type value in the table above

In the event that the processing behavior is synchronous, the request will return a processed transcript payload in the response.   In the event that the processing behavior is asynchronous, the request will return a pending response in the response and a webhook call with the processed transcript will be invoked.

