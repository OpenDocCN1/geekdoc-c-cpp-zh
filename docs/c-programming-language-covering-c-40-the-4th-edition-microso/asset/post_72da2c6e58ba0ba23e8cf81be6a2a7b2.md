
## 8.9.3 The goto Statement

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
            int row, col;
            for (row = 0; row <= 1; ++row)
                for (col = 0; col <= 2; ++col)
                    if (str == table[row,col])
                        goto done;
            Console.WriteLine("{0} not found", str);
            continue;
        done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, col);
    }
}
```

a goto statement is used to transfer control out of a nested scope.

The target of a goto case statement is the statement list in the immediately enclosing switch statement (§8.7.2), which contains a case label with the given constant value. If the goto case statement is not enclosed by a switch statement, if the constant-expression is not implicitly convertible (§6.1) to the governing type of the nearest enclosing switch statement, or if the nearest enclosing switch statement does not contain a case label with the given constant value, a compile-time error occurs.

The target of a goto default statement is the statement list in the immediately enclosing switch statement (§8.7.2), which contains a default label. If the goto default statement is not enclosed by a switch statement, or if the nearest enclosing switch statement does not contain a default label, a compile-time error occurs.

A goto statement cannot exit a finally block (§8.10). When a goto statement occurs within a finally block, the target of the goto statement must be within the same finally block; otherwise, a compile-time error occurs.

> BILL WAGNER These rules make goto a little less than pure evil in C#, but I've yet to see a good use for it.

A goto statement is executed as follows:

- If the goto statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the goto statement.

Because a goto statement unconditionally transfers control elsewhere, the end point of a goto statement is never reachable.

> CHRIS SELLS Please don't use labels or goto statements. I've never read any code that wasn't more readable without them.

> CHRISTIAN NAGEL Although goto statements make sense within switch statements as explicit fall-through options, you shouldn't use them in other scenarios.

> PETER SESTOFT Don Knuth's 1974 paper “Structured Programming with go to Statements” throws a lot of light on alternatives to the goto statement and identifies sensible uses of the goto statement. In the end, Knuth does conclude that “we should, indeed, abolish go to . . . at least as an experiment in training people to formulate their abstractions more carefully.” Just the acknowledgments list of that paper presents a “who’s who” of programming language pioneers.

> The best reason for including goto in C# probably is that you may want to generate code that uses goto—for instance, parsers, lexers, automata, statecharts, virtual machines, and similar programs.

## 8.9.4 The return Statement

The return statement returns control to the caller of the function member in which the return statement appears.

```
return-statement:
    return expression_opt ;
```

A return statement with no expression can be used only in a function member that does not compute a value—that is, a method with the return type void, the set accessor of a property or indexer, the add and remove accessors of an event, an instance constructor, a static constructor, or a destructor.

A return statement with an expression can only be used in a function member that computes a value—that is, a method with a non-void return type, the get accessor of a property or indexer, or a user-defined operator. An implicit conversion (§6.1) must exist from the type of the expression to the return type of the containing function member.

> > **VLADIMIR RESHETNIKOV**  If the return statement is within an anonymous function, the rules from §6.5 are applied instead.

It is a compile-time error for a return statement to appear in a finally block (§8.10).

A return statement is executed as follows:

- If the return statement specifies an expression, the expression is evaluated and the resulting value is converted to the return type of the containing function member by an implicit conversion. The result of the conversion becomes the value returned to the caller.
- If the return statement is enclosed by one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all enclosing try statements have been executed.
- Control is returned to the caller of the containing function member.

Because a return statement unconditionally transfers control elsewhere, the end point of a return statement is never reachable.

## 8.9.5 The throw Statement

The throw statement throws an exception.

```
throw-statement:
    throw expression_opt ;
```

A throw statement with an expression throws the value produced by evaluating the expression. The expression must denote a value of the class type System.Exception, of a class type that derives from System.Exception or of a type parameter type that has System.Exception (or a subclass thereof) as its effective base class. If evaluation of the expression produces null, a System.NullReferenceException is thrown instead.

> **PETER SESTOFT** For this reason, an exception thrown in C# is never null and, therefore, the try-catch matching of an exception (on its class) described in §8.10 makes sense. In fact, the .NET/CLI intermediate language instruction called throw behaves like the C# throw statement in this respect. Thus, even if the exception was thrown by code written in another .NET/CLI language, it would be non-null when handled by the try-catch statement.

A throw statement with no expression can be used only in a catch block, in which case that statement rethrows the exception that is currently being handled by that catch block.

> **VLADIMIR RESHETNIKOV** A throw statement with no expression is not allowed in a finally block or anonymous function that is nested inside the nearest enclosing catch block:

```csharp
delegate void F();
class Program
{
    static void Main()
    {
        try
        {
        }
        catch
        {
            F f = () => { throw; }; // Error CS8156
            try
            {
            }
            finally
            {
                throw;          // Error CS0724
            }
        }
    }
}
```

Because a throw statement unconditionally transfers control elsewhere, the end point of a throw statement is never reachable.

When an exception is thrown, control is transferred to the first catch clause in an enclosing try statement that can handle the exception. The process that takes place from the point of the exception being thrown to the point of transferring control to a suitable exception handler is known as *exception propagation*. Propagation of an exception consists of repeatedly evaluating the following steps until a catch clause that matches the exception is found. In this description, the *throw point* is initially the location at which the exception is thrown.

- In the current function member, each try statement that encloses the throw point is examined. For each statement S, starting with the innermost try statement and ending with the outermost try statement, the following steps are evaluated:
  - If the try block of S encloses the throw point and if S has one or more catch clauses, the catch clauses are examined in order of appearance to locate a suitable handler for the exception. The first catch clause that specifies the exception type or a base type of the exception type is considered a match. A general catch clause (§8.10) is considered a match for any exception type. If a matching catch clause is located, the exception propagation is completed by transferring control to the block of that catch clause.
  - Otherwise, if the try block or a catch block of S encloses the throw point and if S has a finally block, control is transferred to the finally block. If the finally block throws another exception, processing of the current exception is terminated. Otherwise, when control reaches the end point of the finally block, processing of the current exception is continued.
- If an exception handler was not located in the current function member invocation, the function member invocation is terminated. The steps above are then repeated for the caller of the function member with a throw point corresponding to the statement from which the function member was invoked.
- If the exception processing terminates all function member invocations in the current thread, indicating that the thread has no handler for the exception, then the thread is itself terminated. The impact of such termination is implementation-defined.

> > **BILL WAGNER** This process implies that you should do some basic cleanup in the topmost methods for all your threads. Otherwise, the behavior of your application will be undefined in the face of exceptions that will cause threads to be terminated.
