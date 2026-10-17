
默认情况下，第一个名称的值为 0，第二个名称的值为 1，第三个名称的值为 2，以此类推。但你可以通过添加初始化器为名称赋予特定值。例如，在以下枚举中，`green` 将具有值 5。

```cpp
enum color { red, green=5, blue };
```

这里，`blue` 将具有值 6，因为每个名称的值都比前一个名称大一。

## 6. 变量类型

变量为我们的程序提供了命名的存储，我们的程序可以操作它。C++ 中的每个变量都有特定的类型，这决定了变量内存的大小和布局；可以存储在该内存中的值的范围；以及可以应用于变量的操作集。

变量名可以由字母、数字和下划线字符组成。它必须以字母或下划线开头。大写和小写字母是不同的，因为 C++ 是区分大小写的。

C++ 中有以下基本变量类型，如上一章所述：

| Type | Description |
|---|---|
| `bool` | Stores either value true or false. |
| `char` | Typically a single octet (one byte). This is an integer type. |
| `int` | The most natural size of integer for the machine. |
| `float` | A single-precision floating point value. |
| `double` | A double-precision floating point value. |
| `void` | Represents the absence of type. |
| `wchar_t` | A wide character type. |

C++ 还允许定义各种其他类型的变量，我们将在后续章节中介绍，如 `Enumeration`、`Pointer`、`Array`、`Reference`、`Data structures` 和 `Classes`。

以下部分将介绍如何定义、声明和使用各种类型的变量。

### C++ 中的变量定义

变量定义告诉编译器在何处以及为变量创建多少存储空间。变量定义指定数据类型，并包含一个或多个该类型的变量列表，如下所示：

```cpp
type variable_list;
```

这里，`type` 必须是有效的 C++ 数据类型，包括 `char`、`wchar_t`、`int`、`float`、`double`、`bool` 或任何用户定义对象等，而 `variable_list` 可能由一个或多个用逗号分隔的标识符名称组成。以下是一些有效的声明：

```cpp
int   i, j, k;

char  c, ch;

float f, salary;

double d;
```

行 `int i, j, k;` 同时声明并定义了变量 i、j 和 k；它指示编译器创建名为 i、j 和 k 的 int 类型变量。

变量可以在其声明中初始化（赋予初始值）。初始化器由等号后跟常量表达式组成，如下所示：

```cpp
type variable_name = value;
```

一些示例是：

```cpp
extern int d = 3, f = 5;    // declaration of d and f.
int d = 3, f = 5;             // definition and initializing d and f.
byte z = 22;                 // definition and initializes z.
char x = 'x';                // the variable x has the value 'x'.
```

对于没有初始化器的定义：具有静态存储期的变量隐式初始化为 NULL（所有字节的值为 0）；所有其他变量的初始值未定义。

### C++ 中的变量声明

变量声明向编译器保证存在具有给定类型和名称的变量，以便编译器可以在不需要变量完整细节的情况下继续编译。变量声明仅在编译时有意义，编译器在程序链接时需要实际的变量声明。

当你使用多个文件并且在其中一个文件中定义变量，该变量将在程序链接时可用时，变量声明很有用。你将使用 `extern` 关键字在任何位置声明变量。你可以在 C++ 程序中多次声明变量，但在文件、函数或代码块中只能定义一次。

**Example:**

尝试以下示例，其中变量已在顶部声明，但在 main 函数中定义：

```cpp
#include <iostream>

using namespace std;

// Variable declaration:
extern int a, b;
extern int c;
extern float f;

int main ()
{
   // Variable definition:
   int a, b;
   int c;
   float f;

   // actual initialization
   a = 10;
   b = 20;
   c = a + b;

   cout << c << endl ;

   f = 70.0/3.0;
   cout << f << endl ;

   return 0;
}
```

当上述代码被编译和执行时，它会产生以下结果：

```
30

23.3333
```

相同的概念适用于函数声明，在声明时提供函数名，其实际定义可以在其他任何地方给出。例如：

```cpp
// function declaration
int func();

int main()
{
    // function call
    int i = func();
}

// function definition
int func()
{
    return 0;
}
```

### 左值和右值

C++ 中有两种表达式：

- `lvalue`：引用内存位置的表达式称为“左值”表达式。左值可以出现在赋值的左侧或右侧。

- `rvalue`：术语 rvalue 指存储在内存中某个地址的数据值。rvalue 是一个不能为其赋值值的表达式，这意味着 rvalue 只能出现在赋值的右侧，而不能出现在左侧。

