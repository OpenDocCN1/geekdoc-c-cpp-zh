```
using static System.Console;
class CreateSomeEmployees
{
    static void Main()
{
        Employee aWorker = new Employee();
        Employee anotherWorker = new Employee(234);
        Employee theBoss = new Employee('A');
        WriteLine("{0, 4}{1, 14}", aWorker.IdNumber,
            aWorker.Salary.ToString("C"));
        WriteLine("{0, 4}{1, 14}", anotherWorker.IdNumber,
            anotherWorker.Salary.ToString("C"));
        WriteLine("{0, 4}{1, 14}", theBoss.IdNumber,
            theBoss.Salary.ToString("C"));
    }
}
```

Figure 9-25 The CreateSomeEmployees program

| | $0.00 |
|---|---|
| 234 | $0.00 |
| 111 | $100,000.00 |

Figure 9-26 Output of the CreateSomeEmployees program

Most likely, a single application would not use all four constructors of the Employee class. More likely, each application that uses the class would use only one or two constructors. We create a class with multiple constructors to provide flexibility for your clients. For example, some clients might choose to construct Employee objects with just ID numbers, and others might prefer to construct them with ID numbers and salaries.

# Using Constructor Initializers

The Employee class in Figure 9-24 contains four constructors, and each constructor initializes the same fields. In a fully developed code used by a company, many more fields would be initialized, creating a lot of duplicated code. The exists extra work of writing the repetitive statements in these constructors, even more work will be required when the class is modified in the future. For example, if your organization institutes a new employee ID number format that requires a specific number of digits, then each constructor will have to be modified, and one or more of the constructor versions that must be modified might be overlooked, introducing errors into the programs that are clients of the class.