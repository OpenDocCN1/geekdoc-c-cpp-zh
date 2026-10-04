
x[t] = '\0';

printf("After concatenation the first name is:\n\n");
puts(x);

}

```

Output:

Input the first name: DHABAL
Input the last name: SETHI
After concatenation the first name is: DHABALSETHI

# 12.4.5 `strrev()` 函数

该函数用于反转字符串。

11. /* 使用 `strrev(void)` 反转字符串的程序 */

```c
#include <stdio.h>
#include <string.h>

void main(void)
{
    char x[20];

    printf("Input the string: ");
    gets(x);

    strrev(x);

    printf("Reverse of inputted string is: %s", x);
}
```

输出：

输入字符串：dhabal
输入字符串的反转是：labah

记忆技巧
如果 `scanf()` 函数读取字符串输入，则不要在该地址变量中提供 "&"（地址操作符）。

# Q12. /* 不使用 `strrev()` 函数反转字符串的程序 */

```c
#include <stdio.h>
#include <string.h>

void main()
{
    char x[30], revx[30];
    int i = 0, j = 0;

    printf("Input the string to be reversed:");
    scanf("%s", x);

    for (i = strlen(x) - 1; i >= 0; i--)
    {
        revx[j] = x[i];
        j++;
    }

    revx[j] = '\0';

    printf("The reversed string is:%s", revx);
}
```

输出：

输入要反转字符串：UTKAL
反转后的字符串是：LAKTU

记忆技巧
- 最后一个字符始终是 `'\0'`，这个 `'\0'` 被称为空字符。
- `'\0'` 的 ASCII 值为 0。
- `'\0'` 的 ASCII 值为 48。
- `printf()` 函数不会打印 `'\0'`。
- 在 C 语言中，字符串的末尾由空字符标记。
- `'\0'` 不是两个字符，它实际上是一个字符。`\` 表示后面跟着内容，它是一个特殊字符。
- 字符数组的元素存储在连续的内存位置中。
- `'\0'` 不是一个字符串，而是字符的集合。
- `printf()` 函数中使用的 `%s` 是打印字符串的格式说明符。

# Q13. /* 不使用 `strlen()` 函数获取字符串长度的程序 */

```c
#include <stdio.h>

void main(void)
{
    char x[20];
    int j = 0;

    printf("Input the string:");
    gets(x);

    while (x[j] != '\0')
        j++;

    printf("Length of string is: %d", j);
}
```

输出：

输入字符串：DHABAL
字符串长度为：6

# Q14 /* 不使用字符串函数判断字符串是否为回文的程序 */

```c
#include <stdio.h>
#include <string.h>

void main(void)
{
    char x[20];
    int i, j = 0, c = 0;

    printf("Input the string to check palindrome:");
    gets(x);

    for (i = 0; x[i] != '\0'; i++)
        ; // 原代码此处为空语句，计算长度

    j = i - 1;

    while (i < j) // 注意：原代码逻辑此处 i 已指向末尾，循环条件通常不成立，保留原逻辑
    {
        if (x[i] != x[j])
        {
            c = 1;
            break;
        }
        i++;
        j--;
    }

    if (c == 0)
        printf("The string is a palindrome");
    else
        printf("The string is not palindrome");
}
```

输出：

输入要检查回文的字符串：AAA
该字符串是回文

# Q15. /* C语言程序：查找句子中元音、辅音、数字和空格字符的数量 */

```c
#include <stdio.h>

