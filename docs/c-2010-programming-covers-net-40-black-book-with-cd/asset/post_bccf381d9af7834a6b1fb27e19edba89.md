
## Immediate Solutions

## Creating a SQL Server Project

In this section, you learn how to create a CLR object in .NET Framework. Let’s perform the following steps to create a new SQL Server project:

- 1. Open Microsoft Visual Studio 2010.
- 2. Select File→New→Project. The New Project dialog box opens (Figure 23.3).
- 3. Select the Database→SQL Server option in the Installed Templates category and select the Visual C# SQL CLR Database Project template (Figure 23.3).
- 4. Enter a project name, SQLServerProject1, in the Name text box and enter a project location, D:\Black Books\C# 2010\Chapter 23\, in the Location combo box. Figure 23.3 shows the New Project dialog box to create the SQLServerProject1 project:

![](img/e073a4882197be4ab61103cbe0bcb394_1151_0.png)

Figure 23.3: Displaying the New Project Dialog Box to Create the SQLServerProject1 Project

### NOTE

Select the target framework as 2.0, while creating the SQLServerProject1 project.

- 5. Click the OK button. The Add Database Reference dialog box appears (Figure 23.4).
- 6. Select an existing database connection or create a new one. In our case, we are selecting the existing database connection, charu-pc.Northwind.dbo, as shown in Figure 23.4:

![](img/e073a4882197be4ab61103cbe0bcb394_1152_0.png)

Figure 23.4: Selecting a Database Connection in the Add Database Reference Dialog Box

7. Click the OK button (Figure 23.4). The SqlServerProject1 project is displayed in Visual Studio 2010, as shown in Figure 23.5:

![](img/e073a4882197be4ab61103cbe0bcb394_1152_1.png)

Figure 23.5: Displaying the SqlServerProject1 Project in Visual Studio 2010

Let’s now learn how to establish an SQL connection between a SQL Server project and SQL Server 2008.

## Connecting a SQL Server Project with SQL Server 2008

You can connect a SQL Server project with SQL Server 2008, by creating a new connection also. When you create a new SQL Server project, you can click the Add New Reference button (Figure 23.4) to open the New Database Reference dialog box. In the New Database Reference dialog box, you need to provide data source, server name, authentication mode, and database name, as shown in Figure 23.6:

Figure 23.6: Creating a New Connection for a SQL Server Project

Click the OK button to close the New Database Reference dialog box and complete the process of establishing a new SQL connection.

## Creating and Using Stored Procedures

In this section, you learn to create a stored procedure as a CLR object in .NET Framework. To do this, you need to add a Stored Procedure CLR object in SQL Server project. Let’s create a SQL Server project, named ProductDetailsSP (also available on CD), and add a stored procedure, GetProductDetailsSP, to it.

Perform the following steps to create the ProductDetailsSP project and the GetProductDetailsSP stored procedure in Visual Studio 2010:

- 1. Open Microsoft Visual Studio 2010.
- 2. Create a Visual C# SQL CLR Database Project, named ProductDetailsSP, as shown in Figure 23.7:

Figure 23.7: Creating the ProductDetailsSP Project

![](img/e073a4882197be4ab61103cbe0bcb394_1153_0.png)

![](img/e073a4882197be4ab61103cbe0bcb394_1153_1.png)

### NOTE

Select the target framework as 2.0, while creating the ProductDetailsSP project.

- 3. Select an existing database connection or create a new one. In our case, we are selecting the existing database connection, charu-pc.Northwind.dbo.
- 4. Click the OK button. The ProductDetailsSP project is displayed in Visual Studio 2010.
- 5. Right-click the ProductDetailsSP project in Solution Explorer and select the Add→Stored Procedure option. The Add New Item-ProductDetailsSP dialog box opens (Figure 23.8).
- 6. Select the Stored Procedure template and enter GetProductDetailsSP.cs in the Name text box, as shown in Figure 23.8:

![](img/e073a4882197be4ab61103cbe0bcb394_1154_0.png)

Figure 23.8: Entering a Stored Procedure Name

- 7. Click the Add button (Figure 23.8). The GetProductDetailsSP.cs file is added to the ProductDetailsSP project.
- 8. Modify the code of the GetProductDetailsSP.cs file, as given in Listing 23.6:

### Listing 23.6: Showing the Code of the GetProductDetailsSP.cs File

