
# Using Delegates to Call Back Static Methods

Now that you understand how the Counter method is designed and how it works, let’s see how to use delegates to call back static methods. The StaticDelegateDemo method that appears in the previous code sample is the focus of this section.

The StaticDelegateDemo method calls the Counter method, passing null in the third parameter, which corresponds to Counter’s fb parameter. Because Counter’s fb parameter receives null, each item is processed without calling any callback method.

Next, the StaticDelegateDemo method calls Counter a second time, passing a newly constructed Feedback delegate object in the third parameter of the method call. This delegate object is a wrapper around a method, allowing the method to be called back indirectly via the wrapper. In this example, the name of the static method, Program.FeedbackToConsole, is passed to the Feedback type’s constructor, indicating that it is the method to be wrapped. The reference returned from the new operator is passed to Counter as its third parameter. Now when Counter executes, it will call the Program type’s static FeedbackToConsole method for each item in the series. FeedbackToConsole simply writes a string to the console indicating the item being processed.

**Note** The FeedbackToConsole method is defined as private inside the Program type, but the Counter method is able to call Program’s private method. In this case, you might not expect a problem because both Counter and FeedbackToConsole are defined in the same type. However, this code would work just fine even if the Counter method was defined in another type. In short, it is not a security or accessibility violation for one type to have code that calls another type’s private member via a delegate as long as the delegate object is created by code that has ample security/accessibility.

The third call to Counter in the StaticDelegateDemo method is almost identical to the second call. The only difference is that the Feedback delegate object wraps the static Program.FeedbackToMsgBox method. FeedbackToMsgBox builds a string indicating the item being processed. This string is then displayed in a message box.

Everything in this example is type-safe. For instance, when constructing a Feedback delegate object, the compiler ensures that the signatures of Program’s FeedbackToConsole and FeedbackToMsgBox methods are compatible with the signature defined by the Feedback delegate. Specifically, both methods must take one argument (an Int32), and both methods must have the same return type (void). If FeedbackToConsole had been defined like this:

```csharp
private static Boolean FeedbackToConsole(String value) {
    ...
}
```

the C# compiler wouldn’t compile the code and would issue the following error: error CS0123: No overload for 'FeedbackToConsole' matches delegate 'Feedback'.

