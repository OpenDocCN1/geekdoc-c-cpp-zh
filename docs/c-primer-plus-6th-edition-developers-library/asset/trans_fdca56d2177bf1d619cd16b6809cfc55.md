

两种类型具有不同的有效操作集。例如，你可以把一个整数乘以另一个整数，但不能把一个指针乘以另一个指针。你可以使用 * 运算符来解引用指针，但该操作对整数来说毫无意义。C 语言定义了其基本类型的有效操作。然而，当你设计一个方案来表示数据时，你可能需要自行定义有效操作。在 C 中，你可以通过设计 C 函数来表示所需的操作来实现这一点。简而言之，设计一个数据类型包括决定如何存储数据以及设计一组函数来管理数据。

你还将研究一些 *算法*，即操作数据的配方。作为程序员，你会积累这样一套配方，并反复将其应用于类似的问题。

本章探讨设计数据类型的过程，该过程将算法与数据表示相匹配。在其中，你将遇到一些常见的数据形式，例如队列、列表和二叉搜索树。

你还将被介绍抽象数据类型（ADT）的概念。ADT 以问题导向而非语言导向的方式打包方法和数据表示。在你设计出 ADT 之后，你可以轻松地在不同情况下重用它。理解 ADT 在概念上为你进入面向对象编程（OOP）和 C++ 语言的世界做好了准备。

## 探索数据表示

让我们先思考数据。假设你要创建一个通讯录程序。你会使用什么数据形式来存储信息？由于每个条目都关联着多种信息，用结构体来表示每个条目是有意义的。你如何表示多个条目？用标准的结构体数组？用动态数组？还是用其他形式？条目是否应该按字母顺序排列？你是否应该能够按邮政编码搜索条目？按区号搜索？你想要执行的操作可能会影响你决定如何存储信息。总之，在投入编码之前，你有很多设计决策要做。

你将如何表示一个你想存储在内存中的位图图形图像？位图图像是指屏幕上的每个像素都是单独设置的。在黑白屏幕的时代，你可以用一台计算机位（1 或 0）来表示一个像素（开或关），因此得名 *位图*。使用彩色显示器时，描述单个像素需要不止一个位。例如，如果你为每个像素分配 8 位，你可以获得 256 种颜色。现在行业已发展到 65,536 种颜色（每个像素 16 位）、16,777,216 种颜色（每个像素 24 位）、2,147,483,648 种颜色（每个像素 32 位），甚至更远。如果你的颜色是 32 位并且你的显示器分辨率为 2560×1440，你将需要近 1.18 亿位（14MB）来表示一幅位图图形的单个屏幕。这是可行的方法，还是你可以开发一种压缩信息的方法？这种压缩应该是 *无损* 的（不丢失数据）还是 *有损* 的（丢失相对不重要的数据）？同样，在深入编码之前，你有很多设计决策要做。

让我们处理一个特定的数据表示案例。假设你想编写一个程序，让你输入一年中看过的所有电影（包括录像带、DVD 和蓝光）的列表。对于每部电影，你想记录各种信息，例如标题、上映年份、导演、主演、长度、电影类型（喜剧、科幻、浪漫、胡说八道等等）、你的评价等等。这表明为每部电影使用一个结构体，为列表使用一个结构体数组。为了简化问题，让我们将结构体限制为两个成员：电影标题和你的评价，一个 0 到 10 的等级。清单 17.1 显示了使用这种方法的基本实现。

```
Listing 17.1  **The `films1.c` Program**

```c
/* films1.c -- using an array of structures */
#include <stdio.h>
#include <string.h>
#define TSIZE          45      /* size of array to hold title  */
#define FMAX           5       /* maximum number of film titles */

