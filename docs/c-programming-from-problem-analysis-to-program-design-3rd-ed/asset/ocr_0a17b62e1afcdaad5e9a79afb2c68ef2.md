![](bbox=[0.174, 0.095, 0.238, 0.146])

A number of the methods in Table 14-6 begin with Get, followed by a data type, such as `GetString( )`. These methods are called **typed accessors**.

Example 14-10 illustrates using the data reader to process results retrieved using the SQL command. In this example, the values are first stored in an `object`, aMember, of the Member `class`. The Member `object` is then used to populate a list box object for a Windows application.

# Example 14-10

```
```csharp
Member aMember;
OleDbDataReader dbReader;
dbReader = dbCmd.ExecuteReader(); // dbCmd is the OleDbCommand
                                  // object instantiated in Example 14-2.
while (dbReader.Read())
{
    // Retrieve records 1-by-1...
    aMember = new Member(dbReader["FirstName"].ToString(),
                         dbReader["LastName"].ToString());
    this.listBox1.Items.Add(aMember);
}
```
```

Example 14-11 shows the statements that make up the Member `class`. Notice that one of the constructors of the Member `class` accepts two `string` arguments. In Example 14-10, a Member `object`, aMember, is instantiated using two of the retrieved dbReader objects. The database field names (from Figure 14-1) are used as indexers with the retrieved dbReader `object`. Notice how the `ToString( )` method is called with the dbReader `object` in Example 14-10. This is because the dbReader returns each data field as an object. You have to do the type conversion before sending it to the Member constructor; otherwise, an exception is thrown. For the sake of brevity, the Member `class` shown in Example 14-11 contains only the read-only properties, a `ToString( )` method, and two constructors.

# Example 14-11

```
```csharp
// Member.cs
// This class includes private members of
// identification number, first and last
// names, and local phone number. Read-only
// properties are included. The ToString( )
// method is overridden to return a formatted
// full name.
using System;
```
```