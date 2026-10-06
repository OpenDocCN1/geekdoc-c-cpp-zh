# Throwing Exceptions 231

FIGURE C3-1 Hierarchy of C++ exception classes

![](bbox=[0.068, 0.137, 0.893, 0.303])

Here ExceptionClass is the type of exception you want to throw, and stringArgument is an argument to the constructor of ExceptionClass that provides a more detailed description of what may have caused the exception. When a throw ExceptionClass is created, the exception is thrown and propagated back to the point where the function was called, and the statements in the function that follow the throw statement do not execute.

C++ has two families of exceptions that function can throw. You can select one of these or derive a class of them. Although the exception in a throw statement does not need to be derived from a standard C++ exception class, it is a good programming practice to do so. Figure C3-1 shows the family of exception classes provided by C++.

Exceptions derived from runtime_error or one of its derived are thrown by errors that are detectable at runtime, such as division by zero or numeric overflow. If such an exception is thrown, the program will halt, unless it is caught by an assertion. Unlike assertions, however, when a runtime_error exception is thrown, it can contain a message that is displayed to the user giving details about the error and the program remains handled.

Classes derived from the logic_error class represent errors in the logic of the program, such as an precondition or a failure to satisfy a condition, that you could detect before the program executes. In findBox example, if we wanted to throw an exception to indicate the failure to find the target string, we would write:

```
if (!found) {
    throw logic_error("Target not found in box!");
}
```

When we throw exceptions, we first test for an error or unusual condition using an if statement. Then if one occurs, we use the throw statement to throw an exception containing a message to our client.

To restrict the exceptions that a function or method can throw, you include a throw clause in its header. This allows the client to know that the function might throw an exception. A throw clause consists of the keyword throw followed by a list of exception types separated by commas and enclosed within parentheses. For example, here is the prototype of our findBox function with a throw clause added:

```
PlainBox<string> findBox(PlainBox boxes[], int size, string target) throw(logic_error);
```

Listing C3-3 shows the complete findBox function that throws a logic_error exception. Later in this interlude, we will derive an exception class to handle this specific error. First, however, we will look how a client can deal with a thrown exception.