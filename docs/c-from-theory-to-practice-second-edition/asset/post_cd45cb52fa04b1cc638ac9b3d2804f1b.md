
## 4 Operators

Now that you've been introduced to the concepts of C data types, variables, and constants, it is time to learn how to manipulate their values. C provides a rich set of operators that are used to form expressions and perform operations on them. In this chapter, we'll present some of C's most important operators. We'll introduce the rest gradually over the next several chapters, and you'll see how to apply them when writing more complex programs.

### The `=` Assignment Operator

The `=` operator is used to assign a value to a variable. For example, the statement `a = 10;` assigns the value 10 to the variable `a`, while the statement `a = k;` assigns the value of the variable `k` to `a`. When used in a chained assignment, the assigned value is stored in all variables in the chain. For example:

```c
int a, b, c;
a = b = c = 10;
```

the values of `a`, `b`, and `c` become 10. In particular, because the `=` operator is right associative, the rightmost expression is evaluated first and evaluation proceeds from right to left. Therefore, first `c` becomes 10, then `c` is assigned to `b`, and, finally, `b` is assigned to `a`.

An assignment such as `a = 10;` produces a result, which is the value of the left operand (i.e., `a`) after the assignment. For example:

```c
a = 10;
c = a + (b = a+10);
```

The result of the assignment `b = a+10` is 20, so `c` becomes 30. Use separate assignments rather than mixing them together; it is much easier to control the code.

The right operand (*rvalue*) is an expression that has a value, such as a constant or a variable. The left operand must be an *lvalue*. An *lvalue* refers to an object stored in memory, such as a variable. It is not allowed to use a constant or the result of a computation. For example:

```c
10 = a; /* Illegal. */
a+b = 20; /* Illegal. */
```

The compiler will produce an error message similar to "*error '=': left operand must be lvalue.*" Also, the *lvalue* must be modifiable. For example, we'll see in Chapter 8 that an array variable is not a modifiable *lvalue*.

### The `++` and `--` Operators

If the `++` operator is used in postfix form, the increment is performed after the current value of the variable is used in an expression. For example:

```c
int a = 4, b;
b = a++;
```

The current value of a is first stored into b, and then a is incremented. Therefore, a becomes 5, and b becomes 4.

If used in the prefix form, the variable's value is first incremented, and the new value is used in the evaluation of the expression. For example:

```c
int a = 4, b;
b = ++a;
```

a is first incremented, and then that value is stored into b. Therefore, both variables become 5.

In a similar way, the `--` decrement operator is used to decrement the value of a variable by 1. For example:

```c
int a = 4;
a--; /* Equivalent to a = a-1; */
--a; /* Equivalent to a = a-1; */
```

The value of a is decremented twice and becomes 2. When the `--` operator is used in an expression, it behaves like the `++` operator. For example:

```c
#include <stdio.h>
int main(void)
{
    int a = 4, b;

    b = a--;
    printf("a = %d b = %d\n", a, b);

    b = --a;
    printf("a = %d b = %d\n", a, b);
    return 0;
}
```

With the statement `b = a--;` the current value of a is first stored into b and then its value is decremented. Therefore, the first `printf()` displays: a = 3  b = 4. Next, with the statement `b = --a;` the value of a is first decremented and then its value is stored into b. Therefore, the second `printf()` displays: a = 2  b = 2. Let's see another example:

```c
#include <stdio.h>
int main(void)
{
    double a = 3.45;

    printf("%.2f\n", a++);
    printf("%.2f\n", ++a);
    return 0;
}
```

The program first displays 3.45, and then the value of a is incremented. Next, a is first incremented, so the program displays 5.45. Let's see another example where the `++` and `--` operators are combined in the same expression.

```c
#include <stdio.h>
int main(void)
{
    int a = 1, b = 2, c = 3;
    printf("%d\n", (++a)-(b--)+( --c));
    return 0;
}
```

The operation `++a` first increases the current value of a, and then its new value is used. With the operation `b--` the current value of b is first used and then its value is decremented. Finally, with the operation `--c` the value of c is first decremented and then used in the expression. Therefore, the result of the expression is 2-2+2 = 2 and the values of a, b, and c become 2, 1, and 2, respectively.

> Don't apply the `++` and `--` operators in the same variable and create expressions whose values depend on the evaluation order.

For example, the result of: `a * a++;` is implementation dependent. It depends on the compiler whether a is first incremented and then multiplied, or not.

### Relational Operators

The relational operators `>`, `>=`, `<`, `<=`, `!=`, and `==` are used to compare two operands and determine their relationship. As we'll see in next chapters, the relational operators are mostly used in if statements and iteration loops. Consider the following statements:

