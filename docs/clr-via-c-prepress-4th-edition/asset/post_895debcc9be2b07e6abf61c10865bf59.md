
```csharp
Int32[] squares = new Int32[numToDo];
AutoResetEvent done = new AutoResetEvent(false);

// Do a bunch of tasks on other threads
for (Int32 n = 0; n < squares.Length; n++) {
    ThreadPool.QueueUserWorkItem(
        obj => {
            Int32 num = (Int32) obj;

            // This task would normally be more time consuming
            squares[num] = num * num;

            // If last task, let main thread continue running
            if (Interlocked.Decrement(ref numToDo) == 0)
                done.Set();
        },
        n);
}

// Wait for all the other threads to finish
done.WaitOne();

// Show the results
for (Int32 n = 0; n < squares.Length; n++)
    Console.WriteLine("Index {0}, Square={1}", n, squares[n]);
}
```

This example really shows off how easy C# makes implementing what used to be a pretty complex task. The method above defines one parameter, numToDo, and two local variables, squares and done. And the body of the lambda expression refers to these variables.

Now imagine that the code in the body of the lambda expression is placed in a separate method (as is required by the CLR). How would the values of the variables be passed to the separate method? The only way to do this is to define a new helper class that also defines a field for each value that you want passed to the callback code. In addition, the callback code would have to be defined as an instance method in this helper class. Then, the UsingLocalVariablesInTheCallbackCode method would have to construct an instance of the helper class, initialize the fields from the values in its local variables, and then construct the delegate object bound to the helper object/instance method.

**Note**  When a lambda expression causes the compiler to generate a class with parameter/local variables that it modifies, the lifetime of the objects that the variables refer to is lengthened. Usually, a parameter/local variable goes out of scope at the last usage of the variable within a method. However, turning the variable into a field causes the field to keep the object that it refers to alive for the whole lifetime of the object containing the field. This is not a big deal in most applications, but it is something that you should be aware of.

This is very tedious and error-prone work, and, of course, the C# compiler does all this for you automatically. When you write the code shown above, it’s as if the C# compiler rewrites your code so that it looks something like this (comments inserted by me):

```csharp
internal sealed class AClass {
    public static void UsingLocalVariablesInTheCallbackCode(Int32 numToDo) {

        // Some local variables
        WaitCallback callback1 = null;

        // Construct an instance of the helper class
        <>c__DisplayClass2 class1 = new <>c__DisplayClass2();

        // Initialize the helper class's fields
        class1.numToDo = numToDo;
        class1.squares = new Int32[class1.numToDo];
        class1.done = new AutoResetEvent(false);

        // Do a bunch of tasks on other threads
        for (Int32 n = 0; n < class1.squares.Length; n++) {
            if (callback1 == null) {
                // New up delegate object bound to the helper object and
                // its anonymous instance method
                callback1 = new WaitCallback(
                    class1.<UsingLocalVariablesInTheCallbackCode>b__0);
            }

            ThreadPool.QueueUserWorkItem(callback1, n);
        }

        // Wait for all the other threads to finish
        class1.done.WaitOne();

        // Show the results
        for (Int32 n = 0; n < class1.squares.Length; n++)
            Console.WriteLine("Index {0}, Square={1}", n, class1.squares[n]);
    }

    // The helper class is given a strange name to avoid potential
    // conflicts and is private to forbid access from outside AClass
    [CompilerGenerated]
    private sealed class <>c__DisplayClass2 : Object {

        // One public field per local variable used in the callback code
        public Int32[] squares;
        public Int32 numToDo;
        public AutoResetEvent done;

        // public parameterless constructor
        public <>c__DisplayClass2() { }

        // Public instance method containing the callback code
        public void <UsingLocalVariablesInTheCallbackCode>b__0(Object obj) {
            Int32 num = (Int32) obj;
            squares[num] = num * num;
            if (Interlocked.Decrement(ref numToDo) == 0)
                done.Set();
        }
    }
}
```

