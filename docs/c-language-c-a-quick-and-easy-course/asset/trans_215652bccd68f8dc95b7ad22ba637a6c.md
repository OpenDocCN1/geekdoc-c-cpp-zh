
这一行。`printf()` 中的字母 `'f'` 表示 `'formatted'`，因此它是一个格式化打印函数。在 `main()` 函数中，第 10 行和第 11 行调用了两个函数：`Symb()` 和 `print()`。每个调用都以分号结尾，这也是 C 和 Pascal 中所有指令的结束方式。读者请注意，声明（常量、函数或指令）不以分号结尾，注释结束处同样如此。用户自定义函数，例如 `Symb()`，通常以大写字母开头，以免与标准库函数混淆。

## 几点说明

大写字母。在 C 语言中，大写字母和小写字母是不同编码。因此，保留字如果写成大写形式，也可以用作变量，例如 `Auto`（对应保留字是 `auto`）。

错误消息。在大多数情况下，程序编译时给出的错误消息并不会真正指出问题的准确原因。随着经验积累，程序员会逐渐熟悉这些消息的含义。另一些情况下，真正的错误出现在光标所指行之前的代码中。

缩进。缩进是指程序行参差不齐地书写，有些行比另一些行缩进更多；它对机器几乎没有意义，但作为一种排版上的组织方式，目的是方便程序员自己或其他人阅读。例如，将左花括号与对应的右花括号对齐就很重要。为此，其他元素都需要适当缩进。

注意事项。除了要区分数字 0 与字母 'O'（这对刚接触计算机科学的人来说是个大问题）之外，在 C 中还要注意不要把比较相等（`= =`）与赋值（`=`）混用。符号 `=` 用于把右侧表达式的值存入左侧变量，例如 `x = 3*5;` 或 `y = cos(3.14);`。而符号 `==` 只用于条件中，且这类条件通常需要用括号括起来，这一点在之后学习 `if-else`、`while` 和 `do-while` 命令时会看到。另一个需要注意的方面与人体工程学有关，也就是鼠标的使用。一直用食指点击鼠标并不合适，食指不适合承受这种过重负担。如果你确实想始终用同一个手指点击，那就改用拇指，拇指更合适。无论如何，懂得让食指与其他手指分担工作的打字员中，并没有出现肌腱炎的病例。只用食指打字是极其不妥的。如果你没有练习过打字，可以买一个简单的练习程序（软件商店里有很多），并坚持练习几周。

## 练习

1) 编写一个程序，使用三次 `printf()` 打印出三个短句。

2) 编写一个程序，在 `main()` 中创建并使用一个名为 `Beep()` 的函数，声明为 `void Beep()`，其作用是一旦被调用就发出一声鸣响。鸣响是指在屏幕上打印编号为 7 的字符，因此你可以在函数的花括号内声明一个变量，例如 `char b = 7`，然后输出它（`% c`）。

## 第 3 章

### 声明

### `char`、`int`、`float` 及其他类型

虽然在某些语言中可以直接使用未经声明的变量，但在 C 语言中（与 Pascal 一样）这是不允许的。所有变量在使用前都必须声明类型，既可以在模块内的花括号中局部声明，也可以在模块外全局声明。

用于声明变量、函数或类型的数据类型如下：

| 类型 | 范围 | 字节数 |
|---|---|---|
| char | -128 到 +127 | 1 |
| double | 1.7E-308 到 1.7E+308 | 8 |
| float | 3.4E-38 到 3.4E+38 | 4 |
| int | -32768 到 +32767 | 2 |
| long | -2147483648 到 +2147483647 | 4 |
| long double | 1.7E-308 到 1.7E+308 | 8 |
| short | -32768 到 +32767 | 2 |
| unsigned char | 0 到 +255 | 1 |
| unsigned int | 0 到 +65535 | 2 |
| unsigned long | 0 到 +4294967295 | 4 |
| unsigned short | 0 到 +65535 | 2 |
| far | 指针 | 4 |
| *huge* | 指针 | 4 |
| *near* | 指针 | 2 |
| *void* | - | - |

表达式 `3.4E-38` 表示 3.4 乘 10 的负 38 次方，这就是著名的科学计数法。像 183000 这样的数可以写成 `1.83E+05`，因为小数点从最后一个零一直跳到第一个非零数字 1，移动了 5 位。

除了上面列出的类型之外，C 语言还包含一些类别的修饰符或称数据类型，有的很简单，有的比较复杂。它们是：

```c
enum name {int1, ..., intn}
auto type var;
register char var, or register int var;
extern type var;
static type var;
typedef type name;
const type name;
volatile type name;
struct name {type v1; type v2; ...; type vn;} vname;
union {type v1; type v2; ...; type vn} vname;
```

