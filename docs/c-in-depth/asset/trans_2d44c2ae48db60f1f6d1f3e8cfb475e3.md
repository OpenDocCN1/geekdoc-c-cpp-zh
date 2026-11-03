
假设第一个文件的路径输入为-
c:\mydir\myfile.dat

```
(4) main()
{
    FILE *fptr;
    int ch;
    fptr=fopen("names.dat",'w');
    while((ch=fgetc(fptr))!=EOF)
        putchar(ch);
    fclose(fptr);
}
```

```
(5) main()
{
    char name[50];
    int empid;
    fprintf(stdout,"Enter your name : ");
    fgets(name,50,stdin);
    fprintf(stdout,"Enter your empid : ");
    fscanf( stdin,"%d",&empid );
    fprintf(stdout,"Your empid is : %d", empid);
    fputc('\n',stdout);
    fprintf(stdout,"Your name is : ");
    fputs(name,stdout);
}
```

```
(6) main()
{
    FILE *fptr;
    char str[80];
    fptr=fopen("test.txt","r");
    while(fgets(str,80,fptr)!=EOF)
        puts(str);
}
```

```
(7) main(int argc,char *argv[ ])
{
    int i, sum=0;
    for(i=1;i<argc;i++)
        sum=sum+argv[i];
    printf("%d\n",sum);
}
```

假设可执行文件的名称为 add 且在命令行中调用方式为-
add 2 4 6 8

## 编程练习

- 1. 编写一个程序将文件复制到另一个文件，使得空白行不写入新文件。
- 2. 编写一个程序将文件的全部小写字符转换为大写。

- 3. 编写一个程序显示文件中字母和数字字符的总数量。
- 4. 编写一个程序从文件中删除所有注释。假设注释以双斜杠（ // ）开始并持续到行尾。
- 5. 编写一个程序将任意数量的文件连接起来并将输出写入目标文件。
- 6. 编写一个程序在文件中插入行号和页码。
- 7. 考虑以下结构
- struct {
- char name;
- int age;
- int sal;
- }
- 编写一个程序将此结构的 10 条记录存储在文件中并按 name 和 age 排序，其中 name 为主键，age 为次要键。
- 8. 修改程序 P11.21，使待删除的记录被标记为已删除，并编写一个函数从文件中物理删除已标记的记录。

```
struct {
char name;
int age;
int sal;
}
```

编写一个程序将此结构的 10 条记录存储在文件中并按 name 和 age 排序，其中 name 为主键，age 为次要键。

8. 修改程序 P11.21，使待删除的记录被标记为已删除，并编写一个函数从文件中物理删除已标记的记录。

## 答案

- (1) 该程序将显示文件的内容，并在到达文件末尾时进入无限循环，因为 ch 的数据类型为 unsigned char，而 EOF 的值为 -1 为有符号数。
- (2) If value love there cannot be..
由于我们以文本模式读取，所以 26 被视为文件结束字符，其后的任何文本都不会被读取。
- (3) 打开第二个文件时出错。在字符串常量内部，反斜杠被视为转义字符，因此在打开第二个文件时我们应在路径名中使用双反斜杠。第一个文件的名称不是字符串常量，因此无需在其中输入双反斜杠。
- (4) mode 的值应使用双引号括起来，因为它是一个字符串。
- (5) 当使用 stdout 调用 fprintf()、fputc() 时，它们分别等同于 printf()、putchar()。当使用 stdin 调用 fscanf()、fgets()、fgetc() 时，它们分别等同于 scanf()、gets() 和 getchar()。
- (6) fgets() 在文件结束或出错时不会返回 NULL，而是返回 EOF。整个文件的内容将被显示，然后 fgets() 在文件末尾返回 NULL，但循环条件检查 EOF，因此最后一行将被无限显示。
- (7) 命令行参数以字符串形式存储，因此我们必须使用 atoi() 函数将其转换为整数。正确的语句应为 sum = sum + atoi(argv[1]);

## 第 12 章

### C 预处理器

C 具有一种特殊的预处理器功能，使其区别于没有此类功能的其他高级语言。使用预处理器的一些优点是-

- 程序的可读性得到提高。
- 程序修改变得容易。
- 使程序具有可移植性和高效性。

我们知道我们编写的代码由编译器翻译成目标代码。但在编译之前，代码会经过 C 预处理器。预处理器扫描整个源代码并对其进行修改，然后再交给编译器。