callback method.

Fortunately, `System.Reflection.MethodInfo` offers a `CreateDelegate` method that allows you to create a delegate when you just don’t have all the necessary information about the delegate at compile time. Here are the method overloads that `MethodInfo` defines:

```csharp
public abstract class MethodInfo : MethodBase {
    // Construct a delegate wrapping a static method.
    public virtual Delegate CreateDelegate(Type delegateType);

    // Construct a delegate wrapping an instance method; target refers to the ‘this’ argument.
    public virtual Delegate CreateDelegate(Type delegateType, object target);
}
```

Once you’ve created the delegate, you can call it by using `Delegate`’s `DynamicInvoke` method which looks like this:

```csharp
public abstract class Delegate {
    // Invoke a delegate passing it parameters
    public Object DynamicInvoke(params Object[] args);
}
```

Using reflection APIs (discussed in Chapter 23, “Assembly Loading and Reflection”), you must first acquire a `MethodInfo` object referring to the method you want to create a delegate to. Then, you call the `CreateDelegate` method to have it construct a new object of a `Delegate`-derived type identified by the first parameter, `delegateType`. If the delegate wraps an instance method, you will also pass to `CreateDelegate` a target parameter indicating the object that should be passed as the parameter to the instance method.

`System.Delegate`’s `DynamicInvoke` method allows you to invoke a delegate object’s callback method, passing a set of parameters that you determine at runtime. When you call `DynamicInvoke`, it internally ensures that the parameters you pass are compatible with the parameters the callback method expects. If they’re compatible, the callback method is called. If they’re not, an `ArgumentException` is thrown. `DynamicInvoke` returns the object the callback method returned.

The following code shows how to use the `CreateDelegate` and `DynamicInvoke` methods:

```csharp
using System;
using System.Reflection;
using System.IO;

// Here are some different delegate definitions
internal delegate Object TwoInts2(Int32 n1, Int32 n2);
internal delegate Object OneString(String s1);

public static class DelegateReflection {
    public static void Main(String[] args) {
        if (args.Length < 2) {
            String usage =
}

try {
    // Invoke the delegate and show the result
    Object result = d.DynamicInvoke(callbackArgs);
    Console.WriteLine("Result = " + result);
}
catch (TargetParameterCountException) {
    Console.WriteLine("Incorrect number of parameters specified.");
}

// This callback method takes 2 Int32 arguments
private static Object Add(Int32 n1, Int32 n2) {
    return n1 + n2;
}

// This callback method takes 2 Int32 arguments
private static Object Subtract(Int32 n1, Int32 n2) {
    return n1 - n2;
}

// This callback method takes 1 String argument
private static Object NumChars(String s1) {
    return s1.Length;
}

// This callback method takes 1 String argument
private static Object Reverse(String s1) {
    return new String(s1.Reverse().ToArray());
}

}
```

## Chapter 18: Custom Attributes

In this chapter:

- Using Custom Attributes 435
- Defining Your Own Attribute Class 439
- Attribute Constructor and Field/Property Data Types 443
- Detecting the Use of a Custom Attribute 444
- Matching Two Attribute Instances Against Each Other 448
- Detecting the Use of a Custom Attribute Without Creating Attribute-Derived Objects 451
- Conditional Attribute Classes 454

In this chapter, I’ll discuss one of the most innovative features the Microsoft .NET Framework has to offer: *custom attributes*. Custom attributes allow you to declaratively annotate your code constructs, thereby enabling special features. Custom attributes allow information to be defined and applied to almost any metadata table entry. This extensible metadata information can be queried at runtime to dynamically alter the way code executes. As you use the various .NET Framework technologies (Windows Forms, WPF, WCF, and so on), you’ll see that they all take advantage of custom attributes, allowing developers to express their intentions within code very easily. A solid understanding of custom attributes is necessary for any .NET Framework developer.
