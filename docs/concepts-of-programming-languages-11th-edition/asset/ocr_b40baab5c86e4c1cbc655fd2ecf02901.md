+   - Where does execution continue, if at all, after an exception handler completes its execution? (This is the question of continuation or resumption.)
+   - Is some form of finalization provided?
+   - How are user-defined exceptions specified?
+   - If there are predefined exceptions, should there be the default exception handlers for programs that do not provide their own?
+   - Can predefined exceptions be explicitly raised?
+   - Are hardware-detectable errors treated as exceptions that may be handled?
+   - Are there any predefined exceptions?

We are now in a position to examine the exception-handling facilities of several contemporary programming languages.

# 14.2 Exception Handling in C++

The exception handling of C++ was accepted by the ANSI C++ standardization committee in 1990 and subsequently found its way into C++ implementations. The design is based in part on the exception handling of CLU, Ada, and ML. In C++, exceptions are user or library defined and explicitly raised.

# 14.2.1 Exception Handlers

C++ uses a special construct that is introduced with the reserved word try to specify the scope for exception handlers. A try construct includes a compound statement called the try clause and a list of exception handlers. The compound statement defines the scope of the following handlers. The general form of this construct is as follows:

```
try {
  /** Code that might raise an exception
  } catch (formal parameter) {
    /** A handler body
  }
  . . .
catch (formal parameter) {
  /** A handler body
}
```

Each catch function is an exception handler. A catch function can have only a single formal parameter, which is similar to a formal parameter in a function definition in C++, including the possibility of it being an ellipsis (. . .). A handler with an ellipsis formal parameter is the catch-all handler;