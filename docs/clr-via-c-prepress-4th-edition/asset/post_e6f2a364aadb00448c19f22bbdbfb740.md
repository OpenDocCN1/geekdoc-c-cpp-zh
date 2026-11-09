
## The try Block

A `try` block contains code that requires common cleanup operations, exception-recovery operations, or both. The cleanup code should be placed in a single `finally` block. A try block can also contain code that might potentially throw an exception. The exception-recovery code should be placed in one or more catch blocks. You create one catch block for each kind of exception that your application can safely recover from. A try block must be associated with at least one catch or finally block; it makes no sense to have a try block that stands by itself, and C# will prevent you from doing this.

> **Important** Sometimes developers ask how much code they should put inside a single `try` block. The answer to this depends on state management. If, inside a `try` block, you execute multiple operations that could all throw the same exception type and the way that you'd recover this exception type is different depending on the operation, then you should put each operation in its own `try` block so that you can recover your state correctly.

## The catch Block

A `catch` block contains code to execute in response to an exception. A try block can have zero or more catch blocks associated with it. If the code in a try block doesn't cause an exception to be thrown, the CLR will never execute the code contained within any of its catch blocks. The thread will simply skip over all of the catch blocks and execute the code in the `finally` block (if one exists). After the code in the `finally` block executes, execution continues with the statement following the `finally` block.

The parenthetical expression appearing after the `catch` keyword is called the *catch type*. In C#, you must specify a catch type of `System.Exception` or a type derived from `System.Exception`. For example, the previous code contains catch blocks for handling an `InvalidOperationException` (or any exception derived from it) and an `IOException` (or any exception derived from it). The last catch block (which doesn't specify a catch type) handles any exception at all except for the exception type specified by earlier catch blocks; this is equivalent to having a catch block that specifies a catch type of `System.Exception` except that you cannot access the exception information via code inside the catch block's braces.

**Note** When debugging through a `catch` block by using Microsoft Visual Studio, you can see the currently thrown exception object by adding the special `$exception` variable name to a watch window.

The CLR searches from top to bottom for a matching catch type, and therefore you should place the more specific exception types at the top. The most-derived exception types should appear first, followed by their base types (if any), down to `System.Exception` (or an exception block that doesn't specify a catch type). In fact, the C# compiler generates an error if more specific catch blocks appear closer to the bottom because the catch block would be unreachable.

If an exception is thrown by code executing within the `try` block (or any method called from within the try block), the CLR starts searching for catch blocks whose catch type is the same type as or a base type of the thrown exception. If none of the catch types matches the exception, the CLR continues searching up the call stack looking for a catch type that matches the exception. If after reaching the top of the call stack, no catch block is found with a matching catch type, an unhandled exception occurs. I’ll talk more about unhandled exceptions later in this chapter.

Once the CLR locates a catch block with a matching catch type, it executes the code in all inner *finally* blocks, starting from the *try* block whose code threw the exception and stopping with the catch block that matched the exception. Note that any *finally* block associated with the catch block that matched the exception is not executed yet. The code in this *finally* block won’t execute until after the code in the handling catch block has executed.

After all the code in the inner *finally* blocks has executed, the code in the handling catch block executes. This code typically performs some operations to deal with the exception. At the end of the catch block, you have three choices:

- Re-throw the same exception, notifying code higher up in the call stack of the exception.
- Throw a different exception, giving richer exception information to code higher up in the call stack.
- Let the thread fall out of the bottom of the catch block.

Later in this chapter, I’ll offer some guidelines for when you should use each of these techniques. If you choose either of the first two techniques, you’re throwing an exception, and the CLR behaves just as it did before. It walks up the call stack looking for a catch block whose type matches the type of the exception thrown.

If you pick the last technique, when the thread falls out of the bottom of the catch block, it immediately starts executing code contained in the *finally* block (if one exists). After all of the code in the *finally* block executes, the thread drops out of the *finally* block and starts executing the statements immediately following the *finally* block. If no *finally* block exists, the thread continues execution at the statement following the last catch block.

In C#, you can specify a variable name after a catch type. When an exception is caught, this variable refers to the System.Exception-derived object that was thrown. The catch block’s code can reference this variable to access information specific to the exception (such as the stack trace leading up to the exception). Although it’s possible to modify this object, you shouldn’t; consider the object to be read-only. I’ll explain the Exception type and what you can do with it later in this chapter.

**Note** Your code can register with AppDomain’s FirstChanceException event to receive notifications as soon as an exception occurs within an AppDomain. This notification occurs before the CLR searches for any catch blocks. For more information about this event, see Chapter 22, “CLR Hosting and AppDomains.”

## The *finally* Block

A *finally* block contains code that's guaranteed to execute.<sup>12</sup> Typically, the code in a *finally* block performs the cleanup operations required by actions taken in the *try* block. For example, if you open a file in a *try* block, you'd put the code to close the file in a *finally* block:

```csharp
private void ReadData(string pathname) {

    FileStream fs = null;
    try {
        fs = new FileStream(pathname, FileMode.Open);
        // Process the data in the file...
    }
    catch (IOException) {
        // Put code that recovers from an IOException here...
    }
    finally {
        // Make sure that the file gets closed.
        if (fs != null) fs.Close();
    }
}
```

If the code in the *try* block executes without throwing an exception, the file is guaranteed to be closed. If the code in the *try* block does throw an exception, the code in the *finally* block still executes, and the file is guaranteed to be closed, regardless of whether the exception is caught. It's improper to put the statement to close the file after the *finally* block; the statement wouldn't execute if an exception were thrown and not caught, which would result in the file being left open (until the next garbage collection).

A *try* block doesn't require a *finally* block associated with it; sometimes the code in a *try* block just doesn't require any cleanup code. However, if you do have a *finally* block, it must appear after any and all *catch* blocks. A *try* block can have no more than one *finally* block associated with it.

When a thread reaches the end of the code contained in a *finally* block, the thread simply starts executing the statements immediately following the *finally* block. Remember that the code in the *finally* block is cleanup code. This code should execute only what is necessary to clean up operations initiated in the *try* block. The code inside *catch* and *finally* blocks should be very short and should have a high likelihood of succeeding without itself throwing an exception. Usually the code in these blocks is just one or two lines of code.

It is always possible that exception-recovery code or cleanup code could fail and throw an

12 Aborting a thread or unloading an AppDomain causes the CLR to throw a `ThreadAbortException`, which allows the *finally* block to execute. If a thread is simply killed via the `Win32 TerminateThread` function, or if the process is killed via the `Win32 TerminateProcess` function or `System.Environment's FailFast` method, then the *finally* block will not execute. Of course, Windows cleans up all resources that a process was using when a process terminates.
