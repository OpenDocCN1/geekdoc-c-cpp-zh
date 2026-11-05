```
```csharp
var cust = new Tuple<string, string, int>(
"Ravindra", "Pune", 15820);
return cust;
}
//The code snippet below calls the method and receives the returned tuple
var cust = MyClass.ReturnTupleMethod();
Console.WriteLine("Customer:{0}, Living in : {1}, Has account number : {2} .",
cust.Item1, cust.Item2, cust.Item3);
```
```

# A complete program using Tuple

```
```csharp
//C# program that uses 4-item Tuple
using System;
class UseTuple
{
 static void Main()
 {
 // Create four-item tuple.
// ... Use var implicit type.
var tuple = new Tuple<string, string[], int, int[]>("Technical", new string[] { "C#", ".NET" },
2020, new int[] { 15, 8 });
// Passing tuple as argument.
tupleMethod(tuple);
}
static void tupleMethod(Tuple<string, string[], int, int[]> tuple)
{
 // Evaluate the tuple's items.
Console.WriteLine(tuple.Item1);
foreach (string value in tuple.Item2)
{
 Console.WriteLine(value);
}
Console.WriteLine(tuple.Item3);
foreach (int value in tuple.Item4)
{
 Console.WriteLine(value);
}
} //end of tupleMethod
} //end of class
```
```

# Output

Technical
c#
.NET
2020
15
8