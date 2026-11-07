| Function Name and Parameters | Parameter(s) Type | Function Return Value |
|---|---|---|
| `strcpy(destStr, srcStr)` | `destStr` and `srcStr` are null-terminated `char` arrays | The base address of `destStr` is returned; `srcStr` is copied into `destStr`. |
| `strncpy(destStr, srcStr, limit)` | `destStr` and `srcStr` are null-terminated `char` arrays and `limit` is a nonnegative integer value | Copies the string `srcStr` into the string variable `destStr`. At most `limit` characters are copied into `destStr`. |
| `strlen(str)` | `str` is a null-terminated `char` array | An integer value `0` specifying the length of the `str` (excluding the `\0`) is returned. |

# HEADER FILE `string`

This header file—not to be confused with the header file `cstring`—supplies a programmer-defined data type named `string`. Associated with the `string` type are a data type `string::size_type` and a named constant `string::npos`. These are defined as follows:

|  |  |
|---|---|
| `string::size_type` | An unsigned integer type |
| `string::npos` | The maximum value of type `string::size_type` |

The type string contains several functions for string manipulation. In addition to the string functions listed in Table 7-1, the following table describes additional string functions. In this table, we assume that `strVar` is a string variable and `str` is a string variable, a string constant, or a character array. The name of the function is shown in bold.

| Expression | Effect |
|---|---|
| `getline(istreamVar, strVar);` | `istreamVar` is an input stream variable (of type `istream` or `ifstream`).<br><br>Characters until the newline character are input from `istreamVar` and stored in `strVar`. (The newline character is read but not stored into `strVar`.) The value returned by this function is usually ignored. |