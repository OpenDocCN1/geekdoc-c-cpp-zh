# 10.9 static Class Members 455

of the number of Employee objects that have been created. We declare Count's accessor private, because only class Employee should be able to modify Count's value. Count is a static auto-implemented property, that the compiler creates a corresponding private variable that Count manages. When you initialize it, the compiler initializes it to the type's default value (in this case, 0).

When Employee objects exist, Count can be used in any method or property of class Employee—this example increments Count in the constructor (line 19). Client code can access the Count with the expression Employee.Count, which evaluates to the number of Employee objects that have been created.

```
// Fig. 10: Employee.cs
// static property used to maintain a count of the number of
// Employee objects that have been created.
using System;
public class Employee {
    public static int Count { get; private set; } // objects in memory
    public string FirstName { get; }
    public string LastName { get; }

    // initialize name, add 1 to static Count and
    // output string indicating that constructor was called
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Count++; // increment static count of employees
        Console.WriteLine($"Employee constructor: {FirstName}{LastName} = {Count}");
    }
}
```

Fig. 10.10 | static property used to maintain a count of the number of Employee objects that have been created.

**EmployeeTest**
EmployeeTest method Main (Fig. 10.11) instantiates two Employee objects (lines 14–15). When each object's constructor is invoked, lines 17–18 of Fig. 10.10 assign the Employee's first name and last name properties to FirstName and LastName. These states do not make copies of the original string arguments.

# Software Engineering Observation 10.12

![](bbox=[0.14, 0.84, 0.213, 0.873])

Actually, strings in C# are immutable—they cannot be modified after they are created. Therefore, it is safe to have many references to one string. This is not normally the case for most other classes. If strings are immutable, you might wonder why we use operators and += to concatenate strings. String-concatenation operations actually result in a new string containing the concatenated values. The original string objects are not modified.