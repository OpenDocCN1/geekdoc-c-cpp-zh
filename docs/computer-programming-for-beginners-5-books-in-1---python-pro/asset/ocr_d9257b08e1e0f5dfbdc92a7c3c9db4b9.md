```
```csharp
catch
{
    Console.WriteLine("The inner catch");
}
}
catch
{
    Console.WriteLine("The outer catch");
}
}
}
```
```

```
```csharp
public class Employee {

    public string EmployeeName { get; set; }
}
```
```

The code prints the following:

![](bbox=[0.034, 0.485, 0.966, 0.578])

In case there is no inner catch block with the necessary exception type, the exception will flow to outer catch block until an appropriate exception filter is found. Here is an example:

```
```csharp
using System;
public class NestedtryCatch
{
    public static void Main()
    {
        Employee emp = null;

        try
```
```