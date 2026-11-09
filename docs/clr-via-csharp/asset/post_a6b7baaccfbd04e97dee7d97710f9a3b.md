
Here I'm composing my intent by chaining several operations together.¹ This code was easy for me to write and is easy for others to read and maintain because the intent is obvious: Take a string, grab a portion of it, uppercase that portion, and see if it ends with an “E.” This is great, but there is a big assumption being made here: no operation fails. But, of course, errors are always possible, so we need a way to handle those errors. In fact, there are many object-oriented constructs—constructors, getting/setting a property, adding/removing an event, calling an operator overload, calling a conversion operator—that have no way to return error codes, but these constructs must still be able to report an error. The mechanism provided by the Microsoft .NET Framework and all programming languages that support it is called exception handling.

![](img/3c46ff5b170881db4209d365b1f7a808_484_0.png)

> **Important** Many developers incorrectly believe that an exception is related to how *frequently* something happens. For example, a developer designing a file **Read** method is likely to say the following: “When reading from a file, you will eventually reach the end of its data. Since reaching the end will always happen, I’ll design my **Read** method so that it reports the end by returning a special value; I won’t have it throw an exception.” The problem with this statement is that it is being made by the developer designing the **Read** method, not by the developer calling the **Read** method.
>
> When designing the **Read** method, it is impossible for the developer to know all of the possible situations in which the method gets called. Therefore, the developer can’t possibly know how often the caller of the **Read** method will attempt to read past the end of the file. In fact, since most files contain structured data, attempting to read past the end of a file is something that *rarely* happens.

## Exception-Handling Mechanics

In this section, I’ll introduce the mechanics and C# constructs needed in order to use exception handling, but it’s not my intention to explain them in great detail. The purpose of this chapter is to offer useful guidelines for when and how to use exception handling in your code. If you want more information about the mechanics and language constructs for using exception handling, see the .NET Framework documentation and the C# language specification. Also, the .NET Framework exception-handling mechanism is built using the Structured Exception Handling (SEH) mechanism offered by Microsoft Windows. SEH has been discussed in many resources, including my own book, *Windows via C/C++*, 5th ed. (Microsoft Press, 2007), which contains three chapters devoted to SEH.

The following C# code shows a standard usage of the exception-handling mechanism. This code gives you an idea of what exception-handling blocks look like and what their purpose is. In the subsections after the code, I’ll formally describe the **try**, **catch**, and **finally** blocks and their purpose and provide some notes about their use.

¹ In fact, C#’s extension method feature exists in the language to allow you to chain more methods together that would not have been chainable otherwise.

```csharp
private void SomeMethod() {

    try {
        // Put code requiring graceful recovery and/or cleanup operations here...
    }
    catch (InvalidOperationException) {
        // Put code that recovers from an InvalidOperationException here...
    }
    catch (IOException) {
        // Put code that recovers from an IOException here...
    }
    catch {
        // Put code that recovers from any kind of exception other than those above here...

        // When catching any exception, you usually re-throw the exception.
        // I explain re-throwing later in this chapter.
        throw;
    }
    finally {
        // Put code that cleans up any operations started within the try block here...
        // The code in here ALWAYS executes, regardless of whether an exception is thrown.
        // Code below the finally block executes if no exception is thrown within the try block
        // or if a catch block catches the exception and doesn't throw or re-throw an exception.
    }
}
```

This code demonstrates one possible way to use exception-handling blocks. Don’t let the code scare you—most methods have simply a `try` block matched with a single `finally` block or a `try` block matched with a single `catch` block. It’s unusual to have as many `catch` blocks as in this example. I put them there for illustration purposes.

### The try Block

A `try` block contains code that requires common cleanup operations, exception-recovery operations, or both. The cleanup code should be placed in a single `finally` block. A `try` block can also contain code that might potentially throw an exception. The exception-recovery code should be placed in one or more `catch` blocks. You create one `catch` block for each kind of exception that your application can safely recover from. A `try` block must be associated with at least one `catch` or `finally` block; it makes no sense to have a `try` block that stands by itself, and C# will prevent you from doing this.

> **Important** Sometimes developers ask how much code they should put inside a single `try` block. The answer to this depends on state management. If, inside a `try` block, you execute multiple operations that could all throw the same exception type and the way that you’d recover this exception type is different depending on the operation, then you should put each operation in its own `try` block so that you can recover your state correctly.

### The catch Block

A **catch block** contains code to execute in response to an exception. A **try** block can have zero or more **catch** blocks associated with it. If the code in a **try** block doesn't cause an exception to be thrown, the CLR will never execute the code contained within any of its **catch** blocks. The thread will simply skip over all of the **catch** blocks and execute the code in the **finally** block (if one exists). After the code in the **finally** block executes, execution continues with the statement following the **finally** block.

The parenthetical expression appearing after the **catch** keyword is called the *catch type*. In C#, you must specify a catch type of **System.Exception** or a type derived from **System.Exception**. For example, the previous code contains **catch** blocks for handling an **InvalidOperationException** (or any exception derived from it) and an **IOException** (or any exception derived from it). The last **catch** block (which doesn't specify a catch type) handles any exception at all except for the exception type specified by earlier **catch** blocks; this is equivalent to having a **catch** block that specifies a catch type of **System.Exception** except that you cannot access the exception information via code inside the **catch** block's braces.

> **Note** When debugging through a **catch** block by using Microsoft Visual Studio, you can see the currently thrown exception object by adding the special **$exception** variable name to a watch window.

The CLR searches from top to bottom for a matching **catch** type, and therefore you should place the more specific exception types at the top. The most-derived exception types should appear first, followed by their base types (if any), down to **System.Exception** (or an exception block that doesn't specify a catch type). In fact, the C# compiler generates an error if more specific **catch** blocks appear closer to the bottom because the **catch** block would be unreachable.

If an exception is thrown by code executing within the **try** block (or any method called from within the **try** block), the CLR starts searching for **catch** blocks whose catch type is the same type as or a base type of the thrown exception. If none of the catch types matches the exception, the CLR continues searching up the call stack looking for a catch type that matches the exception. If after reaching the top of the call stack, no **catch** block is found with a matching catch type, an unhandled exception occurs. I'll talk more about unhandled exceptions later in this chapter.

Once the CLR locates a **catch** block with a matching catch type, it executes the code in all inner **finally** blocks, starting from within the **try** block whose code threw the exception and stopping with the **catch** block that matched the exception. Note that any **finally** block associated with the **catch** block that matched the exception is not executed yet. The code in this **finally** block won't execute until after the code in the handling **catch** block has executed.
