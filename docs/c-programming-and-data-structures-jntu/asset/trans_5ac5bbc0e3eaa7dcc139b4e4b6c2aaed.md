
**fscanf(f2, "%s %d", item, &quantity);**

与 scanf 类似，fscanf 也返回成功读取的项目数。当到达文件末尾时，它返回值为 EOF。

### 示例 13.2

写一个程序打开名为 INVENTORY 的文件并在其中存储以下数据：

| 项目名称 | 编号 | 价格 | 数量 |
|-----------|--------|-------|----------|
| AAA-1     | 111    | 17.50 | 115      |
| BBB-2     | 125    | 36.00 | 75       |
| C-3       | 247    | 31.75 | 104      |

扩展程序以从文件 INVENTORY 读取此数据并显示包含每项价值的库存表。

程序在图 13.4 中给出。文件名 INVENTORY 通过键盘提供。数据使用函数 fscanf 从文件 stdin 读取，stdin 指终端，然后写入由文件指针 fp 指向的文件。请记住，文件指针 fp 指向文件 INVENTORY。

关闭文件 INVENTORY 后，它会再次以读取方式打开。文件中的数据连同项目价值一起写入文件 stdout，stdout 指屏幕。在从文件读取时，应注意使用与写入文件内容时相同的格式规范。

```
Program
/* ************************************************************ */
/*   HANDLING OF FILES WITH MIXED DATA TYPES                   */
/*          (scanf and printf)                                 */
/* ************************************************************ */
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

    printf("Input inventory data\n");
    printf("Item name Number Price Quantity\n");
    for(i = 1; i <=3; i++)
    {
        fscanf(stdin, "%s %d %f %d", item, &number, &price, &quantity);
        fprintf(fp, "%s %d %2f %d", item, number, price, quantity);
    }
    fclose(fp);
}
```
```
fprintf(stdout, "\n");
fp = fopen(filename, "r");
printf("Item name Number Price Quantity Value\n");
for(i = 1; i<=3; i++)
{
    fscanf(fp, "%s %d %f %d", item, &number, &price, &quantity);
    value = price * quantity;
    fprintf(stdout, "%-8s %7d %8.2f %8d %11.2f\n", item, number, price, quantity, value);
}
fclose(fp);
}
```

输出
输入文件名
INVENTORY
输入库存数据

| 项目名称 | 编号 | 价格 | 数量 |
|---|---|---|---|
| AAA-1 | 111 | 17.50 | 115 |
| BBB-2 | 125 | 36.00 | 75 |
| C-3 | 247 | 31.75 | 104 |

| 项目名称 | 编号 | 价格 | 数量 | 价值 |
|---|---|---|---|---|
| AAA-1 | 111 | 17.50 | 115 | 2012.50 |
| BBB-2 | 125 | 36.00 | 75 | 2700.00 |
| C-3 | 247 | 31.75 | 104 | 3302.00 |

图 13.4 混合数据类型上的操作

## 13.5 I/O 操作期间的错误处理

在文件上的 I/O 操作期间可能发生错误。典型的错误情况包括：

- 1. 尝试读取超出文件结束标记。
- 2. 设备溢出。
- 3. 尝试使用未打开的文件。
- 4. 尝试对文件执行操作，而文件是为另一种类型的操作而打开的。
- 5. 使用无效文件名打开文件。
- 6. 尝试写入写保护文件。

如果我们未能检查此类读写错误，程序在发生错误时可能会异常行为。未检查的错误可能导致程序过早终止或输出不正确。

幸运的是，我们有两个状态查询库函数 feof 和 ferror，可以帮助我们检测文件中的 I/O 错误。

feof 函数可用于测试文件结束条件。它接受一个 FILE 指针作为唯一参数，如果已读取指定文件的所有数据，则返回非零整数值，否则返回零。如果 fp 是刚刚打开用于读取的文件的指针，则语句

```
if(feof(fp))
    printf("End of data.\n");
```

在达到文件结束条件时将显示消息 "End of data."。

ferror 函数报告所指示文件的状态。它也接受 FILE 指针作为参数，如果在处理过程中到该点为止检测到错误，则返回非零整数。否则返回零。语句

```
if(ferror(fp) != 0)
    printf("An error has occurred.\n");
```

如果读取不成功，将打印错误消息。

