
```cs
// Display 100 divided by the first byte in the file.
Console.WriteLine(100 / fs.ReadByte());
```

```cs
{
    // Put cleanup code in a finally block to ensure the file gets closed regardless
    // of whether or not an exception occurs (for example, the first byte was 0).
    if (fs != null) fs.Dispose();
}
```

Ensuring that cleanup code always executes is so important that many programming languages offers constructs that make writing cleanup code easier. For example, the C# language automatically emits try/finally blocks whenever you use the lock, using, and for statements. The C# compiler also emits try/finally blocks whenever you override a class destructor (the Finalize method). Using these constructs, the compiler puts the code you've written inside the try block and automatically puts the cleanup code inside the finally block. Specifically:

- *When you use the lock statement, the lock is released inside a finally block.*
- *When you use the using statement, the object has its Dispose method called inside a finally block.*
- *When you use the foreach statement, the IEnumerator object has its Dispose method called inside a finally block.*
- *When you define a destructor method, the base class's Finalize method is called inside a finally block.*

For example, the following C# code takes advantage of the using statement. This code is shorter than the code shown in the previous example, but the code that the compiler generates is identical to the code generated in the previous example.

```cs
using System;
using System.IO;

internal sealed class SomeType {
    using (FileStream fs = new FileStream(@"C:\Data.bin", FileMode.Open)) {
        // Display 100 divided by the first byte in the file.
        Console.WriteLine(100 / fs.ReadByte());
    }
}
```

For more about the using statement, see Chapter 21; and for more about the lock statement, see Chapter 30.

## Don’t Catch mistake Everything

A ubiquitous mistake by developers who have not been properly trained on the proper use of exceptions is to use catch blocks too often and improperly. When you catch an exception, you're stating that you expected this exception, you understand why it occurred, and you know how to deal with it. In other words, you're defining a policy for the application. This all goes back to the “Trading Reliability for Productivity” section earlier in this chapter.

All too often, I see code this.

```cs
try {
  // try to execute code that the programmer knows might fail...
} catch (Exception) {
}
```

This code indicates that it was expecting and all exceptions and knows how to recover from any and all situations. How can this possibly? A type that’s part of a class library should never, ever, under circumstance catch and swallow all exceptions because there is no way for the type to know exactly how the application intends to respond to an exception. In addition, the type will frequently call out to application via a delegate, virtual method, or interface method. If the application code throws an exception, another part of the application is probably expecting to catch this exception. The exception should be allowed to filter it up the stack call and let the application code handle the exception as it sees fit.

If the exception is unhandled, the CLR terminates the process. I'll discuss unhandled exceptions later in this chapter. Most unhandled exceptions will be discovered during testing of your code. To fix these unhandled exceptions, you will either modify the code to look for a specific exception, or you will rewrite the code to eliminate the conditions that cause the exception to be thrown. The final version of the code that will be running in a production environment should see very few unhandled exceptions and be extremely robust.

> Note In some cases, a method that cannot complete its task will detect that some object's state has been corrupted and cannot be restored. Allowing the application to continue running might result in unpredictable behavior or security vulnerabilities. When this situation is detected, method should not throw an exception; instead, it should force the process to terminate immediately by calling System.FailFast method.

By the way, it is OK to catch System.Exception and execute some code inside the catch block’s braces as long as you re-throw the exception at the bottom of the catch. Catch System.Exception and swallowing the exception (not re-throwing) should never be done because it hides failures that allow the application to run with unpredictable results and potential security vulnerabilities. Studio’s code analysis tool (FxCopCmd.exe) will flag any code that contains a catch (Exception) in the block’s code. The “Backing Out of a Partially

![](img/0ce3b788d061e3d3095fa554b1a34adf_505_0.png)

Completed Operation When an Unrecoverable Exception Occurs—Maintaining State section, coming shortly in this chapter, will discuss this pattern.

Finally, it is OK to catch an exception occurring in one thread and re-throw the exception in another thread. The Asynchronous Programming Model (discussed in Chapter 28, "I/O-Bound Asynchronous Operations") supports this. For example, if a thread pool executes catches an exception, the CLR catches and swallows the exception and allows the thread to return to the thread pool. A later thread should call an EndDxx method to determine the result of the asynchronous operation. The EndDxx method will throw the same exception object that was thrown by the thread thread that did the actual work. In this scenario, the exception is being swallowed by the first thread; however, the exception is being re-thrown by the thread that called the EndDxx method, so it is not being hidden from the application.

## Recovering Gracefully from an Exception

Sometimes you call a method knowing in advance of some the exceptions that it might throw. Because you expect these exceptions, you might want to have some code that allows your application to recover gracefully from the situation and continue running. Here's an example in pseudocode

```cs
public String CalculateSpreadsheetCell(Int32 row, Int32 column) {
    String result;
    try {
        result = /* Code to calculate value of a spreadsheet's cell */;
    } catch (DivideByZeroException) {
        result = "Can show value: Divide by zero";
    }
    catch (OverflowException) {
        result = "Can show value: Too big";
    }
    return result;
}
```

This pseudocode calculates the contents of a cell in a spreadsheet and returns a string representing the value to the caller so that the caller can display the string in the application's window. However, a cell's contents might the result of dividing one cell by another. If the cell contains the denominator 0, the CLR will throw a DivideByZeroException. In this case, the method catches this specific exception.

## Backing Out of a Partially Completed Operation When an Unrecoverable Exception Occurs—Maintaining State

Usually, methods call other methods to perform a single operation. Some of the individual methods might complete successfully, and some might not. For example, let's say that you're serializing a set of objects to a disk file. At this point, the file is corrupted because it contains partially serialized object. The following code demonstrates the correct way to implement this.

```cs
public void SerializeObjectGraph(FileStream fs, IFormatter formatter, Object rootObj) {
    // Save the current position of the file.
    Int64 beforeSerialization = fs.Position;

    try {
        // Attempt to serialize the object graph to the file.
        formatter.Serialize(fs, rootObj);
    } catch (
        // Catch any and all exceptions.
        // If anything goes wrong, reset the file back to a good state.
        fs.Position = beforeSerialization;

        // Truncate the file.
        fs.SetLength(fs.Position);

        // NOTE: The preceding code isn't in a finally block because
        // the stream will be reset only when serialization fails.

        // Let the caller(s) know what happened by re-throwing the SAME exception.
        throw;
    }
}
```

To properly back out of the partially completed operation, write code that catches all exceptions. Yes, catch all exceptions because you don't care what kind of error occurred; you need to put your data structures back into a consistent state. After you've caught and handled the exception, don't swallow it—let the caller know the exception occurred. You can do this by re-throwing the same exception. In fact, C# and many other languages make this easy. Just use C#'s keyword without specifying after throw, as shown in the previous code.

Notice that the catch block in the previous example doesn't specify any exception type because I want to catch any and all exceptions. In addition, the code in the catch block doesn't need to know exactly what kind of exception was thrown, that something went wrong. Fortunately, C# lets me do this easily by not specifying any exception type and by making the throw statement rethrow whatever object is caught.