```
using System;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using Microsoft.SqlServer.Server;
public partial class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetProductDetailsSP(int ProductID)
    {
        SqlConnection con = new SqlConnection("context connection=true");
        con.Open();
        SqlCommand myCommand = new SqlCommand("SELECT ProductID,ProductName,QuantityPerUnit,UnitPrice,UnitsInStock FROM Products WHERE ProductID=@ProductID Order By ProductName", con);
        myCommand.Parameters.Add("@ProductID", SqlDbType.Int);
        myCommand.Parameters["@ProductID"].Value=ProductID;
        SqlDataReader sdr = myCommand.ExecuteReader();
        SqlPipe sp = SqlContext.Pipe;
        sp.Send(sdr);
        con.Close();
    }
};
```

In Listing 23.6, the SqlProcedure attribute is used to show that the stored procedure is for deployment. A SqlConnection object is created with the context connection=true string. The SqlCommand object is created by passing the connection object. An object of the SqlDataReader class is returned by the ExecuteReader() method, which is returned to the client by using the Send() method of the SqlPipe class.

9. Press the CTRL+SHIFT+B keys combination on the keyboard to build the solution.

After creating a stored procedure as a CLR object, you can use it either directly in T-SQL or in .NET Framework 4.0. Let’s use a stored procedure in T-SQL first. Listing 23.7 shows the query to create an assembly, ProductDetailsSP, and a stored procedure, GetProductDetails, to invoke the created stored procedure CLR object:

### Listing 23.7: Creating the ProductDetailsSP Assembly and the GetProductDetails Stored Procedure

```
CREATE ASSEMBLY ProductDetailsSP
FROM 'D:\black Books\C# 2010\Chapter 23\ProductDetailsSP\ProductDetailsSP\bin\debug\ProductDetailsSP.dll'
GO
Create Procedure GetProductDetails
(@productID Int)
AS EXTERNAL NAME ProductDetailsSP.StoredProcedures.GetProductDetailsSP
GO
```

In Listing 23.7, an assembly, ProductDetailsSP, is created. Then, a stored procedure, GetProductDetails, is created on the basis of the CLR object, GetProductDetailsSP.

### NOTE

The following query shows how to enable the CLR in SQL Server 2008:

```
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'clr enabled', 1;
GO
RECONFIGURE;
GO
```

The following query shows how to change the compatibility level of the Northwind database in SQL Server 2008:

```
sp_dbcmptlevel 'Northwind'
sp_dbcmptlevel 'Northwind', 90
```

After executing the query given in Listing 23.7, you can execute the GetProductDetails stored procedure, as shown in the following query:

```
EXECUTE GetProductDetails 3
```

In the preceding query, we are executing the GetProductDetails stored procedure by supplying a product id, 3. Figure 23.9 shows the output of the GetProductDetails stored procedure in T-SQL:

![](img/e073a4882197be4ab61103cbe0bcb394_1155_0.png)

Figure 23.9: Displaying the Output of the GetProductDetails Stored Procedure

Besides calling a stored procedure in T-SQL, you can also use it in a Windows application or a console application in C#.NET. Let’s use the GetProductDetails stored procedure in a console application, named UseProductSP (also available on CD).

Perform the following steps to create the UseProductSP application:

- 1. Open Microsoft Visual Studio 2010.
- 2. Create a Console Application, named UseProductSP.
- 3. Modify the code of the Program.cs file, as given in Listing 23.8:

### Listing 23.8: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;
using System.Data.SqlClient;
namespace UseProductSP
{
    class Program
    {
        static void Main(string[] args)
        {
            string constr = @"Data Source=.;Initial Catalog=Northwind;Integrated Security=True";
            var con = new SqlConnection(constr);
            SqlCommand cmd = con.CreateCommand();
            cmd.CommandText = "GetProductDetails";
            cmd.CommandType = CommandType.StoredProcedure;
            var param = new SqlParameter("@productId", 3);
            cmd.Parameters.Add(param);
            con.Open();
            SqlDataReader sdr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
            while (sdr.Read())
            {
                Console.WriteLine("Product ID: {0} \nItem: {1} \nQuantity: {2} \nPrice: {3}", sdr["productID"], sdr["productName"], sdr["quantityperunit"], sdr["unitPrice"]);
            }
            sdr.Close();
        }
    }
}
```

In Listing 23.8, a variable of SqlConnection type is created to execute the GetProductDetailsSP stored procedure. This stored procedure is taking a parameter of Integer type. Then, the SqlDataReader object is returned by using the ExecuteReader() method, and the Read() method is used in the while loop to show the product details of a selected item.

- 4. Press the CTRL+F5 keys combination on the keyboard to execute the UseProductSP application. Figure 23.10 shows the output of the UseProductSP application:

![](img/e073a4882197be4ab61103cbe0bcb394_1156_0.png)

Figure 23.10: Showing the Output of the UseProductSP Application

Next, let’s learn to create and use the CLR object, triggers.
