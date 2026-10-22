

## 访问结构成员

结构就像一个“超级数组”，其中一个元素可以是 char，下一个元素是 float，再下一个是 int 数组。你可以通过使用下标来访问数组的各个元素。如何访问结构的各个成员？使用点号（.），即结构成员运算符。例如，library.value 是 library 的 value 部分。你可以像使用任何其他 float 变量一样使用 library.value。同样，你可以像使用 char 数组一样使用 library.title。因此，程序使用如下表达式

```
s_gets(library.title, MAXTITL);
```

和

```
scanf("%f", &library.value);
```

本质上，.title、.author 和 .value 充当 book 结构的下标。

请注意，尽管 library 是一个结构，但 library.value 是 float 类型，并像任何其他 float 类型一样使用。例如，scanf("%f",...) 需要一个 float 位置的地址，而 &library.value 就是它。这里点号的优先级高于 &，因此该表达式等同于 &(library.value)。

如果你有第二个相同类型的结构变量，你会使用相同的方法：

```
struct book bill, newt;
```

```
s_gets(bill.title, MAXTITL);
s_gets(newt.title, MAXTITL);
```

.title 指的是 book 结构的第一个成员。请注意初始程序如何以两种不同的格式打印结构 library 的内容。这说明了你在使用结构成员时拥有的自由度。

## 结构的初始化器

C99 和 C11 为结构提供了指定初始化器。其语法与数组的指定初始化器类似。然而，结构的指定初始化器使用点运算符和成员名称来标识特定元素，而不是使用方括号和索引。例如，要仅初始化 book 结构的 value 成员，你可以这样做：

```
struct book surprise = { .value = 10.99 };
```

你可以用任何顺序使用指定初始化器：

```
struct book gift = { .value = 25.99,
    .author = "James Broadfool",
    .title = "Rue for the Toad" };
```

与数组一样，指定初始化器之后出现的普通初始化器会为指定成员之后的成员提供值。此外，为特定成员提供的最后一个值就是它得到的值。例如，考虑以下声明：

```
struct book gift= { .value = 18.90,
    .author = "Philionna Pestle",
    0.25};
```

值 0.25 被分配给 value 成员，因为它是在结构声明中 author 成员之后列出的第一个成员。新的 0.25 值取代了之前提供的 18.90 值。现在你掌握了这些基础知识，就准备好扩展视野，查看结构的几个推论。你将看到结构的数组、结构的嵌套、指向结构的指针，以及处理结构的函数。

## 结构的数组

让我们扩展我们的 book 程序以处理更多书籍。显然，每本书都可以用 book 类型的结构变量来描述。要描述两本书，你需要使用两个这样的变量，以此类推。要处理多本书，你可以使用此类结构的数组，这就是我们在下一程序中创建的内容，见清单 14.2。 （如果你使用 Borland C/C++，请参阅本章后面的“Borland C 和浮点数”部分。）

## 结构与内存

manybook.c 程序使用一个包含 100 个结构的数组。因为该数组是自动存储类对象，信息通常放在栈上。如此大的数组需要一大块内存，这可能会导致问题。如果出现运行时错误，也许抱怨栈大小或栈溢出，你的编译器可能使用的默认栈大小对于此示例来说太小了。要修复这个问题，你可以使用编译器选项将栈大小设置为 10,000 以容纳结构的数组，或者你可以使数组为 static 或 external（这样它就不会放在栈中），或者你可以将数组大小减少到 16。为什么我们一开始不把栈做得小一点？因为你应该了解潜在的栈大小问题，以便在自己遇到时能够应对。

## 清单 14.2 manybook.c 程序

