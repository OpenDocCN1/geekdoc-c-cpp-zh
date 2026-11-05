
- If E is a non-nullable value type then the finally clause is expanded to the semantic equivalent of:

```csharp
finally {
    ((System.IDisposable)e).Dispose();
}
```

- Otherwise the finally clause is expanded to the semantic equivalent of:

```csharp
finally {
    if (e != null) ((System.IDisposable)e).Dispose();
}
```

except that if E is a value type, or a type parameter instantiated to a value type, then the cast of e to System.IDisposable will not cause boxing to occur.

- Otherwise, if E is a sealed type, the finally clause is expanded to an empty block:

```csharp
finally {
}
```

- Otherwise, the finally clause is expanded to:

```csharp
finally {
    System.IDisposable d = e as System.IDisposable;
    if (d != null) d.Dispose();
}
```

The local variable d is not visible to or accessible to any user code. In particular, it does not conflict with any other variable whose scope includes the finally block.

The order in which foreach traverses the elements of an array, is as follows: For single-dimensional arrays elements are traversed in increasing index order, starting with index 0 and ending with index Length - 1. For multi-dimensional arrays, elements are traversed such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.

The following example prints out each value in a two-dimensional array, in element order:

```csharp
using System;

class Test
{
    static void Main() {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };

        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);

        Console.WriteLine();
    }
}
```

The output produced is as follows:

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

In the example

```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```

the type of n is inferred to be int, the element type of numbers.

## 8.9 Jump statements

Jump statements unconditionally transfer control.

- jump-statement:
  - break-statement
  - continue-statement
  - goto-statement
  - return-statement
  - throw-statement

The location to which a jump statement transfers control is called the *target* of the jump statement.

When a jump statement occurs within a block, and the target of that jump statement is outside that block, the jump statement is said to *exit* the block. While a jump statement may transfer control out of a block, it can never transfer control into a block.

Execution of jump statements is complicated by the presence of intervening *try* statements. In the absence of such *try* statements, a jump statement unconditionally transfers control from the jump statement to its target. In the presence of such intervening *try* statements, execution is more complex. If the jump statement exits one or more *try* blocks with associated *finally* blocks, control is initially transferred to the *finally* block of the innermost *try* statement. When and if control reaches the end point of a *finally* block, control is transferred to the *finally* block of the next enclosing *try* statement. This process is repeated until the *finally* blocks of all intervening *try* statements have been executed.

In the example

```
using System;
class Test
{
    static void Main() {
        while (true) {
            try {
                try {
                    Console.WriteLine("Before break");
                    break;
                }
                finally {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```

the *finally* blocks associated with two *try* statements are executed before control is transferred to the target of the jump statement.

The output produced is as follows:

```
Before break
Innermost finally block
Outermost finally block
After break
```

### 8.9.1 The break statement

The break statement exits the nearest enclosing *switch*, *while*, *do*, *for*, or *foreach* statement.

- break-statement:
  - break ;

The target of a break statement is the end point of the nearest enclosing switch, while, do, for, or foreach statement. If a break statement is not enclosed by a switch, while, do, for, or foreach statement, a compile-time error occurs.

When multiple switch, while, do, for, or foreach statements are nested within each other, a break statement applies only to the innermost statement. To transfer control across multiple nesting levels, a goto statement (§8.9.3) must be used.

A break statement cannot exit a finally block (§8.10). When a break statement occurs within a finally block, the target of the break statement must be within the same finally block; otherwise, a compile-time error occurs.

A break statement is executed as follows:

- If the break statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the break statement.

Because a break statement unconditionally transfers control elsewhere, the end point of a break statement is never reachable.

### 8.9.2 The continue statement

The continue statement starts a new iteration of the nearest enclosing while, do, for, or foreach statement.

```
continue-statement:
    continue ;
```

The target of a continue statement is the end point of the embedded statement of the nearest enclosing while, do, for, or foreach statement. If a continue statement is not enclosed by a while, do, for, or foreach statement, a compile-time error occurs.

When multiple while, do, for, or foreach statements are nested within each other, a continue statement applies only to the innermost statement. To transfer control across multiple nesting levels, a goto statement (§8.9.3) must be used.

A continue statement cannot exit a finally block (§8.10). When a continue statement occurs within a finally block, the target of the continue statement must be within the same finally block; otherwise a compile-time error occurs.

A continue statement is executed as follows:

- If the continue statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the continue statement.

Because a continue statement unconditionally transfers control elsewhere, the end point of a continue statement is never reachable.

### 8.9.3 The goto statement

The goto statement transfers control to a statement that is marked by a label.

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

The target of a goto identifier statement is the labeled statement with the given label. If a label with the given name does not exist in the current function member, or if the goto statement is not within the scope of the label, a compile-time error occurs. This rule permits the use of a goto statement to transfer control out of a nested scope, but not into a nested scope. In the example

```
using System;
class Test
{
    static void Main(string[] args) {
        string[,] table = {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };
        foreach (string str in args) {
            int row, colm;
            for (row = 0; row <= 1; ++row)
                for (colm = 0; colm <= 2; ++colm)
                    if (str == table[row,colm])
                        goto done;
            Console.WriteLine("{0} not found", str);
            continue;
        done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, colm);
        }
    }
}
```

a goto statement is used to transfer control out of a nested scope.

The target of a goto case statement is the statement list in the immediately enclosing switch statement (§8.7.2), which contains a case label with the given constant value. If the goto case statement is not enclosed by a switch statement, if the constant-expression is not implicitly convertible (§6.1) to the governing type of the nearest enclosing switch statement, or if the nearest enclosing switch statement does not contain a case label with the given constant value, a compile-time error occurs.

The target of a goto default statement is the statement list in the immediately enclosing switch statement (§8.7.2), which contains a default label. If the goto default statement is not enclosed by a switch statement, or if the nearest enclosing switch statement does not contain a default label, a compile-time error occurs.

A goto statement cannot exit a finally block (§8.10). When a goto statement occurs within a finally block, the target of the goto statement must be within the same finally block, or otherwise a compile-time error occurs.

A goto statement is executed as follows:

- If the goto statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the goto statement.
