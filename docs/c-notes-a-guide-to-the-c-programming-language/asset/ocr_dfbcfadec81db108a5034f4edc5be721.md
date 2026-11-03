plementation to rearrange expressions with like commutative operators:

```
a + b + c is (a + c) + b or (a + b) + c. etc.
```

The arithmetic types (integer and floating) fall into a natural hierarchy from char to double, which is called the widening hierarchy:

```
char → short → int → unsigned → long → float → double
```

which determines the type of value returned by many of the operators when the two operands have different arithmetic type. For example, in

```
(i + '0') - x  /* i is int, x float */
```

the char value '0' is widened to integer which then can be added to i; then this integer result is widened to floating so that the floating x can be subtracted to produce a final floating result. The language also has cast operators, which explicitly request such widenings, so the above is equivalent to

```
(float)(i + (int)'0') - x
```

The normal rule for binary arithmetic operators calls for widening the narrower operand to the wider one. The language reserves the right to perform arithmetic by widening operands more than necessary just to satisfy this rule. Thus, char and short operands are frequently widened to int, while float arithmetic often is performed in double. The distinction usually is not highly visible to the programmer.

When the type of a variable-name-expr is wider than the type of the expression assigned to it, the normal widening will occur; when it is narrower, the conversion is machine-dependent and prone to information-loss, so that narrowing assignments should be used sparingly.

C programs may contain conditional-exprs whose syntax is

```
conditional-expr =
logical-expr ? expr : expr
```