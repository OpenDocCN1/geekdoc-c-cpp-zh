# 13.8 User-Defined Exception Classes

returns to the statement invoked Method3 in the prior method in the stack call (Method2). This unwinds Method3 from the method-call stack.

When control returns to line 40 in Method2, the CLR determines that line 40 is not in a try block. Therefore the exception cannot be caught in Method2, and Method2 terminates. This unwinds Method2 from the stack and returns to line 34 in Method1.

Here again, line 34 is not in a try block, Method1 cannot catch the exception. The method terminates and is unwound from the catch stack, returning to line 14 in Main, which is located in a try block. The try block in Main exits and the catch block (lines 16-28) catches the exception. The catch block uses properties Message, StackTrace and InnerException to create the output. Stack unwinding continues until a catch block catches the exception or the program terminates.

# 13.7.5 Displaying Information About the Exception

The first block of output (which we reformed for readability) in Fig.13.5 contains the exception's string representation, which is returned from an implicit class to Method. The string begins with the name of the exception followed by the Message property value. The next four items present the stack trace of the InnerException object. The remainder of the block shows the StackTrace for the exception thrown in lines 54-55 of Method3. The StackTrace represents the state of the method-call stack at the throw point of the exception, rather than at the point where the exception is caught. This StackTrace indicates the line in which the exception begins with “at” represents a method on the catch block, the file in which the method resides and the line number of the throw point in the file. The inner-exception information includes the inner-exception stack trace.

![](bbox=[0.143, 0.558, 0.213, 0.606])

> When catching and rethrowing an exception, provide additional debugging information in the rethrown exception. To do so, create an object of Exception subclass containing more descriptive debugging information, then pass the original caught exception to the new exception object's constructor to initialize the InnerException property.

The next block of output (two lines) displays the Message property value (Exception occurred in Method3) of the exception thrown in Method3.

The third block of output displays the StackTrace property contains the stack trace starting from line 54 in Method3, because that's the point where the Exception object was created and thrown. The stack trace always begins from the exception's throw point.

Finally, the last block of output displays the string representation of the InnerException property, which includes the namespace and class name of the exception object, as well as its Message and StackTrace properties.

# 13.8 User-Defined Exception Classes

In many cases you can use exception classes from the .NET Framework Class Library to identify exceptions that occur in your programs. In some cases, however, you might wish to create new exception classes specific to the problems that occur in your programs. User-defined exception classes should derive directly or indirectly from class Ex-