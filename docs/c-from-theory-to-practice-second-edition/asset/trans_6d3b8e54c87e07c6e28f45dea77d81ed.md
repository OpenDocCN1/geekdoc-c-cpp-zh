
```c
exit(EXIT_FAILURE);
}
fp_fail = fopen("fail.txt", "w");
if(fp_fail == NULL)
{
    fclose(fp_in);
    fclose(fp_suc);
    printf("Error: fail.txt can't be created\n");
    exit(EXIT_FAILURE);
}
suc_stud = fail_stud = 0;
while(1)
{
    if(fscanf(fp_in, "%s%s%f%f", fnm, lnm, &grd1, &grd2) != 4)
        break;
    if((grd1+grd2)/2 >= 5)
    {
        fprintf(fp_suc, "%s %s %f %f\n", fnm, lnm, grd1, grd2);
        suc_stud++;
    }
    else
    {
        fprintf(fp_fail, "%s %s %f %f\n", fnm, lnm, grd1, grd2);
        fail_stud++;
    }
}
printf("Failed: %d Succeeded: %d\n", fail_stud, suc_stud);
fclose(fp_suc);
fclose(fp_fail);
fclose(fp_in);
return 0;
}
```

## fgets() 函数

fgets() 函数用于从输入文件中读取若干字符。它在 stdio.h 中声明：

```c
char *fgets(char *str, int size, FILE *fp);
```

第一个参数指向为存储所读取字符而分配的内存。第二个参数声明将从 fp 指示的文件中读取的最大字符数。其值不应大于已分配内存的大小，以避免内存溢出。

fgets() 一旦读到换行字符或已读取 size-1 个字符（以先发生者为准）就停止读取字符。fgets() 会在末尾添加一个空字符。如果 fgets() 执行成功，读取的字符将存储在 str 指向的内存中，并返回该指针。如果到达文件末尾或发生读取错误，fgets() 返回 NULL。

下面的程序读取 50 个姓名（每个少于 100 个字符），并将它们存储到文本文件的不同行中。然后，程序读取一个字符，从文件中读取这些姓名，并显示以输入字符开头的姓名。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    FILE *fp;
    char ch, str[100];
    int i, times;

    fp = fopen("test.txt", "w+");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    for(i = 0; i < 50; i++)
    {
        printf("Enter name: ");
        read_text(str, sizeof(str), 1);
        fprintf(fp, "%s\n", str);
    }
    printf("Enter char: ");
    ch = getchar();

    fseek(fp, 0, SEEK_SET);
    times = 0;
    while(1)
    {
        if(fgets(str, sizeof(str), fp) == NULL)
            break;
        if(str[0] == ch)
        {
            printf("Name: %s\n", str);
            times++;
        }
    }
    printf("Total occurrences = %d\n", times);
    fclose(fp);
    return 0;
}
```

## 中美科技竞争背景下的“卡脖子”与产业自主可控

近年来，中美科技竞争不断加剧，美国通过出口管制、实体清单等手段对中国高科技产业实施封锁，导致部分关键技术和零部件出现“卡脖子”问题。在此背景下，实现产业自主可控成为国家战略重点。

### 一、什么是“卡脖子”技术

“卡脖子”技术是指在关键产业链中，依赖外部供应且难以替代的技术或产品。一旦供应中断，将严重影响产业安全和国家安全。典型的“卡脖子”领域包括高端芯片、光刻机、航空发动机、操作系统等。

### 二、产业自主可控的路径

- 加强基础研究，突破核心技术瓶颈
- 完善产业链条，培育本土供应链
- 加大政策支持，引导社会资本投入
- 推动产学研协同，促进成果转化
- 深化国际合作，构建开放创新生态

### 三、案例分析：芯片产业

芯片产业是“卡脖子”问题的典型代表。我国在芯片设计领域已取得一定进展，但在高端制造设备、EDA软件、先进制程工艺等方面仍受制于人。近年来，国内企业加大研发投入，部分环节已实现局部突破。

| 环节 | 现状 | 挑战 |
| --- | --- | --- |
| 设计 | 部分企业达到国际水平 | 架构授权受限 |
| 制造 | 成熟制程量产 | 先进制程受限 |
| 设备 | 部分环节自主化 | 光刻机差距明显 |
| 材料 | 中低端基本自给 | 高端依赖进口 |

```c
if(fp == NULL)
{
    printf("Error: fopen() failed\n");
    exit(EXIT_FAILURE);
}
printf("\nLine contents\n");
lines = 1;
while(1)
{
    ch = getc(fp);
    if((ch == EOF) || (lines > 2))
        break;
    if(ch == '\n') /* Once the new line character is read, increment the variable that counts the lines. */
        lines++;
    if(lines == 2) /* Only the characters of the second line are displayed. */
        printf("%c", ch);
}
fclose(fp);
return 0;
```

注释：一旦程序显示第二行，循环就终止。

## C.15.10

假设 test.txt 是一个文本文件。下面程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    FILE *fp;
    char ch;

    if((fp = fopen("test.txt", "r")) != NULL)
    {
        while(ch = getc(fp) != EOF)
            putc(ch, stdout);
        fclose(fp);
    }
    return 0;
}
```

