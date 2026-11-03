
变量 a 的值丢失，你说得对。它的值确实丢失了，但函数返回的地址仍然引用着一块已分配的内存。

练习 20-12：将《清单 20-8》中的代码复制到编辑器中。构建并运行。

![](img/dcc0cd79d4a45cfce24fa49d85442884_338_0.png)

注意 fill_structure() 函数中的 scanf() 语句。记住 -> 是指针的“窥视”记法。要获取地址，你必须在 scanf() 函数中使用 & 为变量加上前缀。

### 编辑链表

由于链表是通过引用内存位置链接在一起的，因此编辑是通过修改这些内存位置来完成的。例如，在图 20-2 中，如果你想从列表中删除第三项，你可以通过将第二项链接到第四项来绕过它。第三项通过此操作被有效地删除（并丢失）。

同样，你可以通过编辑前一个结构中的 next 指针将项目插入列表，如图 20-3 所示。

![](img/dcc0cd79d4a45cfce24fa49d85442884_338_1.png)

更改链表中项目的最佳方式是拥有一个交互式程序，让你查看、添加、插入、删除和编辑各种结构。这样的程序会相当长且复杂，这就是为什么它显示在清单 20-9 中。

![](img/dcc0cd79d4a45cfce24fa49d85442884_338_2.png)

### 清单 20-9：一个交互式链表程序

```c
/* An interactive linked-list program */
/* Dan Gookin, C Programming For Dummies */
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

struct lili {
    int value;
    struct lili *next;
};
struct lili *first;
struct lili *current;

int menu(void);
void add(void);
void show(void);
void delrec(void);
struct lili *create(void);

/* the main function works with input only
   everything else is handled by a function */
int main()
{
    /* initialize variables */
    int choice='\0';
    first=NULL;

    while(choice!='Q')
    {
        choice=menu();
        switch (choice)
        {
            case 'S':
                show();
                break;
            case 'A':
                add();
                break;
            case 'R':
                delrec();
                break;
            case 'Q':
                break;
        }
    }

    return(0);
}

/* output the main menu and collect input */
int menu(void)
{
    int ch;

    printf("Show, A)dd, R)emove, Q)uit: ");
    ch=getchar();
    /* delete excess input */
    while(getchar()!='\n')
        ;
    return(toupper(ch));
}

/* add an item to the end of the linked list */
void add(void)
{
    /* special case for the first item */
    if(first==NULL)
    {
        first=create();
        current=first;
    }
    /* otherwise, find the last item */
    else
    {
        current=first;
        /* find the NULL */
        while(current->next)
            current=current->next;
        current->next=create();
        current=current->next;
    }
    printf("Type a value: ");
    scanf("%d",&current->value);
    current->next=NULL;
    /* delete excess input */
    while(getchar()!='\n')
        ;
}

/* output all structures in the linked list */
void show(void)
{
    int count=1;

    /* is the list empty? */
    if(first==NULL)
    {
        puts("Nothing to show");
        return;
    }
    puts("Showing all records:");
    current=first;
    /* loop until current==NULL */
    while(current)
    {
        printf("Record %d: %d\n", count,current->value);
        current=current->next;
        count++;
    }
}

/* delete a record from the list */
void delrec(void)
{
    /* the previous record must be saved */
    struct lili *previous;
    int r,c;

    /* is the list empty? */
    if(first==NULL)
    {
        puts("No records to remove");
        return;
    }

    puts("Choose a record to remove:");
    /* output the list */
    show();
    printf("Record: ");
    scanf("%d",&r);
    /* delete excess input */
    while(getchar()!='\n')
        ;
    c=1;
    /* reset the list */
    current=first;
    /* initialize the previous pointer */
    previous=NULL;
    while(c!=r)
    {
        previous=current;
        current=current->next;
        c++;
        /* bail on the end of the list */
        if(current==NULL)
        {
            puts("Record not found");
            return;
        }
    }
    /* 'current' holds the record to delete */
    /* is it the first record? */
    if(previous==NULL)
        first=current->next;
    /* otherwise, reset the next reference */
    else
        previous->next=current->next;
    printf("Record %d removed.\n",r);
    /* release memory of the current record */
    free(current);
}

/* build an empty structure & return its address */
struct lili *create(void)
{
    struct lili *a;

    a=(struct lili *)malloc(sizeof(struct lili)*1);
    if(a==NULL)
    {
        puts("Some kind of malloc() error");
        exit(1);
    }

    return(a);
}
```