![](img/a76c706396af8b310f291a5313a27079_392_0.png)

以符号 # 开头的行称为预处理器指令。当预处理器找到以符号 # 开头的行时，它将其视为自己的命令并据此工作。所有指令都由预处理器执行，编译器不会接收任何以 # 符号开头的行。预处理器指令的一些特性是-

- 每个预处理器指令都以 # 符号开头。
- 一行上只能有一个指令。
- 指令末尾没有分号。
- 要在下一行继续指令，应在行尾放置反斜杠。
- 预处理器指令可以放置在程序的任何位置（函数内部或外部），但通常写在程序的开头。
- 指令从出现的位置起一直有效到程序结束。

预处理器指令执行的主要功能是-

- 1. 简单宏替换
- 2. 带参数的宏
- 3. 条件编译

### 4. 包含文件

### 5. 错误生成、pragmas 和预定义宏名称

执行这些功能的预处理器指令如下所示-

- #define #else #error
- #if #elif #line
- #ifdef #endif #pragma
- #ifndef #undef

有三个运算符与这些指令一起使用-

- Defined 运算符 - defined( )
- 字符串化运算符 - #
- 标记粘贴运算符 - ##

除了通过指令提供的功能外，预处理器执行的另一项重要任务是将其中的每个注释替换为单个空格。

### 12.1 #define

我们已经使用过此指令来定义符号常量。一般语法是-

```
#define macro_name macro_expansion
```

这里 macro_name 是任何有效的 C 标识符，通常用大写字母表示以区别于其他变量。macro_expansion 可以是任何文本。macro_name 和 macro_expansion 之间需要一个空格。C 预处理器用 macro_expansion 替换 macro_name 的所有出现。例如-

```
#define TRUE 1
#define FALSE 0
#define PI 3.14159265
#define MAX 100
#define RETIRE_AGE 58
```

C 预处理器在 C 源代码中搜索 macro_name 并用 macro_expansion 替换它

例如，无论代码中出现宏名 TRUE 的位置，都将被 1 替换。这类常量称为符号常量。这些常量提高了程序的可读性。例如，使用名称 PI 比使用其本身的值更好。此外，如果在一段时间后我们决定更改常量的值，则只需在一个地方进行更改。例如，如果我们决定将 RETIRE_AGE 从 58 增加到 60，则只需更改 #define 指令即可。如果我们没有定义此常量，则必须将每次出现的 58 替换为 60。我们已经利用此功能来定义数组的大小。

我们也可以在 macro_expansion 的位置定义任何字符串常量。

```
/*P12.1 Program to show that macro expansion can be a string constant*/
#include <stdio.h>
#define MSG "I understand the use of #define\n"
main()
{
printf(MSG);
}
```

### 输出：

I understand the use of #define

C 预处理器搜索宏名 MSG 并在 printf() 中替换消息 "I understand the use of #define\n"。

我们有各种各样的宏扩展。以下是更多示例-

```
#define AND &&
#define OR ||
#define BEGIN main(){
#define END }
#define INFINITE while( 1 )
#define NEW_LINE printf("\n");
#define ERROR printf("An error has occurred\n");
```

最后两个指令中有一个分号。此分号只是 macro_expansion 的一部分。现在每当我们在程序中写 NEW_LINE 或 ERROR 时，它们将被 printf 调用和终止分号替换。

请记住，C 预处理器将简单地用 macro_expansion 替换 macro_name，而 macro_expansion 可以是任何文本。因此，我们有责任确保替换后生成的代码在 C 中有效。例如，如果我们像这样定义宏 MAX-

```
#define MAX 5;
```

现在考虑以下声明语句-

```
int arr[MAX];
```

这将被预处理器翻译为-

```
int arr[5];
```

这在 C 中是无效的。

如果 macro_name 出现在字符常量、字符串常量或注释中，则不会被替换而是保持原样。例如-

```
#define SUN 2
#define WINDOWS 3
printf("Rays of SUN are coming through the WINDOWS");
```

这里字符串内部不会进行替换。

也可以在没有 macro_expansion 的情况下定义宏。例如-

```
#define TEST
```

这用于编译指令中，预处理器只需要知道宏是否已定义。

### 12.2 带参数的宏

#define 指令也可以用于定义带参数的宏。一般语法是-

```
#define macro_name(arg1, arg2, .....) macro_expansion
```
