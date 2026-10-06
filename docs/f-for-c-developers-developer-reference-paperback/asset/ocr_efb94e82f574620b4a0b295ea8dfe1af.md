# Using a Wrapper Type Provider

Imagine that you have a sealed class and need to add some logic for each member function, such as logging the function usage. The most common technique for a C# developer is to write a wrapper with the sealed class instance as a variable, as shown in Listing 5-26. It would be a tedious and boring task to refactor the sealed class. Reflection can be an option, but the performance impact of this approach is something cannot be ignored.

**LISTING 5-26** Wrapper class to expand a sealed class

```
// sealed class A
public sealed class A
{
    public void F1() { ... }
}

// new class to add logging function around the F1 defined in sealed class A
public class MyClass
{
    private A a = new A();
    public void F1()
    {
        LogBefore();
        a.F1();
        LogAfter();
    }
}
```

A custom type provider is another way to perform meta-programming, and it has a performance advantage over reflection. The type provider logic is simple:

+   - Generate the same method with the same function name and signature.
- In the function implementation, first invoke the LogBefore method, then invoke the base class; and finally invoke the LogAfter method.

As usual, the way to invoke the type provider is defined first, as you can see in Listing 5-27. The sealed class and the logging function are defined in Listing 5-28.

**LISTING 5-27** Invoking the wrapper type provider and the expected result

```
# r@"\bin\Debug\ShareInfoTypeProvider.dll"

type T = Samples.ShareInfo.TPTest;
let t = T()

//invoke F1 and also output logging info
t.F1("hello")
```