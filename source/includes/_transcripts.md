# Transcripts

The Transcript resource provides the core functionality for accessing the MeasureOne transcript processing capabilities.   At a structural level, a Transcript consists of a set of attributes that provide information about the Transcript, and Source Data that contains the raw academic data.   The Source Data payload may be a structured payload (e.g., JSON or XML), a structured document (e.g., PDF or HTML), or an unstructured document (e.g., JPEG).  In all cases the platform will attempt to ingest, extract and normalize this data, providing the processed transcript back in a normalized JSON format.  Depending on the format of the Source Data, processing may require asynchronous communication.   To facilitate this, the [webhook apis](#webhook) provide callback mechanisms.

### Transcript Creation
`POST /transcripts/new`