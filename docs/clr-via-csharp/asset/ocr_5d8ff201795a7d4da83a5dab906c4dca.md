```
```csharp
// If last task, let main thread continue running
if (Interlocked.Decrement(ref numToDo) == 0)
    done.Set();
},
n);

// Wait for all the other threads to finish
done.WaitOne();

// Show the results
for (Int32 n = 0; n < squares.Length; n++)
    Console.WriteLine("Index {0}, Square={1}", n, squares[n]);
}
```
```

This example really shows off how easy C# makes implementing what used to be a pretty complex task. The method above defines one parameter, **numToDo**, and two local variables, **squares** and **done**. And the body of the lambda expression refers to these variables.

Now imagine that the code in the body of the lambda expression is placed in a separate method (as is required by the CLR). How would the values of the variables be passed to the separate method? The only way to do this is to define a new helper class that also defines a field for each value that you want passed to the callback code. In addition, the callback code would have to be defined as an instance method in this helper class. Then, the **UsingLocalVariablesInTheCallBackCode** method would have to construct an instance of the helper class, initialize the fields from the values in its local variables, and then construct the delegate object bound to the helper object/instance method.

> > **Note**   When a lambda expression causes the compiler to generate a class with parameter/local variables turned into fields, the lifetime of the objects that the variables refer to are lengthened. Usually, a parameter/local variable goes out of scope at the last usage of the variable within a method. However, turning the variable into a field causes the field to keep the object that it refers to alive for the whole lifetime of the object containing the field. This is not a big deal in most applications, but it is something that you should be aware of.

This is very tedious and error-prone work, and, of course, the C# compiler does all this for you automatically. When you write the code shown above, it's as if the C# compiler rewrites your code so that it looks something like this (comments inserted by me):

```
```csharp
internal sealed class AClass {
    public static void UsingLocalVariablesInTheCallBackCode(Int32 numToDo) {

        // Some local variables
        WaitCallback callBack1 = null;

        // Construct an instance of the helper class
        <>c__DisplayClass2 class1 = new <>c__DisplayClass2();
```
```