# 8.9.2 The continue Statement

The continue statement starts a new iteration of the nearest enclosing while, do, for, or foreach statement.

```
continue-statement:
    continue ;
```

The target of a continue statement is the end point of the embedded statement of the nearest enclosing while, do, for, or foreach statement. If a continue statement is not enclosed by a while, do, for, or foreach statement, a compile-time error occurs.

When multiple while, do, for, or foreach statements are nested within each other, a continue statement applies only to the innermost statement. To transfer control across multiple nesting levels, a goto statement (§8.9.3) must be used.

A continue statement cannot exit a finally block (§8.10). When a continue statement occurs within a finally block, the target of the continue statement must be within the same finally block; otherwise, a compile-time error occurs.

A continue statement is executed as follows:

+   - If the continue statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
+   - Control is transferred to the target of the continue statement.

Because a continue statement unconditionally transfers control elsewhere, the end point of a continue statement is never reachable.

> **PETER SESTOFT** Some languages—notably the Java programming language—have generalized versions of the break and continue statements, where a target label specifies which of multiple enclosing loops should be exited or resumed. The same effect can be obtained in C# using the goto statement. Moreover, although the generalized break and continue statements are disciplined versions of goto, they are almost as difficult to understand as goto statements and, in my opinion, detrimental to readability even in short programs. See examples 78 and 79 in my book *Java Precisely*, second edition.