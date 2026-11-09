If the CallbackWithoutNewingADelegateObject method had not been static, the anonymous method's code could contain references to instance members. If it doesn't contain references to instance members, the compiler will still produce a static anonymous method because this is more efficient than an instance method because the additional this's parameter is not necessary. But, if the anonymous method's code does reference an instance member, the compiler will produce a nonstatic anonymous method.

```
~~~csharp
internal sealed class AClass {
    private String m_name;   // An instance field

    // An instance method
    public void CallbackWithoutNewingADelegateObject() {
        ThreadPool.QueueUserWorkItem(
            // The callback code can reference instance members.
            obj => Console.WriteLine(m_name + ": " + obj),
            5);
    }
}
~~~
```

On the left side of the => operator is where you specify the names of any arguments that are to be passed to the lambda expression. There are some rules you must follow here. See the following examples.

```
~~~csharp
// If the delegate takes no arguments, use ()
Func<String> f = () => "Jeff";

// If the delegate takes 1+ arguments, you can explicitly specify the types
Func<Int32, String> f2 = (Int32 n) => n.ToString();
Func<Int32, Int32, String> f3 = (Int32 n1, Int32 n2) => (n1 + n2).ToString();

// If the delegate takes 1+ arguments, the compiler can infer the types
Func<Int32, String> f4 = (n) => n.ToString();
Func<Int32, Int32, String> f5 = (n1, n2) => (n1 + n2).ToString();

// If the delegate takes 1 argument, you can omit the ()s
Func<Int32, String> f6 = n => n.ToString();

// If the delegate has ref/out arguments, you must explicitly specify ref/out and the type
Bar b = (out Int32 n) => n = 5;
~~~
```

For the last example, assume that Bar is defined as follows.

```
~~~csharp
delegate void Bar(out Int32 z);
~~~
```

On the right side of the => operator is where you specify the anonymous function body. It is very common for the body to consist of a simple or complex expression that ultimately returns a non-void value. In the preceding code, I was assigning lambda expressions that returned Strings to all the Func delegate variables. It is also quite common for the body to consist of a single statement. An example of this is when I called ThreadPool.QueueUserWorkItem, passing it a lambda expression that called Console.WriteLine (which returns void).