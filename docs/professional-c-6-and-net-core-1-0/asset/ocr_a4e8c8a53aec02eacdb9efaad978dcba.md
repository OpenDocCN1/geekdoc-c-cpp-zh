# Casing of Names

In many cases you should use *Pascal casing* for names. With Pascal casing, the first letter of each word in a name is capitalized:

```
EmployeeSalary, ConfirmationDialog, PlainTextEncoding.
```

Notice that nearly all the names of namespaces, classes, and members in the base classes follow Pascal casing. In particular, the convention of joining words using the underscore character is discouraged. Therefore, try not to use names such as employee_salary. It has also been common in other languages to use all capitals for names of constants. This is not advised in C# because such names are harder to read—the convention is to use Pascal casing throughout:

```
const int MaximumLength;
```

The only other casing convention that you are advised to use is *camel casing*. Camel casing is similar to Pascal casing, except that the first letter of the first word in the name is not capitalized: employeeSalary, confirmationDialog, plainTextEncoding. Following are three situations in which you are advised to use camel casing:

+   - For names of all private member fields in types:

```
private int subscriberId;
```

Note, however, that often it is conventional to prefix names of member fields with an underscore:

```
private int _subscriberId;
```

+   - For names of all parameters passed to methods:

```
public void RecordSale(string salesmanName, int quantity);
```

+   - To distinguish items that would otherwise have the same name. A common example is when a property wraps around a field:

```
private string employeeName;
public string EmployeeName
{
    get
    {
        return employeeName;
    }
}
```

If you are wrapping a property around a field, you should always use camel casing for the private member and Pascal casing for the public or protected member, so that other classes that use your code see only names in Pascal case (except for parameter names).

You should also be wary about case sensitivity. C# is case sensitive, so it is syntactically correct for names in C# to differ only by the case, as in the previous examples. However, bear in mind that your assemblies might at some point be called from Visual Basic applications—and *Visual Basic is not case sensitive*. Hence, if you do use names that differ