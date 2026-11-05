Because a `throw` statement unconditionally transfers control elsewhere, the end point of a `throw` statement is never reachable.

When an exception is thrown, control is transferred to the first `catch` clause in an enclosing `try` statement that can handle the exception. The process that takes place from the point of the exception being thrown to the point of transferring control to a suitable exception handler is known as *exception propagation*. Propagation of an exception consists of repeatedly evaluating the following steps until a `catch` clause that matches the exception is found. In this description, the *throw point* is initially the location at which the exception is thrown.

+   - In the current function member, each `try` statement that encloses the throw point is examined. For each statement *S*, starting with the innermost `try` statement and ending with the outermost `try` statement, the following steps are evaluated:
+     - If the `try` block of *S* encloses the *throw point* and if *S* has one or more `catch` clauses, the `catch` clauses are examined in order of appearance to locate a suitable handler for the exception. The first `catch` clause that specifies an exception type *T* (or a type parameter that at run-time denotes an exception type *T*) such that the run-time type of *E* derives from *T* is considered a match. If the clause contains an exception filter, the exception object is assigned to the exception variable, and the exception filter is evaluated. When a `catch` clause contains an exception filter, that `catch` clause is considered a match if the exception filter evaluates to `true`. A general `catch` (§12.11) clause is considered a match for any exception type. If a matching `catch` clause is located, the *exception propagation* is completed by transferring control to the block of that `catch` clause.
+     - Otherwise, if the `try` block or a `catch` block of *S* encloses the *throw point* and if *S* has a `finally` block, control is transferred to the `finally` block. If the `finally` block throws another exception, processing of the current exception is terminated. Otherwise, when control reaches the end point of the `finally` block, processing of the current exception is continued.
+   - If an exception handler was not located in the current function invocation, the function invocation is terminated, and one of the following occurs:
+     - If the current function is `non-async`, the steps above are repeated for the caller of the function with a *throw point* corresponding to the statement from which the function member was invoked.
+     - If the current function is `async` and task-returning, the exception is recorded in the return task, which is put into a faulted or cancelled state as described in §14.15.2.
+     - If the current function is `async` and `void`-returning, the synchronization context of the current thread is notified as described in §14.15.3.
+   - If the exception processing terminates all function member invocations in the current thread, indicating that the thread has no handler for the exception, then the thread is itself terminated. The impact of such termination is implementation-defined.

# ## 12.11 The `try` statement

The `try` statement provides a mechanism for catching exceptions that occur during execution of a block. Furthermore, the `try` statement provides the ability to specify a block of code that is always executed when control leaves the `try` statement.

```
try_statement
    : 'try' block catch_clauses
```