
| Operation | Expression |
|---|---|
| Pre-increment | ++x |
| Pre-decrement | --x |
| Unary plus | +x |
| Unary minus | -x |
| Multiplication | x * y |
| Division | x / y |
| Modulo | x % y |
| Addition | x + y |
| Subtraction | x - y |

The first kinds of operations are increment and decrement. These operations can be used to increase or decrease a number by 1. As they change the value of the number, they only make sense for variables and not for temporary results, for instance:

Click here to view code image

```
int i = 3;
i++; // i is now 4
const int j = 5;
j++; // Error: j is constant
(3 + 5)++; // Error: 3 + 5 is only a temporary
```

In short, the increment and decrement operations need something that is modifiable and addressable. The technical term for an addressable data item is lvalue (more formally expressed in Definition C–1 in Appendix C). In our code snippet above, this is true for i only. In contrast to it, j is constant and 3 + 5 is not addressable.

Both notations—prefix and postfix—have the effect on a variable that they add or subtract 1 from it. The value of an increment and decrement expression is different for prefix and postfix operators: the prefix operators return the modified value and postfix the old one, e.g.:

Click here to view code image

```
int i = 3, j = 3;
int k = ++i + 4; // i is 4, k is 8
int l= j++ + 4; // j is 4, l is 7
```

At the end, both `i` and `j` are 4. However in the calculation of `l`, the old value of `j` was used while the first addition used the already incremented value of `i`.

In general, it is better to refrain from using increment and decrement in mathematical expressions and to replace it with `j+1` and the like or to perform the in/decrement separately. It is easier for human readers to understand and for the compiler to optimize when mathematical expressions have no `Side Effects`. We will see quite soon why (§I.3.12).

The unary minus negates the value of a number:

Click here to view code image

```
int i= 3;
int j= -i; // j is -3
```

The unary plus has no arithmetic effect on standard types. For user types, we can define the behavior of both unary plus and minus. As shown in Table 1–2, these unary operators have the same priority as pre-increment and pre-decrement.

The operations `*` and `/` are naturally multiplication and division, and both are defined on all numeric types. When both arguments in a division are integers, the fractional part of the result is truncated (rounding toward zero). The operator `%` yields the remainder of the integer division. Thus, both arguments should have an integral type.

Last but not least, the operators `+` and `-` between two variables or expressions symbolize addition and subtraction.

The semantic details of the operations—how results are rounded or how overflow is handled—are not specified in the language. For performance reasons, C++ leaves this typically to the underlying hardware.

In general, unary operators have higher priority than binary. On the rare occasions that both postfix and prefix unary notations have been applied, postfix notations are prioritized over prefix notations.

Among the binary operators, we have the same behavior that we know from math: multiplication and division precede addition and subtraction and the operations are left associative, i.e.:

```
x - y + z
```

is always interpreted as

```
(x - y) + z
```

Something really important to remember: the order of evaluation of the arguments is not defined. For instance:

Click here to view code image

```
int i = 3, j = 7, k;
k = f(++i) + g(++i) + j;
```

In this example, associativity guarantees that the first addition is performed before the second. But whether the expression f(++i) or g(++i) is computed first depends on the compiler implementation. Thus, k might be either f(4) + g(5) + 7 or f(5) + g(4) + 7 (or even f(5) + g(5) + 7 when both increments are executed before the function call). Furthermore, we cannot assume that the result is the same on a different platform. In general, it is dangerous to modify values within expressions. It works under some conditions, but we always have to test it and pay enormous attention to it. Altogether, our time is better spent by typing some extra letters and doing the modifications separately. More about this topic in Section 1.3.12.

=> c++03/num_1.cpp

With these operators, we can write our first (complete) numeric program:

Click here to view code image

```
#include <iostream>

int main ()
{
    const float r1= 3.5, r2 = 7.3, pi = 3.14159;

    float areal = pi * r1*r1;
    std::cout << "A circle of radius " << r1 << " has area "
    << areal << "." << std::endl;

    std::cout << "The average of " << r1 << " and " << r2 << "
    is "
    << (r1 + r2) / 2 << "." << std::endl;
}
```

