
```c
3. main() {
 char fname[ ];
 "c:\\students.dat";
 FILE *fp;
 fp = fopen( fname ,"r");
 if (fp == NULL)
 printf("\nUnable to open file...");
}
```

输出：无错误。但请记住必须包含 "stdio.h"。

```c
4. main() {
 FILE *fp;
 char str[80];
 fp = fopen("Try.c","r");
 while(fgets(str,80,fp) != EOF)
 fputs(str);
 fclose(fp);
}
```

输出：错误。因为 fputs() 需要两个参数，应写成 fputs(str,fp)，并且因为我们在循环中使用字符串，所以 EOF 的位置会出现 NULL。

```c
5. unsigned char;
```

```c
{
 puts("\nEnter name");
 gets(name);
 fwrite(name,sizeof(name),1,fp);
}
```

输出：错误。因为 sizeof 应该是单个单词，并且应使用 fclose 来关闭文件。

```c
10. FILE *fp;
 fp=fopen("matrix","r");
 fseek(fp,20,SEEK_SET);
 fclose(fp);
```

输出：应使用 20L 而不是 20，因为 fseek() 需要一个 long 偏移值。

```c
11. FILE *fp;
 char s[80];
 fp=fopen("matrix","r");
 while(!feof(fp))
 {
 fgets(s, 80,fp);
 puts(s);
 }
 fclose(fp);
```

输出：“matrix” 文件的最后一行将被读取两次。为避免

FILE *fp;
fp=fopen("matrix",
"r");
while((ch=getc(fp))!=EOF)
    printf("%c",ch);
fclose(fp);

输出：EOF 已在文件 "stdio.h" 中定义为 # define EOF -1，而 unsigned char 的范围是 0 到 255，因此当从文件中读取 EOF 时无法容纳在 ch 中。解决方法是将 ch 声明为 int。

6.    unsigned char;
FILE *fp;
fp=fopen("matrix",
"r");
    if(!fp)
    {
        printf("file
opening

为此，使用：
while(fgets(s,80,fp)!=NULL)
    puts(s);

![](img/3a2b6e5e90a58a56458b0539952c0cd2_265_0.png)

C - Programmer  
Harry.

![](img/3a2b6e5e90a58a56458b0539952c0cd2_265_1.png)

## 第13章
(杂项主题)

我们已经知道 # define 语句可用于定义符号常量。因此常量提供了一种简写表示法。Define 语句可用于定义宏，即它们可用于替换表达式、完整语句或一组语句。

使用宏求两个数最大值程序：

```c
#define max(a,b) a>b?a:b /*declaration of macro*/
main()
{
int a,b,ans;
printf("Enter two numbers");
scanf("%d %d",&a,&b);
ans = max(a,b);
printf("max = %d",ans);
getch();
}
```

该程序包含一个宏 max，表示表达式 a>b?a:b。当程序编译时，表达式 a>b?a:b 将替换标识符 max。

宏定义通常放在文件的开头，在第一个文件函数定义之前。宏的作用域是全局的。

多行宏也可以通过在除最后一行外的每一行末尾放置反斜杠来定义。此功能允许将单个宏表示为复合语句。

### 将变量声明为常量:-

我们可能希望某个变量的值在程序执行期间不发生变化。这可以通过在初始化时使用关键字 const 声明变量来实现。

```c
const float PI = 3.14;
```

此声明告诉编译器变量 pi 的值在程序执行期间不得更改。

### 将变量声明为 volatile:-

ANSI 标准定义了另一个限定符 volatile，可用于明确告知编译器变量的值可能随时被某些外部源（来自程序外部）更改。

```c
volatile int date;
```

即使变量不出现在赋值语句的左侧，其值也可能被某些外部因素更改。

当我们将变量声明为 volatile 时，编译器每次遇到该变量时都会检查其值，以查看是否有任何外部更改导致值发生变化。

### Mind Drill Note-

请记住，声明为 volatile 的变量的值也可以由其自身程序修改。

如果我们希望值不得被程序修改，而可能被其他进程更改，则可以将变量同时声明为 const 和 volatile，如 (volatile const int = 150;)。

### 定义符号常量:-

我们经常在程序中使用一些常量。这些常量可能在程序中多次出现。例如，pi 的值应始终为 3.14。因此它

可以在程序中用作

```c
# define PI 3.14
```

# 被称为预处理器或编译器指令。

正如我们所知，PI 是一个常量，因此其值在整个程序中必须始终相同。符号常量也称为常量标识符。以下规则适用于 # define 语句：

- 为了区分变量和符号常量，符号常量以大写形式书写。
- # 与单词 define 之间不留空白。
- define 与符号常量之间需要留一个空白。
- 符号名称不使用数据类型声明。
- #define 语句不以分号结尾。
- #define 语句可以在程序的任何位置出现，但必须在使用之前。通常它们在 main () 之前使用。

### 预处理器指令:-

预处理器顾名思义，是在源代码通过编译器之前对其进行处理的程序。

### C 预处理器:

预处理器是一组特殊语句，在编译过程开始时执行。这些被称为指令。

### 一些预处理器有:

- 1. #include.:- 用于包含头文件。
- 2 #define :- 该语句用于定义符号常量和宏：即等同于表达式的单个标识符。

### 例如:

```c
#include<stdio.h>
#define area length*width
main()
{
    int length, width;
    printf("enter length and width");
    scanf("      %d %d",&length,&width);
    printf("\n area is %d",area);
}
```

3. #if、#elif、#else 和 #endif 允许根据一个或多个真/假条件的值对源程序进行条件编译。它们也与 defined 运算符一起使用。

### 例如:

```c
#if defined(FOREGROUND)
    #define BACKGROUND 0
#else
    #define FOREGROUND 0
    #define BACKGROUND 7
#endif
```

4. #elif :- #elif 类似于控制语句中使用的 else – if 子句

- 5. #else:-
- 6 #endif
- 7 #ifdef :- #ifdef 等价于 #if defined()。
- 8. #ifndef:- #ifndef 等价于 #if!defined。 即 "if not defined"。
- 9. #undef:- #undef 指令“取消定义”符号常量或宏标识符；即，它抵消了 #define 指令的效果。

### 例如:

```c
#define FOREGROUND 7
#define BACKGROUND 0
main()
{
    ........
```

```c
#undef FOREGROUND
#undef BACKGROUND
}
```

**Mind Drill Note-** _#if、#ifdef、#ifndef 必须以 #endif 结尾._

### 运算符:-

预处理器还包括两个特殊运算符：defined # 和 ##。

### 字符串化运算符 (#):-

它允许宏定义中的形式参数转换为字符串。如果宏定义中的形式参数前面有此运算符，则相应的实际参数将自动用双引号括起来。

### 标记粘贴运算符 (##):-

它导致宏定义中的各个项目被连接起来，从而形成单个项目。

### 示例:

```c
#define display(i) printf("x" #i "=%f\n",x##i)
```

假设此宏通过编写    display(3); 来访问；

结果将是：     printf("x3=%f\n", x3);

因此表达式 x##i 成为变量 x3，因为 3 是参数 i 的当前值。

### 多选题:

|  |  |
|---|---|
| **1. 什么是预处理器指令？**<br>1. 编译器向程序员发送的消息。<br>2. 编译器向链接器发送的消息。<br>3. 程序员向预处理器发送的消息。 | **4. 头文件是：**<br>1. 包含标准库函数的文件。<br>2. 包含定义和宏的文件。<br>3. 包含用户定义函数的文件。 |

