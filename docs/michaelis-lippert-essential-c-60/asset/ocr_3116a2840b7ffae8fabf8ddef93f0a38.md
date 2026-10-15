One other means of reducing the syntax is possible, as shown in Listing 12.13: A lambda expression that has exactly one parameter whose type is inferred may omit the parentheses around the parameter list. If there are zero parameters or more than one parameter, or if the single parameter is explicitly typed, the lambda must have parentheses around the parameter list.

# LISTING 12.13: Statement Lambdas with a Single Input Parameter

```
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
// ...
IEnumerable<Process> processes = Process.GetProcesses().Where(
    process => { return process.WorkingSet64 > 1000000000; });
// ...
```

In Listing 12.13, the where() method returns a query for processes that have a physical memory utilization greater than 1 billion bytes. Contrast this with Listing 12.14, which has a parameterless statement lambda. The empty parameter list requires parentheses. Note also that in Listing 12.14, the body of the statement lambda includes multiple statements inside the statement block (via curly braces). Although a statement lambda can contain any number of statements, typically a statement lambda uses only two or three statements in its statement block. (The use of the generic Func delegate type is described in the section “General-Purpose Delegates: System.Func and System.Action” later in this chapter.)

# LISTING 12.14: Parameterless Statement Lambdas

```
using System;
// ...
Func<string> getUserInput =
    () =>
    {
        string input;
        do
        {
            input = Console.ReadLine();
        }
        while(input.Trim().Length == 0);
        return input;
    };
// ...
```