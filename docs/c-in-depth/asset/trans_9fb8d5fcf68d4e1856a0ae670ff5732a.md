
林间小径可爱、幽暗而深邃
但在我睡去之前，我还有很长的路要走。
^Z

执行此程序后，这段文本连同 ^Z 字符将被写入 myfile.txt

### 11.8.2 fgetc()
声明: int fgetc( FILE *fptr );

本函数从给定文件中读取单个字符并递增文件指针位置。成功时返回字符在转换为 int 时不带符号扩展后的值。文件结束或出错时返回 EOF。在下一个程序中，我们将读取在前一个程序中创建的 myfile.txt 文件。

```
/*P11.2 Program to understand the use of fgetc()*/
#include<stdio.h>
main()
{
 FILE *p;
 char ch;
 if((p=fopen("myfile.txt", "r"))==NULL)
   printf("This file doesn't exist\n");
 else
 {
   while((ch=fgetc(p))!=EOF)
     printf("%c",ch);
 }
 fclose(p);
}
```

### Output
输出

林间小径可爱、幽暗而深邃
但在我睡去之前，我还有很长的路要走。

我们在程序中编写的 while 循环等价于以下代码-

```
ch=fgetc(p);
while(ch!=EOF)
{
  printf("%c",ch);
  fgetc(p);
}
```

fputc( ) 和 fgetc( ) 返回的值不是 char 类型而是 int 类型。这是因为函数在文件结束或出错时返回整数值 EOF(-1)。出于同样的原因，用于存储从文件中读取的字符的变量 ch 也被声明为 int 类型。

### 11.8.3 getc() and putc()
getc( ) 和 putc( ) 的操作与 fgetc( ) 和 fputc( ) 完全相似，唯一的区别是前两者被定义为宏，而后两者是函数。

## 11.9 Integer I/O
11.9 整数 I/O

### 11.9.1 putw()
声明: int putw(int value, FILE *fptr)

本函数将整数值写入 fptr 指向的文件。成功时返回写入文件中的整数，出错时返回 EOF。

```
/*P11.3 Program to understand the use of putw() function*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int value;
    fptr=fopen("num.dat","wb");
    for(value=1;value<=30;value++)
        putw(value,fptr);
    fclose(fptr);
}
```

此程序将整数 1 到 30 写入文件 "num.dat"。

### 11.9.2 getw()
声明: int getw( FILE *fptr );

本函数从与 fptr 关联的文件中返回整数值。成功时返回输入文件中的下一个整数，错误或文件结束时返回 EOF。

```
/*P11.4 Program to understand the use of getw() function*/
#include<stdio.h>
main()
{
    FILE *fptr;
    int value;
    fptr=fopen("num.dat","rb");
    while((value=getw(fptr))!=EOF)
        printf("%d\t",value);
    fclose(fptr);
}
```

此程序将读取并打印文件 "num.dat" 中的整数，该文件是在之前创建的。

如果 getw() 与文本文件一起使用，则当文件中存在整数 26 时会停止读取，因为在文本文件中文件结束由 ASCII 26 表示，而这也是一个有效整数值。因此 getw() 不应与文本文件一起使用。

EOF 的值为 -1，这是一个有效的整数值，因此如果文件中不存在 -1，此程序将正确工作，如果文件中存在 -1，则 getw() 将停止读取，-1 之后的所有值都将被遗留未读。因此我们应使用 feof() 检查文件结束，使用 ferror() 检查错误。这些函数将在本章后面讨论。

## 11.9 Integer I/O
11.9 整数 I/O

### 11.9.1 putw()
声明: int putw(int value, FILE *fptr)

本函数将整数值写入 fptr 指向的文件。成功时返回写入文件中的整数，出错时返回 EOF。

```
/*P11.3 Program to understand the use of putw() function*/
#include<stdio.h>
main()
{
FILE *fptr;
int value;
fptr=fopen("num.dat","wb");
for(value=1;value<=30;value++)
    putw(value,fptr);
fclose(fptr);
}
```

此程序将整数 1 到 30 写入文件 "num.dat"。

### 11.9.2 getw()
声明: int getw( FILE *fptr );

本函数从与 fptr 关联的文件中返回整数值。成功时返回输入文件中的下一个整数，错误或文件结束时返回 EOF。

```
/*P11.4 Program to understand the use of getw() function*/
#include<stdio.h>
main()
{
FILE *fptr;
int value;
fptr=fopen("num.dat","rb");
while((value=getw(fptr))!=EOF)
    printf("%d\t",value);
fclose(fptr);
}
```

