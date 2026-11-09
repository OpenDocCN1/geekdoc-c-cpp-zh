Finally, if you write the preceding code and compile it, it's as if the C# compiler rewrote your code to look like the following (comments inserted by me).

```
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
```

The lambda expression must match that of the WaitCallback delegate: it returns void and takes an Object parameter. However, I specified the name of the parameter by simply putting obj to the left of the => operator. On the right of the => operator, Console.WriteLine happens to return void. However, if I had placed an expression that did not return void, the compiler-generated code would just ignore the return value because the method that the compiler generates must have a void return type to satisfy the WaitCallback delegate.

It is also worth noting that the anonymous function is marked as private; this forbids any code not defined within the type from accessing the method (although reflection will reveal that the method does exist). Also, note that the anonymous method is marked as static; this is because the code doesn't access any instance members (which it can't because CallbackWithoutNewingADelegateObject is itself a static method). However, the code can reference any static fields or static methods defined within the class. Here is an example.

```
```csharp
internal sealed class AClass {
    private static String sm_name;  // A static field

    public static void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(
            // The callback code can reference static members.
            obj =>Console.WriteLine(sm_name + ": " + obj),
            5);
    }
}
```
```