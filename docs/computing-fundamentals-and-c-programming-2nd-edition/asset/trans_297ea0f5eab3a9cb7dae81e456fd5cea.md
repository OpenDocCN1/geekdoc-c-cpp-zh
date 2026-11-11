
```c
int number, i;

printf("Contents of DATA file\n\n");
f1 = fopen("DATA", "w");        /* Create DATA file */
for(i = 1; i <= 30; i++)
{
    scanf("%d", &number);
    if(number == -1) break;
    putw(number, f1);
}
fclose(f1);

f1 = fopen("DATA", "r");
f2 = fopen("ODD", "w");
f3 = fopen("EVEN", "w");

/* Read from DATA file */
while((number = getw(f1)) != EOF)
{
    if(number %2 == 0)
        putw(number, f3);   /* Write to EVEN file */
    else
        putw(number, f2);   /* Write to ODD file */
}
fclose(f1);
fclose(f2);
fclose(f3);

f2 = fopen("ODD", "r");
f3 = fopen("EVEN", "r");

printf("\n\nContents of ODD file\n\n");
while((number = getw(f2)) != EOF)
    printf("%4d", number);

printf("\n\nContents of EVEN file\n\n");
while((number = getw(f3)) != EOF)
    printf("%4d", number);

fclose(f2);
fclose(f3);

}
```

该程序如图14.3所示。文件名INVENTORY通过键盘输入。数据使用**fscanf**函数从文件**stdin**读取，**stdin**指的是终端，然后将数据写入文件指针**fp**所指的文件。请记住，文件指针**fp**指向文件INVENTORY。

关闭文件INVENTORY后，再次以读取方式重新打开它。文件中的数据以及项目值被写入文件**stdout**，**stdout**指的是屏幕。从文件读取时，应注意使用与文件内容写入时相同的格式说明。

程序

```c
#include <stdio.h>

main()
{
    FILE *fp;
    int number, quantity, i;
    float price, value;
    char item[10], filename[10];

    printf("Input file name\n");
    scanf("%s", filename);
    fp = fopen(filename, "w");
    printf("Input inventory data\n\n");
    printf("Item name Number Price Quantity\n");
    for(i = 1; i <= 3; i++)
    {
        fscanf(stdin, "%s %d %f %d",
            item, &number, &price, &quantity);
        fprintf(fp, "%s %d %.2f %d",
            item, number, price, quantity);
    }
    fclose(fp);
    fprintf(stdout, "\n\n");

    fp = fopen(filename, "r");

    printf("Item name Number Price Quantity Value\n");
    for(i = 1; i <= 3; i++)
    {
        fscanf(fp, "%s %d %f %d", item, &number, &price, &quantity);
        value = price * quantity;
        fprintf(stdout, "%-8s %7d %8.2f %8d %11.2f\n",
            item, number, price, quantity, value);
    }
    fclose(fp);
}
```

**输出**

```
Input file name
INVENTORY
Input inventory data
```

| 项目名称 | 编号 | 价格 | 数量 |
| --- | --- | --- | --- |
| AAA-1 | 111 | 17.50 | 115 |
| B8B-2 | 125 | 36.00 | 75 |
| C-3 | 247 | 31.75 | 104 |

| 项目名称 | 编号 | 价格 | 数量 | 价值 |
| --- | --- | --- | --- | --- |
| AAA-1 | 111 | 17.50 | 115 | 2012.50 |
| B8B-2 | 125 | 36.00 | 75 | 2700.00 |
| C-3 | 247 | 31.75 | 104 | 3302.00 |

**图14.3** *对混合数据类型的操作*

## 14.5 I/O操作中的错误处理    LO 14.3

文件I/O操作期间可能会发生错误。典型的错误情况包括以下内容：

- 1. 试图读取超过文件结束标记的内容。
- 2. 设备溢出。
- 3. 试图使用尚未打开的文件。
- 4. 当文件以另一种操作类型打开时，尝试对该文件执行操作。
- 5. 使用无效文件名打开文件。
- 6. 尝试写入受写保护的文件。

如果我们未能检查此类读写错误，程序在发生错误时可能会行为异常。未检查的错误可能导致程序提前终止或输出不正确。幸运的是，我们有两个状态查询库函数：**feof** 和 **ferror**，它们可以帮助我们检测文件中的I/O错误。

**feof** 函数可用于测试文件结束条件。它仅接受一个**FILE**指针作为参数，如果指定文件中的所有数据均已读取，则返回非零整数值，否则返回零。如果**fp**是指向刚打开用于读取的文件的指针，则以下语句

