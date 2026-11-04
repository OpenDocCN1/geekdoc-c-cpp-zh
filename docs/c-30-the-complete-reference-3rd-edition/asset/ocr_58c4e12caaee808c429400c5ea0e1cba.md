static variable. A static variable is initialized before its class is used. If no explicit initializer is specified, it is initialized to zero for numeric types, null in the case of reference types, or false for variables of type bool. Thus, a static variable always has a value.

The difference between a static method and a normal method is that the static method can be called through its class name, without any instance of that class being created. You have seen an example of this already: the Sqrt() method, which is a static method within C#'s System.Math class.

Here is an example that declares a static variable and a static method:

```
// Use static.
using System;
class StaticDemo {
    // A static variable.
    public static int Val = 100;
    // A static method.
    public static int ValDiv2() {
        return Val/2;
    }
}
class SDemo {
    static void Main() {
        Console.WriteLine("Initial value of StaticDemo.Val is "
            + StaticDemo.Val);
        StaticDemo.Val = 8;
        Console.WriteLine("StaticDemo.Val is " + StaticDemo.Val);
        Console.WriteLine("StaticDemo.ValDiv2(): " +
            StaticDemo.ValDiv2());
    }
}
```

The output is shown here:

```
Initial value of StaticDemo.Val is 100
StaticDemo.Val is 8
StaticDemo.ValDiv2(): 4
```

As the output shows, a static variable is initialized before any object of its class is created.

There are several restrictions that apply to static methods:

+   - A static method does not have a this reference. This is because a static method does not execute relative to any object.
+   - A static method can directly call only other static methods of its class. It cannot directly call an instance method of its class. The reason is that instance methods operate on specific objects, but a static method is not called on an object. Thus, on what object would the static method operate?