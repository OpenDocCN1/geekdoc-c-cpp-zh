

### 从文件读取一行的程序

```c
#include<stdio.h>
void main()
{
    FILE *fp;
    char str[15];
    char *ps;
    fp = fopen("input.dat", "r");
    ps = fgets(str, 10, fp);
    if(ps != NULL)
    {
        puts(str);
    }
    else
        printf("unsuccessful reading");
}
```

### fputs 的语法：

fputs(str, fp);

str 是要写入由 fp 指向的文件的字符串。它不会自动向文件写入新行。只有当换行符存在时才会写入。

### 示例：

```c
void main()
{
    FILE *fp;
    char str[15];
    char *ps;
    printf("enter the string\n");
    gets(str);
    fp = fopen("file.txt", "w");
    fputs(str, fp);
    fclose(fp);
}
```

### fgetc 和 fputc()：

fgetc() 用于从文件中读取一个字符。

fputc() 用于向文件写入一个字符。

### 语法：

fputc(c, fp1);

c 是要写入文件的字符。

fp1 是由 fopen 返回的文件指针。

c = fgetc(fp1);

从 fp1 指向的文件返回一个字符。

### 示例：

将一个字符从一个文件复制到另一个文件的程序。

```c
void main()
{
    FILE *fp1, *fp2;
    char c;
    fp1 = fopen("f1.txt", "r");
    fp2 = fopen("f2.txt", "w");
    c = fgetc(fp1);
    fputc(c, fp2);
}
```

### 示例问题

| 问题 | RBT 等级 | CO's |
|---|---|---|
| 描述结构体。解释如何声明和初始化结构体。 | L1 | CO4, CO5 |
| 描述文件。解释文件的不同模式。 | L1 | CO4, CO5 |
| 这段 C 代码的输出是什么？<br><pre>#include &lt;stdio.h&gt;<br>struct student<br>{<br>    char *name;<br>};<br><br>void main()<br>{<br>    struct student s, m;<br>    s.name = "st";<br>    m = s;<br>    printf("%s%s", s.name, m.name);<br>}</pre> | L2 | CO4, CO5 |
| 解释结构体实现中非法的操作。 | L2 | CO4, CO5 |
| 举例说明如何定义、声明和初始化结构体。 | L3 | CO4, CO5 |
| 举例说明如何访问结构体成员。 | L3 | CO4, CO5 |
| 用语法举例说明如何打开和关闭文件。 | L3 | CO4, CO5 |
| 文件的特征是什么？ | L4 | CO4, CO5 |
| 结构体的特征是什么？ | L4 | CO4, CO5 |
| 跟踪以下代码并解释输出是什么。<br><pre>#include &lt;stdio.h&gt;<br>struct<br>{<br>    int i;<br>    float ft;<br>} decl;<br>int main()<br>{<br>    decl.i = 4;<br>    decl.ft = 7.96623;<br>    printf("%d %.2f", decl.i, decl.ft);<br>    return 0;<br>}</pre> | L5 | CO4, CO5 |
| 结构体、联合体和枚举之间有什么相似之处？ | L5 | CO4, CO5 |
| 编写一个 C 程序，在结构体数组中搜索姓名。 | L6 | CO4, CO5 |
| 编写一个 C 程序，从两个不同的文件读取学生姓名和 USN，并写入另一个文件。 | L6 | CO4, CO5 |
| 编写一个 C 程序，从键盘读取 n 个数字并写入文件。 | L6 | CO4, CO5 |
| 编写一个 C 程序，将一个文件的内容复制到另一个文件。 | L6 | CO4, CO5 |
| 编写一个程序，使用结构体存储学生的信息（姓名、学号和成绩）。 | L6 | CO4, CO5 |
| 编写一个 C 程序，使用 fwrite() 将一个结构体数组的所有成员写入文件。从文件中读取该数组并显示在屏幕上。 | L6 | CO4, CO5 |
| 编写一个 C 程序，从用户处读取 n 个学生的姓名和成绩，并将它们存储在文件中。如果文件已存在，则追加这 n 个学生的信息。 | L6 | CO4, CO5 |
| 编写一个 C 程序，使用结构体计算两个时间段之间的差值。 | L6 | CO4, CO5 |

### 模块 5：

### 5.1 C 语言中的数据结构

**数据结构**用于以有组织的形式在计算机中存储数据。在 C 语言中，不同类型的数据结构有：数组、栈、队列、链表、树。

- **数组：** 数组是相同数据类型的集合，你可以不按任何顺序在数组中插入和删除元素。
- **栈：** 栈基于后进先出（LIFO）原则工作。最后进入的元素最先移除。
- **队列：** 队列基于先进先出（FIFO）原则工作。最先进入的元素最先移除。
- **链表：** 链表是节点的集合，你可以按任何顺序插入和删除数据。
- **树：** 以非线性形式存储数据，有一个根节点和子节点。

