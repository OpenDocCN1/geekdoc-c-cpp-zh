
- Overloaded unary operators: +, -, !, ~, ++, --, true, false
- Overloaded binary operators: +, -, *, /, %, &, &&, |, ||, ??, ^, <<, >>, ==, !=, >, <, >=, <=
- Assignment operators: +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=
- Implicit and explicit conversions

When no dynamic expressions are involved, C# defaults to static binding, which means that the compile-time types of constituent expressions are used in the selection process. However, when one of the constituent expressions in the operations listed above is a dynamic expression, the operation is instead dynamically bound.

## 7.2.1 Binding-time

Static binding takes place at compile-time, whereas dynamic binding takes place at run-time. In the following sections, the term binding-time refers to either compile-time or run-time, depending on when the binding takes place.

The following example illustrates the notions of static and dynamic binding and of binding-time:

```
object o = 5;
dynamic d = 5;
Console.WriteLine(5); // static binding to Console.WriteLine(int)
Console.WriteLine(o); // static binding to Console.WriteLine(object)
Console.WriteLine(d); // dynamic binding to Console.WriteLine(int)
```

The first two calls are statically bound: the overload of Console.WriteLine is picked based on the compile-time type of their argument. Thus, the binding-time is compile-time.

The third call is dynamically bound: the overload of Console.WriteLine is picked based on the run-time type of its argument. This happens because the argument is a dynamic expression – its compile-time type is dynamic. Thus, the binding-time for the third call is run-time.

## 7.2.2 Dynamic binding

The purpose of dynamic binding is to allow C# programs to interact with dynamic objects, i.e. objects that do not follow the normal rules of the C# type system. Dynamic objects may be objects from other programming languages with different types systems, or they may be objects that are programmatically setup to implement their own binding semantics for different operations.

The mechanism by which a dynamic object implements its own semantics is implementation defined. A given interface – again implementation defined – is implemented by dynamic objects to signal to the C# run-time that they have special semantics. Thus, whenever operations on a dynamic object are dynamically bound, their own binding semantics, rather than those of C# as specified in this document, take over.

While the purpose of dynamic binding is to allow interoperation with dynamic objects, C# allows dynamic binding on all objects, whether they are dynamic or not. This allows for a smoother integration of dynamic objects, as the results of operations on them may not themselves be dynamic objects, but are still of a type unknown to the programmer at compile-time. Also dynamic binding can help eliminate error-prone reflection-based code even when no objects involved are dynamic objects.

The following sections describe for each construct in the language exactly when dynamic binding is applied, what compile time checking – if any – is applied, and what the compile-time result and expression classification is.

## 7.2.3 Types of constituent expressions

When an operation is statically bound, the type of a constituent expression (e.g. a receiver, an argument, an index or an operand) is always considered to be the compile-time type of that expression.

When an operation is dynamically bound, the type of a constituent expression is determined in different ways depending on the compile-time type of the constituent expression:

- A constituent expression of compile-time type dynamic is considered to have the type of the actual value that the expression evaluates to at runtime
- A constituent expression whose compile-time type is a type parameter is considered to have the type which the type parameter is bound to at runtime
- Otherwise the constituent expression is considered to have its compile-time type.

## 7.3 Operators

Expressions are constructed from operands and operators. The operators of an expression indicate which operations to apply to the operands. Examples of operators include +, -, *, /, and new. Examples of operands include literals, fields, local variables, and expressions.

There are three kinds of operators:

- Unary operators. The unary operators take one operand and use either prefix notation (such as ~x) or postfix notation (such as x++).
- Binary operators. The binary operators take two operands and all use infix notation (such as x + y).
- Ternary operator. Only one ternary operator, ?:, exists; it takes three operands and uses infix notation (c? x : y).

The order of evaluation of operators in an expression is determined by the precedence and associativity of the operators (§7.3.1).

Operands in an expression are evaluated from left to right. For example, in F(i) + G(i++) * H(i), method F is called using the old value of i, then method G is called with the old value of i, and, finally, method H is called with the new value of i. This is separate from and unrelated to operator precedence.

Certain operators can be overloaded. Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type (§7.3.2).

## 7.3.1 Operator precedence and associativity

When an expression contains multiple operators, the precedence of the operators controls the order in which the individual operators are evaluated. For example, the expression x + y * z is evaluated as x + (y * z) because the * operator has higher precedence than the binary + operator. The precedence of an operator is established by the definition of its associated grammar production. For example, an additive-expression consists of a sequence of multiplicative-expressions separated by + or - operators, thus giving the + and - operators lower precedence than the *, /, and % operators.

The following table summarizes all operators in order of precedence from highest to lowest:

| Section | Category | Operators |
|---|---|---|
| 7.6 | Primary | x.y f(x) a[x] x++ x-- new typeof default checked unchecked delegate |
| 7.7 | Unary | + - ! ~ ++x --x (T)x |
| 7.8 | Multiplicative | * / % |
| 7.8 | Additive | + - |
| 7.9 | Shift | << >> |
| 7.10 | Relational and type testing | < > <= >= is as |
| 7.10 | Equality | == != |
| 7.11 | Logical AND | & |
| 7.11 | Logical XOR | ^ |
| 7.11 | Logical OR | | |
| 7.12 | Conditional AND | && |
| 7.12 | Conditional OR | || |
| 7.13 | Null coalescing | ?? |
| 7.14 | Conditional | ?: |
| 7.17, 7.15 | Assignment and lambda expression | = *= /= %= += -= <<= >>= &= ^= |= => |

When an operand occurs between two operators with the same precedence, the associativity of the operators controls the order in which the operations are performed:

- Except for the assignment operators, all binary operators are left-associative, meaning that operations are performed from left to right. For example, x + y + z is evaluated as (x + y) + z.
- The assignment operators and the conditional operator (?:) are right-associative, meaning that operations are performed from right to left. For example, x = y = z is evaluated as x = (y = z).

Precedence and associativity can be controlled using parentheses. For example, x + y * z first multiplies y by z and then adds the result to x, but (x + y) * z first adds x and y and then multiplies the result by z.

## 7.3.2 Operator overloading

All unary and binary operators have predefined implementations that are automatically available in any expression. In addition to the predefined implementations, user-defined implementations can be introduced by including operator declarations in classes and structs (§10.10). User-defined operator implementations always take precedence over predefined operator implementations: Only when no applicable user-defined operator implementations exist will the predefined operator implementations be considered, as described in §7.3.3 and §7.3.4.

The overloadable unary operators are:
- !
- ~
- ++
- --
- true
- false

Although true and false are not used explicitly in expressions (and therefore are not included in the precedence table in §7.3.1), they are considered operators because they are invoked in several expressions
