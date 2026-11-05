
## constant-expression:
    expression

A constant expression must be the null literal or a value with one of the following types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, bool, string, or any enumeration type. Only the following constructs are permitted in constant expressions:

- Literals (including the null literal).
- References to const members of class and struct types.
- References to members of enumeration types.
- References to const parameters or local variables
- Parenthesized sub-expressions, which are themselves constant expressions.
- Cast expressions, provided the target type is one of the types listed above.
- checked and unchecked expressions
- Default value expressions
- The predefined +, -, !, and ~ unary operators.
- The predefined +, -, *, /, %, <<, >>, &, |, ^, &&, ||, ==, !=, <, >, <=, and >= binary operators, provided each operand is of a type listed above.
- The ?: conditional operator.

The following conversions are permitted in constant expressions:

- Identity conversions
- Numeric conversions
- Enumeration conversions
- Constant expression conversions
- Implicit and explicit reference conversions, provided that the source of the conversions is a constant expression that evaluates to the null value.

Other conversions including boxing, unboxing and implicit reference conversions of non-null values are not permitted in constant expressions. For example:

```
class C {
    const object i = 5; // error: boxing conversion not permitted
    const object str = "hello"; // error: implicit reference conversion
}
```

the initialization of i is an error because a boxing conversion is required. The initialization of str is an error because an implicit reference conversion from a non-null value is required.

Whenever an expression fulfills the requirements listed above, the expression is evaluated at compile-time. This is true even if the expression is a sub-expression of a larger expression that contains non-constant constructs.

The compile-time evaluation of constant expressions uses the same rules as run-time evaluation of non-constant expressions, except that where run-time evaluation would have thrown an exception, compile-time evaluation causes a compile-time error to occur.

Unless a constant expression is explicitly placed in an unchecked context, overflows that occur in integral-type arithmetic operations and conversions during the compile-time evaluation of the expression always cause compile-time errors (§7.19).

Constant expressions occur in the contexts listed below. In these contexts, a compile-time error occurs if an expression cannot be fully evaluated at compile-time.

- Constant declarations (§10.4).
- Enumeration member declarations (§14.3).
- case labels of a switch statement (§8.7.2).
- goto case statements (§8.9.3).
- Dimension lengths in an array creation expression (§7.6.10.4) that includes an initializer.
- Attributes (§17).

An implicit constant expression conversion (§6.1.8) permits a constant expression of type int to be converted to sbyte, byte, short, ushort, uint, or ulong, provided the value of the constant expression is within the range of the destination type.

## 7.20 Boolean expressions

A boolean-expression is an expression that yields a result of type bool; either directly or through application of operator true in certain contexts as specified in the following.

```
boolean-expression:
    expression
```

The controlling conditional expression of an if-statement (§8.7.1), while-statement (§8.8.1), do-statement (§8.8.2), or for-statement (§8.8.3) is a boolean-expression. The controlling conditional expression of the ?: operator (§7.14) follows the same rules as a boolean-expression, but for reasons of operator precedence is classified as a conditional-or-expression.

A boolean-expression is required to be implicitly convertible to bool or of a type that implements operator true. If neither requirement is satisfied, a binding-time error occurs.

When a boolean expression cannot be implicitly converted to bool but does implement operator true, then following evaluation of the expression, the operator true implementation provided by that type is invoked to produce a bool value.

The DBBool struct type in §11.4.2 provides an example of a type that implements operator true and operator false.

## 8. Statements

C# provides a variety of statements. Most of these statements will be familiar to developers who have programmed in C and C++.

- *statement:*
  *labeled-statement*
  *declaration-statement*
  *embedded-statement*

- *embedded-statement:*
  *block*
  *empty-statement*
  *expression-statement*
  *selection-statement*
  *iteration-statement*
  *jump-statement*
  *try-statement*
  *checked-statement*
  *unchecked-statement*
  *lock-statement*
  *using-statement*
  *yield-statement*

The *embedded-statement* nonterminal is used for statements that appear within other statements. The use of *embedded-statement* rather than *statement* excludes the use of declaration statements and labeled statements in these contexts. The example

```
void F(bool b) {
    if (b)
        int i = 44;
}
```

results in a compile-time error because an *if* statement requires an *embedded-statement* rather than a *statement* for its *if* branch. If this code were permitted, then the variable *i* would be declared, but it could never be used. Note, however, that by placing *i*’s declaration in a block, the example is valid.

### 8.1 End points and reachability

Every statement has an *end point*. In intuitive terms, the end point of a statement is the location that immediately follows the statement. The execution rules for composite statements (statements that contain embedded statements) specify the action that is taken when control reaches the end point of an embedded statement. For example, when control reaches the end point of a statement in a block, control is transferred to the next statement in the block.

If a statement can possibly be reached by execution, the statement is said to be *reachable*. Conversely, if there is no possibility that a statement will be executed, the statement is said to be *unreachable*.

In the example

```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label1;
    Console.WriteLine("unreachable");
    Label1:
    Console.WriteLine("reachable");
}
```

the second invocation of Console.WriteLine is unreachable because there is no possibility that the statement will be executed.

A warning is reported if the compiler determines that a statement is unreachable. It is specifically not an error for a statement to be unreachable.

To determine whether a particular statement or end point is reachable, the compiler performs flow analysis according to the reachability rules defined for each statement. The flow analysis takes into account the values of constant expressions (§7.19) that control the behavior of statements, but the possible values of non-constant expressions are not considered. In other words, for purposes of control flow analysis, a non-constant expression of a given type is considered to have any possible value of that type.

In the example

```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```

the boolean expression of the if statement is a constant expression because both operands of the == operator are constants. As the constant expression is evaluated at compile-time, producing the value false, the Console.WriteLine invocation is considered unreachable. However, if i is changed to be a local variable

```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```

the Console.WriteLine invocation is considered reachable, even though, in reality, it will never be executed.

The block of a function member is always considered reachable. By successively evaluating the reachability rules of each statement in a block, the reachability of any given statement can be determined.

In the example

```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```

the reachability of the second Console.WriteLine is determined as follows:

- The first Console.WriteLine expression statement is reachable because the block of the F method is reachable.
- The end point of the first Console.WriteLine expression statement is reachable because that statement is reachable.
- The if statement is reachable because the end point of the first Console.WriteLine expression statement is reachable.
- The second Console.WriteLine expression statement is reachable because the boolean expression of the if statement does not have the constant value false.

There are two situations in which it is a compile-time error for the end point of a statement to be reachable:
