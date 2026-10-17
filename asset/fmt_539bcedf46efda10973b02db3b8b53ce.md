
```c
/* Program to illustrate the functions fprintf and fscanf */
#include <stdio.h>

/* Beginning of main function */
main()
{
    FILE *fp_item;
    char c_itemname[20], c_ans;
    int i_itemqty, i_ctr = 0;
    float f_itemrate, f_amount = 0;

    fp_item = fopen("item", "w"); /* Opening a file for writing */
    if (fp_item == NULL)
    {
        printf("Error in opening a file\n");
        exit(1);
    }
    else
    {
        do
        {
            i_ctr = i_ctr + 1;
            printf("\nEnter record number %d: ", i_ctr);
            printf("\nEnter item name, item rate and item quantity: ");
            scanf("%s %f %d", c_itemname, &f_itemrate, &i_itemqty);
            /* writing into file */
            fprintf(fp_item, "%s %f %d\n", c_itemname, f_itemrate, i_itemqty);
            printf("\nWould you like to add another record yes(y)/No(n): ");
            scanf(" %c", &c_ans);
        } while ((c_ans == 'y') || (c_ans == 'Y'));
        fclose(fp_item);
    }

    fp_item = fopen("item", "r");
    if (fp_item == NULL)
    {
        printf("Error in opening a file\n");
        exit(1);
    }
    else
    {
        printf("\nThe records entered in file are:\n\n");
        while ((fscanf(fp_item, "%s %f %d", c_itemname, &f_itemrate, &i_itemqty)) != EOF)
        {
            printf("%-10s %5.2f %5d\n", c_itemname, f_itemrate, i_itemqty);
            f_amount = f_amount + f_itemrate * i_itemqty;
        }
        printf("Total amount to be paid is %.2f Rs.\n", f_amount);
    }
    fclose(fp_item);
    return;
}
/* End of function main */
```

### 13.10 二进制文件中的输入/输出

到目前为止，我们讨论的是处理文本文件的程序。如前所述，与文本文件相比，处理二进制文件效率更高。当存储在文件中的数据是记录类型时，通常首选二进制文件。要将内容写入二进制文件，可以使用 `fwrite` 函数。函数 `fwrite` 的语法如下：

```c
fwrite(变量地址, 变量数据类型的大小, 此类变量的数量, 文件指针);
```

函数 `fwrite` 接受四个参数。第一个参数是要写入磁盘的变量的地址。第二个参数是以字节为单位的变量大小。可以使用 `sizeof` 运算符来计算变量占用的字节数。第三个参数是要一次性写入文件中的此类变量的数量。当需要转储变量集合（例如数组）时，函数 `fwrite` 的这个参数非常有用。数据可以组织为结构体，并且整个结构体数组可以转储到文件中。这导致一次在文件中写入多条记录。最后一个参数是指向存储数据的目标文件的文件指针。

要从二进制文件中读取内容，可以使用 `fread` 函数。函数 `fread` 的语法如下：

```c
fread(变量地址, 变量数据类型的大小, 此类变量的数量, 文件指针);
```

函数 `fread` 的格式与函数 `fwrite` 的格式非常相似。它也接受四个参数。第一个参数是用于存储从文件读取的数据的变量的地址。第二个参数是第一个参数中指定的变量的数据类型的大小。第三个参数是要一次性从文件中读取的此类变量的数量。最后一个参数是指向要读取数据源的文件的文件指针。程序 7 展示了在二进制文件中使用 `fread` 和 `fwrite` 函数的方法：

#### 程序 7

