
```
fputs(str,stdout);
break;
case 'f':
l=va_arg(ap,double);
f_to_str(l,str);
fputs(str,stdout);
break;
case '%':
putchar('%');
break;
}
}
else
putchar(*p);
}
```

这里我们使用 int 在 va_arg 中提取 char 值，使用 double 提取 float 值。这是因为在可变数量参数的情况下，默认参数提升会被应用，即类型为 char 和 short int 的参数会被提升为 int，类型为 float 的参数会被转换为 double。因此，使用 int 来提取 char、short int 或 int，使用 double 来提取 float 或 double。

我们将函数 print 定义为 void 类型，如果需要，你可以像 printf() 一样返回输出的字符数。

函数 i_to_str() 和 f_to_str() 不能处理负数，因此在调用这些函数之前，我们需要为负数编写额外的条件，如下所示-
```
if ( k<0)
{
    k = -k; putchar('-');
}
```

## 14.8.1 将可变数量的参数传递给另一个函数

假设我们编写一个函数 func1()，它接受可变数量的参数，并且我们想将所有这些未命名参数传递给另一个函数 func2()。为此，函数 func2() 应该被声明为能够接受 va_list 类型的变量。
```
func1(int num, ...)
{
    va_list ap;
    va_start(ap,num);
    func2(num,ap);
    .....
    .....
}
func2(int num,va_list ap)
{
    ........
    ........
}
```

因此，在 func2() 内部无需声明 va_list 类型的变量，也不需要调用宏 va_start。变量 ap 可以在宏 va_arg 中使用以检索参数。但在 func2() 中，我们只能使用未命名参数一次，不可能再次调用 va_start 来重新遍历可变参数列表。现在我们举一个简单的例子来看看如何实现这一点。在程序 P14.9 中，我们制作了一个函数 sum()，它显示整数并返回其总和。现在我们将制作一个单独的函数 display() 来显示数字，并将初始化的参数指针发送到该函数。
```
/*P14.11 Program in which the variable length list is passed to another function*/
#include<stdio.h>
#include<stdarg.h>
int sum(int ,...);
void display(int,va_list);
main()
{
    printf("Total= %d\n",sum(2,99,68));
    printf("Total= %d\n",sum(3,11,79,32));
    printf("Total= %d\n",sum(5,23,34,45,56,78));
}
int sum(int num, ...)
{
    int i;
    va_list ap;
    int arg,total=0;
    va_start(ap,num);
    display(num,ap);
    for(i=0;i<num;i++)
    {
        arg=va_arg(ap,int);
        total+=arg;
    }
    va_end(ap);
    return total;
}
void display(int num,va_list ap)
{
    int i,arg;
    for(i=0;i<num;i++)
    {
        arg=va_arg(ap,int);
        printf("%d ",arg);
    }
}
```

库函数 vprintf 就是这样一个接受 va_list 类型变量的函数。它与 printf 函数类似，只是它接受 va_list 类型的变量而不是可变参数列表。printf 和 vprintf 的原型如下-
int printf ( const char *format [, argument, ...] );
int vprintf ( const char *format, va_list arglist);
类似地，vfprintf 和 vsprintf 与 fprintf 和 sprintf 类似，只是存在这一个区别。
int fprintf (FILE *stream, const char *format [, argument, ...]);

```
int vfprintf(FILE *stream, const char *format, va_list arglist);
int sprintf (char *buffer, const char *format [, argument, ...]);
int vsprintf(char *buffer, const char *format, va_list arglist);
```

现在我们将编写一个调试函数 error()，它将显示错误信息以及发生错误的文件名、函数名和行号。如果该函数只接受特定类型的固定数量参数，则用处不大，因为在不同时间错误信息可能需要显示不同变量的值。因此我们将其定义为可变参数函数。前四个参数是固定的，其中前三个分别代表文件名、函数名和行号。第四个参数是一个格式字符串，表示错误信息，与 printf() 函数的格式字符串类似。在此之后，我们可以有可变数量的参数，这些参数将根据格式字符串中存在的转换说明符（%d、%s 等）与错误信息一起写入。error() 函数的定义可以写成如下-
```
error(char *file,char *fname,int line,char *format, ...)
{
    va_list ap;
    va_start(ap,format);
    printf("ERROR : ");
    printf("File - %s ", file);
    printf("Function - %s ", fname);
    printf("Line - %d\n", line);
    vprintf(format,ap);
    printf("\n");
}
```

