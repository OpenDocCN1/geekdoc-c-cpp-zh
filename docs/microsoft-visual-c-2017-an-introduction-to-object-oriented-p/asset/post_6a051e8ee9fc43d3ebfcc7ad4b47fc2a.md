
## TWO TRUTHS & A LIE

## Creating Your Own Exception Classes

- 1. To create your Exception types whose objects you can throw, you can extend the ApplicationException class or the Exception class.
- 2. In C#, you can throw any object that you create if it is appropriate for the application.
- 3. You can throw any type of Exception at any time—both those that are already created as part of C# and those of your creation.

Exception or descendent of the Exception class.
The false statement is #2. In C#, you can't throw an object unless it is an Exception

## Rethrowing an Exception

When you write a method that catches an exception, your method does not have to handle it. Instead, you might choose to **rethrow the exception** to the method that called your method. Then you can let the calling method handle the problem.

Within a **catch** block, you can rethrow an unnamed exception that was caught by using the keyword **throw** with no object after it. For example, Figure 11-37 shows a class that contains methods. In this program, the following sequence of events takes place:

- 1. The `Main()` method calls `MethodA()`.
- 2. `MethodA()` calls `MethodB()`.
- 3. `MethodB()` calls `MethodC()`.
- 4. `MethodC()` throws an `Exception`.
- 5. When `MethodB()` catches the `Exception`, it does not handle the `Exception`; instead, it throws the `Exception` back to `MethodA()`.
- 6. `MethodA()` catches the `Exception` but does not handle it either. Instead, `MethodA()` throws the `Exception` back to the `Main()` method.
- 7. The `Exception` is caught in the `Main()` method, where the message that was created in `MethodC()` is finally displayed.

Figure 11-38 shows the execution of the program.

## CHAPTER 11 Exception Handling

```csharp
using System;
using static System.Console;
class ReThrowDemo{
    static void Main()
    {
        try {
            WriteLine("Trying in Main() method");
            MethodA();
        } catch (Exception ae)
        {
            WriteLine("Caught in Main() method --\n {0}",
                ae.Message);
        }
        WriteLine("Main() is done");
    }
    private static void MethodA()
    {
        try {
            WriteLine("Trying in method A");
            MethodB();
        } catch (Exception)
        {
            WriteLine("Caught in method A");
            throw();
        }
    }
    private static void MethodB()
    {
        try {
            WriteLine("Trying in method B");
            MethodC();
        } catch (Exception)
        {
            WriteLine("Caught in method B");
            throw();
        }
    }
    private static void MethodC()
    {
        WriteLine("In method C");
        throw(new Exception("This came from method C"));
    }
}
```

**Figure 11-37** The ReThrowDemo program

## Chapter Summary

```
Trying in Main() method
Trying in method A
Trying in method B
in method C
Caught in method B
Caught in method A
Caught in Main() method --
  This came from method C
Main() method is done
```

**Figure 11-38** Execution of the ReRewDemo program

If you name the Exception argument in a catch block (for example, catch (Exception e then), then you should use that identifier when you use a throw statement in the block (for example, throw e);

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_551_0.png)

## Chapter Summary

- An exception is any error condition or unexpected behavior in an executing program. In C#, all exceptions are objects that are instances of the Exception class or one of its derived classes. Most exceptions you are derived from three classes: SystemException, ApplicationException, and their parent Exception. You can purposely generate a SystemException by forcing a program to contain an error. Although you are not required to handle exceptions, you can use object-oriented techniques to provide elegant error-handling solutions.

## CHAPTER 11 Exception Handling

- When you think an error will occur frequently, the most efficient approach is to handle the error in the traditional way, with if statements. If an error will occur infrequently, instantiating an Exception object when needed is more efficient. In object-oriented terminology, you "try" a procedure that may not properly complete. A method that detects an error condition or "throws" an exception, and the block of code that detects the error "catches" the exception. You must include at least one catch block or finish immediately following a try block.

- Every Exception object contains a ToString() method and a Message property that contains useful information about the Exception.

- You can place as many statements as you need within a try block, and you can catch as many different exceptions as you want. If an error will occur infrequently, instantiating an Exception object when needed is more efficient. In object-oriented terminology, you "try" a procedure that may not properly complete. A method that detects an error condition or "throws" an exception, and the block of code that detects the error "catches" the exception. You must include at least one catch block or finish immediately following a try block.

- Every Exception object contains a ToString() method and a Message property that contains useful information about the Exception.

- You can place as many statements as you need within a try block, and you can catch as many different exceptions as you want. If an error will occur infrequently, instantiating an Exception object when needed is more efficient. In object-oriented terminology, you "try" a procedure that may not properly complete. A method that detects an error condition or "throws" an exception, and the block of code that detects the error "catches" the exception. You must include at least one catch block or finish immediately following a try block.

- You can place as many statements as you need within a try block, and you can catch as many different exceptions as you want. If an error will occur infrequently, instantiating an Exception object when needed is more efficient. In object-oriented terminology, you "try" a procedure that may not properly complete. A method that detects an error condition or "throws" an exception, and the block of code that detects the error "catches" the exception. You must include at least one catch block or finish immediately following a try block.

- You can place as many statements as you need within a try block, and you can catch as many different exceptions as you want. If an error will occur infrequently, instantiating an Exception object when needed is more efficient. In object-oriented terminology, you "try" a procedure that may not properly complete. A method that detects an error condition or "throws" an exception, and the block of code that detects the error "catches" the exception. You must include at least one catch block or finish immediately following a try block.

## Key Terms

An exception is any error condition or unexpected behavior in an executing program.

Exception handling is the set of object-oriented techniques to manage unexpected errors in an executing program.

## Review Questions

1. Any error code or unexpected behavior in an executing program is known as an
2. Which of the following is not treated as a C# Exception?
   a. Your program asks the user to input a number, but the user enters a character.
   b. You calculate a value that is too large for the answer's variable type.
   c. You attempt to access an array with a subscript that is too large.
   d. You attempt to execute a C# program, but the C# compiler has not compiled.
3. Most exceptions you will derive from three classes:
   a. Object, ObjectException, and ObjectApplicationException
   b. Exception, SystemException, and ApplicationException
   c. FormatException, ApplicationException, and IOExceptionException
   d. SystemException, IOException, and FormatException