When the arguments of a binary operation have different types, one or both arguments are automatically converted (coerced) to a common type according to the rules in §C.3.

The conversion may lead to a loss of precision. Floating-point numbers are preferred over integer numbers, and evidently the conversion of a 64-bit `long` to a 32-bit `float` yields an accuracy loss; even a 32-bit `int` cannot always be represented correctly as a 32-bit `float` since some bits are needed for the exponent. There are also cases where the target variable could hold the correct result but the accuracy was already lost in the intermediate calculations. To illustrate this conversion behavior, let us look at the following example:

Click here to view code image

```
long l= 1234567890123;
long l2= 1 + 1.0f - 1.0; // imprecise
long l3= 1 + (1.0f - 1.0); // correct
```

This leads on the author's platform to

Click here to view code image

```
l2 = 1234567954431
l3 = 1234567890123
```

In the case of `l2` we lose accuracy due to the intermediate conversions, whereas `l3` was computed correctly. This is admittedly an artificial example, but you should be aware of the risk of imprecise intermediate results. Especially with large calculations the numerical algorithms must be carefully chosen to prevent the errors from building up. The issue of inaccuracy will fortunately not bother us in the next section.

## 1.3.2 Boolean Operators

Boolean operators are logical and relational operators. Both return `bool` values as the name suggests. These operators and their meaning are listed in Table 1-3, grouped by precedence.

Binary relational and logical operators are preceded by all arithmetic operators. This means that an expression like `4 >= 1 + 7` is evaluated as if it were written `4 >= (1 + 7)`. Conversely, the unary operator `!` for logic negation is prioritized over all binary operators.

### Table 1-3: Boolean Operators

| Operation | Expression |
| :--- | :--- |
| Not | !b |
| Three-way comparison (C++20) | x <=> y |
| Greater than | x > y |
| Greater than or equal to | x >= y |
| Less than | x < y |
| Less than or equal to | x <= y |
| Equal to | x == y |
| Not equal to | x != y |
| Logical AND | b && c |
| Logical OR | b || c |

The boolean operators also have keywords, like not, and, or, and xor. There are even keywords for assignments, like or_eq for |=. We usually don't use them for their paleolithic look but there is one exception: not can make expressions far more readable. When negating something that starts with "!" or "|", the exclamation point is easily overseen. A space already helps, but the keyword makes the negation even more visible:

Click here to view code image

```
big = !little;    // You knew before there's an !
big= not little;  // Much easier to spot, though
```

Although these keywords have been available from the beginning of standard C++, Visual Studio still doesn't support them unless you compile with /permissive- or /Za.

In old (or old-fashioned) code, you might see logical operations performed on int values. Please refrain from this: it is less readable and subject to unexpected behavior.

### Advice

Always use `bool` for logical expressions.

Please note that comparisons cannot be chained like this:

Click here to view code image

```
bool in_bound= min <= x <= y <= max;    // Syntax error
```

Instead we need the more verbose logical reduction:

Click here to view code image

```
bool in_bound= min <= x && x <= y && y <= max;
```

In the following section, we will see similar operators.

## 1.3.3 Bitwise Operators

These operators allow us to test or manipulate single bits of integral types. They are important for system programming but less so for modern application development. Table 1-4 lists these operators by precedence.

The operation `x << y` shifts the bits of `x` to the left by `y` positions. Conversely, `x >> y` moves `x`'s bits `y` times to the right. In most cases, 0s are moved (except for negative `signed` values) to the right where they are implementation defined.

6. Again we compress the double less-than and larger-than symbols to French guillemets for nicer printing.

### Table 1-4: Bitwise Operators

| Operation | Expression |
|---|---|
| One's complement | ~x |
| Left shift | x << y |
| Right shift | x >> y |
| Bitwise AND | x & y |
| Bitwise exclusive OR | x ^ y |
