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
        x.Increment();            // Modify x
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

For further details on boxing and unboxing, see §4.3.

# 11.3.6 Meaning of this

Within an instance constructor or instance function member of a class, this is classified as a value. Thus, while this can be used to refer to the instance for which the function member was invoked, it is not possible to assign to this in a function member of a class.

Within an instance constructor of a struct, this corresponds to an out parameter of the struct type, and within an instance function member of a struct, this corresponds to a ref parameter of the struct type. In both cases, this is classified as a variable, and it is possible to modify the entire struct for which the function member was invoked by assigning to this or by passing this as a ref or out parameter.

# 11.3.7 Field initializers

As described in §11.3.4, the default value of a struct consists of the value that results from setting all value type fields to their default value and all reference type fields to null. For this reason, a struct does not permit instance field declarations to include variable initializers. This restriction applies only to instance fields. Static fields of a struct are permitted to include variable initializers.

The example