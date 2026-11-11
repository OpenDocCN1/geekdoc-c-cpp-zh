
![](img/e22931b583977bc24a4263ee43d0f0bb_630_0.png)

**Figure 14.1** Exception-handling control flow

regardless of how subprogram execution terminates. The ability to specify such a computation is called *finalization*. The choice of whether to support finalization is obviously a design issue for exception handling.

Another design issue is the following: If users are allowed to define exceptions, how are these exceptions specified? The usual answer is to require that they be declared in the specification parts of the program units in which they can be raised. The scope of a declared exception is usually the scope of the program unit that contains the declaration.

In the case where a language provides predefined exceptions, several other design issues follow. For example, should the language run-time system provide default handlers for the built-in exceptions, or should the user be required to write handlers for all exceptions? Another question is whether predefined exceptions can be raised explicitly by the user program. This usage can be convenient if there are software-detectable situations in which the user would like to use a predefined handler.

Another issue is whether hardware-detectable errors can be handled by user programs. If not, all exceptions obviously are software detectable. A related question is whether there should be any predefined exceptions. Predefined exceptions are implicitly raised by either hardware or system software.

The exception-handling design issues can be summarized as follows:

- How and where are exception handlers specified, and what is their scope?
- How is an exception occurrence bound to an exception handler?
- Can information about an exception be passed to the handler?
- Where does execution continue, if at all, after an exception handler completes its execution? (This is the question of continuation or resumption.)
- Is some form of finalization provided?
- How are user-defined exceptions specified?
- If there are predefined exceptions, should there be the default exception handlers for programs that do not provide their own?
- Can predefined exceptions be explicitly raised?
- Are hardware-detectable errors treated as exceptions that may be handled?
- Are there any predefined exceptions?

We are now in a position to examine the exception-handling facilities of several contemporary programming languages.

## 14.2 Exception Handling in C++

The exception handling of C++ was accepted by the ANSI C++ standardization committee in 1990 and subsequently found its way into C++ implementations. The design is based in part on the exception handling of CLU, Ada, and ML. In C++, exceptions are user or library defined and explicitly raised.

### 14.2.1 Exception Handlers

C++ uses a special construct that is introduced with the reserved word try to specify the scope for exception handlers. A try construct includes a compound statement called the try clause and a list of exception handlers. The compound statement defines the scope of the following handlers. The general form of this construct is as follows:

```cpp
try {
    // Code that might raise an exception
} catch (formal parameter) {
    // A handler body
}
...
catch (formal parameter) {
    // A handler body
}
```

Each catch function is an exception handler. A catch function can have only a single formal parameter, which is similar to a formal parameter in a function definition in C++, including the possibility of it being an ellipsis (. . .). A handler with an ellipsis formal parameter is the catch-all handler; it is enacted for any raised exception if no appropriate handler was found.

The formal parameter also can be a naked type specifier, such as `float`, as in a function prototype. In such a case, the only purpose of the formal parameter is to make the handler uniquely identifiable. When information about the exception is to be passed to the handler, the formal parameter includes a variable name that is used for that purpose. Because the class of the parameter can be any user-defined class, the parameter can include as many data members as are necessary. Binding exceptions to handlers are discussed in Section 14.2.2.

In C++, exception handlers can include any C++ code.

### 14.2.2 Binding Exceptions to Handlers

In C++, exceptions are raised only by the explicit statement `throw`, whose general form in EBNF is as follows:

```cpp
throw [expression];
```

The brackets here are metasymbols used to specify that the expression is optional. A `throw` without an operand can appear only in a handler. When it appears there, it rethrows the exception, which is then handled elsewhere.

The type of the `throw` expression selects the particular handler, which of course must have a "matching" type formal parameter. In this case, *matching* means the following: A handler with a formal parameter of type `T`, `const T`, `T&` (a reference to an object of type `T`), or `const T&` matches a `throw` with an expression of type `T`. In the case where `T` is a class, a handler whose parameter is type `T` or any class that is an ancestor of `T` matches. There are more complicated situations in which a `throw` expression matches a formal parameter, but they are not described here.

An exception raised in a `try` clause causes an immediate end to the execution of the code in that `try` clause. The search for a matching handler begins with the handlers that immediately follow the `try` clause. The matching process is done sequentially on the handlers until a match is found. This means that if any other match precedes an exactly matching handler, the exactly matching handler will not be used. Therefore, handlers for specific exceptions are placed at the top of the list, followed by more generic handlers. The last handler is often one with an ellipsis (...) formal parameter, which matches any exception. This would guarantee that all exceptions are caught.

If an exception is raised in a `try` clause and there is no matching handler associated with that `try` clause, the exception is propagated. If the `try` clause is nested inside another `try` clause, the exception is propagated to the handlers associated with the outer `try` clause. If none of the enclosing `try` clauses yields a matching handler, the exception is propagated to the caller of the function in which it was raised. If the call to the function was not in a `try` clause, the exception is propagated to that function's caller. If no matching handler is found in the program through this propagation process, the default handler is called. This handler is further discussed in Section 14.2.4.

### 14.2.3 Continuation

After a handler has completed its execution, control flows to the first statement following the try construct (the statement immediately after the last handler in the sequence of handlers of which it is an element). A handler may reraise an exception, using a throw without an expression, in which case that exception is propagated.

### 14.2.4 Other Design Choices

In terms of the design issues summarized in Section 14.1.2, the exception handling of C++ is simple. There are only user-defined exceptions, and they are not specified (though they might be declared as new classes). There is a default exception handler, terminate, whose only action is to terminate the program. This handler catches all exceptions not caught by the program. It can be replaced by a user-defined handler. The replacement handler must be a function that returns void and takes no parameters. The replacement function is set by assigning its name to set_terminate.

A C++ function can list the types of the exceptions (the types of the throw expressions) that it could raise. This is done by attaching the reserved word throw, followed by a parenthesized list of these types, to the function header. For example,

```cpp
int fun() throw (int, char *) { ... }
```

specifies that the function fun could raise exceptions of type int and char * but no others. The purpose of the throw clause is to notify users of the function what exceptions might be raised by the function. The throw clause is in effect a contract between the function and its callers. It guarantees that no other exception will be raised in the function. If the function does throw some unlisted exception, the program will be terminated. Note that the compiler ignores throw clauses.

If the types in the throw clause are classes, then the function can raise any exception that is derived from the listed classes. If a function header has a throw clause and raises an exception that is not listed in the throw clause and is not derived from a class listed there, the default handler is called. Note that this error cannot be detected at compile time. The list of types in the throw clause may be empty, meaning that the function will not raise any exceptions. If there is no throw specification on the header, the function can raise any exception. The list is not part of the function's type.

If a function overrides a function that has a throw clause, the overriding function cannot have a throw clause with more exceptions than the overridden function.

Although C++ has no predefined exceptions, the standard libraries define and throw exceptions, such as out_of_range, which can be thrown by library container classes, and overflow_error, which can be thrown by math library functions.
