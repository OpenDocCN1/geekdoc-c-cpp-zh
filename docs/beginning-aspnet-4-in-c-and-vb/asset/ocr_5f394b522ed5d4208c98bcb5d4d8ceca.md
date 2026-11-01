> The classes from the namespace System.Data.SqlClient are discussed in Chapter 30.

Invoking the stored procedure written with T-SQL or with C# is not different at all. The code for calling stored procedures is completely identical; from the caller code you don't know if the stored procedure is implemented with T-SQL or the CLR. An extract of the result shows the order dates for the customer with ID 3:

44124 9/1/2001
44791 12/1/2001
45568 3/1/2002
46377 6/1/2002
47439 9/1/2002
48378 12/1/2002

As you have seen, mainly data-driven stored procedures are better done with T-SQL. The code is a lot shorter. Writing stored procedures with the CLR has the advantage if you need some specific data-processing, for example, by using the .NET cryptography classes.

# USER-DEFINED FUNCTIONS

User-defined functions are somewhat similar to stored procedures. The big difference is that user-defined functions can be invoked within SQL statements.

# Creating User-Defined Functions

A CLR user-defined function can be defined with the attribute SqlFunction. The sample function CalcHash() converts the string that is passed to a hashed string. The MD5 algorithm that is used for hashing the string is implemented with the class MD5CryptoServiceProvider from the namespace System.Security.Cryptography. The ComputeHash() method computes the hash from the byte array input and returns a computed hash byte array. The hashed byte array is converted back to a string by using the StringBuilder class:

```
```csharp
using System.Data.SqlTypes;
using System.Security.Cryptography;
using System.Text;
using Microsoft.SqlServer.Server;

public partial class UserDefinedFunctions
{
    [SqlFunction]
    public static SqlString CalcHash(SqlString value)
    {
        byte[] source = ASCIIEncoding.ASCII.GetBytes(value.ToString());
        byte[] hash = new MD5CryptoServiceProvider().ComputeHash(source);

        var output = new StringBuilder(hash.Length);

        for (int i = 0; i < hash.Length - 1; i++)
        {
            output.Append(hash[i].ToString("X2"));
        }

        return new SqlString(output.ToString());
    }
}
```
```