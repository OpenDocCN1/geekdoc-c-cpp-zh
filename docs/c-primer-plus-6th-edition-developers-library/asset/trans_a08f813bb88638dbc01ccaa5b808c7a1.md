

## 将结构体作为参数传递

对于允许将结构体作为参数传递的编译器，上一个示例可以改写为如 14.7 节所示。

### 列表 14.7 funds3.c 程序

```
/* funds3.c -- passing a structure */
#include <stdio.h>
#define FUNDLEN 50

struct funds {
    char  bank[FUNDLEN];
    double bankfund;
    char  save[FUNDLEN];
    double savefund;
};

double sum(struct funds moolah);  /* argument is a structure */

int main(void)
{
    struct funds stan = {
        "Garlic-Melon Bank",
        4032.27,
        "Lucky's Savings and Loan",
        8543.94
    };

    printf("Stan has a total of $%.2f.\n", sum(stan));

    return 0;
}

double sum(struct funds moolah)
{
    return(moolah.bankfund + moolah.savefund);
}
```

再次，输出如下：

Stan has a total of $12576.21.

我们用 moolah 替换了 money，后者是指向 struct funds 的指针，而 moolah 是一个 struct funds 变量。当 sum() 被调用时，会根据 funds 模板创建一个名为 moolah 的自动变量。然后该结构体的成员被初始化为结构体 stan 中对应成员的值的副本。因此，计算

```
void showinfo(const struct namect *);
char * s_gets(char * st, int n);

int main(void)
{
    struct namect person;

    getinfo(&person);
    makeinfo(&person);
    showinfo(&person);
    return 0;
}

void getinfo (struct namect * pst)
{
    printf("Please enter your first name.\n");
    s_gets(pst->fname, NLEN);
    printf("Please enter your last name.\n");
    s_gets(pst->lname, NLEN);
}

void makeinfo (struct namect * pst)
{
    pst->letters = strlen(pst->fname) +
    strlen(pst->lname);
}

void showinfo (const struct namect * pst)
{
    printf("%s %s, your name contains %d letters.\n",
           pst->fname, pst->lname, pst->letters);
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
```

```
}
    return ret_val;
}
```

编译并运行程序会产生如下结果：

```
Please enter your first name.
Viola
Please enter your last name.
Plunderfest
Viola Plunderfest, your name contains 16 letters.
```

程序的工作被分配给从 main() 调用的三个函数。在每种情况下，person 结构体的地址都被传递给函数。

getinfo() 函数将信息从自身传输到 main()。具体来说，它从用户获取姓名并将它们放入 person 结构体中，使用 pst 指针来定位它。回想一下 pst->lname 表示由 pst 指向的结构体的 lname 成员。这使得 pst->lname 等同于一个字符数组的名称，因此是 gets() 的合适参数。注意，尽管 getinfo() 向主程序提供信息，但它不使用返回机制，因此其类型为 void。

makeinfo() 函数执行双向信息传输。通过使用指向 person 的指针，它定位存储在结构体中的两个姓名。它使用 C 库函数 strlen() 计算每个姓名中的字母总数，然后使用 person 的地址存放总和。同样，类型为 void。最后，showinfo() 函数使用指针定位要打印的信息。由于该函数不更改数组的内容，因此它将指针声明为 const。

在所有这些操作中，只有一个结构体变量 person，而每个函数都使用结构体地址来访问它。一个函数将信息从自身传输到调用程序，一个函数将信息从调用程序传输到自身，还有一个函数同时做了这两者。

现在让我们看看如何使用结构体参数和返回值来编程相同的任务。首先，要传递结构体本身，请使用参数 person 而不是 &person。相应的形式参数然后被声明为 struct namect 类型，而不是指向该类型的指针。其次，要向 main() 提供结构体值，可以返回一个结构体。列表 14.9 展示了非指针版本。

### 列表 14.9 names2.c 程序

```
/* names2.c -- passes and returns structures */
#include <stdio.h>
#include <string.h>

#define NLEN 30
struct namect {
```

```
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

这个版本产生的最终结果与前一个版本相同，但其进行的方式不同。三个函数中的每一个都创建了 person 的自己的副本，因此该程序使用四个不同的结构体而不是只有一个。

例如，考虑 makeinfo() 函数。在第一个程序中，person 的地址被传递，函数操作实际的 person 值。在这个第二个版本中，创建了一个名为 info 的新结构体。存储在 person 中的值被复制到 info，函数对副本进行操作。因此，当字母数被计算时，它存储在 info 中，而不是 person 中。然而，返回机制修复了这个问题。makeinfo() 行

```
return info;
```

结合 main() 行

```
person = makeinfo(person);
```

将存储在 info 中的值复制到 person 中。注意 makeinfo() 函数必须被声明为 struct namect 类型，因为它返回一个结构体。

## 结构体还是指向结构体的指针？

假设你必须编写一个与结构体相关的函数。你应该使用结构体指针作为参数，还是使用结构体参数和返回值？每种方法都有其优缺点。

指针参数方法的两个优点是它适用于较旧的 C 实现以及较新的 C 实现，并且速度快；你只需传递一个地址。缺点是你的数据保护较少。被调用函数中的某些操作可能会无意中影响原始结构体中的数据。然而，ANSI C 添加的 const 限定符解决了这个问题。例如，如果你在列表 11.8 的 showinfo() 函数中加入更改结构体任何成员的代码，编译器会将其捕获为错误。

传递结构体作为参数的一个优点是函数使用原始数据的副本，这比使用原始数据更安全。此外，编程风格往往更清晰。假设你定义了以下结构体类型：

```
struct vector {double x; double y;};
```

你想将向量 ans 设置为向量 a 和 b 的和。你可以编写一个结构体传递和返回的函数，使程序看起来像这样：

```
struct vector ans, a, b;
struct vector sum_vect(struct vector, struct vector);
...
ans = sum_vect(a,b);
```

前一个版本对工程师来说看起来比指针版本更自然，指针版本可能看起来像这样：

```
struct vector ans, a, b;
void sum_vect(const struct vector *, const struct vector *, struct vector *);
...
sum_vect(&a, &b, &ans);
```

此外，在指针版本中，用户必须记住和的地址应该是第一个还是最后一个参数。

传递结构体的两个主要缺点是较旧的实现可能无法处理代码，并且浪费时间和空间。特别是在函数只使用结构体的一两个成员时，传递大型结构体尤其浪费。在这种情况下，传递指针或仅将所需成员作为单独参数传递更有意义。

通常，程序员出于效率原因使用结构体指针作为函数参数，在需要时使用 const 来保护数据免受非预期更改。通过值传递结构体通常是针对本身就很小的结构体进行的。

## 结构体中的字符数组还是字符指针

到目前为止的示例都使用字符数组在结构体中存储字符串。你可能想知道是否可以使用指向 char 的指针代替。例如，列表 14.3 有以下声明：

```
#define LEN 20
struct names {
    char first[LEN];
    char last[LEN];
};
```

你能这样做吗？

```
struct pnames {
    char * first;
```