void main(void)
{
    char x[150];
    int j, count1, count2, count3, count4;

    count1 = count2 = count3 = count4 = 0;

    printf("Input an English sentence:");
    gets(x);

    for (j = 0; x[j] != '\0'; j++)
    {
        if (x[j] == 'a' || x[j] == 'e' || x[j] == 'i' || x[j] == 'o' || x[j] == 'u' ||
            x[j] == 'A' || x[j] == 'E' || x[j] == 'I' || x[j] == 'O' || x[j] == 'U')
            count1++;
        else if ((x[j] >= 'a' && x[j] <= 'z') || (x[j] >= 'A' && x[j] <= 'Z'))
            count2++;
        else if (x[j] >= '0' && x[j] <= '9')
            count3++;
        else if (x[j] == ' ')
            count4++;
    }

    printf("Vowels in the sentence:%d\n", count1);
    printf("Consonants in the sentence:%d\n", count2);
    printf("Digits in the sentence:%d\n", count3);
    printf("White spaces in the sentence:%d\n", count4);
}
```

输出：

输入英语句子：I AM DHABAL
句子中的元音：4
句子中的辅音：5
句子中的数字：0
句子中的空格：2

## 总结

- 1. 字符串是字符序列，并被视为一个单一的数据项。
- 2. `%s` 是用于输入和显示字符串的格式字符。
- 3. `strlen()` 用于计算该字符串中存在的字符数量。
- 4. `strcpy()` 函数用于将一个字符串复制到另一个字符串。
- 5. `strcmp()` 函数用于比较两个字符串。
- 6. `strcat()` 函数用于连接字符串。
- 7. `strrev()` 函数用于反转字符串。
- 8. 字符串的最后一个字符是 `'\0'`。

# 问题

- 1. 字符串是什么？
- 2. 字符串处理函数。
- 3. `getchar()` 和 `gets()` 的区别？
- 4. `putchar()` 和 `puts()` 的区别？
- 5. 字符串处理。
- 6. `strcmp()` 是什么？

# 长题

- 1. 编写一个判断字符串是否为回文的 C 程序。
- 2. 编写一个查找句子中元音数量的 C 程序。
- 3. 字符串的末尾是 `'\0'`。

# C语言编程的 324 个概念与技术

## 22. 输出结果是什么？

```c
#include <stdio.h>

void main()
{
    char x[] = "Bhubaneswar";
    x[0] = 'C';
    printf("%s,%s", x);
    x = "Cuttack";
    printf("%s", x + 1);
}
```

输出：
编译错误

## 23. 输出结果是什么？

```c
#include <stdio.h>

void main(void)
{
    printf(12 + "BHUBANESWAR-ODISHA");
}
```

输出：
ODISHA

## 24. 输出结果是什么？

输出：
输入字符串： dhabal labdah

# 13 指针

## 13.1 引言

在第 4 章中我们学习了变量是一个用于存储值的内存位置。为了访问变量的内存地址，我们可以使用 `&`（取地址符）运算符。

让我们来看编程示例：

```c
#include <stdio.h>

void main(void)
{
    int x;
    printf("Address of variable x is:%u", &x);
}
```

输出：
变量 x 的地址：1000

**解释：**

从上面的讨论中，我们学习了内存地址。让我们来看看指针的概念。定义：它是一种由基本数据类型之一（如 `int`, `char`, `float`, `double`）构建的派生类型。它将内存地址作为它的值。它可以用于访问和操作存储在计算机内存中的数据。因此，指针是 C 语言中最强大且最令人兴奋的特性之一。

### 使用指针的主要优点

1. 函数一次不能向调用者返回多个值。但指针可以在函数中使用指针向调用者返回多个值。
2. 在数组中，我们可以通过分配必要的空间，在运行时决定数组的大小。
3. 它支持动态内存分配。

### 指针的缺点

如果运行时没有足够的内存来存储指针，程序可能会崩溃（可能性极小）。

### 13.1.1 什么是指针变量？

指针变量是一个存储计算机内存中另一个变量地址的变量。

### 13.1.2 指针变量声明

**指针变量声明的语法**

`data_type *variable_name;`

**解释：**
在上面的声明中，数据类型通过使用基本数据类型（如 `int`, `char`, `float`, `double`）决定指针将持有什么类型的数据值，然后 `*variable_name` 前面的 `*` 标识该 `variable_name` 是一个指针变量。

### 记忆技巧

指针变量声明之所以有效，因为它向 C 编译器提供了关于指针变量的三个基本信息/报告。第一是放在指针变量前的星号 (`*`) 标识了它是一个指针变量。第二是指针变量需要一个内存位置，其中将包含另一个变量的地址，第三是指针变量应该指向相同数据类型的变量。

让我们来看带有相应数据类型的指针变量声明示例。

### 使用基本数据类型声明指针变量的示例

1. `int *x;`
2. `float *x;`
3. `char *x;`
4. `double *x;`

#### 示例 1 到 4 的解释

1. `int *x;`
   此语句声明变量 `x` 是一个指向整数类型值的指针变量，例如，指针变量 `x` 可能持有一个垃圾值，因为在上面的语法中没有对值进行初始化，或者如果初始化了则持有初始化值。

2. `float *x;`
   此声明变量 `x` 是一个指向 `float` 类型值的指针变量。它可能持有垃圾值或初始化值。

3. `char *x;`
   此声明变量 `x` 是一个指向 `char` 类型值的指针变量。它可能持有垃圾值或初始化值。

4. `double *x;`
   此声明变量 `x` 是一个指向 `double` 类型值的指针变量。它可能持有垃圾值或初始化值。

### 记忆技巧

指针用于访问和输入存储在计算机内存中的数据。

**Q. 当我们声明指针变量时，例如 `int *x;` 或带有其他数据类型（`char`, `float`, `double`）的指针变量 `x`，那么 x 将包含什么值？**
答案是当我们声明指针变量 `x` 时，它将指向未知的位置，因为它在寻找一些数据值来存储。这些数据值被称为垃圾值，是由系统自动生成的。

![图 13.1 指针变量声明的图示](img/15f2d3c4e623a0624f0481e94908bbcb_342_0.png)

### 记忆技巧

`int *x;`
在上面的声明中，`x` 是一个指针变量，`*x` 并不被称为指针变量。但 `x` 前面的 `*` 标识了 `x` 是一个指针变量。

### 记忆技巧

指针是一个变量，它只包含地址，例如，它包含另一个变量的地址。

指针概念中有两个重要的运算符。它们是：

- (a) `*` 和 (b) `&`
- (a) `*` 称为间接运算符或解引用运算符。
- (b) `&` 称为地址运算符。

## 13.2 指针的不同声明方式

1. `int *x;`
2. `float *x;`
3. `char *x;`
4. `double *x;`

### 13.3 指针初始化

指针初始语法为：

`pointer_name = &variable_name;`

在上面的图中，让我们看看指针变量 `y` 如何持有另一个变量 `x` 的地址 1000。

## 13.4 空指针

被赋值的指针被称为空指针。如果指针变量被赋值了任何值，那么它总是被赋值为 `NULL` 指针变量。空指针是一个在库中定义的值的常量。

```c
{
    int *y = NULL;
    printf("value of pointer variable y is:%u", y);
}
```

输出:
指针变量 y 的值是:0

## 13.5 使用指针概念访问变量

要通过指针概念访问变量的值，程序员应该使用星号运算符 (`*`)。星号通常被称为间接引用运算符。间接引用运算符另一个名称是解引用运算符。

# Q3. 解引用指针的示例。

解决方案：

```c
************************************************
文件名: pointer3.c
作者信息: Mr. x, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
程序执行日期: 10/8/2015
程序名称: 解引用指针的示例。
************************************************
```

```c
#include <stdio.h>

