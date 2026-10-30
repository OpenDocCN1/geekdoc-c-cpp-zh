| Attribute | Status | Description |
|---|---|---|
| attributes-charset | required | the character set used by attributes of type text or name |
| attributes-natural-language | required | the natural language used by attributes of type text or name |
| printer-uri | required | the printer's Universal Resource Identifier |
| requesting-user-name | optional | name of user submitting job (used for authentication, if enabled) |
| job-name | optional | name of job used to distinguish between multiple jobs |
| ipp-attribute-fidelity | optional | if true, tells printer to reject job if all attributes can't be met; otherwise, printer does its best to print the job |
| document-name | optional | the name of the document (suitable for printing in a banner, for example) |
| document-format | optional | the format of the document (e.g., plaintext, PostScript) |
| document-natural-language | optional | the natural language of the document |
| compression | optional | the algorithm used to compress the document data |
| job-k-octets | optional | size of the document in 1,024-octet units |
| job-impressions | optional | number of impressions (images imposed on a page) submitted in this job |
| job-media-sheets | optional | number of sheets printed by this job |

Figure 21.5 Attributes of print-job request

The IPP header contains a mixture of text and binary data. Attribute names are stored as text, but sizes are stored as binary integers. This complicates the process of building and parsing the header, since we need to worry about such things as network byte order and our host processor's ability to address an integer on an arbitrary byte boundary. A better alternative would have been to design the header to contain text only. This simplifies processing at the cost of slightly larger protocol messages.

# 21.3 The Hypertext Transfer Protocol

Version 1.1 of HTTP is specified in RFC 2616. HTTP is also a request-response protocol. A request message contains a start line, followed by header lines, a blank line, and an optional entity body. The entity body contains the IPP header and data in this case.

HTTP headers are ASCII, with each line terminated by a carriage return (\r) and a line feed (\n). The start line consists of a method that indicates which operation the client is requesting, a Uniform Resource Locator (URL) that describes the server and protocol, and a string indicating the HTTP version. The only method used by IPP is POST, which is used to send data to a server.

The header lines specify attributes, such as the format and length of the entity body. A header line consists of an attribute name followed by a colon, optional white space, and the attribute value, and is terminated by a carriage return and a line feed. For example, to specify that the entity body contains an IPP message, we include the header line

```
Content-Type: application/ipp
```