```
static void Main() {
    try {
        F();
    }
    catch (Exception e) {
        Console.WriteLine("Exception in Main: " + e.Message);
    }
}
```

the method F catches an exception, writes some diagnostic information to the console, alters the exception variable, and re-throws the exception. The exception that is re-thrown is the original exception, so the output produced is:

```
Exception in F: G
Exception in Main: G
```

If the first catch block had thrown e instead of rethrowing the current exception, the output produced is would be as follows:

```
Exception in F: G
Exception in Main: F
```

It is a compile-time error for a break, continue, or goto statement to transfer control out of a finally block. When a break, continue, or goto statement occurs in a finally block, the target of the statement must be within the same finally block, or otherwise a compile-time error occurs.

It is a compile-time error for a return statement to occur in a finally block.

A try statement is executed as follows:

+   - Control is transferred to the try block.
+   - When and if control reaches the end point of the try block:
+     - If the try statement has a finally block, the finally block is executed.
+     - Control is transferred to the end point of the try statement.
+   - If an exception is propagated to the try statement during execution of the try block:
+     - The catch clauses, if any, are examined in order of appearance to locate a suitable handler for the exception. The first catch clause that specifies the exception type or a base type of the exception type is considered a match. A general catch clause is considered a match for any exception type. If a matching catch clause is located:
+       - If the matching catch clause declares an exception variable, the exception object is assigned to the exception variable.
+       - Control is transferred to the matching catch block.
+       - When and if control reaches the end point of the catch block:
+         - If the try statement has a finally block, the finally block is executed.
+         - Control is transferred to the end point of the try statement.
+       - If an exception is propagated to the try statement during execution of the catch block:
+         - If the try statement has a finally block, the finally block is executed.
+         - The exception is propagated to the next enclosing try statement.
+     - If the try statement has no catch clauses or if no catch clause matches the exception: