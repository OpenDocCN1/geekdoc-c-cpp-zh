```
```csharp
        cmd.ExecuteNonQuery();
    }
    catch (System.Data.SqlClient.SqlException ex)
    {
        Console.WriteLine("Source: " + ex.Source);
        Console.WriteLine("Number: " + ex.Number.ToString());
        Console.WriteLine("Message: " + ex.Message);
        Console.WriteLine("Class: " + ex.Class.ToString());
        Console.WriteLine("Procedure: " + ex.Procedure.ToString());
        Console.WriteLine("Line Number: " + ex.LineNumber.ToString());
        Console.WriteLine("Server: " + ex.Server.ToString());

    }
    catch (System.Exception ex)
    {
        Console.WriteLine("Source: " + ex.Source);
        Console.WriteLine("Exception Message: " + ex.Message);
    }
    finally
    {
        if (conn.State == ConnectionState.Open)
        {
            Console.WriteLine("Finally block closing the connection");
            conn.Close();
        }
    }
}
```
```

# **Purposeful use of Finally block in ADO .NET exceptions**

A finally block is executed whether or not an exception occurs. Hence, it is particularly useful for cleanup operations. The purpose of a finally statement is to ensure that the necessary cleanup of objects, usually objects that are holding external resources, happens immediately, even if an exception is thrown. Consider an open database connection in a try block. If an exception occurs, it is caught in the catch block just after the try block as shown in the code snippet below,

```
```csharp
string connectionString = ...;// Some connection string
SqlConnection sqlConnection = null;
try
{
    sqlConnection = new SqlConnection(connectionString);
    sqlConnection.Open();
    //Some code
}
```
```