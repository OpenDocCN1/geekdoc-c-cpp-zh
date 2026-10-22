
隐式转换可能会丢失信息，符号可能会丢失（当有符号类型被隐式转换为无符号类型时），也可能发生溢出（当 `long long` 被隐式转换为 `float` 时）。

## 类型隐式转换示例：

```c
// An example of implicit conversion
#include<stdio.h>
int main()
{
    int x = 10;   // integer x
    char y = 'a'; // character c

    // y implicitly converted to int. ASCII
    // value of 'a' is 97
    x = x + y;

    // x is implicitly converted to float
    float z = x + 1.0;

    printf("x = %d, z = %f", x, z);
    return 0;
}
```

1. **输出：**

   `x = 107, z = 108.000000`

2. **显式类型转换**——这个过程也称为类型转换（type casting），由用户定义。这里，用户可以对结果进行类型转换，使其成为特定的数据类型。

C 语言中的语法如下：

```c
(type) expression
```

这里的 `type` 表示最终结果被转换成的数据类型。

```c
// C program to demonstrate explicit type casting
#include<stdio.h>

int main()
{
    double x = 1.2;

    // Explicit conversion from double to int
    int sum = (int)x + 1;

    printf("sum = %d", sum);

    return 0;
}
```

输出：

```text
sum = 2
```

## C 语言中的运算符

运算符是任何编程语言的基础。因此，不使用运算符，C 语言的功能就不完整。运算符允许我们对操作数执行不同类型的操作。在 C 语言中，运算符可以分为以下几类：

- **算术运算符**（+, -, *, /, %，后置递增、前置递增、后置递减、前置递减）
- **关系运算符**（==, !=, >, <, >=, <=）
- **逻辑运算符**（&&, || 和 !）
- **位运算符**（&, |, ^, ~, >> 和 <<）
- **赋值运算符**（=, +=, -=, *= 等）
- **其他运算符**（条件、逗号、sizeof、取地址、间接引用）

**算术运算符：**这些运算符用于对操作数执行算术/数学运算。属于此类的二元运算符有：

- **加法：**`+` 运算符将两个操作数相加。例如，x+y。
- **减法：**`-` 运算符将两个操作数相减。例如，x-y。
- **乘法：**`*` 运算符将两个操作数相乘。例如，x*y。
- **除法：**`/` 运算符将第一个操作数除以第二个操作数。例如，x/y。
- **取模：**`%` 运算符返回第一个操作数除以第二个操作数后的余数。例如，x%y。

```c
// C program to demonstrate working of binary arithmetic operators
#include<stdio.h>

int main()
{
    int a = 10, b = 4, res;

    //printing a and b
    printf("a is %d and b is %d\n", a, b);

    res = a+b; //addition
    printf("a+b is %d\n", res);

    res = a-b; //subtraction
    printf("a-b is %d\n", res);

    res = a*b; //multiplication
    printf("a*b is %d\n", res);

    res = a/b; //division
    printf("a/b is %d\n", res);

    res = a%b; //modulus
    printf("a%%b is %d\n", res);

    return 0;
}
```

**输出：**

```text
a is 10 and b is 4
a+b is 14
a-b is 6
a*b is 40
a/b is 2
a%b is 2
```

归属于一元算术运算符类别的是：

- **递增：**`++` 运算符用于将整数值增加 1。当它放在变量名之前（也称为前置递增运算符）时，该变量的值会立即增加。例如，**++x**。当它放在变量名之后（也称为后置递增运算符）时，该变量的值会暂时保留到当前语句执行完毕，并在执行下一条语句之前更新。例如，**x++**。
- **递减：**`--` 运算符用于将整数值减少 1。当它放在变量名之前（也称为前置递减运算符）时，该变量的值会立即减少。例如，**--x**。当它放在变量名之后（也称为后置递减运算符）时，该变量的值会暂时保留到当前语句执行完毕，并在执行下一条语句之前更新。例如，**x--**。