The FeedbackToFile method works as the FeedbackToConsole and FeedbackToMsgBox methods, except that it opens a file and appends the string to the end of the file. (The Status file that the method creates can be found in the application's AppBase directory.)

Again, the purpose of this example is to demonstrate that delegates can wrap calls to instance methods as well as static methods. For instance methods, the delegate needs to know the instance of the object the method is going to operate on. Wrapping an instance method is useful because code inside the object can access the object's instance members. This means that the object can have some state that can be used while the callback method is doing its processing.

## Demystifying Delegates

On the surface, delegates seem easy to use: you define them by using C#'s delegate keyword, you construct instances of them by using the familiar new operator, and you invoke the callback by using the familiar method-call syntax (except instead of a method name, you use the variable that refers to the delegate object).

However, what's really going on is quite a bit more complex than what the earlier examples illustrate. The compilers and the CLR do a lot of behind-the-scenes processing to hide the complexity. In this section, I'll focus on how the compiler and the CLR work together to implement delegates. Having this knowledge will improve your understanding of delegates and will teach you how to use them effectively and efficiently. I'll also touch on some additional features delegates make available.

Let's start by reexamining this line of code.

```csharp
internal delegate void Feedback(Int32 value);
```

When the compiler sees this line, it actually defines a complete class that looks something like this.

```csharp
internal class Feedback : System.MulticastDelegate {
    // Constructor
    public Feedback(Object @object, IntPtr method);

    // Method with same prototype as specified by the source code
    public virtual void Invoke(Int32 value);

    // Methods allowing the callback to be called asynchronously
    public virtual IAsyncResult BeginInvoke(Int32 value,
        AsyncCallback callback, Object @object);
    public virtual void EndInvoke(IAsyncResult result);
}
```

The class defined by the compiler has four methods: a constructor, Invoke, BeginInvoke, and EndInvoke. In this chapter, I'll concentrate on the constructor and Invoke methods. The BeginInvoke and EndInvoke methods are related to the .NET Framework's Asynchronous Programming Model which is now considered obsolete and has been replaced by tasks that I discuss in Chapter 27, "Compute-Bound Asynchronous Operations."

In fact, you can verify that the compiler did indeed generate this class automatically by examining the resulting assembly with ILDasm.exe, as shown in Figure 17-1.

![](img/857bdf6cef9e242b53a37f88df9a1287_422_0.png)

FIGURE 17-1 ILDasm.exe showing the metadata produced by the compiler for the delegate.

In this example, the compiler has defined a class called Feedback that is derived from the System.MulticastDelegate type defined in the Framework Class Library (FCL). (All delegate types are derived from MulticastDelegate.)

> **Important** The System.MulticastDelegate class is derived from System.Delegate, which is itself derived from System.Object. The reason why there are two delegate classes is historical and unfortunate; there should be just one delegate class in the FCL. Sadly, you need to be aware of both of these classes because even though all delegate types you create have MulticastDelegate as a base class, you'll occasionally manipulate your delegate types by using methods defined by the Delegate class instead of the MulticastDelegate class. For example, the Delegate class has static methods called Combine and Remove. (I explain what these methods do later.) The signatures for both of these methods indicate that they take Delegate parameters. Because your delegate type is derived from MulticastDelegate, which is derived from Delegate, instances of your delegate type can be passed to these methods.

The class has private visibility because the delegate is declared as internal in the source code. If the source code had indicated public visibility, the Feedback class the compiler generated would also be public. You should be aware that delegate types can be defined within a type (nested within another type) or at global scope. Basically, because delegates are classes, a delegate can be defined anywhere a class can be defined.

Because all delegate types are derived from MulticastDelegate, they inherit MulticastDelegate's fields, properties, and methods. Of all of these members, three non-public fields are probably most significant. Table 17-1 describes these significant fields.

Now that you know how delegate objects are constructed and what their internal structure looks like, let's talk about how the callback method is invoked. For convenience, I've repeated the code for the Counter method here.

```csharp
private static void Counter(Int32 from, Int32 to, Feedback fb) {
    for (Int32 val = from; val <= to; val++) {
        // If any callbacks are specified, call them
        if (fb != null)
            fb(val);
    }
}
```

Look at the line of code just below the comment. The if statement first checks to see if fb is not null. If fb is not null, on the next line, you see the code that invokes the callback method. The null check is required because fb is really just a variable that can refer to a Feedback delegate object; it could also be null. It might seem as if I'm calling a function named fb and passing it one parameter (val). However, there is no function called fb. Again, because it knows that fb is a variable that refers to a delegate object, the compiler generates code to call the delegate object's Invoke method. In other words, the compiler sees the following.

```csharp
fb(val);
```

But the compiler generates code as though the source code said the following.

```csharp
fb.Invoke(val);
```

You can verify that the compiler produces code to call the delegate type's Invoke method by using ILDasm.exe to examine the Intermediate Language (IL) code created for the Counter method. Here is the IL for the Counter method. The instruction at IL_0009 in the figure indicates the call to Feedback's Invoke method.

```il
.method private hidebysig static void Counter(int32 from,
                                              int32 'to',
                                              class Feedback fb) cil managed
{
    // Code size       23 (0x17)
    .maxstack  2
    .locals init (int32 val)
    IL_0000:  ldarg.0
    IL_0001:  stloc.0
    IL_0002:  br.s       IL_0012
    IL_0004:  ldarg.2
    IL_0005:  brfalse.s  IL_000e
    IL_0007:  ldarg.2
    IL_0008:  ldloc.0
    IL_0009:  callvirt   instance void Feedback::Invoke(int32)
    IL_000e:  ldloc.0
    IL_000f:  ldc.i4.1
    IL_0010:  add
    IL_0011:  stloc.0
    IL_0012:  ldloc.0
    IL_0013:  ldarg.1
    IL_0014:  ble.s      IL_0004
    IL_0016:  ret
} // end of method Program::Counter
```