### 5.1.1 数据结构中的数组

**数组**是在单个变量中存储相同数据类型值的集合。数组是 C 语言中的一种派生数据类型，由 C 语言的基本数据类型构造而成。

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_134_0.png)

### 在数组的特定位置插入元素

```c
#include<stdio.h>
#include<conio.h>

void main()
{
    int i, a[5], no, pos;
    clrscr();
    printf("Enter element in array: ");
    for(i = 0; i < 5; i++)
    {
        scanf("%d", &a[i]);
    }
    printf("\nStored element in array: ");
    for(i = 0; i < 5; i++)
    {
        printf(" %d", a[i]);
    }
    printf("\nEnter position for enter element: ");
    scanf("%d", &pos);
    if(pos > 5)
    {
        printf("\nThis is out of range");
    }
    else
    {
        printf("\nEnter new element: ");
        scanf("%d", &no);
        --pos;
        for(i = 5; i >= pos; i--)
        {
            a[i + 1] = a[i];
        }
        a[pos] = no;
        printf("\nStored data in array: ");
        for(i = 0; i < 6; i++)
        {
            printf(" %d", a[i]);
        }
    }
    getch();
}
```

### 输出

```text
Enter elements in array: 4
4
2
5
7
Stored data in array: 4 4 2 5 7
Enter position for enter element: 2
Enter new element: 8
Stored data in array: 4 8 4 2 5 7
```

### 删除数组特定位置的元素

```c
#include <stdio.h>
void main()
{
    int vectorx[10];
    int i, n, pos, element, found = 0;

    printf("Enter how many elements\n");
    scanf("%d", &n);
    printf("Enter the elements\n");

    for(i = 0; i < n; i++)
    {
        scanf("%d", &vectorx[i]);
    }

    printf("Input array elements are\n");
    for(i = 0; i < n; i++)
    {
        printf("%d\n", vectorx[i]);
    }

    printf("Enter the element to be deleted\n");
    scanf("%d", &element);

    for(i = 0; i < n; i++)
    {
        if(vectorx[i] == element)
        {
            found = 1;
            pos = i;
            break;
        }
    }

    if(found == 1)
    {
        for(i = pos; i < n - 1; i++)
        {
            vectorx[i] = vectorx[i + 1];
        }

        printf("The resultant vector is \n");
        for(i = 0; i < n - 1; i++)
        {
            printf("%d\n", vectorx[i]);
        }
    }
    else
        printf("Element %d is not found in the vector\n", element);
}
```

### 5.1.2 C 语言中的队列

队列按照**先进先出（FIFO）**原则工作，这意味着最早进入的元素最先移除。队列有前后两端，即队首和队尾，从队首可以插入元素，从队尾可以删除元素。

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_139_0.png)

### 队列的现实示例

队列的一个常见示例是电影院售票柜台，排在售票窗口前的第一个人先取票然后离开队伍，新来的人总是排在队伍的末尾。

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_139_1.png)

队列的现实示例：图书馆柜台

### 单车道单向公路：第一辆车先行

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_140_0.png)

售票柜台：第一个人先取票，然后先出去。

### 队列的其他一些现实示例

- 操作系统中的进程队列。
- 任何服务点（如售票等）的人群队列。
- 数据通信中的数据包队列。
- 等待着陆指令的飞机队列。

### 队列数据结构在 C 语言中的应用

队列用于任何需要对某些实体高效维持先进先出顺序的情况。在运输和运筹学中，各种实体被存储并保留以待后续处理，即队列起到缓冲区的作用。

在多任务操作系统中，CPU 无法同时运行所有任务，因此任务必须分批处理，然后按照某种策略进行调度。在这种情况下，队列可能也是一个合适的选择。

### 队列的操作

可以在队列上执行的基本操作有：

- 在队列中插入一个元素。
- 从队列中删除一个元素。

### 在队列中插入一个元素

在队列中，从队尾插入任何元素。如果在队列中插入新元素，队尾（Rear）的值将增加 1。

![](img/bb6d48ce0279cc8c245e23e6b7e31d4d_141_0.png)

### 在队列中插入元素

```c
void insert()
{
    int item;
    printf("Element : ");
    scanf("%d", &item);
    if(front == (rear + 1) % 3)
    {
        printf("Queue is Full");
        return;
    }
    if(front == -1)
    {
        rear = front = 0;
    }
    else
    {
        rear = (rear + 1) % 3;
    }
    cque.cqueue[rear] = item;
}
```

