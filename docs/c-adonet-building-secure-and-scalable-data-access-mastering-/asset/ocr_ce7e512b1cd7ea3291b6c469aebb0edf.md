```
```csharp
while (reader.Read())
{
    // Processing each row of data
    int employeeId = reader.GetInt32(0);
    string employeeName = reader.GetString(1);
    Console.WriteLine($"Employee ID: {employeeId}, Employee Name: {employeeName}");
}
}
}
}
}
```
```

# Key Features and Improvements

ADO.NET Core offers several key features and improvements over traditional ADO.NET, such as:

+   - **Cross-Platform Compatibility:** ADO.NET Core runs on different operating systems, such as Windows, macOS, and Linux.
+   - **Improved Performance:** ADO.NET Core is optimized for performance, providing better performance compared to traditional ADO.NET.
+   - **Increased Flexibility:** ADO.NET Core is more flexible and modular, allowing developers to choose the components they need for their specific requirements.
+   - **Support for New Data Sources:** ADO.NET Core supports new data sources, such as NoSQL databases, which were not supported by traditional ADO.NET.