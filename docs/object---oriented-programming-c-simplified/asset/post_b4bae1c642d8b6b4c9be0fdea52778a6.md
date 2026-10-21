
```cpp
cout << "Returned value in res= " << res << endl;
}
```

**OUTPUT:**

```
Returned value in res= 0
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_75_0.png)

**Figure 3.8.** *Output screen of program.*

**EXPLANATION:** In the expression, the condition before `&&` is false and after `&&` it is true, so the overall value of the expression is false, so a `0` is assigned to `res`.

## Logical OR (||)

The operator works with two operands which may be any expression, variable, constant or function. It checks whether any of its operands returns a true value or not. If any of them returns a true value, it returns a true value, i.e., a decimal 1. If both of its operands are false, a false value is returned, i.e., a decimal 0.

```cpp
/*PROG 3.9 DEMO OF LOGICAL OR OPERATOR (||)*/

#include <iostream.h>
void main()
{
    int res, a = 100, b = 120;
    res = (a >= 100 || b < 0);
    cout << "Returned value in res= " << res << endl;
}
```

**OUTPUT:**

```
Returned value in res= 1
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_75_1.png)

**Figure 3.9.** *Output screen of program.*

**EXPLANATION:** The `||` is called OR operator. On both sides of this operator condition is specified. If any of the conditions is true, the returned value is true, that is 1, else 0. In the above program, the first condition in the expression is true but the second is false, so `res` contains 1 as the result.

## Logical NOT (!)

The operator converts a true value into false and vice-versa. Again the operand may be any expression, constant, variable or function.

```cpp
/*PROG 3.10 DEMO OF LOGICAL OPERATOR !(NOT) VER 1*/

#include <iostream.h>
void main()
{
    int res, a = 1;
    res = !a;
    cout << "Returned value in res= " << res << endl;
}
```

**OUTPUT:**

```
Returned value in res= 0
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_76_0.png)

**Figure 3.10.** *Output screen of program.*

**EXPLANATION:** The `!` is called NOT or negation operator. It is a unary operator, meaning only one operand is required by it. If the operand's value is non-zero, it is converted into a false value, that is 0, and vice-versa. Similarly, if a true condition is specified, it will be turned into false and vice-versa. Try changing the value of `a` to zero, and the returned value in `res` will be 1.

```cpp
/*PROG 3.11 DEMO OF LOGICAL OPERATOR (NOT ! OPERATOR) VER 2*/

#include <iostream.h>
void main()
{
    int res;
    res = !(10 > 5 && -4 <= 1);
    cout << "returned value in res  := " << res << endl;
}
```

**OUTPUT:**

```
returned value in res  := 0
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_77_0.png)

**Figure 3.11.** *Output screen of program.*

**EXPLANATION:** Both conditions in the `&&` operator are true, so the whole inner expression is true; after negation, the returned value will be 0.

## 4. Assignment Operator

The `=` operator is called assignment operator. We have seen several instances of this operator in many of the earlier programs. One more use of this operator is the shortening of following types of expressions:

```
x = x + 1, y = y * (x - 5), a = a / 10, t = t % 10;
```

In all the above expressions, the variable on both sides of the `=` operator is the same, so we can change the above expressions into shorter form as follows:

```
x = x + 1        =>   x += 1
y = y * (x - 5)  =>   y *= (x - 5)
a = a / 10       =>   a /= 10
t = t % 10       =>   t %= 10
```

This form `op=`, where operator may be any operator, is called compound operator or shorthand assignment operator.

## 5. Increment Operator (++) and Decrement Operator (--)

The operator `++` is known as increment operator and the operator `--` is known as decrement operator. Both are unary operators. The `++` increments the value of its operand by 1 and `--` decrements the value of its operand by 1. For example, `++x` becomes 11 and `--x` becomes 9 (assume `x = 10` prior to the operation).

See the program given below for more explanation:

```cpp
/*PROG 3.12 DEMO OF ++ OPERATOR VER 1*/

#include <iostream.h>
void main()
{
    int x;
    x = 20;
    cout << "Before increment x = " << x << endl;
    x++;
    cout << "After increment x = " << x << endl;
}
```

**OUTPUT:**

