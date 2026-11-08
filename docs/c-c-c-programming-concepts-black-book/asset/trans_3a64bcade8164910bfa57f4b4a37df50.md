
在代码清单 5.20 中，我们尝试从文件中读取一整句话。首先，我们以只读模式打开文件，然后使用 `fgets()` 函数从文件中读取一整句话。

前面程序的输出如下：

```
THIS IS HOW WE READ SENTENCE FROM A FILE.
```

在下一节中，我们来学习如何创建文件。

## 创建文件

文件在处理之前需要先创建。文本文件或面向流的文件可以通过两种方式创建。既可以借助某些外部文字处理软件来创建，也可以通过编写某个程序将信息写入数据文件来创建。无格式文件只能借助程序创建。代码清单 5.21 展示了如何创建文件：

**代码清单 5.21：创建文件**

```c
#include<stdio.h>

    int main()
    {
        char ch='A';
        FILE *fp;

        fp = fopen("D:\\create_readme.txt","w");

        if(!fp)
        {
            printf("\n Failed to open the file");
            return 0;
        }

        putc(ch, fp);
        fclose(fp); /* For closing the file pointer */
        getch();

        return 0;
    }
```

前面的程序以写模式创建一个数据文件。接下来，我们来学习如何向文件写入内容。

## 向文件写入内容

在以写模式打开文件（即通过 `fopen()` 函数中的“w”来完成）之后，用户可以使用 `fputc()` 和 `fputs()` 等函数将信息写入文件。`fputc()` 函数允许用户向文件中写入字符；而 `fputs()` 函数允许用户向文件进行多行写入。代码清单 5.22 展示了如何使用 `fputc()` 函数向文件写入内容：

**代码清单 5.22：向文件写入内容**

```c
#include<stdio.h>

    int main()
    {
        char character;
        FILE *fp,*fd;

        fp = fopen("D:\\readme.txt", "r");
        fd = fopen("D:\\readme_new.txt", "w");

        if(!fp)
```

前面的代码将信息写入文件，但采用了一种优化的方式。代码不是逐个字符复制，而是一次复制 100 个字符的缓冲区，并将其写入目标文件。

现在，我们来学习如何向文件添加记录。

## 向文件添加记录

数据文件通常用于存储记录，而记录是一组不同类型的信息。要将此类记录写入数据文件，我们可以使用 `fprintf()` 函数。此外，要从数据文件中获取记录，我们可以使用 `fscanf()` 函数。代码清单 5.24 展示了 `fprintf()` 和 `fscanf()` 函数的工作方式：

**代码清单 5.24：** 添加和获取记录

```c
#include<stdio.h>

struct student
{
        char name[20];
        int class;
        int age;
};

int main()
{
        struct student stu;
        FILE *fp;
        int choice;

        fp = fopen("D:\\studentRecords.dat","a");

        do
        {
                printf("\n 1. Add records to a file ");
                printf("\n 2. Exit");
                printf("\n Enter your choice => ");
                scanf("%d",&choice);

                switch(choice)
                {
                        case 1:
                                printf("\n Enter Name Class Age =>");
                                scanf("%s %d",&stu.name,&stu.class,&stu.age);
                                fprintf(fp,"%s %d %d",stu.name,stu.class,stu.age);
                                break;
                        case 2:
                                break;
                        default:break;
                }
        }while(choice != 2);

        fclose(fp);

        fp = fopen("D:\\studentRecords.dat","r");

        printf("\n Records Inserted are ");

        while(fscanf(fp,"%s %d %d",&stu.name,&stu.class,&stu.age) != EOF)
        {
                printf("\n %s %d %d ",stu.name,stu.class,stu.age);
        }
        getch();
        return 0;
}
```

在前面的程序中，我们使用 `scanf()` 函数将数据写入 student 结构体。在填充结构体变量 stu 之后，我们将信息写回数据文件。在将信息写回数据文件时，我们使用 `fprintf()` 函数，该函数将文件指针作为参数。与 `printf()` 类似，`fprintf()` 也允许以多种方式格式化数据。在显示信息时，我们使用 `fscanf()`，它的工作方式与 `scanf()` 相同。唯一的区别是，它将文件指针作为参数，并从该文件读取信息。

前面程序的输出如下：