练习 20-13：如果你有时间，请将清单 20-9 的源代码输入到你的编辑器中。我可以说，亲手输入有助于你更好地理解代码。构建并运行几次以熟悉它。

### 保存链表

链表只存在于内存中。虽然你可以将链表中的所有记录保存到文件中，但在从文件读取信息时，每个结构中的 next 指针成员应被丢弃。原因是因为链表可能不会在同一块内存中布局。

请参阅第 22 章，了解有关文件操作的详细信息——具体来说是随机文件访问的主题。

### 本章内容

- 编程时间函数
- 理解 Unix 纪元
- 获取当前时间
- 显示日期和时间
- 暂停程序执行

## 第 21 章

## 关于时间

是时候编程了！或者换句话说，是时候编程时间了。C 库充满了各种面向时间的函数，让你不仅可以报告当前时间，还可以显示日期和时间。你甚至可以——有意地——暂停程序的执行，前提是你知道正确的函数。

### 现在几点了？

有人知道现在几点了吗？说真的，有人真的知道现在几点了——或者过去几点了吗？

电子设备都有时钟，但这并不使它们成为最好的计时器。事实上，今天大多数小玩意都会通过使用互联网时间服务器不断更新其内部时钟。否则，你的电脑、手机或平板电脑上的时钟永远不会准确。

当你在 C 中编程时间时，你依赖于所使用的设备准确报告日期和时间。这凸显了围绕时间主题及其如何测量的大量术语和技术。

### 了解日历

数字设备通过计算 1 和 0 来跟踪时间。人类喜欢通过计算秒、分钟、小时、天、周、月和年来跟踪时间。已经开发出各种方案来在两者之间工作。

*儒略历*几个世纪以来都很流行。它由 Julius Caesar 开发并用拉丁语编写，这个日历很长时间内运行良好。

不幸的是，老 Julius 没有考虑到随时间累积的一天的小数部分。在 1500 年，教皇 Gregory 开发了 *格里高利历*，它修正了 Caesar 的疏忽。这个日历也是用拉丁语编写的。

计算机科学家在 1950 年代开发了名为 *改进儒略日 (MJD)* 的东西。他们将公元前 4713 年 1 月 1 日设为第 0 天，并对此后的每一天进行编号。小时以一天的小数部分给出。2014 年 1 月 1 日中午是 2456239.5 MJD。

当 Unix 出现时，两件事诞生了：C 语言和 Unix 纪元。在 1970 年 1 月 1 日午夜，Unix 计算机开始计数秒。*Unix 纪元*自那一刻起以 *time_t* 值衡量，它是 *long unsigned int* 的 *typedef*。该数据类型的范围使 Unix 纪元日历有效期至 2038 年 1 月 19 日凌晨 3:14:07，此时计算机突然认为日期又回到了 1901 年 12 月 13 日。那是一个星期五！

大多数 Unix 计算机已经解决了 2038 年问题，因此与 Y2K 危机不同，2038 年 1 月 19 日之后不会发生任何坏事。然而，Unix 纪元仍在使用 C 函数进行时间编程。

### 在 C 中使用时间

C 语言中的时间函数和相关事项保存在 `time.h` 头文件中。在此文件中，你会找到满足程序及时需求的好东西。这些项目包括 `time_t` 数据类型和 `tm` 结构：

|  |  |
| --- | --- |
| `time_t` | `time_t` 数据类型保存 Unix 纪元的值，或自 1970 年 1 月 1 日以来经过的秒数。在大多数系统上，`time_t` 是 long signed int 的 typedef；使用 `%ld` 或 `%lu` 占位符输出此值。 |
| `struct tm` | `tm` 结构保存用于存储时间戳各个部分的定义。它由 `localtime()` 函数填充。参见后面的章节“切片时间字符串”。 |
