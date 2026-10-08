
# Chapter 13 Exception Handling: A Deeper Look

exceptionMethod.StackTrace() in C:\Users\PaulDeitel\Documents\examples\nch13_05\Properties\Properties.cs:line 54
at Properties.Method2() in C:\Users\PaulDeitel\Documents\examples\nch13_05\Properties\Properties.cs:line 40
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\nch13_05\Properties\Properties.cs:line 34
at Properties.Main() in C:\Users\PaulDeitel\Documents\examples\nch13_05\Properties\Properties.cs:line 14

exceptionParameter.InnerException:
System.FormatException: Input string was not in a correct format.
at System.String.ToNumber(String str, NumberStyles options,
NumberBuffer&number,FormatInfo info, Boolean parseDecimal)
at System.Number.ParseInt32(String s, NumberStyles style,
FormatInfo info)
at System.Int32.Parse(String s)
at Properties.Method3() in C:\Users\PaulDeitel\Documents\examples\nch13_05\Properties\Properties.cs:line 49

Fig. 13.5 Stack unwinding and Exception class properties (Part 3 of 3)

Program execution begins with Main, which becomes the first method on the method-call stack. Line 14 of the try block invokes Method1 (declared in lines 32–35), which becomes the second method on the stack. If Method1 throws an exception, the catch block in lines 16–28 handles the exception and provides information about the exception that occurred. Line 34 of Method1 invokes Method2 (lines 38–41), which becomes the third method on the stack. Then line 40 of Method2 invokes Method3 (lines 44–47), which becomes the fourth method on the stack.

At this point, the method-call stack (from top to bottom) for the program is:

+ Method3
+ Method2
+ Method1
+ Main

The method called most recently (Method3) appears at the top of the stack; the first method called (Main) appears at the bottom. The try statement (lines 47–56) in Method3 invokes int.Parse (line 49), which attempts to convert a string to an int. At this point, int.Parse becomes the fifth and final method on the stack.

# 13.7 Throwing an Exception with an InnerException

Because the argument to int.Parse is not in int format, line 49 throws a FormatException that was caught in line 51 of Method3. The exception terminates the call to int.Parse, so the method is unwound (i.e., removed) from the method-call stack. The catch block in Method3 then creates and throws an Exception object. The first argument to the Constructor is the custom error message for our, "Exception occurred in Method3." The second argument is the InnerException.

The StackTrace for this new exception reflects the point at which the exception was thrown (lines 54–55). Now Method3 terminates, because the exception thrown in the catch block is not caught in the method body. Thus, control

# 13.8 User-Defined Exception Classes

returns to the statement invoked Method3 in the prior method in the stack call (Method2). This unwinds Method3 from the method-call stack.

When control returns to line 40 in Method2, the CLR determines that line 40 is not in a try block. Therefore the exception cannot be caught in Method2, and Method2 terminates. This unwinds Method2 from the stack and returns to line 34 in Method1.

Here again, line 34 is not in a try block, Method1 cannot catch the exception. The method terminates and is unwound from the catch stack, returning to line 14 in Main, which is located in a try block. The try block in Main exits and the catch block (lines 16-28) catches the exception. The catch block uses properties Message, StackTrace and InnerException to create the output. Stack unwinding continues until a catch block catches the exception or the program terminates.

# 13.7.5 Displaying Information About the Exception

The first block of output (which we reformed for readability) in Fig. 13.5 contains the exception's string representation, which is returned from an implicit class to Method. The string begins with the name of the exception followed by the Message property value. The next four items present the stack trace of the InnerException object. The remainder of the block shows the StackTrace for the exception thrown in lines 54-55 of Method3. The StackTrace represents the state of the method-call stack at the throw point of the exception, rather than at the point where the exception is caught. This StackTrace indicates the line in which the exception begins with “at” represents a method on the catch block, the file in which the method resides and the line number of the throw point in the file. The inner-exception information includes the inner-exception stack trace.

![](img/57baed2319be0bb1b5f98674846f2711_571_0.png)

> When catching and rethrowing an exception, provide additional debugging information in the rethrown exception. To do so, create an object of Exception subclass containing more descriptive debugging information, then pass the original caught exception to the new exception object's constructor to initialize the InnerException property.

The next block of output (two lines) displays the Message property value (Exception occurred in Method3) of the exception thrown in Method3.

The third block of output displays the StackTrace property contains the stack trace starting from line 54 in Method3, because that's the point where the Exception object was created and thrown. The stack trace always begins from the exception's throw point.

Finally, the last block of output displays the string representation of the InnerException property, which includes the namespace and class name of the exception object, as well as its Message and StackTrace properties.

# 13.8 User-Defined Exception Classes

In many cases you can use exception classes from the .NET Framework Class Library to identify exceptions that occur in your programs. In some cases, however, you might wish to create new exception classes specific to the problems that occur in your programs. User-defined exception classes should derive directly or indirectly from class Exception of namespace System. When you create code that throws exceptions, they should be well documented, so that other developers who use your code will know how to handle them.

> > Good Programming Practice 13.1
Associating each type of malfunction with an appropriately named exception class proves clarity.

> > Software Engineering Observation 13.4
Before creating a user-defined exception class, investigate the existing exceptions in the .NET Framework Class Library to determine whether an appropriate exception type exists.

Class NegativeNumberException 13.6 demonstrates a user-defined exception class. NegativeNumberException (13.6) represents exceptions that occur when a program performs an illegal operation on a negative number, such as attempting to calculate its square root. According to Microsoft’s “Best Practices for Handling Exceptions” (bit.ly/Exceptions-BestPractices), user-defined exceptions should typically extend Exception, have a class name that ends with Exception and define three constructors:

+   * a parameterless constructor,
* a constructor that receives a string argument (the error message), and
* a constructor that receives a string argument and an Exception argument (the error message and the inner-exception object).

Defining these three constructors makes your class more flexible, allowing other programmers to use and extend it.

```
// Fig. 13.6: NegativeNumberException.cs
// NegativeNumberException represents exceptions caused by
// illegal operations performed on negative numbers.
public class NegativeNumberException : Exception
{
    // default constructor
    public NegativeNumberException()
    : base("Illegal operation for a negative number")
    {
        // empty body
    }

    // constructor for customizing error message
    public NegativeNumberException(string messageValue)
    : base(messageValue)
}
```

Fig. 13.6 | NegativeNumberException represents exceptions caused by illegal operations performed on negative numbers. (Part I of 2.)
