Although it is bad style for ToString to have side effects, the example demonstrates that no boxing occurred for the three invocations of x.ToString(). end example]

Similarly, boxing never implicitly occurs when accessing a member on a constrained type parameter when the member is implemented within the value type. For example, suppose an interface ICounter contains a method Increment, which can be used to modify a value. If ICounter is used as a constraint, the implementation of the Increment method is called with a reference to the variable that Increment was called on, never a boxed copy. [Example:

```
```csharp
using System;
interface ICounter
{
    void Increment();
}
struct Counter: ICounter
{
    int value;
    public override string ToString() {
        return value.ToString();
    }
    void ICounter.Increment() {
        value++;
    }
}
class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();  // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```
```

The first call to Increment modifies the value in the variable x. This is not equivalent to the second call to Increment, which modifies the value in a boxed copy of x. Thus, the output of the program is:

0
1
1

end example]

# 16.4.8 Field initializers

As described in §16.4.5, the default value of a struct consists of the value that results from setting all value type fields to their default value and all reference type fields to null. For this reason, a struct does not permit instance field declarations to include variable initializers. This restriction applies only to instance fields. Static fields of a struct are permitted to include variable initializers. [Example: The following

```
```csharp
struct Point
{
    public int x = 1; // Error, initializer not permitted
    public int y = 1; // Error, initializer not permitted
}
```
```

is in error because the instance field declarations include variable initializers. end example]