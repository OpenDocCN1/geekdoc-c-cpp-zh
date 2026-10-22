

## 摘要

本章的主要主题是程序控制。C 提供了许多用于结构化程序的辅助工具。`while` 和 `for` 语句提供了入口条件循环。`for` 语句特别适合涉及初始化和更新的循环。逗号运算符使你能够在一个 `for` 循环中初始化和更新一个以上的变量。对于较少见的需要出口条件循环的情况，C 有 `do while` 语句。

一个典型的 `while` 循环设计如下所示：

```
get first value
while (value meets test)
{
    process the value
    get next value
}
```

执行相同功能的 `for` 循环如下所示：

```
for (get first value; value meets test; get next value)
    process the value
```

所有这些循环都使用测试条件来确定是否执行另一次循环。总体而言，如果测试表达式求值为非零值，则循环继续；否则，循环终止。通常，测试条件是一个关系表达式，即使用关系运算符形成的表达式。这样的表达式如果关系为真则值为 1，否则为 0。C99 引入的 `_Bool` 类型的变量只能保存值 1 或 0，表示真或假。

除了关系运算符之外，本章还研究了 C 的几个算术赋值运算符，例如 `+=` 和 `*=`。这些运算符通过对其执行算术运算来修改左操作数的值。

数组是下一个主题。数组使用方括号声明以指示元素数量。数组的第一个元素编号为 0；第二个编号为 1，以此类推。例如，声明

```
double hippos[20];
```

创建一个包含 20 个元素的数组，各个元素从 `hippos[0]` 到 `hippos[19]`。用于编号数组的子脚本可以通过使用循环方便地操作。

最后，本章展示了如何编写和使用具有返回值 的函数。

## 复习题

你可以在附录 A“复习题答案”中找到复习题的答案。

- 1. 在每行之后 `quack` 的值是多少；最后五条语句中的每一条都使用前一条语句产生的 `quack` 的值。
  ```
  int quack = 2;
  quack += 5;
  quack *= 10;
  quack -= 6;
  quack /= 8;
  quack %= 3;
  ```

- 2. 已知 `value` 为 `int`，以下循环会产生什么输出？
  ```
  for ( value = 36; value > 0; value /= 2 )
      printf("%3d", value);
  ```
  如果 `value` 是 `double` 而不是 `int` 会有什么问题？

- 3. 表示以下每个测试条件：
  a. `x` 大于 5。
  b. `scanf()` 尝试读取一个 `double`（称为 `x`）并失败。
  c. `x` 的值为 5。

- 4. 表示以下每个测试条件：
  a. `scanf()` 成功读取一个整数。
  b. `x` 不等于 5。
  c. `x` 大于或等于 20。

- 5. 你怀疑以下程序不完美。你能找到什么错误？
  ```
  #include <stdio.h>
  int main(void)
  {
      int i, j, list(10);
  
      for (i = 1, i <= 10, i++)
      {
          list[i] = 2*i + 3;
          for (j = 1, j >= i, j++)
              printf(" %d", list[j]);
  ```

```
printf("\n");
}
/* line 11 */
/* line 12 */
```

- 6. 使用嵌套循环编写一个产生以下模式的程序：

$$$$$$$$ 
$$$$$$$$ 
$$$$$$$$ 
$$$$$$$$

- 7. 以下每个程序会打印什么？

a.
```
#include <stdio.h>

int main(void)
{
    int i = 0;

    while (++i < 4)
        printf("Hi! ");
    do
        printf("Bye! ");
    while (i++ < 8);
    return 0;
}
```

b.
```
#include <stdio.h>

int main(void)
{
    int i;
    char ch;

    for (i = 0, ch = 'A'; i < 4; i++, ch += 2 * i)
        printf("%c", ch);
    return 0;
}
```

- 8. 给定输入 `Go west, young man!`，以下每个程序会产生什么输出？（`!` 在 ASCII 序列中跟在空格字符之后。）

a.
```
#include <stdio.h>
```
```
int main(void)
{
    char ch;

    scanf("%c", &ch);
    while ( ch != 'g' )
    {
        printf("%c", ch);
        scanf("%c", &ch);
    }
    return 0;
}
```

