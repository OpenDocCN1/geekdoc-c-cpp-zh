```
return employee;
}
```

```
class Program
{
    static void Main()
    {
        Employee employee1;

        Employee employee2 = new Employee();
        employee2.SetName("Inigo", "Montoya");
        employee2.Save();

        // Modify employee2 after saving.
        IncreaseSalary(employee2);

        // Load employee1 from the saved version of employee2
        employee1 = DataStore.Load("Inigo", "Montoya");

        Console.WriteLine(
            "{0}: {1}",
            employee1.GetName(),
            employee1.Salary);

        // ...
    }
    // ...
}
```

Output 5.4 shows the results.

# OUTPUT 5.4:

```
Name changed to 'Inigo Montoya'
Inigo Montoya
```

The reverse of the save process appears in Listing 5.14, which uses a StreamReader rather than a StreamWriter. Again, Close() needs to be called on both FileStream and StreamReader once the data has been read.

Output 5.4 does not show any salary after “Inigo Montoya.” because Salary was not set to “Enough to survive on” by a call to IncreaseSalary() until after the call to Save().