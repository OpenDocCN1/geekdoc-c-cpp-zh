
Although division by zero is often allowed in floating-point arithmetic, for the purposes of this example we treat any attempt to divide by zero as an error. Thus, function `quotient` tests its second parameter to ensure that it isn’t zero before allowing the division to proceed. If the second parameter is zero, the function throws an exception to indicate to the caller that a problem occurred. The caller (main in this example) can then process the exception and allow the user to type two new values before calling function `quotient` again. In this way, the program can continue executing even after an improper value is entered, thus making the program more robust.

The example consists of two files. `DivideByZeroException.h` (Fig. 16.1) defines an exception class that represents the type of problem that might occur in the example, and `fig16_02.cpp` (Fig. 16.2) defines the `quotient` function and the main function that calls it. Function main contains the code that demonstrates exception handling.

## Defining an Exception Class to Represent the Type of Problem That Might Occur

Figure 16.1 defines class DivideByZeroException as a derived class of Standard Library class `runtime_error` (defined in header `<stdexcept>`). Class `runtime_error`—a derived class of Standard Library class `exception` (defined in header `<exception>`)—is the C++ standard base class for representing runtime errors. Class exception is the standard C++ base class for all exceptions. (Section 16.12 discusses class exception and its derived classes in detail.) A typical exception class that derives from the `runtime_error` class defines only a constructor (e.g., lines 12–13) that passes an error-message string to the base-class `runtime_error` constructor. Every exception class that derives directly or indirectly from exception contains the virtual function `what`, which returns an exception object’s error message. You’re not required to derive a custom exception class, such as DivideByZeroException, from the standard exception classes provided by C++. However, doing so allows you to use the virtual function `what` to obtain an appropriate error message. We use an object of this DivideByZeroException class in Fig. 16.2 to indicate when an attempt is made to divide by zero.

```cpp
// Fig. 16.1: DivideByZeroException.h
// Class DivideByZeroException definition.
#include <stdexcept> // stdexcept header contains runtime_error
using namespace std;

// DivideByZeroException objects should be thrown by functions
// upon detecting division-by-zero exceptions
class DivideByZeroException : public runtime_error
{
public:
   // constructor specifies default error message
   DivideByZeroException()
      : runtime_error("attempted to divide by zero")
   {
   }
}; // end class DivideByZeroException
```

**Fig. 16.1 |** Class `DivideByZeroException` definition.

## Demonstrating Exception Handling

Figure 16.2 uses exception handling to wrap code that might throw a “divide-by-zero” exception and to handle that exception, should one occur. The user enters two integers, which are passed as arguments to function `quotient` (lines 10–18). This function divides its first

```cpp
43    cout << "\nEnter two integers (end-of-file to end): ";
44 } // end while

46    cout << endl;
47 } // end main
```

```text
Enter two integers (end-of-file to end): 100 7
The quotient is: 14.2857

Enter two integers (end-of-file to end): 100 0
Exception occurred: attempted to divide by zero

Enter two integers (end-of-file to end): ^Z
```

**Fig. 16.2** | Exception-handling example that throws exceptions on attempts to divide by zero. *(Part 2 of 2.)*

## Enclosing Code in a try Block

The program begins by prompting the user to enter two integers. The integers are input in the condition of the while loop (line 29). Line 35 passes the values to function `quotient` (lines 10–18), which either divides the integers and returns a result, or throws an exception (i.e., indicates that an error occurred) on an attempt to divide by zero. Exception handling is geared to situations in which the function that detects an error is unable to handle it.

As you learned in Section 7.11, try blocks enable exception handling. A try block encloses statements that might cause exceptions and statements that should be skipped if an exception occurs. The try block in lines 33–37 encloses the invocation of function `quotient` and the statement that displays the division result. In this example, because the invocation of function `quotient` (line 35) can throw an exception, we enclose this function invocation in a try block. Enclosing the output statement (line 36) in the try block ensures that the output will occur only if function `quotient` returns a result.

> **Software Engineering Observation 16.3**
> 
> *Exceptions may surface through explicitly mentioned code in a try block, through calls to other functions and through deeply nested function calls initiated by code in a try block.*

## Defining a catch Handler to Process a DivideByZeroException

You saw in Section 7.11 that exceptions are processed by catch handlers. At least one catch handler (lines 38–42) must immediately follow each try block. The exception parameter is declared as a reference to the type of exception the catch handler can process (`DivideByZeroException` in this case). When an exception occurs in a try block, the catch handler that executes is the one whose type matches the type of the exception that occurred (i.e., the type in the catch block matches the thrown exception type exactly or is a base class of). If an exception parameter includes an optional parameter name, the catch handler can use that parameter name to interact with the caught exception in the body of the catch handler, which is delimited by braces (`{` and `}`). A catch handler typically reports the error to the user, logs it to a file, terminates the program gracefully or tries an alternate strategy to accomplish the failed task. In this example, the catch handler simply reports that the user attempted to divide by zero. Then the program prompts the user to enter two new integer values.

> **Common Programming Error 16.1**  
> *It’s a syntax error to place code between a try block and its corresponding catch handlers or between its catch handlers.*

> **Common Programming Error 16.2**  
> *Each catch handler can have only a single parameter—specifying a comma-separated list of exception parameters is a syntax error.*

> **Common Programming Error 16.3**  
> *It’s a logic error to catch the same type in two different catch handlers following a single try block.*

## Termination Model of Exception Handling

If an exception occurs as the result of a statement in a try block, the try block expires (i.e., terminates immediately). Next, the program searches for the first catch handler that can process the type of exception that occurred. The program locates the matching catch by comparing the thrown exception’s type to each catch’s exception-parameter type until the program finds a match. A match occurs if the types are identical or if the thrown exception’s type is a derived class of the exception-parameter type. When a match occurs, the code contained in the matching catch handler executes. When a catch handler finishes processing by reaching its closing right brace (}), the exception is considered handled and the local variables defined within the catch handler (including the catch parameter) go out of scope. Program control does not return to the point at which the exception occurred (known as the throw point), because the try block has expired. Rather, control resumes with the first statement (line 44) after the last catch handler following the try block. This is known as the termination model of exception handling. Some languages use the resumption model of exception handling, in which, after an exception is handled, control resumes just after the throw point. As with any other block of code, when a try block terminates, local variables defined in the block go out of scope.

> **Common Programming Error 16.4**  
> *Logic errors can occur if you assume that after an exception is handled, control will return to the first statement after the throw point.*

> **Error-Prevention Tip 16.1**  
> *With exception handling, a program can continue executing (rather than terminating) after dealing with a problem. This helps ensure the kind of robust applications that contribute to what’s called mission-critical computing or business-critical computing.*

If the try block completes its execution successfully (i.e., no exceptions occur in the try block), then the program ignores the catch handlers and program control continues with the first statement after the last catch following that try block.

If an exception that occurs in a try block has no matching catch handler, or if an exception occurs in a statement that is not in a try block, the function that contains the
