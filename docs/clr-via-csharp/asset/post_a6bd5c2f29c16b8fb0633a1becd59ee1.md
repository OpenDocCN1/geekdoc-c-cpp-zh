
The **ReliabilityContractAttribute** looks like this:

```csharp
public sealed class ReliabilityContractAttribute : Attribute {
    public ReliabilityContractAttribute(Consistency consistencyGuarantee, Cer cer);
    public Cer Cer { get; }
    public Consistency ConsistencyGuarantee { get; }
}
```

This attribute lets a developer document the reliability contract of a particular method⁹ to the method's potential callers. Both the **Cer** and **Consistency** types are enumerated types defined as follows:

```csharp
enum Consistency {
    MayCorruptProcess, MayCorruptAppDomain, MayCorruptInstance, WillNotCorruptState
}
```

```csharp
enum Cer { None, MayFail, Success }
```

If the method you are writing promises not to corrupt any state, use **Consistency.WillNotCorruptState**. Otherwise, document what your method does by using one of the other three possible values that match whatever state your method might corrupt. If the method that you are writing promises not to fail, use **Cer.Success**. Otherwise, use **Cer.MayFail**. Any method that does not have the **ReliabilityContractAttribute** applied to it is equivalent to being marked like this:

```csharp
[ReliabilityContract(Consistency.MayCorruptProcess, Cer.None)]
```

The **Cer.None** value indicates that the method makes no CER guarantees. In other words, it wasn't written with CERs in mind; therefore, it may fail and it may or may not report that it failed. Remember that most of these settings are giving a method a way to document what it offers to potential callers so that they know what to expect. The CLR and JIT compiler do not use this information.

When you want to write a reliable method, make it small and constrain what it does. Make sure that it doesn't allocate any objects (no boxing, for example), don't call any virtual methods or interface methods, don't use any delegates, or don't use reflection because the JIT compiler can't tell what method will actually be called. However, you can manually prepare these methods by calling one of these methods defined by the **RuntimeHelpers** class:

```csharp
public static void PrepareMethod(RuntimeMethodHandle method);
public static void PrepareMethod(RuntimeMethodHandle method,
    RuntimeTypeHandle[] instantiation);
public static void PrepareDelegate(Delegate d);
public static void PrepareContractedDelegate(Delegate d);
```

> **Note** Even if all the methods are eagerly prepared, a method call could still result in a **StackOverflowException**. When the CLR is not being hosted, a **StackOverflowException** causes the process to terminate immediately by the CLR internally calling **Environment.FailFast**. When hosted, the **PrepareConstrainedRegions** method checks the stack to see if there is approximately 48KB of stack space remaining. If there is limited stack space, the **StackOverflowException** occurs before entering the **try** block.

You should also look at **RuntimeHelpers' ExecuteCodeWithGuaranteedCleanup** method which is another way to execute code with guaranteed cleanup:

```csharp
public static void ExecuteCodeWithGuaranteedCleanup(TryCode code, CleanupCode backoutCode,
    Object userData);
```

When calling this method, you pass the body of the **try** and **finally** block as callback methods whose prototypes match these two delegates respectively:

```csharp
public delegate void TryCode(Object userData);
public delegate void CleanupCode(Object userData, Boolean exceptionThrown);
```

And finally, another way to get guaranteed code execution is to use the **CriticalFinalizerObject** class which is explained in great detail in Chapter 21.

## Code Contracts

Code contracts provide a way for you to declaratively document design decisions that you've made about your code within the code itself. The contracts take the form of:

- **Preconditions** Typically used to validate arguments.
- **Postconditions** Used to validate state when a method terminates either due to a normal return or due to throwing an exception.
- **Object Invariants** Used to ensure an object's fields remain in a good state through an object's entire lifetime.

Code contracts facilitate code usage, understanding, evolution, testing^{10}, documentation, and early error detection. You can think of preconditions, postconditions, and object invariants as parts of a method's signature. As such, you can loosen a contract with a new version of your code, but you cannot make a contract stricter with a new version without breaking backward compatibility.