```c
if(feof(fp))
    printf("End of data.\n");
```

将在到达文件结束条件时显示消息“End of data.”。

**ferror** 函数报告所指示文件的状态。它也以**FILE**指针作为参数，如果在处理过程中检测到错误，则返回非零整数，否则返回零。以下语句

```c
if (ferror(fp) != 0)
    printf("An error has occurred.\n");
```

如果读取不成功，将打印错误消息。

我们知道，每当使用 `fopen` 函数打开文件时，都会返回一个文件指针。如果由于某种原因无法打开文件，则该函数返回一个NULL指针。此功能可用于测试文件是否已打开。例如：

```c
if (fp == NULL)
    printf("File could not be opened.\n");
```

### 例题14.4

编写一个程序来说明文件操作中的错误处理。

图14.4所示的程序说明了NULL指针测试和`feof`函数的用法。当我们输入文件名TETS时，函数调用`fopen("TETS", "r");`返回一个NULL指针，因为文件TETS不存在，因此打印出消息“Cannot open the file”。

类似地，当所有数据都被读取后，调用`feof(fp2)`返回非零整数，因此程序打印消息“Ran out of data”并终止进一步读取。

**程序**

```c
#include <stdio.h>

main()
{
        char *filename;
        FILE *fp1, *fp2;
        int i, number;

        fp1 = fopen("TEST", "w");
        for(i = 10; i <= 100; i += 10)
                putw(i, fp1);

        fclose(fp1);

        printf("\nInput filename\n");

open_file:
        scanf("%s", filename);

        if((fp2 = fopen(filename,"r")) == NULL)
        {
            printf("Cannot open the file.\n");
            printf("Type filename again.\n\n");
            goto open_file;
        }
        else

        for(i = 1; i <= 20; i++)
        { number = getw(fp2);
          if(feof(fp2))
          {
            printf("\nRan out of data.\n");
            break;
          }
          else
            printf("%d\n", number);
        }

        fclose(fp2);

}
```

**输出**

```
Input filename
TETS
Cannot open the file.
Type filename again.

TEST
10
20
30
40
50
60
70
80
90
100

Ran out of data.
```

**图14.4** *文件操作中错误处理的说明*

## 14.6 文件的随机访问

LO 14.4

到目前为止，我们已经讨论了用于顺序读写数据的文件函数。然而，有时我们只希望访问文件的特定部分，而不读取其他部分。这可以借助I/O库中的**fseek**、**ftell**和**rewind**函数来实现。

**ftell**接受一个文件指针，并返回一个**long**类型的数字，该数字对应于当前位置。此函数可用于保存文件的当前位置，以便在程序中稍后使用。其形式如下：

```c
n = ftell(fp);
```

**n**将给出当前位置的相对偏移量（以字节为单位）。这意味着n个字节已被读取（或写入）。

**rewind**接受一个文件指针，并将位置重置到文件开头。例如，语句

```c
rewind(fp);
n = ftell(fp);
```

因为**rewind**已将文件位置设置为文件开头，所以会将**0**赋给**n**。请记住，文件中的第一个字节编号为0，第二个为1，依此类推。此函数帮助我们可以多次读取文件，而无需关闭和重新打开文件。请记住，每当为读取或写入而打开文件时，都会隐式地执行**rewind**。

**fseek**函数用于将文件位置移动到文件中的所需位置。其形式如下：

```c
fseek(file_ptr, offset, position);
```

**file_ptr**是指向相关文件的指针，**offset**是long类型的数字或变量，**position**是整数。**offset**指定从**position**指定的位置移动的字节数。**position**可以取以下三个值之一：

| 值 | 含义 |
| --- | --- |
| 0 | 文件开头 |
| 1 | 当前位置 |
| 2 | 文件末尾 |

偏移量可以是正数，表示向前移动，也可以是负数，表示向后移动。

表14.2中的示例说明了**fseek**函数的操作：

**表14.2** fseek函数的操作

| 语句 | 含义 |
| --- | --- |
| fseek(fp,0L,0); | 转到文件开头。（类似于rewind） |
| fseek(fp,0L,1); | 停留在当前位置。（很少使用） |
| fseek(fp,0L,2); | 转到文件末尾，越过文件的最后一个字符。 |
| fseek(fp,m,0); | 移动到文件中的第(m+1)个字节。 |
| fseek(fp,m,1); | 向前移动m个字节。 |
| fseek(fp,-m,1); | 从当前位置向后移动m个字节。 |
| fseek(fp,-m,2); | 从末尾向后移动m个字节。（将文件定位到距末尾第m个字符处。） |

