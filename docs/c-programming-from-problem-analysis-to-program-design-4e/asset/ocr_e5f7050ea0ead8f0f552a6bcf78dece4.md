# TABLE 14-6 OleDbDataReader class members

| OleDbDataReader members | Description |
|---|---|
| `Close()` | Closes an `OleDbDataReader` object |
| `FieldCount` | Property; gets the number of columns in the current row |
| `GetBoolean(int)` | Gets the value of the specified column as a Boolean |
| `GetChar(int)` | Gets the value of the specified column as a `char` |
| `GetDecimal(int)` | Gets the value of the specified column as a `decimal` |
| `GetDouble(int)` | Gets the value of the specified column as a `double` |
| `GetInt16(int)`, `GetInt32(int)`, `GetInt64(int)` | Gets the value of the specified column as an integer |
| `GetName(int)` | Gets the name of the specified column as a Boolean |
| `GetOrdinal(string)` | Given the name of the column, gets the ordinal location |
| `GetString(int)` | Gets the value of the specified column as a `string` |
| `GetType(int)` | Gets the type of a specified column |
| `Read()` | Advances the `OleDbDataReader` object to the next record |

**NOTE** A number of the methods in Table 14-6 begin with `Get`, followed by a data type, such as `GetString()`. These methods are called **typed accessors**.

Example 14-10 illustrates using the data reader to process results retrieved using the SQL command. In this example, the values are first stored in an `object`, a member of the `Member` class. The `Member` object is then used to populate a list box object for a Windows application.