```
```csharp
{
    [Conditional("DEBUG")]
    public static void M() {
        Console.WriteLine("Executed Class1.M");
    }
}
class Class2
{
    public static void Test() {
        Class1.M();
    }
}
```
```

declares Class1.M as a conditional method. Class2's Test method calls this method. Since the conditional compilation symbol DEBUG is defined, if Class2.Test is called, it will call M. If the symbol DEBUG had not been defined, then Class2.Test would not call Class1.M.

It is important to note that the inclusion or exclusion of a call to a conditional method is controlled by the conditional compilation symbols at the point of the call. In the example

# File class1.cs:

```
```csharp
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}
```
```

# File class2.cs:

```
```csharp
#define DEBUG
class Class2
{
    public static void G() {
        Class1.F();        // F is called
    }
}
```
```

# File class3.cs:

```
```csharp
#undef DEBUG
class Class3
{
    public static void H() {
        Class1.F();        // F is not called
    }
}
```
```