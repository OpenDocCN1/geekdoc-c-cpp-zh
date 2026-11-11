# **14.2.3 Continuation**

After a handler has completed its execution, control flows to the first statement following the try construct (the statement immediately after the last handler in the sequence of handlers of which it is an element). A handler may reraise an exception, using a throw without an expression, in which case that exception is propagated.

# **14.2.4 Other Design Choices**

In terms of the design issues summarized in Section 14.1.2, the exception handling of C++ is simple. There are only user-defined exceptions, and they are not specified (though they might be declared as new classes). There is a default exception handler, unexpected, whose only action is to terminate the program. This handler catches all exceptions not caught by the program. It can be replaced by a user-defined handler. The replacement handler must be a function that returns void and takes no parameters. The replacement function is set by assigning its name to set_terminate.

A C++ function can list the types of the exceptions (the types of the throw expressions) that it could raise. This is done by attaching the reserved word throw, followed by a parenthesized list of these types, to the function header. For example,

```
int fun() throw (int, char *) { ... }
```

specifies that the function fun could raise exceptions of type int and char * but no others. The purpose of the throw clause is to notify users of the function what exceptions might be raised by the function. The throw clause is in effect a contract between the function and its callers. It guarantees that no other exception will be raised in the function. If the function does throw some unlisted exception, the program will be terminated. Note that the compiler ignores throw clauses.

If the types in the throw clause are classes, then the function can raise any exception that is derived from the listed classes. If a function header has a throw clause and raises an exception that is not listed in the throw clause and is not derived from a class listed there, the default handler is called. Note that this error cannot be detected at compile time. The list of types in the list may be empty, meaning that the function will not raise any exceptions. If there is no throw specification on the header, the function can raise any exception. The list is not part of the function's type.

If a function overrides a function that has a throw clause, the overriding function cannot have a throw clause with more exceptions than the overridden function.

Although C++ has no predefined exceptions, the standard libraries define and throw exceptions, such as out_of_range, which can be thrown by library container classes, and overflow_error, which can be thrown by math library functions.