```c
/* 演示使用 fread 和 fwrite 函数的程序 */

#include<stdio.h>

/* main 函数开始 */
main()
{
    FILE *fp_item;

    struct item
    {
        int i_itemno;
        char c_itemname[20];
        int i_itemqty;
        float f_itemrate;
    };

    item;
    int i_ctr=0;
    char c_temp,c_ans;
    fp_item=fopen("temp","wb"); /*打开文件用于写入*/
    if(fp_item==NULL)
        printf("打开文件时出错\n");
    else
    {
        do
        {
            items.i_itemno=++i_ctr;
            printf("\n ************输入第 %d 条记录:*********** ",
                   i_ctr);
            printf("\n请输入物品名称、物品单价和物品数量: ");
            scanf("%s %f %d",&items.c_itemname,&items.f_itemrate,&items.i_itemqty);
            c_temp=getchar();

            /* 写入文件 */
            fwrite(&items,sizeof(items),1,fp_item);
            printf("\n是否想添加另一条记录 是(y)/否(n): ");
            scanf("%c",&c_ans);
        }while (c_ans=='y' || c_ans == 'Y');
        fclose(fp_item);
    }

    fp_item=fopen("itemb","rb");

    if (fp_item==NULL)
        printf("打开文件时出错\n");
    else
    {
        printf("\n 文件中输入的记录如下:\n\n");
        while (fread(&items,sizeof(items),1,fp_item) != 0)
        {
            printf(" %d %-15s %5.2f %5d", items.i_itemno,
                   items.c_itemname,
                   items.f_itemrate,items.i_itemqty);
            printf("\n\n");
        };
    }

    fclose(fp_item);
    return;
}
/* main 函数结束 */
```

**输出：**

```text
**********输入第 1 条记录:**********
请输入物品名称、物品单价和物品数量: Pen 10 12
是否想添加另一条记录 是(y)/否(n): y
**********输入第 2 条记录:**********
请输入物品名称、物品单价和物品数量: Pencil 1.50 50
是否想添加另一条记录 是(y)/否(n): n
文件中输入的记录如下:
1 Pen		10.00		12
2 Pencil	1.50		50
```

在程序 7 中，文件 `itemb` 以写入模式打开。模式规范为 `wb`，其中 `b` 代表二进制。从用户处获取并存储到文件中的值被组织为一个结构体。这些值随后使用 `scanf` 函数从用户处扫描输入。这些值使用 `fwrite` 函数存储在名为 `itemb` 的二进制文件中。函数 `fwrite` 的第一个参数是结构体变量 `items` 的地址。第二个参数是以结构体变量为参数的 `sizeof` 运算符。第三个参数是 1。这表明在每次操作中，只会写入一个由第二个参数指定的字节大小的数据块到文件中。第四个参数是指向数据存储目标文件的文件指针。用户可以继续输入任意数量的记录。为了终止循环，用户可以指定字符 `n` 或 `N`。然后关闭文件 `item`。

要读取文件 `itemb`，需以 `rb` 模式打开。要从文件中读取内容，使用 `fread` 函数。`fread` 函数接受其语法中指定的四个参数。第一个参数是结构体的地址。第二个参数是结构体 `items` 的 `sizeof`。第三个参数是 1。第四个参数是指向内容读取源文件的文件指针。函数 `fread` 返回从文件中读取的记录数。实际上，它将等于作为第三个参数指定的数量。当到达文件末尾（EOF）时，函数 `fread` 无法读取任何内容，因此它返回 0。因此，`fread` 的返回值可用于终止条件。一旦读取了文件内容，while 循环即终止。然后使用 `fclose` 函数关闭已打开的文件。

### 13.11 文件的随机访问

到目前为止，我们讨论的文件函数适用于按顺序读写数据。然而，有时我们只希望访问特定的记录。可能是直接访问第 5 条记录，第 10 条记录，或最后一条记录。在某些情况下，当文件指针位于第 10 条记录时，可能需要访问第 5 条记录。在这种情况下，需要向后移动文件指针。这种文件的随机访问可以通过 C 库中提供的 `fseek`、`ftell` 和 `rewind` 函数来实现。让我们逐一讨论它们。

#### 重新定位文件指针

函数 `fseek` 用于将文件位置移动到文件内的期望位置。函数 `fseek` 的语法如下：

```c
fseek(file_pointer, offset, position);
```

函数 `fseek` 接受三个参数。第一个参数是指向目标文件的文件指针。在上述语法中，第二个参数 `offset` 是文件指针由函数 `fseek` 移动的字节数。`offset` 可以是正数或负数。正的偏移量用于指示函数 `fseek` 将文件指针在文件中向前移动。负的偏移量用于在文件中向后移动。位置参数可以取 0、1 和 2 三个值之一，其中 0 表示文件开头，1 表示文件指针当前位置，2 表示文件末尾（EOF）。`offset` 的数据类型为 `long`。表 3 展示了使用函数 `fseek` 可以对文件执行的各种操作。