变量是左值，因此可以出现在赋值的左侧。数字字面量是右值，因此不能被赋值，也不能出现在左侧。以下是有效语句：

```cpp
int g = 20;
```

但以下不是有效语句，会产生编译时错误：

```cpp
10 = 20;
```

## 7. 变量作用域

作用域是程序的一个区域，大致来说，变量可以在三个地方声明：

- 在函数或块内部声明，称为局部变量，

- 在函数参数的定义中声明，称为形式参数。

- 在所有函数之外声明，称为全局变量。

我们将在后续章节学习什么是函数及其参数。这里让我们解释一下局部变量和全局变量。

### 局部变量

在函数或块内部声明的变量是局部变量。它们只能被该函数或代码块内部的语句使用。局部变量对函数外部不可见。以下是使用局部变量的示例：

```cpp
#include <iostream>

using namespace std;

int main ()
{
   // Local variable declaration:
   int a, b;
   int c;

   // actual initialization
   a = 10;
   b = 20;
   c = a + b;

   cout << c;

   return 0;
}
```

### 全局变量

全局变量在所有函数之外定义，通常位于程序顶部。全局变量将在程序的整个生命周期内保持其值。

任何函数都可以访问全局变量。也就是说，在其声明之后，全局变量可在整个程序中使用。以下是使用全局变量和局部变量的示例：

```cpp
#include <iostream>

using namespace std;


// Global variable declaration:
int g;


int main ()
{
    // Local variable declaration:
    int a, b;


    // actual initialization
    a = 10;

    b = 20;

    g = a + b;


    cout << g;


    return 0;
}
```

程序中局部变量和全局变量可以同名，但函数内部局部变量的值会优先。示例：

```cpp
#include <iostream>

using namespace std;


// Global variable declaration:
int g = 20;
```

在用十进制形式表示时，必须包含小数点、指数或两者，而在用指数形式表示时，必须包含整数部分、小数部分或两者。有符号指数由 `e` 或 `E` 引入。

以下是一些浮点字面量的示例：

```cpp
3.14159       // Legal
314159E-5L    // Legal
510E          // Illegal: incomplete exponent
210f          // Illegal: no decimal or exponent
.e55          // Illegal: missing integer or fraction
```

### 布尔字面量

布尔字面量有两个，它们是标准 C++ 关键字的一部分：

- 表示真的 `true` 值。

- 表示假的 `false` 值。

你不应认为 `true` 的值等于 1，`false` 的值等于 0。

### 字符字面量

字符字面量用单引号括起来。如果字面量以 `L` 开头（仅大写），它是宽字符字面量（例如 `L'x'`），应存储在 `wchar_t` 类型的变量中。否则，它是窄字符字面量（例如 `'x'`），可以存储在简单的 `char` 类型变量中。

字符字面量可以是普通字符（例如 `'x'`）、转义序列（例如 `'\t'`）或通用字符（例如 `'\u02C0'`）。

在 C++ 中，某些字符在前面加上反斜杠时会有特殊含义，用于表示换行（`\n`）或制表符（`\t`）等。这里列出了一些转义序列代码：

| 转义序列 | 含义 |
|---|---|
| `\\` | `\` 字符 |
| `\'` | `'` 字符 |
| `\"` | `"` 字符 |
| `\?` | `?` 字符 |
| `\a` | 警报或铃声 |
| `\b` | 退格 |
| `\f` | 换页 |
| `\n` | 换行 |
| `\r` | 回车 |
| `\t` | 水平制表 |
| `\v` | 垂直制表 |
| `\ooo` | 一到三位八进制数 |
| `\xhh...` | 一位或多位十六进制数 |

以下是展示一些转义序列字符的示例：

```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello\tWorld\n\n";
    return 0;
}
```

当上述代码被编译和执行时，会产生以下结果：

```text
Hello   World
```

### 字符串字面量

字符串字面量用双引号括起来。字符串包含与字符字面量相似的字符：普通字符、转义序列和通用字符。

你可以使用字符串字面量将长行拆分为多行，并用空白分隔。

以下是一些字符串字面量的示例。三种形式都是相同的字符串。

```cpp
"hello, dear"

"hello, \
dear"

"hello, " "d" "ear"
```

### 定义常量

在 C++ 中定义常量的有两种简单方法：

- 使用 `#define` 预处理器。