答案：如果 while 语句编写正确，程序本应显示文件中的字符。其正确语法是：

```c
while((ch = getc(fp)) != EOF)
```

内层括号是出于优先级原因所需要的。由于缺少这些括号，只要未到达文件末尾，就会先执行表达式 getc(fp) != EOF，其值为 1。因此，ch 变为 1，程序会连续显示该 ASCII 值对应的字符。当 getc() 返回 EOF 时，ch 变为 0，循环终止。

## C.15.11 一种简单的数据加密方法是将其与密钥进行异或。编写一个程序，读取一个密钥字符和一个文本文件的名称，并通过将每个字符与密钥进行异或来加密其内容。加密后的字符应存储在用户选择的第二个文件中。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

int main(void)
{
    FILE *fp_in, *fp_out;
    char str[100];
    int ch, key_ch;

    printf("Enter input file: ");
    read_text(str, sizeof(str), 1);

    fp_in = fopen(str, "r");
    if(fp_in == NULL)
    {
        printf("Error: Input file can't be loaded\n");
        exit(EXIT_FAILURE);
    }
    printf("Enter output file: ");
    read_text(str, sizeof(str), 1);

    fp_out = fopen(str, "w");
    if(fp_out == NULL)
    {
        fclose(fp_in);
        printf("Error: Output file can't be created\n");
        exit(EXIT_FAILURE);
    }
    printf("Enter key char: ");
    key_ch = getchar();
    while(1)
    {
        ch = getc(fp_in);
        if(ch == EOF)
            break;
        putc(ch ^ key_ch, fp_out);
    }
    fclose(fp_in);
    fclose(fp_out);
    return 0;
}
```

注释：如果重新运行程序，并将加密文件和相同的密钥作为输入，输出文件将与原始文件相同，因为根据布尔代数有：(a ^ b) ^ b = a。

## C.15.12

定义一个 country 类型的结构体，成员包括：name、capital 和 population。假设名称少于 100 个字符。假设一个文本文件包含若干国家的数据。第一行包含国家数量，后续行以如下形式存储每个国家的数据：

name capital population

编写一个程序，读取文件名，并使用 country 类型将国家数据存储到动态分配的内存中。然后，程序应读取一个数字，并显示人口高于该数字的国家。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int read_text(char str[], int size, int flag);

typedef struct
{
    char name[100];
    char capital[100];
    int pop;
} country;

int main(void)
{
    FILE *fp;
    country *cntr;
    char str[100];
    int i, num_cntr, pop;
    printf("Enter file name: ");
    read_text(str, sizeof(str), 1);
    fp = fopen(str, "r");
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    if(fscanf(fp, "%d", &num_cntr) != 1)
    {
        fclose(fp);
        printf("Error: fscanf() failed\n");
        exit(EXIT_FAILURE);
    }
    /* Dynamic memory allocation to store the countries' data. */
    cntr = (country*) malloc(num_cntr * sizeof(country));
    if(cntr == NULL)
    {
        fclose(fp);
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
```

```c
    break;
    printf("%c", ch);
}
fclose(fp);
    return 0;
}
```

该循环只显示字符 a 和 b，下一次调用 getc() 就会结束循环，因为下一个字符被解释为文件末尾。另一方面，如果我们使用 "w+b" 模式，程序将显示所有字符，因为在二进制文件中没有字符具有特殊含义。

## fseek() 和 ftell() 函数

每次读或写操作通常按顺序执行。然而，在必要时，可以按任意顺序读取或写入文件。fseek() 函数用于在文件内进行随机访问。它在 stdio.h 中声明：

```c
int fseek(FILE *fp, long int offset, int origin);
```

fseek() 将与 fp 关联的文件指针移动到距 origin 指示位置 offset 字节的新位置。如果 offset 为负，文件指针向后移动。origin 的值必须是以下常量之一，这些常量定义在 stdio.h 中：

- SEEK_SET。文件指针从文件开头移动 offset 字节。
- SEEK_CUR。文件指针从当前位置移动 offset 字节。
- SEEK_END。文件指针从文件末尾移动 offset 字节。

例如，要移动到文件末尾，我们可以写：

```c
fseek(fp, 0, SEEK_END);
```

要从文件开头移动 20 字节，我们可以写：

```c
fseek(fp, 20, SEEK_SET);
```

如果 fseek() 执行成功，它返回 0。否则，返回非零值。

当 fseek() 用于文本文件时，需要小心换行字符。例如，假设以下代码在文本文件的前两行写入一些文本。如果操作系统将 '\n' 扩展为 '\r' 和 '\n'，则为了移动到第二行开头，offset 的值应为 6（而不是 5）。

```c
fputs("text\n", fp);
fputs("another text\n", fp);
/* Move to the beginning of the second line. */
fseek(fp, 6, SEEK_SET);
```
