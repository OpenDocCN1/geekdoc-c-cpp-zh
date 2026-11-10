For example, as shown in Table 4.2, a TYPE c data object will be filled with spaces initially, whereas a TYPE n data object would be filled with zeros.

| Data Type | Initial Field Length (Bytes) | Valid Field Length (Bytes) | Initial Value |
|---|---|---|---|
| **Numeric Types** | | | |
| i | 4 | 4 | 0 |
| int8 | 8 | 8 | 0 |
| f | 8 | 8 | 0 |
| p | 8 | 1-16 | 0 |
| decfloat16 | 8 | 8 | 0 |
| decfloat34 | 16 | 16 | 0 |
| **Character Types** | | | |
| c | 1 | 1-65535 | Space |
| d | 8 | 8 | '00000000' |
| n | 1 | 1-65535 | '0 ... 0' |
| t | 6 | 6 | '000000' |
| **Hexadecimal Type** | | | |
| x | 1 | 1-65535 | X'0 ... 0' |

**Table 4.2** Elementary Data Types: Technical Specifications

Predefined nonnumeric data types can be further classified as follows:

+   - **Character types**
+   
+     Data types c, n, d, and t are character types. Data objects of these types are known as *character fields*. Each position in one of these fields can store one code character. For example, a data object of LENGTH 5 can store five characters and a data object of LENGTH 10 can store ten characters. Currently, ABAP only works with single-byte codes, such as American Standard Code for Information Interchange (ASCII) and Extended Binary Coded Decimal Interchange Code (EBCDIC). As of release 6.10, SAP NetWeaver AS ABAP supports both Unicode and non-Unicode systems. However, support for non-Unicode systems has been withdrawn from SAP NetWeaver 7.5.