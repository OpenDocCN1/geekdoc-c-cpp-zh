
There is one point to remember about using a catch-all catch: It must be the last catch clause in the catch sequence.

> Note In the vast majority of cases you should not use the "catch all" handler as a means of dealing with exceptions. It is normally better to deal individually with the exceptions that your code can generate. The inappropriate use of the "catch all" handler can lead to situations in which errors that would otherwise be caught during testing are masked. It is also difficult to correctly handle all types of exceptions with a single handler. That said, a "catch all" handler might be appropriate in certain specialized circumstances, such as in a runtime code analysis tool.

## Nesting try Blocks

One try block can be nested within another. An exception generated within the inner try block that is not caught by a catch associated with that try is propagated to the outer try block. For example, here the IndexOutOfRangeException is not caught by the inner try block, but by the outer try:

```csharp
// Use a nested try block.

using System;

class NestTrys {
    static void Main() {
        // Here, numer is longer than denom.
        int[] numer = { 4, 8, 16, 32, 64, 128, 256, 512 };
        int[] denom = { 2, 0, 4, 4, 0, 8 };

        try { // outer try
            for(int i=0; i < numer.Length; i++) {
                try { // nested try
                    Console.WriteLine(numer[i] + " / " +
                        denom[i] + " is " +
                        numer[i]/denom[i]);
                }
                catch (DivideByZeroException) {
                    Console.WriteLine("Can't divide by Zero!");
                }
            }
        }
        catch (IndexOutOfRangeException) {
            Console.WriteLine("No matching element found.");
            Console.WriteLine("Fatal error -- program terminated.");
        }
    }
}
```

The output from the program is shown here:

```
4 / 2 is 2
Can't divide by Zero!
16 / 4 is 4
32 / 4 is 8
Can't divide by Zero!
128 / 8 is 16
No matching element found.
Fatal error -- program terminated.
```

In this example, an exception that can be handled by the inner try—in this case a divide-by-zero error—allows the program to continue. However, an array boundary error is caught by the outer try, which causes the program to terminate.

Although certainly not the only reason for nested try statements, the preceding program makes an important point that can be generalized. Often, nested try blocks are used to allow different categories of errors to be handled in different ways. Some types of errors are catastrophic and cannot be fixed. Some are minor and can be handled immediately. Many programmers use an outer try block to catch the most severe errors, allowing inner try blocks to handle less serious ones. You can also use an outer try block as a “catch all” block for those errors that are not handled by the inner block.

## Throwing an Exception

The preceding examples have been catching exceptions generated automatically by the runtime system. However, it is possible to throw an exception manually by using the throw statement. Its general form is shown here:

```
throw exceptOb;
```

The exceptOb must be an object of an exception class derived from Exception.

Here is an example that illustrates the throw statement by manually throwing a DivideByZeroException:

```
// Manually throw an exception.

using System;

class ThrowDemo {
 static void Main() {
   try {
     Console.WriteLine("Before throw.");
     throw new DivideByZeroException();
   }
   catch (DivideByZeroException) {
     Console.WriteLine("Exception caught.");
   }
   Console.WriteLine("After try/catch statement.");
 }
}
```

The output from the program is shown here:

```
Before throw.
Exception caught.
After try/catch statement.
```

Notice how the **DivideByZeroException** was created using **new** in the **throw** statement. Remember, **throw** throws an object. Thus, you must create an object for it to throw. That is, you can't just throw a type. In this case, the default constructor is used to create a **DivideByZeroException** object, but other constructors are available for exceptions.

Most often, exceptions that you throw will be instances of exception classes that you created. As you will see later in this chapter, creating your own exception classes allows you to handle errors in your code as part of your program's overall exception handling strategy.

## Rethrowing an Exception

An exception caught by one **catch** can be rethrown so that it can be caught by an outer **catch**. The most likely reason for rethrowing an exception is to allow multiple handlers access to the exception. For example, perhaps one exception handler manages one aspect of an exception, and a second handler copes with another aspect. To rethrow an exception, you simply specify **throw**, without specifying an expression. That is, you use this form of **throw**:

```csharp
throw;
```

Remember, when you rethrow an exception, it will not be recaught by the same **catch** clause. Instead, it will propagate to an outer **catch**.

The following program illustrates rethrowing an exception. In this case, it rethrows an **IndexOutOfRangeException**.

```csharp
// Rethrow an exception.

using System;

class Rethrow {
  public static void GenException() {
    // Here, num is longer than denom.
    int[] numer = { 4, 8, 16, 32, 64, 128, 256, 512 };
    int[] denom = { 2, 0, 4, 4, 0, 8 };

    for(int i=0; i<numer.Length; i++) {
      try {
        Console.WriteLine(numer[i] + " / " +
                          denom[i] + " is " +
                          numer[i]/denom[i]);
      }
      catch (DivideByZeroException) {
        Console.WriteLine("Can't divide by Zero!");
      }
      catch (IndexOutOfRangeException) {
        Console.WriteLine("No matching element found.");
        throw; // rethrow the exception
      }
    }
  }
}

class RethrowDemo {
  static void Main() {
    try {
Rethrow.GenException();
}
catch(IndexOutOfRangeException) {
    // recatch exception
    Console.WriteLine("Fatal error -- " + "program terminated.");
}
}
```

In this program, divide-by-zero errors are handled locally, by GenException(), but an array boundary error is rethrown. In this case, the IndexOutOfRangeException is handled by Main().

## Using finally

Sometimes you will want to define a block of code that will execute when a try/catch block is left. For example, an exception might cause an error that terminates the current method, causing its premature return. However, that method may have opened a file or a network connection that needs to be closed. Such types of circumstances are common in programming, and C# provides a convenient way to handle them: finally.

To specify a block of code to execute when a try/catch block is exited, include a finally block at the end of a try/catch sequence. The general form of a try/catch that includes finally is shown here:

```
try {
    // block of code to monitor for errors
}
catch (ExceptType1 exOb) {
    // handler for ExceptType1
}
catch (ExceptType2 exOb) {
    // handler for ExceptType2
}
:
finally {
    // finally code
}
```

The finally block will be executed whenever execution leaves a try/catch block, no matter what conditions cause it. That is, whether the try block ends normally, or because of an exception, the last code executed is that defined by finally. The finally block is also executed if any code within the try block or any of its catch blocks returns from the method.

Here is an example of finally:

```
// Use finally.
using System;
class UseFinally {
public static void GenException(int what) {
```

One other point: Syntactically, when a finally block follows a try block, no catch clauses are technically required. Thus, you can have a try followed by a finally with no catch clauses. In this case, the finally block is executed when the try exits, but no exceptions are handled.

## A Closer Look at the Exception Class

Up to this point, we have been catching exceptions, but we haven't been doing anything with the exception object itself. As explained earlier, a catch clause allows you to specify an exception type and a variable. The variable receives a reference to the exception object. Since all exceptions are derived from Exception, all exceptions support the members defined by Exception. Here we will examine several of its most useful members and constructors, and put the exception variable to use.

Exception defines several properties. Three of the most interesting are Message, StackTrace, and TargetSite. All are read-only. Message contains a string that describes the nature of the error. StackTrace contains a string that contains the stack of calls that lead to the exception. TargetSite obtains an object that specifies the method that generated the exception.

Exception also defines several methods. One that you will often use is ToString(), which returns a string that describes the exception. ToString() is automatically called when an exception is displayed via WriteLine(), for example.

The following program demonstrates these properties and this method:

```csharp
// Using Exception members.

using System;

class ExcTest {
    public static void GenException() {
        int[] nums = new int[4];

        Console.WriteLine("Before exception is generated.");

        // Generate an index out-of-bounds exception.
        for(int i=0; i < 10; i++) {
            nums[i] = i;
            Console.WriteLine("nums[{0}]: {1}", i, nums[i]);
        }

        Console.WriteLine("this won't be displayed");
    }
}

class UseExcept {
    static void Main() {
        try {
            ExcTest.GenException();
        }
        catch (IndexOutOfRangeException exc) {
```
