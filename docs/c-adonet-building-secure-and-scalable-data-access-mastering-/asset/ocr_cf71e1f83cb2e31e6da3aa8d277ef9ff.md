returns the name of the field at the current position, and the GetValue method returns the value of the field at the current position.

```
for (int i = 0; i < reader.FieldCount; i++)
{
    string fieldName = reader.GetName(i);
    object fieldValue = reader.GetValue(i);
    Console.WriteLine("Field Name: {0}, Field Value: {1}", fieldName, fieldValue);
}
```

+   - **Check for Null Values:** Use the IsDBNull method to check if a field value is null before attempting to access it. This will prevent null reference exceptions from occurring.

```
object fieldValue = reader.GetValue(i);
if (!reader.IsDBNull(i))
{
    // Code to handle non-null value
}
else
{
    // Code to handle null value
}
```

+   - **Close the Data Reader After Use:** Be sure to close the Data Reader after you're done with it. This will release any resources associated with the Data Reader and ensure that the connection is closed.

```
reader.Close();
```