我们知道，每当使用 fopen 函数打开文件时，都会返回一个文件指针。如果由于某种原因无法打开文件，则函数返回空指针。此功能可用于测试文件是否已打开。示例：

```
if(fp == NULL)
    printf("File could not be opened.\n");
```

### 示例 13.3

编写一个程序来说明文件操作中的错误处理。

图 13.5 所示的程序说明了空指针测试和 feof 函数的使用。当我们输入文件名 TETS 时，函数调用

```
fopen("TETS", "r");
```

返回空指针，因为文件 TETS 不存在，因此打印出消息 "Cannot open the file"。

类似地，当整个数据已被读取时，调用 feof(fp2) 返回非零整数，因此程序打印消息 "Ran out of data" 并终止进一步读取。

```
/* **************************************************************************/
/* *                                                                      */
/* *                        ERROR HANDLING IN FILE OPERATIONS             */
/* *                                                                      */
/* **************************************************************************/
#include <stdio.h>
main()
{
    char filename[20];
    FILE *fp1,*fp2;
    int i,number;
    fp1 = fopen("TEST","w");
    for(i=0;i<=100;i+=10)
        putw(i,fp1);
    fclose(fp1);
    printf("\n\nInput filename\n");
open_file:
    scanf("%s",filename);
    if((fp2 = fopen(filename,"r")) == NULL)
    {
        printf("Cannot open the file.\n");
```
```
printf("Type filename again.\n\n");
goto open_file;
}
else
for(i = 1; i <=20; i++)
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

输出
输入文件名
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

图 13.5 错误处理的说明

## 13.6 文件的随机访问

到目前为止，我们讨论了用于顺序读取和写入数据的有用文件函数。然而，有时我们只对访问文件的特定部分感兴趣，而不想读取其他部分。这可以通过 I/O 库中提供的 fseek、ftell 和 rewind 函数来实现。

ftell 接受一个文件指针并返回一个类型为 long 的数字，对应于当前位置。此函数在保存文件当前位置方面很有用，该位置可在程序后面使用。其形式如下：

```
n = ftell(fp);
```

n 将给出当前位置的相对偏移量（以字节为单位）。这意味着已经读取（或写入）了 n 个字节。

rewind 接受一个文件指针并将位置重置为文件的开头。例如，语句

```
rewind(fp);
 n = ftell(fp);
```

将把 0 分配给 n，因为 rewind 已将文件位置设置为文件的开头。请记住，文件中的第一个字节编号为 0，第二个为 1，以此类推。此函数帮助我们在不必关闭和打开文件的情况下多次读取文件。请记住，每当打开文件进行读取或写入时，都会隐式执行 rewind。

fseek 函数用于将文件位置移动到文件内的所需位置。其形式如下：

```
fseek(file ptr, offset, position);
```

file ptr 是有关文件的指针，offset 是类型为 long 的数字或变量，position 是整数。offset 指定从 position 指定的位置移动的位置数（字节）。position 可以取以下三个值之一：

| 值 | 含义 |
|---|---|
| 0 | 文件开头 |
| 1 | 当前位置 |
| 2 | 文件末尾 |

offset 可能是正数，表示向前移动，或负数，表示向后移动。以下示例说明了 fseek 函数的操作：

| 语句 | 含义 |
|---|---|
| fseek(fp,0L,0); | 转到开头。（类似于 rewind） |
| fseek(fp,0L,1); | 保持在当前位置。（很少使用） |
| fseek(fp,0L,2); | 转到文件末尾，超出文件的最后一个字符。 |
| fseek(fp,m,0); | 移动到文件中的第 (m+1) 个字节。 |
| fseek(fp,m,1); | 向前移动 m 个字节。 |
| fseek(fp,-m,1); | 从当前位置向后移动 m 个字节。 |
| fseek(fp,-m,2); | 从末尾向后移动 m 个字节。（将文件定位到从末尾算起的第 m 个字符。） |

当操作成功时，fseek 返回零。如果我们尝试将文件指针移动到文件边界之外，则会发生错误，fseek 返回 −1（负一）。在继续之前检查是否发生错误是良好的做法。

### 示例 13.4

编写一个程序使用 ftell 和 fseek 函数。采用 ftell 和 fseek 函数的程序显示在图 13.6 中。我们创建了一个名为 RANDOM 的文件，其内容如下：
