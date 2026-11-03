
Position ———→ 0 1 2 ........ 25
Character
stored ———→ A B C ........ Z

我们两次读取文件。第一次，我们读取每第五个位置的内容并将其值与其位置一起打印到屏幕上。第二次，我们从文件末尾读取文件内容并同样打印到屏幕上。

在第一次读取期间，当 fseek (fp,n,0) 的参数 n 变为 30 时，文件指针会越过文件结束标记。因此，在打印位置 30 的内容后，循环终止。（位置 30 中没有内容。）

为了从末尾读取文件，我们使用语句

```
fseek(fp, -1L,2);
```

将文件指针定位到最后一个字符。由于每次读取都会使位置向前移动一个位置，因此我们必须将其向后移动两个位置以读取下一个字符。这是通过函数

```
fseek(fp, -2L, 1);
```

在 while 语句中实现的。该语句还测试文件指针是否越过文件边界。只要越过边界，循环就会立即终止。

```
Program
/*************************************************/
/*************************************************/
/* ILLUSTRATION OF fseek & ftell FUNCTIONS */
/*************************************************/

#include <stdio.h>
main()
{
 FILE *fp;
 long n;
 char c;
 fp = fopen("RANDOM", "w");
 while((c=getchar())!=EOF)
 putc(c,fp);
 printf("No. of characters entered = %ld\n", ftell(fp));
 fclose(fp);
 fp = fopen("RANDOM", "r");
 n = 0L;
 while(feof(fp) == 0)
 {
 fseek(fp, n, 0); /* Position to (n+1)th character */
 printf("Position of %c is %ld\n", getc(fp), ftell(fp));
 n = n+5L;
 }
 putchar('\n');
 fseek(fp, -1L,2); /* Position to the last character */
 do
 {
 putchar(getc(fp));
}
while(fseek(fp,-2L,1));
fclose(fp);
}
输出
ABCDEFGHIJKLMNOPQRSTUVWXYZ
输入的字符数 = 26
A 的位置是 0
F 的位置是 5
K 的位置是 10
P 的位置是 15
U 的位置是 20
Z 的位置是 25
? 的位置是 30
ZYXWVUTSRQPONMLKJIHGFEDCBA
```

图 13.6 fseek 和 ftell 函数的说明

## 13.7 命令行参数

什么是命令行参数？它是在程序被调用时提供给程序的参数。该参数可能表示程序应处理的文件名。例如，如果我们想执行一个程序来复制名为 X_FILE 的文件的内容到另一个名为 Y_FILE 的文件，则可以使用如下命令行

```
C>PROGRAM X_FILE Y_FILE
```

PROGRAM 是存储程序可执行代码的文件名。这消除了程序在执行期间请求用户输入文件名的需要。这些参数如何进入程序？我们知道每个 C 程序都应有一个 main 函数，它标志着程序的开始。但我们迄今未提及的是，它也可以像其他函数一样接受参数。事实上 main 可以接受两个参数称为 argc 和 argv，命令行中的信息在系统调用 main 时通过这些参数传递给程序。变量 argc 是一个参数计数器，计算命令行上的参数数量。argv 是一个参数向量，表示指向命令行参数的字符指针数组。此数组的大小将等于 argc 的值。例如，对于上面给出的命令行，argc 为三，argv 是指向字符串的三个指针的数组，如下所示：

```
argv[0] ------> PROGRAM
argv[1] ------> X_FILE
argv[2] ------> Y_FILE
```

为了访问命令行参数，我们必须按如下方式声明 main 函数及其参数：

```
main(argc, argv)
int argc;
char *argv[];
{
    ....
    ....
}
```

命令行中的第一个参数始终是程序名，因此 argv[0] 始终表示程序名。

## 示例 13.5

编写一个程序，使其接收文件名和一行文本作为命令行参数，并将文本写入文件。

图 13.7 显示了命令行参数的使用。命令行是

F12_6 TEXT AAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG.

命令行中的每个单词都是 main 的一个参数，因此参数总数为 9。