```
Before increment x = 20
After increment x = 21
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_78_0.png)

**Figure 3.12.** *Output screen of program.*

**EXPLANATION:** The `++` operator is called increment operator. It is a unary operator, that is, it requires only one operand to operate, which increments the value of operand by 1, i.e., `x++` is equivalent to `x = x + 1`. If `++` is written before the operand, i.e., `++x`, it is known as pre-increment; and if `++` is written after the operand, i.e., `x++`, it is known as post-increment. In the above program we have used the post-increment operator. Had we used pre-increment, the output would be the same. For distinction between the two, check out the next two programs.

```cpp
/*PROG 3.13 DEMO OF ++ OPERATOR VER 2*/

#include <iostream.h>
void main()
{
    int x, y;
    x = 20;
    y = x++;
    cout << "x=" << x << "\t" << "y=" << y << endl;
}
```

**OUTPUT:**

```
x = 21 y = 20
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_78_1.png)

**Figure 3.13.** *Output screen of program.*

**EXPLANATION:** In the above program we have used the post-increment operator with `x` and we are assigning the value to `y`. Due to post-increment, first `x` will be assigned to `y` and `x` will be incremented by 1, that is `y = x++` is equivalent to the following statements:

```
y = x;
x = x + 1;
```

If we write `x = 20; y = ++x;`, then due to pre-increment first `x` will be incremented by 1 and the same incremented value will be assigned to `y`. `y = ++x` is equivalent to the following two statements:

![](img/ad5299318df8d4d7c6df5eaa86590ea3_79_0.png)

> Note: There is only `++` operator which is used to increment the value of the operand by one. There is no such operator as `+++` or `++++` which increments the value by 2 or 3.

```cpp
/*PROG 3.14 DEMO OF ++ OPERATOR VER 3*/

#include <iostream.h>
void main()
{
    int x, y;
    x = 10;
    y = ++x;
    cout << "x=" << x << "\t" << "y=" << y << endl;
    --x;
    cout << "x=" << x << endl;
    y--;
    cout << "y=" << y << endl;
    x = y++;
    cout << "x=" << x << "\t" << "y=" << y << endl;
    y = --x;
    cout << "x=" << x << "\t" << "y=" << y << endl;
    x = y++;
    cout << "x=" << x << "\t" << "y=" << y << endl;
}
```

**OUTPUT:**

```
x=11 y=11
x=10
y=10
x=10 y=11
x=9 y=9
x=9 y=10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_80_0.png)

**Figure 3.14.** *Output screen of program.*

**EXPLANATION:** For explanation observe the following table:

| Statement | Value of x | Value of y |
|---|---:|---:|
| `y = ++x` | 11 | 11 |
| `--x` | 10 | 11 |
| `y--` | 10 | 10 |
| `x = y++` | 10 | 11 |
| `y = --x` | 09 | 09 |
| `x = y++` | 09 | 10 |

```cpp
/*PROG 3.15 DEMO OF ++ OPERATOR VER 4*/

#include <iostream.h>
void main()
{
    int x;
    x = 10;
    cout << --x << endl << ++x << endl << x << endl << x++ << endl
         << x-- << endl;
}
```

**OUTPUT:**

```
10
11
10
9
10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_81_0.png)

**Figure 3.15.** *Output screen of program.*

**EXPLANATION:** The output will be determined from right of `cout` statement:

| Statement | Value of x | Explanation |
|---|---:|---|
| `x--` | 10 | Value of x will be printed then decremented |
| `x++` | 09 | Value of x will be printed then incremented |
| `x` | 10 | Value of x will be printed |
| `++x` | 11 | Value of x will be incremented then printed |
| `--x` | 10 | Value of x will be decremented then printed |

So the output is 10 11 10 9 10.

## 6. Bitwise Operators

They are called so because they operate on bits. They can be used for the manipulation of bits. All these operators are extensively used when interfacing with the hardware and for setting of bits in registers of the device. C provides a total of 6 types of bitwise operators. They are as follows:

**Table 3.6: Bitwise Operators**

| S.No. | Operator | Meaning/Used for |
|---|---|---|
| 1. | `&` | Bitwise AND |
| 2. | \| | Bitwise OR |
| 3. | `^` | Bitwise XOR |
| 4. | `~` | One's complement |
| 5. | `>>` | Right shift |
| 6. | `<<` | Left shift |

For all the following programs we consider only first 4 bits of the number for explanation purpose. So range of possible numbers is -8 to 7 in case of signed numbers (`-2^3` to `2^3 - 1`) and (0 to `2^4 - 1`) in case of unsigned numbers. In case you assume 8 bits for the numbers then use full 8 bits for the number even if it can be using 4 bits, for example 10 can be written using 4 bits as 1010 and using 8 bits as 00001010.
