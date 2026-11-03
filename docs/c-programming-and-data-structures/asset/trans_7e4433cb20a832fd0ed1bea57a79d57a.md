
## 示例 A.68

使用结构体实现以下员工信息字段：

- 员工编号
- 姓名（名、中间名、姓）
- 入职日期（DOJ）
- 总薪资（HRA、BASIC、特殊津贴）

### 程序

```
/*Program for demonstrating nesting of structures*/
#include <stdio.h>
#include <conio.h>

void main ()
{
 struct employee/*Declaring the nested structure*/
 {
  int emp_id;
  struct name
  {
   char First[20];
   char Middle[20];
   char Last[20];
  }emp_name;
  char doj[20];
  struct G_Sal
  {
   float basic;
   float hra;
   float spl_allow;
  }emp_sal;
 };
 struct employee emp1;
 clrscr();

 /*Initializing structure variable emp1*/
 emp1.emp_id=37;
 strcpy(emp1.emp_name.First,"N");
 strcpy(emp1.emp_name.Middle,"Siva");
 strcpy(emp1.emp_name.Last,"Kumar");
 strcpy(emp1.doj,"22/10/2004");
 emp1.emp_sal.basic=17432.00;
 emp1.emp_sal.hra=10032.00;
 emp1.emp_sal.spl_allow=5000.00;

 /*Printing the values of emp1*/
 printf("\nEmp ID: %d",emp1.emp_id);
 printf("\nName: %s %s %s",emp1.emp_name.First,emp1.emp_name.Middle,emp1.emp_name.Last);
 printf("\nDate of Joining (DD MM YYYY): %s",emp1.doj);
 printf("\nGross Salary: %.2f",emp1.emp_sal.basic+emp1.emp_sal.hra+emp1.emp_sal.spl_allow);

 }
 getch();
}
```

### 输出
员工编号：37
姓名：N Siva Kumar
入职日期（日 月 年）：22/10/2004
总薪资：32464.00

## 示例 A.69 编写一个简单程序演示联合体的使用。

### 程序
```c
/*Program for demonstrating the use of unions*/
#include <stdio.h>
#include <conio.h>

void main ()
{
union student/*Declaring union*/
{
int roll_no;
char result;
}st1,st2;
clrscr();

/*Initializing union variables*/
st1.roll_no=20;
st2.result='P';

/*Accessing and printing the values correctly*/
printf("\nRoll NO: %d",st1.roll_no);
printf("\nResult: %c",st2.result);

printf("\n\n");

/*Accessing and printing the values incorrectly*/
printf("\nRoll NO: %d",st2.roll_no);
printf("\nResult: %c",st1.result);

getch();
}
```

### 输出
学号：20
结果：P

学号：12880
结果：¶

## 示例 A.70 编写一个程序显示结构体变量的大小。

### 程序
```
/*Program for demonstrating the use of sizeof operator with structures*/
#include <stdio.h>
#include <conio.h>

void main ()
{
    struct s/*Declaring a structure*/
    {
        int a;
        char b;
        float c;
        long d;
    }s1;
    clrscr();

    /*Printing the size of structure variable s1*/
    printf("\nSize of (s1) = %d",sizeof(s1));

    getch();
}
```

### 输出
(s1)的大小 = 11

## 示例 A.71 编写一个程序，使用 sizeof 运算符区分结构体和联合体。

### 程序
```
/*Program for differentiating between structure and union*/
#include <stdio.h>
#include <conio.h>

void main ()
{
    struct s/*Declaring a structure*/
    {
        int a;
        char b;
        float c;
        long d;
    }s1;

    union u/*Declaring a union*/
    {
        int a;
```
```
char b;
float c;
long d;
}u1;
clrscr();

/*Printing the sizes of structure and union variables*/
printf("\nSize of {s1} = %d",sizeof(s1));
printf("\nSize of {u1} = %d",sizeof(u1));

getch();
}
```

### 输出

{s1}的大小 = 11
{u1}的大小 = 4

## 示例 A.72 编写一个简单程序打开和关闭文件；若操作不成功则打印错误消息。

### 程序

```
/*Program for opening and closing a file*/
/*Source.txt file is placed at ../bin/ location*/
#include <stdio.h>
#include <conio.h>

void main()
{
FILE *fs;/*Declaring file access pointer*/
char ch;
clrscr();

fs = fopen("Source.txt","r");/*Opening a file*/
if(fs==NULL)
{
printf("Source file cannot be opened.");/*Displaying error message incase of unsuccessful opening of the file*/
getch();
exit(0);
}
else
printf("\nFile Source.txt successfully opened");

fclose(fs);/*Closing the file*/
printf("\nFile Source.txt successfully closed");

printf("\nPrint any key to end the program execution");
getch();
}
```

