```
```csharp
public class Program
{
    public static void Main()
    {
        Console.WriteLine(typeof(Program).Namespace);
        //StackOverflow.Documentation.CSharp.Keywords
    }
}
```
```

Namespaces in C# can also be written in chained syntax. The following is equivalent to above:

```
```csharp
namespace StackOverflow.Documentation.CSharp.Keywords
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine(typeof(Program).Namespace);
            //StackOverflow.Documentation.CSharp.Keywords
        }
    }
}
```
```

# ## Section 52.24: ref, out

The `ref` and `out` keywords cause an argument to be passed by reference, not by value. For value types, this means that the value of the variable can be changed by the callee.

```
```csharp
int x = 5;
ChangeX(ref x);
// The value of x could be different now
```
```

For reference types, the instance in the variable can not only be modified (as is the case without `ref`), but it can also be replaced altogether:

```
```csharp
Address a = new Address();
ChangeFieldInAddress(a);
// a will be the same instance as before, even if it is modified
CreateANewInstance(ref a);
// a could be an entirely new instance now
```
```

The main difference between the `out` and `ref` keyword is that `ref` requires the variable to be initialized by the caller, while `out` passes that responsibility to the callee.

To use an `out` parameter, both the method definition and the calling method must explicitly use the `out` keyword.

```
```csharp
int number = 1;
Console.WriteLine("Before AddByRef: " + number); // number = 1
AddOneByRef(ref number);
Console.WriteLine("After AddByRef: " + number); // number = 2
SetByOut(out number);
Console.WriteLine("After SetByOut: " + number); // number = 34

void AddOneByRef(ref int value)
{
```
```