- 使用 `const` 关键字。

### #define 预处理器

使用 `#define` 预处理器定义常量的形式如下：

```cpp
#define identifier value
```

以下示例详细解释了它：

```cpp
#include <iostream>
using namespace std;

#define LENGTH 10
#define WIDTH 5
#define NEWLINE '\n'

int main()
{
    int area;
    area = LENGTH * WIDTH;
```

## 9. 修饰符类型

C++ 允许 `char`、`int` 和 `double` 数据类型在其前面有修饰符。一个修饰符用于改变基本类型的含义，使其更精确地满足各种情况的需求。

数据类型修饰符列在这里：

- `signed`

- `unsigned`

- `long`

- `short`

修饰符 `signed`、`unsigned`、`long` 和 `short` 可以应用于整数基本类型。此外，`signed` 和 `unsigned` 可以应用于 `char`，`long` 可以应用于 `double`。

修饰符 `signed` 和 `unsigned` 也可以用作 `long` 或 `short` 修饰符的前缀。例如，`unsigned long int`。

C++ 允许声明 `unsigned`、`short` 或 `long` 整数的简写符号。你可以简单地使用 `unsigned`、`short` 或 `long`，而无需 `int`。它自动隐含 `int`。例如，以下两个语句都声明了无符号整数变量。

```cpp
unsigned x;

unsigned int y;
```

要理解 C++ 如何解释有符号和无符号整数修饰符之间的差异，你应该运行以下简短程序：

```cpp
#include <iostream>

using namespace std;

/* This program shows the difference between
 * signed and unsigned integers.
 */
int main()
{
    short int i;          // a signed short integer
    short unsigned int j;  // an unsigned short integer

    j = 50000;

    i = j;
    cout << i << " " << j;

    return 0;
}
```

运行此程序时，输出如下：

```text
-15536 50000
```

上述结果是因为表示 50,000 的短无符号整数的位模式被短整数解释为 -15,536。

### C++ 中的类型限定符

类型限定符提供了有关它们所前置变量的额外信息。

| 限定符 | 含义 |
|---|---|
| `const` | 类型为 `const` 的对象在程序执行期间不能被更改 |
| `volatile` | `volatile` 修饰符告诉编译器变量的值可能以程序未明确指定的方式被更改。 |
| `restrict` | 由 `restrict` 限定的指针最初是访问其所指向对象的唯一手段。只有 C99 才添加了名为 restrict 的新类型限定符。 |

## 10. 存储类

存储类定义了变量和/或函数在 C++ 程序中的作用域（可见性）和生命周期。这些说明符位于它们修饰的类型之前。在 C++ 程序中可以使用的存储类有：

- `auto`

- `register`

- `static`

- `extern`

- `mutable`

### auto 存储类

`auto` 存储类是所有局部变量的默认存储类。

```
{
    int month;
    auto int month;
}
```

上面的示例定义了两个具有相同存储类的变量，`auto` 只能用于函数内部，即局部变量。

### register 存储类

`register` 存储类用于定义应存储在寄存器中而不是 RAM 中的局部变量。这意味着该变量的大小最大等于寄存器大小（通常为一个字），并且不能对其应用一元 `&` 运算符（因为它没有内存位置）。

```
{
    register int miles;
}
```

`register` 应仅用于需要快速访问的变量，例如计数器。还应注意，定义“register”并不表示变量一定会存储在寄存器中。它表示该变量可能会根据硬件和实现限制存储在寄存器中。

### static 存储类

`static` 存储类指示编译器在程序的生命周期内保持局部变量存在，而不是在每次进入和离开作用域时创建和销毁它。因此，将局部变量设为 `static` 可以使它们在函数调用之间保持其值。

`static` 修饰符也可以应用于全局变量。此时，它会使该变量的作用域限制在声明它的文件内。

在 C++ 中，当 `static` 用于类数据成员时，它会使该成员只有一份副本，由其类的所有对象共享。

```cpp
#include <iostream>

// Function declaration
void func(void);

static int count = 10; /* Global variable */

main()
{
    while(count--)
    {
        func();
    }
    return 0;
}
// Function definition
void func( void )
{
    static int i = 5; // local static variable
    i++;
    std::cout << "i is " << i ;
    std::cout << " and count is " << count << std::endl;
}
```

当上述代码被编译和执行时，它产生以下结果：

```text
i is 6 and count is 9

i is 7 and count is 8
```