*enum* 类型是一个有序整数集合，其值依次为 0、1、2……在 *enum* 值 `{a, b, c, d}` 中，有 a = 0、b = 1、c = 2、d = 3；但在月份 *enum* `{January = 1, Feb, Mar, Apr}` 中，January = 1、Feb = 2，依此类推。

*auto* 类型声明一个局部变量，它只在函数被调用时有效。既然是在所讨论的函数内声明，它就已经是自动的，无需再额外说明。

*register* 类型会把变量放入处理器寄存器中，从而提高程序运行速度，但不能与指针一起使用。*extern* 变量类型在程序中供全局使用，必须声明在各模块之外。*static* 变量在程序执行期间保持其值不变。声明为 *const* 的名称在程序执行期间的任何时候都不能改变它的值。*volatile* 变量类型具有与 *const* 相反的性质。*signed* 修饰符用于 `int` 和 `char` 类型，其作用与 `unsigned` 相反；`unsigned` 用于声明无符号变量。

`typedef` 关键字用于在程序中创建新类型。在 `typedef long double Value` 中，标识符 `Value` 可以用来声明 `long double` 变量，例如 `Value x;`。

结构体 `struct` 的用法与 `enum` 类似，但它不仅能容纳整数元素，也不是按顺序列出这些元素，此外还能创建新类型。例如：

```c
struct Body{char n[80]; int age; float height;};
Body girl[20];
girl[5].age = 23;
```

这里用 `Body` 结构声明了 20 个 `girl` 变量，其中编号为 5 的 `girl` 的 `age` 被赋值为 23。

联合体 `union` 修饰符与 `struct` 有相同的语法，但它把不同类型存储在同一个内存位置上，并且同一时刻只能使用其中一个。例如：

```c
union Conj {int ; float v; unsigned char k;} trio;
```

在这个例子中，创建联合体的同时自动声明了一个名为 `trio` 的变量。我们也可以像前一段中声明 `girl` 变量那样来处理。

下面是一个示例程序，说明变量声明及其相对大小：

### 示例程序 #3

```c
/* Program “Variable.cpp” */
#include <stdio.h>
#define PI 3.1415926
int i; long k; short j; char c; unsigned int ui;
unsigned long uk; unsigned short uj; unsigned char uc;
float fl; double db; long double ld;
main()
{

i=PI*(-1E4); k=-PI*(-1E5); j=i/30000; ui=-i; uk=-k;
uj=j; uc=c; fl=PI; db=fl*(1E-103); ld=db;
printf("i=%d\t int\t %d bytes\n",i,sizeof(i));
printf("k=%d\t long\t ",k);
printf("%d bytes \n",sizeof(k));
printf("j=%d\t short\t %d bytes \n",j,sizeof(j));
printf("\nValor\ttype\tsize\n");
printf("c=%d\t char\t %d byte \n",c,sizeof(c));
printf("ui=%d\t uns int\t %d bytes \n",ui,sizeof(ui));
printf("uk=%d\t uns long ",uk);
printf("%d bytes\n",sizeof(uk));
printf("uj=%d\t uns short %d bytes\n",uj,sizeof(uj));
printf("uc=%d\t uns char %d byte\n",uc,sizeof(uc));
printf("fl=%f\t float\t %d bytes\n",fl,sizeof(fl));
printf("db=%e\t double\t %d bytes\n",db,sizeof(db));
printf("ld=%le\t long double ",ld);
printf("%d bytes\n",sizeof(ld));
}
```

练习修改：尝试删除几行 `printf()`，例如与 `long` 类型有关的三行。如果使用 Borland IDE，请将光标放在该行上，按住 Ctrl 键并按 `'y'`。第二项修改：程序使用了 `#define` 指令，它用于声明一个具有特定值的常量。这个常量通常写成大写字母。请把 `PI` 这个标识符换成其他常量，并使用不同的值。

## `printf()` 的格式化语句

在 `printf()` 和其他函数的括号内，我们会看到许多前面带有 `'%'` 或 `'\'` 的符号，它们分别表示替代字符和转义序列。下面是这些代码的表格：

| 代码 | 含义 | 代码 | 含义 |
|------|---------|------|---------|
| %c | 字符 | \f | 换页 |
| %d | 整数 | \n | 换行 |
| %e | 科学计数法 | \r | 回车 |
| %f | 浮点数 | \t | 水平制表符 |
| %g | %e 或 %f，取较短者 | \v | 垂直制表符 |
| %o | 八进制无符号 | \ | 反斜杠 |
| %s | 字符串 | \? | 问号 |
| %u | 十进制无符号 | \' | 撇号 |
