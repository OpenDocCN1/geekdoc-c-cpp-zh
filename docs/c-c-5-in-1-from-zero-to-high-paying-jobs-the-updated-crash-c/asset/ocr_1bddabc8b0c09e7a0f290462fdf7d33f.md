}
}
```

# Step 4: Use the Custom ORM

Use the custom ORM framework to map C# objects to database tables and perform CRUD operations:

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        string connectionString = "your_connection_string_here";
        CustomORM orm = new CustomORM(connectionString);

        // Example class and attributes
        [Table("Employees")]
        class Employee
        {
            [Column("Id")]
            public int EmployeeId { get; set; }

            [Column("Name")]
            public string EmployeeName { get; set; }
        }

        Employee newEmployee = new Employee
        {
            EmployeeId = 1,
            EmployeeName = "John Doe"
        };

        orm.Insert(newEmployee);

        // Perform other CRUD operations as needed
        Console.WriteLine("CRUD operations completed.");
    }
}
```
```