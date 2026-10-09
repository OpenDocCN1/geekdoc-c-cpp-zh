```
{
    return first < second;
}
);
```

// ...

In general, explicitly declared parameter types are optional in all lambda expressions if the compiler can infer the types from the delegate that the lambda expression is being converted to. For situations when specifying the type makes code more readable, however, C# enables you to do so. In cases where inference is not possible, the C# language requires that the lambda parameter types be stated explicitly. If one lambda parameter type is specified explicitly, then all of them must be specified explicitly, and they must all match the delegate parameter types exactly.

> **Guidelines**

**CONSIDER** omitting the types from lambda formal parameter lists when the types are obvious to the reader or when they are an insignificant detail.

One other means of reducing the syntax is possible, as shown in Listing 13.14: A lambda expression that has exactly one parameter whose type is inferred may omit the parentheses around the parameter list. If there are zero parameters or more than one parameter, or if the single parameter is explicitly typed, the lambda must have parentheses around the parameter list.

# **LISTING 13.14: Stetement Lambdas with a Single Input Parameter**

```
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
// ...
IEnumerable<Process> processes = Process.GetProcesses().Where(
    process => { return process.WorkingSet64 > 1000000000; });
// ...
```

In Listing 13.14, the Where() method returns a query for processes that have a physical memory utilization greater than 1 billion bytes. Contrast