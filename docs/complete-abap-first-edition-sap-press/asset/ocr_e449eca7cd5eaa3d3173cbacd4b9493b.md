| **Data Type** | **Definition** |
| --- | --- |
| *c* | Text field<br>(alphanumeric characters) |
| *d* | Date field<br>(format: *YYYYMMDD*) |
| *n* | Numeric text field<br>(numeric characters 0 to 9) |
| *t* | Time field<br>(format: *HHMMSS*) |
| *x* | Hexadecimal field |

**Table 4.1** Predefined Elementary Data Types (Cont.)

Predefined elementary data types can be classified as numeric or nonnumeric types. There are six predefined numeric elementary data types:

+   - 4-byte integer (*i*)
+   - 8-byte integer (*int8*)
+   - Binary floating-point number (*f*)
+   - Packed number (*p*)
+   - Decimal floating point number with 16 decimal places (*decfloat16*)
+   - Decimal floating point number with 34 decimal places (*decfloat34*)

There are five predefined nonnumeric elementary data types:

+   - Text field (*c*)
+   - Numeric character string (*n*)
+   - Date (*d*)
+   - Time (*t*)
+   - Hexadecimal (*x*)

The field length for data types *f*, *i*, *int8*, *decfloat16*, *decfloat34*, *d*, and *t* is fixed. In other words, you don't need to specify the length when you use these data types to declare data objects (or user-defined elementary data types) in your program. The field length determines the number of bytes that the data object occupies in memory. In types *c*, *n*, *x*, and *p*, the length is not part of the type definition. Instead, you define it when you declare the data object in your program.