```c
// C program to demonstrate working of Unary arithmetic operators
#include<stdio.h>

int main()
{
    int a = 10, b = 4, res;

    // post-increment example:
    // res is assigned 10 only, a is not updated yet
    res = a++;
    printf("a is %d and res is %d\n", a, res); //a becomes 11 now

    // post-decrement example:
    // res is assigned 11 only, a is not updated yet
    res = a--;
    printf("a is %d and res is %d\n", a, res); //a becomes 10 now

    // pre-increment example:
    // res is assigned 11 now since a is updated here itself
    res = ++a;
    // a and res have same values = 11
    printf("a is %d and res is %d\n", a, res);

    // pre-decrement example:
    // res is assigned 10 only since a is updated here itself
    res = --a;
    // a and res have same values = 10
    printf("a is %d and res is %d\n",a,res);

    return 0;
}
```

**输出：**

```text
a is 11 and res is 10
a is 10 and res is 11
a is 11 and res is 11
a is 10 and res is 10
```

### 关系运算符

关系运算符用于比较两个值。让我们逐一介绍：

- `==` 运算符检查两个给定操作数是否相等。如果相等，则返回真；否则返回假。例如，**5==5** 将返回真。
- `!=` 运算符检查两个给定操作数是否相等。如果不相等，则返回真；否则返回假。它是 `==` 运算符在布尔意义上的精确补运算。例如，**5!=5** 将返回假。
- `>` 运算符检查第一个操作数是否大于第二个操作数。如果是，则返回真；否则返回假。例如，**6>5** 将返回真。
- `<` 运算符检查第一个操作数是否小于第二个操作数。如果是，则返回真；否则返回假。例如，**6<5** 将返回假。
- `>=` 运算符检查第一个操作数是否大于或等于第二个操作数。如果是，则返回真；否则返回假。例如，**5>=5** 将返回真。
- `<=` 运算符检查第一个操作数是否小于或等于第二个操作数。如果是，则返回真；否则返回假。例如，**5<=5** 也将返回真。

```c
// C program to demonstrate working of relational operators
#include <stdio.h>

int main()
{
    int a=10, b=4;

    // relational operators
    // greater than example
    if (a > b)
        printf("a is greater than b\n");
    else printf("a is less than or equal to b\n");

    // greater than equal to
    if (a >= b)
        printf("a is greater than or equal to b\n");
    else printf("a is lesser than b\n");

    // less than example
    if (a < b)
        printf("a is less than b\n");
    else printf("a is greater than or equal to b\n");

    // lesser than equal to
    if (a <= b)
        printf("a is lesser than or equal to b\n");
    else printf("a is greater than b\n");

    // equal to
    if (a == b)
        printf("a is equal to b\n");
    else printf("a and b are not equal\n");

    // not equal to
    if (a != b)
        printf("a is not equal to b\n");
    else printf("a is equal to b\n");

    return 0;
}
```

**输出：**

```text
a is greater than b
a is greater than or equal to b
a is greater than or equal to b
a is greater than b
a and b are not equal
a is not equal to b
```

### 逻辑运算符

逻辑运算符用于组合两个或多个条件/约束，或对当前所考虑条件的求值结果进行取反。具体描述如下：

- **逻辑与：**当所考虑的两个条件都满足时，`&&` 运算符返回真；否则返回假。例如，当 a 和 b 都为真（即非零）时，**a && b** 返回真。
- **逻辑或：**当所考虑的条件中有一个（或两个）满足时，`||` 运算符返回真；否则返回假。例如，如果 a 或 b 中有一个为真（即非零），则 **a || b** 返回真。当然，当 a 和 b 都为真时，它也返回真。
- **逻辑非：**如果所考虑的条件不满足，`!` 运算符返回真；否则返回假。例如，如果 a 为假，即当 a=0 时，**!a** 返回真。

```c
// C program to demonstrate working of logical operators
#include <stdio.h>

int main()
{
    int a=10, b=4, c = 10, d = 20;

    // logical operators

    // logical AND example
    if (a>b && c==d)
        printf("a is greater than b AND c is equal to d\n");
    else printf("AND condition not satisfied\n");

    // logical OR example
    if (a>b || c==d)
        printf("a is greater than b OR c is equal to d\n");
}
```

