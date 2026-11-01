# ExecuteScalar()

On many occasions, it is necessary to return a single result from a SQL statement, such as the count of records in a given table, or the current date/time on the server. The ExecuteScalar() method can be used in such situations:

```
using System;
using System.Data.SqlClient;

public class ExecuteScalarExample
{
    public static void Main(string[] args)
    {
        string source = "server=(local);" +
            "integrated security=SSPI;" +
            "database=Northwind";
        string select = "SELECT COUNT(*) FROM Customers";
        SqlConnection conn = new SqlConnection(source);
        conn.Open();
        SqlCommand cmd = new SqlCommand(select, conn);
        object o = cmd.ExecuteScalar();
        Console.WriteLine(o);
    }
}
```

code download ExecuteReaderExample.cs

The method returns an object, which you can cast to the appropriate type if required. If the SQL you are calling returns only one column, it is preferable to use ExecuteScalar() over any other method of retrieving that column. That also applies to stored procedures that return a single value.

# ExecuteXmlReader() (SqlClient Provider Only)

As its name implies, the ExecuteXmlReader() method executes the command and returns an XmlReader object to the caller. SQL Server permits a SQL SELECT statement to be extended with a FOR XML clause. This clause can take one of three options:

+   - FOR XML AUTO — Builds a tree based on the tables in the FROM clause
+   - FOR XML RAW — Maps result set rows to elements, with columns mapped to attributes
+   - FOR XML EXPLICIT — Requires that you specify the shape of the XML tree to be returned

For this example, use AUTO:

```
using System;
using System.Data.SqlClient;
using System.Xml;

public class ExecuteXmlReaderExample
{
    public static void Main(string[] args)
    {
        string source = "server=(local);" +
            "integrated security=SSPI;" +
            "database=Northwind";
        string select = "SELECT ContactName,CompanyName " +
            "FROM Customers FOR XML AUTO";
        SqlConnection conn = new SqlConnection(source);
        conn.Open();
        SqlCommand cmd = new SqlCommand(select, conn);
        XmlReader xr = cmd.ExecuteXmlReader();
        xr.Read();
        string data;
        do
```