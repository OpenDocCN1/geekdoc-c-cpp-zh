# Monitoring and Auditing Database Access

Monitor and audit database access by implementing logging mechanisms:

```
using System;
using System.IO;
using System.Security.Cryptography;

string logPath = "log.txt";
string connectionString = "Server=localhost;Database=SampleDatabase;Integrated Security=true;";
using (StreamWriter writer = new StreamWriter(logPath, true))
{
    writer.WriteLine($"{DateTime.Now}: Connection opened");
    try
    {
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            writer.WriteLine($"{DateTime.Now}: Connection successful");
            // Your code here
        }
    }
    catch (Exception ex)
    {
        writer.WriteLine($"{DateTime.Now}: Connection failed - {ex.Message}");
    }
}
```

By implementing these best practices for securing database connections in C# ADO.NET, you can protect sensitive information and prevent unauthorized access to your database.