参数向量 argv[1] 指向字符串 TEXT，因此语句

```
fp = fopen(argv[1], "w");
```

以名称 TEXT 打开一个文件。紧接着的 for 循环将剩余的 7 个参数写入文件 TEXT。

程序还打印两个输出，一个来自文件 TEXT，另一个来自系统内存。参数向量 argv 包含内存中的整个命令行，因此语句：

```
printf("%s\n", argv[i]);
```

从内存中打印参数。

```
Program
/*.........................................................................*/
/* COMMAND LINE ARGUMENTS */
/*.........................................................................*/

#include <stdio.h>
main(argc, argv)    /* main with arguments */
int argc;           /* argument count */
char *argv[];       /* list of arguments */
{
    FILE *fp;
    int i;
    char word[15];
    fp = fopen(argv[1], "w");    /* open file with name argv[1] */
    printf("\nNo. of arguments in Command line = %d\n", argc);
    for(i = 2; i < argc; i++)
        fprintf(fp, "%s ", argv[i]);    /* write to file argv[1] */
    fclose(fp);
    /* Writing content of the file to screen */
    printf("Contents of %s file\n", argv[1]);
    fp = fopen(argv[1], "r");
    for(i = 2; i < argc; i++)
{
    fscanf(fp, "%s", word);
    printf("%s", word);
}
fclose(fp);
printf("\n");
/* Writing the arguments from memory          */
for(i = 0; i < argc; i++)
    printf("%s\t\n", argv[i]);
}
输出
C:\F12_6 TEXT AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG
命令行中的参数数 = 9
TEXT 文件的内容
AAAAAA BBBBBB CCCCCC DDDDDD EEEEEE FFFFFF GGGGGG
C:\F12_6.EXE
TEXT
    AAAAAA
        BBBBBB
            CCCCCC
                DDDDDD
                    EEEEEE
                        FFFFFF
                            GGGGGG
```

图 13.7 命令行参数的使用

## 案例研究

### 向文件追加项目

这里开发了一个程序，用于向文件 INVENTORY 追加额外项目并打印文件的总内容。该程序如图 13.8 所示。它使用结构定义来描述每个项目，并使用函数 append () 将项目添加到文件中。

执行时，程序会请求要追加数据的目标文件名。在追加项目后，最后一个字符在文件中的位置被赋给 n，然后文件被关闭。

文件重新打开以供读取并显示其内容。请注意，读取和显示是在 while 循环的控制下进行的。循环将当前文件位置与 n 进行比较，并在它们相等时终止。

```
Program
/* ************************************************************/
/*      APPENDING ITEMS TO AN EXISTING FILE                   */
/* ************************************************************/
#include <stdio.h>
struct invent_record
{
    char name[10];
    int  number;
    float price;
    int  quantity;
};
main()
{
    struct invent_record item;
    char filename[10];
    int  response;
    FILE *fp;
    long n;
    printf("Type filename:");
    scanf("%s", filename);
    fp = fopen(filename, "a+");
    do
    {
        append(&item, fp);
        printf("\nItem %s appended \n",item.name);
        printf("\nDo you want to add another item \\(1 for YES /0 for NO)?");
        scanf( "%d", &response);
    } while (response == 1);
    n = ftell(fp);        /* Position of last character */
    fclose(fp);
    fp = fopen(filename, "r");
    while(ftell(fp) < n)
    {
        fscanf(fp, "%s %d %f %d",
        item.name, &item.number, &item.price, &item.quantity);
        printf("%8s %7d %7.2f %8d\n",
        item.name, item.number, item.price, item.quantity);
    }
    fclose(fp);
}
append(product, ptr)
struct invent_record *product;
FILE  *ptr;
{
    printf("Item name:");
    scanf("%s", product->name);
    printf("Item number:");
    scanf("%d", &product->number);
    printf("Item price:");
    scanf("%f", &product->price);
    printf("Quantity:");
    scanf("%d", &product->quantity);
    fprintf(ptr, "%s %d %f %d",
    product->name,
    product->number,
    product->price,
    product->quantity);
}
```