At the heart of the code contracts is the static **System.Diagnostics.Contracts.Contract** class:

```csharp
public static class Contract {
    // Precondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Requires(Boolean condition);
    public static void EndContractBlock();

    // Preconditions: Always
    public static void Requires<TException>(Boolean condition) where TException : Exception;

    // Postcondition methods: [Conditional("CONTRACTS_FULL")]
    public static void Ensures(Boolean condition);
    public static void EnsuresOnThrow<TException>(Boolean condition)
        where TException : Exception;

    // Special Postcondition methods: Always
    public static T Result<T>();
    public static T OldValue<T>(T value);
    public static T ValueAtReturn<T>(out T value);

    // Object Invariant methods: [Conditional("CONTRACTS_FULL")]
    public static void Invariant(Boolean condition);

    // Quantifier methods: Always
    public static Boolean Exists<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean Exists(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);
    public static Boolean ForAll<T>(IEnumerable<T> collection, Predicate<T> predicate);
    public static Boolean ForAll(Int32 fromInclusive, Int32 toExclusive,
        Predicate<Int32> predicate);

    // Helper methods: [Conditional("CONTRACTS_FULL")] or [Conditional("DEBUG")]
    public static void Assert(Boolean condition);
    public static void Assume(Boolean condition);

    // Infrastructure event: usually your code will not use this event
    public static event EventHandler<ContractFailedEventArgs> ContractFailed;
}
```

As indicated above, many of these static methods have the **[Conditional("CONTRACTS_FULL")]** attribute applied to them. Some of the helper methods also have the **[Conditional("DEBUG")]** attribute applied to them. This means that the compiler will ignore any code you write that calls these methods unless the appropriate symbol is defined when compiling your code. Any methods marked with “Always” mean that the compiler always emits code to call the method. Also, the **Requires**, **`Requires<TException>`**, **Ensures**, **EnsuresOnThrow**, **Invariant**, **Assert**, and **Assume** methods have an additional overload (not shown) that takes a **String** message argument so you can explicitly specify a string message that should appear when the contract is violated.

By default, contracts merely serve as documentation as you would not define the **CONTRACTS_FULL** symbol when you build your project. In order to get some additional value out of using contracts, you must download additional tools and a Visual Studio property pane from http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx. The reason why all the code contract tools are not included with Visual Studio is because this technology is relatively new and is being improved rapidly. Microsoft's DevLabs Web site can offer new versions and improvements more quickly than Visual Studio itself. After downloading and installing the additional tools, you will see your projects have a new property pane available to them, as shown in Figure 20-9.

![](img/3c46ff5b170881db4209d365b1f7a808_531_0.png)

**FIGURE 20-9** The Code Contracts pane for a Visual Studio project

To turn on code contract features, select the Perform Runtime Contract Checking check box and select Full from the combo box next to it. This defines the **CONTRACTS_FULL** symbol when you build your project and invokes the appropriate tools (described shortly) after building your project. Now, at runtime, when a contract is violated, **Contract's ContractFailed** event is raised. Usually, developers do not register any methods with this event, but if you do, then any methods you register will receive a **ContractFailedEventArgs** object that looks like this:

```csharp
public sealed class ContractFailedEventArgs : EventArgs {
    public ContractFailedEventArgs(ContractFailureKind failureKind,
        String message, String condition, Exception originalException);

    public ContractFailureKind FailureKind     { get; }
    public String               Message        { get; }
    public String               Condition      { get; }
    public Exception            OriginalException { get; }

    public Boolean Handled { get; }     // true if any handler called SetHandled
    public void SetHandled();           // Call to ignore the violation; sets Handled to true

    public Boolean Unwind { get; }      // true if any handler called SetUnwind or threw
    public void SetUnwind();            // Call to force ContractException; set Unwind to true
}
```
