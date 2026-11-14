
In general, unary operators have higher priority than binary. On the rare occasions that both postfix and prefix unary notations have been applied, prefix notations are prioritized over postfix notations.

Among the binary operators, we have the same behavior that we know from math: multiplication and division precede addition and subtraction and the operations are left associative, i.e.:

```
x - y + z
```

is always interpreted as

```
(x - y) + z
```

Something really important to remember: the order of evaluation of the arguments is not defined. For instance:

```
int i = 3, j = 7, k;
k = f(++i) + g(++i) + j;
```

In this example, associativity guarantees that the first addition is performed before the second. But whether the expression f(++i) or g(++i) is computed first depends on the compiler implementation. Thus, k might be either f(4) + g(5) + 7 or f(5) + g(4) + 7. Furthermore, we cannot assume that the result is the same on a different platform. In general, it is dangerous to modify values within expressions. It works under some conditions, but we always have to test it and pay enormous attention to it. Altogether, our time is better spent by typing some extra letters and doing the modifications separately. More about this topic in Section 1.3.12.

```
=> c++03/num_1.cpp
```

With these operators, we can write our first (complete) numeric program:

```
#include <iostream>

int main ()
{
    const float r1= 3.5, r2 = 7.3, pi = 3.14159;

    float area1 = pi * r1*r1;
    std::cout << "A circle of radius " << r1 << " has area "
              << area1 << "." << std::endl;

    std::cout << "The average of " << r1 << " and " << r2 << " is "
              << (r1 + r2) / 2 << "." << std::endl;
}
```

When the arguments of a binary operation have different types, one or both arguments are automatically converted (coerced) to a common type according to the rules in Section C.3.

The conversion may lead to a loss of precision. Floating-point numbers are preferred over integer numbers, and evidently the conversion of a 64-bit long to a 32-bit float yields an accuracy loss; even a 32-bit int cannot always be represented correctly as a 32-bit float since some bits are needed for the exponent. There were also cases where the target variable could hold the correct result but the accuracy was already lost in the intermediate calculations. To illustrate this conversion behavior, let us look at the following example:

```cpp
long l = 1234567890123;
long l2 = l + 1.0f - 1.0; // imprecise
long l3 = l + (1.0f - 1.0); // correct
```

This leads on the author's platform to

```
l2 = 1234567954431
l3 = 1234567890123
```

In the case of l2 we lose accuracy due to the intermediate conversions, whereas l3 was computed correctly. This is admittedly an artificial example, but you should be aware of the risk of imprecise intermediate results.

The issue of inaccuracy will fortunately not bother us in the next section.

## 1.3.2 Boolean Operators

Boolean operators are logical and relational operators. Both return bool values as the name suggests. These operators and their meaning are listed in Table 1-3, grouped by precedence.

Binary relational and logical operators are preceded by all arithmetic operators. This means that an expression like 4 >> 1 + 7 is evaluated as if it were written 4 >> (1 + 7). Conversely, the unary operator ! for logic negation is prioritized over all binary operators. In old (or old-fashioned) code, you might see logical operations performed on int values. Please refrain from this: it is less readable and subject to unexpected behavior.

> **Advice**
> Always use bool for logical expressions.

Table 1-3: Boolean Operators

| Operation | Expression |
| :--- | :--- |
| Not | !b |
| Greater than | x > y |
| Greater than or equal to | x >= y |
| Less than | x < y |
| Less than or equal to | x <= y |
| Equal to | x == y |
| Not equal to | x != y |
| Logical AND | b && c |
| Logical OR | b || c |

Please note that comparisons cannot be chained like this:

bool in_bound = min <= x <= y <= max; // Error

Instead we need the more verbose logical reduction:

bool in_bound = min <= x && x <= y && y <= max;

In the following section, we will see quite similar operators.

## 1.3.3 Bitwise Operators

These operators allow us to test or manipulate single bits of integral types. They are important for system programming but less so for modern application development. Table 1-4 lists all operators by precedence.

The operation x << y shifts the bits of x to the left by y positions. Conversely, x >> y moves x's bits y times to the right. In most cases, 0s are moved in except for negative signed values in a right shift where it is implementation-defined. The bitwise AND can be used to test a specific bit of a value. Bitwise inclusive OR can set a bit and exclusive OR flip it. These operations are more important in system programming than scientific applications. As algorithmic entertainment, we will use them in §3.6.1.

## 1.3.4 Assignment

The value of an object (modifiable lvalue) can be set by an assignment:

```
object = expr;
```

When the types do not match, expr is converted to the type of object if possible. The assignment is right-associative so that a value can be successively assigned to multiple objects in one expression:

```
o3 = o2 = o1 = expr;
```

Speaking of assignments, the author will now explain why he left-justifies the symbol. Most binary operators are symmetric in the sense that both arguments are values. In contrast, assignments have a modifiable variable on the left-hand side. While other languages use asymmetric symbols (e.g., := in Pascal), the author uses an asymmetric spacing in C++.

Table 1-4: Bitwise Operators

| Operation | Expression |
|---|---|
| One's complement | ~x |
| Left shift | x << y |
| Right shift | x >> y |
| Bitwise AND | x & y |
| Bitwise exclusive OR | x ^ y |
| Bitwise inclusive OR | x | y |

The compound assignment operators apply an arithmetic or bitwise operation to the object on the left side with the argument on the right side; for instance, the following two operations are equivalent:

```
a += b; // corresponds to
a = a + b;
```

All assignment operators have a lower precedence than every arithmetic or bitwise operation so the right-hand side expression is always evaluated before the compound assignment:

```
a *= b + c; // corresponds to
a = a * (b + c);
```

The assignment operators are listed in Table 1-5. They are all right-associative and of the same priority.

| Operation | Expression |
|---|---|
| Simple assignment | x = y |
| Multiply and assign | x *= y |
| Divide and assign | x /= y |
| Modulo and assign | x %= y |
| Add and assign | x += y |
| Subtract and assign | x -= y |
| Shift left and assign | x <<= y |
| Shift right and assign | x >>= y |
| AND and assign | x &= y |
| Inclusive OR and assign | x |= y |
| Exclusive OR and assign | x ^= y |

## 1.3.5 Program Flow

There are three operators to control the program flow. First, a function call in C++ is handled like an operator. For a detailed description of functions and their calls, see Section 1.5.

The conditional operator c ? x : y evaluates the condition c, and when it is true the expression has the value of x, otherwise y. It can be used as an alternative to branches with if, especially in places where only an expression is allowed and not a statement; see Section 1.4.3.1.

A very special operator in C++ is the Comma Operator that provides a sequential evaluation. The meaning is simply evaluating first the sub-expression to the left of the comma and then that to the right of it. The value of the whole expression is that of the right sub-expression:

```
3 + 4, 7 * 9.3
```

The result of the expression is 65.1 and the computation of the first sub-expression is entirely irrelevant. The sub-expressions can contain the comma operator as well so that arbitrarily long sequences can be defined. With the help of the comma operator, one can
