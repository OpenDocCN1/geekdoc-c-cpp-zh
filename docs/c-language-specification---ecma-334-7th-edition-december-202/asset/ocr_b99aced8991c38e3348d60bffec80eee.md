# 13.2 End points and reachability

Every statement has an *end point*. In intuitive terms, the end point of a statement is the location that immediately follows the statement. The execution rules for composite statements (statements that contain embedded statements) specify the action that is taken when control reaches the end point of an embedded statement.

> *Example:* When control reaches the end point of a statement in a block, control is transferred to the next statement in the block. *end example*

If a statement can possibly be reached by execution, the statement is said to be *reachable*. Conversely, if there is no possibility that a statement will be executed, the statement is said to be *unreachable*.

*Example:* In the following code

```
void F()
{
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```

the second invocation of Console.WriteLine is unreachable because there is no possibility that the statement will be executed.

*end example*

A warning is reported if a statement other than *throw_statement*, *block*, or *empty_statement* is unreachable. It is specifically not an error for a statement to be unreachable.

> *Note:* To determine whether a particular statement or end point is reachable, the compiler performs flow analysis according to the reachability rules for each statement. The flow analysis takes into account the values of constant expressions (§12.23) that control the behavior of statements, but the possible values of non-constant expressions are not considered. In other words, for purposes of control flow analysis, a non-constant expression of a given type is considered to have any possible value of that type.

In the example

```
void F()
{
    const int i = 1;
    if (i == 2)
        Console.WriteLine("unreachable");
}
```

the Boolean expression of the if statement is a constant expression because both operands of the == operator are constants. As the constant expression is evaluated at compile-time, producing the value false, the Console.WriteLine invocation is considered unreachable. However, if i is changed to be a local variable

```
void F()
{
    int i = 1;
    if (i == 2)
```