b.
```
#include <stdio.h>

int main(void)
{
    char ch;

    scanf("%c", &ch);
    while ( ch != 'g' )
    {
        printf("%c", ++ch);
        scanf("%c", &ch);
    }
    return 0;
}
```

c.
```
#include <stdio.h>

int main(void)
{
    char ch;

    do {
        scanf("%c", &ch);
        printf("%c", ch);
    } while ( ch != 'g' );
    return 0;
}
```

d.
```
#include <stdio.h>

```
{ char ch;

scanf("%c", &ch);
for ( ch = '$'; ch != 'g'; scanf("%c", &ch) )
    printf("%c", ch);
return 0;
}
```

9. 以下程序会打印什么？

```
#include <stdio.h>
int main(void)
{
    int n, m;

    n = 30;
    while (++n <= 33)
        printf("%d|",n);

    n = 30;
    do
        printf("%d|",n);
    while (++n <= 33);

    printf("\n***\n");

    for (n = 1; n*n < 200; n += 4)
        printf("%d\n", n);

    printf("\n***\n");

    for (n = 2, m = 6; n < m; n *= 2, m+= 2)
        printf("%d %d\n", n, m);

    printf("\n***\n");

    for (n = 5; n > 0; n--)
    {
        for (m = 0; m <= n; m++)
            printf("=");
        printf("\n");
    }
    return 0;
}
```

10. 考虑以下声明：

```
double mint[10];
```

- a. 数组名是什么？
- b. 数组有多少个元素？
- c. 每个元素可以存储什么类型的值？
- d. 以下哪一个是使用 `scanf()` 与此数组的正确用法？
  i. scanf("%lf", mint[2])
  ii. scanf("%lf", &mint[2])
  iii. scanf("%lf", &mint)

11. 诺亚先生喜欢逢二计数，所以他编写了以下程序来创建一个数组并用整数 2、4、6、8 等填充它。这个程序有什么问题，如果有的话？

```
#include <stdio.h>
#define SIZE 8
int main(void)
{
    int by_twos[SIZE];
    int index;

    for (index = 1; index <= SIZE; index++)
        by_twos[index] = 2 * index;
    for (index = 1; index <= SIZE; index++)
        printf("%d ", by_twos[index]);
    printf("\n");
    return 0;
}
```

12. 你想编写一个返回 `long` 值的函数。你的函数定义应包含什么？

13. 定义一个函数，它接受一个 `int` 参数并返回该值的平方作为 `long`。

14. 以下程序会打印什么？

```
#include <stdio.h>
int main(void)
{
    int k;
```

如果你的系统不按数字顺序编码字母，请参阅编程练习 3 中的建议。

- 5. 让程序要求用户输入一个大写字母。使用嵌套循环产生如下的金字塔模式：
  A
  ABA
  ABCBA
  ABCDCBA
  ABCDEDCBA

模式应扩展到输入的字符。例如，前面的模式将由输入值 `E` 产生。提示：使用外层循环处理行。使用一行中的三个内层循环，一个处理空格，一个用于按升序打印字母，一个用于按降序打印字母。如果你的系统不使用 ASCII 或类似系统，该系统以严格的数字顺序表示字母，请参阅编程练习 3 中的建议。

- 6. 编写一个程序打印一张表，每行给出一个整数、其平方和其立方。要求用户输入表的下限和上限。使用 `for` 循环。

- 7. 编写一个程序将单个单词读入字符数组，然后反向打印该单词。提示：使用 `strlen()`（第 4 章）计算数组中最后一个字符的索引。

- 8. 编写一个程序请求两个浮点数并打印它们之差除以它们之积的值。让程序循环处理输入值对，直到用户输入非数字输入。

- 9. 修改练习 8，使其使用函数返回计算值。

- 10. 编写一个程序请求下限和上限整数限制，计算从下限的平方到上限的平方的所有整数平方之和，并显示答案。程序应继续提示输入限制并显示答案，直到用户输入的上限小于或等于下限。示例运行应如下所示：

```
Enter lower and upper integer limits: 5 9
The sums of the squares from 25 to 81 is 255
Enter next set of limits: 3 25
The sums of the squares from 9 to 625 is 5520
Enter next set of limits: 5 5
Done
```

