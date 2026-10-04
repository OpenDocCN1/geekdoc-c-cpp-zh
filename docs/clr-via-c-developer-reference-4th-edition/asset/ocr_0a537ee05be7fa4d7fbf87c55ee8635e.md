```
// This task would normally be more time consuming
squares[num] = num * num;

// If last task, let main thread continue running
if (Interlocked.Decrement(ref numToDo) == 0)
{
    done.Set();
}

// Wait for all the other threads to finish
done.WaitOne();

// Show the results
for (Int32 n = 0; n < squares.Length; n++)
{
    Console.WriteLine("Index {0}, Square={1}", n, squares[n]);
}}
```

This example really shows-off how easy C# makes implementing what was used to be a pretty complex task. The preceding method defines one parameter, numToDo, and two local variables, squares and done. And how of the lambda expression refers to these variables.

Now imagine that the code in the body of the lambda expression is placed in a separate method (as required by the CLR). How would the values of variables be passed to the separate method? The only way to do this is to define a new helper class that also defines a field for each value that you passed to the callback code. In addition, the callback would have to be defined as an instance method in this helper class. Then, the UsingLocalVariablesInTheCallback method would have to construct an instance of the helper class, initialize the fields in its local variables, and construct the delegate object bound to the helper object/instance.

> Note When a lambda expression causes the callback to generate a class with parameter/local variables turned into fields, the lifetime of the objects that the variables refer to is lengthened. Usually, a parameter/local variable goes out of scope at the last usage of the variable within a method. However, turning the variable into a field causes the field to keep the object that it refers to alive for the whole lifetime of the object containing the field. This is not big deal in most applications, but it is something you should be aware of.

This is tedious and error-prone work, and of course, the C# compiler does all this for you automatically. When you are writing the code, it's as if the C# compiler rewrites your code so that it looks something the following (comments inserted by me).

```
internal sealed class Class {
    public static void UsingLocalVariablesInTheCallbackCode(Int32 numToDo) {

    // Some local variables
    WaitCallback1 = null;
}
```

![](bbox=[0.576, 0.068, 0.638, 0.114])