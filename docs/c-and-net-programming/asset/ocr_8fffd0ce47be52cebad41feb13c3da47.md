# Example

```
```csharp
// Illustration of Instance methods.
Class InstanceDemo
{
    void method1()
    {
        Console.WriteLine("First Instance method.");
    }
    void method2()
    {
        Console.WriteLine("Second Instance method.");
    }
    static void Main( string[] args )
    {
        InstanceDemo Obj = new InstanceDemo();
        obj.method1();
        obj.method2();
        Console.Read();
    }
}
Input Nil
```
```

# Output

| Output |
|---|
| First Instance method. |
| Second Instance method. |

# 5.4  Anonymous Methods

# Concept

+   1. Anonymous methods are inline methods that do not have a name.
+   2. Anonymous methods reduce the coding overhead by eliminating the need to create a separate method.
+   3. Without anonymous methods developers often had to create instance of a class just to call one method.

# Explanation

# Example

```
```csharp
//Illustration of anonymous method
using System;
using System.Timers;

public class AnonymousMethod
{
```
```