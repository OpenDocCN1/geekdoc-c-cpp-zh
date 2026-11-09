
Finally, if you write the code shown above and compile it, it's as if the C# compiler rewrote your code to look like this (comments inserted by me):

```csharp
internal sealed class AClass {
    // This private field is created to cache the delegate object.
    // Pro: CallbackWithoutNewingADelegateObject will not create
    //      a new object each time it is called.
    // Con: The cached object never gets garbage collected
    [CompilerGenerated]
    private static WaitCallback <>9__CachedAnonymousMethodDelegate1;

    public static void CallbackWithoutNewingADelegateObject() {
        if (<>9__CachedAnonymousMethodDelegate1 == null) {
            // First time called, create the delegate object and cache it.
            <>9__CachedAnonymousMethodDelegate1 =
                new WaitCallback(<CallbackWithoutNewingADelegateObject>b__0);
        }
        ThreadPool.QueueUserWorkItem(<>9__CachedAnonymousMethodDelegate1, 5);
    }

    [CompilerGenerated]
    private static void <CallbackWithoutNewingADelegateObject>b__0(Object obj) {
        Console.WriteLine(obj);
    }
}
```

The lambda expression must match that of the WaitCallback delegate: it returns void and takes an Object parameter. However, I specified the name of the parameter by simply putting obj to the left of the => operator. On the right of the => operator, Console.WriteLine happens to return void. However, if I had placed an expression that did not return void, the compiler-generated code would just ignore the return value because the method that the compiler generates must have a void return type to satisfy the WaitCallback delegate.

It is also worth noting that the anonymous function is marked as private; this forbids any code not defined within the type from accessing the method (although reflection will reveal that the method does exist). Also, note that the anonymous method is marked as static; this is because the code doesn't access any instance members (which it can't, since CallbackWithoutNewingADelegateObject is itself a static method). However, the code can reference any static fields or static methods defined within the class. Here is an example:

```csharp
internal sealed class AClass {
    private static String s_name;   // A static field

    public static void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(
            // The callback code can reference static members.
            obj => Console.WriteLine(s_name + ": " + obj),
            5);
    }
}
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

This example really shows off how easy C# makes implementing what used to be a pretty complex task. The method above defines one parameter, **numToDo**, and two local variables, **squares** and **done**. And the body of the lambda expression refers to these variables.

Now imagine that the code in the body of the lambda expression is placed in a separate method (as is required by the CLR). How would the values of the variables be passed to the separate method? The only way to do this is to define a new helper class that also defines a field for each value that you want passed to the callback code. In addition, the callback code would have to be defined as an instance method in this helper class. Then, the **UsingLocalVariablesInTheCallBackCode** method would have to construct an instance of the helper class, initialize the fields from the values in its local variables, and then construct the delegate object bound to the helper object/instance method.

> **Note**   When a lambda expression causes the compiler to generate a class with parameter/local variables turned into fields, the lifetime of the objects that the variables refer to are lengthened. Usually, a parameter/local variable goes out of scope at the last usage of the variable within a method. However, turning the variable into a field causes the field to keep the object that it refers to alive for the whole lifetime of the object containing the field. This is not a big deal in most applications, but it is something that you should be aware of.

This is very tedious and error-prone work, and, of course, the C# compiler does all this for you automatically. When you write the code shown above, it's as if the C# compiler rewrites your code so that it looks something like this (comments inserted by me):

```csharp
internal sealed class AClass {
    public static void UsingLocalVariablesInTheCallBackCode(Int32 numToDo) {

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
                // Now delegate object bound to the helper object and
                // its anonymous instance method
                callback1 = new WaitCallback(
                    class1.<UsingLocalVariablesInTheCallBackCode>b__0);
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
        public void <UsingLocalVariablesInTheCallBackCode>b__0(Object obj) {
            Int32 num = (Int32) obj;
            squares[num] = num * num;
            if (Interlocked.Decrement(ref numToDo) == 0)
                done.Set();
        }
    }
}
```

> **Important** Without a doubt, it doesn't take much for programmers to start abusing C#'s lambda expression feature. When I first started using lambda expressions, it definitely took me some time to get used to them. After all, the code that you write in a method is not actually inside that method, and this also can make debugging and single-stepping through the code a bit more challenging. In fact, I'm amazed at how well the Microsoft Visual Studio debugger actually handles stepping through lambda expressions in my source code.
>
> I’ve set up a rule for myself: If I need my callback method to contain more than three lines of code, I will not use a lambda expression; instead, I’ll write the method manually and assign it a name of my own creation. But, used judiciously, lambda expressions can greatly increase programmer productivity as well as the maintainability of your code. Below is some code in which using lambda expressions feels very natural. Without them, this code would be tedious to write, harder to read, and harder to maintain.

```csharp
// Create and initialize a String array
String[] names = { "Jeff", "Kristin", "Aidan", "Grant" };

// Get just the names that have a lowercase 'a' in them.
Char charToFind = 'a';
names = Array.FindAll(names, name => name.IndexOf(charToFind) >= 0);

// Convert each string's characters to uppercase
names = Array.ConvertAll(names, name => name.ToUpper());

// Display the results
Array.ForEach(names, Console.WriteLine);
```

## Delegates and Reflection

So far in this chapter, the use of delegates has required the developer to know up front the prototype of the method that is to be called back. For example, if `fb` is a variable that references a `Feedback` delegate (see this chapter’s first program listing), to invoke the delegate, the code would look like this:

```csharp
fb(item);    // item is defined as Int32
```

As you can see, the developer must know when coding how many parameters the callback method requires and the types of those parameters. Fortunately, the developer almost always has this information, so writing code like the preceding code isn’t a problem.

In some rare circumstances, however, the developer doesn’t have this information at compile time. I showed an example of this in Chapter 11, “Events,” when I discussed the `EventSet` type. In this example, a dictionary maintained a set of different delegate types. At runtime, to raise an event, one of the delegates was looked up in the dictionary and invoked. At compile time, it wasn’t possible to know exactly which delegate would be called and which parameters were necessary to pass to the delegate’s callback method.

Fortunately, `System.Delegate` offers a few methods that allow you to create and invoke a delegate when you just don’t have all the necessary information about the delegate at compile time. Here are the corresponding methods that `Delegate` defines:

```csharp
public abstract class Delegate {
    // Construct a 'type' delegate wrapping the specified static method.
    public static Delegate CreateDelegate(Type type, MethodInfo method);
    public static Delegate CreateDelegate(Type type, MethodInfo method,
        Boolean throwOnBindFailure);
}
```