```
/* manybook.c -- multiple book inventory */
#include <stdio.h>
#include <string.h>
char * s_gets(char * st, int n);
#define MAXTITL  40
#define MAXAUTL  40
#define MAXBKS   100        /* maximum number of books  */

struct book {
    /* set up book template */
    char title[MAXTITL];
    char author[MAXAUTL];
    float value;
};

int main(void)
{
    struct book library[MAXBKS]; /* array of book structures */
    int count = 0;
    int index;

    printf("Please enter the book title.\n");
    printf("Press [enter] at the start of a line to stop.\n");
    while (count < MAXBKS && s_gets(library[count].title, MAXTITL) != NULL
        && library[count].title[0] != '\0')
    {
        printf("Now enter the author.\n");
        s_gets(library[count].author, MAXAUTL);
        printf("Now enter the value.\n");
        scanf("%f", &library[count++].value);
        while (getchar() != '\n')
            continue;           /* clear input line */
        if (count < MAXBKS)
            printf("Enter the next title.\n");
    }

    if (count > 0)
    {
        printf("Here is the list of your books:\n");
        for (index = 0; index < count; index++)
            printf("%s by %s: $%.2f\n", library[index].title,
                library[index].author, library[index].value);
    }
    else
        printf("No books? Too bad.\n");

    return 0;
}

char * s_gets(char * st, int n)
{
    char * ret_val;
    char * find;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
```

```
char first[LEN];
char last[LEN];
};

struct guy {
    // second structure
    struct names handle;    // nested structure
    char favfood[LEN];
    char job[LEN];
    float income;
};

int main(void)
{
    struct guy fellow = {  // initialize a variable
        { "Ewen", "Villard" },
        "grilled salmon",
        "personality coach",
        68112.00
    };

    printf("Dear %s, \n\n", fellow.handle.first);
    printf("%s%s\n", msgs[0], fellow.handle.first);
    printf("%s%s\n", msgs[1], fellow.job);
    printf("%s\n", msgs[2]);
    printf("%s%s%s", msgs[3], fellow.favfood, msgs[4]);
    if (fellow.income > 150000.0)
        puts("!!");
    else if (fellow.income > 75000.0)
        puts("!");
    else
        puts(".");
    printf("\n%40s%s\n", " ", "See you soon,");
    printf("%40s%s\n", " ", "Shalala");

    return 0;
}
```

以下是输出：

Dear Ewen,

    Thank you for the wonderful evening, Ewen.
You certainly prove that a personality coach
is a special kind of guy. We must get together
over a delicious grilled salmon and have a few laughs.

                                    See you soon,
                                    Shalala

指定结构成员值的第二种方法源于以下序列：如果 him == &fellow[0]，那么 *him == fellow[0]，因为 & 和 * 是互逆运算符。因此，通过替换，你得到以下内容：

```
fellow[0].income == (*him).income
```

需要括号，因为 . 运算符的优先级高于 *。

总之，如果 him 是指向名为 barney 的 guy 类型结构的指针，以下所有表达式都是等价的：

```
barney.income == (*him).income == him->income   // assuming him == &barney
```

现在让我们看看结构与函数之间的交互。

## 告诉函数关于结构

回想一下，函数参数将值传递给函数。每个值都是一个数字——可能是 int，可能是 float，可能是 ASCII 字符代码，或可能是地址。结构比单个值复杂一些，因此不足为奇，古老的 C 实现不允许结构作为函数的参数使用。这一限制在更新的实现中被移除了，ANSI C 允许结构作为参数使用。因此，现代实现为你提供了在参数中传递结构和传递指向结构的指针之间的选择——或者如果你只关心结构的一部分，你可以传递结构成员作为参数。我们将检查这三种方法，首先从传递结构成员作为参数开始。

## 传递结构成员

只要结构成员是具有单一值的数据类型（即 int 或其相关类型、char、float、double 或指针），它就可以作为函数参数传递给接受该特定类型的函数。清单 14.5 中初级的财务分析程序，它将客户的银行账户加到其储蓄和贷款账户，说明了这一点。

## 清单 14.5 funds1.c 程序

```
/* funds1.c -- passing structure members as arguments */
#include <stdio.h>
#define FUNDLEN 50

struct funds {
    char  bank[FUNDLEN];
    double bankfund;
    char  save[FUNDLEN];
    double savefund;
};
```
