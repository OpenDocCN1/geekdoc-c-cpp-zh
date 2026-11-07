
We preset the compiler options for this example to

```text
-std=c++2a -fcontracts
```

which, again, compiles the code with C++20 and default-level contracts support, so the line 10 `audit-level` precondition contract is ignored. In main, we created two vectors of integers containing the same values—v1 is sorted (line 36), and v2 is unsorted (line 42). With the initial compiler settings, the precondition that ensures the vector is sorted is not tested, so the `binarySearch` calls in lines 16 and 21 complete, and the program displays the output:

```text
70 was found in v1
60 was not found in v2
```

Because the `audit-level` precondition was ignored, our program has a logic error. The second line of output shows that 60 was not found in v2. Again, the algorithm expects v2 to be sorted, so it failed to find 60, even though it’s in v2. Changing the contract build level to audit in the compiler options, as in

```text
-std=c++2a -fcontracts -fcontract-build-level=audit
```

enables audit level contract checking. When the program runs with audit contracts enabled, the vector v1 in line 37’s `binarySearch` call satisfies the precondition in line 10 and, as before, lines 38–39 output

```text
70 was found in v1
```

However, the vector v2 in line 43’s `binarySearch` call causes a contract violation, resulting in the error message:

```text
default std::handle_contract_violation called:
  ./example.cpp 10 binarySearch<int> is_sorted(begin(items), end(items)) audit
  default 0
```

### Custom Contract Violation Handler

The examples so far used the default contract violation handler. When a contract violation occurs, a `contract_violation` object is created containing the following information:

- the line number of the violation—returned by member function `line_number`,
- the source-code filename—returned by member function `file_name`,
- the function name in which the violation occurred—returned by member function `function_name`,
- a description of the condition that was violated—returned by member function `comment` and
- the contract level—returned by member function `assertion_level`.

The contract_violation is passed to the violation handler function of the form

```cpp
void handle_contract_violation(const contract_violation& violation) {
    // handler code
}
```

The experimental contracts implementation in g++ provides a default implementation of this function. If you define your own, g++ will call your version.

### Checkpoint

- 1 (True/False) A key idea behind incorporating contracts is that many errors we currently deal with via exceptions can be located via preconditions and postconditions, then eliminated by fixing the code.

    Answer: True.

- 2 (Fill-in) The contract attribute ................ specifies a function's preconditions that are checked before the function's body begins executing, and the attribute ................ specifies a function's postconditions that are checked just before the function returns.

    Answer: expects, ensures.

- 3 (Code) Write an assertion that tests whether an integer exam grade is in the range 0 through 100.

    Answer: [[assert: grade >= 0 && grade <= 100]];

    Note that the assert in the preceding statement is not an assert macro.

## 12.14 Wrap-Up

C++ is used to build real-world, mission-critical and business-critical software. The systems it's used for are often massive. In this chapter, you learned that it's essential to eliminate bugs during development and decide how to handle problems once the software is in production.

We discussed the ways that exceptions may surface in your code. We discussed how exception handling helps you write robust, fault-tolerant programs that catch infrequent problems and continue executing, perform appropriate cleanup and terminate gracefully, or terminate abruptly in the case of unanticipated exceptions.

We reviewed exception-handling concepts in an example that demonstrated the flows of control when a program executes successfully and when an exception occurs. We discussed use-cases for catching, then rethrowing exceptions. We showed how stack unwinding enables other functions to handle exceptions that are not caught in a particular scope.

You learned when to use exceptions. We also introduced the exception guarantees you can provide in your code—no guarantee, the basic exception guarantee, the strong exception guarantee and the no-throw exception guarantee. We discussed why exceptions are used to indicate errors during construction and why destructors should not throw exceptions. We also showed how to use function try blocks to catch exceptions from a constructor's member-initializer list or from base-class destructors when a derived-class object is destroyed.

You saw that operator new throws bad_alloc exceptions when dynamic memory allocation fails. We also showed how dynamic memory allocation failures were handled in legacy C++ code with set_new_handler.

We introduced the C++ standard library exception class hierarchy and created a custom exception class that inherited from a C++ standard library exception class. You learned why it’s important to catch exceptions by reference to enable exception handlers to catch exception types related by inheritance and without slicing. We also introduced logging exceptions into a file that developers can analyze later for debugging purposes.

We discussed why some organizations disallow exception handling. You also saw that some libraries provide dual interfaces, so developers can choose whether to use versions of functions that throw exceptions or versions that set error codes.

The chapter concluded with an introduction to the contracts feature, originally adopted for C++20 but delayed to a future C++ version. We showed how to use contracts to test preconditions, postconditions and assertions at runtime. You learned that these test conditions that should always be true in correct code. You saw that if such conditions are false, contract violations occur and, by default, the code terminates immediately. This enables you to find errors faster, eliminate them during development and create more robust code.

Chapter 6 introduced the array and vector standard library classes. In Chapter 13, you’ll learn about many additional C++ standard library containers as well as iterators, which are used by standard library algorithms to walk through containers and manipulate their elements.

## Exercises

- 12.1 If no exceptions are thrown in a try block, where does control proceed after the try block completes execution?

- 12.2 What happens if an exception is thrown outside a try block?

- 12.3 Give a key advantage and a key disadvantage of using catch(...).

- 12.4 What happens if no catch handler matches the type of a thrown object?

- 12.5 What happens if several handlers match the type of the thrown object?

- 12.6 Suppose a catch handler with a precise match to an exception object type is available. Under what circumstances might a different handler be executed for exception objects of that type?

- 12.7 What does the statement throw; in a catch handler do?

- 12.8 *(Exceptional Conditions)* List various exceptional conditions that have occurred throughout this textbook. List as many additional exceptional conditions as you can. For each of these exceptions, describe briefly how a program typically would handle the exception using the exception-handling techniques discussed in this chapter. Some typical exceptions are division by zero, arithmetic overflow, array subscript out of bounds, exhaustion of the free store, etc.

- 12.9 *(catch Parameter)* Under what circumstances would you not provide a parameter name when defining the type of object that will be caught by a handler?

- 12.10 **(throw Statement)** Where in a program would you normally expect to find the following statement?

    ```cpp
    throw;
    ```

    What would happen if that statement appeared in a different part of the program?

- 12.11 **(Exception Handling vs. Other Schemes)** Compare and contrast exception handling with the various other error-processing schemes discussed in the text.

- 12.12 **(Handling Related Exceptions)** Describe a technique for handling related exceptions.

- 12.13 **(Throwing Exceptions from a catch)** Suppose a program throws an exception and the appropriate exception handler begins executing. Now suppose that the exception handler itself throws the same exception. Does this create infinite recursion? Write a program to check your observation.

- 12.14 **(Catching Derived-Class Exceptions)** Write a program using classes from the C++ standard library’s exception hierarchy to prove that a catch handler specifying a base-class exception type can catch derived-class exceptions.

- 12.15 **(Local-Variable Destructors)** Write a program illustrating that all destructors for objects constructed in a block are called before an exception is thrown from that block.

- 12.16 **(Member-Object Destructors)** Write a program illustrating that member-object destructors are called for only those member objects that were constructed before an exception occurred.

- 12.17 **(Catching All Exceptions)** Write a program that demonstrates several exception types being caught with the `catch(...)` exception handler.

- 12.18 **(Order of Exception Handlers)** Write a program illustrating that the order of exception handlers is important. The first matching handler is the one that executes. Attempt to compile and run your program two different ways to show that two different handlers execute with two different effects.

- 12.19 **(Constructors Throwing Exceptions)** Write a program that shows a constructor passing information about constructor failure to an exception handler after a try block.

- 12.20 **(Rethrowing Exceptions)** Write a program that illustrates rethrowing an exception.

- 12.21 **(Uncaught Exceptions)** Write a program that illustrates that a function with its own try block does not have to catch every possible error generated within the try. Some exceptions should slip through and be handled in outer scopes.

- 12.22 **(Stack Unwinding)** Write a program that throws an exception from a deeply nested function and still has the catch handler following the try block enclosing the initial call in `main` catch the exception.
