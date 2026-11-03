
DivideByZeroException object created by function quotient's throw statement (line 14), so that the catch handler does not make a copy of the exception object.

The catch's body (lines 39-40) prints the error message returned by function what of base-class runtime_error (i.e., the string that the DivideByZeroException constructor (lines 11-12 in Fig. 22.1) passed to the runtime_error base-class constructor.

> **Good Programming Practice 22.1**
> Associating each type of runtime error with an appropriately named exception type improves program clarity.

## 22.3 Rethrowing an Exception

A function might use a resource—like a file—and might want to release the resource (i.e., close the file) if an exception occurs. An exception handler, upon receiving an exception, can release the resource then notify its caller that an exception occurred by rethrowing the exception via the statement

throw;

Regardless of whether a handler can process an exception, the handler can rethrow the exception for further processing outside the handler. The next enclosing try block detects the rethrown exception, which a catch handler listed after that enclosing try block attempts to handle.

> **Common Programming Error 22.5**
> Executing an empty throw statement outside a catch handler abandons exception processing and terminates the program immediately.

The program of Fig. 22.3 demonstrates rethrowing an exception. In main's try block (lines 29-34), line 32 calls function throwException (lines 8-24). The throwException function also contains a try block (lines 11-15), from which the throw statement in line 14 throws an instance of standard library-class exception. Function throwException's catch handler (lines 16-21) catches this exception, prints an error message (lines 18-19) and rethrows the exception (line 20). This terminates function throwException and returns control to line 32 in the try...catch block in main. The try block terminates (so line 33 does not execute), and the catch handler in main (lines 35-38) catches this exception and prints an error message (line 37). Since we do not use the exception parameters in the catch handlers of this example, we omit the exception parameter names and specify only the type of exception to catch (lines 16 and 35).

```
1 // Fig. 22.3: fig22_03.cpp
2 // Rethrowing an exception.
3 #include <iostream>
4 #include <exception>
5 using namespace std;
6
7  // throw, catch and rethrow exception
8  void throwException()
9  {
10    // throw exception and catch it immediately
11    try
12    {
13      cout << "  Function throwException throws an exception\n";
14      throw exception(); // generate exception
15    } // end try
16    catch ( exception & ) // handle exception
17    {
18      cout << "  Exception handled in function throwException"
19        << "\n  Function throwException rethrows exception";
20      throw; // rethrow exception for further processing
21    } // end catch
22
23    cout << "This also should not print\n";
24  } // end function throwException
25
26  int main()
27  {
28    // throw exception
29    try
30    {
31      cout << "\nmain invokes function throwException\n";
32      throwException();
33      cout << "This should not print\n";
34    } // end try
35    catch ( exception & ) // handle exception
36    {
37      cout << "\n\nException handled in main\n";
38    } // end catch
39
40    cout << "Program control continues after catch in main\n";
41  } // end main
```

```
main invokes function throwException
  Function throwException throws an exception
  Exception handled in function throwException
  Function throwException rethrows exception

Exception handled in main
Program control continues after catch in main
```

Fig. 22.3 | Rethrowing an exception. (Part 2 of 2.)

## 22.4 Stack Unwinding

When an exception is thrown but not caught in a particular scope, the function call stack is “unwound,” and an attempt is made to catch the exception in the next outer try...catch block. Unwinding the function call stack means that the function in which the exception was not caught terminates, all local variables that have completed initialization in that

```
function1 is called inside main
function2 is called inside function1
function3 is called inside function2
In function 3
Exception occurred: runtime_error in function3
Exception handled in main
```

Fig. 22.4 | Stack unwinding. (Part 2 of 2.)

In main, the try block (lines 34–38) calls function1 (lines 24–28). Next, function1 calls function2 (lines 17–21), which in turn calls function3 (lines 8–14). Line 13 of function3 throws a runtime_error object. However, because no try block encloses the throw statement in line 13, stack unwinding occurs—function3 terminates at line 13, then returns control to the statement in function2 that invoked function3 (i.e., line 20). Because no try block encloses line 20, stack unwinding occurs again—function2 terminates at line 20 and returns control to the statement in function1 that invoked function2 (i.e., line 27). Because no try block encloses line 27, stack unwinding occurs one more time—function1 terminates at line 27 and returns control to the statement in main that invoked function1 (i.e., line 37). The try block of lines 34–38 encloses this statement, so the first matching catch handler located after this try block (lines 39–43) catches and processes the exception. Line 41 uses function what to display the exception message.

## 22.5 When to Use Exception Handling

Exception handling is designed to process synchronous errors, which occur when a statement executes, such as out-of-range array subscripts, arithmetic overflow (i.e., a value outside the representable range of values), division by zero, invalid function parameters, and unsuccessful memory allocation (due to lack of memory). Exception handling is not designed to process errors associated with asynchronous events (e.g., disk I/O completions, network message arrivals, mouse clicks and keystrokes), which occur in parallel with, and independent of, the program's flow of control.

> **Software Engineering Observation 22.4**
> Exception handling provides a single, uniform technique for processing problems. This helps programmers on large projects understand each other's error-processing code.

> **Software Engineering Observation 22.5**
> Exception handling enables predefined software components to communicate problems to application-specific components, which can then process the problems in an application-specific manner.

Exception handling also is useful for processing problems that occur when a program interacts with software elements, such as member functions, constructors, destructors and classes. Such software elements often use exceptions to notify programs when problems occur. This enables you to implement customized error handling for each application.

If an object has member objects, and if an exception is thrown before the outer object is fully constructed, then destructors will be executed for the member objects that have been constructed prior to the occurrence of the exception. If an array of objects has been partially constructed when an exception occurs, only the destructors for the constructed objects in the array will be called.

> **Error-Prevention Tip 22.6**
> When an exception is thrown from the constructor for an object that's created in a new expression, the dynamically allocated memory for that object is released.

> **Error-Prevention Tip 22.7**
> A constructor should throw an exception if a problem occurs while initializing an object. Before doing so, the constructor should release any memory that it dynamically allocated.

### Initializing Local Objects to Acquire Resources

An exception could preclude the operation of code that would normally release a resource (such as memory or a file), thus causing a resource leak that prevents other programs from acquiring the resource. One technique to resolve this problem is to initialize a local object to acquire the resource. When an exception occurs, the destructor for that object will be invoked and can free the resource.

## 22.7 Exceptions and Inheritance

Various exception classes can be derived from a common base class, as we discussed in Section 22.2, when we created class DivideByZeroException as a derived class of class exception. If a catch handler catches a reference to an exception object of a base-class type, it also can catch a reference to all objects of classes publicly derived from that base class—this allows for polymorphic processing of related exceptions.

> **Error-Prevention Tip 22.8**
> Using inheritance with exceptions enables an exception handler to catch related errors with concise notation. One approach is to catch each type of reference to a derived-class exception object individually, but a more concise approach is to catch pointers or references to base-class exception objects instead. Also, catching pointers or references to derived-class exception objects individually is error prone, especially if you forget to test explicitly for one or more of the derived-class reference types.

## 22.8 Processing new Failures

When operator new fails, it throws a bad_alloc exception (defined in header <new>). In this section, we present two examples of new failing. The first uses the version of new that throws a bad_alloc exception when new fails. The second uses function set_new_handler to handle new failures. [Note: The examples in Figs. 22.5–22.6 allocate large amounts of dynamic memory, which could cause your computer to become sluggish.]

### new Throwing bad_alloc on Failure

Figure 22.5 demonstrates new implicitly throwing bad_alloc on failure to allocate the requested memory. The for statement (lines 16–20) inside the try block should loop 50