此程序将读取并打印文件 "num.dat" 中的整数，该文件是在之前创建的。

如果 getw() 与文本文件一起使用，则当文件中存在整数 26 时会停止读取，因为在文本文件中文件结束由 ASCII 26 表示，而这也是一个有效整数值。因此 getw() 不应与文本文件一起使用。EOF 的值为 -1，这是一个有效的整数值，因此如果文件中不存在 -1，此程序将正确工作，如果文件中存在 -1，则 getw() 将停止读取，-1 之后的所有值都将被遗留未读。因此我们应使用 feof() 检查文件结束，使用 ferror() 检查错误。这些函数将在本章后面讨论。

## 11.10 String I/O
11.10 字符串 I/O

### 11.10.1 fputs()
声明: int fputs(const char *str, FILE *fptr);

本函数将 str 指向的以空字符结尾的字符串写入文件。标记字符串结束的空字符不会写入文件。成功时返回写入的最后一个字符，错误时返回 EOF。

```
/*P11.5 Program to understand the use of fputs()*/
#include<stdio.h>
main()
{
FILE *fptr;
char str[80];
fptr=fopen("test.txt","w");
printf("Enter the text\n");
printf("To stop entering, press Ctrl+d in Unix and Ctrl+z in Dos\n");
while(gets(str)!=NULL)
fputs(str,fptr);
fclose(fptr);
}
```

假设我们在运行程序后输入以下文本-

Yesterday is history
Tomorrow is mystery
Today is a gift
That's why it is called Present
^Z

当输入第一行文本并按下 Enter 键时，gets() 函数将换行符转换为空字符，数组 str 包含 "Yesterday is history"(20 个字符 +1 个空字符)。现在 str 使用 fputs() 写入文件 test.txt。空字符不会写入文件，因此只写入 20 个字符。

在前几章中我们学习过 puts() 函数，它在屏幕上打印字符串。这两个函数的不同之处在于 puts() 将空字符转换为换行符，而 fputs() 不会。fputs() 只有在字符串中包含换行符时才会将换行符写入文件。因此第一行文本后换行符不会进入文件。紧跟在第一行文本之后，第二行文本将被写入。在下一个程序中我们将看到如何使用 fgets() 读取此文件

### 11.10.2 fgets()
声明: char *fgets(char *str, int n, FILE *fptr);

本函数用于从文件中读取字符并将这些字符存储在 str 指向的字符串中。它最多从文件中读取 n-1 个字符，其中 n 为第二个参数。fptr 是一个文件指针，指向从中读取字符的文件。本函数在成功时返回 str 指向的字符串，在错误或文件结束时返回 NULL。

本函数与 printf() 函数相同，但它将格式化数据写入文件而不是标准输出(屏幕)。本函数与 printf() 的参数相同，但它有一个额外的参数，即 FILE 类型的指针，指向要写入输出的文件。它在成功时返回输出到文件的字符数，错误时返回 EOF。

```c
/*P11.7 Program to understand the use of fprintf()*/
#include<stdio.h>
main()
{
    FILE *fp;
    char name[10];
    int age;
    fp=fopen("rec.dat","w");
    printf("Enter your name and age : ");
    scanf("%s%d",name,&age);
    fprintf(fp,"My name is %s and age is %d",name,age);
    fclose(fp);
}
```

```c
/*P11.8 Program to understand the use of fprintf()*/
#include<stdio.h>
struct student
{
    char name[20];
    float marks;
}stu;
main()
{
    FILE *fp;
    int i,n;
    fp=fopen("students.dat","w");
    printf("Enter number of records : ");
    scanf("%d",&n);
    for(i=1;i<=n;i++)
    {
        printf("Enter name and marks : ");
        scanf("%s%f",stu.name,&stu.marks);
        fprintf(fp,"%s %f",stu.name,stu.marks);
    }
}
```

### 11.11.2 fscanf()
声明: fscanf ( FILE *fptr, const char *format [, address, ...] );

本函数与 scanf() 函数类似，但它从文件而不是标准输入读取数据，因此它有一个额外的参数，即 FILE 类型的指针，指向将从中读取数据的文件。它在成功时返回被赋值的参数数量，在文件结束时返回 EOF。

在下一个程序中，我们将读取使用 fprintf() 在 P11.8 中创建的 students.dat 文件。请注意，fscanf() 中使用的格式字符串应与写入文件时 fprintf() 中使用的格式字符串相同。
