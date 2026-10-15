7. Click the Add button (Figure 23.19). The RectAreaFunction.cs file is added to the SqlServerProjectUDF project.

8. Modify the code of the RectAreaFunction.cs file, as given in Listing 23.12:

# Listing 23.12: Showing the Code of the RectAreaFunction.cs File

```
using System;
using System.Data;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using Microsoft.SqlServer.Server;

public partial class UserDefinedFunctions
{
    [Microsoft.SqlServer.Server.SqlFunction]
    public static SqlDecimal RectAreaFunction(decimal RectLength, decimal RectWidth)
    {
        // Put your code here
        return new SqlDecimal(RectLength * RectWidth);
    }
};
```

In Listing 23.12, we are creating a UDF, RectAreaFunction, with two parameters, RectLength and RectWidth. The data type of the parameters is decimal, and the return type of the function is SqlDecimal. The RectAreaFunction function returns the area of a rectangular shape with the provided values for its parameters. Note that the SqlFunction attribute is required for the deployment of a function.

9. Press the CTRL+SHIFT+B keys combination on the keyboard to build the solution.

After creating a UDF as a CLR object, you can use it either directly in T-SQL or in .NET Framework 4.0. Listing 23.13 shows the query to create an assembly, SqlServerProjectUDF, and a function, RectAreaFunction, to invoke the created UDF CLR object:

# Listing 23.13: Creating the SqlServerProjectUDF Assembly and the RectAreaFunction Function

```
CREATE ASSEMBLY SqlServerProjectUDF
FROM 'D:\Black Books\C# 2010\Chapter 23\SqlServerProjectUDF\SqlServerProjectUDF\bin\Debug\SqlServerProjectUDF.dll'
GO
Create Function RectAreaFunction
(@RectLength decimal(4,1), @RectWidth decimal(4,1))
RETURNS decimal(8,2)
AS EXTERNAL NAME SqlServerProjectUDF.UserDefinedFunctions.RectAreaFunction
GO
```

In Listing 23.13, an assembly, SqlServerProjectUDF, is created. Then, a function, RectAreaFunction, is created on the basis of the CLR object, RectAreaFunction.

Now, let’s create the following table, Papers, in SQL:

```
CREATE TABLE Papers
(
    PaperID int PRIMARY KEY,
    PaperLength decimal(4,1),
    PaperWidth decimal(4,1),
    PaperArea AS
    (
        dbo.RectAreaFunction(PaperLength, PaperWidth)
    )
)
```

In the preceding query, you can see that the Papers table is created with four columns, PaperID, PaperLength, PaperWidth, and PaperArea. The PaperArea column stores the area of any rectangular shape paper. Let’s insert some records in the Papers table by using the following query: