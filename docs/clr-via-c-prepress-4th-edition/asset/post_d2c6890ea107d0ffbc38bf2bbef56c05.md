
many applications, managed code is the better choice because it greatly enhances programmer productivity.

## Guidelines and Best Practices

Understanding the exception mechanism is certainly important. It is equally important to understand how to use exceptions wisely. All too often, I see library developers catching all kinds of exceptions, preventing the application developer from knowing that a problem occurred. In this section, I offer some guidelines for developers to be aware of when using exceptions.

**Important** If you’re a *class library developer* developing types that will be used by other developers, take these guidelines very seriously. You have a huge responsibility: You're trying to design the type in your class library so that it makes sense for a wide variety of applications. Remember that you don’t have intimate knowledge of the code that you’re calling back (via delegates, virtual methods, or interface methods). And you don’t know which code is calling you. It’s not feasible to anticipate every situation in which your type will be used, so don’t make any policy decisions. Your code must not decide what conditions constitute an error; let the caller make that decision.

In addition, watch state very closely and try not to corrupt it. Verify arguments passed to your method by using code contracts (discussed later in this chapter). Try not to modify state at all. If you do modify state, then be ready for a failure and then try to restore state. If you follow the guidelines in this chapter, application developers will not have a difficult time using the types in your class library.

If you’re an *application developer*, define whatever policy you think is appropriate. Following the design guidelines in this chapter will help you discover problems in your code before it is released, allowing you to fix them and make your application more robust. However, feel free to diverge from these guidelines after careful consideration. You get to set the policy. For example, application code can get more aggressive about catching exceptions than class library code.

## Use finally Blocks Liberally

I think finally blocks are awesome! They allow you to specify a block of code that’s guaranteed to execute no matter what kind of exception the thread throws. You should use finally blocks to clean up from an operation that successfully started before returning to your caller or allowing code following the finally block to execute. You also frequently use finally blocks to explicitly dispose of any objects to avoid resource leaking. Here’s an example that has all cleanup code (closing the file) in a finally block:

```csharp
using System;
using System.IO;

public sealed class SomeType {
    private void SomeMethod() {
        FileStream fs = new FileStream(@"C:\Data.bin", FileMode.Open);
        try {
            // Display 100 divided by the first byte in the file.
            Console.WriteLine(100 / fs.ReadByte());
        }
        finally {
            // Put cleanup code in a finally block to ensure that the file gets closed regardless
            // of whether or not an exception occurs (for example, the first byte was 0).
            if (fs != null) fs.Dispose();
        }
    }
}
```

Ensuring that cleanup code always executes is so important that many programming languages offer constructs that make writing cleanup code easier. For example, the C# language automatically emits try/finally blocks whenever you use the lock, using, and foreach statements. The C# compiler also emits try/finally blocks whenever you override a class’s destructor (the Finalize method). When using these constructs, the compiler puts the code you’ve written inside the try block and automatically puts the cleanup code inside the finally block. Specifically,

- When you use the lock statement, the lock is released inside a `finally` block.
- When you use the using statement, the object has its Dispose method called inside a `finally` block.
- When you use the foreach statement, the IEnumerator object has its Dispose method called inside a finally block.
- When you define a destructor method, the base class’s Finalize method is called inside a finally block.

For example, the following C# code takes advantage of the using statement. This code is shorter than the code shown in the previous example, but the code that the compiler generates is identical to the code generated in the previous example.

```csharp
using System;
using System.IO;

internal sealed class SomeType {
    private void SomeMethod() {
        using (FileStream fs = new FileStream(@"C:\Data.bin", FileMode.Open)) {
            // Display 100 divided by the first byte in the file.
            Console.WriteLine(100 / fs.ReadByte());
        }
    }
}
```

For more about the using statement, see Chapter 21; and for more about the lock statement, see Chapter 30, “Hybrid Thread Synchronization Constructs.”

## Don’t Catch Everything

A ubiquitous mistake made by developers who have not been properly trained on the proper use of exceptions is to use catch blocks too often and improperly. When you catch an exception, you’re stating that you expected this exception, you understand why it occurred, and you know how to deal with it. In other words, you’re defining a policy for the application. This all goes back to the “Trading Reliability for Productivity” section earlier in this chapter.

All too often, I see code like this:

```csharp
try {
    // try to execute code that the programmer knows might fail...
}
catch (Exception) {
    ...
}
```

This code indicates that it was expecting any and all exceptions and knows how to recover from *any* and *all* situations. How can this possibly be? A type that’s part of a class library should never, *ever*, *under any circumstance* catch and swallow all exceptions because there is no way for the type to know exactly how the application intends to respond to an exception. In addition, the type will frequently call out to application code via a delegate, virtual method, or interface method. If the application code throws an exception, another part of the application is probably expecting to catch this exception. The exception should be allowed to filter its way up the call stack and let the application code handle the exception as it sees fit.

If the exception is unhandled, the CLR terminates the process. I’ll discuss unhandled exceptions later in this chapter. Most unhandled exceptions will be discovered during testing of your code. To fix these unhandled exceptions, you will either modify the code to look for a specific exception, or you will rewrite the code to eliminate the conditions that cause the exception to be thrown. The final version of the code that will be running in a production environment should see very few unhandled exceptions and will be extremely robust.

> **Note** In some cases, a method that can’t complete its task will detect that some object’s state has been corrupted and cannot be restored. Allowing the application to continue running might result in unpredictable behavior or security vulnerabilities. When this situation is detected, that method should not throw an exception; instead, it should force the process to terminate immediately by calling the `System.Environment.FailFast` method.

By the way, it is OK to catch System.Exception and execute some code inside the catch block’s braces as long as you re-throw the exception at the bottom of that code. Catching System.Exception and swallowing the exception (not re-throwing it) should never be done because it hides failures that allow the application to run with unpredictable results and potential security vulnerabilities. Visual Studio’s code analysis tool (FxCopCmd.exe) will flag any code that contains a catch (Exception) block unless there is a throw statement included in the block’s code. The “Backing Out of a Partially Completed Operation When an Unrecoverable Exception Occurs—Maintaining State” section, coming shortly in this chapter, will discuss this pattern.

Finally, it is OK to catch an exception occurring in one thread and re-throw the exception in another