这里我们使用 vprintf 来打印错误信息以及可变数量的参数。现在假设该函数在文件 myfile.c 的函数 myfunc() 中于第 44 行被调用，如下所示-
```
myfunc()
{
    ........
    error(__FILE__,
"myfunc",__LINE__,"Value of a must be less than %d and greater than %d\n",100,5);
    ........
}
```

输出如下-
ERROR : File - c:\dir\myfile.c , Function - myfunc , Line - 44
Value of a must be less than 100 and greater than 5

如果我们想将输出发送到流 stderr，则可以在 error 函数的定义中使用 fprintf 和 vfprintf 代替 printf 和 vprintf。

## 14.9 lvalue 和 rvalue

有时我们会遇到使用术语 lvalue 和 rvalue 的编译器错误。可以出现在赋值运算符左侧的表达式称为 lvalue，只能出现在赋值运算符右侧的表达式称为 rvalue。

rvalue 的一些例子是-
- x+y*z
- monday（这里 monday 是一个枚举常量）
- &x（这里 x 是一个整数变量）
- arr（这里 arr 是数组的名称）

这些表达式的值可以在程序中使用，但不能被修改，我们不能将它们写在赋值运算符的左侧。如果我们尝试编写如下语句，将会得到 'lvalue required' 错误-
```
5 = x;
x+y*z = 12;
&x = p;
arr = ptr;
```

lvalue 的一些例子是-
- var（var 是一个整数变量）
- ptr（ptr 是一个指针）
- *ptr（ptr 是一个指针变量）
- emp（emp 是一个结构体变量）
- emp->salary（这里 emp 是一个结构体变量，salary 是其成员）
- arr[2]（arr 是一个 1-d 数组）

所有这些表达式都可以出现在赋值运算符的左侧和右侧，即我们可以在程序中使用它们的值，并且它们的值可以被修改。

## 14.10 C 程序的编译与执行

在程序被转换为可执行形式之前，它会经过不同的阶段。下面的图示显示了这些阶段-

### 14.10.1 预处理器

源代码是我们使用任何文本编辑器编写的代码，源代码文件扩展名为 '.c'。该源代码首先通过预处理器。预处理器展开此代码并将其传递给编译器。我们已在第 12 章讨论了预处理器的作用。

### 14.10.2 编译器

展开后的代码被传递给编译器。编译器将此代码转换为机器的汇编语言代码。

### 14.10.3 汇编器

该汇编语言由系统的汇编器转换为目标代码。目标文件名称与源文件相同。在 DOS 中，目标文件扩展名为 '.obj'，在 UNIX 中扩展名为 '.o'。

### 14.10.4 链接器

通常用 C 编写的程序都使用库函数。库函数是预编译的，其目标代码存储在扩展名为 '.lib'（或 '.a'）的库文件中。链接器将库函数目标代码与我们程序的目标代码合并。我们的程序可能还包含引用

![](img/a76c706396af8b310f291a5313a27079_473_0.png)

到在其他文件中定义的函数。链接器也将这些文件目标代码链接到我们的程序中。因此，链接器的任务是将我们程序的目标代码与其他文件或库函数的目标代码合并。链接器的输出是可执行文件。在 DOS 中，可执行文件与源代码文件同名，扩展名为 ‘.exe’，在 UNIX 中，可执行文件命名为 a.out 或使用 -o 选项指定的输出名称。

## 练习

```c
enum month{jan,feb,mar,apr,may};
main()
{
	enum month m;
	m++;feb;
	printf("%d\n", m);
}
```

```c
enum day{sum=1,mon,tue,wed};
main()
{
	enum day dl;
	printf("%d\n",mon);
	dl=mon+2;
	printf("%d\n",dl);
}
```

```c
struct tag{
```