```
1. Add records to a file
2. Exit
Enter your choice -> 1

Enter Name Class Age ->JOHN 9 14

1. Add records to a file
2. Exit
Enter your choice -> 1

Enter Name Class Age ->RICHARD 6 11

1. Add records to a file
2. Exit
Enter your choice -> RON 12 16

Enter Name Class Age ->
1. Add records to a file
2. Exit
Enter your choice -> 2

Records Inserted are
JOHN 9 14
RICHARD 6 11
RON 12 16
```

现在，我们来详细了解二进制文件。

## 二进制文件

二进制文件是字节的集合。二进制文件的一个例子是音频文件，其中包含不可打印的字符。文本文件与二进制文件的区别在于两者检测文件结束的方式。对于文本文件，ASCII 值为 26 的特殊字符被视为文件结束字符。如果遇到该字符，则意味着已到达文件末尾。然而，二进制文件中不存在这样的特殊字符。文件结束由文件大小决定。二进制文件可能被用于存储数字。在这种情况下，数字 26 可能表示文件结束，并导致程序提前终止。在文本文件中，换行字符会被转换为回车换行组合（\r\n），然后写入文件。然而，如果以二进制模式打开文件，则不会发生这种转换。

代码清单 5.25 展示了如何从二进制文件读取以及向二进制文件写入：

**代码清单 5.25：处理二进制文件**

```c
#include<stdio.h>

struct student
{
    char name[20];
    int class;
    int age;
};

int main()
{
    struct student stu;
    FILE *fp;
    int choice;

    fp = fopen("D:\\studentRecords.dat","wb");

    do
    {
        printf("\n 1. Add records to a file ");
        printf("\n 2. Exit");
        printf("\n Enter your choice -> ");
        scanf("%d",&choice);

        switch(choice)
        {
            case 1:
                printf("\n Enter Name Class Age ->");
                scanf("%s %d %d",&stu.name,&stu.class,&stu.age);
                fwrite(&stu, sizeof(stu), 1, fp);
                break;
            case 2:
                break;
            default:break;
        }
    }while(choice != 2);

    fclose(fp);

    fp = fopen("D:\\studentRecords.dat","rb");

    printf("\n Records inserted are ");

    while(fread(&stu, sizeof(stu), 1, fp))
    {
        printf("\n %s %d %d ",stu.name,stu.class,stu.age);
    }

    getch();
    return 0;
}
```

在前面的程序中，我们以 `wb` 模式打开文件，这表明我们正在处理二进制文件。

前面程序的输出如下：

```
1. Add records to a file
2. Exit
Enter your choice -> 1

Enter Name Class Age ->MICHELLE 5 12

1. Add records to a file
2. Exit
Enter your choice -> 1

Enter Name Class Age ->CHARLIE 8 16

1. Add records to a file
2. Exit
Enter your choice -> 2

Records Inserted are
MICHELLE 5 12
CHARLIE 8 16
```

在处理二进制文件时，我们没有使用 `fscanf()` 和 `fprintf()`，而是使用了两个新函数：`fread()` 和 `fwrite()`。

`fread()` 函数返回读取到的项数。`fread()` 的签名如下：

```c
size_t fread(void *buffer, size_t num_bytes, size_t count, FILE *fp);
```

在前面的签名中，`buffer` 是指向内存区域的指针，该内存区域将接收来自文件的数据。`count` 的值决定要读取多少项，其中每一项的长度为 `num_bytes` 字节。如果已到达文件末尾或发生错误，该返回值可能小于 `count`。

`fwrite()` 函数返回成功写入磁盘的项数。`fwrite()` 的签名如下：

```c
size_t fwrite(const void *buffer, size_t num_bytes, size_t count, FILE *fp);
```

其参数及其用法与 `fread()` 相同。

在前面的程序中，我们已经从二进制文件读取并写入信息。然而，数据库应用涉及更复杂的任务，例如在二进制文件中更新、删除和添加记录。代码清单 5.26 展示了使用二进制文件管理数据库的代码。

**代码清单 5.26：使用二进制文件管理数据库**

```c
#include<stdio.h>

struct student
{
        char name[20];
        int class;
        int age;
};

int main()
{
        struct student stu;
        FILE *fp,*fd;
        int choice;
```
