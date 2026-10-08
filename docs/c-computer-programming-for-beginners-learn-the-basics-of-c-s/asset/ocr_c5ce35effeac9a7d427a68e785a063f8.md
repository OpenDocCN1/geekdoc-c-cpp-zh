one.

Creating custom attributes – The .Net framework allows creation of custom attributes that can be used to store declarative information that can be retrieved at run-time. Information can be related to any target element depending upon the design criteria and application need. (Tutorials Point)

# The Anonymous methods in C#

As described earlier delegates are used to reference methods that have the same signature as that of a delegate. This means that you can call a method that can be referenced by a delegate using that delegate object.

The anonymous methods provide a technique to pass a code block as a delegate parameter. These are the methods that only have the body, but no name. You need to specify the return type in an anonymous method; it is inferred from the return statement inside the method body.

The anonymous methods are declared with the creation of the delegate instance, with a delegate keyword. Example for anonymous method is as follows –

```
delegate void NumberChanger(int n);
```

```
...
NumberChanger nc = delegate(int x)
{
Console.WriteLine("Anonymous Method: {0}", x);
};
```

Here, the code block Console.WriteLine("Anonymous Method: {0}", x); is the body of anonymous method.

One of the programming features of C# is the Lambda expression. The Lambda expression is an anonymous method that you can use to create expression or delegate tree types. By using this expression, you can write local functions that can be passed