- `if(a > 10)` the `>` operator is used to check whether `a` is greater than 10.
- `if(a >= 10)` the `>=` operator is used to check whether `a` is greater than or equal to 10.
- `if(a < 10)` the `<` operator is used to check whether `a` is less than 10.
- `if(a <= 10)` the `<=` operator is used to check whether `a` is less than or equal to 10.
- `if(a != 10)` the `!=` operator is used to check whether `a` is not equal to 10.
- `if(a == 10)` the `==` operator is used to check whether `a` is equal to 10.

> An expression is considered true when it has a nonzero value; otherwise, it is considered false.

When used in an expression, the value of the expression is either 0 or 1. For example, the value of `(a > 10)` is 1 only if a is greater than 10; otherwise, it is 0. How about this one: `-5 < a < 2`? Does the value of that expression depend on the value of a?

Because the `<` operator is left associative (see Appendix A), first the value of `-5 < a` is evaluated, which is either 0 or 1, and then that value is compared with 2, which is always true. Therefore, the value of the expression is 1, no matter what the value of a is. As we'll see next, to test whether a value is within a given set, we use the `&&` operator.

> Don't confuse the `==` operator with the `=` operator. The `==` operator is used to check whether two expressions have the same value, while the `=` operator is used to assign a value.

For example, the value of the expression `a == 10` is 1, only if `a` is equal to 10, otherwise, it is 0. On the other hand, the expression `a = 10` assigns the value 10 into `a`. We'll see more examples like this when presenting the `if` statement in the next chapter.

### Exercises

**C.4.1** What is the output of the following program?

```c
#include <stdio.h>
int main(void)
{
    int a = 3, b = 5, c;

    a = (a > 3) + (b <= 5);
    b = (a == 3) + ((b-2) >= 3);
    c = (b != 1);
    printf("%d %d %d\n", a, b, c);
    return 0;
}
```

**Answer:** Since `a` is 3, the value of the expression `(a > 3)` is 0. The value of `(b <= 5)` is 1 because `b` is 5. Therefore, `a = 0+1 = 1`. Since `a` is 1, the value of `(a == 3)` is 0. The value of `((b-2) >= 3)` is 1 because `b-2 = 5-2 = 3`. Therefore, `b = 0+1 = 1`. Since `b` is 1, the value of `(b != 1)` is 0. Therefore, `c` becomes 0. As a result, the program displays: `1 1 0`.

### Compound Assignment Operators

The compound assignment operators are used to shorten statements using the form: `exp1 op= exp2;` This statement is equivalent to `exp1 = exp1 op (exp2)`. Notice that the compiler encloses the expression `exp2` in parentheses for reasons of priority. Typically, the `op` operator is one of the arithmetic operators: `+`, `-`, `*`, `/`, `%`, although it can also be any of the bit operators: `&`, `^`, `|`, `<<`, `>>`, as we'll describe later in this chapter. For example, consider the following program:

```c
#include <stdio.h>
int main(void)
{
    int a = 4, b = 2;
    a += 6;
    a *= b+3;
    a -= b+8;
    a /= b;
    a %= b+1;
    printf("Num = %d\n", a);
    return 0;
}
```

The statement `a += 6;` is equivalent to: `a = a+6 = 4+6 = 10`.

The next statement `a *= b+3;` is equivalent to: `a = a*(b+3) = 10*(2+3) = 50`. Notice that the compiler encloses the expression `b+3` in parentheses rather than `a = a*b+3`.

The statement `a -= b+8;` is equivalent to: `a = a-(b+8) = 50-(2+8) = 40`.

The statement `a /= b;` is equivalent to: `a = a/b = 40/2 = 20`.

Finally, the statement `a %= b+1;` is equivalent to: `a = a%(b+1) = 20%(2+1) = 2`. Therefore, the program outputs: Num = 2.

When the expression is a long one, the compound operator can make the code easier to read and safer to write as well. For example, it is more convenient and safer to write:

```c
publisher[1].book[j].prc += 10;
```

rather than the two long expressions. Yes, it is more convenient, but why is it safer? Because it is too easy to make a typing error and write:

```c
publisher[1].book[j].prc = publisher[1].book[i].prc + 10;
```

and use i instead of j, in the right expression. As you'll learn in Chapter 7, a crash might happen because of that error!

![](img/b8da5dcf9ba7f1fad5213c453d095246_71_0.png)

> When using the compound assignment operators, be careful first to write the op operator and then the `=`. If you switch the characters, you most likely insert a bug.

For example, if you write `a =- 3;` the value of a becomes -3. In a later chapter, there is an exercise that contains such an oversight. Watch out!

### Logical Operators

The logical operators `!`, `&&`, and `||` are used to form logical expressions. The `!` operator is unary, while `&&` and `||` are both binary. The logical operators produce either 0 or 1, just like
