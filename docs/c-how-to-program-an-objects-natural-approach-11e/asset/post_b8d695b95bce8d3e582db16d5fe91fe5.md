
### Checkpoint

1. **(Fill-in)** A typical derived class of runtime_error defines only a(n) ________.
   **Answer:** constructor that passes an error-message string to the base-class constructor.
2. **(Fill-in)** Generally, you should derive a custom exception class from a(n) ________ and choose a name that makes it clear what problem occurred.
   **Answer:** C++ standard library exception class.

## 12.2.2 Demonstrating Exception Handling

Figure 12.2 uses exception handling to wrap code that might throw a DivideByZeroException and to handle that exception should one occur. The quotient function receives two doubles, divides the first by the second and returns the double result. The function treats all attempts to divide by zero as errors. If the second argument is zero, it throws a DivideByZeroException (line 13) to indicate this problem to the caller. The throw operand can be an object of any copy-constructible type, not just exception and its derived types. Copy-constructible types are required because the exception mechanism copies the exception into a temporary exception object.^15

```cpp
// fig12_02.cpp
// Example that throws an exception on
// an attempt to divide by zero.
#include <format>
#include <iostream>
#include "DivideByZeroException.h" // DivideByZeroException class

// performs division only if the denominator is not zero;
// otherwise, throws DivideByZeroException object
double quotient(double numerator, double denominator) {
    // throw DivideByZeroException if trying to divide by zero
    if (denominator == 0.0) {
        throw DivideByZeroException{};
    }

    // return division result
    return numerator / denominator;
}

int main() {
    int number1{}; // user-specified numerator
    int number2{}; // user-specified denominator

    std::cout << "Enter two integers (end-of-file to end): ";

    // enable user to enter two integers to divide
    while (std::cin >> number1 >> number2) {
       // try block contains code that might throw exception
       // and code that will not execute if an exception occurs
       try {
          double result{quotient(number1, number2)};
          std::cout << std::format("The quotient is: {:.2f}\n", result);
       }
       catch (const DivideByZeroException& divideByZeroException) {
          std::cout << std::format("Exception occurred: {}\n",
             divideByZeroException.what());
       }

       std::cout << "\nEnter two integers (end-of-file to end): ";
    }

    std::cout << '\n';
}
```

**Fig. 12.2** | Example that throws an exception on an attempt to divide by zero. (Part 1 of 2.)

**Fig. 12.2** | Example that throws an exception on an attempt to divide by zero. (Part 2 of 2.)

![](img/7b5e2088e71c7f78681d4ddbcf104c06_718_0.png)

Assuming the user does not specify 0 as the denominator for the division, `quotient` returns the division result. If the user enters 0 for the denominator, `quotient` throws an exception. In this case, main handles the exception then asks the user to enter two new values before calling `quotient` again. In this way, the program can continue executing even after improper input, making the program more robust. In the sample output, the first two lines show a successful calculation, and the next two show a failure due to an attempt to divide by zero. After we discuss the code, we’ll consider the user inputs and flows of control that yield the outputs shown in Fig. 12.3.

### Checkpoint

- **(Fill-in)** The operand of a throw can be of any ______ type, not just objects of types that directly or indirectly derive from exception.
  
  **Answer:** copy-constructible

## 12.2.3 Enclosing Code in a try Block

The program prompts the user to enter two integers, then inputs them in the while loop’s condition (line 27). Line 31 passes the values to `quotient` (lines 10–18), which either divides the integers and returns a result or throws an exception if the user attempts to divide by zero.

Line 13 in `quotient` is known as the throw point. Exception handling is geared to situations where the function that detects an error cannot perform its task.¹⁶

The try block in lines 30–33 executes two statements:

- the `quotient` function call (line 31), which can throw an exception, and
- the statement that displays the division result (line 32).

Line 32 executes only if `quotient` successfully returns a result.

## 12.2.4 Defining a catch Handler for DivideByZeroExceptions

At least one catch handler (lines 34–37) must immediately follow each try block. An **exception parameter should be declared as a const reference to the exception type to process**—in this case, a DivideByZeroException. This has two key benefits:

- It prevents copying the exception as part of the catch operation.
- It enables catching derived-class exceptions without slicing (see below).

### Catching By Reference Avoids Slicing

When an exception occurs in a try block, C++ executes the **first catch handler** with a parameter of the same type as, or a base-class type of, the thrown exception’s type. If a base-class catch handler catches a derived-class exception object **by value**, only the base-class portion of the derived-class exception object will be copied into the exception parameter. This logic error, known as slicing, occurs when a derived-class object is copied or assigned to a base-class object. Always catch exceptions by **reference to prevent slicing**.

### Catch Parameter Name

An exception parameter that includes the *optional* parameter name (as in line 34) enables the catch handler to interact with the caught exception. Line 36 calls its `what` member function to get the exception’s error message.

### Tasks Performed in catch Handlers

Typical tasks performed by catch handlers include

- logging errors to a file that developers can study for debugging purposes,
- terminating the program gracefully,
- trying an alternative strategy to accomplish the failed task,
- rethrowing the exception to the current function’s caller or
- throwing a different exception type.

This example’s catch handler simply reports that the user attempted to divide by zero for demonstration purposes.

16. C++ Core Guidelines, “E.2: Throw an Exception to Signal That a Function Can’t Perform Its Assigned Task.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#e-throw.

### Common Errors When Defining catch Handlers

Programmers new to exception handling should be aware of several common coding errors:

- It’s a syntax error to place code between a try block and its corresponding catch handlers or between its catch handlers.
- Each catch handler can have only one parameter—specifying a comma-separated list of exception parameters is a syntax error.
- It’s a compilation error to catch the same type in multiple catch handlers following a single try block.
- It’s a logic error to catch a base-class exception before a derived-class exception—compilers typically warn you when this occurs.

### Checkpoint

1. **(Fill-in)** Declare each exception parameter as a(n) ________ to prevent copying the exception object and to enable catching derived-class exceptions.
   **Answer:** const reference to the exception type to handle.
2. **(Fill-in)** When an exception occurs in a try block, C++ executes the first catch handler with a parameter of the same type as, or a(n) ________ of, the thrown exception’s type.
   **Answer:** base-class type
3. **(Fill-in)** The logic error known as ________ occurs when a derived-class object is copied into or assigned to a base-class object.
   **Answer:** slicing.

## 12.2.5 Termination Model of Exception Handling

If no exceptions occur in a try block, program control continues with the first statement after the last catch following that try block. If an exception does occur, the try block terminates immediately—any local variables defined in that block go out of scope. This is a strength of exception handling. Destructors for the try block’s local variables are guaranteed to run, enabling programs to avoid resource leaks.¹⁷ Next, the program searches for and executes the first matching catch handler. If execution reaches that catch handler’s closing right brace (}), the exception is considered handled. Any local variables in the catch handler, including the catch parameter, go out of scope.

C++ uses the termination model of exception handling, in which program control cannot return to the throw point. Instead, control resumes with the first statement (line 39) after the try block’s last catch handler.

If an exception occurs in a function and is not caught there, the function terminates immediately. The program attempts to locate an enclosing try block in the calling function. This process, called stack unwinding, is discussed in Section 12.5.

17. “Technical Report on C++ Performance,” February 15, 2006. Accessed April 18, 2023. http://www.open-std.org/jtc1/sc22/wg21/docs/TR18015.pdf (page 34).