### 输出
文件 Source.txt 成功打开

文件 Source.txt 成功关闭

按任意键结束程序执行

## 示例 A.73 编写一个程序将一个文件的内容复制到另一个文件。

### 程序
```c
/*Program for copying contents of one file into another*/
/*Source.txt file is placed at ../bin/ location*/
#include <stdio.h>
/*include <conio.h> is placed at ../bin/ location*/
void main()
{
FILE *fs,*ft;/*Declaring file access pointers*/
char ch;
clrscr();
fs = fopen("Source.txt","r");/*Opening the source file in read mode*/
if(fs==NULL)
{
printf("Source file cannot be opened.");
exit(0);
}
ft = fopen("Destination.txt","w");/*Opening the target file in write mode*/
if (ft==NULL)
{
printf("Target file cannot be opened.");
exit(0);
}
while(1)
{
ch=fgetc(fs);/*Reading contents of Source.txt character by character*/
if (ch==EOF)
break;
else
fputc(ch,ft);/*Copying Source.txt file contents into Destination.txt one character at a time*/
}
/*Closing the files*/
fclose(fs);
fclose(ft);
printf("\nFile copy operation performed successfully");
printf("\nYou can confirm the same by checking the Destination.txt file");
getch();
}
```

### 输出
文件复制操作成功执行

您可以通过检查 Destination.txt 文件来确认这一点

## A.64 计算机编程

### 程序
```c
/*Program for counting the number of characters present in a file*/
/*Source.txt file is placed at ../bin/ location*/
#include <stdio.h>
#include <conio.h>
void main()
{
FILE *fs;/*Declaring the file access pointer*/
char ch;
long count=0;/*Declaring the count variable*/
clrscr();
fs = fopen("Source.txt","r");/*Opening the source file*/
if(fs==NULL)
{
printf("Source cannot be opened.");
exit(0);
}
while(1)
{
ch=fgetc(fs);
if (ch==EOF)
break;
else
count=count+1;/*Counting the number of characters present in the source file*/
}
fclose(fs);
printf("\nThe number of characters in %s is %ld", "Source.txt",count);
getch();
}
```

### 输出

Source.txt 中的字符数为 41

### 程序
```c
/*Program reading file contents and printing its reverse*/
/*Source.txt file is placed at ../bin/ location*/
#include <stdio.h>
/*Source.txt file is placed at ../bin/ location*/
#include <conio.h>
```
（续）

```
void main()
{
FILE *fs,*ft;/*Declaring file access pointers*/
char str[100];
int i;
clrscr();

fs = fopen("Source.txt","r");/*Opening the source file in read mode*/
if(fs==NULL)
{
printf("Source file cannot be opened.");
exit(0);
}
ft = fopen("Target.txt","w");/*Opening the target file in write mode*/
if (ft==NULL)
{
printf("Target file cannot be opened.");
fclose(fs);
exit(0);
}

i=0;
while(1)
{
str[i]=fgetc(fs);/*Reading contents of Source.txt character by character*/
if (str[i]==EOF)
break;
else
i=i+1;
}

for(i=strlen(str)-2;i>=0;i--)
fputc(str[i],ft);/*Writing the reverse of file contents*/

/*Closing the files*/
fclose(fs);
fclose(ft);

printf("\nContents of Source.txt successfully printed in reverse order in Target.txt");
printf("\nYou can confirm the same by checking the Target.txt file");
getch();
}
```

### 输出

Source.txt 的内容已成功按逆序打印到 Target.txt 中
您可以通过检查 Target.txt 文件来确认这一点

## 示例 A.76 编写一个程序从一个文件读取整数列表，并按逆序将其复制到另一个文件。

### 程序
```
/*Program for demonstrating the use of getw and putw*/
#include <stdio.h>
#include <conio.h>
/*
This program uses source file named S1, which contains the following elements:
1
2
3
4
5
*/
void main()
{
FILE *fs,*ft,*fp;/*Declaring file access pointers*/
int i,j,arr[10],num;
clrscr();
fs = fopen("S1","r");/*Opening the source file in read mode*/
if (fs==NULL)
{
printf("Source file cannot be opened.");
exit(0);
}
ft = fopen("S2","w");/*Opening the destination file in write mode*/
if (ft==NULL)
{
printf("Target file cannot be opened.");
fclose(fs);
exit(0);
}
i=0;
while((arr[i]=getw(fs))!=EOF)/*Reading integers from source file and storing them in array arr[]*/
i=i+1;
fclose(fs);
for(j=i-1;j>=0;j--)
putw(arr[j],ft);/*Copying the source integer list into target file in reverse order*/
fclose(ft);
/*Verifying the contents of the target file*/
fp = fopen("T2","r");
if (fp==NULL)
{
printf("Target file cannot be opened.");
```
