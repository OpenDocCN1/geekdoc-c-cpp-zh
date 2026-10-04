
There are several things you can do to help mitigate corruption:

- The CL doesn't allow a thread to be aborted when executing code inside a catch or finally block. so we could make the Transfer method more robust by doing the following.

```
public static void Transfer(Account from, Account to, Decimal amount) {
    try { /* do nothing in here */ }
    finally {
        from = amount;
        // now a abort (due to Thread.Abort/AppDomain.Unload) can't happen
        to += amount;
    }
}
```

However, it is absolutely not recommended that you write all your code in finally blocks! You should only use this technique for modifying extremely sensitive state.

- You can use the System.Diagnostics.Contracts to apply code contracts to your methods. Code contracts give you a way to validate arguments and other variables before you attempt to modify state using these arguments/variables. If the arguments/variables meet the contract, then the chance of corrupted state is minimized (not completely eliminated). If a contract fails, then an exception is thrown before any state has been modified. I will talk about code contracts later in this chapter.

- You can use constrained execution regions (CERs), which give you a way to take CLR uncertainty out of the picture. For example, before entering a try block, you can have the CLR load all assemblies needed by code in any associated catch and finally blocks. In addition, the CLR will compile all the code in catch and finally blocks including the methods called from within these blocks. This will eliminate a bunch of exceptions (including FileLoadException,FormatException, InvalidProgramException, FieldAccessException, MissingFieldException, MethodException) from occurring when trying to execute recovery code (in catch blocks) or cleanup code (in finally block). It will also reduce the potential for OutOfMemoryException and other exceptions as well. I will talk about CERs later in this chapter.

Depending on the state you live, you can use transactions to ensure that all state is modified or no state is modified. If the data is in a database, for example, transactions work well. Windows also supports transactional registry and file operations (on an NTFS volume only), so you might be able to use this; however the .NET Framework doesn't expose this functionality today. You will have to P/Invoke to native code to leverage it. The System.Transactions.Scope class for more details about this.

- You can design your methods to be more explicit. For example, the Monitor class is typically used for taking/releasing a thread lock as follows.

```
public static class SomeType {
    private static Object s_myLockObject = new Object();
```

```
public static void someMethod () {
    Monitor.Enter(s_myLockObject); // If this throws, did the lock get taken
    // not? If it did, then it won't get released!

    try {
        // Do thread-safe operation here...
    }
    finally {
        Monitor.Exit(s_myLockObject);
    }
}
// ...
}
```

Due to the problem just shown, the overload of the preceding Monitor's Enter method used is now discouraged, and it is recommended that you rewrite the code as follows.

```
public static class SomeType {
    private static Object s_myLockObject = new Object();
```

```
public static void someMethod () {
    Boolean lockTaken = false; // Assume the lock was not taken
    try {
        // This works unless an exception is thrown or not!
        Monitor.Enter(s_myLockObject, ref lockTaken);

// Do thread-safe operation here...
    }
    finally {
        // If the lock was taken, release it
        if (lockTaken) Monitor.Exit(s_myLockObject);
    }
}
// ...
}
```

The explicitness in this code is an improvement, in the case of thread synchronization locks, the recommendation is now to not use them with exception handling at all. See Chapter 30, "Hybrid Thread Synchronization Constructs," for more details about this.

If, in your code, you have determined that state has already been corrupted beyond repair, you should destroy any corrupted state so that it can cause no additional harm. Restart your application so your state initializes itself to a good condition and hopefully, the state corruption will not happen again. Because managed state cannot leak outside of an AppDomain, you can destroy any corrupted state that lives within an AppDomain by unloading the entire AppDomain by calling AppDomain's Unload method (Chapter 22 for details).

And, if you feel that your state is so bad that the whole process should be terminated, then you call Environment's static FailFast method.

```
public static void FailFast(String message);
public static void FailFast(String message, Exception exception);
```

This method terminates the process without running any active try/finally blocks or Finalize methods. This is good because executing more code while state is corrupted could easily make ters worse. However, FailFast will allow any CriticalFinalizer-derived objects, discussed in Chapter 21, "The Managed Heap and Garbage Collection," a chance to clean up. This is OK because they tend to close native resources, and Windows state is probably fine even the CLR's state or your application's state is corrupted. The FailFast writes the message string and any optional exception (usually the exception captured in a catch block) to the application event log, produces a Windows error report, creates a memory dump of your application, and terminates the current process.

> Important Most of the FCL code does not ensure that state remains in the case of an unexpected exception. If your code catches an exception that passes through FCL code and continues to use FCL objects, there is a chance that these objects will behave unpredictably. It's a shame that more FCL objects don't maintain their state better in the face of unexpected exceptions or call FailFast if their state cannot be restored.

The point of this discussion is to make aware of the potential problems related to using the CLR's exception-handling mechanism. Most applications cannot tolerate running with a corrupted state it leads to incorrect data and security holes. If you are writing an application that cannot tolerate (like an operating system or database engine), then managed code is ot a good technology to use. And although Microsoft Exchange Server is largely written in managed code, it uses a native database to store email messages. The native database is called the Extensible Storage Engine; it ships with Windows, and can be found at C:\Windows\System32\Esent.dll. Your applications can also use this engine if you'd like: search for "Extensible Storage Engine" on the Microsoft website.

Managed code is a good choice for applications that can tolerate an application terminating when state corruption has possibly occurred. There are many applications that fall into this category. Also, it takes significantly more resources and skills to write a robust native class library or application; for many applications, managed code is the better choice because it greatly enhances programmer productivity.

# Guidelines and Best Practices

Understanding the exception mechanism is certainly important. It is equally important to understand how to use exceptions wisely. Too often, I see library developers catching all kinds of exceptions, preventing the application developer from knowing that a problem occurred. In this section, I offer some guidelines for developers to be aware of when using exceptions.

> Important If you're a class library developer developing types that will be used by other developers, take these guidelines seriously. You have a huge responsibility: you're trying to design the type in your class library so that it makes sense for a wide variety of applications. Because you don't have intimate knowledge of the code that you're calling back (via delegates, virtual, or interface methods). And you don't know which code is calling you. It's not feasible to anticipate every situation in what your type will be, so don't make any policy decisions. Your code must not decide what conditions constrain an error; let the caller make that decision.

In addition, watch very closely and not to corrupt it. Verify arguments passed to your method using code contracts (discussed in this chapter). Try not to modify state at. be ready for a failure and then try to restore state. If you follow the guidelines in this chapter, application developers will not have a difficult time using the types in your class library.

If you're an application developer, define whatever policy you think is appropriate. Following the guidelines in this chapter will help you discover problems in your code before it is released, allowing you to fix them and make your application more robust. However, feel free to diverge from these guidelines after careful consideration. You get to set the policy. For example, application code can get more aggressive about catching exceptions than class library code.

# Use finally Blocks Literally

I think finally blocks are awesome! They allow you to specify a block of code that's guaranteed to execute no matter what kind of exception the thread throws. You should use finally blocks to clean up any operation that successfully started before returning to your caller or calling the finally block to execute. You also frequently finally blocks to explicitly dispose of any objects to avoid resource leaking. Here's an example that has all cleanup code (closing the file) in a finally block.

```
using System;
using System.IO;

public sealed class SomeType {
    private void SomeMethod() {
        FileStream fs = new FileStream("C:\Data.bin", FileMode.Open);
        try {
```

478 PART IV Core Facilities
