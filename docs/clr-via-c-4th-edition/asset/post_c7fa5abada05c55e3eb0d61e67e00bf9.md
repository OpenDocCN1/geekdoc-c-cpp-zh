
or ARM processor. Also, JIT compilers associated with other CLR implementations (such as Microsoft's .NET Compact Framework or the open-source Mono project) are likely to produce different code.

Actually, I've been able to test some of my own code with a few different JIT compilers that Microsoft has internally, and the difference in performance that I've observed has been quite dramatic and surprising. The point is that you must test your code on the various platforms that you expect your users to run on, and make changes accordingly. Again, I wouldn't worry about the performance of using exception handling; the benefits typically far outweigh any negative performance impact.

If you're interested in seeing how exception handling impacts the performance of your code, you can use the Performance Monitor tool that comes with Windows. The screen in Figure 20-8 shows the exception-related counters that are installed along with the .NET Framework.

![](img/857bdf6cef9e242b53a37f88df9a1287_518_0.png)

FIGURE 20-8 Performance Monitor showing the .NET CLR Exceptions counters.

Occasionally, you come across a method that you call frequently that has a high failure rate. In this situation, the performance hit of having exceptions thrown can be intolerable. For example, Microsoft heard back from several customers who were calling Int32's Parse method, frequently passing in data entered from an end user that could not be parsed. Because Parse was called frequently, the performance hit of throwing and catching the exceptions was taking a large toll on the application's overall performance.

To address customers' concerns and to satisfy all the guidelines described in this chapter, Microsoft added a new method to the Int32 class. This new method is called TryParse, and it has two overloads that look like the following.

```csharp
public static Boolean TryParse(String s, out Int32 result);
public static Boolean TryParse(String s, NumberStyles styles,
    IFormatProvider provider, out Int32 result);
```

You’ll notice that these methods return a Boolean that indicates whether the String passed in contains characters that can be parsed into an Int32. These methods also return an output parameter named result. If the methods return true, result will contain the result of parsing the string into a 32-bit integer. If the methods return false, result will contain 0, but you really shouldn’t execute any code that looks at it anyway.

One thing I want to make absolutely clear: A TryXxx method’s Boolean return value returns false to indicate one and only one type of failure. The method should still throw exceptions for any other type of failure. For example, Int32’s TryParse throws an ArgumentException if the style argument is not valid, and it is certainly still possible to have an OutOfMemoryException thrown when calling TryParse.

I also want to make it clear that object-oriented programming allows programmers to be productive. One way that it does this is by not exposing error codes in a type’s members. In other words, constructors, methods, properties, etc. are all defined with the idea that calling them won’t fail. And, if defined correctly, for most uses of a member, it will not fail, and there will be no performance hit because an exception will not be thrown.

When defining types and their members, you should define the members so that it is unlikely that they will fail for the common scenarios in which you expect your types to be used. If you later hear from users that they are dissatisfied with the performance due to exceptions being thrown, then and only then should you consider adding TryXxx methods. In other words, you should produce the best object model first and then, if users push back, add some TryXxx methods to your type so that the users who experience performance trouble can benefit. Users who are not experiencing performance trouble should continue to use the non-TryXxx versions of the methods because this is the better object model.

### Constrained Execution Regions (CERs)

Many applications don’t need to be robust and recover from any and all kinds of failures. This is true of many client applications like Notepad.exe and Calc.exe. And, of course, many of us have seen Microsoft Office applications like WinWord.exe, Excel.exe, and Outlook.exe terminate due to unhandled exceptions. Also, many server-side applications, like web servers, are stateless and are automatically restarted if they fail due to an unhandled exception. Of course some servers, like SQL Server, are all about state management and having data lost due to an unhandled exception is potentially much more disastrous.

In the CLR, we have AppDomains (discussed in Chapter 22), which contain state. When an AppDomain is unloaded, all its state is unloaded. And so, if a thread in an AppDomain experiences an unhandled exception, it is OK to unload the AppDomain (which destroys all its state) without terminating the whole process.8

8 This is definitely true if the thread lives its whole life inside a single AppDomain (like in the ASP.NET and managed SQL Server stored procedure scenarios). But you might have to terminate the whole process if a thread crosses AppDomain boundaries during its lifetime.

By definition, a CER is a block of code that must be resilient to failure. Because AppDomains can be unloaded, destroying their state, CERs are typically used to manipulate any state that is shared by multiple AppDomains or processes. CERs are useful when trying to maintain state in the face of exceptions that get thrown unexpectedly. Sometimes we refer to these kinds of exceptions as *asynchronous exceptions*. For example, when calling a method, the CLR has to load an assembly, create a type object in the AppDomain's loader heap, call the type's static constructor, JIT IL into native code, and so on. Any of these operations could fail, and the CLR reports the failure by throwing an exception.

If any of these operations fail within a `catch` or `finally` block, then your error recovery or cleanup code won't execute in its entirety. Here is an example of code that exhibits the potential problem.

```csharp
private static void Demo1() {
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type1's static constructor is implicitly called in here
        Type1.M();
    }
}

private sealed class Type1 {
    static Type1() {
        // if this throws an exception, M won't get called
        Console.WriteLine("Type1's static ctor called");
    }

    public static void M() { }
}
```

When I run the preceding code, I get the following output.

```text
In try
Type1's static ctor called
```

What we want is to not even start executing the code in the preceding `try` block unless we know that the code in the associated `catch` and `finally` blocks is guaranteed (or as close as we can get to guaranteed) to execute. We can accomplish this by modifying the code as follows.

```csharp
private static void Demo2() {
    // Force the code in the finally to be eagerly prepared
    RuntimeHelpers.PrepareConstrainedRegions(); // System.Runtime.CompilerServices namespace
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type2's static constructor is implicitly called in here
        Type2.M();
    }
}

public class Type2 {
    static Type2() {
        Console.WriteLine("Type2's static ctor called");
    }

    // Use this attribute defined in the System.Runtime.ConstrainedExecution namespace
    [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
    public static void M() { }
}
```

Now, when I run this version of the code, I get the following output.

```text
Type2's static ctor called
In try
```

The `PrepareConstrainedRegions` method is a very special method. When the JIT compiler sees this method being called immediately before a `try` block, it will eagerly compile the code in the `try`'s `catch` and `finally` blocks. The JIT compiler will load any assemblies, create any type objects, invoke any static constructors, and JIT any methods. If any of these operations result in an exception, then the exception occurs *before* the thread enters the `try` block.

When the JIT compiler eagerly prepares methods, it also walks the entire call graph eagerly preparing called methods. However, the JIT compiler only prepares methods that have the `ReliabilityContractAttribute` applied to them with either `Consistency.WillNotCorruptState` or `Consistency.MayCorruptInstance` because the CLR can't make any guarantees about methods that might corrupt `AppDomain` or process state. Inside a `catch` or `finally` block that you are protecting with a call to `PrepareConstrainedRegions`, you want to make sure that you only call methods with the `ReliabilityContractAttribute` set as I've just described.

The `ReliabilityContractAttribute` looks like this.

```csharp
public sealed class ReliabilityContractAttribute : Attribute {
    public ReliabilityContractAttribute(Consistency consistencyGuarantee, Cer cer);
    public Cer Cer { get; }
    public Consistency ConsistencyGuarantee { get; }
}
```

This attribute lets a developer document the reliability contract of a particular method to the method's potential callers. Both the `Cer` and `Consistency` types are enumerated types defined as follows.⁹

```csharp
enum Consistency {
    MayCorruptProcess, MayCorruptAppDomain, MayCorruptInstance, WillNotCorruptState
}

enum Cer { None, MayFail, Success }
```

If the method you are writing promises not to corrupt any state, use `Consistency.WillNotCorruptState`. Otherwise, document what your method does by using one of the other three possible values that match whatever state your method might corrupt. If the method that you are writing

⁹ You can also apply this attribute to an interface, a constructor, a structure, a class, or an assembly to affect the members inside it.
