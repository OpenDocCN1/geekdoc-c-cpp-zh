# Listing 23.16: Creating a Table Using XML Data Type

```
CREATE TABLE XMLDataTb
(
XMLDataId INT NOT NULL PRIMARY KEY,
XMLContent XML,
DataFeedDate DATETIME DEFAULT GETDATE()
)
insert into XMLDataTb values (1,'<Record><Employee EmpID="1"/>
<Name>Kabir</Name>
<Address>Delhi</Address>
<Phone>1111111</Phone>
</Record>','06/Aug/2010')
insert into XMLDataTb values (2,'<Record><Employee EmpID="4"/>
<Name>Shilpa</Name>
<Address>Delhi</Address>
<Phone>2222222</Phone>
</Record>','05/Aug/2010')
insert into XMLDataTb values (3,'<Record><Employee EmpID="2"/>
<Name>Dheeraj</Name>
<Address>Dubai</Address>
<Phone>4444444</Phone>
</Record>','06/Aug/2010')
```

In Listing 23.16, we are creating the XMLDataTb table using the CREATE TABLE statement. This table is created with three columns, XMLDataId, XMLContent, and DataFeedDate. The data types of these columns are INT, XML, and DATETIME, respectively. Then, three records are inserted in the XMLDataTb table using the INSERT statement.

# NOTE

The XMLDataTb table is created in a user defined database, MyData.

Now, let’s create a console application to access the XMLDataTb table in SQL Server, which stores XML data. The source code of the AccessXMLData application is also available in the provided CD. Listing 23.17 shows the code of the Program.cs file of the AccessXMLData application:

# Listing 23.17: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using System.Xml;
namespace AccessXMLData
{
    class Program
    {
        static void Main(string[] args)
        {
            string connection = @"Data Source=.;Initial Catalog=MyData;Integrated Security=True";
            var con = new SqlConnection(connection);
            var command = con.CreateCommand();
            command.CommandText = "Select * from XMLDataTb";
            con.Open();
            var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
            StringBuilder xmldat a = new StringBuilder("-----Employees-----", 40);
            Console.WriteLine(xmldat a.ToString());
            while (reader.Read())
            {
                SqlXml xml = reader.GetSqlXml(1);
                XmlReader xmlreader = xml.CreateReader();
                while (xmlreader.Read())
```