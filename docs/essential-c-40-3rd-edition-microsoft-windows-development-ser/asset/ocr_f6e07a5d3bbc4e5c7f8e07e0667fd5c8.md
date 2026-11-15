# LISTING 12.18: Statement Lambdas with a Single Input Parameter

```
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
// ...
IEnumerable<Process> processes = Process.GetProcesses().Where(
    // process => { return process.WorkingSet64 > 2^30; });
    ...
```
```

(In Listing 12.18, Where() returns a query for processes that have a physical memory utilization greater than 1GB)

Note that back in Listing 12.17, the body of the statement lambda includes multiple statements inside the statement block (via curly braces). Although a statement lambda can have any number of statements, typically a statement lambda uses only two or three statements in its statement block.

# Expression Lambdas

Unlike a statement lambda, which includes a statement block and, therefore, zero or more statements, an expression lambda has only an expression, with no statement block. Listing 12.19 is the same as Listing 12.15, except that it uses an expression lambda rather than a statement lambda.

# LISTING 12.19: Passing a Delegate with a Statement Lambda

```
```csharp
class DelegateSample
{
    // ...
    static void Main(string[] args)
    {
        int i;
        int[] items = new int[5];
        for (int i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer:");
            items[i] = int.Parse(Console.ReadLine());
        }
    }
}
BubbleSort(items, (first, second) => first < second; );
```
```