void main(void)
{
    int x = 5;
    int *y;
    y = &x;

    printf("value of x is:%d\n", x);
    printf("value of x is:%d\n", *y);  // 原代码 *x 非法，推测为 *y
    printf("value of x is:%d\n", (*y)); // 原代码 (*x) 非法，推测为 (*y)
    printf("value of x is:%d\n", *y);
}
```

输出：
x 的值是: 5
x 的值是: 5
x 的值是: 5
x 的值是: 5

**解释：**

通过程序中上面的 `printf` 语句，我们以不同的方式打印 `x` 的值。首先打印变量 `x` 的值，然后第二、第三、第四个 `printf` 语句都是通过指针概念打印 `x` 的值。

## 13.6 通用指针

通用指针的另一种名称是空指针。通用指针是一种可以指向任何数据类型的指针变量。当我们声明它时，语法与通用指针变量相同，但使用 `void` 代替基本数据类型。

# Q4. 通用指针变量示例。

解决方案：

```c
************************************************************************************
文件名: pointer2.c
作者信息: Mr. x, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
程序执行日期: 10/8/2015
程序名称: 通用指针变量的示例。
************************************************************************************
```

```c
#include <stdio.h>

void main()
{
    int x = 4;
    char c = 'D';
    float m = 10.7;
    void *y;

    y = &x;
    printf("%d\n", *(int *)y);

    y = &c;
    printf("%c\n", *(char *)y);

    y = &m;
    printf("%f\n", *(float *)y);
}
```

输出：

4
D
10.700000

**解释：**

在上面的程序中，第一个 `printf` 函数打印输出 4。在 `printf` 语句中使用类型转换 `(int *)y` 是因为 `y` 是 `void` 类型，而我们的目标是打印 `int` 类型的 `x` 的值，我们通过语法 `(int *)` 将 `void` 数据类型强制转换为 `int` 数据类型，后续的 `printf` 语句都遵循了第一个语法。

## 13.7 指针的指针

在指针的指针声明中，声明了两个指针变量，其中一个包含单星号，另一个包含双星号 (`**`)。指针的指针意味着一个指针变量（包含双星号）持有另一个指针变量（包含单星号）的地址。同样，另一个指针变量（包含单星号）持有一个变量的地址。整个过程被称为多次间接引用。

**指针的指针变量声明语法**

`int **x;`

双星号用于声明指针的指针变量。上面的声明告诉我们 `x` 是一个指向 `int` 类型指针的指针。
