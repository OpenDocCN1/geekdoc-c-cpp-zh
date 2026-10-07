# Table 5.1: DS2 Predefined Packages by SAS Release

| Package | SAS Release | Purpose |
| FCMP | SAS 9.4 M0 | Allows calling FCMP functions and subroutines from a DS2 program. |
| Hash | SAS 9.4 M0 | Enables you to use hash objects in your DS2 programs. Hash objects enable you to quickly and efficiently store, search, and retrieve data based on lookup keys. Hash records can also be easily manipulated, sorted, and saved to a table within a DS2 program. |
| Hiter | SAS 9.4 M0 | Enables you to conduct iterative processing of the associated hash object in your DS2 program. You must declare the hash before declaring the associated hiter. |
| HTTP | SAS 9.4 M2 | Provides an HTTP client with methods that allow you to access HTTP web services and capture the returned results in a DS2 program. |
| JSON | SAS 9.4 M3 | Provides the methods necessary to parse and write JSON text and is quite handy for decoding results returned by the HTTP package. |
| Logger | SAS 9.4 M0 | Provides methods to detect which SAS logging facility message levels are active in the current SAS session and to write messages at user-selected levels. This package is pretty simple to use but it does not currently produce output when operating in client/server mode. Therefore, it is not useful when programming in SAS Studio or SAS Enterprise Guide. For these reasons, there will not be a logger section in this book, but it is mentioned here so that we do not forget it exists. |
| Matrix | SAS 9.4 M0 | Implements SAS/IM capabilities in DS2, providing powerful and flexible matrix programming tools. No licensing over Base SAS is required to use the matrix package. |
| SQLSTMT | SAS 9.4 M0 | Provides methods for passing a dynamic FedSQL statement to a database for execution and for accessing any result rows produced without using a SET statement. |
| TZ | SAS 9.4 M3 | Provides methods for facilitating the processing of local and international time and date values in a DS2 program. |