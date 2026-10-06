# ISO/IEC 14882:2017(E)

unwind before this call to std::terminate() is implementation-defined (18.5.1).

Referring to any non-static member or base class of an object in the handler for a function-try-block of a constructor or destructor for that object results in undefined behavior.

The scope and lifetime of parameters of a function or constructor extend into the handlers of a function-try-block.

Exceptions thrown in destructors of objects with static storage duration or in constructors of namespace-scope objects with static storage duration are not caught by a function-try-block on the main function (6.6.1). Exceptions thrown in destructors of objects with thread storage duration are not caught by a function-try-block on the initial function of the thread.

If a return statement appears in a handler of the function-try-block of a constructor, the process is ill-formed.

The currently handled exception is rethrown if the end of the function-try-block of a constructor or destructor reaches. Otherwise, flow off the end of the exception-statement of a handler of a function-try-block is invoked (9.6.3).

The variable declared by the exception-declaration, of type ct or T, is initialized from the exception object, of type E, as:

+   - if T is a base class of E, the variable is copy-initialized (11.6) from the corresponding base subclass of the exception object;
- otherwise, the variable is copy-initialized (11.6) from the exception object.

The lifetime of the exception ends when the handler exits, with the destruction of any automatic objects initialized within the handler.

When the handler deletes an object, changes to that object will not affect the exception object. When the handler refers to an exception, any changes to the rethrown exception are changes to the exception object and will effect that object be rethrown.

# 18.4 Exception specifications [except.spec]

The predicate indicates whether a function cannot throw except it is called the exception specification of the function. If the predicate is false, the function has a potentially-throwing exception specification, or explicitly by using a noexcept exception specification. The exception specification is either implicitly, or explicitly by using a noexcept-specifier as a suffix of a function declarator (11.3.5).

```
noexcept-specifier:
except { constant-expression }
```

In noexcept-specifier, the constant-expression, if supplied, shall be a contextually evaluated constant expression of type bool (8.20); constant expression is the exception specification of the type in which the noexcept-specifier appears. A (token) that follows noexcept is not part of the noexcept-specifier and does not commence an initializer (11.6). The noexcept-specifier without a constant-expression is deprecated (D.3), and equivalent to the noexcept-specifier(throw()).

If a declaration of a function does not have a noexcept-specifier, the declaration has a potentially throwing exception specification unless it is a destructor or a declaration function or is executed on its first declaration, in which cases it has a noexcept specification as specified below and no other declaration for that function shall have a noexcept-specifier. (17.7.2) a noexcept-specifier may be specified, but is not required. If a noexcept-specifier is specified in an explicit instantiation directive, the exception specification shall be the same as the exception specification of all other declarations of that function.