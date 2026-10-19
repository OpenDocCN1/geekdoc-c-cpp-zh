example, if Salary needs to be used in calculations, it can be retrieved as Double, which is its type in the database table, using the following statement shown in line 71:

```
double salary = drEmployee.GetDouble(2);
```

This approach, however, requires knowledge of the exact type of the fields, when data are retrieved.

Step 7-3: Comment out line 61, and add the code from line 65 in Figure 12-69 to display salary using the ordinal. Run the form to test the code.

Comment out line 65, and add the code from lines 67 and 68, which use the GetOrdinal method. Run the form to test the code.

Comment out lines 67 and 68, and add the code from lines 71 and 72, which use the GetDouble method. Uncomment lines 74 and 75. Run the form to test the code.

The DataReader has several other methods and properties that help to work with it. Some commonly used methods/properties are shown in Table 12-1.

# Table 12-1: Methods and Properties of SqlDataReader

| Method/property name | Description | Example |
|---|---|---|
| Close | Closes the DataReader object | drEmployee.Close |
| Dispose | Releases resources used | drEmployee.Dispose |
| GetBoolean, GetDateTime, GetDecimal, GetDouble, GetFloat, GetInt32, GetString | Gets the value in its original type | drEmployee.GetString(0)
drEmployee.GetDouble(2) |
| GetOrdinal(String) | Gets the ordinal | drEmployee.GetOrdinal["EmpId"] |
| GetSchemaTable | Returns a data table that contains field attributes | drEmployee.GetSchemaTable |
| GetValue | Gets the value as object | drEmployee.GetValue(0) |
| GetValues | Gets the values in the row as an array of objects | object[] colValues = new object[10];
drEmployee.GetValues(colValues); |
| Read | Advances to next row | drEmployee.Read() |
| Properties |  |  |
| FieldCount | Gets the number of columns | int count = drEmployee.FieldCount |
| HasRows | Indicates whether the DataReader contains any rows | if (drEmployee.HasRows) |

# ExecuteNonQuery Method of SqlCommand

Previous sections used the ExecuteScalar method and ExecuteReader method of the SqlCommand to retrieve data from tables. The SqlCommand has a third method, ExecuteNonQuery, to execute queries that do not retrieve any data, but can be used to update, insert and delete records, and to do other database operations like create tables. For update, insert and delete, the method returns the number of records affected. For most other operations, the return value is -1.

You will use the ExecuteNonQuery to update the salary when the user enters the new salary into the TextBox, txtSalary, and clicks the Update Salary button on the Employee_Reader1 form presented earlier in Figure 12-65. The code is shown in Figure 12-70.