#### 表 3：fseek() 函数及其各种可能性

| **语句** | **操作** |
| :--- | :--- |
| fseek(file_pointer, 0L, 0) | 将文件指针移动到文件开头 |
| fseek(file_pointer, 0L, 1) | 保持在当前位置 |
| fseek(file_pointer, 0L, 2) | 将文件指针移动到文件末尾 |
| fseek(file_pointer, k, 0) | 将文件指针从文件开头向前移动第 (k+1) 个字节 |
| fseek(file_pointer, -k, 2) | 将文件指针从文件末尾向后移动第 (k-1) 个字节 |

当操作成功时，函数 fseek 返回零。当执行不成功的操作时，该函数返回 −1。不成功操作的例子是 fseek(fp_item,5,2)。数字 2 表示 EOF（文件结束）。因此，语句 fseek(fp_item, 5, 2) 试图将文件指针从文件末尾向前移动 5 个字节。C 库还包含一个 rewind 函数，用于将文件指针定位在文件开头。其工作方式与 fseek(file_pointer,0L,0) 类似。

程序 8 说明了函数 fseek 的使用，用于显示磁盘文件中可用的记录，并定位到用户提供的位置：

### ▶ 程序 8

```c
/* Program to illustrate the use of function fseek*/
#include<stdio.h>

/* Beginning of main function */
int main()
{
    FILE *fp_item;
    struct item
    {
        int i_itemno;
        char c_itemname[20];
        int i_itemqty;
        float f_itemrate;
    } items;
    
    int i_ctr=0, i_num, i_recsz=sizeof(items);
    char c_temp, c_ans;

    fp_item=fopen("itemb", "rb");
    if (fp_item==NULL)
        printf("Error in opening a file\n");
    else
    {
        do
        {
            printf("\nEnter the position of the item you would like to display: ");
            scanf("%d", &i_num);
            c_temp=getchar();
            rewind(fp_item);
            fseek(fp_item, --i_num*i_recsz, 1);

            if (fread(&items, i_recsz, 1, fp_item)!=0)
            {
                printf("\n The record you are searching for is....\n\n");
                printf("    %d %-15s %5.2f  %5d ", items.i_itemno,
                    items.c_itemname,
                    items.f_itemrate, items.i_itemqty);
                printf("\n");
            }
            else
                printf("\nThe record you are searching is not available.\n");
            
            printf("\nWould you like to continue (y/n): ");
            scanf("%c", &c_ans);
        } while (c_ans=='y' || c_ans=='Y');
    }
    fclose(fp_item);
    return 0;
}
/* End of function main */
```

**输出：**

> 输入您想要显示的项目位置：2

> 您正在查找的记录如下....

>        2 Pencil                1.50     50

> 是否继续 (y/n): y

> 输入您想要显示的项目位置：3

> 您正在查找的记录不可用。

> 是否继续 (y/n): n

程序 7 创建的文件在程序 8 中以读模式打开。用户被要求输入位置。语句 `fseek(fp_item,--i_num*i_recsz,1);` 提供了三个参数。第一个参数是指向文件 *itemb* 的文件指针 `fp_item`。第二个参数是 `--i_num*i_recsz`，其中变量 `i_recsz` 是以字节为单位的单条记录大小。在程序 8 中，变量 `i_recsz` 将是保存结构变量 items 的数据元素 itemno、itemname、itemrate 和 itemqty 所需的字节数之和。因此，`i_recsz` 的值将为 28 字节。变量 `i_num` 是文件指针要定位到的位置。由于使用了自减运算符作用于变量 `i_num`，在乘以 `i_recsz` 之前，`i_num` 的值会先减 1。表达式 `--i_num*i_recsz` 的结果随后用于计算文件指针需要向前移动的字节数。如表中所述，函数 `fseek` 从作为第三个参数提供的位置向前移动 k+1 个字节，其中 k 是字节集，1 代表一个这样的字节集。因此，k 应取比预期移动量少 1 的值。如果用户输入 5，则文件指针应从文件开头向前移动 4*28 字节。因此，函数 `fseek` 将文件指针定位在距文件开头 4*28 字节处，这正是用户想要的第五条记录。
