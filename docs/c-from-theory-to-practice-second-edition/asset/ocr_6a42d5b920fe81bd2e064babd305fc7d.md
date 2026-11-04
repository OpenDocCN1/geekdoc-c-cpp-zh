the bit operators: & , ^ , | , <<, >>, as we'll describe later in this chapter. For example, consider the following program:

```
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
```

The statement a += 6; is equivalent to: a = a+6 = 4+6 = 10.

The next statement a *= b+3; is equivalent to: a = a*(b+3) = 10*(2+3) = 50. Notice that the compiler encloses the expression b+3 in parentheses rather than a = a*b+3.

The statement a -= b+8; is equivalent to: a = a-(b+8) = 50-(2+8) = 40.

The statement a /= b; is equivalent to: a = a/b = 40/2 = 20.

Finally, the statement a %= b+1; is equivalent to: a = a%(b+1) = 20%(2+1) = 2. Therefore, the program outputs: Num = 2.

When the expression is a long one, the compound operator can make the code easier to read and safer to write as well. For example, it is more convenient and safer to write:

```
```
publisher[1].book[j].prc += 10;
```
```

rather than the two long expressions. Yes, it is more convenient, but why is it safer? Because it is too easy to make a typing error and write:

```
```
publisher[1].book[j].prc = publisher[i].book[1].prc + 10;
```
```

and use i instead of j, in the right expression. As you'll learn in Chapter 7, a crash might happen because of that error!

![](bbox=[0.1, 0.78, 0.15, 0.84])

> When using the compound assignment operators, be careful first to write the op operator and then the =. If you switch the characters, you most likely insert a bug.

For example, if you write a = - 3; the value of a becomes -3. In a later chapter, there is an exercise that contains such an oversight. Watch out!

# Logical Operators

The logical operators !, &&, and || are used to form logical expressions. The ! operator is unary, while && and || are both binary. The logical operators produce either 0 or 1, just like