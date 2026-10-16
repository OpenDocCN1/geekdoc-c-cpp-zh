```
public override string ToString() => $"{id.ToString()}: {name, -20} {salary:C}";
}
```

In the Main method of the sample application, a new Dictionary<TKey, TValue> instance is created, where the key is of type EmployeeId and the value is of type Employee. The constructor allocates a capacity of 31 elements. Remember that capacity is based on prime numbers.
However, when you assign a value that is not a prime number, you don’t need to worry. The Dictionary<TKey, TValue> class itself takes the next prime number that follows the integer passed to the constructor to allocate the capacity. After creating the employee objects and IDs, they are added to the newly created dictionary using the new dictionary initializer syntax. Of course, you can also invoke the Add method of the dictionary to add objects instead (code file DictionarySample/Program.cs):

```
public static void Main()
{
    var employees = new Dictionary<EmployeeId, Employee>(31);
    var idTony = new EmployeeId("C3755");
    var tony = new Employee(idTony,"Tony Stewart", 379025.00m);

    var idCarl = new EmployeeId("F3547");
    var carl = new Employee(idCarl,"Carl Edwards", 403466.00m);

    var idKevin = new EmployeeId("C3386");
    var kevin = new Employee(idKevin,"Kevin Harwick", 415261.00m);

    var idMatt = new EmployeeId("F3323");
    var matt = new Employee(idMatt,"Matt Kenseth", 1589390.00m);

    var idBrad = new EmployeeId("D3234");
    var brad = new Employee(idBrad,"Brad Keselowski", 322295.00m);

    var employees = new Dictionary<EmployeeId, Employee>(31)
    {
        [idTony] = tony,
        [idCarl] = carl,
        [idKevin] = kevin,
        [idMatt] = matt,
        [idBrad] = brad
    };

    foreach (var employee in employees.Values)
    {
        WriteLine(employee);
    }
}
```

After the entries are added to the dictionary, inside a while loop employees are read from the dictionary. The user is asked to enter an employee number to store in the variable userInput, and the user can exit the application by entering X. If the key is in the dictionary, it is examined with the TryGetValue method of the Dictionary<TKey, TValue> class. TryGetValue returns true if the key is found and false otherwise. If the value is found, the value associated with the key is stored in the employee variable. This value is written to the console.