struct film {
    char title[TSIZE];
    int rating;
};
char * s_gets(char * st, int n);
int main(void)
{
    struct film movies[FMAX];
    int i = 0;
    int j;

    puts("Enter first movie title:");
    while (i < FMAX && s_gets(movies[i].title, TSIZE) != NULL &&
           movies[i].title[0] != '\0')
    {
        puts("Enter your rating <0-10>:");
        scanf("%d", &movies[i++].rating);
        while (getchar() != '\n')
            continue;
        puts("Enter next movie title (empty line to stop):");
    }
    if (i == 0)
        printf("No data entered. ");
    else
        printf ("Here is the movie list:\n");

        for (j = 0; j < i; j++)
            printf("Movie: %s Rating: %d\n", movies[j].title,
                   movies[j].rating);
}
```
```

```
printf("Bye!\n");

return 0;
}

char * s_gets(char * st, int n)
{
    char * ret_val;
    char * find;

    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        find = strchr(st, '\n');    // look for newline
        if (find)                   // if the address is not NULL,
            *find = '\0';           // place a null character there
        else
            while (getchar() != '\n')
                continue;           // dispose of rest of line
    }
    return ret_val;
}
```

该程序创建一个结构体数组，然后用用户输入的数据填充数组。输入会一直继续，直到数组已满（FMAX 测试），直到到达文件结束（NULL 测试），或直到用户在行首按下 Enter 键（‘\0’ 测试）。

这种表述存在一些问题。首先，该程序很可能会浪费大量空间，因为大多数电影的标题没有 40 个字符那么长，但有些电影的标题确实很长，例如 The Discreet Charm of the Bourgeoisie 和 Won Ton Ton, The Dog Who Saved Hollywood。其次，许多人会发现每年五部电影的限制过于严格。当然，你可以增加该限制，但什么值才合适？有些人一年看 500 部电影，所以你可以将 FMAX 增加到 500，但这对某些人来说仍然可能太小，而对其他人来说可能会浪费大量内存。此外，一些编译器为自动存储类变量（如 movies）可用的内存量设置了默认限制，而这样大的数组可能会超出该值。你可以通过将数组设为静态或外部数组或指示编译器使用更大的栈来修复它，但这并没有解决真正的问题。

真正的问题是数据表示过于不灵活。你必须在编译时做出在运行时做出更好决定的决策。这表明切换到使用动态内存分配的数据表示。你可以尝试这样做：

```
#define TSIZE 45          /* size of array to hold title */
struct film {
    char title[TSIZE];
    int rating;
};
```

```
```c
int n, i;
struct film * movies; /* pointer to a structure */
...
printf("Enter the maximum number of movies you'll enter:\n");
scanf("%d", &n);
movies = (struct film *) malloc(n * sizeof(struct film));
```
```

在这里，就像第 12 章“存储类、链接和内存管理”中一样，你可以使用指针 movies，就好像它是一个数组名一样：

```
```c
while (i < FMAX && s_gets(movies[i].title, TSIZE) != NULL && movies[i].title[0] != '\0')
```
```

通过使用 malloc()，你可以推迟确定元素数量直到程序运行时，因此如果只需要 20 个元素，程序就不必分配 500 个元素。然而，它把为条目数量提供正确值的负担放在了用户身上。

## 超越数组到链表

理想情况下，你希望能够无限地添加数据（或直到程序内存耗尽）而无需提前指定将要创建多少条目，也无需让程序不必要地分配巨大的内存块。你可以通过在每次输入后调用 malloc() 并只分配足够空间来容纳新条目来实现这一点。用户输入三部电影，程序调用 malloc() 三次。如果用户输入 300 部电影，程序调用 malloc() 300 次。

这个好主意引发了一个新问题。为了了解它是什么，请比较一次调用 malloc()，请求足够容纳 300 个电影结构体的空间，以及 300 次调用 malloc()，每次请求足够容纳一个电影结构体的空间。前一种情况将内存分配为一个连续的内存块，你只需要跟踪内容的一个指向结构体变量（film），该变量指向块中的第一个结构体，如前面的代码段所示。第二种方法的难题在于，不能保证连续的 malloc() 调用会产生相邻的内存块。这意味着结构体不一定会连续存储（参见图 17.1）。因此，与其存储指向 300 个结构体块的一个指针，不如存储 300 个指针，每个独立分配的结构体一个！

