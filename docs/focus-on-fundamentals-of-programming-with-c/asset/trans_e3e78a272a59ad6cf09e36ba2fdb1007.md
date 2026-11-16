

当然，你可能希望在程序中交换 foo1() 和 foo2() 的顺序，一切都会正常。但是，在包含几十个函数的大型程序中，可能不容易正确排列函数顺序。使用函数原型，我们永远不必担心函数的顺序。

使用函数原型的最后一个原因涉及构建大型程序和链接源代码。这将在以后讨论。

## 函数返回值

请注意，即使函数返回一个值，程序也不必使用它：

```c
while (...) {
    :
    getchar(); // get a character and do nothing with it
    c = getchar(); // get another character and assign to c
    :
}
```

## void 返回值和 void 参数列表

如果函数不返回任何值，其返回类型应指定为 void。void 说明符告知编译器函数不返回值。从某种意义上说，void 数据类型实际上定义了数据类型的缺失，声明为 void 类型的函数没有返回值，不能像有返回值一样在表达式中使用。

```c
void printHeader(void) {
    printf("Program Number 1\n");
    printf("by Richard Stegman\n");
    printf("Version 1.0, released 2/12/14\n");
}
```

如你所见，此函数不返回值。你可以用以下语句调用它：

```c
printHeader();
```

请注意，调用时必须包含 ( )。如果不包含，函数不会被调用，即使在许多系统上可以正确编译。

如果函数不接收任何参数（即，没有声明形参），则应在函数名后的括号内的参数列表中指定 void。以下是一个不接受任何值、生成并返回 0 到 255 之间随机数的函数：

```c
int getRandomNumber(void) {
    return (rand() % 255);
}
```

函数头：

```c
int getRandomNumber()
```

向程序的其余部分声明函数：

```c
getRandomNumber()
```

并指定该函数不接受任何参数，将返回 int 结果。

## 函数参数

传递给函数的值称为 *实参* 或 *实际参数*。出现在函数头中的参数称为 *形参* 或 *形式参数*。我们说实际参数被传递给形式参数。

在 C 中，函数参数始终按 *值传递*。每个参数都会被求值，其值在函数头中局部替代形式参数。因此，如果将参数传递给函数，该参数的存储值在调用环境中不会改变。例如：

```c
#include <stdio.h>

void foo(int num);

int main(void) {
    int num = 5;
    printf("%d\n", num);
    foo(num);
    printf("%d\n", num);
    return 0;
}

int foo(int num) {
    printf("%d\n", num);
    num = num + 1;
    printf("%d\n", num);
}
```

产生以下输出：

```
5
6
5
5
```

如果我们想按 *引用传递* 参数（即，在函数中更改参数的值，并使该新值反映回调用函数），则必须将参数的 *地址* 传递给函数，而不是参数本身。一旦函数可以访问用于存储实际参数的内存位置，它就可以修改其内容，从而修改实际参数。

例如：

```c
#include <stdio.h>

void foo(int *num);

int main(void) {
    int num = 5;

    printf("%d\n", num);
    foo(&num);
    printf("%d\n", num);

    return 0;
}

void foo(int *num) {
    printf("%d\n", *num);
    *num = *num + 1;
    printf("%d\n", *num);
}
```

产生以下输出：

```
5
5
6
6
```

请注意，实际参数的值已通过对 foo() 的调用而更改。

要按引用传递，我们必须先将实际参数的地址传递给函数。这是通过使用取地址运算符 (&) 实现的。当 & 放在变量前面时，它返回该变量的地址。

因此，在 main() 中的调用：

```c
foo(&num);
```

我们将 num 的地址传递给函数 foo()。

现在查看函数头中 foo() 的形式参数声明。出现在 num 前面的 * 表示传递给 foo() 的值实际上是内存地址，而不是数据值。如果我们有一个内存地址并想获取该内存位置中存储的数据值，则必须使用间接运算符 (*) 来获取它。在函数中尝试访问形式参数的每个位置，都将 * 放在形式参数名称之前。

以下是一个按引用传递两个整数并交换其值的程序：

```c
#include <stdio.h>

void swap(int *x, int *y);

int main(void) {
    int a, b;

    a = 5;
    b = 9;

    printf("Before swap: a = %d   b = %d\n", a, b);
    swap(&a, &b);

    printf("After swap: a = %d   b = %d\n", a, b);

    return 0;
}

void swap(int *x, int *y) {
    int temp;

    temp = *x;
    *x = *y;
    *y = temp;
}
```

我们的程序输出如下：

```
Before swap: a = 5   b = 9
After swap: a = 9   b = 5
```

## 按引用传递和 scanf() 函数

如前所述，scanf() 需要知道要读取的项目的地址。因此，变量名前面加上取地址运算符 &。但是，如果参数按引用传递给函数，并且该变量在 scanf() 语句中使用，则无需在变量前面放置取地址运算符。这是因为该变量已经表示一个地址，因为它是按引用传递的。

```c
#include <stdio.h>

void getValue(int *num);

int main(void) {
    int num;

    getValue(&num);
    printf("The Value input = %d\n", num);
    return 0;
}

void getValue(int *num) {
    printf("Enter a number: ");
    scanf("%d", num); // No address-of (&) operator required
}
```

产生的输出如下：

```
Enter a number: 35
The value input = 35
```

## 函数回顾作业

- 1. 编写一个函数 `timeUpdate()`，它接收三个 `int` 参数 `hour`、`min`、`sec`，表示当前时间，并返回更新一秒后的时间。该函数应使用 24 小时制，其中 4:30 a.m. 表示为 4:30，4:30 p.m. 表示为 16:30。

- 2. 解释以下程序的输出。在最后一个 `printf()` 语句中交换参数是否会有任何区别？

```c
#include <stdio.h>

int main(void)
{
    char a = 127, b = -128;

    printf("%5d %5d %5d\n", a, a + 1, b);
    printf("%5d %5d %5d %5d\n", a, a += 1, b, a);
    return 0;
}
```

输出：
127 128 -128
127 -128 -128 -128

C 不指定处理函数参数的顺序。因此，某些 C 编译器可能先查看第一个参数，从而更改可能引用参数的参数的值。一个好的遵循规则是，不要在参数中使用可能更改参数值的表达式。

```c
void timeUpdate(int *hour, int *min, int *sec)
{
    *sec++;
    if (*sec == 60) {
        *sec = 0;
        *min++;
        if (*min == 60) {
            *min = 0;
            *hour++;
            if (*hour == 24)
                *hour = 0;
        }
    }
}
```

[教师注释]
如果 printf 从右到左求值参数，输出：-128 -128 -128
如果从左到右，则输出与打印所示一致。也可能是 -128 -128 -128 -128
答案是未知的。

## 支票账户实验

构建一个 C 程序 check.c，读取月度支票账户的详细信息并输出汇总这些交易的银行对账单。输入文件 account.txt 包含一个月支票账户的交易列表。输入文件的每一行由一个单字符交易代码和一个包含交易金额的 double 组成。有效交易代码如下：

- I : 从上个月结转的初始余额
- D : 存款
- C : 支票

输入每笔交易时，应在单行上输出交易类型、交易金额（存款和支票分列）以及处理交易后的余额：

| 交易 | 存款 | 支票 | 余额 |
|---|---|---|---|
| 初始余额 | | | 478.83 |
| 存款 | 127.45 | | 606.28 |
| 存款 | 619.84 | | 1226.12 |
| 支票 | | 945.12 | 281.00 |
| 支票 | | 4.76 | 276.24 |
| ... | | | |

银行的服务费（应在月底从余额中扣除）如下：

- 每月账户维护费 $3.00。
- 每张兑现的支票 $0.06。
- 每笔存款 $0.03。
- 每当兑现的支票使余额低于 $0.00 时，透支费 $5.00。

注意：当交易是存入透支账户但未使余额高于零时，不收取透支服务费。

