
# 面向软件开发者的现代 C++：严肃的 C++ 开发

## 前言

这是一本关于使用现代 C++ 进行严谨软件开发的书籍。它是我开发 C++ 时首选的桌面参考书。我希望你也能以这种崇高的眼光来看。

本书分为八大部分部分。第一部分是 C 语言快速复习。假设读者熟悉 C 语言。第二部分介绍 C++。这是 C++11 之前的 C++。接下来的四个章节讨论了 C++11、C++14、C++17 以及最新标准 C++20 的重要特性。随后是一个章节讨论了 C++ 标准库中的重要函数。下一部分专门介绍 GNU C++ 编译器和 GNU 调试器。最后一部分查看了一些杂杂主题。

书中讨论的每一个重要的 C++ 特性都配有一个简短的 C++ 程序，用于演示该特性的工作原理。你可以将这些示例复制并粘贴到 `wandbox` (`https://wandbox.org/`) 中，然后编译并运行。

本书可以顺序阅读，也可以直接查看感兴趣的话题。

前言的剩余部分仅是我对 C++ Web 应用的一些个人见解漫述。C++ Web 应用开发是过时的吗？你可以安全地跳过前言的这部分。

## C++ 之路之旅

当我上大学时，我有一个朋友喜欢说 *我用 C 语言思考*。他显然非常喜欢 C。在 C 诞生 40 多年后，C 仍然非常流行。很多人真的非常喜欢 C。看来 C 对大脑的认知负载非常小；C 很容易进入大脑。

但 C 也有它的局限性。几年前，我曾用 C 开发一个深度神经网络。在写了大约 30,000 行代码后，我开始发现处理应用程序变得困难。这不是对该语言的批评，而是观察到 C 语言在构建大型应用程序方面的缺陷。

这正是 C++ 发挥作用的地方。C++ 提供了构建极其大型应用程序的结构。构建百万行的应用程序是可行的。这完全归于类、函数重载、运行时多态和模板等特性。这些特性非常灵活，可以处理非常复杂的领域问题。

但这并不是说 C++ 是完美的。每一个新的 C++ 版本都带来了改进，例如 `static_assert`、`constexpr`、`constinit`、`enum`、`auto`、`noexcept`、`nodiscard`。C++ 委员会意识到了这些问题。C++ 的正确性构造正在不断扩展。

C++ 并不是 Web 语言。这是一个关于互联网的经常出现的谬言。这在过去可能是正确的，但现在不是了。基于动态语言的 Web 框架被认为是开发 Web 应用的最佳环境。

*(注：由于原文文本中存在大量重复的段落，译文已根据要求进行了去重处理，确保不重复输出原文内容。)*

## 理论实践

我想通过一个生产环境质量的 C++ Web 应用程序来验证我的怀疑。由于我是一名律师，我使用 Drogon C++ 框架开发了 `https://truelawdocs.com`。这是一个用于文档生成的多线程应用程序。花费了大约四个月的兼职时间。该应用程序使用 Cassandra NoSQL 数据库进行文档存储。对于像 TrueLawDocs 这样的应用来说，这显然是大材小用。由于我之前没有任何 Cassandra 经验，Cassandra 减慢了开发周期。我想学习 Cassandra 是假设我未来可能需要这种列式 NoSQL 数据库。我非常喜欢 Cassandra，它的设计非常好。

TrueLawDocs 有一个使用 Bootstrap、Vue、Javascript 和 CSS 开发的前端。C++ 后端与前端通过 websocket 通信。正如你所看到的，TrueLawDocs 具有强解耦的架构。

除了 Drogon 框架和 C++ 标准库外，使用的唯一库是 `nlohmann/json`（一个 C++ JSON 库）、`AES.hpp`（一个仅头文件的 C++ 加密库）、用于 Cassandra 的 DataStax C 库、`ASAN`（地址消毒器）和 `UBSAN`（未定义行为消毒器）。第三方库就这些。其他所有内容都是硬编码。

为了与 Stripe 集成支付，使用了 `LibCurl` 库与 Stripe 支付服务器交互。Stripe 不支持 C++，且没有提供集成 C++ 程序的示例代码。TrueLawDocs C++ 代码与 Stripe 服务器的集成体现了 C++ 的原生强大。

整体开发体验非常愉快。Drogon 源码易于理解；它是由一位现代 C++ 大师编写的。

TrueLawDocs 包括 Cassandra 运行在从沙迦一家公司租用的每月 7 美元的 VPS 上。

## 经验教训

在担任 Rails 应用程序合同期间，我很少遇到对其他编程语言有广泛经验的开发者。他们通常只了解自己的框架。在十年的合同工生涯中，我从未遇到过一个精通 C++ 的 Rails 程序员。

动态类型 Web 语言流行的原因之一是它们容易学习。你可以在三个月内掌握 Rails。相比之下，除非用该语言编程了大约两年，否则无法获得 C++ 的合理熟练。现代 C++ 的学习曲线非常陡。遗憾的是，这是不可避免的。

另一个因素是经济因素。用动态类型语言构建的 Web 应用程序依赖廉价劳动力。财富 500 公司使用大量外国承包和软件质量测试人员来开发和维护他们的应用程序。在我看来，这说明了动态类型语言在 Web 开发中的局限性。如果没有这些廉价资源，开发模型将转向节省昂贵、高质量的人力资源。

在开发 TrueLawDocs 所花费的调试工作方面，我估计 75% 的精力用于调试 Vue 和 Javascript 前端。C++ 提供了卓越的调试工具，因此调试后端是轻而易举。在后端调试基础设施方面，我依赖于大量使用 Debug 宏、`ASAN`（检测内存错误）、`UBSAN` 和 `GDB` 调试器。使用 Sonlint 检查语法。

开发环境是 Linux Mint（经典 GNOME 界面，带有 24 个打开虚拟窗口）。IDE 是 VisualCode。编译器套件是 GCC。编译和调试在终端中完成。一个 python 脚本执行“编译-链接-运行-调试”循环。终端始终开启着以 `tail` 调试输出。应用程序产生大量的调试信息。我投入了特殊精力生成高质量的调试输出。这使得追踪错误变得异常简单。用户验收测试是通过 Selenium 完成的。

正如你所推断的，我离开了 Rails。这是一个正确的决定。我一直在脑海中考虑开发一个 C++ 的 YouTube 克隆项目。像 Rails 一样，我最终厌倦了谷歌的审查。总之，这就是 C++ 的力量。

感谢您的诚心考虑。

Karan Singh

## C 语言复习

### 声明与定义

在 C 和 C++ 中，标识符是用户分配给程序元素的名称，例如变量、类型、模板、类、函数或命名空间。

变量存储一个值。在 C 和 C++ 中，变量在使用之前之前必须进行声明。声明指定了变量的类型和名称。声明隐式地指定了变量存储一个值所需的内存量。例如：

```
int x;
```

声明 `x` 是一个 `int` 类型的变量，这种类型的变量需要 32 位内存。

函数声明由函数返回类型、函数名和函数参数的类型组成。例如：

```
int foo(int x, int y);
```

变量定义会创建一个变量并可能为该变量设置（赋值）值：

```
int x               // 变量 x 的声明
x = 5;             // 变量 x 的定义
```

此定义将值 5 放入分配给变量 `x` 的内存中。

声明和定义可以合并为一个语句。例如：

```

对于 `int`、`long`、`float` 和 `double` 等基础 C 和 C++ 类型，声明也是一种定义。但对于我们之后会遇到的更复杂类型，情况并非如此。
函数定义告诉编译器函数如何工作。它展示了由函数执行的指令：

### 语句终止

在 C 和 C++ 中，语句不通过换行符（'\n'）终止。它们通过分号（;）终止。因此，C 和 C++ 语句可以自由地跨行。

### 字面量

字面量是常量。C 有四种字面量：整数字面量（如 45）、浮点数字面量（如 3.12）、字符串字面量（如 "hello world"）以及字符字面量（如 'c'）。

字面量是直接表示值的程序元素。例如，509 是一个整数字面量或常量。

### 字符字面量
字符字面量是用单引号括的单个字符。如果单引号内有多个字符，将抛出错误。

| long long | LL or ll |

### C 和 C++ 中的变量作用域

变量作用域是指变量存在并可以访问的区域。

在 C 中，变量可以在三个地方进行声明：

- 在大括号分隔的块 `{ ... }` 内部（局部变量）
- 在函数的参数列表中
- 在所有函数之外（全局变量）

大括号对 `{}` 定义了一个块，在块内部声明的变量的作用域被限制在该块内。在 C 中，变量的作用域从其声明处开始。

C 和 C++ 实现了**词法作用域（lexical scope）**。这意味着任何变量的作用域都可以在编译时通过检查源代码确定。

**词法作用域**可以解释如下：假设编译器在代码块中遇到一个变量名，并想要知道该名称是否存在以及它的值。编译器首先检查当前块中是否有该名称的声明，如果没有找到，它会检查任何外层嵌套块，最后在全局作用域中查找该变量名。

下面的 C++ 程序展示了 C/C++ 的词法作用域：

```cpp
#include <iostream>

int value = 999;

void f()
{
    int value = 1;
    std::cout << "value in f - " << value << std::endl;
}
```

```cpp
{
  std::cout << "value in f - " << value << std::endl;
}
int main() {
{
  int value = 2;
  f();
  std::cout << "value in main - " << value << std::endl;
  return 0;
}
// output
value in f - 1
value in f - 999
value in main - 2
```

### C 语言：函数原型

#### 前向声明

以下程序将无法编译：

```cpp
#include <stdio.h>
int main() {
    printMe(5);
}
// printMe 在此处声明并定义
void printMe(int x) {
    printf("%d", x);
}
```

问题在于当编译器在 `main` 中遇到 `printMe` 语句时，它不知道 `printMe` 是什么，因为 `printMe` 尚未声明。这个问题可以通过在 `main` 之前包含 `printMe` 的定义，或者在使用之前包含 `printMe` 的声明来解决。

```cpp
#include <stdio.h>
void printMe(int);
int main() {
    printMe(5);
}
// printMe 的定义
void printMe(int x) {
```

这种对 `printMe` 的前向声明称为函数原型。

### void 类型

数据类型 `void` 表示没有值。如果函数没有接受任何参数，应该始终声明为 `void`。

```cpp
void foo(void);
void foo();
```

C 编译器将第一个原型解释为不接受任何参数且没有返回值。第二个声明被 C 编译器解释为不知道 `foo` 是否接受任何参数且没有返回值（C++ 编译器的行为则不同）。

### C 语言：C 风格强制转换

变量值以位序列存储。变量的数据类型告诉编译器如何将这些位转换为有意义的值。不同的数据类型可以用不同的方式表示“同一个”数字。例如，整数值 3 和浮点值 3.0 被存储为完全不同的位模式。

在 C 中，我们可以通过在变量或字面量前加上圆括号括起来的目标类型，将其从一种类型转换为另一种类型：

```cpp
float y = (float) 6/4;
```

这是一个类型转换的示例。编译器将把整数 6 转换为浮点数，然后将其除以 4 得到 1.25。注意，如果右侧没有出现浮点类型转换，则右侧将求值为 1，并将 1.0 赋值给 `y`。由于 `y` 是浮点类型，编译器会执行整数 1 到浮点类型的隐式类型转换。

C 同时也实现了函数风格强制转换：

其中 T 是某种类型。

```cpp
int x = int(3.14)          // 3.14 被转换为 int 类型。
```

我们在上面的示例中显示的类型转换是显式类型转换。然而，当目标类型与主体类型不同时，编译器会自动尝试进行隐式类型转换。隐式类型转换或自动类型转换会在三种情况下发生：

```cpp
float y = 5; // int 类型 5 转换为 float
```

```cpp
int myFunc(float p); // 调用 myFunc 时传入 int 参数。例如，myFunc(3)
```

函数的返回值被更改为不同的类型。

```cpp
float y = myFunc(5); // myFunc 返回整数类型
```

每当值从一种基本数据类型转换为另一种基本数据类型时，就会发生自动类型转换。

指针是一个存储另一个变量地址的变量。指针声明的语法为：

```cpp
int *ptr;
```

这表示 `ptr` 是一个指针，其值是一个 `int` 类型变量的地址。注意这只是一个声明，`ptr` 尚未初始化。假设我们有：

```cpp
int x = 5;
```

那么 `x` 的地址（`x` 存储的内存地址）是：

```
&x
```

**地址运算符 &** 获取变量 `x` 的地址。我们可以这样初始化 `ptr`（让 `ptr` 指向 `x`）：

```c
ptr = &x;
```

现在 `ptr` 包含了 `x` 的地址。我们可以通过以下方式获取 `ptr` 所指地址的值：

```c
```

这被称为解引用指针。`*` 是**解引用运算符**，获取指针所指向位置的值。

### 指针算术

指针变量可以进行递增和递减。增加会将指针变量的值设置为比当前指针值向前偏移（指向的数据类型大小）字节字节的位置。

在我们的示例中，指针指向 `int` 类型，其长度为 4 字节，因此 `++ptr` 指向当前位置向前 4 字节的位置。递减运算符也是如此。普通的加法和减法原理也类似。

```cpp
#include <iostream>
int main() {
    int x = 5;
    int *ptr1;
    int **ptr2;
    ptr1 = &x;
    ptr2 = &ptr1;
    int z = **ptr2;
    std::cout << z << std::endl;
}
```

# 结果

5

### C 语言：数组

数组是相同类型变量的集合，通过公共名称进行引用。数组中的特定元素通过索引访问。在 C 和 C++ 中，数组由连续的内存位置组成。最低地址对应数组的第一个元素，最高地址对应最后一个元素。数组可以有一维到多个维度。最常见的数组是空终止字符串，它仅仅是一个被包含在双引号内的字符序列，并以空字符（'\0'）结束。

#### 一维数组

此类类型的数组使用以下语法指定：

```c
type name[size];
```

在这里，`type` 声明数组的类型（即数组中每个元素的类型），`size` 定义了数组将包含的元素数量。数组必须显式声明，以便编译器在内存中为它们分配空间。这里有一个示例：

```c
int flowers[5];
```

数组元素通过中括号运算符 `([])` 和索引值访问，索引从 0 开始，直到但不包含数组的大小。索引 0 指向数组的第一个元素：

```c
int p = flowers[0];
int p = flowers[2]; // 第三个数组元素
```

C 和 C++ 不对数组进行边界检查。

#### 数组指针

在 C 和 C++ 中，数组名被定义为指向数组第一个元素的指针：

```cpp
int *p;
int sample[10];
p = sample;
```

我们也可以通过以下方式定义指向第一个元素的指针：

```c
p = &sample[0];
```

### 数组与双重间接 (** ptr)

考虑一个数组，其中每个元素都是一个空终止字符串：

```cpp
char* names[10];
names[0] = "hello";
...
names[9] = "world";
char* ptr = names;
```

`ptr` 是指向 `names` 数组的指针。`ptr = names` 和 `ptr = &names[0]` 是等价的。然而 `names[0]` 本身是一个指向空终止字符串的指针。因此 *ptr 是一个指向空终止字符串的指针*。因此，数组中的第一个字符串是 **ptr**。

由于如此，`char **ptr` 是指向空终止字符串数组的指针。`**ptr+1` 指向第二个空终止字符串。

#### 数组初始化器

在 C++ 中，我们可以如下初始化数组：

```cpp
int array[5] = {1, 2, 3, 4, 5};
```

初始化器的数量可以少于数组长度，在这种情况下，剩余的数组元素将被初始化为该数组类型的“零”。

#### 向函数传递一维数组

在 C 和 C++ 中，我们不能将整个数组作为参数传递给函数。然而，我们可以通过指定不带索引的数组名来传递数组指针。

```c
int main(void)
{
    int sample[10];
    func(sample);
}
```

数组名（不带索引）是数组第一个元素的指针。

接收数组的函数的形参数可以声明为指向数组数据类型的指针，也可以声明为有大小或无大小的数组。例如：

```c
func (int *p)
func (int m[10]);
func(int m[])
```

以上所有都是等价的。数组大小可以是任何值；例如，`func(int m[100000])` 也是有效的。函数参数列表中的数组参数只是语法糖，函数接收的是指向数组的指针。程序员负责确保不会发生缓冲区溢出。

#### 多维数组

多维数组可以使用以下语法指定：

```c
int m[6][8];              // 整数的二维数组
char s[7][3][5];      // 字符的三维数组
```

数组可以有任意数量的维度。

### C 语言：字符串



# C 和 C++ 实现了空终止字符串

`C` 和 `C++` 实现了空终止字符串。字符串是一个空终止字符数组（空值为 ASCII 0，表示为 `'\0'`）。因此，`C` 风格的空终止字符串是一个以空字符作为其最后一个最后一个元素的字符数组。这里有一个示例：

```c
"hello world"
```

`C` 编译器会自动在该字符串字面量的末尾添加一个空字符。包含在双引号内的字符序列被 `C` 编译器解释为常量字符字符串。常量字符串不能更改。

```c
char* str = "hello world";
str = 'z'; // 错误 - 尝试将 'h' 改为 'z'
```

声明一个存储空终止字符串的字符数组时，必须将其声明为比它可以包含的最大字符串长一个字符。即额外的字符 `'\0'`。

以下字符串声明都是等价的：

```c
char* str = "hello world";
char str[12] = "hello world";
char str[] = "hello world";
```

## 文件格式化输入

`fscanf` 函数从文本文件中读取数据并将数据放入变量中。文件中的数据元素必须用空格分隔。如果发生错误或尝试读取文件末尾，`fscanf` 将返回 `EOF`。这是一个示例：

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char name[1024];
    float length;
    int mass;

    fp = fopen("animals.txt", "r");
    while (fcanf(fp, "%s %f %d", name, &length, &mass) != EOF)
        printf("%s animal, %d lbs, %.1f meters\n", name, mass, length);

    fclose(fp);
}
```

## 写入文件

我们使用 `fopen("filename", "w")` 打开一个文件进行写入。如果文件已存在，它将被截断为长度 0。

文件读取函数 `getc`、`fgets` 和 `fscanf` 有对应的文件写入函数：`fputc`、`fputs` 和 `fprintf`。我们如下所示使用这些函数：

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    int x = 32;

    fp = fopen("output.txt", "w");
    fputs('B', fp);
    fputc('\n', fp);
    fprintf(fp, "x = %d\n", x);
    fputs("Hello, world!\n", fp);

    fclose(fp);
}
```

注意，由于 `stdout` 是指向 `FILE` 的指针，我们可以执行 `f = stdout`。

## 二进制文件

二进制文件的工作原理与文本文件非常相似，但 I/O 子系统不会对数据进行像文本文件那样的转换。对于二进制文件，我们得到原始字节流，它不会被 I/O 子系统转换。

要以二进制模式打开文件，我们在文件模式中添加 `'b'`（`'rb'` 或 `'wb'`）。最常用的函数是 `fread()` 和 `fwrite()`。这些函数从文件流读取或向其写入指定数量的字节。

## C 语言：内存分配

`C` 语言使用 `malloc()` 函数来分配内存。`malloc()` 将分配的字节数作为其唯一参数，并返回指向新分配连续内存块的 `void` 指针。`void` 类型指针可以转换为任何其他类型。如果无法分配内存，`malloc()` 返回 `NULL`。`malloc` 不初始化新分配的内存。

在我们完成内存的使用后，使用 `free()` 释放内存。这是一个示例：

```c
#include <stdlib>
// 从 void* 到 int* 的隐式类型转换
int *p = malloc(sizeof(int));
*p = 12;

printf("%d\n", *p);
free(p);
```

`calloc()` 与 `malloc()` 类似。它接收单个元素的大小和分配的元素个数。`calloc()` 将分配的内存初始化为 ASCII 空 字节（`"\0"`）。

```c
#include <stdlib>
int *p = calloc(sizeof(int), 10);
...
free(p);
```

`realloc()` 函数可用于缩小或扩大已分配的内存。`realloc` 接收指向已分配内存的指针和新内存分配的大小。它会扩大或缩小内存，并返回指向它的 `void` 指针。

```c
float *p = malloc(40);   // 分配 40 字节
...
float *new_p = realloc(p, 80);
```

## C 语言：存储类限定符

存储类限定符告诉编译器如何存储变量。`C` 语言有四种存储类限定符：

- `extern`
- `static`
- `register`
- `auto`

带有存储类限定符的变量声明方式如下：

```c
storage_class_specifier type variable_name;
```

### extern

`C` 和 `C++` 允许将大型程序拆分为多个文件，并对这些文件进行单独编译，然后链接在一起。由于由于，必须有一种方法告诉一个文件在其他文件中声明的变量。

变量声明声明了变量的名字和类型。变量定义会为变量分配存储。在大多数情况下，变量声明和定义是结合在一起的（例如 `int x = 5`）。但当我们在变量声明之前加上 `extern` 限定符时，我们告知编译器该变量是在另一个文件中声明的。

`extern` 的一个显著用法是在一个一个文件中声明所有的全局变量，并在其他文件中使用 `extern` 声明来访问这些变量。

示例：

文件 1

文件 2

```c
int x, y;           extern int x, y;
```

`extern` 限定符告诉编译器紧随其后的变量名已经在其他文件中声明过。换句话说，`extern` 让编译器知道这些全局变量的类型和名称，而无需再次为它们创建存储。当链接器链接两个目标文件时，所有对外部变量的引用都会被解析。

`extern` 关键字具有这种通用形式：

```c
extern type variable_name;
```

### 静态变量

与全局变量不同，静态变量在声明它的函数或文件外部是不可知的。此外，在函数内部声明的静态变量在函数调用之间保持其值。

#### 函数内部的静态变量

函数内部的静态局部变量在函数调用之间保留其值。

这是一个示例：

```c
int series(void)
{
    static int series_num;
    series_num = series_num+23;
    return series_num;
}
```

静态局部变量在函数调用之间保留其值。

#### 静态全局变量

将 `static` 限定符应用于变量，告知编译器该变量仅在声明它的文件中可见。



```c
int series(void)
{
    static int series_num;
    series_num = series_num+23;
    return series_num;
}
```

## 静态变量

将 `static` 限定符应用于变量，告知编译器该变量仅在声明它的文件中可见。这编译器可以可以以以以更更访问访问。

## 寄存器变量

寄存器类为编译器提供提示，局部变量将被频繁使用，因此应该放在 CPU 寄存器中内存。在 C 语言中，`register` 关键字已废弃。

## C 语言：const

`const` 是一个限定符，表示变量不可被修改。这是一个示例：

```c
const int x = 9;
```

这意味着 `x` 是一个整数且其值不能被改变。

```c
const int* p;
```

这意味着 `p` 是指向整数的指针且其指向的值不能被改变。

```c
int* const p;
```

这意味着指针 `p` 是一个常量，因此不能被递增。

## 函数中的 const

在函数中使用 `const` 特别重要。考虑以下情况：

```cpp
#include <stdio.h>
#include <iostream>

int main() {
    int x = 5;
    f(x);
}

void f(const int y) {
    y++;
    std::cout << y << std::endl;
}
```

`f` 接收整数 `x` 的 `const` 拷贝。此程序将无法编译，因为 `f` 尝试修改 `y`。

## C 语言：函数指针

尽管函数不是变量，但它们在内存中有物理位置。函数有一个包含其可执行代码的内存块。该内存块的起始地址是函数的入口，它是在调用函数时使用的地址。

函数内存块的起始地址可以赋值给指针变量。该变量随后被称为函数指针。可以通过函数指针调用函数。函数指针还允许向函数传递参数。

我们通过使用函数名（不带任何括号或参数）来获取函数的地址（函数所使用的内存的起始地址）。

假设我们要为一个接收一个 `char` 指针和一个整数作为参数并返回整数的函数指定函数指针。

```c
int (* func)(char* ch, int b)
```

`func` 是该类型函数的函数指针。表达式 `(* func)` 仅仅是编译器理解为表示函数指针的符号。编译器识别出 `func` 为指向函数的指针。`func` 可以赋值给任何具有 `char` 指针和 `int` 参数并返回 `int` 的函数。

假设我们有一个函数 `int pick(char*, int)`，那么我们可以将我们的 `pick` 函数赋值给函数指针 `func`：

`func = pick;`

这是一个具体的示例：

```c
#include <stdio.h>
#include <string.h>

// check 函数的正向声明
// 第三个参数是一个函数指针
void check(char *a, char *b, int (*cmp)(const char *, const char *));

int main(void)
{
    char s1[80] = "hello world";
    char s2[80] = "bye";

    // 声明一个函数指针
    int (*p)(const char *, const char *);

    // 将 strcmp 函数赋值给 p
    p = strcmp;
    check(s1, s2, p);
    return 0;
}

void check(char *a, char *b, int (*cmp)(const char *, const char *))
{
    printf("Testing for equality.\n");

    if (cmp(a, b))
        printf("Equal");
    else
        printf("Not Equal");
}
```

`check` 函数的实现

当调用 `check()` 函数时，传入了两个指针和一个函数指针作为参数。在 `check()` 内部，表达式 `(*cmp)(a, b)` 调用了由 `cmp` 指向的 `strcmp()`，并传递了参数 `a` 和 `b`。

## C语言：setjmp 和 longjmp

`setjmp()` 和 `longjmp()` 函数可以用于保存程序的执行上下文并在稍后的某个点恢复它。我们所说的执行上下文是指 CPU 寄存器状态、栈和分配的内存的状态。`setjmp()` 保存程序的执行上下文，而 `longjmp()` 恢复它。

`setjmp()` 和 `longjmp()` 可以跳转到程序的不同部分。实际用途包括跳出深度嵌套循环、调用错误处理以及跳转到命名的标签。所有这些都通过示例进行了解释：

```c
#include <setjmp.h>
#include <stdio.h>

void jumper(jmp_buf env) {
    printf("inside jumper\n");
    longjmp(env, 1);
    printf("after longjmp\n");
}

int main() {
    jmp_buf env;
    int ret = setjmp(env);
    if (ret == 0) {
        printf("setjmp executed\n");
    } else {
        printf("returned from longjmp\n");
        return 1;
    }
    jumper(env);
    return 0;
}
```

输出：

`setjmp executed`

`inside jumper`

## goto 语句

C 和 C++ 中的 `goto` 关键字是通过 `setjmp` 和 `longjmp` 实现的。`goto` 允许我们跳转到程序标签：

```c
#include <setjmp.h>
#include <stdio.h>

int main() {
    printf("hello world\n");
    goto foo_label;
    printf("1+1=2\n");

foo_label:
    printf("goodbye\n");
    return 0;
}
```

输出：

`hello world`

`goodbye`

## C语言：typedef

我们可以使用 `typedef` 关键字为现有数据类型定义新名称。通过 `typedef`，我们并没有实际上创建一个新的数据类型，而是为现有类型定义了一个新名称。

`typedef` 可以帮助使依赖于机器的程序更具可移植性。如果我们为程序中使用的每个依赖于机器的数据类型都定义了类型名称，那么在不同架构的机器上编译程序时，只需要修改 `typedef` 语句即可。

`typedef` 的语法如下：

```c
typedef old_type_name new_type_name;
```

例如：

```c
typedef float balance;
```

`balance` 只是 `float` 类型的另一个别名；既然 `balance` 已定义为一种类型，我们可以这样做：

```c
balance over_due;
```

`over_due` 是一个 `balance` 类型的变量。

## C语言：枚举

枚举（enumeration）是一种用户定义的类型，其值被限于一组命名的整数常量。此类类型的变量只能具有等于该类型指定的这些命名整数常量之一的值。

枚举的语法为：

```c
enum enum_name { enumeration list } variable_list;
```

枚举名（`enum_name`）和变量列表（`variable_list`）都是可选的。这里有一个示例：

```c
enum FILETYPE { FILE_NONE, FILE_C, FILE_ASM, FILE_OBJ } FileType;
```

关于枚举，需要理解的关键点是：枚举列表中的每个符号都是一个整数值。因此，它们可以用任何可以使用整数的地方。每个符号赋予的值比其前一个符号大 1。第一个枚举符号的值为 0。

这里有一个示例：

```c
enum coin { penny, nickel, dime, quarter, half_dollar, dollar };
```

```c
enum coin money
```

`enum coin` 是一个枚举类型，`money` 是一个 `enum coin` 类型的变量。注意，类型是 `enum coin` 而不是 `coin`。在 C++ 中，枚举名是一个完整的类型，因此我们可以这样声明变量 `money`：

```cpp
coin money
```

我们还可以声明带有特定枚举值的枚举：

```cpp
enum coin {penny, nickel, dime, quarter, half_dollar, dollar};
```

| `penny` | 0 |

|---|---|

| `nickel` | 1 |

| `dime` | 2 |

| `quarter` | 3 |

| `half_dollar` | 4 |

| `dollar` | 5 |

## 匿名枚举

一个匿名枚举的定义方式如下：

```c
enum { COLOR };
```

这与 `int` 相同，但我们无法获取它的地址。这在定义 `const` 时非常有用。匿名枚举实际上是一个编译时常量。

## C语言：size_t 和 sizeof

`size_t` 是一种无符号整数类型。在 `<stdio.h>` 和 `<stdlib.h>` 中定义。`size_t` 用于表示对象的大小。它是 `sizeof` 运算符的返回类型。`size_t` 保证足够大，能够容纳主机处理的最大整数。最大允许的大小取决于编译器。如果编译器是 32 位的，`size_t` 就是简单的 `unsigned int`；如果编译器是 64 位的，`size_t` 就是 `unsigned long long`。`size_t` 数据类型永远为负数。

## 编译时运算符 sizeof

`sizeof` 是一个一元运算符，用于返回其前的变量或括号内类型的长度（字节）。

```c
double f;
printf("%d", sizeof(f));
printf("%d", sizeof(int));
printf("%d", sizeof(double));
printf("%d", sizeof(struct Employee));
```

如果 `sizeof` 操作数是原生 C 或 C++ 类型，必须包含在括号内。`sizeof` 主要有助于生成依赖于内置数据类型大小的可移植代码。

结构体和联合体可以创建不同大小的变量。这些变量的实际大小随机器而变化。`sizeof` 运算符计算任何变量或类型的大小，并帮助消除程序中依赖机器的代码。该运算符在涉及结构体或联合体时特别有用。

## #define 指令

`#define` 指令指定一个标识符和一个字符序列（即一组字符）。每当在源文件中遇到该标识符时，字符序列就会被替换该标识符。`#define` 语句被称为宏。

该标识符被称为宏名（macro name），替换字符被称为宏替换内容（macro replacement）。该指令的一般形式为：

```
#define macro-name char-sequence
```

请注意，该语句末尾没有分号。宏名和字符序列之间可以有任意数量的空格，但一旦字符序列开始，它仅由换行符终止。

如果我们希望对单词 `LEFT` 使用值 0，对单词 `RIGHT` 使用值 1，我们可以声明这两个 `#define` 指令：

```
#define LEFT 0
#define RIGHT 1
```

这会导致预处理器在源文件中每次遇到 `LEFT` 宏名或遇到 `RIGHT` 宏名时，都将其替换为 0 或 1。

一旦定义了宏名，它就可以在其他宏名的定义中使用。例如：

```
#define ONE 1
#define TWO ONE + ONE
```

宏替换简单地将宏名替换为与其关联的字符序列。

**注意：** 如果宏名位于引号内，则不会发生宏名替换。

如果字符序列超过一行，我们可以在行末尾放置一个反斜杠来在下一行继续编写，如下所示：

```
#define LONG_STRING "this is a very long \
string that is used as an example"
```

按照惯例，使用大写字母表示宏名。将所有程序宏放在一个单独文件中也是一种惯例。

宏的常见用途之一是标识“魔术数字”（magic numbers）。

使用 `#define` 宏的一个问题是，编译器永远看不见宏，因为预处理器在将文件移交给编译器之前执行了宏替换。例如，如果我们指定了 `#define GREEN`，编译器将永远看不到 `GREEN` 标识符。此外，如果我们未能包含含有此宏定义的文件，那么编译器在每次看到 `GREEN` 时都会抛出未知声明的错误。

## 定义函数形式的宏

`#define` 指令具有一个强大的特性：宏名可以带有参数。每当遇到宏名时，其定义中使用的参数就会被程序中找到的实际参数替换。这种形式的宏被称为函数形式（function-like）。

```
#include <stdio.h>

#define ABS(a) (a)<0 ? -(a) : (a)

int main(void) {
    printf("abs of -1 and 1: %d %d", -1, ABS(1));
    return 0;
}
```

当编译此程序时，宏定义中的 `a` 将被替换为值 -1 和 1。括号确保了在所有情况下都能正确替换。

强烈不建议使用函数宏，因为可能会产生奇怪的结果。

查看以下程序片段：

```
// 使用 a 和 b 的最大值调用 f
#define CALL_WITH_MAX(a, b) f((a) > (b) ? (a) : (b))

int a = 5, b = 0;
CALL_WITH_MAX(++a, b);      // a 被自增了两次
CALL_WITH_MAX(++a, b+10);   // a 被自增了一次
```

在调用 `f` 之前 `a` 自增的次数取决于它与什么进行比较。

在实际函数中使用函数形式的宏有一个主要优点：它增加了代码的执行速度，因为没有函数调用开销。然而，如果函数形式宏的大小非常大，那么由于代码重复，这种速度的提升可能以程序体积增大为代价。

## NULL 宏

在 C 语言中，`NULL` 定义如下：

```
#define NULL 0
```

## #error

`#error` 指令发出错误消息并强制编译器停止编译。它主要用于调试。`#error` 指令的一般形式为：

```
#error error-message
```

用法的示例为：

```
#if _STDC_ != 1
#error "Not a standard compliant compiler"
#endif
```

## #include 指令

`#include` 指令指示编译器读取另一个源文件，并将其放置在包含 `#include` 指令的源文件中。该文件将在 `#include` 指令出现的行处包含。附加源文件的名称必须封装在双引号或角括号之间。

```
#include "stdio.h"
```

或者

```
#include <stdio.h>
```

被包含的文件内部也可以有 `#include` 指令。这被称为嵌套包含（nested includes）。允许的嵌套层数在不同编译器之间有所不同。标准 C 规定必须至少支持 8 层嵌套包含。标准 C++ 建议至少支持 256 层嵌套。

文件名是封装在引号中还是角括号中决定了如何对指定的文件进行搜索。如果文件名封装在角括号中，则按照编译器创建者定义的方式搜索该文件。通常，这意味着搜索某些预留给包含文件的特殊目录。这是包含库文件的典型方式。

如果文件名封装在引号中，则按照实现者或程序创建者定义的方式搜索文件。这是包含用户文件的方式。对于许多编译器来说，这意味着搜索当前目录。

## 条件指令

有几种指令允许我们选择性地编译源代码的部分。最常用的条件指令是 `#if`、`#elif`、`#else` 和 `#endif`。这些条件指令允许我们根据常量表达式的值来选择性地编译。

`#if` 指令的形式为：

```
#if constant-expression
statements
#endif
```

如果 `#if` 的表达式为真，则 `#if` 和 `#endif` 之间的代码将被编译。否则，将跳过它。`#if` 后的表达式在编译时评估。因此它必须只包含已定义的标识符和常量。

```
/* Simple #if example */
#include <stdio.h>
#define MAX 10
int main(void) {
    #if MAX > 99
    printf("Compiled greater than 99");
    #endif
    return 0;
}
```

`#else` 指令在 `#if` 失败时建立一个替代方案。

```
/* Simple #if/#else example */
#include <stdio.h>
#define MAX 10
int main(void) {
    #if MAX > 99
    printf("Compiled greater than 99");
    #else
    printf("Compiled for a small array.");
    #endif
    return 0;
}
```

`#elif` 指令表示“else if”。它为多个编译选项建立 if-else 链。`#elif` 跟着一个常量表达式。如果表达式为真，则附加到 `#elif` 的块将被编译，且不再测试其他 `#elif`。否则，将测试 `#if` 链中的下一个块。

`#elif` 的一般形式为：

```
#if expression
statement sequence
#elif expression 1
statement sequence
#elif expression 2
.
#else
statement sequence
#endif
```



示例：

```
#define US 0
#define ENGLAND 1
#define FRANCE 2
```

```
#if ACTIVE_COUNTRY == US
char currency[] = "dollar";
#elif ACTIVE_COUNTRY == ENGLAND
char currency[] = "pound";
#else
char currency[] = "franc";
#endif
```

## #ifdef 和 #ifndef

另一种用于条件编译的预处理器使用了 `#ifdef` 和 `#ifndef` 指令。分别表示“如果定义”和“如果未定义”。

`#ifdef` 的一般形式为：

```
#ifdef macro-name
statement sequence
#endif
```

如果 `macro-name` 之前在 `#define` 语句中已定义，则代码块将被编译。

`#ifndef` 的一般形式为：

```
#ifndef macro-name
statement sequence
#endif
```

如果 `macro-name` 当前未被 `#define` 语句定义，则代码块将被编译。

`#ifdef` 和 `#ifndef` 指令都可以使用 `#elif` 或 `#else` 指令。例如：

```
#include <stdio.h>
#define __FREE 10
int main(void)
{
    #ifdef MONTHLY_SUBSCRIPTION
    printf("Monthly\n")
    #elif defined __YEARLY_SUBSCRIPTION
    printf("yearly\n")
    #elif defined __FREE
    printf("Free\n")
    #else
    printf("error\n")
    #endif

    #ifndef ALICE
    printf("ALICE not defined\n")
    #endif

    return 0;
}
```

### 使用 defined

除了 `#ifdef` 之外，还有另一种方法判断宏名是否被定义。我们可以使用 `#if` 指令配合 `defined` 编译时运算符。`defined` 运算符的格式如下：

```
defined 宏名
```

如果宏名已定义，则该表达式为真，否则为假。因此，我们也可以这样做：

```cpp
#if defined SUM
...
#endif
```

我们还可以在 `defined` 之前加上 `!` 运算符来反转条件：

```cpp
#if !defined SUM
...
#endif
```

## #undef

`#undef` 指令用于移除跟随其后的、之前定义的宏名定义。也就是说，它“取消定义”了一个宏名。`#undef` 的通用形式为：

```
#undef 宏名
```

`#undef` 主要用于允许宏名仅局部于需要它的那些代码部分。

## #line

`__LINE__` 标识符包含当前编译代码行的行号。

`__FILE__` 标识符是一个字符串，包含正在编译的源文件的名称。`#line` 可以更改行号并可选地更改文件名。`#line` 的通用形式为：

```cpp
#line 数字 "文件名"
```

其中数字可以是任意正整数。它将成为 `__LINE__` 的新值，可选的文件名可以是任何有效的文件标识符，它将成为 `__FILE__` 的新值。

`#line` 主要用于调试和特殊应用。

## #pragma

`#pragma` 是编译器定义的指令，允许向编译器提供各种指令。我们必须检查编译器文档以获取其 pragma 细节和选项。

## C 语言：assert

`assert` 宏在运行时测试表达式为真还是为假。如果表达式为假，程序将终止。其语法为：

```cpp
#include <assert.h>
assert(expression);
```

在 C 语言中，包含 `assert.h` 的惯用方法是：`#include <cassert>`

在 C 中，表达式的零值被解释为假。非零表达式被解释为真。

这里有一个 C++ 示例：

```cpp
#include <iostream>
#include <cassert>

int main() {
    std::cout << "Hello, World!" << std::endl;
    assert(1 == 0);
}

// 输出
Hello, World!

prog.exe: prog.cc:9: int main(): Assertion `1 == 0` failed.
aborted
Finish
```

可以通过在 `assert` 宏之前包含该宏来禁用它：

```cpp
#define NDEBUG
```

## C 语言：在 C++ 中调用 C 函数

### 简介

C++ 起初是 C 语言的扩展版本。C++ 扩展最早是由 Bjarne Stroustrup 于 1979 年在贝尔实验室发明的。

C++ 的发明是由于一个主要的编程因素而变得迫在需要的：复杂性的增加。计算机程序变得越来越大、越来越复杂。一旦程序变得非常大，C 语言就有其局限性。在 C 中，一旦程序超过了 25,000 到 100,000 行代码，它就会变得极其复杂，难以从整体上把握。

## 头文件

当我们在程序中使用库函数时，必须包含其头文件。这是通过使用 `#include` 语句实现的。例如，在 C 语言中，我们这样包含 I/O 函数的头文件：

```cpp
#include <stdio.h>
```

在 C++ 中，我们可以这样做：

```cpp
#include <cstdio>
或
#include <stdio.h>
```

在惯用的 C++ 中，通过在库名上添加 `c` 前缀并去掉 `h` 后缀来包含标准 C 库文件。

文件名可以用双引号或尖括号括起来。这决定了如何进行对指定文件的搜索。如果文件名包含在尖括号中，则将按照编译器创建者定义方式搜索文件。通常，这意味着在某些为包含文件留的特殊目录中搜索。如果文件名包含在引号中，则以某种实现定义的方式查找文件。对于许多编译器来说，这意味着搜索当前工作目录。

## 在 C++ 代码中包含非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## 在 C++ 代码中调用非系统 C 头文件

如果我们要包含的是一个不在 C 标准库中的 C 头文件，则需要 `extern` 限定符，因为 C 和 C++ 在在栈上放置函数参数和返回值方面有不同的约定。

```cpp
// 在 C++ 文件中
extern "C" {
#include "my_c_header_file.h"
}
```

如果我们要包含的是一个不是系统提供的 C 头文件，并且如果我们能够更改该 C 头文件，我们应该考虑在 C 头文件内部添加 `extern "{...}"` 逻辑，以便 C++ 用户更容易将其 `#include` 到他们的 C++ 代码中。由于 C 编译器不会理解 `extern "C"` 结构，你必须将 "C" 头文件的代码封装在一个 `#ifdef` 块中，使 C 编译器无法看到它。以下步骤解释了如何这样做：

**步骤 1：** 在 C 头文件的顶部放置以下行：

```cpp
#ifdef cplusplus
extern "C" {
#endif
#include 语句
```

**步骤 2：** 在 C 头文件的最底部放置以下行：

```cpp
#ifdef __cplusplus
}
#endif
```

现在我们可以在 C++ 代码中无需任何 `extern "C"` 包装的情况下包含该头文件。

注意：当且仅当编译器是 C++ 编译器时，符号 `__cplusplus` 才会被 `#define`。

## C++ 类

封装将数据绑定到操作它的代码上。封装控制对数据的访问。在面向对象的语言如 C++ 中，代码和数据结合以创建一个自包含的“黑盒”。这个黑盒就是 C++ 类。

在 C++ 中，封装通过类来实现。

在 C++ 中，类的行为类似于类型，实际上是用户定义的类型。就像 `int` 和 `float` 等内置 C++ 类型一样，可以从抽象类型创建对象。

类使用 `class` 关键字创建。类声明了一个封装代码和数据的逻辑类型。类的物理表示称为对象或实例。从类创建对象的行为称为实例化。

类具有以下语法：

```cpp
class 类
{
// 私有数据函数
private:
...
// 公有数据函数
public:
...
// 保护数据函数
protected:
...
} 对象列表;
```

对象列表是可选的。如果没有这个列表，我们只有类声明。

对类成员的访问由这三个 C++ 关键字控制：

```cpp
public
private
protected
```

默认情况下，类内部的函数和数据是私有的。这意味着它们只能由类的其他成员访问。公有访问限定符允许函数和数据从程序的其他部分访问；即类外部。一旦使用了访问限定符，它将一直有效，直到遇到另一个访问限定符或类声明结束。

我们可以在类声明中频繁更改访问规范。

这里有一个类的示例：

```cpp
class Employee
{
    char name[80];
    double wage;

public:
    void putname(char *n);
    void getname();
    void putwage(double w);
    double getwage();
};
```



注意，这个类只包含函数原型（或函数声明）。成员函数的实际实现将在类声明之外。尽管如此，类声明也可以包含函数实现。

在类内部声明的函数被称为成员函数或方法。成员函数可以访问其所属类的任何其他成员。

这包含了所有私有元素。

类声明中的成员数据变量具有一些局限性：

- 成员变量不能被声明为 `extern` 或 `register` 变量。
- 非静态成员变量不能通过赋值进行初始化（在类中声明它的点）。

作为一个一般规则，我们应该强制执行数据的封装。也就是说，类中的所有数据成员都应该声明为 `private`。

## 访问公共成员

访问公共成员的语法如下：指定对象的名称，然后是点运算符 `.`，最后是成员变量或成员函数。

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    // 这些数据变量整个程序都可以访问
    int i, j, k;
};

int main() {
    Foo a, b;
    // 访问 i, j 和 k 是允许的
    a.i = 100;
    a.j = 4;
    a.k = a.i * a.j;

    b.k = 12; // 不同的类实例

    cout << a.k << " " << b.k;
    return 0;
}

// 输出
400 12
```

## 作用域解析运算符

`::` 作用域运算符将成员与类名关联。它告诉编译器该成员属于哪个类。作用域解析运算符还有另一个用途：它可以允许访问某些作用域内的名称。这允许访问某些作用域内与本地声明同名的名称。

下面的示例展示了它是如何工作的：

```cpp
int i;      // 全局变量 i
void f() {
    int i;      // 局部变量 i
    i = 10;     // 使用局部 i
}

void g() {
    int i;      // 局部变量 i
    ::i = 10;    // 指向全局变量 i
}
```

## 类函数实现

考虑以下类规范：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

class Foo {
public:
    void buildstr(char *s);
    void showstr();

private:
```

```cpp
char str[255];

void Foo::buildstr(char *s) {
  // 初始化成员字符串变量
  strcpy(str, s);
}

void Foo::showstr() {
  cout << str << "\n";
}
```

此示例中的类仅包含类成员函数的原型。类类函数的实现位于类之后，并使用作用域解析运算符来识别每个函数所属的类。这是类的声明方式。然而，我们可以在类内部提供函数实现。

## 静态类成员

类的成员函数和成员变量可以声明为 `static`。静态成员由该类的所有实例共享。适用以下限制：

- 静态成员函数只能引用该类的其他静态成员函数和静态数据成员。
- 静态成员函数没有 `this` 指针。
- 我们不能让同一个成员函数拥有静态和非静态的版本。
- 静态函数不能声明为具有 `const` 或 `volatile` 属性。

以下是一个示例：

```cpp
#include <iostream>
using namespace std;

class Foo
```

```cpp
static int resource;
public:
    static int get_resource();
    void free_resource() { resource = 0; }
};
```

```cpp
int Foo::resource = 0; // 初始化 resource

int Foo::get_resource() {
    if(resource)
        return 0;
    else
        {
            resource = 1;
            return 1;
        }
}
```

```cpp
int main() {
    int ret = Foo::get_resource();
    cout << "resource = " << ret << endl;
    return 0;
}
```

```cpp
// 输出
resource = 1
```

注意此示例中 `Foo` 没有被实例化。

## 对象赋值

假设两个对象是相同类型，我们可以使用常用的赋值运算符 `=` 将一个对象赋值给另一个对象。这会导致右侧的数据按位拷贝到左侧的对象中。

## 局部类

局部类是在函数内部定义的类。下面的示例在函数内部内部定义了一个类：

```cpp
#include <iostream>
using namespace std;

// 函数 f 的前声明
void f();

int main()
{
    f();
    return 0;
}
```

```cpp
void f()
{
    // 在 f 内部定义一个局部类
class Foo {
    int i;
    public:
    void put_i(int n) { i=n; }
    int get_i() { return i; }
}

Foo foo;

```

```cpp
foo.put_i(10);
cout << "foo i data member = " << foo.get_i() << endl;
```

```cpp
// 输出
foo i data member = 10
```

对局部类的使用有严格的限制：

- 所有成员函数必须在类声明内部定义。
- 局部类可能访问其定义处函数中的任何局部变量；在函数内部声明的静态变量除外。
- 局部类内部不能声明静态变量。

局部类可以访问 `typedef` 和。

## C++ 命名空间

命名空间的目的是将名称局部化以避免冲突。在命名空间发明之前，如果我们的程序定义了一个函数，可能会发生冲突。命名空间通过将名称局部化到它们声明的作用域来解决这个问题。这允许在不同的上下文中中使用相同的名称。命名空间通过创建区域来允许我们划分全局命名空间。

如果我们的程序定义了一个名为 `abs()` 的函数，可能会覆盖标准库函数，因为它们都在全局命名空间中。命名空间的创建解决了这个问题。命名空间允许在不同的上下文中使用相同的名称。

命名namespace的语法如下：

```cpp
namespace name {
// 声明
}
```

命名空间内任何名称的可见性限于其定义的作用域。

```cpp
namespace counter_namespace {
int upperbound;
int lowerbound;
class Counter {
int count;
public:
counter(int n) {
    if(n <= upperbound)
        count = n;
    }
}
```

```cpp
else
    count = upperbound;
}
void reset(int n)
{
    if(count > lowerbound)
        return count--;
    else
        return lowerbound;
}
```

这里 `upperbound`、`lowerbound` 和 `Counter` 类的可见性限于 `counter_namespace`。

命名空间块内部定义的标识符可以在没有任何命名限定的情况下引用。例如，在 `counter_namespace` 内部，`run()` 函数可以直接引用 `lowerbound`。然而，由于命名空间定义了作用域，我们需要使用作用域运算符来从外部引用命名空间内声明的对象。

例如，从 `counter_namespace` 外部为 `upperbound` 赋值 10，我们必须使用作用域运算符：

```cpp
counter_namespace::upperbound = 10;
```

并且从 `counter_namespace` 外部声明 `Counter` 类型的对象，我们使用：

```cpp
counter_namespace::Counter foo;
```

## 全局命名空间

如果标识符没有在任何命名空间定义，它是全局命名空间的一部分。通常，我们应该避免在全局命名空间中进行声明，入口函数 `main` 必须在全局命名空间中。

要使用全局命名空间中的标识符如 `someFunction()`，我们使用没有任何前缀的作用域运算符，例如：

```cpp
::someFunction(x);
```

## 最佳实践

当你想引用全局变量（它在全局命名空间中）时，在变量前加上作用域运算符。这将让我们知道变量定义在全局命名空间中。示例：

```cpp
foo(int x) {
  return x + ::y;
}
```

## 将标识符引入作用域

我们可以通过使用作用域运算符限定标识符将其引入另一个命名空间的作用域中。语法如下：

```cpp
void foo() {
  std::cout << std::string("Hello World");
}
```

这会将 `std` 命名空间中的 `cout` 和 `string` 引入作用域。

### 命名空间：using 指令

如果我们的程序频繁引用命名空间中的标识符，那么每次引用这些标识符时都要指定命名空间和作用域解析运算符，很快就会变得繁琐。`using` 语句缓解了这个问题。`using` 语句有两种通用的形式：

```
using namespace foo;
using foo::bar;
```

在第一种形式中，`foo` 指定我们想要访问的命名空间名称。`foo` 命名空间内定义的所有成员都被引入作用域（它们成为当前命名空间的一部分），并且可以使用而不带作用域解析运算符（例如使用 `vector` 而不是 `std::vector`）。在第二种形式中，只有 `foo` 命名空间中的特定成员 `bar` 被引入作用域。

假设如所示 `counter_namespace`，以下 `using` 语句和赋值是有效的：

```
// 只有 lowerbound 可见
using counter_namespace::lowerbound;

// OK，因为 lowerbound 在当前作用域内是的
lowerbound = 10;
```

### using namespace 的危险

在头文件中声明 `using namespace <some identifier>` 被认为是一种不良实践，因为会将该命名空间引入整个程序中。

在实现文件中声明 `using namespace` 也不被推荐，因为可能会导致非常难以调试的歧义（ambiguity）。考虑这个示例：

```
#include <iostream>

namespace my_library {
    double calculate(double x) { return x + x; }
}

namespace foreign_lib {
    int calculate(int x) { return x + x; }
}

using namespace my_library;
using namespace foreign_lib;

int main() {
    calculate(2);
    calculate(2.3);
}
```

这段代码的问题在于，调用的 `calculate` 版本取决于 `calculate` 参数的类型。这可能会在程序中引入非常难以追踪的错误。

最佳实践是始终为标识符加上命名空间前缀。

## 匿名命名空间

有一种特殊的命名空间类型称为匿名命名空间（unnamed namespace），它允许我们创建在命名空间内唯一且在命名空间外不可见的标识符。

匿名命名空间也称为匿名命名空间（anonymous namespaces）。它们具有以下语法：

```
namespace {
    // declarations
}
```

匿名命名空间允许我们建立仅在命名空间作用域内已唯一标识符。考虑一个内容被匿名命名空间封装的文件。在包含该匿名命名空间的文件内部，命名空间的成员可以直接使用而无需限定。但在文件外部，这些标识符是未知的且无法被访问的。

## 合并命名空间

可以有多个相同（命名空间）名称的命名空间声明。这允许将命名空间拆分到多个文件中，甚至在文件中拆分开。

```
#include <iostream>
using namespace std;

namespace NS {
int i;
}

// 间隙代码
namespace NS {
int j;
}
int main() {
NS::i = NS::j = 10;

// 特别地引用 NS
cout << NS::i * NS::j << endl;

// 使用 NS 命名空间
using namespace NS;
cout << i * j << endl;
}

// 输出
100
```

在这个示例中，命名空间 `NS` 被分成了两个部分。然而，每个部分的内容仍然同一个命名空间 `NS` 中。

命名空间可以嵌套在另一个命名空间内部。但是，命名空间不能声明在函数体内部。不过我们可以在函数内部使用 `using namespace name`。

```
#include <iostream>
using namespace std;

namespace NS {
    int i;
    namespace NS2 { // 一个嵌套的命名空间
    int j;
} // NS2 结束
} // NS1 结束

int main() {
    NS1::i = 19;
    // NS2::j = 10; // 错误，NS2 嵌套在 NS1 内部
    NS1::NS2::j = 10; // 这是正确的

    cout << NS1::i << endl;

    // 使用 NS1
    using namespace NS1;

    // 现在 NS1 可见，NS2 可以
    // 独立使用来引用 j
    cout << i * NS2::j;

    return 0;
}

// 输出
19
190
```

## std 命名空间

标准 C++ 库将其整个库定义在自己的名为 `std` 的命名空间中。

`using namespace std;`

这条 `using` 语句将 `std` 命名空间中的标识符引入当前命名空间，使我们直接访问库中定义的函数和类的名称，而无需为每个名称加上 `std` 限定。

## 命名空间别名

命名空间标识符可以被别名替换。例如：

```
namespace newfarm = farm;
```

现在可以使用 `newfarm` 别名来代替 `farm` 命名空间：

```
newfarm::pets = 5; // 等同于 farm::pets;
```

```
#include <iostream>
namespace T {
    int ctr = 0;
}
int main() {
    namespace Z = T;
    std::cout << Z::ctr << std::endl;
}
// 输出
0
```

## C++ 结构体与联合体

在 C++ 中，`struct` 仅仅是所有数据成员和成员函数默认都是公开的类。与 C 不同，C++ `struct` 可以包含成员函数。

这里是一个 C++ `struct` 声明的示例：

```cpp
// 一个 C++ struct
#include <iostream>
#include <cstring>

using namespace std;

struct Foo {
    // public
    void buildString(const char *s);
    void showWord();

private:
    unsigned short u;
    unsigned char c[2];
};

void Foo::buildString(const char *s) {
    // 初始化
    strcpy(c[0], s);
}

void Foo::showWord() {
    cout << u;
}

void Foo::setColor(unsigned short i) {
    u = i;
}

int main() {
    // 使用 struct
    Foo foo;
    foo.buildString("hello world");
    foo.showWord();
}

// 输出
hello world
```

## 联合体与类

在 C++ 中，`union`（联合体）可以同时包含成员函数和数据成员。它们还可以包含构造函数和析构函数。对于联合体，所有元素共享相同的内存位置。联合体成员默认是公开的。像 `struct` 一样，联合体成员默认是公开的。

这是一个示例：



```cpp
#include <iostream>
using namespace std;

union swapByte
{
    void swap();
    void setColor(unsigned short i);
    void showWord();

private:
    unsigned short u;
    unsigned char c[2];
};

void swapByte::swap() {
    unsigned char t;
    t = c[0];
    c[1] = t;
}

void swapByte::setColor(unsigned short i) {
    u = i;
}

void swapByte::showWord() {
    cout << u;
}

int main() {
    swapByte foo;
    foo.setColor(49034);
    foo.swap();
    foo.showWord();
}

// 输出
35519
```

# C++ 中的联合体限制

C++ 中的联合体有很多限制：

- 联合体不能继承任何类
- 联合体不能作为其他类的基类
- 联合体不能包含虚函数
- 联合体不能包含静态成员
- 联合体不能重载赋值运算符
- 如果对象有显式构造函数或析构函数，则对象不能作为联合体的成员

## 匿名联合体

C++ 中有一种特殊的联合体类型称为匿名联合体 `anonymous union`。匿名联合体没有名称，无法创建匿名联合体的对象。

相反，匿名联合体告诉编译器其数据成员共享内存位置。匿名联合体必须只包含公开成员。

匿名联合体中的数据成员直接引用，而不使用通常的点运算符语法。例如，考虑这段程序：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

int main()
{
    // 定义一个匿名联合体
    union {
        long l;
        double d;
        char s[4];
    }

    // 现在直接引用联合体元素
    l = 100000;
    cout << l << " ";

    d = 123.2342;
    cout << d << " ";

    strcpy(s, "hi");
    cout << s;
}

    // 输出
    100000 123.2342 hi
```

联合体元素的引用方式就像声明普通局部变量一样。

所有涉及联合体的限制都适用于匿名联合体。全局匿名联合体必须指定为 `static`。

# C++ 友元函数与友类

通过使用 `friend` 关键字，我们可以允许非成员函数访问类的私有成员。友元函数可以访问其所属类的所有私有成员和受保护成员。要声明一个友元函数，将其声明包含在类内部，并在该声明前加上 `friend` 关键字。

```cpp
#include <iostream>
using namespace std;

class Foo {
    int a, b;
public:
    friend int sum(Foo);
    void setAb(int i, int j);
};

void Foo::setAb(int i, int j) {
    a = i;
    b = j;
}

// 注意：sum() 并不是任何类的成员函数。
int sum(Foo f) {
    /* 因为 sum() 是 Foo 的友元，它可以
       直接访问私有成员 a 和 b。 */
    return f.a + f.b;
}

int main() {
    Foo klass;
    klass.setAb(3, 4);
    cout << sum(klass) << endl;
}

// output
7
```

在这个示例中，`sum()` 函数不是 `Foo` 的成员。然而，由于它是 `Foo` 的友元，它仍然具有访问 `Foo` 私有成员的权限。

## 前置声明或前向引用

当对象在声明之前被使用时，需要进行前置声明。以下示例了如何对类进行前置声明：

```cpp
// 类 C2的前置声明
class C2
{
  int status;
public:
  void setStatus(int);
  int getStatus(C2);
}
```

## 友类

也可以使一个类成为另一个类的友类。在这种情况下，友类的所有成员函数都可以访问宿主类的私有和受保护成员。例如：

```cpp
#include <iostream>
using namespace std;

// 类 Min的前置声明
class Min;

class TwoValues
{
  int a;
  int b;
public:
  TwoValues(int i, int j) { a = i; b = j; }
  friend class Min;
};

class Min
{
public:
  int minimum(TwoValues x);
};

int Min::minimum(TwoValues x)
{
    return x.a < x.b ? x.a : x.b;
}

int main()
{
    TwoValues obj(10, 20);
    Min m;
    cout << m.minimum(obj);
    return 0;
}
// output
10
```

# C++ 内联函数

在 C++ 中，我们可以创建实际上并没有被调用的短函数；相反，它们的代码会在声明处进行内联展开。这会导致代码运行更快，因为不需要使用栈来加载参数。我们可以通过在函数声明前加上 `inline` 关键字，使函数被内联展开而不是调用。

```cpp
#include <iostream>
inline int max(int a, int b)
{
    return a > b ? a : b;
}
int main()
{
    std::cout << max(10, 20) << std::endl;
    std::cout << max(99, 88) << std::endl;
    return 0;
}
```

内联函数之所以是 C++ 的重要补充，是因为它们允许我们创建非常高效的代码。由于类通常需要几个频繁执行的接口函数，这些函数的效率是至关重要的。每当调用函数时，调用和返回机制都会产生大量的开销。通常情况下，在调用函数时会将参数推入栈中并保存各种寄存器，然后在函数返回时恢复这些寄存器。问题在于这些指令是非常耗时的。然而，如果函数是内联的，这些操作就不会发生。

虽然内联函数可以提高运行速度，但由于代码重复，它会导致代码体积增大。因此，最好的做法仅对那些对程序性能有显著影响的小函数使用 `inline`。`inline` 实际上只是一个请求，而不是命令，编译器可以选择忽略它。

## 在类内定义内联函数

类成员函数可以在类内隐式声明，也可以显式声明，如下：

```cpp
#include <iostream>
class Foo
{
    int a, b;
public:
    void init(int i, int j);
    // 隐式内联
    void show() { std::cout << a << " " << b << "\n"; };
}

// 显式创建内联成员函数
inline void Foo::init(int i, int j)
{
    a = i;
    b = j;
}

int main()
{
    Foo foo;
    foo.init(1, 3);
    foo.show();
}

// output
1 3
```

如示例所示，我们可以在类内部完全定义内联函数，也可以在类外部显式定义。当函数定义在类内部时，它会自动变成内联函数。在这种情况下不需要在函数声明前加上 `inline` 关键字。

# 构造函数与析构函数

析构函数的名称与类名相同，但带有 `~` 前缀。

当对象产生时会调用对象的构造函数，当对象被销毁时会自动调用对象的析构函数。

全局对象的构造函数在 `main` 开始执行之前执行。在同一个文件中，全局构造函数按照声明顺序执行。当全局构造函数分布在多个文件中时，它们的执行顺序是未知的。全局析构函数在 `main` 结束后按反顺序执行。

局部对象的构造函数在遇到对象定义时执行。局部对象的析构函数按照构造函数的相反顺序执行。

## 私有析构函数

```cpp
#include <iostream>
class Foo {
private:
    ~Foo();
};
int main() {
    Foo foo;
}

// output
error: 'Foo::~Foo()' 在此上下文中是私有的
```

此程序无法编译。原因是 `foo` 在栈上创建的，一旦 `foo` 离开作用域，由于析构函数是私有的，将无法调用。将类的析构函数设为私有可以确保只有类对象自己可以销毁。例如，引用对象可以在计数变为零时销毁自己。

规则：如果一个类具有私有析构函数，则它应该在堆上创建，而不是在栈上。

# 将对象传递给函数

可以使用默认的按值传递机制将对象传递给函数。这意味着当对象传递给函数时，会创建该对象的拷贝。函数接收的是该对象的位拷贝。

然而，创建拷贝这一事实本质上意味着了另一个对象。这引发了一个问题：在创建拷贝时，对象的构造函数是否会被执行？当拷贝被销毁时，析构函数是否会被执行？

```cpp
// 将对象传递给函数
#include <iostream>
class Foo {
    int i;
  public:
    Foo(int n);
    ~Foo();

    void set(int n) { i=n; }
    int get() { return i; }
};

// Foo 的构造函数
Foo::Foo(int n) {
    i = n;
    std::cout << "Foo Constructor: " << i << "\n";
}

// Foo 的析构函数
Foo::~Foo() {
    std::cout << "Destroying foo " << "\n";
}

// 函数 func 的前置声明
void func(Foo obj);

int main()
{
  Foo foo(1);
  func(foo);      // 按值传递 foo 对象

  std::cout << "This is i in foo = ";
  std::cout << foo.get() << "\n";
}

void func(Foo obj)
{
  obj.set(2);
  std::cout << "This is i in func: " << obj.get() << "\n";
}
```

// // 输出

Foo Constructor: 1

This is i in func: 2

Destroying foo

This is i in foo = 1

Destroying foo

注意，析构函数被执行了两次，但构造函数只被调用了一次。如输出所示，当将 `obj` 的拷贝传递给 `func` 时，构造函数并没有被调用。创建拷贝时没有调用构造函数的原因很容易理解。当我们把对象传递给函数时，我们想要传递对象的当前状态。如果在创建拷贝时调用构造函数，将会发生初始化，并可能会改变对象。因此，当为函数调用生成对象的拷贝时，构造函数不会执行。

尽管在将对象传递给函数时不会调用构造函数，但在拷贝被销毁时，必须调用析构函数。`obj` 拷贝可能执行诸如内存分配等操作，这些操作在拷贝销毁时需要调用析构函数。

默认情况下，会创建对象的拷贝，即进行位拷贝。这意味着新对象是原始对象的完全复制。创建完全副本这一事实可能是问题的根源。例如，假设一个对象分配了内存，然后该对象被按值传递给一个函数。当函数退出时，拷贝的析构函数会被自动调用，原始对象分配的内存将被释放。这将导致原始对象处于受损状态。

# 返回对象

函数可以向调用者返回一个对象：

```cpp
// 从函数返回对象。
#include <iostream>
class Foo
{
    int i;
    public:
    void set(int n) { i=n; }
    int get() { return i; }
};

// 前置声明；func 返回类型为 Foo 的对象
Foo func();
int main()
{
    Foo obj = func();
    std::cout << obj.get() << "\n";
}

// 定义 func()
Foo func()
{
    Foo foo;
    foo.set(99);
    return foo;
}

// // 输出
99
```

当函数返回一个对象时，栈上会自动创建一个临时对象。函数实际上实际上返回的正是这个对象。在我们的示例中，返回的对象被赋值给局部对象 `obj`，然后栈上的返回对象 `foo` 就会被销毁。

栈上这个临时对象的销毁在某些情况下可能会导致意外的副作用。例如，如果函数返回的对象具有一个释放动态分配内存的析构函数，那么即使接收返回值的对象将使用该内存，该内存也会被释放。

# C++ 内存分配

C++ 支持 C 语言的内存分配函数 `malloc`、`calloc`、`alloc` 和 `free`。此外，C++ 还提供了两个内存运算符：`new` 和 `delete`。这些运算符用于在运行时分配和释放内存。

`new` 运算符在堆上分配内存并返回指向该内存起始位置的指针。`delete` 运算符释放之前由 `new` 分配的内存。`new` 和 `delete` 的通用形式为：

```cpp
#include <new>
type_t* ptrMem = new type_t;
delete ptrMem;
```

在这里，`ptrMem` 是一个指针变量，接收一个指向足够容纳 `type_t` 类型内存的指针。

由于堆是有限的，它可能会被耗尽。如果没有足够的内存来满足分配请求，`new` 将因 `bad_alloc` 错误而失败。此错误实际上是一个异常，我们将在后面的章节中讨论。`bad_alloc` 定义在头文件 `<new>` 中。程序应该处理此错误并在发生失败时采取适当的措施。如果我们的程序没有处理此错误，程序将终止。

```cpp
#include <iostream>
#include <new>

using namespace std;

int main() {
    int *p;
    try {
        // 分配内存
        p = new int;
    }
    catch (bad_alloc& xa) {
        cout << "Allocation Failure\n";
        return 1;
    }
    delete p;
    return 0;
}
```

## 初始化分配的内存

我们可以通过在 `new` 语句的类型名后面加上初始化器来初始化分配的标量类型：

```cpp
scalarType* p = new scalarType(45);
```

括号不能为空。

## 为数组分配内存

我们可以使用 `new` 为数组分配内存：

```cpp
array_type* ptrMem = new array_type[size];
```

`size` 指定数组中的元素数量。

要释放数组，使用这种形式的 `delete`：

```cpp
delete [] ptrMem; // 或 delete []p
```

`[]` 通知 `delete` 正在释放数组。

这是一个示例：

```cpp
#include <iostream>
#include <new>

using namespace std;

int main() {
    int *p, i;
    try {
        // 分配10个元素的整数数组
        p = new int[10];
    }
    catch (bad_alloc& xa) {
        cout << "Allocation Failure\n";
        return 1;
    }

    // 初始化数组
    for(i=0; i < 10; i++)
        p[i] = i;

    for (i = 0; i < 10; i++)
        cout << p[i] << " ";

    delete [] p; // 释放数组

    return 0;
}

// // 输出
0 1 2 3 4 5 6 7 8 9 
```

## 为对象分配内存

我们可以使用 `new` 为对象分配内存。当我们这样做时，会创建一个对象并返回指向对象的指针。这个动态创建的对象的行为与任何其他对象一样。当它被创建时，它的构造函数会被调用。当对象被释放时，它的析构函数会被执行。

```cpp
#include <iostream>
#include <new>
#include <cstring>

using namespace std;

class Balance {
    double cur_bal;
    char name[80];
public:
    void set(double bal, const char *s)
    {
        cur_bal = bal;
        strcpy(name, s);
    }

    double get_bal() {
        return cur_bal;
    }
};

int main()
{

    Balance *p;

    double bal;

    try {

        p = new Balance;

    } catch (bad_alloc& xa) {
```



`cout` << "Allocation Failure\n";

return 1;

}

p->set(12387.87, "alice");

bal = p->get_bal();

`cout` << "balance is: " << bal << endl;

delete p;

}

//output

balance is: 12388

使用以下语法分配 `Balance` 对象：

p = new Balance;

删除该对象的语法为：

delete p;

## C++ 数组

在 C++ 中，可以拥有对象数组。声明和使用对象数组的语法与任何其他类型的数组相同。在接下来的示例中，我们创建了一个包含三个 *Foo* 类型类型对象的数组：

```cpp
#include <iostream>
using namespace std;

class Foo
{
    int i;
public:
    void set(int j) { i=j; }
    int get() { return i; }
};

int main() {
    Foo foo[3];
    int i;

    for (i = 0; i < 3; i++) foo[i].set(i+1);
    for (i = 0; i < 3; i++)
        cout << foo[i].get() << " ";
}

// output
1 2 3
```

### 使用单参数构造函数初始化数组

如果类 *Foo* 包含一个单参数构造函数，那么 *Foo* 对象数组可以按如下方式初始化：

```cpp
#include <iostream>
using namespace std;

class Foo
{
    int i;
public:
    Foo(int j) { i=j; } // 单参数构造函数
    int get() { return i; }
};

int main() {
  Foo obj[3] = {1, 2, 3}; // 初始化列表
  int i;

  for(i = 0; i < 3; i++)
    cout << obj[i].get() << " ";

  return 0;
}
```

如果类构造函数有两个或更多参数，我们必须使用以下初始化语法：

```cpp
#include <iostream>
using namespace std;

class Foo {
  int h;
  int i;
public:
  // 带有2个参数的构造函数
  Foo(int j, int k) { h=j; i=k; }
  int get_i() { return i; }
  int get_h() { return h; }
};

int main() {
  Foo obj[3] = {
    Foo(1, 2), // 构造函数的初始化列表
    Foo(3, 4),
    Foo(5, 6)
  };

  int i;
  for (i = 0; i < 3; i++) {
    cout << obj[i].get_h();
    cout << ", ";
    cout << obj[i].get_i() << "\n";
  }
}

// output
1, 2
3, 4
5, 6
```

### 创建初始化和未初始数组

当我们想要同时创建初始化和未初始对象数组时，就会出现特殊情况。考虑以下类：

```cpp
class Foo
{
    int i;
public:
    Foo(int j) { i=j }
    int get() { return i; }
};
```

`Foo` 的数组声明：`Foo ar[9];` 将失败，因为数组中的每个对象都必须通过调用构造函数来实例化，而 `Foo` 没有适当的构造函数。只有当 `Foo` 也有一个无参数的构造函数时，编译才能成功。

我们可以通过重载 `Foo` 构造函数来指定任何处理初始化和未初始化对象的数组：

```cpp
class Foo
{
    int i;
public:
    // 用于未初始化数组的构造函数
    Foo() { i = 0; }

    // 用于初始化数组的构造函数
    Foo(int j) { i = j; }
    int get_i() { return i; }
};
```

给定该类声明，以下是有效的对象实例化：

```cpp
Foo a[3] = {3, 5, 6};      // 初始化数组
Foo b[34];                   // 未初始化数组
```

### 动态构建数组

假设我们动态创建一个包含五十个 `double` 值的数组。以下是在堆上分配此数组的语法：

```cpp
double* ptrMem = new double[50];
```

我们使用以下代码释放此内存分配：

```cpp
delete []ptrMem;
```

## C++ 指针

与变量指针一样，我们可以拥有指向对象的指针。给定一个对象的指针，我们使用箭头 (`->`) 运算符而不是点运算符 (`.`) 来访问对象的成员。以下程序说明了如何通过指针访问对象：

```cpp
#include <iostream>
class Foo {
    int i;
public:
    Foo(int j) { i=j; }
    int get() { return i; }
};

int main() {
    // p 是指向 Foo 对象的指针
    Foo* p;
    Foo obj(77);

    // 获取 obj 的地址
    p = &obj;

    // 使用 -> 调用 get()
    std::cout << p->get() << std::endl;
    return 0;
}

// output
```

### 指针的递增

当指针递增时，它指向其所指类型的下一个元素。例如，整数指针将指向下一个整数。

通常，所有的指针运算都是相对于所指向对象的类型或原生类型的。

由于类型或类具有以字节为单位的大小，增加指针会将指针地址增加等于所指向类型或对象大小的字节数。

### 成员函数指针

假设我们有一个类 `Foo`，它包含一个公共成员函数 `add`，声明如下：`int add(int, int);`

那么，指向成员函数（如 `add`）的声明如下：

```cpp
return_type (Class_Name::* pointer_name)(Argument_List);
```

这表示 *pointer_name* 是指向指定类中某个成员函数的指针。

### this 指针

每个 C++ 对象都有一个 `this` 指针，它是指向对象本身的指针。该指针的值是对象的地址。

当调用非静态成员函数时，`this` 指针会自动作为隐式参数传递进去。

考虑以下程序：

```cpp
#include <iostream>

class Foo {
    int i;
public:
    Foo(int x) { i = x; } // 隐式传递 this 指针
    int square() {
        return this->i*this->i;
    }
};

int main() {
    Foo foo(5);
    std::cout << foo.square() << std::endl;
}

// output
25
```

```cpp
return i*i;
```

注意，友元函数不是类的成员，因此它们不会被传递 *this* 指针。其次，静态成员函数没有 *this* 指针，因为它与任何实例化的对象没有唯一的关联。

# C++ 引用

C++ 包含一个与指针相关的重要特性，称为引用（references）。引用是一个隐式的指针变量，可以像操作它所指向的实际对象或变量一样对其操作。

创建引用变量的语法如下：

```cpp
#include <iostream>

int main() {
    int z = 5;
    int& x = z; // 或 int &x = z;
    std::cout << x << std::endl;
}
// 输出
5
```

在这里，`x` 是一个 `int` 类型变量的引用。引用变量在创建时必须初始化。引用变量在声明时，必须指向某个已初始化的变量。

像 `int& x = 5;` 这样的声明将无法编译，因为 5 是一个瞬时值，没有地址，因此无法被指向（这一点稍后将在右值相关的章节中详细讨论）。此外，字面量 5 一旦语句执行完毕就会消失。

使用引用变量有三种方式：作为函数参数、作为函数返回值以及作为独立变量。在之前的示例中，`x` 是一个独立的引用变量。

## 函数引用参数

引用变量最重要的用途是创建使用“引用传递”参数传递的函数。参数可以通过两种方式传递给函数：使用**值传递**（call by value）或使用**引用传递**（call by reference）。当使用值传递时，参数的拷贝会被传递给函数。而引用传递则将参数的地址传递给函数。

默认情况下，C++ 使用值传递来将参数传递给函数，但它也提供了两种通过引用传递参数的方法。首先，我们可以显式地将指针变量传递给函数。其次，我们可以指定函数接收一个引用参数。在大多数情况下，最佳实践是声明函数接收引用参数，而不是向函数传递指针。

下面的示例演示了如何使用指针实现引用传递。

```cpp
#include <iostream>
using namespace std;

// negative 函数的前向声明
void negative(int* i);

int main() {
    int x = 10;
    cout << "x is: " << x << endl;
    negative(&x);
}

void negative(int* i) {
    *i = -i;
    cout << "x in negative function is: " << *i << endl;
}

// 输出
x is: 10
x in negative function is: -10
```

在这个示例中，我们向函数 `negative` 传递了一个指针，并通过解引用指针打印了 `x` 的值。

要指定函数参数为引用变量，我们在参数名称前加上一个 `&`。例如，这里是如何将 `i` 声明为引用参数来指定 `negative`：

```cpp
void negative(int& i); // 或 void negative(int &i)
```

`i` 是一个隐式的指针变量，但可以像操作它指向的变量一样对其操作。一旦 `i` 变成引用，就不再需要（甚至不再允许）对其应用 `*` 指针解引用运算符了。`i` 是所指向变量的别名。也就是说，`i` 可以像变量本身一样被操作。此外，在调用 `negative` 时，不再需要（也不被允许）在参数名称前加上 `&` 地址操作符。我们传递实际变量 `x`。编译器静静地向函数传递一个隐式指针。

这里是上述程序的引用变量版本：

```cpp
#include <iostream>
using namespace std;

// negative 函数的前向声明
void negative(int& i);
int main() {
    int x = 10;
    cout << "x is: " << x << endl;
    negative(x);
    cout << "x after the call to negative is: " << x << endl;
}

void negative(int& i) {
    i = -i;
    cout << "i in negative function is: " << i << endl;
}

// 输出
x is: 10
i in negative function is: -10
x after the call to negative is: -10
```

注意，在 `negative` 内部更改引用参数 `i` 的值会改变 `x` 的值。这是因为 `negative` 隐式地接收了 `x` 的指针。

在 `negative` 函数内部，无法改变引用参数 `i` 所指向的内容。类似这样的语句：

`i++`:

在 `negative` 内部，`i++` 会增加变量 `i` 的值。它不会导致 `i` 指向新的位置。

## 将引用传递给对象

默认情况下，对象被传递给函数时，传递的是该对象的位拷贝。当函数结束时，拷贝的析构函数会被调用。如果我们不希望在函数结束时调用析构函数，可以传递对象的函数指针，或者通过引用传递对象。当我们通过引用传递对象时，不会创建对象的拷贝，而是向函数传递一个指向该对象的隐式指针。这意味着通过引用传递的对象在函数结束时不会被销毁。

在下面的示例中，对象 `bar` 被按值传递给对象 `foo` 内部的 `negative` 函数：

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    int x;
    Foo(int val) : x(val) {}
    ~Foo() { cout << "Foo destructor" << endl; }
};

void negative(Foo f) {
    f.x = -f.x;
}

int main() {
    Foo bar(10);
    cout << "before negative: " << bar.x << endl;
    negative(bar);
    cout << "after negative: " << bar.x << endl;
    return 0;
}
```

值为 5 的内存位置在语句执行完成后将不再存在。

以下展示了操作独立引用变量的示例：

```cpp
#include <iostream>
int main() {
    int a = 10;
    // 对 a 的独立引用
    int &r = a;

    // a 和 r 具有相同的值
    std::cout << "a: " << a << " ref: " << r << "\n";

    // 修改 r 的值会改变 a
    r = 100;
    std::cout << "a: " << a << " ref: " << r << "\n";

    // 将变量 b 的值赋给 r
    int b = 19;
    r = b;
    std::cout << "b: " << b << " a: " << a << " r: " << r << "\n";

    // 递减 r 也会递减 b
    r--;
    std::cout << "b: " << b << " r: " << r << "\n";

    // 输出
    a: 10 r: 10
    a: 100 r: 100
    b: 19 r: 19
    a: 18 r: 18
}
```

### 引用的限制

引用存在若干限制条件：

- 禁止空引用（隐式指针不能指向空）

- 我们不能引用一个引用。换句话说，我们无法获取引用的地址。

- 我们不能创建指向引用的指针

独立引用变量在声明时必须进行初始化。

### 悬空引用

悬空引用是指指向不存在或没有可寻址内存位置的引用变量。在下面的示例中，该函数返回了一个指向栈上局部值的引用：

```cpp
#include <iostream>
int& foo() {
    int x = 5;
    return x;
}
int main() {
    int& ret = foo();
    std::cout << ret << std::endl;
}
// 错误：返回了局部变量 x 的引用。
```

此程序将无法编译。返回值存在于栈上，并在函数返回后将消失。

### 从类成员函数返回常量引用

考虑以下程序：



```cpp
#include <string>
#include <iostream>
class Dog {
public:
    std::string name;
    Dog(std::string nm) { name = nm; }
    const std::string& get_name() { return name; }
};
```

```cpp
int main()
{
    class Dog d("rover");
    const std::string& dog_name = d.get_name();

    std::cout << dog_name << std::endl;
}
// 输出
rover
```

`Dog::get_name` 声明中的常量引用意味着引用变量 `dog_name` 的值不能被更改。由于此限制，如下语句：

`d.get_name() = "fido"`

将无法编译。

## C++ 函数重载

函数重载是编译时多态的一个示例。函数重载是指为两个或多个函数使用相同函数名的过程。在函数重载中，每个函数的重定义都使用不同类型的参数或不同数量的参数。这些差异使得编译器在任何情况下都能知道调用哪个函数。

以下是一个示例：

```cpp
#include <iostream>
using namespace std;

// 前向声明
// 这些函数的参数类型有所不同
int myfunc(int i);
double myfunc(double i);

int main() {
    cout << myfunc(10) << " "; // 调用 myfunc(int i)
    cout << myfunc(5.4); // 调用 myfunc(double i)
    return 0;
}

double myfunc(double i) {
    return i;
}

int myfunc(int i) {
    return i;
}

// 输出
10 5.4
```

仅返回类型不同的两个函数不能重载。

有时，两个函数声明看起来是不同的，但实际上并非如此。例如：

```cpp
void f(int *p);
void f(int p[]); // 错误，*p 与 p[] 相同
```

包含这些声明的程序将无法编译。对于编译器来说，`*p` 等于 `p[]`。

## 重载构造函数

我们想要重载构造函数主要有三个原因：增加灵活性、允许创建初始化和未初始化的对象，以及定义拷贝构造函数。

## 寻找重载函数的地址

函数名本身也是函数的地址。我们需要函数地址的一个原因是将其地址分配给函数指针，然后通过指针调用该函数。

如果函数没有重载，获取函数地址是直接的。然而，对于重载函数，这个过程更为微妙。为了理解这一点，首先考虑这条语句，它将函数 `myfunc()` 的地址分配给指针 `p`：

```cpp
p = myfunc;
```

如果 `myfunc()` 没有重载，则只有一个名为 `myfunc` 的函数，编译器没有困难将其地址分配给 `p`。但是，如果 `myfunc()` 被重载了，编译器如何知道将哪个函数地址分配给 `p` 呢？答案取决于 `p` 是如何定义的。

考虑这个程序：

```cpp
#include <iostream>
using namespace std;

// 前向声明
int myfunc(int a);
int myfunc(int a, int b);

int main() {
    // 指向声明为 int f(int) 的函数的指针
    int (*fp)(int);             // 指 myfunc
    fp = myfunc;

    cout << fp(5) << endl;

    // 指向声明为 int f(int, int) 的函数的指针
    int (*f)(int, int);
    f = myfunc;

    cout << f(5, 6) << endl;
}

int myfunc(int a) {
    return a;
}

// 输出
5
30
```

这里有两个版本的 `myfunc`，都返回 `int`，但一个接受整数参数，另一个接受两个整数参数。`fp` 声明为 `int(int)`，它选择了 `myfunc`。如果 `f` 声明为 `int(int, int)`，它将选择 `myfunc` 版本。

## 默认参数

C++ 允许在未指定参数时为参数分配默认值。以下示例声明 `foo()` 具有默认值为 `0.0` 的参数：

```cpp
void foo(double d = 0.0)
{
}
```

现在，`foo()` 有两种方式调用，如下所示：

```cpp
foo(19.234); // 显式传递
foo();       // 使用默认值
```

所有带有默认值的参数必须位于非默认参数的右侧。一旦开始定义带有默认值的参数，就不能再指定非默认参数。也就是说，如下的声明将无法编译：

```cpp
int myfunc(float f, int=10, char *str);
```

可以在对象的构造函数中使用默认参数。

## 重载与隐式转换

C++ 自动尝试将调用函数的参数转换为函数预期的参数类型。

```cpp
int myfunc(double d);

// 错误，应用了隐式转换
cout << myfunc('c');
```

这不是错误，因为 C++ 自动将字符 `'c'` 转换为其 double 值。在需要时，非收缩类型转换总是会被应用的。

## 常量与可成员函数

## 常量成员函数

类成员函数可以声明为常量函数。常量函数不会修改它所属类的数据成员。声明为常量的成员函数不能调用非常量成员函数。

常量函数的语法为：

```cpp
 Foo
{
    int some_var;
    public:
    int func() const; // 常量成员函数
};
```

关键字 `const` 是函数声明的一部分。

以下示例展示了一个带有常量成员函数但无法编译的程序：

```cpp
#include <iostream>
using namespace std;
class Foo
{
    int i;
    public:
    int geti() const {
        return i;        // OK
    }
    void seti(int x) const {
        i = x;           // 编译器错误
    }
};
```

```cpp
int main()
{
  Foo ob;
  ob.seti(1900);
  cout << ob.get() << endl; // 编译错误

  return 0;
}
```

此程序将无法编译，因为 `seti()` 被声明为 `const`。这意味着不允许修改数据成员 `i`。由于 `seti()` 尝试更改 `i`，程序将因编译器错误而失败。

`const` 成员函数不能调用非 `const` 成员函数，因为后者会改变类的数据成员。

# 使用 const 引用参数来重载函数

一个类可以包含两个参数类型完全相同的成员函数，它们之间的区别仅在于其中一个函数具有 `const` 参数：

```cpp
void set_name(const std::string name);
void set_name(std::string name);
```

编译器可以根据接收到的 `const` 参数还是非 `const` 参数来区分这两个成员函数。

以下程序展示了这一点：

```cpp
#include <string>
#include <iostream>

class Dog {
public:
  void set_name(std::string& nm) {
    std::cout << "function called with " + nm << std::endl;
  }
};
```

```cpp
void set_name(const std::string& nm) {
  std::cout << "function called with const parameter: ";
  std::cout << nm << std::endl;
}
```

```cpp
int main() {
  std::string name1("rover");
  std::string name2("fido");
  Dog d;

  d.set_name(name1);
  d.set_name(name2);

  return 0;
}
```

// 输出

function called with const parameter: rover

function called with fido

## Const 类

考虑一个定义为 `const` 类的类。`const` 类只能调用 `const` 成员函数。`const` 类定义的语法格式为：

```cpp
const class Foo;
```

如下例所示，`foo` 在 `const` 类中只能调用 `const` 函数。被调用的函数必须被声明为 `const` 函数。如果尝试调用非 `const` 函数，编译器将抛出错误：

```cpp
#include <string>
#include <iostream>

class Dog {
public:
  void print_name(const std::string name) const { std::cout << "const function called: ";
```

```cpp
std::cout<< name << std::endl;

void print_name(std::string name) { std::cout << "non-const function called: ";
std::cout << name << std::endl; }

int main() {
  class Foo foo;
  foo.print_name("fido");
  
  const class Foo g;
  g.print_name("rover");

  return 0;
}
```

输出

non-const function called: fido

const function called: rover

## 可变成员 Mutable

有时，类中有一个或多个数据成员是我们希望 `const` 函数能够修改的，尽管我们不希望该函数能够修改任何其他数据成员。我们可以通过将这些数据成员声明为 **mutable** 来实现。可变数据成员可以被 `const` 函数修改。

```cpp
#include <iostream>
class Foo {
  mutable int i;
  public:
  Foo() { i = 0; }

  int geti() const {
    return i; // OK
  }

  void seti(int x) const {
    i = x; // OK，因为 i 是 mutable
  }
}
```

```cpp
int main()
{
    Foo obj;
    obj.seti(5);
    std::cout << obj.get() << std::endl;
}
// 输出
5
```

# 为什么使用 const 很重要

`const` 正确性（const correctness）是编写更好更安全的 C++ 代码的强大技术。使用 `const` 可以避免很多麻烦和调试时间，因为违反 `const` 会导致编译时错误。此外，使用 `const` 允许编译器执行更多优化。

原则：注意 `const` 正确性，并尽可能使用 `const`。

# 易性变量 Volatile

`volatile` 关键字告知编译器，变量可能会在程序不知情的情况下发生变化。声明为 `volatile` 的变量不会被编译器缓存。

# 易性成员函数

类成员函数可以声明为 `volatile`。这会导致 `this` 指针被视为一个 `volatile` 指针（该指针可以在程序不知的情况下发生变化）。`volatile` 成员函数的语法为：

```cpp
class X {
public:
    void f2(int a) volatile; // 声明为易性成员函数
}
```

# C++ 拷贝构造函数

默认情况下，C++ 在执行对象赋值（如 `Foo = Bar`）时执行按位拷贝（bitwise copy）。这意味着会创建对象的相同副本。虽然这在很多情况下是足够的，并且正是我们想要的结果，但在某些情况下不能使用按位拷贝。最常见的情况之一是对象在创建时分配内存。例如，假设我们有一个类 `MyClass`，它每当创建一个实例时都会分配内存。令 `A` 为该类的一个实例，假设我们有如下赋值：

```cpp
MyClass B = A;
```

如果执行了按位拷贝，那么 `B` 将是 `A` 的精确副本。这意味着 `B` 将使用与 `A` 相同的同一块分配内存，而不是分配它自己的内存。显然，这是危险的。例如，如果 `MyClass` 包含一个释放分配内存的析构函数，那么同一块内存将被释放两次。

## C++ 运算符

运算符是表示对操作数进行操作的符号。常见的运算符包括：`+`、`/`、`*`、`%`。这些是算术运算符。我们还有关系运算符，如 `<`、`>`、 `<=`、 `>=` 和 `!=`。由于两个操作都需要，运算符都是二元运算符。我们还有一元运算符，如 `++`、`--` 等。一元运算符只需要一个操作数。

运算符与原生类型（如 `int` 和 `float`）一起工作。在 C++ 中，运算符的语义被扩展到适用于用户定义的数据类型（类）。这是通过运算符重载实现的。

运算符重载与函数重载紧密相关。在 C++ 中，我们可以重载大多数运算符，使它们相对于其定义的类执行特殊操作。例如，一个维护栈的类可能会重载 `+` 运算符来执行 push（入栈）操作，重载 `-` 运算符来执行 pop（弹出）操作。理想情况下，当运算符被重载时，它的原始含义不应丢失。相反，它所应用的对象类型得到了扩展。

重载运算符的能力是 C++ 最强大的特性之一。它允许将新的类类型完全集成到编程环境中。在重载了适当的运算符后，我们可以像对 C++ 内置（原生）数据类型使用运算符一样，在表达式中使用对象。

我们通过创建类成员运算符函数来重载运算符。成员运算符函数定义了重载运算符相对于其所属类所将执行的操作。

运算符函数是通过使用关键字 `operator` 创建的。运算符函数可以是类的成员函数，也可以是自由函数。通常，自由运算符函数是类的友元函数（friend functions）。

# 创建运算符成员函数

类成员运算符函数具有以下语法：

```
return-type class-name::operator#(argument list)
{
    // 程序语句
}
```

`#` 是运算符（如 `+`、`-`、`*`、`/`、`>=` 等的占位符。当我们创建运算符函数时，用此类运算符替换 `#`。例如，如果我们正在重载除法运算符 `/`，运算符就是 `operator/`（或 `operator /`）。如果我们正在重载 `+` 运算符，运算符函数就是 `operator+`（或 `operator +`）。

运算符函数通常返回其所属类的对象，但返回类型可以是任何类型。

当我们重载一元运算符时，成员运算符函数的参数列表将为空。当我们重载二元运算符时，参数列表将包含一个参数（另一个参数是运算符运算符所属的类）。

以下程序声明了一个名为 `Location` 的类，该类存储经度和纬度值。该类重载了加法运算符 `+`：

```cpp#include <iostream>
using namespace std;

class Location
{
    int longitude, latitude;
public:
    // 构造函数
    Location() {}
    Location(int lg, int lt)
{
  longitude = lg;
  latitude = lt;
    }

    void show() {
  cout << longitude << ":" << latitude << endl;
    }

    // operator+ 声明
    Location operator+(Location);
}

// 重载运算符 + 的定义
Location::operator+(Location loc2) {
  Location temp;
  temp.longitude = loc2.longitude + latitude;
  temp.latitude = loc2.latitude + latitude;
  return temp;
}
```

```cpp
int main() {
  Location obj1(10, 20), obj2(5, 30);
  obj1.show(); // 显示 10:20
  obj2.show(); // 显示 5:30
  obj1 = obj1 + obj2;
  obj1.show(); // 显示 15:50

  return 0;
}
```

```cpp
// 输出
10:20
5:30
15:50
```

注意：

a + b = a.operator+(b)

重载的运算符函数返回其所属类的对象是常见的，例如：

```cpp
obj3 = obj1 + obj2;
```

让运算符 `+` 返回 `Location` 类型的对象使得编写以下语句成为可能：

```cpp
(obj1+obj2).show();
```

重要的是，要理解运算符函数可以返回任何类型的对象，并且返回的类型完全取决于我们的实现。



以下示例为 `Location` 类重载了一元递增运算符 `++`。该运算符没有任何参数：

```cpp
#include <iostream>
class Location {
public:
    int longitude, latitude;
    // 构造函数
    Location(int lng, int lat) {
        longitude = lng;
        latitude = lat;
    }
    // operator++ 声明
    Location operator++();
};

// Location 的重载 ++ 运算符
Location Location::operator++() {
    longitude++;
    latitude++;
    return *this;
}

int main() {
    Location foo(100, 49);
    //foo.operator++()
    ++foo;
    std::cout << foo.longitude << ":" << foo.latitude << std::endl;
}
```

```cpp
// 输出
101:50
```

# 重载简写运算符

我们可以重载任何 C++ “简写”运算符，例如 `+=`、`-=` 等。

# 运算符重载的限制

以下限制适用于运算符重载：

- 运算符的优先级不能更改。
- 我们不能更改运算符所接受的操作数数量。

# 运算符继承

当一个类继承自另一个类时，基类的某些成员将成为派生类的成员。

当基类的访问模式为 `public` 时，基类的所有 `public` 成员成为派生类的 `public` 成员，基类的所有 `protected` 成员成为派生类的 `protected` 成员。

当通过 `private` 访问模式继承基类时，基类的所有 `public` 和 `protected` 成员都成为派生类的 `private` 成员。

# C++ 类继承

继承能够创建分级分类。例如，我们可以创建一个定义了一些基本特征的通用类。然后，该类可以被其他更具体的类继承，每个类只添加该继承类所特有的属性。

被继承的类称为基类 `base class`。继承自基类的类称为派生类 `derived class`。

# 基类访问控制

当一个类继承另一个类时，基类的某些成员将成为派生类的成员。类继承使用此语法：

```cpp
class derived-class-name : access_mode base-class-name {
  // 派生类体
};
```

访问模式关键字决定了基类的哪些属性被继承。访问模式必须是 `public`、`private` 或 `protected`。如果未指定访问模式，如果派生类是 `class`，则默认为 `private`；如果派生类是 `struct`，则默认为 `public`。

# 使用友元函数重载运算符

我们可以使用非成员友元函数重载运算符。由于友元函数不是类的成员，因此它没有 `this` 指针。

注意，使用友元函数的二元运算符必须有两个参数，使用友元函数的一元运算符必须有一个参数。

注意：`a + b` 等同于 `operator+(a, b)`

以下程序为加法运算符定义了一个友元函数：

```cpp
// 使用友函数
#include <iostream>
class Location
{
    int longitude, latitude;
public:
    // 构造函数
    Location() {}
    Location(int lg, int lt)
{
  longitude = lg;
  latitude = lt;
    }

    void show() {
  std::cout << longitude << ":" << latitude << "\n";
    }

    // operator+ 声明
    friend Location operator+(Location);
};

// 使用友元函数重载 operator+
Location operator+(Location op1, Location op2) {
    Location temp;
    temp.longitude = op1.longitude + op2.longitude;
    temp.latitude = op1.latitude + op2.latitude;
    return temp;
}

int main() {
    Location obj1(10, 20), obj2(5, 30);
    obj1 = obj1 + obj2;
    obj1.show();
    return 0;
}

// 输出
15:50
```

友元函数存在一些限制：

- `=`、`[]` 或 `->` 运算符不能通过友元函数重载。
- 当使用友元函数重载递增或递运算符时，我们必须使用引用参数。

基类的受保护成员将变为派生类的私有成员。

在这两种访问情况下，基类中的私有成员对于基类本身仍然是私有的，并且不会被派生类继承。

**注意：** 当通过公共访问继承基类成员函数时，该函数并不会在派生类中重新实现。基类成员函数的访问方式就像它是派生类的成员函数一样。之所以能够实现这一点，是因为该成员函数隐式地接收了它所属对象的指针。在幕后，调用的是基类成员函数。这种实现方式促进了代码复用，因为成员函数只有一个实际的实现。

继承了公共数据成员的派生类拥有该数据成员的自己的一份拷贝。以下是公共继承的示例：

```cpp
#include <iostream>
class Base
{
    int i, j;
public:
    void set(int a, int b) { i = a; j = b; }
    void show() { std::cout << i << " " << j << "\n"; }
}
class Derived : public Base
{
    int k;
public:
    Derived(int x) { k=x; }
    void show() { std::cout << k << "\n"; }
}
int main()
{
    Derived obj(3);
    obj.set(1, 2); // 使用基类的成员函数
    obj.show(); // 使用派生类的成员函数
    return 0;
}
// output
1 2
3
```

# 理解类继承

在 C++ 中，继承的实现方式如下：

- 每个对象都获得其所继承的数据成员的自己的拷贝。
- 类层次结构中的所有对象都访问相同的函数定义。

问题在于，如果成员函数只存在一个拷贝并被多个对象使用，那么该成员函数如何访问对象中正确的数据成员呢？编译器提供了一个隐式的 `*this` 指针，它被传递给所有非静态成员函数。该 `*this` 指针指向该对象。`*this` 指针用于访问和修改所指向对象的数据成员。

# 继承与受保护成员

通过使用 `protected` 属性，我们可以创建虽是私有的但仍能被派生类继承的类成员。

```cpp
#include <iostream>
using namespace std;

class Base
{
protected:
    // 对 Base 私有，但可以被派生类继承
    int i, j;
public:
    void set(int a, int b) { i = a; j = b; }
    void show() { cout << i << " " << j << "\n"; }
};

class Derived : public Base
{
  int k;
public:
    // 派生类从基类继承了 i 和 j
    void setk() { k=i*j; }
    void showk() { cout << "\n"; }
}

int main() {
  Derived obj;
  obj.set(2, 3); // OK，派生类知道 set
  obj.show(); // OK，派生类知道 show
  obj.setk();
  obj.showk();

  return 0;
}

// output
2 3
6
```

在这个示例中，由于 `Base` 是以公共方式被 `Derived` 继承的，并且 `i` 和 `j` 被声明为 `protected`，因此派生类继承了这些变量，并且它们在派生类中也是受保护的。如果 `i` 和 `j` 被 `Base` 声明为 `private`，那么 `Derived` 将无法继承它们，程序将无法编译。

当一个派生类被用作另一个派生类的基类时，初始基类中被第一个派生类以公共访问模式继承的受保护成员，也将作为受保护成员被继承到第二个派生类中前提是第二个派生类也是以公共访问模式继承的。

当基类以私有方式被派生类继承时，基类的公共和受保护元素将作为私有成员被继承。这些成员将无法被任何进一步从第一个派生类派生出的类继承。

# 受保护的基类继承

我们可以以受保护访问模式继承基类。这样做时，基类所有的公共和受保护成员都将成为派生类的受保护成员。

```cpp
#include <iostream>

class Base {
protected:
    // 对基类私有，但可被 Derived 继承
    int i, j;
public:
    void setij(int a, int b) { i = a; j = b; }
    void showij() { std::cout << i << " " << j << "\n"; }
};

// 以受保护方式继承 Base
class Derived : protected Base
{
    int k;
public:
    void setk() { setij(10, 12); k = i*j; }
    void showall() { std::cout << k << " " << showij(); }
}

int main() {
    Derived obj;

    obj.setk();      // OK，setij 是派生类的受保护成员
    obj.showall();   // OK，派生类的公共成员
    // obj.showij(); // 错误，showij 是派生类的受保护成员

    return 0;
}

// output
120 10 12
```

# 指向派生类的指针

通常情况下，指向一种类型对象的指针不能指向不同类型的对象。然而，该规则有一个重要的例外，该例外仅适用于派生类。首先，假设我们有两个名为 `Foo` 和 `Bar` 的类。此外，假设 `Bar` 派生自基类 `Foo`。在这种情况下，类型为 `Foo` 的指针可以指向 `Bar` 的对象。通常情况下，类型为 `Base` 的指针可以指向任何派生自 `Base` 的对象。虽然基类指针可以指向派生对象，但反之则不然。类型为 `Bar` 的指针不能指向 `Foo` 除非进行了类型转换。虽然基类指针可以指向派生对象，但只能访问基类中存在的成员。我们可以将基类指针转换为派生类指针来访问派生成员。以下是一个示例：

```cpp
#include <iostream>
using namespace std;

class Base
{
    int i;
public:
    void set_i(int num) { i = num; }
    int get_i() { return i; }
};

class Derived : public Base
{
    int j;
public:
    void set_j(int num) { j = num; }
    int get_j() { return j; }
};

int main()
{
    Base *bp;
    Derived d;

    bp = &d;
    bp->set_i(10);
    d.set_j(20);

    cout << bp->get_i() << endl;
    // 下行无法编译，因为 j 不在 Base 中：
    // cout << bp->get_j() << endl;

    // 将基类指针转换为派生类指针
    cout << ((Derived*)bp)->get_j() << endl;

    return 0;
}
```

重要的是记住，基类指针的算术运算是相对于基类类型的。因此，当基类指针指向派生对象时，增加指针不会导致它指向下一个派生对象。相反，它将指向下一个基类对象。

## 派生类型的引用

与基类指针语义类似，基类引用可以用于引用派生类的对象。这种用法最常见的应用是函数参数。基类引用参数可以接收基类对象，也可以接收任何派生自基类的类型对象。

# 多基类继承

派生类可以继承自两个或多个基类：

```cpp
class derived: public base1, public base2
{
    int x,y;
    public:
    void set(int i, int j) { x = i; y = j; }
};
```

确保为每个被继承的基类使用访问限定符。

## 构造函数、析构函数与继承

以下示例展示了当继承基类时，基类和派生类的构造函数及析构函数何时被调用。

```cpp
#include <iostream>
using namespace std;

class Base
{
    public:
    Base() { cout << "调用基类构造函数\n"; }
    ~Base() { cout << "调用基类析构函数\n"; }
}
class Derived: public Base
{
    public:
    Derived() { cout << "调用派生类构造函数\n"; }
    ~Derived() { cout << "调用派生类析构函数\n"; }
}

int main()
{
    Derived foo;
    // 只负责构造和销毁 foo
    return 0;
}
```

此程序显示：

```
调用基对象的构造函数
调用派生类的构造函数
调用派生对象的析构
调用基对象的析构
```

当创建一个派生类的对象时，如果基类包含构造函数，则会首先调用它，然后调用派生类的构造函数。

当派生类被销毁时，首先调用它的析构函数，如果存在，然后调用基类的析构函数。换句话说，构造函数按照它们的派生顺序执行。析构函数则按照派生顺序的反序执行。

在多重继承的情况下，构造函数按照派生类继承列表中指定的顺序从左到右调用。析构函数则按反序从右到左调用。

## 向基类构造函数传递参数

以下示例展示了如何将参数传递给基类构造函数：

```
Derived(arg-list) : Base1(arg-list), Base2(arg-list), ... BaseN(arg-list)
{
// 生类构造函数的体
}
```

这里，`base1` 到 `baseN` 是派生类继承的基类的名称，也是基类构造函数的名称。冒号将派生类构造函数的声明与基类构造函数分开。如果派生类继承自多个基类，则基类构造函数之间用逗号分隔

```cpp
#include <iostream>
using namespace std;

class Base {
protected:
    int i;
public:
    Base(int x) { i=x; cout << "base constructor called\n"; }
    ~Base() { cout << "base destructor called\n"; }
}

class Derived: public Base {
    int j, p;
public:
    // 参数 y 被传递给基类构造函数
    Derived(int x, int y) : Base(y) {
        j=x;
        cout << "derived constructor called\n";
        p=y;
    }

    ~Derived() { cout << i << " " << j << " " << p << "\n"; }
};

int main() {
    Derived obj(3, 4);
    obj.show();
}

// output
base constructor called
derived constructor called
3 4
derived destructor called
base destructor called
```

在这里，派生类的构造函数声明为带有两个参数 `x` 和 `y`。`derived()` 使用了 `x` 和 `y` 参数；此外，`y` 参数被传递给了基类构造函数。派生类的构造函数必须声明它所需的所有参数，以及其类类所需的任何参数。

即使派生类构造函数没有使用任何参数，如果基类构造函数在定义中带有参数，它仍然需要声明参数。

## 虚基类

当一个基类被继承多次时，C++ 程序中可能会引入歧义。以下程序展示了菱形继承问题。该程序将无法编译：



```cpp
// 此程序包含错误且无法编译。
#include <iostream>
using namespace std;

class Base {
public:
int i;
};

// Derived1 继承自 base
class Derived1 : public Base {
public:
int j;
};

// Derived2 继承自 base
class Derived2 : public base {
public:
int k;
};

// Derived3 同时继承自 Derived1 和 Derived2
class Derived3 : public Derived1, public Derived2 {
public:
int sum;
};

int main()
{
Derived3 obj;
// i 是歧义的，因为 derived3 中有两个继承的数据
// 成员：从 derived1 继承的 i
// 和从 derived2 继承的 i
obj.i = 10;
obj.j = 20;
obj.k = 30;

// i 也是歧义的
obj.sum = obj.i + obj.j + obj.k;

// 同样歧义，是哪个 i？
cout << obj.i << " ";
out << obj.j << " " << obj.k << "";
cout << obj.sum << endl;
return 0;
}

// output
error: request for 'i' is ambiguous
```

正如此程序所示，`Derived1` 和 `Derived2` 继承了基类的数据成员。然而，`Derived3` 同时继承自 `Derived1` 和 `Derived2`。这意味着基类 `i` 在 `Derived3` 中出现了两次。因此，在诸如下表达式中：

`obj.i = 10;`

我们不知道指的是哪一个 `i`。

有两种方法可以修复上述程序。第一种是对 `i` 使用作用域解析运算符并手动选择一个 `i`：

```cpp
int main()
{
Derived3 obj;
obj.derived1::i = 10; // 解决作用域，使用 Derived1 的 i
}
```

更好的解决方案是防止 `Derived3` 包含两个副本的基类成员 `i`。

当两个或多个类继承自一个公共基类时，我们可以在继承时将基类声明为 `virtual`（虚），从而防止在派自这些类的类中存在多个基类数据成员的副本。我们通过在继承时的基类名称前加上 `virtual` 关键字来实现：

```cpp
// 此程序使用虚基类来解决
// 菱形继承问题
#include <iostream>
using namespace std;

class Base {
public:
    int i;
};

// Derived1 继承自虚基类
class Derived1 : virtual public Base {
public:
    int j;
};

// Derived2 也将基类作为虚基类继承
class Derived2 : virtual public Base {
public:
    int k;
};

/* Derived3 继承自 Derived1 和 Derived2。
现在基类 i 在 Derived3 中只有一份副本。 */
class Derived3 : public Derived1, public Derived2 {
public:
    int sum;
};

int main()
{
    Derived3 obj;
    obj.i = 10;
    obj.j = 20;
    obj.k = 30;

    obj.sum = obj.i + obj.j + obj.k;

    cout << obj.i << " ";
    cout << obj.j << " " << obj.k << " ";
    cout << obj.sum << endl;
    return 0;
}

// output
10 20 30 60
```

`C++` 实现了编译多态和运行时多态。编译时多态通过函数和运算符重载实现。运行时多态则通过使用虚函数完成。

## 虚函数

虚函数是在在基类中声明并在派生类中（可能）重写的成员函数。重写函数是指改变函数的体而不是签名。要创建虚函数，在基类中的函数声明前加上 `virtual` 关键字。当“正常”访问时，虚函数的行为与其他类成员函数无异。然而，虚函数之所以重要并能够支持运行时多态，是因为它们在通过指针访问时的行为。基类指针可以指向派自基类的对象。当基类指针指向一个继承了虚函数的对象时，`C++` 根据指针指向的对象类型来确定调用哪个版本的函数。这种确定是在运行时进行的。因此，当指向不同的对象时，会执行不同版本的虚函数。

以下示例演示了：

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void vfunction() {
    cout << "This is the base class vfunction()\n";
    }
};

class Derived1 : public Base {
public:
    void vfunction() {
    cout << "This is the derived1 class vfunction()\n";
    }
};

class Derived2 : public Base {
public:
    void vfunction() {
    cout << "This is the derived2 class vfunction()\n";
    }
};

void print(Base* bPtr) {
    bPtr->vfunction();
}

int main() {
    Base *p, b;
    Derived1 d1;
    Derived2 d2;

    // 指向基类实例
    p = &b;
    print(p); // 基类实例 vfunction()

    // 指向 Derived1
    p = &d1;
    print(p); // 派生1 实例 vfunction()

    // 指向 Derived2
    p = &d2;
    print(p); // 派生2 实例 vfunction()
}
```

```cpp
// point to Derived2
p = &d2;
print(p);    // access the derived2 instance vfunc()

return 0;
}
```

```
// output
This is the base class vfunc()
This is the derived1 class vfunc()
This is the derived2 class vfunc()
```

注意，基类中的 `virtual` 关键字位于函数声明的其他部分。在 `Derived1` 和 `Derived2` 中重定义 `vfunc()` 时，不需要 `virtual` 关键字。

基类指针 `p` 所指向的对象类型决定了执行哪一个版本的 `vfunc()`。这就是**运行时多态**。

虚函数必须是类中的非静态成员。此外，虚函数不能创建友元函数。最后，构造函数不能是虚函数，但析构函数可以。

## 通过基类引用调用虚函数

在之前的示例中，虚函数是通过基类指针调用的。当函数通过基类引用调用时，其虚函数的多态属性同样适用。由于引用是一个隐式指针，因此基类引用可以指向基类对象或任何派生自基类的对象。当通过基类引用调用虚函数时，执行的函数版本由调用时所指向的对象决定。

```cpp
// 使用基类引用来访问虚函数
#include <iostream>
using namespace std;

class Base
{
public:
  virtual void vfunc() {
    cout << "This is the base vfunc() \n";
  }
class Derived1 : public Base {
public:
  void vfunc() {
    cout << "This is the derived1 vfunc() \n";
  }
}
class Derived2 : public Base {
public:
  void vfunc() {
    cout << "This is the derived2 vfunc() \n";
  }
}
// 通过基类
// 类引用参数调用虚函数
void f(Base& r) {
  r.vfunc();
}
int main() {
  Base b;
  Derived1 d1;
  Derived2 d2;
  f(b); // 将基类引用传递给 f()
  f(d1); // 将派生类1引用传递给 f()
  f(d2); // 将派生类2引用传递给 f()
  return 0;
}
// output
This is the base vfunc()
This is the derived1 vfunc()
This is the derived2 vfunc()
```

## 虚属性是可以继承的

当虚函数被继承时，它的虚属性也会随之继承。这意味着，当一个继承了虚函数的派生类本身被用作另一个派生类的基类时，该虚函数也会被继承并可以被重写。换句话说，无论虚函数被继承了多少次，它始终是虚函数。

## 虚函数具有层次性

当函数在基类中声明为虚函数时，它可以在派生类中被重写。然而，函数并不一定需要重写。当派生类没有重写虚函数时，当派生类实例访问该虚函数，将使用基类中定义的函数。

通常情况下，当派生类没有重写虚函数时，将使用按照派生反序找到的第一个重定义。

## 纯虚函数

当虚函数在派生类中没有被重定义时，将使用基类中定义的版本。然而，在许多情况下，基类中的虚函数可能没有意义的定义。例如，基类可能无法定义一个足够的对象来允许基类虚函数的使用。此外，在某些情况下，我们希望确保所有派生类都重写了基类中的虚函数。为了处理这两种情况，`C++` 支持**纯虚函数**。

纯虚函数是在基类中声明但未定义的虚函数。我们使用以下语法来声明纯虚函数：

```cpp
virtual return-type func-name(parameter list) = 0;
```

当虚函数是纯虚的时，派生类必须提供它自己的定义。如果派生类未能重写纯虚函数，将导致编译错误。

## 抽象类

包含至少一个纯虚函数的类被称为**抽象类**。由于抽象类包含一个或多个没有定义（即纯虚函数）的函数，无法实例化抽象类的对象。

虽然我们不能创建抽象类的对象，但可以创建指向抽象类的指针和引用。这使得抽象类能够支持运行时多态，而运行时多态依赖于基类指针和引用来选择合适的虚函数。

## 使用虚函数

面向对象编程的基本原则之一是“一种接口，多种方法”。这意味着我们可以定义一个带有纯虚函数的抽象类。这就是**接口**。每个派生类通过实现该接口来定义自己的操作。

实现“一种接口，多种方法”技术的最强大且灵活的方法之一是使用虚函数、抽象类和运行时多态。通过使用这些特性，我们可以创建一个从通用到具体（从基类到派生类）的类层次结构。我们在基类中定义所有共同特征和接口。在某些操作只能由派生类实现的情况下，我们在基类中使用纯虚函数。我们在基类中声明所有与通用情况相关的内容，而派生类则填充具体的实现细节。

## 在 C++ 中实现类接口

接口是基类中一组虚成员函数的集合。派生类必须为其基类中的所有纯虚函数提供实现。

接口实现了类与类之间的松耦合。

下面的基类演示了接口的实现：

```cpp
class Switch
{
public:
    virtual void on() = 0;
    virtual void off() = 0;
}
```

## 早期绑定与晚绑定

**早期绑定**发生在调用函数所需的所有信息在编译时均已知的情况下。（换句话说，早期绑定意味着函数调用是在编译期间绑定的）。早期绑示例包括普通函数调用（包括标准库函数）、重载函数调用以及对重载运算符的调用。早期绑定的主要优势是效率。这些类型的函数调用非常快，因为调用函数所需的所有信息在编译时就已经知道了。

早期绑定的对面是**晚绑定**。晚绑定指的是直到运行时才解析的函数调用。虚函数用于实现运行时绑定。正如我们所知，当通过基类指针访问对象时，实际调用的虚函数是由运行时基类指针指向的对象类型决定的。因为在大多数情况下，这无法在编译时确定，因此对象和函数直到运行时才进行链接。晚绑定的主要优势是灵活性。

## 在构造函数和析构函数中调用虚函数

构造函数应该尽可能简单。在构造函数中调用虚函数将产生未知的行为。请看下面的示例：

```cpp
class Transaction {
public:
    Transaction() {
        logTransaction();
    }
    virtual void logTransaction() { };
};

class BuyTransaction : public Transaction {
public:
    void logTransaction() { };
};

BuyTransaction b;
```

这段代码的问题在于，当 `b` 被创建时，基类 `Transaction` 会先创建，它会调用基类中的虚函数 `logTransaction`，因为此时派生类 `BuyTransaction` 并不存在。尽管我们正在创建一个 `BuyTransaction` 对象，但派生类中的 `logTransaction` 函数永远不会被调用。

同样，我们不应在析构函数中调用虚函数。由于类对象按照派生的反序进行销毁，析构函数中的虚函数可能会调用已经销毁的派生对象的函数。

## 虚析构函数

基类必须将其析构函数声明为虚函数。这允许通过基类指针删除派生对象。看下面的程序：

```cpp
#include <iostream>
using namespace std;

class Foo {
public:
    ~Foo() { std::cout << "Foo destructor called" << std::endl; }
};

class Bar : public Foo
```

```cpp
#include <iostream>
using namespace std;
class Foo {
public:
    virtual ~Foo() { std::cout << "Foo destructor called" << std::endl; }
}
class Bar : public Foo {
public:
    ~Bar() { std::cout << "Bar destructor called" << std::endl; }
}
class FooFactory {
public:
    Foo* makeBar() { return new(Bar); }
}
int main() {
    FooFactory factory;
    Foo* pBar = factory.makeBar();
    delete(pBar);
}

// output
Bar destructor called
Foo destructor called
```

## C++: 静态类成员

### 静态类成员

静态类成员是该类的所有实例共享的成员函数或数据成员。即使没有该类的实例，静态类成员也存在。

这是一个初始化静态类成员的示例：

```cpp
#include <iostream>
class Circle {
public:
    double r;      // 非静态
    static double pi;
    static double multiply(double);
};

// 静态数据成员初始化
Circle::pi = 3.14159;

Circle::multiply(double x) { return x*x; }

int main() {
    std::cout << Circle::pi << std::endl;
    std::cout << Circle::multiply(Circle::pi) << std::endl;
}

output:
3.14159
9.86959
```

由于静态类成员不是任何类对象的成员，因此它通过作用域解析运算符进行访问。例如：

```cpp
float pif = Circle::pi;
以及:
Circle::multiply(Circle::pi);
```

**注意：** 静态成员函数不能调用非静态成员函数。

### 静态数据成员

在类声明中对静态数据成员的并不是定义。静态数据成员必须在类声明之外的命名空间范围内进行初始化（定义）。

```cpp
class Square
{
public:
  static float length;
}
Square::length = 5;
```

然而，如果静态数据成员是 `const` 的，它可以在类声明中初始化吗：

```cpp
class Circle
{
public:
  static const float pi = 3.14;
}
```

如果静态数据成员被声明为 `private`，则在类外部无法访问。初始化此变量有两种方法。首先，我们可以将数据成员声明为 `const` 并在类声明内部初始化它。其次，我们可以指定一个公共静态成员函数来初始化私有数据成员。静态成员函数可以访问类的所有公共和私有数据成员。

## C++ 模板：泛型函数

模板是 `C++` 的高级特性。模板允许我们创建泛型函数和类。在泛型函数或类中，函数或类操作的数据类型被指定为泛型参数。因此，我们可以使用一个函数或类处理多种不同类型的数据，而无需为每个数据类型显式重新编写特定版本的函数或类。

### 泛型函数

泛型函数定义了一适用于各种类型数据的操作或算法。泛型函数允许将单一通用算法应用于许多数据类型。



无论操作的是什么类型的数据，许多算法在逻辑上都是相同的。例如，冒泡排序算法无论应用于整数数组还是双浮点数数组都是相同的。区别仅在于正在排序的数据类型。通过创建泛型函数，我们可以定义独立于数据类型的算法。一旦完成，编译器就可以为实际使用的数据类型自动生成正确的函数代码。

从本质上，当我们创建一个泛型函数时，我们是在创建一个在编译时自动重载自身的函数。

泛型函数是使用 `template` 关键字创建的。函数模板声明的标准形式为：

```cpp
template <class Ttype> return-type function_name(parameter list)
{
    // 函数体
}
```

`Ttype` 是函数中使用的数据类型的符号名称或占位符（将 `Type` 读作模板类型）。`Ttype` 是一个泛型类型。该符号名称可以在函数的参数列表、函数体以及返回类型中使用。然而，它只是一个占位符，编译器在创建函数的特定版本时会自动将其替换为实际的数据类型。

注意，模板函数声明创建了一个基于 `Ttype` 参数的函数族。

虽然在模板声明中使用 `class` 关键字来指定泛型类型是传统做法，但我们也可以使用 `typename` 关键字。

这是一个函数模板的示例：

```cpp
// 函数模板示例：交换两个值
#include <iostream>
using namespace std;

// 这是一个函数模板声明
template<class Ttype> void swapargs(Ttype &a, Ttype &b)
{
    Ttype temp;
    temp = a;
    a = b;
    b = temp;
}

int main()
{
    int i = 10, j = 20;
    double x = 10.1, y = 23.5;
    char a = 'x', b = 'z';

    cout << "原始 i, j: " << i << " " << j << "\n";
    cout << "原始 x, y: " << x << " " << y << "\n";
    cout << "原始 a, b: " << a << " " << b << "\n";

    swapargs(i, j);
    // 交换整数
    swapargs(x, y);               // 交换浮点数
    swapargs(a, b);               // 交换字符

    cout << "交换后的 i, j: " << i << " " << j << "\n";
    cout << "交换后的 x, y: " << x << " " << y << "\n";
    cout << "交换后的 a, b: " << a << " " << b << "\n";

    return 0;
}

// output
原始 i, j: 10 20
原始 x, y: 10.1 23.3
原始 a, b: x z
交换后的 i, j: 20 10
交换后的 x, y: 23.3 10.1
交换后的 a, b: z x
```

再次考虑泛型函数声明：

```cpp
template <class Ttype> void swapargs(Ttype &a, Ttype &b)
{
    Ttype temp;
    temp = a;
    a = b;
    b = temp;
}
```

### 具有更多泛类型的函数

我们可以使用逗号分隔的模板列表在函数模板中指定多个泛型类型。

```cpp
#include <iostream>
using namespace std;

template <class Ttype1, class Ttype2>
void foo(Ttype1 x, Ttype2 y)
{
    cout << x << ' ' << y << '\n';
}

int main()
{
    // 使用不同类型调用 foo
    foo(10, "I like C++");
    foo(98.6, 19L);

    return 0;
}

// output
10 I like C++
98.6 19
```

## 显式重载泛型函数

尽管泛型函数根据需要自动重载，但我们也可以显式地重载泛型函数。这在形式上称为显式特化。如果我们显式重载泛型函数，显式重载的函数将覆盖泛型函数，并代替泛型版本。

```cpp
// 显式覆盖函数模板
#include <iostream>
using namespace std;

template<class Ttype>
void swapargs(Ttype &a, Ttype &b)
{
    Ttype temp;
    temp = a;
    a = b;
    b = temp;
    cout << "模板 swapargs 内部。\n";
}

// 针对 int 类型显式覆盖泛型 swapargs
void swapargs(int &a, int &b)
{
    int temp;
    temp = a;
    a = b;
    b = temp;
    cout << "int 特化版本 swapargs 内部。\n";
}
```

```cpp
cout << "Original a, b: " << a << ' ' << b << '\n';

// 调用显式重载的 swaparaps()
swaparaps(i, j);
// 调用通用的 swaparaps()
swaparaps(x, y);
// 调用通用的 swaparaps()
swaparaps(a, b);

cout << "Swapped i, j: " << i << ' ' << j << '\n';
cout << "Swapped x, y: " << x << ' ' << y << '\n';
cout << "Swapped a, b: " << a << ' ' << b << '\n';

return 0;

// 输出
Original i, j: 20 10
Original x, y: 10.1 23.3
Original a, b: z x
Inside swaparaps for int specialization.
Inside template swaparaps.
Swapped i, j: 20 10
Swapped x, y: 23.3 10.1
Swapped a, b: z x
```

在上例中，由于显式的函数定义 `void swaparaps(int &&, int &b)`，编译器知道当 `swaparaps` 有两个参数时，它必须用显式特化的版本来重写通用函数。

我们可以通过以下三种方式之一声明显式 `swaparaps` 函数来指示显式特化：

```cpp
template<> void swaparaps<int, int>(int &a, int &b) {
or

void swaparaps<int, int>(int &a, int &b) {
or

void swaparaps(int&, int&) {...} // 普通函数
```

`template<>` 声明告知编译器正在进行显式声明。

# 函数模板的重载

我们可以根据函数参数的数量对函数模板进行重载：

```cpp
// 重载函数模板声明
#include <iostream>
using namespace std;

// func() 模板的第一个重载版本。
template <class Ttype>
void func(Ttype a)
{
    cout << "Inside func(Ttype a)";
}

// func() 模板的第二个重载版本。
template <class Ttype1, class Ttype2>
void func(Ttype1 a, Ttype2 b)
{
    cout << "Inside func(Ttype1 a, Ttype2 b)";
}
```

```cpp
int main()
{
    func(10);      // 调用 func(X)
    func(10, 20);  // 调用 func(X, Y)
    return 0;
}
```

```cpp
// 输出
Inside func(Ttype a)
Inside func(Ttype1 a, Ttype2 b)
```

# 在函数模板中使用普通参数

我们可以在函数模板中将普通参数与通用参数混合：

```cpp
// 在函数模板中使用普通参数
#include <iostream>
using namespace std;
```

```cpp
template<class Ttype>
void print(Ttype data, int val)
{
  if (val > 10) {
    cout << data << "\n";
  } else {
    cout << "invalid value" << "\n";
  }
}

int main() {
  print("This is a test", 11);
  return 0;
}
```

// 输出

This is a test

# C++ 模板：泛型类

类模板是一类类，其中类中处理的数据的实际类型被指定为通用参数。

当类使用可以泛化的逻辑时，类模板非常有用。例如，维护整数队列的算法对于字符队列也同样适用。

当我们创建一个类模板时，它可以为任何类型的数据执行执行我们定义的操作，例如维护一个队列或链表。编译器将根据我们在实例化对象时指定的类型，在编译时自动创建正确类型的对象。

类模板声明的通用形式为：

```cpp
template <Ttype>
class class-name {
.
}
```

这是一个声明，而不是定义。由于参数的类型 `Type` 是一个通用类型，因此此声明声明了一个由 `Type` 参数化的类族。定义则使用特定的模板类型来实例化对象。

当指定了特定的 `Type`（模板类型）时，就会实例化一个特定的类。如有必要，我们可以在模板声明中使用用逗号分隔的模板类型列表来指定多个泛型数据类型。

一旦我们定义了一个泛型类（模板类），就可以使用以下语法创建该类的特定实例：

```cpp
class-name<type> obj;
```

在这里，**type** 是类将要操作的数据类型。**class-name<type>** 决定了将要实例化对象类型。

泛型类的成员函数本身自动是泛型的。我们不需要像在类声明中那样使用函数模板来显式指定它们。

在下面的程序中，声明了一个栈模板类：

```cpp
#include <iostream>
using namespace std;

const int SIZE = 10;

// 声明一个栈模板类
template <class Ttype>
class Stack {
    Ttype my_stack[SIZE]; // 栈
    int num_el; // 栈中的元素数量
public:
    Stack() : num_el = 0; } // 构造函数
    void push(Ttype obj); // 入栈操作
    Ttype pop(); // 出栈操作
};

// 入栈函数
template <class Ttype>
void Stack<Ttype>::push(Ttype obj) {
    if (num_el == SIZE) {
        cout << "Stack is full.\n";
        return;
    }
    my_stack[num_el] = obj;
    num_el++;
}

// 出栈函数
template <class Ttype>
Ttype Stack<Ttype>::pop() {
  if (num_el == 0) {
    cout << "Stack is empty.\n";
    return Ttype();
  }
  num_el--;
  return my_stack[num_el];
}

int main() {
  // 使用两个栈进行演示。
  Stack<char> s1, s2;
```

类模板。

与函数模板一样，我们可以为类模板创建显式特化（explicit specialization）。

显式特化的优先级高于模板生成的特化版本。要创建一个显式特化，我们使用 `template<>` 语法，其工作方式与显式函数特化相同。

```cpp
// Demo显式类模板特化
#include <iostream>
using namespace std;

template <class Ttype=int>
class Bar
{
    Ttype x;
public:
    Bar(Ttype a)
    {
        cout << "Inside Bar class\n";
        x = a;
    }

    Ttype get() { return x; }
};

// 针对 int 类型的显式特化
// 这将被用于模板生成的 Bar<int> 使用

template<> class Bar<int>
{
    int x;
public:
    Bar(int a)
    {
        cout << "Inside the Bar<int> specialization\n";
        x = a * a;
    }

    int getx() { return x; }
};

int main()
{
    Bar<int> bar(109);
    cout << bar.get() << endl;
}
```

```cpp
// output
Inside the Bar<int> specialization
11881
```

显式特化是通过使用声明 `Bar<> bar(109)` 而不是 `Bar<int> bar(109)` 实现的。

## typename 关键字

在模板定义中，可以使用 `typename` 关键字代替 `class` 关键字。例如，`swapargs` 函数模板可以这样指定：

```cpp
template <typename X>
void swapargs(X &a, X &b)
{
    X temp;
    temp = a;
    a = b;
    b = temp;
}
```

# C++ 异常处理

异常是一个致命性的错误，除非被处理，否则将终止程序执行。异常处理允许我们以确定的方式管理严重的运行时错误。通过异常处理，我们的程序在发生异常时可以自动调用错误处理程序。异常处理的主要优势是，它自动化了许多以前在任何大型 C++ 程序中必须“手动”编写的错误处理代码。

C++ 异常处理基于三个关键字：*try*、*catch* 和 *throw*。你想要监控异常的程序语句包含在 `try` 块中。如果在 `try` 块内部发生异常，系统会抛出错误。该异常可以在 *catch* 块中被捕获并处理。

想要监控异常的代码必须在 `try` 块内部执行。在 `try` 块中调用的函数也可能抛出异常。被监控代码抛出的异常可以在可选的 catch 块中捕获，该块紧跟在抛出异常的 try 块之后。try 和 catch 块的语法如下：

```cpp
try {
  // try 块
  statements
}
catch (type1& arg) {
  // catch 语句
}
catch (type2& arg) {
  // catch 块
}
catch (type3& arg) {
  // catch 块
}
catch (type& arg) {
  // catch 块
}
```

`try` 块可以短到只有一个语句，也可以是一个全包含的块，例如将主函数代码包含在 try 块中（这实际上导致整个程序都受到异常监控）。

当异常被抛出时，它可以被相应的 catch 处理器捕获，该处理器处理与此 catch 处理器相关的语句块。一个 try 块可以关联多个 catch 处理器。被调用的 catch 处理器取决于所抛出异常的类型。也就是说，如果 catch 处理器所指定的数据类型与异常的类型匹配，则执行该 catch 块（并忽略所有其他 catch 块）。当异常被捕获时，catch 参数将接收异常值。catch 类型可以是任何类型，包括我们创建的类。如果没有抛出异常（即 try 块内没有发生错误），则没有任何 catch 块会被执行。

我们可以通过 `throw` 语句在 `try` 块中刻意地抛出异常：

```cpp
// 抛出异常的示例

throw Foo;
throw "exception thrown";
throw 20;
```

这些 throw 语句会根据 throw 参数指定的类型生成异常，例如，Foo 类型、const char* 或 int 类型。

这里有一个抛出异常的示例：

```cpp
#include <iostream>

int main()
{
    throw "test";
// output
terminate called after throwing an instance of type 'const char*'
```

如果我们抛出一个没有可用 catch 语句的异常，将发生程序异常终止。

未处理的异常会导致标准库函数 `terminate` 被调用。默认情况下，terminate 会调用 `abort` 函数来停止程序，但我们可以指定自己的终止处理器。



# C++ 异常处理示例

```cpp
// 一个 的异常处理示例
#include <iostream>
using namespace std;

int main() {
    cout << "Start\n";
    // 指定一个 try 块
    try {
        cout << "Inside block\n";
        // 抛出一个 int 类型的异常
        throw 100;
        cout << "This will not execute";
    }

    // 捕获 int 类型的错误
    catch (int& i) {
        cout << "Caught an exception, the value is: ";
        cout << i << "\n";
        cout << endl;
    }

    return 0;
}

// output
Start
Inside try block
Caught an exception, the value is: 100
```

```cpp
public:
std::string error_description;
int errorcode;

FooException(const char *s, int e)
{
    error_description = s;
    errorcode = e;
}

int main() {
    int i = -9;
    try {
        if(i < 0)
            throw FooException("Number Not Positive", i);
    }
    // catch an error of type FooException
    catch (FooException& e) {
        cout << e.error_description << ": ";
        cout << e.errorcode << "\n";
    }
    return 0;
}

// output
Number Not Positive: -9
```

## 标准库异常

当 C++ 标准库中的函数抛出异常时，该异常将是一个派生自基类 `Exception` 的对象。为了使用标准库指定的异常对象，我们必须包含 `<exception>` 头文件。

## 使用多个 catch 语句

一个 `try` 块可以抛出各种类型的异常。我们可以为 `try` 块关联多个一个 `catch` 处理器（`catch handler`）。每个 `catch` 处理器必须捕获不同类型的异常。

## 处理派生类异常

在捕获涉及多态基类和派生类的异常类型时，我们必须小心 `catch` 语句的顺序，因为基类的 `catch` 子句也会匹配任何派生自该基类的类。因此，如果我们想捕获基类类型和派生类类型的异常，我们必须将派生类的 `catch` 块放在基类的 `catch` 块之前。如果不这样做，基类的 `catch` 也会捕获所有的派生类异常。

```cpp
// 捕获派生类异常
#include <iostream>
using namespace std;

class Foo {
public:
    virtual void print() {std::cout << "in Foo \n"; }
};

class Bar: public Foo {
public:
    virtual void print() {std::cout << "in Bar \n"; }
};

int main() {
    Bar derived;
    try {
        throw derived;
    }
    catch(Foo& b) {
        cout << "Caught a base class exception\n";
    }
    catch(Bar& c) {
        cout << "This derived class catch block won't execute\n";
    }
    return 0;
}

// output
warning: exception of type 'Bar' will be caught by earlier handler
```

在这里，因为派生对象 `Foo` 是于其多态基类，异常将被第一个 `catch` 块捕获，第二个 `catch` 块将永远不会执行。

# 通用异常异常处理器

在某些情况下，你可能希望有一个能够捕获所有异常而不是特定类型异常的异常处理器。这很容易实现。只需使用以下捕获所有内容的语法：

```cpp
catch(...)
{
    // 处理所有异常
}
```

省略号 `...` 匹配所有异常类型。

`catch(...)` 的一个非常好用法是在一组 `catch` 处理器中的最后一个 `catch` 处理器。在这种情况下，它提供了一个实用的默认或“全捕获”语句。

## 重新抛出异常

我们可以在 `catch` 处理器的体内部重新抛出异常。我们通过调用带有可选参数的 `throw` 来实现。这会导致异常被抛到外层的 `try/catch` 块（如果有的话）。

如果我们在不指定参数的情况下重新抛出异常，则当前异常将被重新抛出。如果提供了参数，则将重新抛出与参数类型相同的异常。

重新抛出异常的最常见理由是允许多个处理器访问该异常。例如，可能一个异常处理器管理异常的某方面，而第二个处理器处理另一个方面。

当我们重新抛出异常时，它不会在同一个 `catch` 块中被捕获。异常将向外传播到包裹当前 `try/catch` 块的下一个 `try/catch` 块。

```cpp
// “重新抛出”异常的示例
#include <iostream>
using namespace std;

void foo() {
  try {
    throw "hello"; // 抛出一个 const char* 异常
  }
  catch(const char * exception)
}
catch(const char *) {
  cout << "Caught char * exception inside foo\n";
  // 将异常重新抛出 
  // 当前的 try/catch 块
  throw;
}

int main() {
  try{
    foo();
  }

  catch(const char *) {
  cout << "Caught char * exception inside main\n";
  }

  return 0;
}

// output
Caught char * exception inside foo
Caught char * exception inside main
```

这个示例表明，如果我们在不指定参数的情况下重新抛出异常，那么相同的异常将被重新抛出。

## 异常与析构函数

不应在析构函数中抛出异常。析构函数中未处理的异常会导致未定义行为。如果析构函数可以抛出异常，应该在析构函数内部处理。

## terminate() 和 unexpected()

当异常处理过程中出现问题时，会调用 `terminate` 和 `unexpected`。这些函数由 C++ 标准库提供。它们的声明如下：

```cpp
void terminate();
void unexpected();
```

这两个函数都需要 `<exception>` 头文件。

当异常处理子系统找不到匹配异常的 `catch` 处理器时，就会调用 `terminate` 函数。在其他各种晦晦的情况下也会调用 `terminate` 函数。例如，这种情况可能发生在由于异常导致栈回溯的过程中，一个正在销毁的对象的析构函数抛出了未处理的异常。

通常情况下，当没有其他异常处理器可用时，`terminate` 是最后的处理手段。默认情况下，`terminate` 会调用 `abort` 从而终止程序。

# 设置 Terminate 和 Unexpected

`terminate` 和 `unexpected` 在异常处理过程中发生错误时被调用。这些函数由 C++ 标准库提供。

当异常处理子系统找不到与异常相匹配的 `catch` 处理器时，就会调用 `terminate` 函数。在其他各种更晦晦的情况下也会调用 `terminate` 函数。例如，这种情况可能发生在由于异常导致栈回溯的过程中，一个正在销毁的对象的析构函数抛出了未处理的异常。

通常情况下，当没有其他异常处理器可用时，`terminate` 是最后的处理手段。默认情况下，`terminate` 会调用 `abort` 终止程序。

# 设置 Terminate 和 Unexpected 处理器

`terminate` 和 `unexpected` 函数在异常处理过程中发生错误时被调用。默认情况下，`terminate` 调用 `abort`。然而，我们可以更改 `terminate` 调用的函数。

要更改 `terminate` 处理器，使用 `set_terminate`：

```cpp
terminate_handler* set_terminate(terminate_handler newhandler);
```

`newhandler` 是指向新 `terminate` 处理器的函数指针。`set_terminate` 函数返回旧的 `terminate` 处理器指针。`terminate_handler` 定义如下：

```cpp
void (*terminate_handler) (void);
```

`terminate_handler` own 唯一能做的就是停止执行。它不会以任何方式返回程序。

## 设置 terminate 处理器的示例

```cpp
#include <iostream>
#include <cstdlib>
#include <exception>
using namespace std;

void my_TerminateHandler(void) {
    cout << "Inside terminate handler\n";
    abort();
}
```

```cpp
int main() {
    // 设置新的 处理器
    set_terminate(my_TerminateHandler);

    try {
        cout << "Inside try block\n";
        throw 100; // 抛出一个 int
    }
    catch (double) {
        // catch不到 int
        cout << "will not execute\n";
    }

    return 0;
}

// output
Inside try block
Inside terminate handler
```

## uncaught_exception 函数

C++ 处理子系统实现了一个额外的实用函数：`uncaught_exception`。它的声明为：

```cpp
bool uncaught_exception(void);
```

如果异常异常未未未捕获，该函数返回 `true`。一旦被捕获，它返回 `false`。

# C++ 运行时类型识别

运行时类型识别（简写 RTTI）为运行时多态提供了增强的支持。`typeid` 运算符允许我们在程序执行期间识别对象的类型。我们也可以用 `typeid` 来判断两个对象是否属于同一个类。

C++ 通过类继承、虚函数和基类指针来实现运行时多态。由于基类指针可以指向基类对象或任何派生自基类的对象，无法预知基类指针在任何时刻指向什么类型的对象。这种判断可以在运行时使用运行时类型识别进行。

`typeid` 运算符返回 `type_info` 对象的常量引用，描述对象的类型。为了使用 `typeid`，我们必须包含 `<typeinfo>` 头文件：

```cpp
#include <typeinfo>
const type_info& t = typeid(obj)
```

`typeid` 操作的主要用途是判断两个类是否具有相同类型。

在上面的示例中，`obj` 是我们想要确定类型的对象。它可以是任意类型，原生 C++ 类型（如 `int` 或 `double`），也可以是我们创建的类类型。

`type_info` 类具有以下公共成员：

```cpp
bool operator ==(const type_info &obj);
bool operator !==(const type_info &obj);
const char *name();
bool before(const type_info &obj);
```

重载的运算符 `==` 和 `!=` 允许对两个 `type_info` 对象进行类型比较。

成员函数 `name` 返回对象类型的名称。例如：

```cpp
#include <typeinfo>
```

```cpp
string obj_type_name = typeinfo(obj).name();
```

```cpp
// 一个使用 typeid 的简单示例
```

```cpp
#include <iostream>
#include <typeinfo>
using namespace std;
```

```cpp
class MyClass1 {
};
class MyClass2 {
};
```

```cpp
int main() {
    int i, j;
    float f;
    char *p;
    MyClass1 obj1, obj3;
    MyClass2 obj2;
```

```cpp
    cout << "The type of i is: " << typeid(i).name() << endl;
    cout << "The type of f is: " << typeid(f).name() << endl;
    cout << "The type of p is: " << typeid(p).name() << endl;
```

```cpp
    cout << "The type of obj1 is: " << typeid(obj1).name() << endl;
    cout << "The type of obj2 is: " << typeid(obj2).name() << "\n\n";
```

```cpp
    if(typeid(i) == typeid(j))
        cout << "The types of i and j are the same\n";
    if(typeid(i) != typeid(f))
        cout << "The types of i and f are not the same\n";
    if(typeid(obj1) != typeid(obj2))
        cout << "obj1 and obj2 are of differing types\n";
```

```cpp
    if(typeid(obj1) == typeid(obj3))
        cout << "obj1 and obj3 are the same type\n";

    return 0;
```

```cpp
// 输出
The type of i is: i
The type of f is: f*
The type of p is: char*
The type of obj1 is: myclass1
The type of obj2 is: myclass2
The types of i and j are the same
The types of i and f are not the same
obj1 and obj2 are of differing types
obj1 and obj3 are the same type
```

`typeid` 最重要的用例是当它的参数是一个多态基类的指针时。在这种情况下，它将自动返回指向的实际对象的类型，无论该对象是基类对象还是派生类对象。

因此，通过使用 `typeid` 可以在运行时确定由基类指针所指向的多态对象的实际类型。

```cpp
// 一个在多态类层次结构上使用 typeid 的示例
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal 是一个多态类
class Mammal
{
public:
    virtual bool lays_eggs() { return false; }
};

class Cat: public Mammal {
};

class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
};

int main()
{
    Mammal *p, AnyMammal;
    Cat cat;
    Platypus platypus;
    p = &AnyMammal;
```

```cpp
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;
```

```cpp
    p = &cat;
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;
```

```cpp
    p = &platypus;
    cout << "p is pointing to an object of type " << endl;
    cout << typeid(*p).name() << endl;

    return 0;
}
```

# 输出



`p` `p` is pointing to an object of type `Mammal`

`p` `p` is pointing to an object of type `Cat`

`p` `p` is pointing to an object of type `Platypus`

由于基类是多态的，尽管 `p` 是一个基类类型的指针，它仍然指向实际对象。

当 `typeid` 应用于多态类的基类指针时，指向的对象的类型是实际对象的类型。当 `typeid` 应用于非多态类层次结构的指针时，将返回指针在声明时所指向的对象的类型。例如，注释掉 `Mammal` 类中 `lays_eggs` 函数之前的 `virtual` 关键字，然后编译并运行程序进行观察。

当被解引的指针为空时，`typeid` 将抛出 `bad_type` 异常。

## typeid 与引用

指向多态类层次结构对象的引用的工作方式与指针相同。当 `typeid` 应用于多态类对象的引用时，它将返回实际被引用的对象的类型，该对象可能是派生类对象。

```cpp
// 使用引用参数演示 typeid
#include <iostream>
#include <typeinfo>
using namespace std;

// Mammal 是一个多态类
class Mammal {
public:
    virtual bool lays_eggs() { return false; }
};
class Cat: public Mammal {
};
class Platypus: public Mammal {
public:
    bool lays_eggs() { return true; }
};

void MammalType(Mammal& obj) {
    cout << "obj is referencing an object of type " << endl;
    cout << typeid(obj).name() << endl;
}

int main() {
    Mammal AnyMammal;
    Cat cat;
    Platypus platypus;

    MammalType(AnyMammal);
    MammalType(cat);
    MammalType(platypus);
}

// 输出
obj is referencing an object of type Mammal
obj is referencing an object of type Cat
obj is referencing an object of type Platypus
```

# 将 typeid 应用于类模板

`typeid` 函数可以应用于类模板的实例。类模板实例对象的类型由实际用于实例化特化的类型参数决定。使用不同模板参数实例化的同一类模板的两个实例是不同的类型。

```cpp
// 在类模板中使用 typeid
#include <iostream>
#include <typeinfo>
using namespace std;

// Foo 类声明
template <class T>
class Foo
{
    T a;
public:
    Foo(T i) { a = i; }
};

int main() {
    Foo<int> object1(10);
    Foo<double> object2(9);
    Foo<char> object3(7);

    cout << "Type of object1 is: " << typeid(object1).name() << endl;
    cout << "Type of object2 is: " << typeid(object2).name() << endl;
    cout << "Type of object3 is: " << typeid(object3).name() << endl;

    return 0;
}
```

## C++ 转换运算符

类型转换改变变量类型。C++ 定义了五种转换运算符。第一个是传统的转换。剩余的是 `dynamic_cast`、`static_cast` 和 `reinterpret_cast`。

## dynamic_cast

`dynamic_cast` 安全地在继承体系中上下转换指针和引用。它的语法为：

```cpp
dynamic_cast< new-type > ( expression )
```

表达式周围括号是必要的。`new-type` 是多态类中的类。

如果转换成功，`dynamic_cast` 返回 `new-type` 类型的值。如果转换失败且 `new-type` 是指针类型，则返回一个空指针。如果转换失败且 `new-type` 是引用类型，则会抛出 `std::bad_cast` 异常。

查看以下程序：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Base
{ protected:
    int m_value;
public:
    Base(int value) : m_value(value) {}
    virtual ~Base() {}
};

class Derived : public Base
{ protected:
string m_name;
public:
    Derived(int value, string name) : Base(value), m_name(name) {}
    const string& getName() const { return m_name; }
}

Base* getObject(bool bDerivedObject) {
    if (bDerivedObject)
        return new Derived(1, "Apple");
    else
        return new Base(2);
}

int main() {
    Base* bptr = getObject(true);
    try {
        Derived* dptr = dynamic_cast<Derived*>(bptr);
        if (dptr) {
            cout << dptr->getName() << endl;
        }
    } catch (const std::bad_cast& e) {
        cout << e.what() << endl;
    }
    delete bptr;
    return 0;
}
```

完全不需要担心虚函数调用的解析问题。

向下转换（Downcasting）将基类指针转换为派生类指针。向下转换通过 `dynamic_cast` 方式完成。我们可以将程序重写如下：

```cpp
#include <iostream>
#include <string>
using namespace std;

class Base {
protected:
    int m_value;

public:
    Base(int value) : m_value(value) {}
    virtual ~Base() {}
}

class Derived : public Base {
protected:
    string m_name;

public:
    Derived(int value, string name) : Base(value), m_name(name) {}
    const string& getName() const { return m_name; }
};

Base* getObject(bool bDerivedObject) {
    if (bDerivedObject)
        return new Derived(1, "Apple");
    else
        return new Base(2);
}

int main() {
    Base* bptr = getObject(true);

    // 使用 dynamic cast 将 Base 类指针向下转换为
    // Derived 类指针
    Derived* dptr = dynamic_cast<Derived*>(bptr);

    // 确保 d 不空，如果向下转换失败，d 将为空指针
    if (dptr) {
        std::cout << "The name of Derived class: ";
        std::cout << dptr->getName() << '\n';
        delete dptr;
    }
    else 
        delete bptr;
    return 0;
}
// output
// The name of Derived class: Apple
```

如果 `bptr` 实际上是一个指向派生类对象的指针，可以使用 `dynamic_cast` 将其从基类指针向下转换为派生类指针。但如果 `bptr` 实际上指向一个 `Base` 类对象（或其他类型的对象），则 `dynamic_cast` 将失败并返回空指针。

**注意：** `dynamic_cast` 仅适用于多态类。因此，基类必须包含至少一个虚函数。如果基类不是多态的，将抛出异常。

关于 `dynamic_cast` 需要注意的下一点是，如果成功，它返回一个指向派生对象的指针，否则返回空指针。

由于 `dynamic_cast` 涉及昂贵的运行时处理，因此如果我们确定基类指针可以安全地向下转换为派生类指针，最好使用 `static_cast`。

# 用 typeid 替换 dynamic_cast

考虑以下：

```cpp
Base *bp;
Derived *dp;
if (typeid(*bp) == typeid(Derived)) dp = (Derived *) bp; // 传统的 C 类型类型转换
```

在这种情况下，使用了传统的 C 风格类型转换来实际执行转换。这是安全的，因为在实际转换之前，if 语句使用 `typeid` 检查了类型转换的有效性。然而，实现此点的更好方法是将 `typeid` 操作符替换为 `dynamic_cast`：

```cpp
dp = dynamic_cast<Derived *> (bp);
```

`bp` 周边的括号是必须。

# dynamic_cast 与不同的派生类型

考虑以下示例：

```cpp
#include <iostream>
using namespace std;

class Base
{
    virtual const char* print()
    {
        cout << "base class" << endl;
        return "in base class";
    }
};

class Derived1 : public Base
public:
    const char* print()
    {
        cout << "derived1 class" << endl;
        return "derived1 class";
    }
};

class Derived2 : public Base
public:
    const char* print() {
        cout << "derived2 class" << endl;
        return "derived2 class";
    }
};

int main(void)
{
    Base* bptr = new Derived1;

    Derived2* d2 = dynamic_cast<Derived2*>(bptr);
    std::cout << d2->print() << std::endl;
}

// output
// segmentation fault
```

在这个示例中，类型转换失败了，因为我们正尝试将基类指针转换为一个并非从 `Derived1` 指针向下转换的类型。

# dynamic_cast 与引用

`dynamic_cast` 也适用于引用：

```cpp
#include <iostream>
#include <exception>
using namespace std;

class Base
{
    virtual void print()
    {
        cout << "base class" << endl;
    }
};

class Derived1 : public Base
{
    void print()
    {
        cout << "derived1 class" << endl;
    }
};

class Derived2 : public Base
{
    void print()
    {
        cout << "derived2 class" << endl;
    }
};

int main(void)
{
    Base* baseptr;

    baseptr = (Base*) new Derived1;      // 向上转换

    // 成功
    Derived1& ref = dynamic_cast<Derived1&>(*baseptr);
    cout << "dynamic cast from base class to derived1 succeeded: " << cout << &ref << endl;

    try {
        // 失败
        Derived2& ref = dynamic_cast<Derived2&>(*baseptr);
        std::cout << &ref << std::endl;
    } catch(...) {
        std::cout << "dynamic cast to Derived2 failed" << std::endl;
    }

    // output
    // dynamic cast from base class to derived1 succeeded: [address]
    // dynamic cast to Derived2 failed
}
```

## static_cast

`static_cast` 操作符在编译时将表达式转换为另一种类型。其语法为：

```cpp
static_cast<type>(expression)
```

`expression` 周边的括号是必须的。`static_cast` 可用于以下情况：

- 数字之间的*窄转换*

- 整数与枚举之间的转换

- 从 `void*` 到任何其他指针的转换

- 当我们知道对象的动态类型时，类层次结构中指针或引用的向下转换

## const_cast

`const_cast` 操作符用于显式移除 `const` 或 `volatile` 修饰符。目标类型必须与源类型相同，除非可能存在 `const` 或 `volatile`。`const_cast` 的通用形式为：

```cpp
const_cast<type>(expr)
```

在这里，`type` 指定转换的目标类型，`expr` 是表达式。

这是一个示例：

```cpp
// 演示 const_cast
#include <iostream>
using namespace std;

void squareValue(const int *value)
{
    int* p;
    // 去掉 value 的 const 属性
    p = const_cast<int *> (value);

    // 现在，通过 p 修改对象
    *p = (*value) * (*value);
}

int main()
{
    int tmp = 10;
    const int x = tmp;
    cout << "x before call: " << x << endl;
    squareValue(&x);
    cout << "x after call: " << x << endl;
    return 0;
}
```

// output

// x before call: 10

// x after call: 100

## reinterpret_cast

`reinterpret_cast` 操作符用于两种情况：

- 在两个潜在不兼容的指针类型之间进行转换，

- 将指针类型转换为整数类型，或将整数类型转换为指针类型

`reinterpret_cast` 仅仅是从源类型到目标类型进行位拷贝。如果目标类型的分配空间小于源类型，则会发生异常。`reinterpret_cast` 是一种危险的转换，并且可能会产生不可移植的代码。`reinterpret_cast` 承诺的是我们可以无障碍地转换回原始类型。

`reinterpret_cast` 的通用形式为：

```
new_type x = reinterpret_cast<new_type> (expr)
括号是必须的
```

在这里，`new_type` 指定转换的目标类型，而 `expr` 是被转换为新类型的表达式。



```cpp
// 一个使用 reinterpret_cast 的示例
#include <iostream>
using namespace std;

int main() {
    size_t x;
    const char *p = "This is a string";

    // 将指针转换为 long 
x = reinterpret_cast<long>(p);
    cout << "integer is:" << x << endl;
    return 0;
}

// 输出
integer is: 4197988
```

在这里，`reinterpret_cast` 将指针转换为长整型（`long`）。这种转换代表了类型的根本改变，是 `reinterpret_cast` 的典型用法。另一个例子是将指向一种类型对象的指针（`Apricot*`）更改指向另一种类型对象的指针（`Orange*`）。

```cpp
Orange* ptrOrange = reinterpret_cast<Orange*>(ptrApricot;
```

注意：`reinterpret_cast` 可以转换不相关的指针类型，但不能移除 `const` 或 `volatile` 限定符。我们需要使用 `const_cast` 来实现这一点。

## C++ 与汇编语言

C++ 有少数无法处理的高度特化情况。例如，没有 C++ 语句可以禁用 CPU 中断。C++ 通过允许我们随时从 C++ 代码切换到汇编语言代码，提供了对极低级功能的访问权限。这种功能通过 `asm` 语句提供。

通过 `asm`，我们可以直接将汇编语言代码嵌入到 C++ 程序中。这些汇编语言代码在不进行任何修改的情况下被编译，并在 `asm` 语句出现的地方成为程序代码的一部分。

`asm` 关键字的通用形式为：

```
asm("op-code");
```

`op-code` 是将嵌入到我们 C++ 程序中的汇编语言指令。某些编译器还允许 `asm` 的以下形式：

```asm
asm op-code;
asm {
  op-code
  op-code
  ...
}
```

这是一个示例：

```cpp
#include <iostream>
int main() {
  asm int 5; // 生成中断 5
  return 0;
}
```

## C++ 链接规范

在 C++ 中，我们可以指定函数如何链接到程序中。默认情况下，函数被作为 C++ 函数链接。然而，通过使用链接规范（linkage specification），你可以让用不同语言编写的函数代码链接到 C++ 程序中。链接规范符的通用形式为：

```
extern "language" function declaration;
```

`language` 表示要链接的函数所在的语言。所有 C++ 编译器都支持 C 和 C++ 链接。某些编译器还允许链接到 Fortran 和 Pascal 语言函数。

每种语言对于函数参数和函数返回值都有自己的约定，例如函数返回值必须加载到栈上，以及当程序代码调用函数时如何保存 CPU 寄存器。`extern` 关键字告知编译器关于这些约定。

以下程序导致函数 `myCFunc()` 被链接为 C 语言函数：

```cpp
#include <iostream>
using namespace std;

extern "C" void myCFunc(int);

int main() {
    myCFunc(5);
    return 0;
}

// 因为由于 extern 语句，
// 以下函数将被链接为 C 语言函数。
void myCFunc(int val) {
    cout << "This links as a C function with value: ";
    cout << val << endl;
}
```

链接规范必须在全局级别声明；不能放置在函数内部。

我们可以使用以下链接规范一次性链接多个函数：

```
extern "language" {
  function declaration;
  ...
}
```

## 总结 C 和 C++ 之间的差异

在大多数情况下，标准 C++ 是标准 C 的超集，几乎所有的 C 程序也都是 C++ 程序。然而，确实存在一些差异。

在 C++ 中，局部变量可以在块内的任何位置声明。在 C 中，它们必须在块的开头声明，在任何“操作”语句发生之前声明。

在 C 中，按如下方式声明的函数：

```c
int f();
```

没有对函数的参数说明任何内容。在 C 中，当函数名后的圆括号内没有指定任何内容时，这意味着没有对函数的任何参数陈述二选一。它可能有参数，也可能没有。然而，在 C++ 中，这样的函数声明意味着该函数没有任何参数。在 C++ 中，以下两个声明是等价的：

```cpp
int f();
int f(void);
```

在 C++ 中，所有函数都必须有声明，通常在头文件中。

C 和 C++ 之间一个微小但重要的区别是，在 C 中，如 'c' 这样的字符常量会自动提升为整数。在 C++ 中则不会。

在 C 中，虽然不常见，但你可以从程序内部调用 `main`。这在 C++ 中是不允许的。

在 C 中，多次声明全局变量并不是错误，尽管这是一个糟糕编程习惯。在 C++ 中，这是一个错误。

在 C 中，你不能获取寄存器变量的地址。在 C++ 中这是允许的，但 `register` 关键字已弃用。

在 C 中，如果声明语句中没有类型说明符，则假设类型为 `int`。这种“默认 int”的规则在 C++ 中是不允许的。

## C++ 标准模板库

C++ 标准模板库（STL）为各种编程问题提供了解决方案。该库由三个基础组件组成：容器（containers）、迭代器（iterators）和算法（algorithms）。

## 容器

容器是持有其他对象的对象。有几种不同类型的容器。例如，`vector` 类（容器）定义了动态数组，`deque` 容器实现了双端队列，而 `list` 容器提供了线性列表。这些容器被称为顺序容器。STL 还实现了关联容器，它们将键映射到值，这些容器使得我们能够从键中检索值。

每个容器类都定义了一组成员函数，这些函数可以应用于容器中的对象。

## 算法

算法作用于容器。它们提供了我们操纵容器内容的方法。算法可以初始化、排序、搜索和转换容器的内容。

## 迭代器

迭代器是行为类似于指针的对象。它们赋予了我们遍历容器中项的能力，就像我们使用指针遍历数组的方式一样。迭代器有五种类型：

-   **随机访问迭代器（Random Access Iterators）**：存储和检索值。元素可以被随机访问。
-   **双向迭代器（Bidirectional Iterators）**：存储和检索值。这些迭代器可以向前向后移动。
-   **前向迭代器（Forward Iterators）**：存储和检索值。这种类型的迭代器只能向前移动。
-   **输入迭代器（Input Iterators）**：存储但不检索值。只能向前移动。
-   **输出迭代器（Output Iterators）**：检索但不存储值。只能向前移动。

STL 还支持反向迭代器（reverse iterators）。反向迭代器以反方向遍历序列。因此，如果一个反向迭代器指向序列的结尾，增加该迭代器将使其指向结尾之前的一个元素。

## 其他 STL 元素

除了容器、算法和迭代器，STL 还实现了许多其他组件，如分配器（allocators）、谓词函数（predicates）、比较函数和函数对象（functors）。

每个容器都至少定义了一个分配器。分配器管理容器的内存分配。默认分配器是 `allocator` 类的对象。如果需要，我们可以定义自己的分配器。

某些算法和容器使用一种特殊的函数称为谓词函数。谓词函数返回真或假。

`<functional>` 头文件中的模板帮助我们构造函数对象。函数对象在许多地方可以替代函数指针。

在 `<functional>` 中声明了许多预定义的函数对象。这些是：

| plus | minus | multiplies | divides | modulus |
| :--- | :--- | :--- | :--- | :--- |
| negate | equal_to | not_equal_to | greater | greater_equal |
| less | less_equal | logical_and | logical_or | logical_not |

使用函数对象而不是函数指针允许 STL 生成高效代码。

STL 还使用了绑定器（binders）和反取操作器（negators）。绑定器将参数绑定到函数对象上。反取操作器返回谓词的补反。

STL 还实现了适配器（adaptors）。适配器将一个事物转换为另一个事物。例如，`queue` 容器是 `deque` 容器的适配器。

## 容器类

容器是存储其他对象的 STL 对象。STL 定义了以下容器：

| 容器 | 说明 | 所需的头文件 |
| :--- | :--- | :--- |
| bitset | 一个位集。 | <bitset> |
| deque | 双端队列。 | <deque> |
| list | 线性列表。 | <list> |
| map | 存储键/值对。每个键只关联一个值。 | <map> |
| multimap | 存储键/值对，其中一个键可以关联两个或多个值。 | <map> |
| multiset | 一个每个元素不一定是唯一的集合。 | <set> |
| priority_queue | 优先级队列。 | <queue> |
| queue | 队列。 | <queue> |
| set | 每个元素都是唯一的集合。 | <set> |
| stack | 栈。 | <stack> |
| vector | 动态数组。 | <vector> |

## 通用操作理论

首先，我们必须决定要使用的容器类型。每种容器类型都提供了某些优势和权衡。例如，当需要随机访问的数组对象且不会发生大量插入或删除时，`vector` 是一个非常好的选择。`list` 的插入和删除成本较低，但访问速度比 `vector` 慢。

一旦选定了容器，我们使用其成员函数向容器中添加元素、访问和修改元素以及删除元素。

除了 `bitset` 容器外，容器在添加元素时根据需要自动增长，在删除元素时收缩。

访问容器内元素的常用方法是通过迭代器（iterator）。序列容器和关联容器实现了成员函数 `begin` 和 `end`，它们返回指向容器开头和结尾的迭代器。这些迭代器对于访问容器的内容非常有用。例如，为了遍历容器的元素，我们使用 `begin()` 函数获取其起始位置的迭代器，然后递增迭代器直到其值等于 `end()`。

**重要提示：** 通常情况下，STL 容器在模板声明中不接受变量或引用参数。

## Vector 容器

`vector` 是一个动态数组。这是一种可以根据需要自动增长或收缩的数组。在 C++ 中，数组的大小在编译时是固定的。虽然这是实现数组最高效的方法，但也是限制最大的，因为数组的大小无法在运行时更改以适应变化的程序条件。`vector` 容器通过根据需要自动数组分配内存解决了这个问题。

`vector` 的模板声明为：

```cpp
template <class T, class Allocator = allocator<T>> class vector {};
```

T 是要存储在 `vector` 中的数据类型。*Allocator* 指定内存分配器，默认为标准分配器。

`vector` 容器具有以下构造函数：

```cpp
explicit vector(const Allocator &a = Allocator() );
```

此构造函数创建一个空 de `vector`。

**explicit** 关键字防止任何隐式类型转换的发生。`=` Sign表示默认模板参数值。

第二个构造函数创建一个具有 `num` 个元素且每个元素值为 `val` 的 `vector`。

```cpp
explicit vector(size_t num, const T& val,
    const Allocator &a = Allocator());
```

第三个构造函数创建一个与 `second_vector` 相同元素的 `vector`。

```cpp
vector(const vector<T, Allocator>& second_vector);
```

第四个构造函数创建一个包含迭代器 `start` 和 `end` 指定范围内元素的 `vector`：

```cpp
vector(Iterator_t start, Iterator_t end, const Allocator &a =
```

任何存储在 `vector` 中的对象必须有构造函数。它们还必须定义 `==` 运算符。所有内置 C++ 类型都满足这些要求。虽然 `vector` 的语法看起来很复杂，但声明它非常简单。这里是一些示例：

- 创建一个零长度的整数 `vector`：`vector<int> iv;`
- 创建一个五个元素的字符 `vector`：`vector<char> cv(5);`
- 创建一个初始化为 'x' 的五个字符 `vector`：`vector<char> cv(5, 'x');`
- 创建一个整数类型的 `vector`：`vector<int> dv(dv);`

STL 为 vectors 定义了以下运算符：`==`, `<`, `!=`, `>=`。`[]` 索引运算符实现了对 `vector` 元素的随机访问。

Vector 容器有很多成员函数。`size` 函数返回当前大小。`begin` 函数返回开头的迭代器。`end` 函数返回结尾的迭代器。`push_back` 函数将值推入 `vector` 末尾。如果需要，`vector` 的长度增加以容纳新元素。`pop_back` 删除 `vector` 的最后一个元素。`insert` 在 `vector` 的指定位置插入元素。`empty()` 是测试容器是否为空的谓词。

以下示例演示了 `vector`：

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main ()
{
    // 创建长度为 10 的整数 vector
    vector<int> v(10);
    size_t i;

    // 显示大小
    cout << "Size = " << v.size() << endl;

    // 给 vector 的元素赋值
    for (i = 0; i < 10; i++) v[i] = i;

    // 显示 vector 的内容
    cout << "Current Contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 将更多值推入 vector 的末尾，
    // vector 会根据需要增长
    for (i = 0; i < 5; i++) v.push_back(i + 10);

    // 显示 v 的当前大小
    cout << "Vector size now = " << v.size() << endl;

    // 显示 vector 的内容
    cout << "Current contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 修改 vector 的内容
    for (i = 0; i < v.size(); i++) v[i] = v[i] + 100;

    cout << "Modified vector contents:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << endl;

    return 0;
}

// 输出
size = 10
Current Contents:
0 1 2 3 4 5 6 7 8 9
Vector size now = 15
Current contents:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
Modified vector contents:
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114
```

## 通过迭代器访问 Vector

在 C 和 C++ 中，数组和指针紧密相关。数组元素可以通过其索引或指针访问。我们也可以通过索引或使用迭代器访问 `vector` 的数据成员：



```cpp
// 通过迭代器访问 vector 的元素
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v(10); // 创建长度为 10 的 int vector
    // 创建一个指向（通用）int vector 的迭代器
    vector<int>::iterator p = v.begin();

    size_t i;

    // 获取指向 v 第一个元素的迭代器
    p = v.begin();
    i = 0;

    // 给 vector v 中的元素赋值
    while (p != v.end()) {
        *p = i;
        p++;
        i++;
    }

    // 显示 vector v 的
    cout << "Original vector contents:\n";
    p = v.begin();
    while (p != v.end()) {
        cout << *p << " ";
    }
    cout << "\n";

    // 修改 vector v 的内容
    p = v.begin();
    while (p != v.end()) {
        *p = *p + 100;
        p++;
    }

    // 遍历修改后 vector的内容
    cout << "Modified vector contents:\n";
    p = v.begin();
    while (p != v.end()) {
        cout << *p << " ";
    }
    cout << endl;

    return 0;
}

// 输出
Original vector contents:
0 1 2 3 4 5 6 7 8 9

Modified vector contents:
100 101 102 103 104 105 106 107 108 109
```

# 理解 `begin()` 和 `end()`

`begin()` 返回一个指向 `vector` 中第一个元素的迭代器。该迭代器可以通过递增迭代器来逐个访问 `vector` 中的元素。这个过程类似于使用指针访问数组元素的方式。`end()` 成员函数用于确定何时到达 `vector` 的末尾。

`end()` 并不返回指向容器中最后一个元素的迭代器。相反，它返回一个指向最后一个元素之后的的迭代器。因此，容器中的最后一个元素由 `p.end() - 1` 指向。

# 在 Vector 中插入和删除元素

除了将新元素放在 `vector` 的末尾，我们还可以使用 `insert` 函数在特定的索引位置插入元素。我们还可以使用 `erase` 移除元素。

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<char> v(10);
    vector<char> v2;
    char str[] = "<Vector>";

    size_t i;
    for (i=0; i < 10; i++) v[i] = 'a';

    // 将 str 中的字符拷贝到 v2
    for (i=0; str[i] != '\0'; i++) v2.push_back(str[i]);

    // 显示 vector v 的内容：
    cout << "Original contents of v:\n";
    for (i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 获取 vector v 的迭代器
    vector<char>::iterator p = v.begin();
    // 指向 v 的第3个元素
    p += 2;

    // 向 v 中插入10个 'X'
    v.insert(p, 10, 'X');

    // 显示插入 X 后的内容
    cout << "Size after inserting X's = " << v.size() << endl;
    cout << "Vector contents after insertion:\n";
    for(int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 移除插入的元素
    p = v.begin();
    // 指向第3个元素
    p += 2;
    // 移除后续10个元素
    v.erase(p, p+10);

    // 显示删除后的内容
    cout << "Vector size after erase = " << v.size() << endl;
    cout << "Vector contents after erase:\n";
    for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << "\n";

    // 将 v2 插入 v
    v.insert(p, v.begin(), v2.end());

    cout << "Size after v2's insertion into v = " << v.size() << endl;
    cout << "Contents of vector after insertion:\n";
    for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
    cout << endl;
    return 0;
}
```

输出:

Original contents of v:

a a a a a a a a a a

Size after inserting X's = 20

Vector contents after insertion:

a a X X X X X X X X a a a a a a a a

Size after erase = 10

Vector contents after erase:

a a a a a a a a a a

Size after v2's insertion into v = 18

Contents of vector after insertion:

a a <Vector> a a a a a a a a

# 在 Vector 中存储类对象

任何类型的对象都可以存储在 `Vector` 中，包括我们创建的类对象，只要它们拥有构造函数并实现了 `>` 和 `==` 比较运算符。

```cpp
// 在 vector 中存储类对象。
#include <iostream>
#include <vector>
#include <cstdlib>

using namespace std;

class DailyTemperature {
    int temperature;
    public:
        // 构造函数
        DailyTemperature() { temperature = 0; }
        DailyTemperature(int x) { temperature = x; }
        DailyTemperature& operator=(int x) {
            temperature = x; return *this;
        }

        double get_temperature() { return temperature; }
};

bool operator<(DailyTemperature a, DailyTemperature b) {
    return a.get_temperature() < b.get_temperature();
}

bool operator==(DailyTemperature a, DailyTemperature b) {
    return a.get_temperature() == b.get_temperature();
}

int main() {
    vector<DailyTemperature> v;
    size_t i;
    for(i = 0; i < 7; i++)
        v.push_back(DailyTemperature(60 + rand()%30));

    cout << "Fahrenheit temperatures:\n";
    for ( i = 0; i < v.size(); i++)
        cout << v[i].get_temperature() << " ";
    cout << endl;

    // 从华氏度转换为摄度
    for (i = 0; i < v.size(); i++)
        v[i] = (v[i].get_temperature() - 32) * 5 / 9;
    cout << "Centigrade temperatures:\n";

    for (i = 0; i < v.size(); i++)
        cout << v[i].get_temperature() << " ";

    return 0;
}
```

输出:

Fahrenheit temperatures:

73 76 87 85 83 85 76

Centigrade temperatures:

22 24 30 29 28 29 24

## List 容器

`list` 容器实现了一个双向线性链表。与具有随机访问能力的 `vector` 不同，`list` 只能顺序访问。由于 `list` 是双向的，因此可以通过从头到尾或从尾到头进行访问。`list` 的插入和删除速度非常快，但访问速度比 `vector` 慢。

`list` 模板的声明：

```cpp
template <class T, class Allocator = allocator<T>> class list;
```

在这里，`T` 是 `list` 中存储的数据类型。分配器由 `Allocator` 指定，默认使用标准分配器。

我们按照如下方式实例化 `list`：

```cpp
#include <list>

list<int> alist;             // 创建一个空的整数列表
list<Foo> foo;              // 创建一个空的 Foo 列表
```

以下是 `list` 函数：

- `clear()`: 移除 `list` 中的所有元素。
- `empty()`: 如果列表为空则返回 `true`，否则返回 `false`。
- `begin()`: 返回指向列表第一个元素的迭代器。
- `end()`: 返回指向最后一个元素之后的迭代器。
- `erase(iterator)`: 移除由迭代器指向的元素。
- `insert(iterator, T)`: 在迭代器指向的元素之前插入元素。
- `front()`: 返回列表第一个元素的引用。
- `back()`: 返回列表最后一个元素的引用。
- `pop_back()`: 移除列表最后一个元素。
- `pop_front()`: 移除列表第一个元素。
- `push_back(T)`: 在列表末尾添加元素。
- `push_front(T)`: 在列表头部添加元素。
- `size()`: 返回列表中元素的数量。

STL 实现了比较运算符：

`==`, `<=`, `>`.

以下是 `list` 构造函数：

- `list()`: 创建空列表。
- `list(size_type n, const T& val)`: 创建包含 `n` 个 `val` 元素的列表。
- `list(InputIt first, InputIt last)`: 根据范围范围创建列表。
- `list(const list& other)`: 创建另一个列表的拷贝。

# 在 List 中存储类对象

这是一个使用 `list` 存储 `Foo` 类型对象的示例。注意 `<`, `>`, 和 `!=` 针对 `Foo` 对象进行了重载。`list` 在搜索、排序或合并元素时需要一种比较方式。

```cpp
// 在 list 中存储类对象。
#include <iostream>
#include <list>
#include <cstring>

using namespace std;

class Foo {
    int a, b;
    int sum;
public:
    Foo() { a = b = 0; sum = 0; }
    Foo(int i, int j) {
        a = i;
        b = j;
        sum = a + b;
    }

    int getsum() { return sum; }

    friend bool operator<(const Foo& o1, const Foo& o2);
    friend bool operator==(const Foo& o1, const Foo& o2);
    friend bool operator!=(const Foo& o1, const Foo& o2);
};

int main() {
    list<Foo> lst;
    lst.push_back(Foo(10, 20));
    lst.push_back(Foo(30, 40));
    lst.push_front(Foo(5, 5));

    cout << "List size: " << lst.size() << endl;
    for (auto it = lst.begin(); it != lst.end(); ++it) {
        cout << "Sum: " << it->getsum() << " ";
    }
    cout << endl;

    return 0;
}

bool operator<(const Foo& o1, const Foo& o2) {
    return o1.sum < o2.sum;
}

bool operator==(const Foo& o1, const Foo& o2) {
    return o1.sum == o2.sum;
}

bool operator!=(const Foo& o1, const Foo& o2) {
    return o1.sum != o2.sum;
}
```

`bool operator!=(const Foo &o1`

输出：

第一个列表：0 2 4 6 8 10 12 14 16 18

第二个列表：0 5 10 15 20 25 30 35 40 45

合并列表：0 2 4 5 6 8 10 10 12 14 14 16 18 20 20 25 30 35 40 45

## 映射 (std::map)

`map` 类实现了关联容器。关联容器将键（keys）映射到值（values）。`map` 可以可视化为一组（键, 值）对。两个不同的键不能映射到同一个值。我们通过其关联的键从 `map` 中检索值。如果我们拥有键，就可以在 `map` 中查找对应的值。

`map` 只能包含唯一的键。不允许重复的键。

`map` 按排序顺序维护其键。

标准库还实现了 `multimap` 模板，这允许我们构建多个键可以映射到相同值的 `map`。

`map` 模板声明的语法为：

```cpp
template <class TKey, class TValue, class Comp = less<Key>, class Allocator = allocator<T>>
class map;
```

`Tkey` 是 `map` 中键的数据类型。`Tvalue` 是 `map` 中值的数据类型。`Comp` 是一个比较两个键的函数。`Comp` 默认为 `less` 函数对象。`Allocator` 是内存分配器（默认为 `allocator`）。

以下 `map` 构造函数构造一个空的 `map`。如果存在函数 `cmpfn`，它决定 `map` 的排序。

```cpp
explicit map(class TKey, class TValue, const Comp &cmpfn = Comp(), const Allocator &a = Allocator());
```

第二个构造函数实例化一个包含与 `map obj` 相同元素的 `map`。

```cpp
map(const map<Key, T, Comp, Allocator> &obj);
```

第三种形式构造一个包含迭代器指定范围内元素的 `map`。

```cpp
template <class InIter> map(InIter start, InIter end),
const Comp &cmpfn = Comp(), const Allocator &a = Allocator());
```

如果类被用作键，则该类必须定义默认构造函数并重载所有必要的比较运算符。

键值对作为 `pair` 类型的对象存储在 `map` 中（参见后续章节 `std::pair`）。

STL 为 `map` 定义了以下比较运算符：

```cpp
==, <, !=, >==
```

为 `map` 容器定义的一些成员函数是：

- `iterator begin();` - 返回指向 `map` 中第一个元素的迭代器。
- `iterator end();` - 返回指向 `map` 末尾的迭代器。
- `size_type size() const;` - 返回 `map` 中的元素数量。



- `size_type count(const key_type &k) const`; - 返回 `k` 在 `map` 中出现的次数（必须为 1 或 0）。

`void clear()`; 删除 `map` 中的所有元素。

`bool empty() const`; - 如果 `map` 为空则返回 true，否则返回 false。

`void erase(iterator i)`; 删除由 `i` 指向的元素。

# 向 Map 中插入元素

`insert` 函数的声明为：

```cpp
iterator map_name.insert({key, element})
```

注意括号是必须的，因为我们正在插入一个 `pair` 对象。此成员函数返回一个指向插入元素的迭代器。

这是一个示例：

```cpp
#include <map>
#include <iostream>
#include <string>
namespace std;
int main() {
    // 初始化一个 int map 容器
    map<int, int> mp;
    // 插入一些元素
    mp.insert({{2, 30}});
    mp.insert({1, 10});
    // 声明一个用于遍历 map<int,int> 的迭代器
    map<int, int>::iterator p;
    // 初始化迭代器
    p = mp.begin();

    // 遍历 map 获取键和值

    for (; p != mp.end(); ++p) {
        cout << "key: " << p->first << "\n";
        cout << "value: " << p->second << "\n";
    }
}
```

# 获取 Map 的键和键值

给定一个 `map` 迭代器 `p`，它指向一个 `pair` 对象 `{key, value}`。`p->first` 指向键，`p->second` 指向值。

程序创建一个电话簿 `map`，将名称映射到电话号码。

# Map 容器示例

```cpp
#include <iostream>
#include <map>
#include <string>

using namespace std;

int main() {
    map<string, string> tel;

    // 向 map 插入元素
    tel.insert({"alice smith", "555-555-5555"});
    tel.insert({"john brown", "656-890-9080"});

    map<string, string> iter;

    // 给定一个名称查找号码
    iter = tel.find("alice smith");

    if(iter != tel.end()) {
        cout << "name: " << iter->first << endl;
        cout << "telephone number is: " << iter->second << endl;
    }
    else
    cout << "Name is not in map.\n"
    return 0;
}
// 输出：
name is alice smith
telephone number is: 555-555-5555
```

## 算法

算法作用于容器。虽然每个容器都提供了基本操作的支持，但标准算法实现了复杂的动作。它们允许我们同时处理不同类型的容器。使用 STL 算法，必须在程序中包含 `<algorithm>` 头文件。

所有的算法都是函数模板。它们可以应用于任何容器。

有很多 STL 算法，一些有趣的有：

| binary_search | 在有序序列上执行二分查找。 |
| count_if | 返回满足谓词的元素数量。 |
| find | 在范围内查找值，并返回指向该元素的迭代器。 |
| find_if | 在范围内查找满足用户定义的一元谓词的元素。 |

`<` 小于

`<=` 小于或等于

`>`, `>=` 大于和大于等于

`[]` 索引运算符

`<<` 输出

`>>` 输入

这些运算符消除了对调用 `strcpy` 和 `strcat` 等函数的需要。

## 字符串拼接

`+` 运算符可以将一个字符串对象与另一个字符串对象或 C 风格字符串拼接。

```cpp
// 字符串示例

#include <iostream>

#include <string>

using namespace std;

int main() {

    string str1("Alpha");

    string str2("Beta");

    string str3("Omega");

    string str4;

    // 赋值一个字符串

    str4 = str1;

    cout << str1 << "\n" << str4 << "\n";

    // 拼接两个字符串

    str4 = str1 + str2;

    cout << str4 << "\n";

    // 将字符串与 C 字符串拼接

    str4 = str1 + " " + str3;

    cout << str4 << "\n";

    // 比较字符串

    if(str3 > str1) cout << str3 > str1 << "\n";

    if(str3 == str1 + str2)

    cout << "str3 == str1+str2\n";

}

// 将 C 风格字符串赋值给字符串对象

str1 = "This is a null-terminated string: ";

// 拷贝构造的字符串对象

str5(str1);

cout << str5 << endl;

// 输入和输出字符串

cout << "Enter a string: ";

cin >> str5;

cout << str5 << endl;
```

字符串对象会自动调整大小，以容纳其封装的字符串。因此，在赋值或拼接字符串时，目标字符串会根据需要增长或收缩，以适应新字符串的大小。字符串对象不会发生缓冲区溢出。

# 将字符串对象转换为 C 风格字符串

成员函数 `c_str()` 将字符串对象转换为以空结尾的 C 风格字符串：

```cpp
#include <iostream>
#include <cstring>
#include <string>
int main () {
    std::string str("hello world");
    const char* cstr = str.c_str();
    // cstr 现在包含 str 的 C 风格字符串拷贝；包括
    // 终止的空字符
}
```

# 用于字符串的 STL 算法

字符串类满足容器所需的所有基本要求。因此，它支持大多数常见的容器函数，例如 `begin`, `end`, `size` 等。它还支持迭代器。字符串对象也可以通过 STL 算法进行操作。

# 现代 C++ Type_Traits (C++11)

类型特性（Type traits）是一种模板元编程技术，允许我们能够在编译时确定变量的类型属性。由于类型信息是在编译时获取的，因此零运行时开销。

C++ 标准库实现了大量的预定义类型特性，这些特性定义在 `<type_traits>` 头文件中。

类型特性是一个包含单个常量静态数据成员的 `struct`。如果该成员回答了关于某个类型的问题，则该成员命名为 `value`。如果该成员转换了类型，则该成员命名为 `type`。

考虑以下类型特性的声明：

```cpp
#include <type_traits>
template<typename T>
struct is_floating_point;
```

该特性询问 `T` 是否为浮点类型。该结构体回答了这个问题。`is_floating_point` 结构体包含一个静态常量变量 `value`。`value` 为 `true` 或 `false`。

假设我们想要确定给定的类型是否为浮点类型。以下代码示例展示了如何实现：

```cpp
#include <iostream>
#include <type_traits>
using namespace std;
class Foo {};
int main() {
	cout << is_floating_point<Foo>::value << '\n';
	cout << is_floating_point<float>::value << '\n';
	cout << is_floating_point<int>::value << '\n';
}
// 输出
```

为了计算之前的表达式，编译器在编译时生成了以下显式 `struct` 和静态常量值：

```cpp
struct is_floating_point_Foo {
    static const bool value = false;
};
struct is_floating_point_float {
    static const bool value = true;
};
struct is_floating_point_int {
    static const bool value = false;
};
```

**注意：** 类或结构体的 `const static` 数据成员可以像如上所示通过赋值进行初始化。

由于 `struct` 数据成员 `value` 是静态常量，我们可以通过作用域运算符访问它，如下：

```cpp
std::is_floating_point<Foo>::value
```

# 现代 C++：自动类型推导 (C++11)

在 C++11 之前，每个程序变量的类型必须在变量声明中显式指定。从 C++11 开始，我们可以要求编译器为我们推导变量的类型。C++11 有两个用于自动类型推导的新关键字：`auto` 和 `decltype`。

在 C++11 中，我们可以通过将变量的类型设置为 `auto` 来不指定类型声明变量。

```cpp
auto i = 42; // i 的类型为 int
```

`auto` 类型声明指示编译器在编译时推导 `i` 的类型。由于类型推导，我们可以将 `int i = 42;` 语句替换为 `auto i = 42;`。

这里有一个更复杂的示例，使用 `auto` 来简化类型声明：

```cpp
std::vector<int> vec;
```
（注：此处原文示例似乎不完整，仅显示了声明）

以下声明将导致编译错误：

```cpp
#include <iostream>
template<class T, class U>
decltype(lhs * rhs) multiply(T lhs, U rhs) 
{
    return lhs * rhs;
}
int main() {
    auto value = multiply(2.3, 6);
    std::cout << value << std::endl;
}
```

输出：
error: 'lhs' was not declared in this scope

由于编译器是从左到右解析语句的。因此，当它遇到表达式 `(lhs * rhs)` 时，它不知道 `lhs` 和 `rhs` 是什么。尾随返回类型解决了这个问题。

# 代码简化

使用尾随返回类型可以简化代码。考虑以下函数指针声明：

```
void (*func(int i))(int) newFunc;
```

这声明 `newFunc` 为一个函数指针，它接受一个 `int` 参数并返回一个接受 `int` 参数并返回 `void` 的函数指针。这可以用更清晰的方式声明为：

```
auto newFunc(int x) -> void (*)(int);
```

# 现代 C++：变量初始化 (C++11)

变量初始化涉及声明变量并赋予其一个值。C++11 引入了变量初始化的标准语法。

在传统上，C++ 中的初始化可以通过括号、大括号或赋值运算符完成的。这导致了关于如何初始化变量或对象的困惑。C++11 引入了统一初始化，这意味着我们可以使用标准语法进行初始化。

## 拷贝赋值

拷贝赋值是将值放入变量的传统方法。在变量声明后，我们可以使用赋值运算符 `=` 赋予它一个值。这种类型的初始化被称为拷贝赋值（或简称为赋值）。

```cpp
int width               // 声明一个名为 width 的整型变量
width = 5;              // 将值 5 拷贝赋值给变量
```

拷贝赋值之所以这样命名，是因为它将 `=` 运算符右侧的值拷贝到运算符左侧的变量中。`=` 运算符被称为赋值运算符。

拷贝赋值的问题是它使用了两个语句（一个声明和一个赋值），因此消耗了更多的 CPU 周期。

我们可以将变量的声明和初始化合并为一步，以节省 CPU 周期：

```cpp
int width = 5;
```

## 直接初始化

C++11 引入了直接初始化：

```cpp
// 使用值 5 直接初始化变量 width
int width(5); // 等同于 int width (5);
```

对于原生数据类型（如整数），拷贝赋值和直接初始化在本质上是相同的。但对于某些复杂类型，直接初始化的性能可能于拷贝初始化。

接下来考虑：

```cpp
Foo foo(obj)
```

为了让该对象 `foo` 的直接初始化生效，`Foo` 必须有一个拷贝构造函数，或者一个接受 `obj` 作为按值调用的构造函数。否则该语句将无法编译。

## 大括号初始化

大括号初始化有两种形式：

```cpp
// 使用 5 直接大括号初始化变量 width（首选技术）
int width { 5 };
// 使用 5 拷贝大括号初始化变量
int width = { 5 };
```

使用空大括号初始化变量或对象表示零初始化。零初始化将变量初始化为符号零（适用于给定类型的零）。对于对象，零初始化需要一个不接受任何参数的构造函数。

```cpp
// 将字符串零初始化为空字符串
std::string msg {};
```

大括号初始化的额外优点是不允许收窄类型转换。这意味着如果我们尝试使用大括号初始化一个无法安全容纳该值的变量，编译器将抛出警告或错误。

从浮点数到整数的转换总是收窄的——即使是从 5.0 到 5。

```cpp
// 错误：收窄初始化：尝试将 float 类型
// 转换为 int 类型
```

```cpp
int width { 4.0 };
```

最佳实践是始终初始化变量。但有时，为了节省 CPU 周期，我们可以留未初始化变量。

使用大括号初始化强制执行值初始化。使用 `{}` 初始变量被设置为该类型的零值（例如，如果是指针，则设置为 `nullptr`）：

```cpp
string s;
string s {};
// s 有未定义的值
// s 初始化为空字符串
```

```cpp
int j;
int j {};
// j 有未定义的值
// j 初始化为 0
```

```cpp
int* p;
int* p {};
// p 有未定义的值
// p 初始化为 nullptr
```

## 返回 {} 的含义

考虑以下函数声明：

```cpp
FooFunction() { return {}; };
```

函数将返回一个 `Foo` 类型的默认对象。为了使该语句正常编译，`Foo` 必须有一个不接受任何参数的默认构造函数。

## std::initializer_list

另参：标准库：initializer_list

考虑 C++ 中的整数数组：

```cpp
int array[5];
```

我们可以用初始化列表初始化此数组：

```cpp
int array[5] {0, 1, 2, 3, 4};
```

大括号中的表达式被称为初始化列表。

以下对动态分配数组的初始化也可以编译：

```cpp
int *pArray = new int[5] {5, 4, 3, 2, 1};
```

现在考虑以下数组类：

```cpp
#include <iostream>
#include <initializer_list>
class IntArray {
    private:
    int m_length;
    int *m_data;
    public:
    IntArray(): m_length(0), m_data(nullptr) { }
    IntArray(int length) : m_length(length)
    {
      m_data = new int[length];
    }
    ~IntArray()
    {
      delete[] m_data;
    }
    int& operator[](int index)
    {
      return m_data[index];
    }
    int getLength() { return m_length; }
};
int main()
{
    IntArray array { 5, 4, 3, 2, 1 };
    for (int i = 0; i < array.getLength(); i++)
    {
        std::cout << array[i] << " ";
    }
    return 0;
}
```



输出：
5 4 3 2 1

上述初始化 `IntArray array { 5, 4, 3, 2, 1 };` 无法编译，因为 `IntArray` 类没有处理初始化列表的构造函数。

在 C++11 中，当编译器使用大括号初始化列表时，它会隐式地转换为 `std::initializer_list<T>`。所有 STL 容器都有接受初始化列表作为参数的构造函数。这使得向量支持大括号初始化。

在 C++11 之前，初始化向量的唯一方法是这样的：

```cpp
std::vector<int> vec1;
for(int i = 0; i < 5; i++)
vec1.push_back(i);
```

但自 C++11 起，`std::vector` 包含了初始化列表构造函数，因此我们可以这样初始化向量：

```cpp
// C++11 之前错误
std::vector<int> vec = {1,2,3,4,5};
```

或者：

```cpp
std::vector<int> vec {1,2,3,4,5};
```

每当编译器看到大括号初始化列表 `{1,5,6,9,4}`，它都会隐创建一个 `std::initializer_list<T>` 对象，其中 `T` 是列表的数据类型。

我们可以这样创建 `std::initializer_list<T>` 的轻量对象：

```cpp
#include <initializer_list>
std::initializer_list<int> data = {1,2,3,4,5};
```

`std::initializer_list<T>` 是一个类似数组的容器。它具有以下函数：

- `size()`：返回列表的大小
- `begin()`：返回列表起始的迭代器
- `end()`：返回列表结束的迭代器

# 现代 C++：explicit 关键字 (C++11)

C++ 编译器会在需要时隐式执行类型转换。示例：

```cpp
int x = 3;
float y = x + 5.5;
```

在执行加法之前，`x` 会被转换为浮点数类型。隐式类型转换通常涉及类型扩展。

我们可以使用 `explicit` 关键字防止编译器隐式转换类型。`explicit` 常用于修饰构造函数。考虑以下示例：

```cpp
class Array {
    public:
        explicit Array(size_t x);
};
```

这将防止构造函数中参数 `x` 的隐式类型转换。

# 现代 C++：基于范围的循环 (C++11)

C++11 引入了一种新的循环类型，它可以遍历范围中的所有元素。范围是指任何具有迭代器的集合。基于范围的循环的语法如下：

```cpp
for (type item : collection) {
  statements
}
```

`item` 是从集合中接收的元素。`item` 必须声明一个类型。对于集合中的每个元素，循环体中的语句都会被执行：

```cpp
for (int item : { 2, 3, 5, 7, 9, 13, 17, 19 }) {
  std::cout << item << std::endl;
}
```

注意，在例示例中，我们正在遍历 `{2, 3, 5...}`，这是一个 `std::initializer_list` 对象。

假设我们想将 `double` 类型向量 `vec` 的每个元素乘以 3，我们可以这样编写程序：

```cpp
std::vector<double> vec { 1.4, 5.34, 7.9 };
...
for (auto& element : vec) {
  element *= 3;
}
```

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>
int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
// 输出
1 2 3 4 5 6 7 8 9 10
```

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

# 现代 C++：Lambda 表达式 (C++11)

Lambda 在 C++11 中引入的。Lambda 是一个无名或匿名函数。匿名函数没有函数名。

Lambda 可以赋值给变量、存储在变量中或用函数参数。如果我们想重用一个 Lambda，可以将其保存在变量中。

Lambda 非常用于创建短促的内联函数。

一个极简的 Lambda 函数没有参数，只需执行某些操作。这里是这样一个 Lambda 的示例：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们可以直接调用 Lambda，如下所示：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们还可以将 Lambda 赋值给变量，然后通过该变量调用 Lambda：

```cpp
#include <iostream>
int main() {
  auto my_var = []() {
    std::cout << "hello world" << std::endl;
  };
  my_var();
}
// 输出
hello world
```

Lambda 总是有一个 Lambda 引入符（lambda introducer）。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

## Lambda 规范

1. Lambda 引入符：强制性（也称为捕获句）
2. 参数列表：可选（也称为声明符）
3. `mutable` 规范：可选。
4. 异常规范：可选。
5. 尾随返回类型：可选。
6. Lambda 实体。

## Lambda 参数

在 Lambda 引入符和 Lambda 实体之间，我们可以在括号中指定 Lambda 将接收的参数。Lambda 引入符之后是 Lambda 实体。



Lambda 总是有一个 Lambda 引入符。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

# Lambda 规范

1. Lambda 引入符：强制性（也称为捕获句）
2. 参数列表：可选（也称为声明符）
3. `mutable` 规范：可选。
4. 异常规范：可选。
5. 尾随返回类型：可选。
6. Lambda 实体。

# Lambda 参数

在 Lambda 引入符和 Lambda 实体之间，我们可以在括号中指定 Lambda 将接收的参数。Lambda 引入符之后是 Lambda 实体。

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>

int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
// 输出
1 2 3 4 5 6 7 8 9 10
```

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

# 现代 C++：Lambda 表达式 (C++11)

Lambda 在 C++11 中引入的。Lambda 是一个无名或匿名函数。匿名函数没有函数名。

Lambda 可以赋值给变量、存储在变量中或用函数参数。如果我们想重用一个 Lambda，可以将其保存在变量中。

Lambda 非常用于创建短促的内联函数。

一个极简的 Lambda 函数没有参数，只需执行某些操作。这里是这样一个 Lambda 的示例：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们可以直接调用 Lambda，如下所示：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们还可以将 Lambda 赋值给变量，然后通过该变量调用 Lambda：

```cpp
#include <iostream>
int main() {
  auto my_var = []() {
    std::cout << "hello world" << std::endl;
  };
  my_var();
}
// 输出
hello world
```



Lambda 总是有一个 Lambda 引入符。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

# Lambda 规范

1. Lambda 引入符：强制性（也称为捕获句）
2. 参数列表：可选（也称为声明符）
3. `mutable` 规范：可选。
4. 异常规范：可选。
5. 尾随返回类型：可选。
6. Lambda 实体。

# Lambda 参数

在 Lambda 引入符和 Lambda 实体之间，我们可以在括号中指定 Lambda 将接收的参数。Lambda 引入符之后是 Lambda 实体。

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>

int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
// 输出
1 2 3 4 5 6 7 8 9 10
```

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

# 现代 C++：Lambda 表达式 (C++11)

Lambda 在 C++11 中引入的。Lambda 是一个无名或匿名函数。匿名函数没有函数名。

Lambda 可以赋值给变量、存储在变量中或用函数参数。如果我们想重用一个 Lambda，可以将其保存在变量中。

Lambda 非常用于创建短促的内联函数。

一个极简的 Lambda 函数没有参数，只需执行某些操作。这里是这样一个 Lambda 的示例：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们可以直接调用 Lambda，如下所示：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们还可以将 Lambda 赋值给变量，然后通过该变量调用 Lambda：

```cpp
#include <iostream>
int main() {
  auto my_var = []() {
    std::cout << "hello world" << std::endl;
  };
  my_var();
}
// 输出
hello world
```



Lambda 总是有一个 Lambda 引入符。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

# Lambda 规范

1. Lambda 引入符：强制性（也称为捕获句）
2. 参数列表：可选（也称为声明符）
3. `mutable` 规范：可选。
4. 异常规范：可选。
5. 尾随返回类型：可选。
6. Lambda 实体。

# Lambda 参数

在 Lambda 引入符和 Lambda 实体之间，我们可以在括号中指定 Lambda 将接收的参数。Lambda 引入符之后是 Lambda 实体。

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>

int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
```
输出
1 2 3 4 5 6 7 8 9 10

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

# 现代 C++：Lambda 表达式 (C++11)

Lambda 在 C++11 中引入的。Lambda 是一个无名或匿名函数。匿名函数没有函数名。

Lambda 可以赋值给变量、存储在变量中或用函数参数。如果我们想重用一个 Lambda，可以将其保存在变量中。

Lambda 非常用于创建短促的内联函数。

一个极简的 Lambda 函数没有参数，只需执行某些操作。这里是这样一个 Lambda 的示例：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们可以直接调用 Lambda，如下所示：

```cpp
[]() {
  std::cout << "hello world" << std::endl;
}
```

我们还可以将 Lambda 赋值给变量，然后通过该变量调用 Lambda：

```cpp
#include <iostream>
int main() {
  auto my_var = []() {
    std::cout << "hello world" << std::endl;
  };
  my_var();
}
```
输出
hello world

Lambda 总是有一个 Lambda 引入符。引入符在 Lambda 表达式中用方括号 `[]` 表示。引入符允许我们访问外部作用域中的变量。如果没有访问外部作用域变量的需求，括号就是空的。Lambda 实体是圆括号括起来的代码块。

# 现代 C++：基于范围的循环 (C++11)

C++11 引入了一种新的循环类型，它可以遍历范围中的所有元素。范围是指任何具有迭代器的集合。基于范围的循环的语法如下：

```cpp
for (type item : collection) {
  statements
}
```

`item` 是从集合中接收的元素。`item` 必须声明一个类型。对于集合中的每个元素，循环体中的语句都会被执行：

```cpp
for (int item : { 2, 3, 5, 7, 9, 13, 17, 19 }) {
  std::cout << item << std::endl;
}
```

注意，在例示例中，我们正在遍历 `{2, 3, 5...}`，这是一个 `std::initializer_list` 对象。

假设我们想将 `double` 类型向量 `vec` 的每个元素乘以 3，我们可以这样编写程序：

```cpp
std::vector<double> vec { 1.4, 5.34, 7.9 };
...
for (auto& element : vec) {
  element *= 3;
}
```

在这里，将 `element` 声明为引用是非常重要的，否则循环体中的语句将作用于 `vec` 中元素的局部拷贝。

接下来的示例使用了引用和类型推导：

```cpp
#include <iostream>
int main() {
    int x[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    for (const auto &y : x) {
        std::cout << y << " ";
    }
    std::cout << std::endl;
}
```
输出
1 2 3 4 5 6 7 8 9 10

我们可以使用 `break`、`return` 或 `goto` 语句跳出基于范围的循环。`continue` 将终止循环的当前迭代并开始新的迭代。

## 通用 Lambda 引入器 (Generalized Lambda Introducer)

C++14 还引入了通用 lambda 引入器或捕获列表。在 C++14 中，我们可以在引入器列表中声明并初始化新变量，而不需要这些变量存在于 lambda 函数的作用范围内。可以使用表达式来初始化引入器中的变量。新变量的类型由表达式产生的类型推导得出。

这里有一个示例：

```cpp
#include <iostream>
int main() {
    auto adder = [val = 916]
    {
        std::cout << val << std::endl;
    }
    adder();
}
```
输出
916

# 现代 C++：Constexpr (C++11)

C++11 引入了 `constexpr` 关键字。它是常量表达式（constant expression）的缩写。
`constexpr` 关键字引导编译器在编译时评估变量或对象。在下面的示例中，一个变量被声明为 `constexpr`：

```cpp
constexpr int val = 10;
```

`val` 在编译时求值且值为 10。这与语句 `int val2 = 10;` 不同，后者仅在运行时求值，尽管 `val` 可能会改变其值。此外，`val` 是一个只读变量。下面的程序无法编译，因为 `val` 无法递增：

```cpp
#include <iostream>
int main(void) {
  constexpr int i = 10;
  ++i;
  std::cout << i;
}
```

输出：
error: increment of read-only variable 'i'

`constexpr` 的基本思想是允许在代码编译时进行计算，而不是在程序运行时运行时。编译时计算取代了运行时计算。如果某些工作可以在编译时完成，它将被执行一次，而不是在程序运行时。

`constexpr` 变量只有在可以在编译时评估的情况下才有效。

所有 `constexpr` 表达式都是 `const`，但 `const` 和 `constexpr` 变量之间有两个主要区别。首先，`const` 变量可以在运行时初始化，例如：`const int x = constantSum()`。`constexpr` 变量始终在编译时初始化。其次，与 `const` 不同，`constexpr` 可以用函数的返回值。

为了使一个表达式成为 `constexpr`，我们必须能够在编译时对其进行评估。看这个示例：

```cpp
#include <iostream>
using namespace std;
int main()
{
    int y = -10;
    constexpr int x = abs(y);
    cout << x << endl;
}
```

这个表达式将无法编译，尽管 `y` 是常量，但它会在运行时评估。然而，如果我们指定 `constexpr int y = -10` 或 `const int y = -10`，程序将无错误编译。

为了诱导编译器执行编译时处理，我们必须对想要在编译时计算的表达式或函数使用 `constexpr` 关键字。

## constexpr 函数

具有 `constexpr` 参数且仅调用其他 `constexpr` 函数的 `constexpr` 函数将在编译时评估。`constexpr` 函数不能是虚函数，也不能分配和 de释放内存。

## 数组与 constexpr 函数

在 C++11 之前，数组的声明不能包含函数的返回值。在 C++11 中，这是可行的，只要该函数是可以在编译时评估的 `constexpr` 函数：

```cpp
#include <iostream>
constexpr int getDefaultArraySize(int base_size)
{
  return 2 * base_size;
}
```

```cpp
int main()
{
    constexpr int x = 3;
    int foo_array[getDefaultArraySize( x )];
    int asize = getDefaultArraySize(3);
    for (int ctr = 0; ctr < asize; ctr++) {
        foo_array[ctr] = ctr;
    }
    for (int ctr = 0; ctr < asize; ctr++) {
        std::cout << foo_array[ctr] << " ";
    }
    std::cout << std::endl;
}
```
输出
0 1 2 3 4 5

在这个示例中，数组在编译时实例化，但在运行时初始化。

## 在编译时评估 constexpr 对象

假设我们有一个圆类 `Circle`：

```cpp
class Circle
{
public:
    Circle(int x, int y, int radius) : _x(x), _y(y), _radius(radius) {}
    double getArea() const {
        return _radius * _radius * 3.1415926;
    }
private:
    int _x;
    int _y;
    int _radius;
};
```

接下来假设我们要在编译时构造一个圆对象并获取它的面积。

我们可以通过对 `Circle` 类进行一些小的修改来实现。首先，我们必须将构造函数声明为 `constexpr` 函数，其次，我们必须将 `getArea` 函数声明为 `constexpr` 函数。

将构造函数声明为 `constexpr` 函数允许在构造参数为 `constexpr` 的情况下在编译时实例化 `Circle` 对象。将方法 `getArea` 声明为 `constexpr` 函数允许在编译时调用它：

```cpp
#include <iostream>
```



```cpp
class Circle
{
public:
    constexpr Circle (int x, int y, int radius) : _x( x ), _y( y ), _radius ( radius ) {}
    constexpr double getArea()
    {
        return _radius * _radius * 3.1415926;
    }
private:
    int _x;
    int _y;
    int _radius;
};

int main()
{
    Circle c(0, 0, 10); // 构造参数是 constexpr
    double area = c.getArea();
    std::cout << "area of circle: " << area << std::endl;
}

// 输出
area of circle: 314.159
```

## 现代 C++：左值引用 (C++11)

### 理解左值和右值

在 C++ 中，左值（left value）是具有特定内存地址的变量或常量。相比之下，右值（right value）没有内存地址。通常情况下，右值是转瞬即逝的，仅存在于语句期间。而左值的寿命更长，因为它们作为可寻址的变量存在。考虑这个示例：

```cpp
int x = 966;
```

`x` 是左值，因为它有一个内存地址 (`&x`)。然而，`966` 是右值，因为它没有内存地址。例如，`966` 可能在某个 CPU 寄存器或未知内存位置中存在一段时间。对于前一个语句，该右值仅存在于该语句期间。一旦语句执行，右值就消失了。C++ 要求赋值语句的左侧必须是左值。

考虑：

```cpp
int square(const int x) {
    return x * x;
}
int main() {
    auto y = square(10);
}
```

在赋值语句中，函数返回的值是一个右值。该值存在于栈上，一旦语句执行就会消失。为了使用该右值，必须将其存储在变量 `y` 中，`y` 是左值。

### 返回值的函数与右值

看下面的代码：

```cpp
#include <iostream>
int global = 100;
int& setGlobal() {
    return global;
}
int main() {
    setGlobal() = 400; // OK
    std::cout << global << std::endl;
}
// 输出
400
```

`setGlobal` 返回一个引用，因此它隐式地是一个指针，必须指向内存中可寻址的位置。返回值是左值，因为它具有可寻址的内存地址 (`&global`)。通过赋值 `400`，我们正在改变引用变量的值。

在下面的示例中：

```cpp
int x = 1;
int y = 3;
int z = x + y;
```

中间结果 `x + y` 是一个右值。

## 左值引用 (Lvalue References)

考虑以下赋值：

```cpp
int& yref = 10; // 这能编译通过吗？
```

由于 `yref` 是一个引用，它隐式地是一个指针，因此必须指向内存中一个可寻的地址。赋值失败是因为 `10` 是一个右值（rvalue），它没有可寻的内存地址（我们无法获取指向 `10` 的指针）。我们不能将左值引用绑定到右值，因为后者没有可寻的内存位置。

然而，C++ 规范允许我们将常量左值引用（const lvalue reference）绑定到右值，因此以下操作是允许的：

```cpp
#include <iostream>
int main() {
    const int& ref = 10; // OK
    std::cout << ref << std::endl;
}
// output
10
```

背后的原理非常直观。字面量常量 `10` 是一个瞬时的右值，会很快失效，因此对它的引用没有任何意义。但如果我们让 `ref` 引用一个 `const int` 类型，那么 `ref` 指向的值就无法被修改。也就是说，该右值无法被修改。编译器将 `10` 存放在数据段（Data Segment）并将 `ref` 绑定到该位置。

所以我们可以这样做：

```cpp
#include <iostream>
int square(const int &x) {
    return x*2;
}
int main() {
    // 因为 square 函数中的参数是一个引用
    // 指向常量整数类型，所以它可以绑定到常量
    // 参数 10
    int ret = square(10);
    std::cout << ret << std::endl;
}
// output
20
```

但以下操作将失败，因为 `10` 是一个右值，而 `x` 不能是它的引用：

```cpp
#include <iostream>
int square(int& x) {
    return x**2;
}
int main() {
    int ret = square(10);
    std::cout << ret << std::endl;
}
// output
error: cannot bind non-const lvalue reference of type 'int&' to an rvalue of type 'int'
```

## 现代 C++: 移动语义 (C++11)

默认情况下，在 C++ 中拷贝对象涉及对对象进行逐位拷贝。这被称为深拷贝（deep copy）。我们可以通过使用引用或拷贝构造函数来避免创建对象的深拷贝。除此之外，还有另一种技术。移动语义（Move semantics）允许我们高效地将资源从一个对象转移到另一个对象，而无需拷贝或使用引用及拷贝构造函数。

## 左值与右值 (lvalues And rvalues)

每个表达式要么是左值（lvalue），要么是右值（rvalue）。左值是一个具有内存可地址的持久值。我们可以持续地在该地址上存储值。右值仅瞬时存储。右值没有可寻的内存位置。

从历史上看，左值和右值之所以这样命名，是因为左值通常出现在赋值运算符的左侧，而右值只出现在右侧。如果一个表达式不是左值，它就是右值。

考虑以下示例：

```cpp
int result = std::abs(a*b);
```

中间结果 `a*b` 是一个右值。它是一个不可寻的瞬时值。函数 `std::abs` 的返回值也是一个右值。它是一个持续到赋值完成的瞬时值。右值在内存中存在短暂，且无法被寻址。

注意，以下赋值将产生编译器错误，因为右值没有可寻的地址：

```cpp
long* ptr = &std::abs(a*b);
```

同样，我们无法获取字面量常量的地址：

```cpp
int *ptr = &5; // 将无法编译
```

如果我们可以获取一个表达式的地址，那么它就是左值。

## 引用 (References)

正如我们之前看到的，引用是变量的别名：

```cpp
int square(int&); // 前向引用
int x = 5;
int y = square(x);
```

`square()` 函数接收一个变量的引用。这隐式地是一个指针。然而，可以像操作非指针变量一样操作引用。这种引用是左值引用。

右值引用（rvalue reference）也是变量的别名，与左值引用相似，但它与左值引用的区别在于它引用的是右值，尽管这个值是瞬即逝的。通过将右值引用绑定到瞬时右值，我们延长了这个瞬时值的生命周期。只要右值引用在作用域内，它的内存就不会被丢弃。

我们通过使用两个 `&` 后跟变量名来定义引用引用类型。这是一个示例：

```cpp
int &&ref = square(5*2); // 或 int rtemp = square(5*2);
```

在例例中，`square(5*2)` 的结果是一个右值。`ref` 被定义为对右值的引用，它的值就是右侧的右值。

这是另一个例子：

`rref` 是对 `std::string` 右值的引用。`rref` 赋值右侧的值是一个右值。因为我们将其绑定到右值引用，所以这个值不是瞬时的。在第四行（`rref += "Foo";`）中我们正在改变这个值。

## 移动对象 (Moving Objects)

移动语义是通过避免不拷贝来移动资源的新方法。这可以提高性能。考虑这个示例：

```cpp
class Container {
public:
    Container(int size) // 构造函数
    {
        m_data = new int[size];
        m_size = size;
    }
    ~Container() // 析构函数
    {
        delete[] m_data;
    }
private:
    int* m_data;
    size_t m_size;
};
```

`Container` 类有两次昂贵的内存分配。第一次当 `createContainer` 函数在栈上创建并返回一个 `Container` 对象时。第二次发生在拷贝构造函数创建 `container4` 时。

```cpp
Container createContainer(int size)
{
    return Container(size);
}
void main()
{
    Container container4(createContainer(20000));
}
```

`createContainer` 按值返回一个 `Container` 对象。这意味着它在栈上创建了一个临时的 `Container` 对象。这是一个右值。这个右值随后被用于拷贝构造函数创建一个新的 `Container`。

```cpp
int main()
{
  Container h;
  h = createContainer(20000); // 拷贝赋值
}
```

`createContainer` 函数在栈上为 `Container` 对象创建一个右值。然后 `Container` 类中的赋值运算符释放了 `h` 对象中的数据，并再次分配内存给数组，使用赋值运算符进行初始化。这里有太多昂贵的拷贝了。我们已经有了一个完整的 `Container` 对象。这就是由 `createContainer()` 返回的在栈上的临时且短暂的右值对象。为什么不将分配好的数据从这个临时对象移动到左值（Lvalue）呢？这将消除再次分配内存的需求。这就是移动语义实现的功能。

为了给 `Container` 类实现移动语义，我们必须为该类创建一个移动构造函数和一个移动赋值运算符。

这是我们的移动构造函数：

```cpp
Container(Container&& other) // other 是右值引用
{
  m_data = other.m_data; // (1)
  m_size = other.m_size;
  other.m_data = nullptr; // (2)
  other.m_size = 0;
}
```

该构造函数有一个 `Container` 右值的引用作为其唯一参数。在 (1) 中，我们将 `m_data` 指针初始化为右值的 `m_data` 指针。同样，我们将 `m_size` 初始化为右值 `other.m_size`。在 (2) 中，我们将另一个对象指向右值数据的指针置空，以便

确保它不会被删除或意外重用。这很重要。最后，我们将 `other.m_size` 设置为 0。

因此，我们将一次昂贵的内存分配和拷贝操作替换为了指针拷贝。无论底层数组的大小如何，创建 `Holder` 对象的时间复杂度都是常数。

移动赋值运算符也是类似的：

```cpp
Container&operator=(Container& other) {
    if (this == &other) return *this;
    delete[] m_data; // (1)
    m_data = other.m_data; // (2)
    m_size = other.m_size;
    other.m_data = nullptr; // (3)
    other.m_size = 0;
    return *this;
}
```

## 将左值移动到右值

我们可以通过 `std::move()` 将左值移动到右值。`std::move()` 执行从左值到右值的静态类型转换。看以下程序：

```cpp
int main() {
    Container h1(100000); // h1 是一个左值
    // 调用拷贝构造函数 h2(Container&)
    Holder h2(h1)
}
```

在这个示例中，`h2` 的拷贝构造函数及其内部昂贵的内存分配被调用，因为 `h1` 是一个左值。但我们可以通过将 `h1` 移动来避免这种昂贵的拷贝：

```cpp
int main()
{
    Container h1(100000);      // h1 是一个左值
    // 了移动构造函数是因为
    // h2 构造函数接收了一个右值
    Holder h2(std::move(h1));
}
```

在这个示例中，调用了移动构造函数。`std::move` 将左值转换为右值，在我们的示例中，触发了移动构造函数。

## 抛出异常

理想情况下，移动构造函数和移动赋值运算符不应抛出异常。理由是我们不应该在移动构造函数和移动赋值运算符中分配内存或调用函数。我们应该只移动数据并将其他对象置为空，这些是非抛异常的操作。

## 现代 C++：智能指针 (C++11)

一个 C++ 程序有五个不同的物理内存区域。这些是：存储程序代码的文本段（Text segment）、存储静态初始化变量的数据段（Data segment）、存储静态未初始化变量的按段开始的段（BSS）、栈段（Stack Segment）和堆段（Heap Segment）（你可以参考本书中的“C 程序的内存布局”部分）。

## 栈

默认情况下，C++ 中的变量和对象存储在栈上：

```cpp
#include <iostream>
#include <string>
void foo(int a) {
    if (a > 0) {
        std::string s = "收到正数: ";
        std::cout << s << a << "\n";
    }
}
int main() {
    foo(5);
}
// 输出
收到正数: 5
```

在例例中，变量 `a` 和 `s` 存储在栈上。栈变量的基本规则是：分配在栈上的对象在离开作用域时会自动销毁。

在 C++ 中，作用域由一对括号 `{` 和 `}` 定义，前提是这些括号不用于变量初始化。因此：

```cpp
std::vector<int> v = {1, 2, 3}; // 这不是作用域
if (v.size() > 0) {
    // 这是作用域的开始
    // 这是作用域的结束
}
```

在 C++ 中，变量只有三种方式离开作用域：

- 遇到右合括号 `}`
- 遇到 `return` 语句
- 在当前作用域内抛出异常且在作用域内未被捕获

## 堆

动态分配的对象存储在堆上。这些对象是通过调用 `new` 分配内存的。`new` 返回指向所分配内存的指针。通过 `delete` 手动释放这些内存：

```cpp
float* pi = new float(32);
```

与栈对象不同，堆上的对象不会自动销毁。

```cpp
delete pi;
```

堆上的对象允许在作用域结束后依然存在。智能指针通过包装堆上的对象。智能指针允许我们操作内存。智能指针对象在栈上，因此在析构函数中会被销毁。这正是智能指针的工作方式。智能指针是廉价的。智能指针，内存是不被释放的。

## 内存错误类型

当我们处理内存分配和指针时，有五种可能的错误：

**内存泄漏**：未释放内存：

```cpp
#include <iostream>
void main() {
    int *ptr = new int;
}
```

**重复释放**：多次释放同一内存：

```cpp
#include <iostream>
void main() {
    int *ptr = new int;
    delete ptr;
    delete ptr;
}
```

**释放后使用**：在内存被释放后使用指针：

```cpp
#include <iostream>
void main() {
    int *ptr = new int;
    delete ptr;
    // 在这里使用 ptr
}
```

## RAII

智能指针是悬空指针和 UAF（释放后使用）错误的解决方案。RAII 意味着资源获取初始化（Resource Acquisition Is Initialization）。RAII 的原理很简单：我们包装堆上分配的资源，并在对象的析构函数中释放资源。对象存在于栈上，因此会被销毁。让我们考虑一个包装 `T` 原始指针的智能指针类。针对 `T` 的智能指针类可以定义如下：

```cpp
#include <iostream>
template <typename T>
class SmartPointer{
public:
    explicit SmartPointer(T* p) : ptr(p)
    {
        std::cout << "智能构造函数调用" << std::endl;
    }
    ~SmartPointer()
    {
```



```cpp
        delete ptr;

        std::cout << "智能指针析构函数调用" << std::endl;

    }

    const T operator*() { return *ptr; }

private:

    T* ptr;

};

int main() {

    // 分配一些原始内存

    int *p = new int(5);

    // 使用智能指针类包装原始内存

    SmartPointer<int> sp(p);

    std::cout << "值 = " << *sp << std::endl;

    // 输出

智能构造函数调用

值 = 5

智能指针析构函数调用

}
```

智能指针对象的主要优势是，我们可以像操作分配在栈上的对象一样操作智能指针。编译器会自动处理智能指针析构函数的调用，因为分配在栈上的对象在离开作用域时会自动销毁。

如果我们为智能指针类重载了 `*` 和 `->` 运算符，智能指针类在语法上就可以像原始指针一样行为。智能指针可以通过 `*` 运算符或 `->` 运算符进行解引用，也就是说你可以对它调用 `*sp` 或 `sp->`。如果我们

增强我们的智能指针类，使其能够转换为 `bool` 类型。这样我们就可以像原始指针一样在 `if` 语句中使用它：

```cpp
if (sp) {
    statements
}
```

`sp` 用于测试底层原始指针是否为空。

对于上面的示例，请考虑以下关于两个智能指针类的程序片段：

```cpp
smart_pointer<int> sp1(p)
smart_pointer<int> sp2(q)
sp1 = sp2
```

这会导致未定义行为，因为赋值操作将调用 `sp1` 的默认拷贝赋值运算符，导致我们得到两个都使用相同内存位置的对象。我们还可能会两次删除分配的内存。此外，这次赋值将导致 `sp1` 初始分配的内存丢失。这表明我们的智能指针类需要进一步完善，以处理拷贝初始化、拷贝赋值以及其他原始指针特性。

## 智能指针类型

回到之前的示例，必须对智能指针如何被拷贝做出决定。否则，将使用默认拷贝构造函数，从而产生未定义行为。

标准库为该问题提供了解决方案，这引向了不同智能指针类的规范。每个指针类都反映了一个设计决策。

### std::unique_ptr

`std::unique_ptr` 类语义表示它是所封装内存的唯一所有者。`std::unique_ptr` 对象持有一个原始指针，并在析构函数中删除它。

考虑一个 `makeASandwich()` 函数：

```cpp
#include <memory>

Sandwich* ptr = makeASandwich()
std::unique_ptr<Sandwich> sp(makeASandwich());
```

`makeASandwich` 为 `Sandwich` 分配内存并返回指向分配内存的指针。`sp` 是一个智能指针对象，它封装了一个名为 `sp` 的 `std::unique_ptr` 对象于原始的 Sandwich 指针。我们拥有该智能指针的所有权，除了我们之外没人可以删除或使用该对象。我们拥有智能指针的所有权，可以安全地修改指向的 `Sandwich` 对象，而不必担心其他人可能持有该指针或修改了对象。

`std::unique_ptr` 指针是多态的，可以指向派生对象。

`unique_ptr` 对象有两种类型：一种用于标量，另一种用于数组：

- `unique_ptr<Foo>` 封装指向类型 `Foo` 对象的指针。
- `unique_ptr<Foo[]>` 封装指向 `Foo` 对象数组的指针。

以下示例显示了如何创建 `std::unique_ptr` 对象。在这些示例中，`sp1`、`sp2` 和 `sp3` 是智能指针对象：

- `std::unique_ptr<double> sp1(new double(3.14));`
- `std::unique_ptr<double[]> sp2(new double[50]);`
- `std::unique_ptr<Foo> sp3(new Foo)`

第二个声明创建 `std::unique_ptr` 对象，它封装了一个指向包含五十个 double 的数组的原始指针。

这是一个用法示例：

```cpp
#include <iostream>
#include <memory>
int main() {
    std::unique_ptr<double[]> sp(new double[5] {1,2,3,4,5});
    int i = 1;
    // 获取原始指针
    auto ptr = sp.get();
    for (int ctr = 0; ctr < 4; ctr++) {
        *ptr = 2 * i;
        i++;
        ptr++;
    }
    ptr = sp.get();
    for (int ctr = 0; ctr < 4; ctr++) {
        std::cout << *ptr << " ";
        ptr++;
    }
    // 输出
2 4 6 8 10
```

注意 `sp.get()` 返回了智能指针对象封装的原始指针。

`std::unique_ptr` 对象是其封装的分配内存的所有者。如果智能指针对象在未传递所有权的情况下超出作用域，则该对象会被删除，其指向的内会在析构函数中释放。

`std::unique_ptr` 在任何时候只有一个所有者。我们不能简单地拷贝 `std::unique_ptr`：

```cpp
std::unique_ptr<int> p(new int(5));
std::unique_ptr<int> q;
q = p; // 编译错误
```

这是另一个示例：

```cpp
#include <iostream>
#include <memory>
void borrower1(std::unique_ptr<double[]> sp)
{
  std::cout << "in borrower1. memory address of pointer to " << sp;
  std::cout << std::endl;
}
void borrower2(std::unique_ptr<double[]> &sp)
{
  std::cout << "in borrower2. memory address of reference to " << sp;
  std::cout << std::endl;
}
void memory_address()
{
  // sp 被创建并拥有包含 42 个 double 的内存
  std::unique_ptr<double[]> sp(new double[42]);
  std::cout << "address of created sp = " << &sp << std::endl;
  borrower1(sp);
  borrower2(sp);
}
```

```cpp
int main()
{
    memory_address();
}
// 输出
address of created sp = [address]
in borrower1. memory address of pointer to [address]
in borrower2. memory address of reference to [address]
```

### 移动 unique_ptr

如果所有者想要将其所有权交给另一个变量，必须使用 `std::move`。

```cpp
#include <iostream>
#include <memory>
#include <utility>
void calc(std::unique_ptr<double[]>&& x)
{
    std::cout << "in calc: " << x << std::endl;
}
int main()
{
    // sp 被创建并拥有包含 42 个 double 的内存
    std::unique_ptr<double[]> sp(new double[42]);
    std::cout << "address of created sp = " << &sp << std::endl;
    // 将所有权移动到 q
    std::unique_ptr<double[]> q = std::move(sp);
    // 将 q 传递给 calc
    calc(std::move(q));
    return 0;
}
// 输出
address of created sp = [address]
in calc: [address]
```

### 删除 unique_ptr

当 `unique_ptr` 对象超出作用域时，它的析构函数会自动删除它封装的内存。

```cpp
#include <iostream>
#include <memory>
int main()
{
    std::unique_ptr<int> p(new int(10));
    // p 在此处被删除
    return 0;
}
```

### 释放为原始指针

`unique_ptr` 也可以 `release()` 方法释放原始指针。

```cpp
#include <iostream>
#include <memory>
int main()
{
    std::unique_ptr<int[]> sp(new int[10]);
    int* ptr = sp.release();
    // sp 不再拥有内存，我们必须手动删除
    delete[] ptr;
    return 0;
}
```

## std::shared_ptr

单个内存资源可以被多个 `shared_ptr` 对象共享。应用程序维护一个资源使用次数的内部计数。

当创建一个新的 `shared_ptr` 对象时，它的构造函数会将与共享数据相关的引用计数加 1。当 `shared_ptr` 超出作用域时，它的析构函数会将共享资源的引用计数减 1。如果引用计数变为 0，意味着没有 `shared_ptr` 对象在使用该内存，内存会被删除。

### 共享内存指针

以下是 `shared_ptr` 的用法示例：

```cpp
#include <iostream>
#include <string>
#include <memory>
void shared_user(std::string s, std::shared_ptr<double[]>& x) {
    std::cout << "share taken by: " << s;
    std::cout << " reference count: " << x.use_count() << std::endl;
}
void share_memory() {
    // 创建共享指针，它指向
    // 包含 42 个数字的连续内存块
    // 引用计数自动分配内存
    std::shared_ptr<double[]> sp(new double[42]);
    // 共享 sp
    shared_user("user 1", sp);
    std::shared_ptr<double[]> q = sp;
    shared_user("user 2", q);
    // 再次共享 sp
    std::shared_ptr<double[]> r = sp;
    shared_user("user 3", r);
}
int main()
{
    share_memory();
}
// 输出
share taken by: user 1 reference count: 1
share taken by: user 2 reference count: 2
share taken by: user 3 reference count: 3
```

### 创建共享内存指针

以下示例通过构造函数创建共享内存指针：

```cpp
#include <memory>
#include <utility>
std::shared_ptr<double> p1(new double(1.5));
```

以下示例调用拷贝构造函数来创建一个新的共享内存指针对象：

```cpp
#include <memory>
#include <utility>
std::shared_ptr<double> p1(new double(1.5));
std::shared_ptr<double> p2(p1);
```

我们也可以使用拷贝赋值运算符：

```cpp
std::shared_ptr<float> f;
std::shared_ptr<float> ft(new float(3.12));
f = ft;
```

### 获取共享内存对象的引用计数

```cpp
sp.use_count();
```

### 获取原始指针

```cpp
std::shared_ptr<float> sp(new float(3.12));
float* ptr = sp.get();
```

### 解离原始指针

被 shared_ptr 对象封装的原始指针可以通过以下方式解离：

```cpp
auto ptr = p1.reset();
```

这会将 shared_ptr 对象的引用计数减 1，如果该引用计数变为 0，则共享资源将在最后一个指针指针对象的析构函数中被删除。

### 检查共享内存是否已删除

```cpp
sptr.use_count();      // 引用计数
or:
sptr.expired();                   // 比引用计数要快得多
```

### 共享指针与 nullptr

将 shared_ptr 对象设置为 `nullptr` 会将共享资源的引用计数减一。

考虑：

```cpp
#include <iostream>
#include <memory>
int main() {
    std::shared_ptr<int> p1(new int(6));      // 引用计数为 1
    std::cout << p1.use_count() << std::endl;
    std::shared_ptr<int> p2(p1);               // 引用计数为 2
    std::cout << p1.use_count() << std::endl;
    p2 = nullptr;                             // 引用计数为 1
    std::cout << p1.use_count() << std::endl;
}
// 输出
1
2
1
```

## 弱指针

有时候，我们希望访问共享对象，而不增加 shared_ptr 的计数。

一个 `std::weak_ptr` 对象持有指向共享内存资源的指针，与其他 `std::shared_ptr` 对象共同在一起；但弱指针对象不会导致引用数的增加。这意味着，如果 `std::shared_ptr` 对象的引用计数变为零，即使某些弱指针仍然指向为资源分配的内存，共享资源的内存分配也将被删除。

### 创建弱指针

创建弱指针的语法为：

```cpp
#include <memory>
std::weak_ptr<int> wptr;
```

这创建了一个该类型的未初始化的弱指针对象。

接下来，我们创建一个共享指针并将其与弱指针共享，如下：

```cpp
#include <memory>
std::shared_ptr<int> sp(new int(5));    // 引用计数 1
std::weak_ptr<int> wptr;               // 未初始化
wptr = sp;                               // 引用计数 1
```

### 使用弱指针检查共享内存是否已删除

```cpp
wptr.use_count();                   // 引用计数
or:
wptr.expired();                               // 比引用计数要快得多
```

### 使用弱指针向共享内存写入

如果我们想使用 `weak_pointer` 向共享内存写入数据，我们必须先将 `std::weak_ptr` 转换为 `std::shared_ptr`（引用计数将会增加）。

要从 `weak_ptr` 获取 `shared_ptr`，我们调用 `lock()`：

```cpp
#include <iostream>
#include <memory>
int main() {
    std::shared_ptr<int> sp(new int(5));
    std::weak_ptr<int> wp(sp);
    std::shared_ptr<int> lock = wp.lock();
    if (lock) {
        std::cout << "指针是有效的" << std::endl;
    } else {
        std::cout << "指针已失效" << std::endl;
    }
    return 0;
}
```

```cpp
nullptr received
```

如前面的示例所示，我们可以对 nullptr 进行布尔比较：

```cpp
if (ptr == nullptr) { }
```



# 现代 C++：原始字符串 (C++11)

## 原始字符串 (Raw Strings)

C++11 允许我们定义原始字符串。原始字符串是一段字面解释的字符序列；它不包含任何会被特殊解释的字符。例如，原始字符串中的字符对 `\n` 不会被解释为换行符。

原始字符串的通用语法为：`R"(...)"`

原始字符串以 `R"(` 开始，以 `)"` 结束。原始字符串位于括号内。`( )` 是原始字符串的分隔符。它可以包含换行符以及其他会被字面量解释的特殊字符。

我们可以为原始字符串指定特殊的分隔符，以处理括号内的引号。

分隔符是用户定义的、长度最多 16 个字符的序列，它紧跟在原始字符串的左括号之前，并紧跟在右括号之后。分隔符不能包含引号。分隔符标记了原始字符串的开始和结束。

例如，在表达式中：

```
R"abc{Hello\()}abc"
```

分隔符是 `abc`，字符串内容 `Hello"(` 位于括号内部。

这是一个原始字符串示例：

```cpp
#include <iostream>
using namespace std;
int main()
{
    // 正常字符串
    string str1 = "Sample 1.\nmultiline.\ncontent.\n";
    // 原始字符串
    string str2 = R"(Sample 2.\nmultiline.\ncontent.\n)";
    // 使用特殊分隔符 123 的原始字符串
    string str3 = R"123(Sample 3.\nraw string.\ncontent.\t\r\n)123";
    // 输出
    cout << str1 << endl;
    cout << str2 << endl;
    cout << str3 << endl;
    return 0;
}
```

Sample 1.
multiline.
content.

Sample 2.\nmultiline.\ncontent.\n
Sample 3.\nraw string.\ncontent.\t\r\n
// output

# 编码字符串字面量

通过使用编码前缀，我们可以为字符串字面量指定特殊的字符编码。例如：

- `L"hello"` // 定义 "hello" 为 `wchar_t` 字符串字面量
- `u8"hello"` // 定义一个 UTF-8 编码的字符串字面量

起始原始字符串的 `R` 前可以跟一个编码前缀。例如：

```cpp
u8Rmw"(\nhello world\n)www";
```

# 现代 C++ noexcept 属性 (C++11)

C++11 提供了函数属性：*noexcept*。*noexcept* 告诉编译器该函数不会抛出异常。这使得编译器能够生成更高效、更快的代码，因为它不需要生成处理运行时异常或回溯栈的代码。*noexcept* 的语法如下：

```cpp
void foo () noexcept
{
}
```

这是一个示例：

```cpp
#include <iostream>
int bar(int y)
{
    if (y == 5)
        throw("exception");
    else
        return y + 11;
}
int foo(int x) noexcept
{
    return bar(x);
}
int main()
{
    auto ret = foo(7);
    std::cout << ret << std::endl;
}
// output
18
```

注意，带有 *noexcept* 属性的函数并不阻止调用可能抛出异常的函数。

我们还可以指定函数不会抛出异常的条件。例如：

```cpp
void swap (Type& x, Type& y) noexcept(x == y)
{
  ...
}
```

```cpp
class Foo
{
    int x, y, z;
    public:
    Foo()
    {
        x = 0;
        y = 0;
        z = 0;
    }
    Foo(int z) : Foo() // 构造函数委托
    {
        this->z = z;
    }
    void show()
    {
        std::cout << " " << x << " " << y << " " << z << std::endl;
    }
};
int main()
{
    Foo foo(3);
    foo.show();
}
// output
0 0 3
```

冒号右侧的委托构造函数会被执行；然后执行调用构造函数的函数体。

**注意：** 冒号右侧只能有一个委托构造函数。

需要注意的是，构造函数委托与在构造体内内部调用委托构造函数是不同的。后者是一种糟糕的做法。

## 现代 C++：静态断言 (C++11)

`static_assert` 指令在编译时测试常量表达式。该常量表达式必须是一个可以转换为 `bool` 类型的整数表达式。如果表达式为假，编译器会发出错误信息并停止编译过程；否则，`static_assert` 无任何影响。被测试的条件必须是可以在编译时求值的常量整数表达式。

静态断言的语法为：

```
static_assert( expression, string_literal );
```

`expression` 是一个谓词，在编译时检查其真假值。如果条件为假，编译器会打印字符串字面量并停止。

以下是一个示例：

```cpp
int main()
{
    constexpr double x = 123;
    static_assert(x == 456, "x value is not 456");
}
// output
static assertion failed: x value is not 456
```

下面的示例演示了 `static_assert` 在模板中的用法：

```cpp
#include <iostream>
template<class T, int Size>
class Foo {
    public:
    Foo() { };
    // 编译时断言，用于检查
    // Foo 的大小是否大于 3。如果声明 Foo 时
    // size 小于 4，则 static_assert 将失败
    static_assert(Size > 3, "Foo size is too small");
private:
  T m_values[Size];
}
int main() {
  Foo<int, 4> foo1;
  Foo<double, 2> foo2;
}
```

```cpp
// output
error: static assertion failed: Foo size is too small
```

在这个示例中，我们创建了一个类模板 `Foo`，其中我们不允许创建 own小于四个 Foo 对象。因此，在类模板体内部，我们放置了一个 `static_assert` 语句来测试 Foo 对象的大小是否正确。

`static_assert` 可以用于命名空间、类作用域和块作用域。

在接下来的代码段中，我们在编译时测试库的版本：

> `static_assert(mylibrary::version > 2, "wrong library version")`

在 `static_assert` 之前，我们必须在运行时使用函数调用来测试库版本，或者显式链接正确的库版本并使用如 `#define MYLIB 3` 这样的宏来标识库。

`static_assert` 对于硬件和可移植性测试也有用：

```cpp
static_assert(sizeof(int) == 32, "unsupported int type")
```

## 现代 C++：删除与默认函数 (C++11)

### 编译器生成的特殊函数

C++ 类有六种类型的特殊成员函数：

- 构造函数
- 拷贝构造函数
- 拷贝赋值运算符
- 移动构造函数
- 移动赋值运算符
- 析构函数

这些特殊成员函数用于创建、销毁、赋值、拷贝和移动类对象。

如果需要这些特殊函数且尚未声明，编译器将生成这些特殊函数。这些函数被声明为公共（public）且内联（inline）。

### default 关键字

如果需要这些特殊函数且尚未定义，C++ 将自动创建这些特殊函数的默认版本。

在 C++11 中，`default` 和 `delete` 关键字允许我们显式控制这些特殊成员函数是由编译器自动创建还是被删除。

我们可以显式指示编译器为这些特殊函数中的任何一个创建一个默认实现。这比我们手动编写函数实现更高效。

显式创建特殊函数默认实现的的语法如下：

```cpp
class farm
{
    farm() = default;
    ...
}
```

这将创建一个默认的 `farm` 类构造函数。`default` 关键字表示该特殊成员函数将使用其默认实现进行创建。

注意：空析构函数会在现代 C++ 编译器中引起优化问题，应该避免。相反，请使用以下类型的声明：`~Foo() = default`，或者最好不要声明析构函数。

### 删除函数与 delete 关键字

`delete` 关键字指示编译器不要创建特殊成员函数。删除特殊成员函数可以防止编译器生成该特殊成员函数的默认实现。

注意：尝试为已默认或删除的特殊成员函数提供实现将引发编译时错误。

删除函数的语法为：

```cpp
Foo(Foo&&) = delete;
```

编译器将其隐式转换为枚举类型，而枚举类型不会被隐式转换为整数类型。因此，以下带有作用域枚举（scoped enum）的程序将无法编译：

```cpp
#include <iostream>
#include <string>
int main()
{
    enum class Color { RED, GREEN, BLUE };
    Color my_color;
    my_color = 1;      // error
    if (my_color == Color::GREEN)
        std::cout << "green color" << std::endl;
}
// output
error: cannot convert 'int' to 'main()::Color' in assignment
```

这种强类型安全也适用于 C++11 中的非作用域枚举。

### 枚举的前向引用

我们可以为作用域枚举和非作用域的枚举指定前向声明：

- # Mood 枚举的前向声明
`enum class Mood;`

### 定义良好的枚举大小：`<cstdint>`

C 和 C++ 通常不为其原生类型提供固定的的、定义良好的位宽。例如，有时我们需要一个 32 位的整数，而不仅仅是一个 `int` 类型。这是因为 `int` 类型在不同的 CPU 架构上可能有不同的尺寸。C++11 通过 C99 头文件 `std.h` 解决了这个问题。我们通过 `#include <cstdint>` 此头文件来指定具有定义大小的整数类型。

`cstdint` 头文件包含了 `std::int_t`、`std::int16_t`、`std::int32_t` 和 `std::int64_t`（以及带有 `u` 前缀的无符号版本）。例如：`std::uint8_t` 指的是 8 位的无符号整数类型。`cstdint` 头文件中的整数类型指定了各种类型的位宽。

我们可以如下使用这些 `cstdint` 类型：

```cpp
#include <cstdint>
enum class Colour : std::int8_t { RED = 1, GREEN = 2, BLUE = 3 };
```

## 现代 C++：类型别名 (C++11)

### Typedef

C 或 C++ 的 `typedef` 声明引入了一个名称，该名称在它的作用域内成为现有类型的别名。语法为：

```cpp
typedef [existing-type] [our-alias];
```

这里有一个示例：

```cpp
// 将 UL 为 unsigned long 类型的别名。
typedef unsigned long UL;
UL x = 5;
```

字体 使用 using 关键字的类型别名声明 (using =)

我们之前已经看到，可以使用 `using` 关键字将命名空间引入作用域中：

```cpp
using namespace std;
```

在 C++11 中，我们还可以利用 `using` 关键字来声明一个名称是之前声明的类型的别名。语法为：

```cpp
using new_type_name = some_declared_type;
```

新类型名称在新类型的作用域内是现有类型的别名。

这里是一些示例：

```cpp
using iter_t = std::vector<int, std::string>::iterator;
using counter = long;
using Map = std::map<std::string, std::string>;
```

`using` 类型别名也适用于函数指针，但它们比等效的 `typedef` 更具可读性：

```cpp
double adder(int x, double y) {
    double z = x + y;
    return z;
}
// 类型 funcptr 的声明
using funcptr = double(*)(int, double);
// 定义
funcptr f = adder;
这等同于：
void (*)(int, double) f = adder;
```

`typedef` 和 `using` 可以用于为类型赋予语义内容：

```cpp
using velocity = long;
```

### Using 和模板

类型别名声明相对于 `typedef` 的优势在于，后者不能与模板配合使用。

以下是模板别名的语法：

```cpp
template<class T> using Vec = std::vector<T>;
```

## 现代 C++：用户字面量 (C++11)

在 C++11 中，字面量有四种类型：整数、浮点、字符和字符串。字面量可以通过指定后缀来定义。例如：

```cpp
#include <iostream>
using namespace std;
int main() {
    long a = 100_;
    float b = 3.05f;
    char c = = ""
0 
;
}
```

```cpp
auto decrementor = [foo = 2] {
  std::cout << "foo value in lambda: " << foo << std::endl;
  return foo - 12;
};
```

```cpp
auto ret = decrementor();
std::cout << "foo value after lambda: " << foo << std::endl;
std::cout << "value returned by lambda = " << ret << std::endl;
```

```cpp
// output
foo before lambda: 30
foo value in lambda: 2
foo value after lambda: 30
value returned by lambda = -10
```

在这个示例中，变量 `foo`是通过拷贝的方式传递给 lambda 的。由于 `foo` 是一个只读变量，它在外部作用域中的值无法被更改。

在接下来的示例中，在 lambda 捕获列表中定义了一个新变量。

```cpp
#include <iostream>
int main() {
    auto decrementor = [foo = 2] { return foo - 12; };
    std::cout << decrementor() << std::endl;
}
```

```cpp
// output
-10
```

`foo` 在 lambda 的外部作用域中并不存在，这实际上是一种为 lambda 添加数据成员的技巧。如果捕获列表中的 lambda 变量在 lambda 的外部作用域中不存在，则必须对其初始化。在捕获列表中声明的新类型 lambda 变量是只读的。

**注意：** lambda 捕获列表中变量的类型没有指定，因为编译器会根据变量是否存在于 lambda 的外部作用域或是否在 lambda 捕获列表中进行了初始化来进行推断。

# 现代 C++：constexpr 模板常量 (C++14)

C++14 允许模板常量为 `constexpr`。这些常量在编译时求值。

```cpp
template<typename T>
constexpr T pi = T(3.14159265358979332385);
```

注意 `T(x)` 正在对其参数执行 C 语言风格的类型转换，将其转换为类型 `T`（参见函数风格的强制转换）。

```cpp
#include <iostream>
template<typename T>
constexpr T pi = T(3.14159265358979332385);
template<typename T>
```



```cpp
constexpr T area_of_circle(T radius)
{
    auto area = pi<T> * radius * radius;
    return area;
}

int main()
{
    auto area = area_of_circle(5.78);
    std::cout << area << std::endl;
}

// output
104.956
```

# 现代 C++：constexpr 函数 (C++14)

C++14 允许在 `constexpr` 函数体内包含更多表达式：

- 在 `constexpr` 函数内部允许进行局部变量声明，只要它们不是 `static` 或 `thread_local` 声明。局部变量必须初始化。
- 在 `constexpr` 函数内部允许 `if`、`switch`、`for`、`while`、`do-while` 表达式。

# 现代 C++：二进制字面量 (C++14)

C++14 允许声明二进制字面量。二进制字面量以 `0B` 或 `0b` 前缀开头，后面跟着一系列 1 和 0：

```cpp
auto y = 0b00000101; // 整数5 的二进制（二进制）字面量
```

二进制字面量具有整型。

# 现代 C++：数字分隔符 (C++14)

C++14 允许使用单引号分隔整数字面量，以提高可读性：

```cpp
12345'67890'1245LL
cout << 12345'67890'1245LL
std::cout << 12345'67890'1245LL
std::cout << 12345'67890'1245LL
```

# 现代 C++：[[deprecated]] 属性 (C++14)

`[[deprecated]]` 关键字用于警告某个表达式、函数或类已过时，但不建议使用。语法如下：

```cpp
[[deprecated]]
```

`[[deprecated]]` 编译器会输出项目过时的警告。可以通过以下方式附加可选的消息：

```cpp
[[deprecated("message")]]
```

示例：

```cpp
// 识别过时的函数
[[deprecated("sqlConnect is obsolete")]]
int sqlConnect() {
```

```cpp
// 识别过时的类
#include <iostream>
using std;
int main() {
class [[ deprecated("Foo is obsolete") ]] Foo {
public:
  Foo() { cout << "in constructor" << endl; }
};
Foo foo;
}
```

```
// 返回
warning: 'Foo' is obsolete
```

# 现代 C++：类型推断 (C++17)

## 函数模板参数推断

模板参数推断是指编译器推导函数模板参数类型的能力。

在函数模板中，参数推断实现如下。考虑以下函数模板声明：

```cpp
template<typename T>
void foo(const T& data)
```

在 C++17 中，可以使用类参数推断（CTAD）来避免指定类的模板参数。

## 类模板参数推断

在 C++17 中，可以使用类参数推断（CTAD）来避免指定类的模板参数。

```cpp
template <typename A, typename B>
struct MyPair
{
  MyPair() {}
  MyPair(const A&, const B&) {}
};

int main()
{
  MyPair p1 {11, 22}; // 推断为 MyPair<int, int>
  // MyPair p2; // 错误：没有匹配的构造函数
}
```

# 现代 C++：非模板类型参数 (C++17)

在 C++11 和 C++14 中，只要我们可以自动推断模板参数或函数返回类型，就可以使用类型 `auto`。`auto` 也可以用于泛型 lambda。

在此之前，非模板参数的类型必须在类模板或函数模板中显式声明，因为编译器不会推断这些参数的类型。

### 非模板类型参数总结

以下是在模板中使用非类型参数的示例：

```cpp
#include <iostream>

// size是非模板类型参数
template<class T, int size>
class Foo
{
  T array[size];
public:
  Foo() {}
  ~Foo() {};
  int getSize() const
  {
    return size;
  }
};

int main(){
  Foo<double, 29> foo;
  auto size = foo.getSize();
  std::cout << size << std::endl;
}

// output
29
```

在本示例中，非模板类型参数的大小是模板声明的一部分。
值 20 在编译时被替换到 `Foo` 类的特化版本中。

非模板类型参数是一种特殊的参数类型，在类模板或函数模板特化时，它会被具体值替换。

C++ 要求非模板类型参数的参数必须是以下类型之一：

- 具有整数类型或为枚举的值
- 指向类对象的指针或引用
- 指向函数的指针或引用
- 指向类成员函数的指针或引用
- `nullptr`

**注意**，我们不能将 `double` 或 `float` 类型作为非模板参数。

### Auto 非模板参数

在 C++17 中，我们可以在模板声明中声明类型为 `auto` 的非模板参数，前提是我们可以在特化中推导出该非模板参数的类型。

```cpp
template <class T auto J>
void func(T t, auto x) { }
func("string", 10); // 推导出 J 为 int
```

在此示例中，`auto` 被推导为 `int` 类型。

## 现代 C++：嵌套命名空间 (C++17)

考虑以下嵌套命名空间：

```cpp
namespace A {
    namespace B {
        namespace C {
            int x = 100;
        }
    }
}
```

在 C++17 中，我们可以这样指定嵌套命名空间 C：

```cpp
namespace A::B::C {
    int x = 100;
}
```

这是一个示例：

```cpp
#include <iostream>
namespace A {
    int a = 1;
}
namespace A::B {
    int b = 2;
}
namespace A::B::C {
    int c = 3;
}

int main() {
    std::cout << A::a << " " << A::B::b << " " << A::B::C::c << std::endl;
}

// 输出
1 2 3
```

# 现代 C++：Constexpr If 语句 (C++17)

假设我们有一个可以在编译时评估的 if 语句，那么 C++ 允许我们根据常量 if 表达式的评估结果，在编译时丢弃该 if 语句的分支。使用如下语法：

```cpp
if constexpr(condition) {
    statement1; // 如果条件为假，则丢弃
} else {
    statement2; // 如果条件为真，则丢弃
}
```

这是一个使用该特性的示例（类型特性）：

```cpp
// std::is_integral<T> 谓词函数在 T 为整数类型时返回 true
// 否则返回 false
#include <iostream>
#include <type_traits>

template <typename T>
constexpr bool IntegralTest()
{
    if constexpr (std::is_integral<T>::value) {
        return true;
    }
    else {
        return false;
    }
}

int main()
{
    static_assert(IntegralTest<int>() == true);
    static_assert(IntegralTest<char>() == true);
    // static_assert(IntegralTest<char*>() == true); // 这会导致失败
}
```

# 现代 C++ Auto 类型的初始化 (C++17)

先参阅：`std::initializer_list`

C++ 中的变量初始化有几种形式：

```cpp
默认初始化          std::string s;
默认大括号初始化    std::string s { };
直接初始化           std::string s("hello");
拷贝赋值初始化      std::string s = "hello";
列表初始化          std::string s = {'h', 'e', 'l', 'l', 'o'};

聚合初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};

引用初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};
char& c = s[1];
```

C++11 引入了使用初始化列表的通用语法，通常被称为大括号列表初始化。大括号列表初始化有两种类型：

- 直接列表初始化：`T object {arg1, arg2, ...}`
- 拷贝列表初始化：`T object = {arg1, arg2, ...}`

在 C++17 下，大括号初始化的 `auto` 变量的类型推导遵循类型推导规则：

- 对于直接列表初始化，如果初始化列表有一个类型为 `T` 的单个元素，编译器将为 `auto` 类型变量推导出类型 `T`。如果初始化列表中有多个元素，则是非合法的。
- 对于拷贝列表初始化，如果列表中的所有元素具有相同类型，编译器将从 `std::initializer_list<T>` 推导出 `auto` 变量的类型，否则 `auto` 类型变量将是非法的。

由于这些规则，上述示例变为：

- `auto b {42};` // OK，推导为 int
- `auto d {1, 2};` // 错误，初始化器过多
- `auto a {42};` // OK，std::initializer_list<int>
- `auto c = {1, 2};` // OK，std::initializer_list<int>
- `auto d = {1, 2, 13};` // 错误，初始化列表类型不同

```cpp
auto b {42}; // OK，推导出 int
auto d {1, 2}; // 错误，初始化器过多
auto a {42}; // OK，std::initializer_list<int>
auto c = {1, 2}; // OK，std::initializer_list<int>
auto d = {1, 2, 13}; // 错误，初始化列表类型不同
```

```cpp
#include <iostream>
int main() {
    auto b {42}; // OK，推导出 int
    auto d {1, 2}; // 错误，初始化器过多
    auto a {42}; // OK，std::initializer_list<int>
    auto c = {1, 2}; // OK，std::initializer_list<int>
    // auto d = {1, 2, 13}; // 错误，初始化列表类型不同
    return 0;
}
```

## 现代 C++：结构绑定 (C++17)

结构绑定允许将对象（如结构体、数组或元组）解构为独立的变量。

```cpp
#include <iostream>
struct Point {
    int x;
    int y;
};

int main() {
    Point p{1, 2};
    auto [x, y] = p;
    std::cout << x << " " << y << std::endl;

    int arr[] = {1, 2};
    auto [a, b] = arr;
    std::cout << a << " " << b << std::endl;

    return 0;
}
```



```cpp
// std::is_integral<T> 谓词函数在 T 为整数类型时返回 true
// 否则返回 false

#include <iostream>
#include <type_traits>

template <typename T>
constexpr bool IntegralTest()
{
    if constexpr (std::is_integral<T>::value) {
        return true;
    }
    else {
        return false;
    }
}

int main()
{
    static_assert(IntegralTest<int>() == true);
    static_assert(IntegralTest<char>() == true);
    // static_assert(IntegralTest<char*>() == true); // 这会导致失败
}
```

# 现代 C++ Auto 类型的初始化 (C++17)

先参阅：`std::initializer_list`

C++ 中的变量初始化有几种形式：

```cpp
默认初始化          std::string s;

默认大括号初始化    std::string s { };

直接初始化           std::string s("hello");

拷贝赋值初始化      std::string s = "hello";

列表初始化          std::string s = {'h', 'e', 'l', 'l', 'o'};

聚合初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};

引用初始化          std::string s[5] = {'h', 'e', 'l', 'l', 'o'};

char& c = s[1];
```

C++11 引入了使用初始化列表的通用语法，通常被称为大括号列表初始化。大括号列表初始化有两种类型：

- 直接列表初始化：`T object {arg1, arg2, ...}`
- 拷贝列表初始化：`T object = {arg1, arg2, ...}`

在 C++17 下，大括号初始化的 `auto` 变量的类型推导遵循类型推导规则：

- 对于直接列表初始化，如果初始化列表有一个类型为 `T` 的单个元素，编译器将为 `auto` 类型变量推导出类型 `T`。如果初始化列表中有多个元素，则是非合法的。
- 对于拷贝列表初始化，如果列表中的所有元素具有相同类型，编译器将从 `std::initializer_list<T>` 推导出 `auto` 变量的类型，否则 `auto` 类型变量将是非法的。

由于这些规则，上述示例变为：

- `auto b {42};` // OK，推导为 `int`
- `auto d {1, 2};` // 错误，初始化器过多
- `auto a {42};` // OK，`std::initializer_list<int>`
- `auto c = {1, 2};` // OK，`std::initializer_list<int>`
- `auto d = {1, 2, 13};` // 错误，初始化列表类型不同

```cpp
auto b {42}; // OK，推导出 int

auto d {1, 2}; // 错误，初始化器过多

auto a {42}; // OK，std::initializer_list<int>

auto c = {1, 2}; // OK，std::initializer_list<int>

auto d = {1, 2, 13}; // 错误，初始化列表类型不同
```

```cpp
int y = 5;

if (auto x = test(y); x != -1)
    std::cout << "x = " << x << std::endl;
else
    std::cout << "x = " << x << std::endl;
```

```cpp
// output
x = 1
```

**注意：** 禁止使用复合初始化：

```cpp
if (int y = -2; auto x = test(y); x + y != -1) {....} // error
```

## 带初始化的 switch 语句

在 `switch` 语句中使用初始化语句允许我们为 `switch` 的作用域初始化一个变量：

```cpp
#include <iostream>

int test(int x)
{
    if (x == 0) return 0;
    else if (x > 1) return 1;
    else if (x <= 1) return -1;
    return 0;
}

int main()
{
    switch(int x = -5; x = test(x))
    {
    case -1:
        std::cout << "switch = " << -1 << std::endl;
        break;
    case 1:
        std::cout << "switch = " << 1 << std::endl;
        break;
    default:
        std::cout << "switch = " << 0 << std::endl;
    }
}
```

```cpp
// output
switch = -1
```

## 现代 C++：内联变量 (C++17)

C++ 的优秀特性之一是它支持纯头文件库。在纯头文件库中，头文件定义和实现都包含在单个头文件中。然而，在 C++17 之前，如果库具有全局变量或对象，则无法创建纯头文件库。这一限制是单定义规则（One Definition Rule）的结果。

根据单定义规则 (`ODR`)，变量或实体只能定义一次。这意味着该变量必须仅在一个编译单元中定义。因此，如果纯头文件库定义了一个全局变量，那么该全局变量将被包含在该头头文件库的所有实现文件 (`.cpp`) 中。换句话说，我们将拥有全局变量的多个定义。这是一个错误。出于相同的原因，类中的静态成员变量可能会有多个定义，除非它也被声明为 `const`。C++17 中的 `inline` 变量属性解决了这个问题，确保了头文件中的全局变量只被定义一次。

从 C++17 开始，我们可以在头文件中定义一个全局变量为 `inline`。然后，如果该头文件被多个编译单元使用，编译器将确保该 `inline` 变量只有一个唯一的定义。`inline` 变量的语法为：

```cpp
inline int x = 0;

class Foo {
public:
    static std::string greet = "hello world";
};

inline class Foo foo;
```

## 使用内联变量

在 C++17 中，`inline` 关键字允许我们在头文件中定义全局变量，即使该头文件可能被包含在多个实现 (`.cpp`) 文件中多次包含该头文件不会创建全局变量的多个定义。

内联变量的任何初始化都将由包含该头文件的第一个编译单元执行。

```cpp
// 某些头文件
class Foo {
public:
    // 从 C++17 起允许
    inline static std::string greet = "hello world";
// 即使包含在多个实现 (.cpp) 文件中也允许
inline Foo foo;
```

## 现代 C++：Lambda 扩展 (C++17)

C++17 扩展了 lambda 的用法如下：

- lambda 可以是 `constexpr` 的
- lambda 可以访问对象的 `this` 指针

## constexpr Lambdas

C++17 允许在编译时上下文中使用 lambda，前提是它可以在编译时求值。

为了指定 lambda 可以在编译时求值，我们使用 `constexpr` 属性对其声明：

```cpp
// 从 C++17 起允许
auto squared = [](auto val) constexpr {
    return val*val;
}
```

`constexpr` lambda 不能有任何静态变量、`try/catch` 块或分配内存。

如果此 `constexpr` lambda 无法在编译时求值，将发生编译器错误。以下示例演示了这一点：

```cpp
#include <iostream>
#include <string>

int main()
{
    int value = 9;
    auto summand = [](int val) constexpr {
        static int multiplier = 2;
        return val*multiplier;
    };
    std::cout << summand(value) << std::endl;
}
```
```text
// output (error)
error: 'multiplier' declared 'static' in 'constexpr' function
```

## 在 Lambda 中访问 this 指针

在 C++17 之前，在成员函数中声明的 lambda 无法访问 `this` 指针。C++17 修正这个问题：

```cpp
#include <iostream>
#include <string>

class Foo
{
    std::string name;
public:
    Foo(const std::string& nm) : name(nm) {}
    void bar(){
        auto print = [this] { std::cout << name << std::endl; };
        print();
    }
};

int main() {
    Foo foo("test");
    foo.bar();
}
```
```text
// output
test
```
在上面的示例中，指向对象的 `this` 指针被捕获到 lambda 中。

## 现代 C++：折表达式 (C++17)

折表达式将二元运算符应用于参数包的所有元素上。因此，我们不需要递归就可以对参数包的元素执行二元操作。

我们可以对折表达式使用所有的二元运算符，`~`、`->` 和 `[]`。

在下面的示例中，`foldSum` 函数接收参数包参数并返回所有参数之和：

```cpp
#include <iostream>
#include <string>

template<class Ttype>
auto sum(Ttype ... args) {
    auto sum = (... + args);
    std::cout << "sum = " << sum << std::endl;
    return sum;
}

int main() {
    sum(1, 5, 11, 18, 9);
}
```
```text
// output
sum = 44
```
`(... args)` 被称为折表达式，它从左开始将 `+` 运算符应用于所有的参数包参数。

折表达式的括号是强制性的。

## 使用折表达式

假设运算符是某个二元运算符，那么：

* 下述语法实现了左折叠（left fold），意味着它从左侧开始处理参数包参数：
`( ... operator args)`
这展开为：`((arg1 operator arg2) operator arg3) operator ..`

* 以下是右折叠（right fold）的语法，意味着它从右侧开始处理参数包参数：
`(args operator ...)`
这展开为：`((argN operator argN-1) operator argN-2) operator ....`

括号是折叠表达式的一部分，并且是必须的。

# 处理空参数包

对于空参数包，适用以下规则：

* 如果使用二元运算符 `&&`，则折叠表达式为 true。
* 如果使用二元运算符 `||`，则折叠表达式为 false。
* 对于所有其他运算符，该调用是非法的（ill-formed）。

## 现代 C++：string_view (C++17)

C++17 标准库实现了一个名为 `std::string_view` 的新字符串类。
该类允许我们与字符序列和字符串进行交互，而无需它们分配内存。`string_view` 对象提供了对其他字符序列或字符串的视图。特别是 `std::string_view` 对象引用一个字符序列或字符串但不拥有它。

与 `std::string` 相比，`std::string_view` 对象具有以下属性：

- 底层的字符序列或字符串是只读的。
- 字符序列不保证以空终止（null terminated）。也就是说，字符序列的 `string_view` 可能没有空终止。
- `string_view` 可以是 `nullptr`。当使用默认构造函数创建 `string_view` 时，`data()` 成员函数返回 `nullptr`。

由于存在 `string_view` 对象没有空终止符，在通过 `[]` 运算符或 `data()` 成员函数访问字符之前，我们必须使用 `size()`。成员函数 `data()` 返回指向底层 `string_view` 数组的指针。

这是一个示例：

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main() {
    std::string str("hello world");
    std::string_view sv(str);
    std::cout << sv << std::endl;
    std::cout << sv[6] << std::endl;
}
```

```
// output
hello world
w
```

修改底层字符串会导致 `string_view` 产生未定义行为（这发生在字符串中的内存被重新分配时）：

```cpp
#include <iostream>
#include <string>
#include <string_view>

int main() {
    std::string str("hello world");
    std::string_view sv(str);
    std::cout << sv << std::endl;
    std::cout << sv[6] << std::endl;
    str = str + " goodbye"; // 分配了内存
    std::cout << str << std::endl;
    std::cout << sv << std::endl;
    std::cout << sv[6] << std::endl;
}
// output
hello world
w
hello world goodbye
rld
```

# string_view 与作用域

`string_view` 的生命周期取决于它所观察的字符串。如果字符串离开了作用域，`std::string_view` 将没有可观察的内容，访问它会导致未定义行为。因此，`string_view` 对象不会延长被观察字符串的生命周期。

考虑以下代码：

```cpp
#include <iostream>
#include <string>
#include <string_view>

std::string_view greet()
{
    std::string str {}
    str = "hello";
    std::string_view view {str};
    return view;
}

int main()
{
    std::string_view view {greet()};
    // view 正在观察一个已经销毁的字符串
    // 未定义行为
    std::cout << "greeting is " << view << '\n';
    return 0;
}
    // output
greeting is
```

## 最佳实践

当函数声明将 `const string` 作为函数参数时，请使用 `string_view`。示例：

不要：
```cpp
int ret = foo(const string mirror) { ... }
```

使用：
```cpp
int ret = foo(string_view mirror) { ... }
```

# 现代 C++：__has_include 预处理器指令 (C++17)

`__has_include` 预处理器指令用于判断包含文件是否可用：

```cpp
#if __has_include(<optional>)
#include <optional>
#else
#include <experimental/optional>
#endif
```

该指令用于判断特定的编译器版本或特定的操作系统是否有可用的包含文件。

# 现代 C++：飞船运算符 (C++20)

飞船运算符 `<=>`（称为三路比较运算符）可用于执行以下类型的比较：a < b, a <= b, a == b, a != b, a > b 和 >= b。飞船运算符的返回类型为 `bool`。

假设我们有如下结构体：
```cpp



`struct MyInt` {

  `int` `value`;

  `MyInt`(`int` `val`) { `value` = `val` };

};

现在假设我们想要比较两个 `MyInt` 对象，我们至少需要为该结构体实现 `operator<` 函数：

```cpp
#include <iostream>
using namespace std;
struct MyInt {
  int value;
  MyInt(int val) { value = val };
  bool operator<(MyInt rhs) { return value < rhs.value; }
};
int main() {
  MyInt myInt1(10), myInt2(0);
  bool ret = myInt1 < myInt2; // myInt1.operator<(myInt2)
  cout << boolalpha << ret << endl;
}
// output
false
```

事实上，我们可能需要编写所有的比较运算符：`MyInt::operator<`, `MyInt::operator<=`, `MyInt::operator==`, `MyInt::operator!=`, `MyInt::operator>` 和 `MyInt::operator>=`。

我们可以通过为类声明一个默认的三路比较（飞船）运算符，请求编译器生成所有六个比较运算符：==, !=, <, <= 和 >=。

在下面的示例中，编译器会自动为 `MyInt` 生成所有的比较运算符：

```cpp
#include <iostream>
#include <compare>
using namespace std;
struct MyInt {
    int value;
    MyInt(int val) { value = val; };
    bool operator<=>(const MyInt& rhs) const = default;
};
int main() {
    MyInt my1(10), my2(0);
    bool ret = my1.value < my2.value;
    cout << boolalpha << ret << endl;
}
// output
false
```

**注意：** `operator<=>` 必须声明为一个带有引用参数的 `const` 函数。

编译器将 `<=>` 视为隐式的 `constexpr` 且 `noexcept` 函数。

`<=>` 执行字典序比较。对于对象，字典序比较如下：

```cpp
#include <iostream>
#include <compare>
using namespace std;
template<typename T>
struct MyObject {
    T value;
    MyObject(T val) : value(val) {}
    bool operator<=(const MyObject& rhs) = default;
};
int main() {
    MyObject<float> object1(10.5), object2(30.4);
    bool ret = object1.value < object2.value;
    cout << boolalpha << ret << endl;
    MyObject<const char*> strobej1("hello"), strobej2("hello");
    ret = strobej1.value < strobej2.value;
    cout << boolalpha << ret << endl;
}
// output
true
false
```

# 现代 C++：`coneval` 和 `constinit` (C++20)

C++20 有两个新关键字：`coneval` 和 `constinit`。声明为 `coneval` 的函数总会在编译时执行。

## `consteval` 函数

`coneval` 函数的语法为：

```cpp
coneval int multiply(int n) {
  return n*n;
}
```

`coneval` 函数的所有依赖项必须在编译时解析为常量。因此，`coneval` 函数也是一种 `constexpr` 函数。`coneval` 函数有时被称为立即函数（immediate functions）。

注意：分配内存或释放内存的函数不能是 `coneval` 函数。

`constexpr` 函数可以在编译时或运行时评估，取决于其参数是否为编译时常量。`coneval` 函数必须在编译时求值。

考虑如下：

```cpp
coneval int multiply(int n) {
  return n*n;
}
int main() {
  multiply(5);
  const int x = 10;
  multiply(x);
int z = 5;
multiply(z)
}
```

`5` 和 `x` 都是编译时常量，因此它们可以在 `coneval` 函数中使用。`z` 不是编译时常量，因此 `multiply(z)` 将无法编译。

## `constinit` 变量

全局变量、静态变量、静态类成员和线程局部变量具有静态存储期。这些对象在程序启动时分配，在程序结束时释放。

具有静态存储持续的变量可以在 (i) 编译时初始化，或 (ii) 在运行时遇到声明时初始化（例如当静态变量位于函数块内部时）。

`constinit` 是一种具有静态存储期、且保证在编译时初始化的变量。`constinit` 属性只能应用于静态存储持续的变量。

`const` 变量不一定是 `constinit` 变量，因为它们不需要在编译时初始化。

## `constexpr` `try-catch` 块

C++20 允许在 `constexpr` 函数中使用 `try-catch` 块。

```cpp
// constexpr 函数中的 try-catch 块在编译时被忽略
```

（注：原文此处示例代码不完整，已根据语境翻译逻辑）

## `std::is_constant_evaluated()`

`is_constant_evaluated()` 是一个类型性性，允许检查 `constexpr` 函数调用是否在编译时发生：

```cpp
#include <iostream>
#include <type_traits>
#include <string>
constexpr char* getEval(int x) {
  if (std::is_constant_evaluated()) {
    return "compile-time evaluated";
  }
  return "run-time evaluated";
}
int main() {
  const int x = 5;
  std::cout << getEval(x);
  int y = 5;
  std::cout << getEval(y);
}
// output
compile-time evaluated
```

# `constexpr` 函数中的 `asm`

C++20 允许在 `constexpr` 函数中出现 `asm` 代码。这允许运行时函数拥有 `asm`：

```cpp
constexpr int add(int a, int b) {
  asm("nop");
  return a + b;
}
```

# 基于范围的循环中的初始化 (C++20)

C++20 允许在基于范围的循环中使用初始化：

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    for (vector<int> vec {1, 2, 3}; auto v : vec) {
        cout << v << " ";
    }
    // output
1 2 3
```

# 带 `auto` 参数的函数 (C++20)

在 C++20 中，`auto` 可用于成员函数或自由函数的参数列表中。函数变为函数模板，`auto` 参数变为模板参数。

# 模板中的非参数类型 (C++20)

在 C++20 之前，模板非参数必须是以下之一：

- 整数
- 枚举值
- 指针或引用
- 空指针

C++ 允许浮点和字面量类型非参数。最重要的字面量类型是字符串字面量。

# 虚 `constexpr` 函数 (C++20)

如果 `constexpr` 函数的所有参数都是编译时常量，则它将在编译时执行。如果某些参数在编译时不存在或不是编译时常量，则它将在运行时执行。

C++20 允许 `constexpr` 成员函数为虚函数。虚非 `constexpr` 函数可以覆盖虚 `constexpr` 函数，而虚 `constexpr` 函数可以覆盖虚非 `constexpr` 函数。

这里有一个简单的示例：

```cpp
#include <iostream>
using namespace std;
struct X1 {
    virtual int f() const = 0;
};
struct X2 : public X1
    constexpr int f() const override { return 2; }
struct X3 : public X2
    int f() const override { return 3; }
struct X4 : public X3
    constexpr int f() const override { return 4; }
int main() {
    X2 x2;
    X3 x3;
    X4 x4;
    cout << "x2: " << x2.f() << " " << "x3: " << x3.f() << " " << "x4: " << x4.f();
}
// output
x2: 2 x3: 3 x4: 4
```

# 现代 C++：概念 (C++20)

编译时多态有两种实现方法。首先，我们可以显式地编写所有需要的重载函数。或者，我们可以定义泛型函数模板和泛型类模板。这两种方法都存在问题。第一种方法既繁琐又出错。第二种方法代价太高，因为我们可能想要禁止某些模板特化。

C++20 引入了概念（Concepts）来解决上述问题。概念是谓词表达式，用于约束类或函数模板的模板参数。这些表达式在编译时进行求值，以确定模板参数是否满足给定的约束。只有符合概念所施加约束的模板特化才是允许的。

**定义（概念）：** 概念是对模板类型的一种命名的编译时约束，例如其支持的操作和语义。

有许多语法结构可用以实现概念；以下语法是指定概念的一种方式：

```cpp
template<typename T, typename X, ...>
concept concept_name = <constraint>
模板声明的剩余部分;
```

概念具有以下优势：

- 对模板参数施加的限制是声明的一部分。这意味着概念是自描述的。
- 我们可以使用预定义的概念，也可以定义自己的概念。
- 如果一个函数声明使用了概念，它会自动变成一个函数模板。

# 指定概念的四种方法

实现概念有四种方法。下面将讨论。

# 使用概念为类型名添加缀

在模板声明中，我们在 `typename` 前面加上一个概念：

```cpp
#include <concepts>
#include <iostream>
template<std::integral T>
T add(T a, T b) {
  return (a + b);
}
```

在这里，对模板参数 `T` 的约束是类型声明本身的一部分。这使得 `add` 函数模板中的概念定义是自文档的。

注意：`std::integral` 是一个预定义的类型特质，仅当 `T` 为整数类型时为真。

# 使用 `requires` 子句实现概念

```cpp
#include <concepts>
#include <iostream>
template<typename T>
requires std::integral<T>
T add(T a, T b) {
  return (a + b);
}
```

这种语法将 `requires` 关键字与预定义的概念结合使用。自定义用户定义概念的语法则有所不同。

# 使用尾随 `requires` 子句实现概念

概念可以在尾随 `requires` 子句中指定：

```cpp
#include <concepts>
#include <iostream>
template<typename T>
T add(T a, T b) requires std::integral<T> {
    return (a + b);
}
```

概念被作为泛型函数的属性指定的。

# 使用缩写函数模板实现概念

```cpp
#include <concepts>
#include <iostream>
auto add(std::integral auto a, std::integral auto b) {
    return (a + b);
}
```

注意声明中缺少了 `template<typename T>` 部分。`add` 自动成为函数模板，因为概念约束附加在 `add` 函数的参数上。

# `requires` 子句

`requires` 关键字引入了一个用于指定模板参数约束的子句。`requires` 后面必须紧跟一个概念名称，然后是一个约束：

```cpp
concept concept_name = <constraint>
```

如果我们使用的是标准库预定义的概念，则可以省略约束。

# 将概念应用于函数的返回类型

实现非常简单，我们在函数模板的返回类型前加上一个概念。例如：

```cpp
#include <concepts>
#include <iostream>
std::integral auto add(std::integral auto a, std::integral auto b) {
    return (a + b);
}
```

# 使用多个概念

多个概念可以使用逻辑与 (`&&`) 和逻辑或 (`||`) 组合：

```cpp
template<typename Iter, typename Val>
requires std::input_iterator<Iter>
&& std::equality_comparable<value_type<Iter>, Val>
Iter find(Iter b, Iter e, Val v)
```

有效的连接操作符有：与 (`&&`)、或 (`||`) 和非 (`!`)。

# 编写自定义概念

自定义概念的语法为：

```cpp
template<typename T, typename X, ...>
concept concept_name = <constraint>
```

约束表达式具有以下语法：

```cpp
requires (optional_parameter_list) { requirements; ...;}
```

`optional_parameter_list` 是一个用逗号分隔的模板参数列表。列表中指定的变量用于指定对参数的编译时约束。它们没有任何生命周期、初始化、存储等。如果不需要变量，可以省略括号。

示例：

```cpp
template<typename T>
concept addable = requires (T a, T b) { a + b; };
```

这个概念要求我们能够对模板参数进行加法。

# 验证模板特化是否可以编译

为了验证类型参数可以按照类或函数模板特化的预期方式使用，我们在可选参数列表中引入变量，并将预期的用法写成一个需求表达式。这正是之前的 `addable` 概念所做的。

一旦我们声明了概念 `addable`，就可以如下所示完成 `add` 函数的模板声明：

```cpp
template<addable T>
T add(T a, T b);
```

注意：需求表达式中的 `a + b` 不会被执行；编译器只验证它是否可以成功编译。

# 将模板参数类型约束为具有特定属性的类型

需求表达式可以验证类型是否具有所需的属性。例如：

```cpp
template <typename T>
concept is_vectorizable = requires { typename std::vector<T>; };
```

这个概念仅允许类型 `T` 为向量类型的特化：

这是一个使用 `vectorizable` 概念的完整函数模板规范：

```cpp
template <typename T>
concept is_vectorizable = requires { typename std::vector<T>; }
std::vector<T> vector_add(is_vectorizable a, is_vectorizable b) { };
```

# 将模板参数约束为求值为真的布尔表达式

可以在 `requires` 子句内部求值布尔表达式。以下语法用于评估逻辑表达式：

```cpp
requires { boolean_expression };
```

例如，考虑一个检查模板参数 `T` 的大小是否等于 4 字节的概念。其语法为：

```cpp
template <typename T>
concept C1 = requires { sizeof(T) == 4 };
```

或者我们写成：

```cpp
template <typename T>
concept C1 = sizeof(T) == 4;
```

如果我们使用的是标准库预定义的概念，则可以省略。

注意以下内容不起作用：



```cpp
template <typename T>
concept C2 = requires { sizeof(T) == 4 };
```

`C2` 并没有执行 `sizeof(T) == 4`。它只是验证它是否可以编译。`C1` 将返回 false。

# 使用概念约束 auto

我们之前已经见过这种用法了。我们通过在 `auto` 前面加上概念名称来约束 `auto`。例如：

```cpp
std::integral auto foo{1};
```

这种语法可以用任何 `auto` 的地方，包括 `lambda` 表达式。

在上面的示例中，`foo` 被初始化为 `1`，默认是有符号 `int`，因此编译器将抛出错误。

# 现代 C++：模块 (C++20)

## 在传统的编译过程中

实现文件通常需要一个或多个头文件才能继续编译。这些头文件包含了实现文件中使用的声明。编译器在预处理实现文件时首先包含头文件。之后，编译器会在实现文件中直接或间接地执行任何宏替换。这是一个翻译单元。该翻译单元随后由编译器编译成对象文件。

- 通过防止重复包含头文件来加快编译速度
- 与预处理器宏实现隔离
- 防止违反单一份定义规则（one definition rule）

模块仅会被导入一次，且导入顺序并不重要。

### 模块文件的结构

模块文件具有以下标准结构：

```cpp
module; // 声明全局模块片段
// 模块所需的头文件
#include <numeric>
#include <vector>

export module math; // 模块声明
// import <other modules>

// 未导出的声明：
// 仅在模块内部可见的名称

// 导出的函数
export int add(int first, int second) {
    return first + second;
}

export int multiply(int first, int second) {
    return first*second;
}
```

以关键字 `module` 开头的全局模块片段是可选的。头文件应该包含在它与模块声明之间。

模块声明 `export module math` 命名了模块。该声明部分有时被称为模块范围（module purview）。导入的模块以及导出的和未导出的名称都可以在模块文件的这一部分指定。

### 导出模块符号的方法

我们已经看到了一种使用导出指定符导出顶层名称（符号）的方法：

```cpp
export module math;
export int add(int hour, int second);
```

导出模块符号的第二种方法是使用导出组（export group）：

```cpp
export module math;
export {
  int add(int first, int second);
  int multiply(int first, int second);
}
```

第三，我们可以导出一个命名空间：

```cpp
export module math;
export namespace math {
  int multiply(int hour, int second);
  void makePolar();
}
```

在最后一种情况下，我们通过在名称前加上命名空间前 (`math::multiply(5, 7)`) 来使用导出的名称。

### 使用导出的模块符号

客户端程序通过导入模块来使用模块导出的功能：

```cpp
#include <iostream>
import math;

int main() {
    std::cout << '\n';
    std::cout << "add(3, 4): " << add(3, 4) << '\n';
    std::cout << "mul(3, 4): " << multiply(3, 4) << '\n';
}
```

### 模块接口单元与模块实现单元

对于大型模块文件，将文件分为模块接口单元和模块实现单元可能是是有益的。这模拟了头文件与实现文件之间的划分。以下示例了如何实现：

```cpp
// mathInterfaceUnit.ixx
module;

#include <vector>

export module math;

// import <exported other declarations>
// 仅在模块内部可见的名称

export namespace math {
    // 仅指定函数声明
    int add(int, int);
    int getProduct(int x, y);
}
```

对应的实现单元是：

```cpp
// mathImplementationUnit.cpp

module math;
#include <numeric>
namespace math {

int add(int hour, int seconds) {
    return hour*3600 + seconds;
}

int multiply(int hour, int seconds) {
    return hour * 3600 * seconds;
}
}
```

一个模块接口单元可以有多个实现单元。

### 子模块

导入另一个模块的模块可以如下所示重新导出该模块：

```cpp
module; // 全局模块片段

// 模块所需的头文件
#include <numeric>
#include <vector>

export module math; // 模块声明

// 导入一个模块然后导出它
export import module trig.module
...
```

在这个示例中，`math` 模块导入了 `trig_module` 并将其功能作为 `math` 模块的一部分重新导出。`trig_module` 被称为 `math` 模块的子模块。

### 模块分区

大型模块可以被分区。每个分区由一个模块接口单元（分区接口文件）和零或多个模块实现单元组成。以下示例了如何实现模块分区：

```cpp
// mathPartition.ixx - 主接口模块
export module math;      // 模块声明
export import :math1;
export import :math2;
```

`math` 模块从 `math1` 和 `math2` 导入符号，并将这些符号作为它们自己的符号重新导出（注意冒号）。

实现文件是：

```cpp
// mathPartition1.ixx
export module math:math1;
export int add(int first, int seconds) {
    return first + seconds;
}
```

语句 `export module math:math1` 将 `math1` 分区的符号导出到 `math` 模块。对于第二个分区，我们有：

```cpp
// mathPartition2.ixx
export module math:math2;
export {
    int multiply(int hour, int seconds) {
        return hour * 3600 + seconds;
    }
}
```

我们如下使用分区：

```cpp
import math;

int main() {
    std::cout << '\n';
    std::cout << "add(3, 4): " << add(3, 4) << '\n';
    std::cout << "multiply(3, 4): " << multiply(3, 4) << '\n';
}
```

### 模块接口单元

关于模板的说明

模块接口单元可以用于模板：

```cpp
// mathTemplate.ixx
export module math;

export namespace math {
    template <typename T>
    T add(T first, T second) {
        return first + second;
    }
}
```

客户端程序如下这样使用模板：

```cpp
#include <iostream>
import math;

int main() {
    std::cout << "add(3, 4): " << math::add(3, 4) << '\n';
}
```

# Modern C++：使用 enum (C++20)

当局部作用域中指定使用 `enum enum_name` 的类型别名时，我们可以不带作用域限定符使用枚举器值。

这是一个示例：

```cpp
#include <iostream>
#include <string_view>
using namespace std;

enum class Color {
    red,
    green,
    blue
};
```

```cpp
string_view toString(Color col) {
    switch (col) {
        using enum Color;
        case red: return "red";
        case green: return "green";
        case blue: return "blue";
    }
    return "unknown";
}

int main() {
    std::cout << "toString(Color::red): " << toString(Color::red) << '\n';

    using enum Color;
    std::cout << "toString(green): " << toString(green) << '\n';

    // 输出
    // toString(Color::red): red
    // toString(green): green
    return 0;
}
```

# Modern C++：转换为 bool (ptr)

指针或成员指针转换为 `bool` 是收窄转换，除非进行了显式的类型转换。例外是在直接初始化时，`nullptr` 可以转换为 `bool`。

# Modern C++：boolalpha

`boolalpha` 关键字可以插入到流中，将 `bool` 值转换为文本表示 `true` 或 `false`，而不是整数值。

```cpp
#include <iostream>

int main() {
    using namespace std;

    cout << boolalpha << "hello " << true << endl;
    cout << boolalpha << (10 < 1) << endl;
}
// 输出
// hello true
// false
```

# Modern C++：[[no_unique_address]]

`[[no_unique_address]]` 属性表示类的数据成员不需要唯一的地址。注意在 `union` 中，数据成员通常共享地址。

该属性应用于空数据成员，以便编译器对其进行优化使其不占用内存。具有 `[[no_unique_address]]` 属性的数据成员可能会共享另一个成员的地址。语法如下：

```cpp
[[no_unique_address]] int x {};
```

这是一个完整的示例：

```cpp
struct Empty {}; // 空结构体
struct X {
    int i;
    Empty e;
};
struct Y {
    int i;
    [[no_unique_address]] Empty e;
};
int main() {
    // 空类对象的大小至少为 1
    static_assert(sizeof(Empty) >= 1);

    // 至少需要一个字节给 e 提供地址
    static_assert(sizeof(X) >= sizeof(int) + 1);

    // 成员被优化掉了
    static_assert(sizeof(Y) == sizeof(int));
    return 0;
}
```

输出：0

# Modern C++：[[likely]] 和 [[unlikely]]

这些属性为编译器提供了关于执行路径更有可能的提示。这允许编译器优化代码。

# Modern C++：协程 (Coroutines)

## 简介

协程是 C++20 中的一项重大语言特性。它们在处理异步事件的应用中非常有用。协程是一个可以挂并在以后某个时刻恢复的函数。这可以多次。

普通函数无法挂并在以后某个时刻恢复。一旦普通函数开始执行，它将继续执行直到遇到返回语句或函数的右括号。

C++ 标准要求协程函数必须使用以下至少之一：

- `co_await` 运算符
- `co_yield` 关键字
- `co_return` 关键字

主要的限制是协程函数不能使用 `return` 语句，而是使用 `co_return` 语句从函数返回。遵守这些限制的函数将被 C++ 编译器自动编译为协程。注意协程不需要有 `co_return` 语句。我们稍讨论额外的限制。

更多信息请参见：https://en.cppreference.com/w/cpp/coroutines

## 为什么使用 co_return 而不是 return?

调用或从协程返回时不使用栈。相反，函数的状态存储在堆上。

当协程不在栈上维护状态时，可以获得大量的简化。考虑多个协程顺序挂起的情况。这些被挂起的协程可以在任何顺序恢复，而不一定按照它们挂起的顺序。由于协程不在栈上传递参数，完全避免了这些协程以任何顺序恢复时维护栈的复杂性。因此，协程可以被无无栈函数（stackless functions）。

## 协程返回对象

协程必须返回一个具有特定定义结构和语义的对象。考虑以下协程可以返回的最简单对象：

```cpp
struct ReturnObject {
    struct promise_type {
        promise_type() = default;
        ReturnObject get_return_object();
        std::suspend_always initial_suspend();
        std::suspend_always final_suspend() noexcept;
        void unhandled_exception();
        void return_void();
    };
};
```

`ReturnObject` 必须返回一个具有特定定义结构和语义。考虑以下协程可以返回的最简单对象：

`std::suspend_always initial_suspend()` 和 `std::suspend_always final_suspend()` 方法用于控制协程的开始和结束。`get_return_object` 方法构造返回给调用者的 `ReturnObject`。如果协程抛出异常，调用 `unhandled_exception` 方法。当协程通过 `co_return` 返回时，调用 `return_void` 方法。

C++ 标准库提供了两个可直接使用的等待对象：

- `std::suspend_always`：指示运行时挂起协程
- `std::suspend_never`：指示运行时不要挂起协程

我们将很快检查 `return_void(void)` 方法。

## 实例化协程

当调用协程时，编译器执行以下序列事件：

1. 使用 *new* 运算符为协程分配内存（此内存称为协程的激活帧）。
2. 将调用函数传递的任何函数参数拷贝到激活帧中。
3. C++ 运行时然后调用 `promise_type` 结构体的构造函数。
4. 在 `promise_type` 对象构造后，运行时调用 `get_return_object` 方法。该方法构造一个 `ReturnObject` 对象。
5. 在执行协程体内的第一行代码之前，会调用 `initial_suspend` 方法。如果 `initial_suspend` 的返回值为 `std::suspend_never`，协程开始执行函数体内的代码。如果返回值为 `std::suspend_always`，协程将进入挂起状态，而不执行协程体内的任何代码。
6. 当协程即将退出时，会执行 `final_suspend` 方法。该函数也返回一个等待对象。

注意，当协程挂起自身或通过 `co_return` 或函数括号退出时，类型为 `ReturnObject` 的对象将返回给调用者。调用函数使用 `ReturnObject` 来恢复挂起的协程、销毁协程或获取其状态信息。

## 从协程返回

`co_return` 语句有两种形式。`co_return` 语句可以返回一个值，也可以返回任意类型的值。在两种情况下，`co_return` 语句的指定如下：

```cpp
co_return;
```

然而，必须定义相应的特殊函数来处理每种 `co_return` 情况。对于 `co_return` 语句不返回值的情况，该特殊函数在 `promise_type` 结构体中声明为：

```cpp
void return_void();
```

函数的体可以是空的，也可以实现一些清理代码。

在下例示例中，我们实现了一个简单地打印 hello world 然后退出的协程：



```cpp
#include <coroutine>
#include <iostream>

struct ReturnObject {
    struct promise_type = default;
    ReturnObject get_return_object() { return {}; };
    std::suspend_never initial_suspend() { return {}; };
    std::suspend_never final_suspend() noexcept { return {}; };
    void unhandled_exception() { };

    void return_void() {}
};
```

```cpp
// 协程 foo 的声明
struct ReturnObject foo() {
    std::cout << "hello world" << std::endl;
    co_return;
}

int main(void) {
    foo();
}

// 输出
hello world
```

# 从协程返回一个值

如果 `co_return` 返回一个值，那么协程除了声明 `return_void()` 之外，还必须在 `ReturnObject` 中声明一个名为 `return_value` 的函数以返回值。

在接下来的示例中，协程在返回时会返回字符串 `"hello, I am returning"`：

```cpp
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return ReturnObject();
        }

        std::suspend_never initial_suspend() {
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            return {};
        }
    };
    void return_void() {}
    void unhandled_exception() { };

    string return_value() const { return "hello, I am returning\n"; };
};

// 协程 foo 的声明
struct ReturnObject foo() {
    co_return;
}

int main(void) {
    ReturnObject ret = foo();
    cout << ret.return_value();
    cout << "exiting main";
}

// 输出
hello, I am returning
exiting main
```

# 挂起协程

协程可以挂起执行。它不能被调用者挂起。当协程自身挂起时，它会将状态保存在堆上并返回一个指向 `ReturnObject` 的句柄（给调用协程的函数）。调用函数可以使用该句柄来恢复或销毁协程。

协程挂起点通过 `co_await` 和 `co_yield` 关键字标识。协程可以有多个挂起点。

`co_await` 运算符接受一个 awaiter 对象作为其唯一参数。例如：

```cpp
co_await std::suspend_always {};
或
co_await std::suspend_never {};
```

在下例示例中，我们的 `foo` 协程挂起了它自己：

```cpp
#include <coroutine>
#include <iostream>

struct ReturnObject {
    struct promise_type = default;
    ReturnObject get_return_object() { return {}; };
    std::suspend_never initial_suspend() { return {}; };
    std::suspend_never final_suspend() noexcept { return {}; };
    void unhandled_exception() { };
    void return_void() {}
};
```

```cpp
// 协程 foo 的声明
struct ReturnObject foo() {
    std::cout << "hello world" << std::endl;

    co_await std::suspend_always {};

    std::cout << "good-bye" << std::endl;
}

int main(void) {
    foo();
}
```

```cpp
// 输出
hello world
```

文本 `good-bye` 没有输出，因为我们已经挂起了协程。

注意 `co_await` 只是一个一元运算符，所以我们可以将其写成：

```cpp
co_await(std::suspend_always {});
```

运算符函数的体可以提供在挂起之前执行的代码。

# 恢复已挂起的协程

调用函数通过 `coroutine_handle` 对象控制协程。

参阅：https://en.cppreference.com/w/cpp/coroutine/handle

`coroutine_handle` 是一个带有如下声明的模板对象：

```cpp
template<typename promise_type = void> struct coroutine_handle;
```

它有两个感兴趣的特化版本。一个基于 `promise_type` 的主特化，以及 `<void>` 特化。后者的特化版本等同于 `template<> struct coroutine_handle`，一个没有参数的模板。

`coroutine_handle` 持有一个指向堆上协程数据的指针，并实现了若干控制协程的函数。编译器可以根据基于主特化的 `coroutine_handle` 隐式转换为 `void` 特化版本。这执行了类型擦除（移除了 `coroutine_handle` 中的 `promise_type`）。

我们现在将分两步展示 `coroutine_handle` 的规范。

首先，`coroutine_handle` 对象必须是 `ReturnObject` 的成员：

```cpp
struct ReturnObject {
    struct promise_type {
        promise_type() = default;
        ReturnObject get_return_object() { return {}; };
        std::suspend_never initial_suspend() { return {}; };
        std::suspend_never final_suspend() noexcept { return {}; };
        void unhandled_exception() { };
        void return_void() { };
    };
    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};
```

这里 `get_return_object` 创建了来自 `promise_type` 对象的句柄。

第二步使用 `coroutine_handle::from_promise` 静态成员函数从 `promise_type` 对象来实例化句柄。`from_promise` 接收 `promise_type` 对象并返回句柄。

因此 `ReturnObject` 的声明如下：

```cpp
struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return coroutine_handle<promise_type>::from_promise(*this);
        }

        std::suspend_never initial_suspend() {
            cout << "ready to execute coroutine" << endl;
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            cout << "exiting coroutine" << endl;
            return {};
        }
    };
    void return_void() {cout << "returning no value to caller" << endl; }
    void unhandled_exception() { };

    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};
```

`ReturnObject` 的构造函数使用了句柄。`coroutine_handle` 提供了 `resume()` 方法来恢复协程。`done()` 方法是一个检查协程是否完成的谓词函数。如果协程处于挂起状态，则返回 true，否则返回 false。

在接下来的示例中，协程挂起了它两次，调用函数恢复了协程两次：

```cpp
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
    struct promise_type {
        promise_type() = default;

        ReturnObject get_return_object() {
            return coroutine_handle<promise_type>::from_promise(*this);
        }

        std::suspend_never initial_suspend() {
            cout << "ready to execute coroutine" << endl;
            return {};
        }

        std::suspend_never final_suspend() noexcept {
            cout << "exiting coroutine" << endl;
            return {};
        }
    };
    void return_void() {cout << "returning no value to caller" << endl; }
    void unhandled_exception() { };

    coroutine_handle<promise_type> handle;
    ReturnObject(coroutine_handle<promise_type> _handle) : handle(_handle) {}
};

// 协程 foo 的声明
struct ReturnObject foo() {
    cout << "coroutine is executing\n";
    co_await std::suspend_always {};
    cout << "coroutine has resumed\n";
    co_await std::suspend_always {};
    cout << "coroutine has resumed\n";
    co_return;
}

int main(void) {
    ReturnObject ret = foo();

    if (ret.handle.done() == false) {
        cout << "resuming coroutine\n";
        ret.handle.resume();
    }

    if (ret.handle.done() == false) {
        cout << "resuming coroutine again\n";
        ret.handle.resume();
    }

    if (ret.handle.done()) {
        cout << "coroutine has finished";
    }
}
```

```
coroutine is executing
resuming coroutine
coroutine has resumed
resuming coroutine again
coroutine has resumed
returning no value to caller
exiting coroutine
coroutine has finished
```

**注意：** 与其使用 `ret.handle.resume()` 恢复，我们可以使用 `ret.handle()`。

# 从挂起的协程中传递中间值

协程可以在挂起自身时，向调用函数传递一个中间值。这种操作可以多次执行。`co_yield` 关键字用于传递中间值。`co_yield` 的语法如下：

```cpp
co_yield val;
```

其中 `val` 是某个对象或标量值。为了使用 `co_yield`，`promise_type` 对象以及 `ReturnObject` 必须进行如下修改：

```cpp
struct promise_type {
    promise_type() = default;

    T val_;
    std::suspend_always yield_value(T val) {
        this->_val = val;
        return std::suspend_always{};
    }

    ReturnObject get_return_object() {
        return ReturnObject
        (std::coroutine_handle<promise_type>::from_promise(*this));
    }

    std::suspend_never initial_suspend() {
        return {};
    }

    std::suspend_never final_suspend() noexcept {
        return {};
    }
};
void return_void() {}
void unhandled_exception() { };

std::coroutine_handle<promise_type> handle;
ReturnObject(std::coroutine_handle<promise_type> handle) : handle {
  _handle
}
T get_value() const { return handle.promise().val_; };
```

`promise_type` 结构体必须有一个名为 `yield_value` 的方法，其参数 `T` 的类型为返回给调用函数的类型。当协程执行 `co_yield` 语句时，会调用 `yield_value` 函数。`yield_value` 返回一个等待器 `std::suspend_always` 对象，它会挂起协程，然后允许调用函数获取中间值。

为了让调用函数能够获取中间值，`ReturnObject` 定义了一个实用方法 `get_value`，它返回 `promise_type` 数据成员 `val_`。`handle.promise()` 获取 promise 类型对象。

在下面的示例中，我们获取了前 12 个自然数的平方：



```cpp
#include <coroutine>
#include <iostream>

using namespace std;

struct ReturnObject {
  struct promise_type {
    promise_type() = default;
    int val_;

    std::suspend_always yield_value(int val) {
        this->val_ = val;
        return std::suspend_always();
    }

    ReturnObject get_return_object() {
        return ReturnObject(
            std::coroutine_handle<promise_type>::from_promise(*this));
    }

    std::suspend_never initial_suspend() {
        return {};
    }

    std::suspend_never final_suspend() noexcept {
        return {};
    }

    void return_void() {}
    void unhandled_exception() { };

    std::coroutine_handle<promise_type> handle;

    ReturnObject(std::coroutine_handle<promise_type> _handle) : handle
    {
        _handle
    }

    int get_value() const { return handle.promise().val_; };
  };
};

// 声明协程 square
ReturnObject square() {
    int square;
    for (int i = 0; i < 12; ++i) {
        square = 1*i;
        co_yield square;
    }
    co_return;
}

int main(void) {
    ReturnObject ret = square();
    while (!ret.handle.done()) {
        cout << ret.get_value() << " ";
        ret.handle.resume();
    }
}
// 输出
0 1 4 9 16 25 36 49 64 81 100 121
```

# 销毁协程

可以使用 `destroy` 方法销毁协程。在之前的 `square` 示例上下文中，销毁协程的语法为：

```cpp
if (!ret.handle.done()) {
    ret.handle.destroy();
}
```

# 协程限制

以下类型的函数不能是协程：

- 使用 `auto` 类型的函数

- 带有变长参数的函数

- 带有 `constexpr` 的函数

- 带有构造函数的函数

# 现代 C++：`#pragma once`

许多编译器支持 `#pragma once`，但它并不是 ISO 标准的一部分。使用 `#pragma once` 有助于防止头文件的多次包含。它比头文件保护（header guard）写法更简单，且不容易发生命名冲突。

# 高效头文件管理

我们如何有效地管理头文件以加快构建速度？第一规则是实现文件应该只包含它实际需要的头文件。第二规则是尽可能使用前置声明而不是包含头文件。

# 前置声明

当实现文件仅使用标识符的指针，且不需要知道标识符的大小或其内容时，对标识符进行前置声明就了。例如，在 C++ 中，我们可以使用前置声明：

```cpp
// elephant.h

// 需要 trunk.h，因为 Elephant 对象包含 Trunk 对象
#include "trunk.h"

class Elephant {
    public:
        // 构造函数
        Elephant(const Trunk& trunk);

    private:
        // Trunk 对象
        Trunk m_trunk;
};
```

这种实现方式的问题是，每当 `trunk.h` 变化时，包含 `elephant.h` 的每个源文件都必须重新编译。我们可以通过在 `elephant.h` 中包含 `trunk` 类的前置引用来移除这种依赖。

```cpp
// elephant.h
// 不需要 trunk.h，因为编译器
// 已经知道指针的所有信息。

class Trunk; // Trunk声明

class Elephant {
    public:
        // 我们使用的是引用（隐式指针），所以
        // 编译器不需要知道 Trunk 类的细节
        Elephant(const Trunk& trunk);

    private:
        // 指向 Trunk 对象的指针，因此不需要
        // trunk 类的具体信息
        Trunk* ptr_trunk;
};
```

这之所以有效，是因为对于编译器来说，指针或引用的尺寸总是相同的，并且始终可以对它们执行相同的操作，无论它们指向或引用的标识符是什么。

在我们的示例中，`elephant` 类包含一个指向 `Trunk` 类的成员 `ptr_trunk`。此时，编译器需要知道的唯一事实是 `ptr_trunk` 是一个指针，并且标识符名称 `Trunk` 存在于其他地方。同样，编译器关于引用 `&trunk` 所需要知道的只有它是一个引用（对...的隐式指针）。

现在对 `trunk.h` 文件所做的更改不会影响 `elephant.h`。

因此，为了防止触发实现文件的冗长重新编译，我们应该优先使用前向声明。

## 头文件保护 (Include Guards)

全局变量只能定义一次。由于由于原因，在一个编译单元中多次包含同一个头文件，当全局变量被定义多次时，将产生编译器错误。

防止多次包含包含的常用方法是使用头文件保护，这种方法是将整个头文件封装在一个 `#ifndef` 区域中，该部分会检查一个特定于头文件的宏是否存在。如果该宏在编译单元中未定义，则该头文件被包含在编译单元中。如果该宏已经在编译单元中定义过，则不会被包含。这确保了头文件在一个编译单元中仅被包含一次。

以下是在头文件中使用头文件保护的示例：

```
// store.h
#ifndef __STORAGE_HEADER__
```

```cpp
#define __STORAGE_HEADER__
各种声明等

#endif // __STORAGE_HEADER__

// store.cpp
#include "store.h"
#include "store.h" // OK，store.h 仅被包含一次
...
```

## pragma once 指令

`pragma once` 指令之前已经讨论过。许多编译器支持 `pragma once` 指令，它可以放置在包含文件的顶部，而不是使用头文件保护：

```
#pragma once
```

## `__has_include` 预处理器指令

C++17 添加了 `__has_include` 预处理器指令。这让我们能够测试包含包含的文件是否存在。如果找到了头文件，预处理器将求值为真：

```cpp
#if __has_include("store.h")
#include "store.h"
#endif
```

## C++ 标准库：`std::any`

`std::any` 实现了一个类型安全的变量，可以动态地持有任何类型的值。

换句话说，`std::any` 变量是动态类型的。其模板声明为：

```
template<class T> class any<T>;
```

这里是一个定义 `std::any` 变量的示例：

```cpp
#include <any>

int main()
{
    std::any<int> tmp {5}
    // 或者
    std::any tmp {5}; // 推断类型为 int
}
```

这将创建一个整数类型、值为 5 的 `std::any` 变量 `tmp`。

我们也可以通过赋值来初始化 `any` 变量：

```cpp
#include <any>
using namespace std;

int main()
{
    any var = 2.1174; // 推断类型为 double
}
```

我们可以为 `any` 变量动态地分配不同类型的值：

```cpp
std::any<float> tmp = 3.14;
tmp = "hello world";
```

实用的 `std::any` 成员函数包括：

- `reset`: 销毁 `any` 变量包含的值

- `has_value`: 检查 `std::any` 变量是否包含一个值

- `type`: 返回 `any` 变量的 `typeid` 对象

函数 `std::any_cast` 接收 `any` 变量的地址并返回指向所包含值的指针。例如：

```cpp
int* ptr = std::any_cast<int>(&a); // a 是一个 any 类型变量
```

下面的 `any_cast` 将抛出异常，因为我们正尝试将 `int` 类型的 `any` 变量转换为 `double` 类型：

```cpp
double* ptr = std::any_cast<double>(&a); // a 是 int 类型
```

这里是一个用法示例：

```cpp
#include <iostream>
#include <any>
using namespace std;

int main() {
    cout << "placing 3.12 in an any container" << endl;
    any icontainer(3.12);
    if (icontainer.has_value())
        cout << "container has value" << endl;
    else {
        cout << "icontainer does not have a value" << endl;
        return -1;
    }

    cout << "contained type = " << icontainer.type().name() << endl;
    double* p = any_cast<double>(&icontainer);
    cout << "contained value = " << *p << endl;
}

// 输出
placing 3.12 in an any container
container has value
contained type = d
contained value = 3.12
```

## C++ 标准库：`std::async`, `std::future`

注意：`std::async` 需要具备 `std::thread` 的知识。建议复习 `std::ref`。

考虑我们想要从子线程向父线程传递一个值的情况。可以使用一个由互斥锁保护的共享变量以及一个条件变量来实现，条件变量会在子线程改变变量时发送通知。`std::async` 函数提供了一种更简单的实现。

以下程序展示了 `std::async` 函数的规范用法：

```cpp
#include <iostream>
#include <future>
// 计算数字的阶乘
size_t factorial(size_t num)
{
    size_t result = 1;
    for (size_t ctr = num; ctr > 0; ctr--)
        result *= ctr;
    return result;
}

int main() {
    std::future<size_t> f = std::async(std::launch::async, factorial, 20);
    size_t fac = f.get();
    std::cout << fac << std::endl;
}
// 输出
243290200817664000
```

（注：由于原文代码块中存在错乱，翻译时已保持代码逻辑结构并根据上下文进行了对齐）

## `std::async` 启动类型

`std::async` 支持不同的启动类型：

- `std::launch::async`: 在新线程中启动目标函数。

- `std::launch::deferred`: 在遇到 `f.get()` 时延迟执行目标函数。它在父线程中执行函数。

- `std::launch::async | std::launch::deferred`: 根据编译器的实现，目标函数可能在主线程或新线程中执行。第一个参数的默认值为 `std::async`。

## `std::promise`

`std::promise` 让父线程能够在未来向子线程发送一个值。

子线程在处理过程中可能会暂停，等待父线程向其发送一个值。

以下规范示例展示了如何实现 promise。父线程创建一个子线程，并在未来向阶乘函数发送值。子线程开始处理并等待父线程发送值。当子线程从父线程获取值时，它恢复处理。最后，阶乘函数将其返回值发送父线程：

```cpp
#include <iostream>
#include <future>

int factorial(std::future<int>& fu) 
{
    int start = fu.get();
    int result = 1;

    for (int ctr = start; ctr > 0; ctr--)
        result *= ctr;

    return result;
}

int main()
{
    std::promise<int> p;
    std::future<int> fu = p.get_future();

    // std::ref 存在是因为 future 对象不能
    // 拷贝或赋值
    std::future<int> f = std::async(std::launch::async, 
        factorial, std::ref(fu));

    std::this_thread::sleep_for(std::chrono::seconds(10));
    p.set_value(10);

    size_t fac = f.get();
    std::cout << fac << std::endl;

}
```

语句 `std::promise<int> p` 创建了一个类型为 `int` 的 promise 对象。这是一个

...

承诺在未来发送一个 `int` 类型的值。

表达式 `p.get_future()` 返回一个 `int` 类型的 `future` 对象，该对象将用于发送承诺的值。

我们将 `std::ref<fu>` 作为参数传递给子函数，因为 `future` 对象不能通过值传递（拷贝）。

`p.set_value()` 将承诺的值发送给子函数。

子函数拥有一个 `std::future<int>` 引用作为参数。在函数体中，`fu.get()` 会导致子函数等待直到接收到承诺的值。

请注意 `[f.get()]` 只能被调用一次。

# `std::shared_future`

考虑这种情况：我们想在十个线程中执行阶乘函数，并且每个线程都通过 `promise` 接收相同的值。由于 `future` 对象不能被拷贝，我们必须为每个线程创建一个不同的 `future` 对象，并将该未来对象作为引用传递给阶乘实例。然而，使用 `std::shared_future` 对象有此更简单的解决方案。

以下程序展示了如何使用共享未来（shared futures）：

```cpp
#include <iostream>
#include <future>

int factorial(std::shared_future<int> fu) {
    int start = fu.get();
    int res = 1;

for (int ctr = start; ctr > 0; ctr--)
res *= ctr;
    return res;
}
int main() {
    std::promise<int> p;
    std::future<int> fu = p.get_future();
    std::shared_future<int> sfu = fu.share();

    std::future<int> f1 = std::async(std::launch::async, factorial, sfu);
    std::future<int> f2 = std::async(std::launch::async, factorial, sfu);

    std::this_thread::sleep_for(std::chrono::milliseconds(100));
    p.set_value(10);

    size_t fac1 = f1.get();
    std::cout << fac1 << std::endl;

    size_t fac2 = f2.get();
    std::cout << fac2 << std::endl;
}
```

Output:

3628800

3628800



一旦 `promise` 返回了一个将将向子函数发送值的 `future`，函数 `fu.share()` 就会将该对象转换为 `std::shared_future` 对象。

共享未来对象作为参数传递给子函数。由于共享对象可以进行拷贝构造和拷贝赋值，因此我们不需要传递指向子对象的引用。

语句 `p.set_value(10)` 通过共享 `future` 对象将相同的值 10 发送给所有子函数。

# C++ 标准库: std::atomic

`std::atomic` 类模板的声明如下：

```cpp
template <class T> struct atomic { }
```

类型为 `std::atomic<class T>` 的对象会以原子方式更改标量变量的值。也就是说，该类型的变量保证在产生任何数据竞态的情况下提供读取和写入访问。原子变量可以在不需要互斥锁（`mutex`）的情况下进行更改。整数原子类型变量可以定义如下：

```cpp
atomic<int> x;
```

`atomic` 类模板支持的类型如：`bool`, `char`, `int`, `long`, `unsigned int`, `unsigned long`, `short`, `unsigned short`, `wchar_t`, `unsigned long long` 等。

原子变量不能被拷贝或移动。

语句 `atomic<int> x;` 将创建一个类型为 `int` 的未初始化原子变量 `x`。

原子模板类的一些方法是：`store`, `load`, `exchange`, `operator++` 和 `operator--`。

以下是一个用法示例：

```cpp
#include <iostream>
#include <atomic>
int main()
{
    std::atomic<int> val(5);
    std::cout << "value of atomic variable val with constructor 5: ";
    std::cout << val << std::endl;
    int x = 3400;
    std::cout << "value of variable x: " << x << std::endl;
    x = val.load();
    std::cout << "value of x after x = val.load(): ";
    std::cout << x << std::endl;
    val++;
    std::cout << "value of atomic variable after val++: ";
    std::cout << val << std::endl;
    val.store(99);
    std::cout << "value of atomic variable after val.store(99): ";
    std::cout << val << std::endl;
    --val;
    std::cout << "value of atomic variable after --val: ";
    std::cout << val << std::endl;
} // output
value of atomic variable val with constructor 5: 5
value of variable x: 3490
value of x after x = val.load(): 5
value of atomic variable after val++: 6
value of atomic variable after val.store(99): 99
value of atomic variable after --val: 98
```

## 原子类型别名

`std::atomic<bool>` `std::atomic_bool`

`std::atomic<int>` `std::atomic_int`

其他类型别名也类似。

# C++ 标准库: std::bind

注意：另请参见 `std::function`。`std::bind` 的声明如下：

```cpp
template <class F, class... Args>
```

`std::bind` 是一个函数适配器。它创建一个可调用对象，该对象使用给定参数调用函数。

以下是一个示例：

```cpp
#include <iostream>
#include <functional>
int adder(int x, int y)
{
    return x + y;
}
int main()
{
    auto f = std::bind(adder, std::placeholders::_1, std::placeholders::_2);
    std::cout << f(10, 20) << std::endl;
    auto f2 = std::bind(adder, 10, std::placeholders::_1);
    std::cout << f2(20) << std::endl;
}
```
Output:
30
30
```

```cpp
#include <iostream>
#include <ratio>
int main()
{
    std::ratio<3,7> rl;
    std::cout << rl.num << " " << rl.den << std::endl;
    typedef std::ratio<4, 8> r2;
    std::cout << r2::num << " " << r2::den << std::endl;
}
// 输出
3 : 7
1 : 2
```

注意在声明中：`ratio<4, 8>`，`r2::num` 和 `r2::den` 被约简为最大公分数。

# 时长 (Durations)

`std::chrono::duration` 是一个表示时间间隔的类模板。它的声明如下：

```cpp
#include <chrono>
template<class Type, class Period = std::ratio<1>>
class duration;
```

该类模板有两个参数。`Type` 是一个算术类型，如 `int`、`long`、`double`、`float` 等。它表示以刻（ticks）计的时间（自时钟起点以来的刻数）。`Period` 是一个 `std::ratio` 参数。它表示每秒的刻数，或者如果大于秒，则表示从一个刻到下一个刻的秒。`Period` 是编译时的有理常量。

`Period<1,500>` 意味着每秒有五千个刻。`Period<1000,1>`（或 `Period<1000>`）意味着每 1000 秒有一个刻。

默认周期是 `Period<1>`（每秒一个刻）。

假设我们每秒有 5000 个刻，那么20 秒的时长可以定义如下：

```cpp
#include <iostream>
#include <chrono>
#include <ratio>
using namespace std;
int main() {
    // 100000 是以刻计的时长
    chrono::duration<int,5000> dur{100000};
    cout << (double) dur.count()/5000;
}
```

`duration` 对象的构造函数接受一个以刻计的值。

`duration` 对象有一个成员函数 `count()`。`count` 返回一个 `Type` 类型的常量。该数值是对象以刻计的时长，或自时钟起点以来的刻数。假设我们的 `count` 函数返回 1000。这是以刻表示的时长。该值根据 `duration` 的周期进行解释。假设周期是 `ratio<1,1000>`。这意味着每秒有一千个刻。因此，`count` 被解释为返回一秒的时长。如果周期是 `ratio<1,10>`，则每秒有 10 个刻。因此 `count` 被解释为返回 10 秒的时长。

总结来说，`duration` 类包含编译时的刻周期，它是一个 `std::ratio` 类型。刻周期指定了每秒的刻数。默认周期是 `ratio<1,1>`，每秒一刻（表示为 `ratio<1>`）。如 `ratio<1,1000>` 这样的周期意味着每秒有一千个刻，因此一刻是毫秒。`ratio<1,1000000>` 周期意味着每秒有一百万个刻，因此一刻是微秒。`ratio<3600,1>`（或 `ratio<3600>`）意味着每 3600 秒有一个刻。

标准库定义了一些常见的时长类型：

```
typedef std::chrono::duration<signed int, ratio<1,1000000000>> std::chrono::nanoseconds;
typedef std::chrono::duration<signed int, ratio<1,100000>> std::chrono::microseconds;
typedef std::chrono::duration<signed int, ratio<1,1000>> std::chrono::milliseconds;
typedef std::chrono::duration<signed int, ratio<1,1>> std::chrono::seconds;
typedef std::chrono::duration<signed int, ratio<60,1>> std::chrono::minutes;
typedef std::chrono::duration<signed int, ratio<3600,1>> std::chrono::hours;
```

使用这些预定义类型的 `<iostream>` 示例如下：

```
#include <iostream>
#include <chrono>
int main()
{
    // 定义一个时长为 1 秒的 duration 对象
    std::chrono::seconds sec(1);
    // 创建一个接收一秒时长对象的微秒对象
    std::chrono::microseconds ms(sec);
    std::cout << ms.count() << std::endl;
    // 输出
    1'000'000
}
```

`duration` 类重载了 `+`、`-`、`*`、`%`、`==`、`<=`、`>`、`>=`、`!=`、`>` 运算符。这些运算符允许对不同周期的 duration 对象进行算术运算和比较。对于算术运算符，两个 duration 操作数都会转换为它们的最大公周期。

另一个 duration 示例：

```cpp
#include <iostream>
#include <chrono>
#include <ratio>
int main()
{
    std::chrono::duration<long, std::ratio<1>> dr1(100);
    std::cout << "duration = " << dr1.count() << std::endl;
    std::chrono::duration<long, std::ratio<60, 1>> dr2(50);
    std::cout << "duration = " << dr2.count() << std::endl;
    std::chrono::duration<double, std::ratio<1, 2>> dr3(100);
    std::cout << "duration = " << dr3.count() << std::endl;
    // 相加两个 duration 对象
    auto dr4 = dr1 + dr2;
    std::cout << "duration = " << dr4.count() << std::endl;
    // 减去 duration 对象
    auto dr5 = dr2 - dr1;
    std::cout << "duration = " << dr5.count() << std::endl;
    return 0;
    // 输出
    duration = 100
    duration = 50
    duration = 100
    duration = 3100
    duration = 2900
```

函数模板 `std::duration_cast` 将 duration 对象转换为具有不同周期的 duration 对象。由于编译器会隐式地将 duration 对象的周期转换为公共周期，因此只有在发生精度损失时才需要此函数。函数模板 `std::duration_cast` 如下：

```
template <class ToDuration, class Rep, class Period>
ToDuration duration_cast(const duration<Rep, Period>& d);
```

函数模板 `duration_cast` 将 duration 对象转换为具有不同周期的 duration 对象。由于编译器会隐式地将 duration 对象的周期转换为公共周期，因此只有在发生精度损失时才需要此函数。

使用 duration_cast 的示例：

```
#include <iostream>
#include <chrono>
int main() {
    // 定义一个 144 分钟的对象
    std::chrono::minutes mins(144);
    // 转换为小时对象
    std::chrono::hours hrs = std::chrono::duration_cast<std::chrono::hours>(mins);
    std::cout << hrs.count() << std::endl;
}
```

# 时间点 (Time Points)

`time_point` 表示自时钟起点（epoch）以来的时间点。

```cpp
#include <chrono>
template <
    class Clock,
    class Duration
>
class time_point;
```

`Clock` 是一个如 `system_clock`、`steady_clock` 或其他类。第二个模板参数是 duration 类型。

`time_point` 的一些成员函数有：

- `time_since_epoch` 自起点开始时长（刻数）
- `operator++`、`operator--` 增加或减少时钟时长
- `operator+=`、`operator-=` 通过给定时长修改时间点
- `operator+`、`operator-` 相加或减去时长

`time_point` 对象可以比较：`operator==`、`operator!=`、`operator>`、`operator <` 和 `operator <=`

`time_point_cast` 将时间点转换为同一时钟上不同时长的时间点。

使用 `time_point` 的示例：

```cpp
#include <iostream>
#include <chrono>
int main() {
    // 获取当前系统时间
    std::chrono::system_clock::time_point now = std::chrono::system_clock::now();
    // 转换为 time_t
    std::time_t t = std::chrono::system_clock::to_time_t(now);
    // 打印
    std::cout << "now is: " << std::ctime(&t);
}
```

# 让当前线程休眠

注意：查看 `std::thread`

```cpp
#include <thread>
#include <chrono>
std::this_thread::sleep_for(std::chrono::seconds(15));
```

# 自 Unix 纪元以来的秒数

```cpp
#include <stdio.h>
#include <time.h>
long seconds = time(NULL);
printf("自 1970 年 1 月 1 日以来的秒数 = %ld\n", seconds);
```

我们也可以使用 `std::chrono`：

```cpp
#include <chrono>
#include <ratio>
size_t time_now = duration_cast<seconds>(std::system_clock::now().time_since_epoch()).count();
```

# C++ 标准库：std::copy

函数模板 `std::copy` 将一个容器拷贝到另一个相同类型的容器中。`std::copy` 的声明如下：

```cpp
template <class InputIterator, class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first, InputIterator last, OutputIterator res);
```

`copy` 函数接收指向第一个容器起始位置的迭代器以及指向第一个容器末尾的迭代器。该函数将第一个容器从第一个迭代器值到（包含）最后一个迭代器值的所有值拷贝到从 `res` 迭代器开始的第二个容器中。该函数返回指向第二个容器的迭代器，该迭代器位于最后一个拷贝项之后的位置：



```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec1 = {0,1,2,3,4,5,6,7,8,9};
    std::vector<int> vec2(10);
    std::cout << "vec1 size = " << vec1.size() << std::endl;

    std::copy(vec1.begin(), vec1.end(), vec2.begin());

    std::cout << "vec2 size = " << vec2.size() << std::endl;

    for (auto item : vec2) {
        std::cout << item << " ";
    }
    // 输出
    vec1 size: 10
    vec2 size = 10
    0 1 2 3 4 5 6 7 8 9
```

**重要说明：** 如果需要，`std::copy` 不会自动为目标 `vector` 分配内存。

# C++ 标准库：std::format

`std::format` 是一个变变函数模板，实现了一个基于 `printf` 的现代格式化功能。`std::format` 还实现了方便的字符串插值。它的声明如下：

```cpp
template<class... Args>
std::string format("fmt", Args&... args);
```

函数参数是一个由文本和占位符组成的字符串。随后是数量数量的函数参数。`format` 函数返回一个字符串。

除了任何占位符外，`fmt` 参数中的文本将原封不动地拷贝到输出字符串中。`fmt` 中的占位符由大括号 `{}` 指定。这些指定的大括号被与大括号位置对应的函数参数所替换。例如：

```cpp
#include <iostream>
#include <string>
#include <format>
```

```cpp
int main() {
    std::string str = std::format("this is an example of {} and {}", "dogs", "cats");
    std::cout << str;
}
```

```cpp
#输出
"this is an example of dogs and cats"
```

占位符可以包含一个整数索引，该索引指定位置处的参数被用于替换。例如：

```cpp
std::string str = std::format(" {2} and {1}", "dogs", "cats");
产生输出：
```

“cats and dogs”

格式函数中的参数可以多于占位符。

在占位符内部可以使用格式指定符。这会格式化替换到占位符中的值。例如：

```cpp
std::format("{1:.2f}", 2.71423)
# 输出
2.71
```

注意格式指定符通过冒号与索引隔开。格式指定符的语法和语义与 `printf` 格式指定符相同。

**注意：** `std::format` 是在 C++20 中引入的，需要 GCC 12.2 或更高版本。

# C++ 标准库：std::function

类模板 `std::function` 是一个多态函数包装器。如果我们有一个自由函数、lambda 表达式、函数指针、成员函数或数据成员，可以使用 `std::function` 将其封装成一个可调用类（仿函数）。该仿函数拥有拷贝构造函数并且是可以赋值的。此外，此仿函数可以存储并作为参数传递给其他函数。

声明如下：

```cpp
#include <functional>
template <class R, class... Args>
std::function<R(Args...)>
```

`R` 是函数返回值的数据类型。`Args` 是函数参数类型的逗号分隔列表。

**注意：** 如下所示为自由函数构造函数对象：

```cpp
#include <iostream>
#include <functional>

// 我们将创建一个函数对象
double adder(int x, double y) {
    double z = x + y;
    std::cout << "inside adder" << std::endl;
    return z;
}

int main() {
    // 声明仿函数并初始化它
    std::function<double(int, double)> fun = adder;

    // 调用 fun 对象中的可调用目标
    auto result = fun(3, 5);
    std::cout << result << std::endl;
}
```

项目 `{4, 1, 11}` 被称为括号初始化列表（braced init list）。

初始化列表具有以下公共成员：

- `begin()` 指向第一个初始化列表项的指针
- `end()` 指向最后一个初始化列表项的指针
- `size()` 初始化列表的大小

一个类允许使用括号初始化列表来实例化对象，前提是该类有一个接收初始化列表作为参数的构造函数。考虑这段代码段：

```cpp
Foo foo = {1, 2, 6, 11};
```

当编译器遇到此语句时，它会从右侧的括号初始化列表创建一个初始化列表（右值）。现在 `foo` 可以用这个初始化列表进行初始化，前提是它有一个接收初始化列表作为参数的构造函数。

## C++ 标准库: std::map

### 插入键值对

```
iterator map_name.insert( { key, element } )
```

需要括号是因为正在插入的是一个对（pair）对象。

### 删除键值对

```
void map_name.erase(iterator i);
```

这将删除由迭代器指向的键值对。

### 测试 Map 是否包含某个键

```cpp
if (myMap.find("foo") == myMap.end()) {
    // 未找到
} else {
    // 找到
}
```

### 测试 Map 是否包含某个值

从 C++20 开始，关联容器拥有 `contains` 成员函数来检查 map 是否包含某个键或 set 是否包含某个元素：

```cpp
std::map<int, char> map {{1, 'a'}, {2, 'b'}};
map.contains(2);                // true
map.contains(123);             // false
```

```cpp
std::set<int> set {1, 2, 3};
set.contains(2); // true
```

## C++ 标准库: std::move

`std::move()` 取左值（lvalue）对象作为参数并返回对象的右值引用。`std::move` 通过对其参数使用 `static_cast` 来实现这一点。`std::move` 让我们能够在对象构造中使用更高效的移动构造函数和移动赋值运算符。

`std::move()` 需要 `<utility>` 头文件。

```cpp
#include <iostream>
#include <utility>
#include <string>

using namespace std;
void print(string&& value) {
    cout << value << endl;
}

int main() {
    string value("print the string");

    // print(value) 失败因为 value 不是右值

    // value 被转换为右值
    print(std::move(value));
}

// 输出
print the string
```

## C++ 标准库: std::optional

考虑一个返回在某些文本中找到数字零的索引的函数。如果文本中不存在零，这是完全可以接受且不属于错误的。`std::optional` 设计设计用于处理这类情况。模板 `std::optional` 声明如下：

```cpp
#include <optional>
std::optional<class T> var;
```

`std::optional<class T>` 类型 T 的所有可能值以及值 `std::nullopt`。`std::nullopt` 表示无值或空物。`std::nullopt` 在语义上表示值的缺失。

以下示例显示了 `std::optional` 的典型用法：

```cpp
#include <iostream>
#include <optional>

using namespace std;

optional<unsigned int> evenNumber(unsigned int num) {
    if (num == 0)
        return num;

    return nullopt;
}

int main() {
    std::optional<unsigned> opt = evenNumber(5);

    if (opt.has_value()) {
        cout << "The number is "
             << opt.value()
             << "\n";
    } else
        cout << "no value returned";

    }
}
// 返回值
no value returned
```

如果 `evenNumber` 函数没有接收到偶数，`evenNumber` 返回 `nullopt`。否则函数返回一个无符号整数。

`opt.has_value()` 是一个谓词，用于检查 `std::optional` 变量是否有值或为 `nullopt`。`opt.value()` 返回该值。

如果 `opt` 是 `nullopt`，`opt.value()` 将抛出类型为 `std::bad_optional_access` 的异常。

## C++ 标准库: std::reference_wrapper

`std::reference_wrapper` 是一个封装引用的类，允许进行赋值和拷贝，而原始引用不行。`std::reference_wrapper` 提供了类似引用的接口，但它是可拷贝的。

```cpp
#include <iostream>
#include <functional>
#include <string>

using namespace std;

int main() {
    int x = 10;
    reference_wrapper<int> ref = x;
    cout << ref << endl;
    x = 20;
    cout << ref << endl; // 输出 20
}
```

`std::reference_wrapper` 是一个封装引用的类模板，允许进行赋值和拷贝，而原始引用不行。`std::reference_wrapper` 提供了类似引用的接口，但它是可拷贝的。

```cpp
#include <iostream>
#include <functional>
#include <string>

using namespace std;

int main() {
    int x = 10;
    reference_wrapper<int> ref = x;
    cout << ref << endl;
    x = 20;
    cout << ref << endl; // 输出 20
}
```

`std::cref` 是一个辅助函数，从对象创建一个 `std::reference_wrapper`。

```cpp
#include <iostream>
#include <functional>
#include <vector>

using namespace std;

int main() {
    int x = 10;
    vector<reference_wrapper<int>> v;
    v.push_back(cref(x));
    x = 20;
    cout << v[0] << endl; // 输出 20
}
```

`std::bindref` 是一个辅助函数，从对象创建一个 `std::reference_wrapper<const T>`。

```cpp
#include <iostream>
#include <functional>
#include <vector>

using namespace std;

int main() {
    const int x = 10;
    vector<reference_wrapper<const int>> v;
    v.push_back(bindref(x));
    cout << v[0] << endl; // 输出 10
}
```

## C++ 标准库: std::map

`std::map` 是一个以键值对形式存储元素的关联容器。每个键都是唯一的，并按键排序。

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> myMap;
    myMap["apple"] = 5;
    myMap["banana"] = 10;

    for (auto const& [key, val] : myMap) {
        std::cout << key << ": " << val << std::endl;
    }
    return 0;
}
```

### 插入键值对

`insert` 方法用于向 map 添加新的键值对。

### 插入键值对

```
iterator map_name.insert( { key, element } )
```

需要括号是因为正在插入的是一个对（pair）对象。

### 删除键值对

```
void map_name.erase(iterator i);
```

这将删除由迭代器指向的键值对。

### 测试 Map 是否包含某个键

```cpp
if (myMap.find("foo") == myMap.end()) {
    // 未找到
} else {
    // 找到
}
```

### 测试 Map 是否包含某个值

从 C++20 开始，关联容器拥有 `contains` 成员函数来检查 map 是否包含某个键或 set 是否包含某个元素：

```cpp
std::map<int, char> map {{1, 'a'}, {2, 'b'}};
map.contains(2);                // true
map.contains(123);             // false
```

```cpp
std::set<int> set {1, 2, 3};
set.contains(2); // true
```

## C++ 标准库: std::move

`std::move()` 取左值（lvalue）对象作为参数并返回对象的右值引用。`std::move` 通过对其参数使用 `static_cast` 来实现这一点。`std::move` 让我们能够在对象构造中使用更高效的移动构造函数和移动赋值运算符。



`std::move()` 需要 `<utility>` 头文件。

```cpp
#include <iostream>
#include <utility>
#include <string>

using namespace std;
void print(string&& value) {
    cout << value << endl;
}

int main() {
    string value("print the string");

    // print(value) 失败因为 value 不是右值

    // value 被转换为右值
    print(std::move(value));
}

// 输出
print the string
```

## C++ 标准库: std::optional

考虑一个返回在某些文本中找到数字零的索引的函数。如果文本中不存在零，这是完全可以接受且不属于错误的。`std::optional` 设计设计用于处理这类情况。模板 `std::optional` 声明如下：

```cpp
#include <optional>
std::optional<class T> var;
```

`std::optional<class T>` 类型 `T` 的所有可能值以及值 `std::nullopt`。`std::nullopt` 表示无值或空物。`std::nullopt` 在语义上表示值的缺失。

以下示例显示了 `std::optional` 的典型用法：

```cpp
#include <iostream>
#include <optional>

using namespace std;

optional<unsigned int> evenNumber(unsigned int num) {
    if (num == 0)
        return num;

    return nullopt;
}

int main() {
    std::optional<unsigned> opt = evenNumber(5);

    if (opt.has_value()) {
        cout << "The number is "
             << opt.value()
             << "\n";
    } else
        cout << "no value returned";

    }
}
// 返回值
no value returned
```

如果 `evenNumber` 函数没有接收到偶数，`evenNumber` 返回 `nullopt`。否则函数返回一个无符号整数。

`opt.has_value()` 是一个谓词，用于检查 `std::optional` 变量是否有值或为 `nullopt`。`opt.value()` 返回该值。

如果 `opt` 是 `nullopt`，`opt.value()` 将抛出类型为 `std::bad_optional_access` 的异常。

### front

`char& string::front();`

`const char& string::front() const;`

返回字符串第一个元素的引用。如果该字符串对象带有 `const` 修饰，则函数返回一个 `const char&`。否则，它返回一个 `char&`。

### 数字转字符串

此字符串方法将数值参数转换为 `std::string`：

```cpp
std::to_string(1.2);      // "1.2"
std::to_string(123);      // "123"
```

### replace

将字符串中从字符位置 `pos` 开始、长度为 `len` 个字符的部分替换为新内容：

```cpp
string& replace (size_t pos, size_t len, const string& str);

string& replace (iterator i1, iterator i2, const string& str);
```

返回替换后字符串的指针。

### 将字符的所有出现处替换为另一个字符

```cpp
#include <algorithm>
#include <string>

void foo() {
    std::string s = "example string";
    // 将每个 'x' 替换为 'y'
    std::replace( s.begin(), s.end(), 'x', 'y');
}
```

### starts_with 和 ends_with

从 C++20 开始，字符串（以及字符串视图）拥有 `starts_with` 和 `ends_with` 成员函数，用于检查字符串是否以指定的子字符串开头或结尾：

```cpp
std::string str = "foobar";
str.starts_with("foo"); // true
str.ends_with("baz"); // false
```

### 字符串转整数

将字符串转换为整数：

```cpp
int num = stoi(str);
```

### 整数转字符串

```cpp
int my_int = 5;
string str = to_string(my_int);
```

### 子字符串

以下字符串函数从字符串返回一个子字符串：

```cpp
string substr(size_t pos = 0, size_t len = npos) const;
```

`pos` 是要拷贝的字符的位置。

`len` 是要拷贝的字符数。如果没有指定 `len`，则拷贝从起始位置到字符串结尾的所有字符。如果字符串长度小于 `len`，则只拷贝到字符串的结尾。

### C++ 标准库 std::swap

函数模板 `std::swap` 交换两个相同类型对象的内容。

`std::swap` 定义如下：

```cpp
template <class T>
void swap (T& a, T& b);
```

示例：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec1 = {0,1,2,3,4,5,6,7,8,9};
    std::vector<int> vec2 {-9, -8, -7, -6, -5, -4, -3, -2, -1, 0};
    std::swap(vec1, vec2);
    for (auto& item : vec1) {
        std::cout << item << " ";
        std::cout << std::endl;
    }
    for (auto& item : vec2) {
        std::cout << item << " ";
        std::cout << std::endl;
    }
    return 0;
}
```

### C++ 标准库：std::thread

C++11 通过 `#include <thread>` 实现了一个线程库。当程序开始执行时，操作系统在程序自身的进程空间中执行该程序。线程背后的思想是将一个进程划分为若干个独立执行的线程。其目的是通过并发执行多个线程来提高程序的性能。

默认情况下，当 C++ 程序开始执行时，它从默认线程 `main` 启动。如果程序没有创建任何线程，则它将完全在主线程中运行。该程序被称为单线程应用程序。

#### 基础线程创建

以下程序使用两个线程来计算范围内的奇数和偶数的个数：

```cpp
#include <iostream>
#include <thread>

size_t oddsum = 0;
size_t evensum = 0;

void even_sum(int start, int stop) {
    for (int i = start; i < stop; i++)
        if (i%2 == 0 ) evensum += i;
}
void odd_sum(int start, int stop) {
    for (int i = start; i < stop; i++)
        if (i%2 != 0 ) oddsum += i;
}

int main() {
    size_t start = 1000;
    size_t stop = 90678124;

    // 创建线程对象 t1 和 t2
    std::thread t1(even_sum, start, stop);
    std::thread t2(odd_sum, start, stop);

t1.join();
```

多次调用 `t1.detach()`（在没有后续 `t1.join()` 的情况下）将抛出异常。

### 互斥锁

当两个或多个线程尝试访问共享资源时，就会发生竞态条件。互斥锁（mutex）目的是通过锁定共享资源来防止竞态条件的发生，确保任何时刻只有一个线程可以访问资源。互斥锁通过锁定访问共享资源的代码部分来实现。

临界区是一个程序语句序列，由一个线程一次完整执行。通常，临界区由访问多个线程共享的变量（资源）的程序语句组成。临界区具有以下类型的符号语法：

```
锁定互斥锁
执行临界区
解锁互斥锁
```

注意，互斥对象必须被所有想要执行临界区语句的线程共享。因此，互斥锁被定义为全局变量。

### 使用 std::lock() 锁定多个互斥锁

`std::lock()` 尝试以无死锁的方式锁定多个互斥锁。其语法为：

```
std::mutex m1;
std::lock(m1);
```

`std::lock()` 将尝试获取其参数中所有互斥锁的锁。如果未能锁定所有互斥锁，它将解锁它已经锁定的互斥锁并等待。因此，这是一个阻塞调用。在下一次尝试中，它将尝试以不同的顺序锁定互斥锁。

如果 `std::lock` 函数成功锁定了所有互斥锁，它可以处理临界区。`std::lock` 函数在处理完临界区后，必须解锁它所定的所有互斥锁。

这是一个示例：

```
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mu;             // 我们的互斥对象
int balance = 0;           // 这是我们的共享资源
void deposit(int amount) {
    mu.lock();              // 获取共享资源的锁
    balance += amount;      // 这是临界区
    mu.unlock();            // 解锁互斥锁
}

int main() {
    std::thread t1(deposit, 100);
    std::thread t2(deposit, 200);

    t1.join();
    t2.join();

    std::cout << balance << std::endl;
}
// 输出
300
```

当 `t1` 锁定 `balance` 而 `t2` 尝试访问它时，`t2` 线程发现资源被锁定。`t2` 将等待 `balance` 被解锁。一旦资源解锁，`t2` 将获取锁并开始更新 `balance`。如果 `t1` 永远不释放互斥锁，就会死锁。

**注意：** 如果执行临界区时抛出异常，互斥锁将不会释放。

### try_lock()

`try_lock` 尝试锁定互斥锁。如果无法锁定互斥锁则返回 `false`，如果获取锁则返回 `true`。语法为：

```
using namespace std;

mutex m1;

bool m1.try_lock();
```

如果 `try_lock` 被已经拥有锁的线程调用，将产生未定义行为。

查看以下代码：

```
#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>
```

```
using namespace std;
mutex mu;

void print(void) {
    if (mu.try_lock() == false) {
        cout << "mutex is locked\n";
    }
    // 临界代码区
    else {
        cout << "mutex is unlocked\n";
        cout << "hello world\n";
        mu.unlock();
    }
}
```

```
int main() {
```

mu.lock();

thread t1(print);

t1.detach();

this_thread::sleep_for(std::chrono::seconds(3));

mu.unlock();

thread t2(print);

t2.detach();

this_thread::sleep_for(std::chrono::seconds(2));

```

输出：
mutex is locked
mutex is unlocked
hello world

线程尝试通过 `mu.try_lock()` 获取锁。如果失败，线程将立即返回。如果成功，线程将获取锁并执行临界代码。在执行完临界区后，它会释放锁。

### 使用 std::try_lock(m1, m2, ... mn) 锁定多个互斥锁

`std::try_lock(m1, m2, ... mn)` 尝试锁定其参数中的所有互斥锁。此函数必须提供两个或多个参数。

声明语法为：

```

int try_lock(m1, m2, ... mn)

```

如果 `try_lock` 成功锁定所有互斥锁，它返回 -1。如果未能锁定所有互斥锁，它将解锁它已经锁定的互斥锁，并返回第一个锁定失败的互斥锁的零开始的索引。

以下代码示例展示了标准用法：

```

#include <iostream>

#include <thread>

#include <mutex>

std::mutex m1, m2;               // 我们的互斥对象

int balance = 500;                // 这是我们的共享资源

void deposit(int amount)

{

    int ret = std::try_lock(m1, m2);

    if (ret == 0) {

        std::cout << "resource m1 is locked\n";

    } else if (ret == 1) {

        std::cout << "resource m2 is locked\n";

    } else {

        std::cout << "resource m1 and m2 not locked\n";

        // 这是临界代码区

        balance += amount;

        std::cout << "critical section processed" << std::endl;

        m1.unlock();

        m2.unlock();

    }

}

int main()

{

    std::cout << "balance: " << balance << std::endl;

    m2.lock();

    m1.lock();

    std::thread t1(deposit, 100);

    std::thread t2(deposit, 200);

    t1.join();

    t2.join();

    m1.unlock();

    m2.unlock();

}

```



以下示例展示了在递归函数中使用 `recursive_mutex` 的方法：

```

#include <iostream>

#include <thread>

#include <mutex>

int dec = 10;

std::recursive_mutex m1;

void rfunc(std::thread_id id) {

    if (dec < 1) return;

    m1.lock();

    // critical section

    dec--;

    std::cout << id << ":" << dec << " ";

    // recursion occurs here

    rfunc(id);

    // end of critical section

    m1.unlock();

}

int main() {

    std::thread t1(rfunc, "a");

    std::thread t2(rfunc, "b");

    t1.join();

    t2.join();

    return 0;

}

// output

a:9 a:8 a:7 a:6 a:5 a:4 a:3 a:2 a:1 a:0 b:-1

```

### 使用 std::lock_guard<mutex>

`lock_guard` 是一个带有模板声明的类模板：

```

std::lock_guard<T> m;

```

模板类型参数必须是实现了 `lock()` 和 `unlock()` 函数的互斥锁类型。

`lock_guard` 在离开作用范围时会自动释放互斥锁，即使抛出了异常。以下示例展示了如何使用 `std::lock_guard<mutex>` 对象：

```

#include <iostream>

#include <thread>

#include <mutex>

size_t sum = 0;

std::mutex m1;
```



```cpp
void adder(std::string id, size_t loop_limit) {

    // 使用参数 m1 创建一个 lock_guard 对象

    std::lock_guard<std::mutex> lock(m1);

    // critical section

    for (size_t i = 0; i < loop_limit; i++) {

        sum += i;

    }

    std::cout << id << ":" << sum << std::endl;

}

int main() {

    std::thread t1(adder, "t1", 20);

    std::thread t2(adder, "t2", 30);

    t1.join();

    t2.join();

    return 0;

}

// output

t1:190

t2:625
```

我们为互斥锁 `m1` 创建了一个 `lock_guard` 对象 `lock`。进入 `adder` 函数的线程将等待获取锁。一旦 `lock_guard` 对象离开作用范围或抛出异常，锁将自动释放。

`lock_guard` 对象的所有权无法通过拷贝构造函数或赋值来传递。

## std::unique_lock<std::mutex>

`std::unique_lock<std::mutex>` 类模板是一个包装器，允许锁定、带时间限制的锁定和递归锁定。互斥锁模板类型必须支持以下函数之一：`lock()`、`try_lock_for` 或 `try_lock_until`。模板类型还必须支持 `unlock()` 函数。

支持以下互斥锁类型：

- 1. `lock(some_mutex)`
- 2. `try_lock(some_mutex)`
- 3. `try_lock_for(some_mutex)`
- 4. `try_lock_until(some_mutex)`
- 6. `owns_lock(some_mutex)` - 对象是否拥有该互斥锁

`owns_lock()` 函数判断 `std::unique_lock` 是否已获取锁。

如果抛出异常或锁对象离开作用范围，由 `unique_lock` 对象获取的锁将自动释放。

`std::unique_lock` 对象可以与条件变量配合使用。此外，这些对象是可移动但不可拷贝的。

这是一个用法示例：

```cpp
#include <iostream>
#include <thread>
#include <mutex>
std::mutex m1; // mutex for critical section
void print_block(int n, char c) {
    // 可以使用以下互斥锁：
    // std::unique_lock<std::mutex> lock (m1);
    // std::unique_lock<std::mutex> try_lock (m1);
    // std::unique_lock<std::mutex> lock (m1);
    // std::unique_lock<std::mutex> try_lock_until (m1);
    std::unique_lock<std::mutex> lock (m1);
    // critical section
    for (int i = 0; i < n; i++) {
        std::cout << c;
    }
    std::cout << '\n';
}
int main () {
    std::thread t1(print_block, 20, 'a');
    std::thread t2(print_block, 20, 'b');
    t1.join();
    t2.join();
    return 0;
}
```
如果我们使用类型推断，可以指定 `std::unique_lock<std::mutex>` 对象为：

条件变量允许我们同步线程；它们只能与 `unique_lock` 对象配合使用。线程可以在条件变量上等待。当条件变量变化时，等待的线程会被通知。以下示例展示了条件变量的标准用法。在示例中，我们想要向银行账户存款然后取款。显然，取款之前必须先存款。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
std::mutex mu;
std::condition_variable cv;
size_t balance = 0; // shared resource
void deposit(size_t amt) {
    mu.lock();
    balance += amt;
    mu.unlock();
    cv.notify_one();
}
void withdraw(size_t amt) {
    std::unique_lock<std::mutex> lock(mu);
    cv.wait(lock, [] { return balance > 0; });
    balance -= amt;
    lock.unlock();
}
int main() {
    std::thread t1(deposit, 500);
    std::thread t2(withdraw, 400);
    t1.join();
    t2.join();
    std::cout << "final balance: " << balance << std::endl;
    return 0;
}
```
注意：条件变量的使用需要 `unique_lock`。在 `withdraw` 函数中，我们首先尝试锁定互斥锁。如果无法锁定，则保持等待。如果 `cv.wait()` 的条件不满足，互斥锁会被释放并继续等待。如果条件变量对象发送通知（`cv.notify_one()`），我们再次尝试获取锁。如果无法获取锁，则保持等待。如果获取了锁，则再次测试条件变量谓词。在 `deposit` 函数中，线程等待获取锁。如果获取了锁，执行存款。接下来释放锁。然后通知一个等待线程（`notify_one`）或所有等待线程（`notify_all`）。

## 线程本地存储

线程可以维护私有的数据。这种数据被称为线程本地数据或线程本地存储。每个线程本地变量的作用域限于创建它的线程。线程本地变量的行为类似于静态变量，只要线程存在它们一直存在。当线程需要这种存储时就会创建，也就是说存储是按需创建的。存储限定 `thread_local` 用于创建线程本地变量。

这是一个线程本地存储的示例：

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
std::mutex mu;
thread_local std::string s {"hello "};
void greet(std::string id)
{
    std::lock_guard<std::mutex> lock(mu);
    s = s + id;
    std::cout << s << std::endl;
}
int main()
{
    std::thread t1(greet, "t1");
    std::thread t2(greet, "t2");
    std::thread t3(greet, "t3");
    t1.join();
    t2.join();
    t3.join();
}
// output
hello t1
hello t2
hello t3
```

## C++ 标准库：std::tuple

`tuple` 是一种可以存储任意数量异构类型项目的数据结构：

```cpp
#include <string>
#include <tuple>
std::tuple<int, std::string, float> t1(5, "hello world", 5.3);
```

这创建了一个给定类型和值的 `tuple`。`tuple` 也可以在没有任何值的情况下构造：

```cpp
std::tuple<int, std::string, float> t2;
```

**注意：** 通常 STL 容器只能存储非引用的值。与其它 STL 容器不同，`tuple` 有一个特殊特性，它可以存储引用。

### Tuple 赋值

我们可以如下所示进行 tuple 拷贝赋值：

```cpp
std::tuple<int, std::string, float> t1{5, "hello", 5.5};
std::tuple<int, std::string, float> t2;
t2 = t1;
```

赋值运算符执行逐成员拷贝。

## 获取 Tuple 元素

我们可以通过如下方式提取 `tuple` 的成员：

```cpp
#include <iostream>
#include <string>
#include <tuple>
```

```cpp
int main() {
    std::tuple<int, std::string, double> t1(5, "hello world", 5.3);
    int x0 = std::get<0>(t1);
    std::string x1 = std::get<1>(t1);
    float x2 = std::get<2>(t1);
    std::cout << x0 << " " << x1 << " " << x2 << std::endl;
    return 0;
}
```

`std::get` 函数返回一个元组值的引用。`std::get<<i>>` 函数中的索引 `i` 必须是一个编译时常量。

相同类型的元组可以按字典序进行比较：

```cpp
if (t2 < t1) {
    ...
}
```

### 元组拼接

元组可以进行拼接：

```cpp
std::tuple<int, std::string, float> t1(5, "hello", 5.5);
std::tuple<std::string, char> t2;
t3 = std::tuple_cat(t1, t2);
```

`t3` 是一个类型为 `<int, string, float, string, char>` 的元组

### 设置元组元素的值

`std::get<<i>>(foo)` 返回元组中第 i<sup>th</sup> 个元素的引用。我们可以通过以下方式设置第 i<sup>th</sup> 个元素：

```cpp
std::get<<i>>(my_tuple) = "hello world";
```

## 元组类型特质 (Tuple Type Traits)

我们可以通过以下方式获取元组的大小和元组成员的类型：

```cpp
// 获取元组 t3 的大小
auto tsize = std::tuple_size<decltype(t3)>::value;
// 获取元组成员的类型
auto tuple_t = std::tuple_element<1, decltype(t3)>::type;
```

## std::pair

`pair` 是 `std::tuple` 的一种特殊情况，拥有两个元素。`std::pair` 定义如下：

```cpp
template <class T1, class T2>
struct pair;
```

## C++ 标准库: std::tie

注意：请先查看 `std::tuple`

模板 `std::tie` 创建一个元素均为引用的元组。`std::tie` 的语法为：

```cpp
template < class T1, class T2, class T3 >
tuple(T1&, T2&, T3&) tie( T1, T2, T3 ) noexcept;
```

以下示例使用 `std::tie` 创建了一个元组：

```cpp
#include <iostream>
#include <string>
#include <tuple>
int main() {
    int x = 5;
    std::string y = "hello world";
    double z = 6.8;
    std::tuple<int, std::string, double> mytuple;
    // 将引用赋值给 my_tuple
    mytuple = std::tie(x, y, z);
    std::cout << "tuple (0): " << std::get<0>(mytuple) << std::endl;
    std::cout << "tuple (1): " << std::get<1>(mytuple) << std::endl;
    std::cout << "tuple (2): " << std::get<2>(mytuple) << std::endl;
    return 0;
}
```

输出：
tuple (0): 5
tuple (1): hello world
tuple (2): 6.8

元组 `mytuple` 包含对 `x`、`y` 和 `z` 的引用。更改 `x`、`y` 或 `z` 会改变 `mytuple`，反之亦然。

我们可以通过使用 `std::ignore` 作为元素值来忽略 `std::tie` 函数中的元素。

## 解析元组

我们也可以使用 `std::tie` 将元组解放到变量中：

```cpp
#include <iostream>
#include <string>
#include <tuple>
int main() {
    int x;
    std::string y;
    double z;
    std::tuple<int, std::string, double, int> mytuple;
    // 给 mytuple 赋值
    mytuple = {5, "hello world", 0.67, 0};
    // 解析元组
    std::tie(x, y, z, std::ignore) = mytuple;
    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;
    std::cout << "z: " << z << std::endl;
    return 0;
}
// 输出
x: 5
y: hello world
z: 0.67
```

## C 和 C++ 程序的内存布局

典型的 C/C++ 程序在内存中包含以下部分：

- 代码段 (Text Segment)
- 数据段 (Data Segment)
- BSS 段 (BSS Segment)
- 堆段 (Heap Segment)
- 栈段 (Stack Segment)

![](img/dbc91000ed9a70eff6930bb93f194ab_532_0.png)

**代码段 (Text Segment)** 也称为 Code Segment，包含了将执行的机器语言代码。通常该部分是共享且只读的。

**数据段 (Data Segment)** 也称为初始化数据段，包含已初始化的全局变量静态变量。

**BSS 段 (BSS Segment)** 也称为未初始化数据段。在程序启动前，操作系统会将其初始化为零。

**堆段 (Heap Segment)**：程序使用 `malloc`、`calloc`、`realloc` 或 `new` 分配动态内存。内存向下增长。

**栈段 (Stack Segment)**：由栈指针管理，存储局部变量和函数参数。栈段的行为类似于后进先出 (`LIFO`)，当栈指针遇到堆时耗尽。我们可以通过以下代码获取程序的内存布局：

```c
#include <stdio.h>
/* BSS 段中的未初始化变量 */
int global;
// 存储在栈上的参数
int Foo(int z) {
    // 存储在数据段的静态变量
    static int i = 100;
    // 存储在栈上的局部变量
    int x = 5;
    // 存储在栈上的返回值
    return x;
}
int main() {
    // 堆上的动态分配
    float* y = malloc;
    free(y);
}
```

可以通过命令获取此程序的内存布局：
```bash
gcc -c -o memory-layout memory.c
```

## C++ 编译器

### GNU C++ 版本
```bash
g++ --version
```

### gcc 和 g++ 的区别

`GCC` 或 GNU Collection 指编译器支持的所有不同语言。

```bash
gcc 是 GNU 编译器
g++ 是 GNU C++ 编译器
```

- `gcc` 分别将 `*.c` 和 `*.cpp` 文件编译为 C 和 C++ 文件。
- `g++` 会编译 `*.c` 和 `*.cpp` 文件，但会将它们视为 C++ 文件。
- 如果我们使用 `g++` 链接由编译器创建的对象文件，它会自动链接 C++ 库（`gcc` 不这样做）。

### 编译并运行程序

```bash
g++ -a helloworld.cpp foo.cpp bar.c
```



如果没有用 `-a` 参数指定输出文件，编译器将创建可执行文件 `a.out`。

# 编译并输出文件

```bash
g++ -c foo.cpp
```

编译器将编译 `foo.cpp` 并输出对象文件 `foo.o`。

# 编译程序并链接库

```bash
g++ -o foo foo.cpp -lmath
```

`-lmath` 选项将库文件 `libmath.a` 或 `libmath.so` 链接到对象文件 `foo.o`。由于没有指定 `-L` 选项，库文件必须位于标准的编译器位置，例如 `/usr/lib`。

# gcc 和 g++ 选项

- `-std` 指定在 `g++` 中使用的 C++ 标准。例如：`-std=c++11`
- `-std=c99` 编译 ANSI C99。例如：`gcc hello.c -lsqlite3`
- `-fsyntax-only` 仅检查源码语法错误。
- `-S` 从源码创建汇编文件。
- `-g` 开启 `gdb` 调试。
- `-O` 或 `-O2` 开启优化。
- `-Wall` 开启大部分编译器警告。
- `-Wextra` 启用额外的警告标志。
- `-Wfatal-errors` 遇到第一个错误时终止。
- `-Werror` 将所有警告转换为错误。

# 编译过程

我们可以从源码获取汇编代码文件：

```bash
g++ -S foo.cpp
```

对象代码文件是包含机器语言指令的文件。可执行文件是机器代码文件的一种特殊类型。可执行文件通常采用操作系统可以理解的特定格式。可执行文件有一个部分称为文本段（text section），程序机器代码存储在此。在 Unix 和 Linux 中，机器文件（对象文件）被称为可执行可链接格式文件或 ELF 文件。

# 创建静态库和共享库

## 静态和共享库

库是预编译对象文件的集合，可以由链接器链接到程序中。库有两种类型：静态库和共享库。

静态库在 Unix 中的扩展名为 `.a`（归档文件）。当程序链接静态库时，程序使用的库函数机器代码会被复制到可执行程序中。

共享库在 Unix 中的扩展名为 `.so`（共享对象）。当程序链接共享库时，只会在可执行文件中创建一个小型表。在可执行文件运行之前，操作系统会加载程序使用的外部库函数的机器代码。这个过程被称为动态链接。动态链接使得可执行文件更小并节省磁盘空间，因为多个程序共享同一个库副本。此外，大多数操作系统允许内存中只存在一个运行程序使用的共享库副本，从而节省内存。无需重新编译主程序即可升级共享库。

静态库的一个主要优势是速度。静态库中没有符号的动态查询。

# 头文件和库的位置

在编译程序时，编译器需要头文件来编译源码。

编译器会搜索头文件的包含路径（include paths）以解析外部引用。包含路径通过编译器命令行上的 `-I` 选项（大写 I 后跟目录路径）或环境变量 `PATH` 来指定。由于头文件名是已知的（例如 `iostream.h`、`stdio.h`），编译器只需要包含目录路径。

链接器会搜索库路径以查找要链接到可执行文件中的库。库路径通过 `-L` 选项（大写 L）后跟目录路径，或通过环境变量 `LIBRARY_PATH` 来指定。

# 编译、链接与静态库

当一个 C 或 C++ 程序被编译时，编译器会生成目标代码。在生成目标代码后，编译器会调用链接器。链接器的主要任务之一是让库函数的目标代码对程序可用。链接器可以通过两种方式实现这一点：首先，通过将库代码合并到你的目标代码中（静态库），或者通过某些安排，使得库函数的完整目标代码不合并，但在运行时可用（动态链接库）。

在静态链接中，链接器将库函数的目标代码添加到可执行文件中。

## 创建静态库

### 第 1 步：创建源文件

创建包含库函数的源文件：

```cpp
/* filename: foo.cpp */
#include <stdio.h>
void funfoo() {
    printf("called funfoo()");
}
```

### 第 2 步：为库创建头文件

为库源文件创建包含文件：

```cpp
/* filename: foobar.h */
void funfoo();
```

### 第 3 步：编译库源文件

编译库源文件并生成目标文件：

```bash
gcc -c foo.cpp -o foo.o
gcc -c bar.cpp -o bar.o
```

如果我们创建一个动态库，必须使用 `-fPIC` 选项编译源文件。PIC 是位置无关代码（position independent code）的缩写：

```bash
gcc -fPIC foo.cpp -o foo.o
gcc -fPIC bar.cpp -o bar.o
```

### 第 4 步：创建静态库

通过将所有目标文件封装到一个静态库中创建静态库：

```bash
ar rcs foobar.a foo.o bar.o
```

`ar` 是一个 GNU 归档程序。选项有：r - 替换，c - 创建归档，v - 详细，s - 创建索引。目标文件的路径在命令行上指定。

### 第 5 步：将静态库链接到程序

我们可以按照如下方式使用 `foobar.a` 库。创建一个主程序：

```cpp
/* filename: driver.cpp */
#include "foobar.h"
int main() {
    funfoo();
    return 0;
}
```

编译 `driver.cpp` 并获取目标文件 `driver.o`。

```bash
gcc -c driver.cpp -o driver.o
```

如果库存在于非标准位置，必须使用 `-L` 选项指定静态库所在的目录。`-l` 标志指示库的。`-l` 假设库名以 `.a` 结尾（因此不必指定 `.a`）。链接过程会创建一个名为 `driver` 的可执行文件。

## 备选第 4 步：创建共享库

共享库通过使用 GCC 的 `-shared` 标志创建，并将生成文件的扩展名命名为 `.so` 而不是 `.a`：

```bash
g++ -shared foo.o bar.o -o shared/libobar.so
```

## 备选第 5 步：链接到共享库

我们按照如下方式动态链接共享库 `libobar.so`：

```bash
gcc driver.o -L./shared -lfoobar -o driver
```

`-L` 和 `-l` 选项含义与之前相同。如果库位于 `/usr/lib` 等标准位置，我们不需要使用 `-L` 选项。

# GCC 环境变量

- `PATH`：可执行文件和运行时共享库（`.so`）的搜索路径。
- `CPATH`：包含文件的搜索路径。它在 `-I<dir>` 选项指定的路径之后搜索。`C_INCLUDE_PATH` 和 `CPLUS_INCLUDE_PATH` 可用于指定 C 或 C++ 语言中头文件的搜索路径。
- `LIBRARY_PATH`：库的搜索路径。它在 `-L<dir>` 选项指定的路径之后搜索。

# 查找共享库

在 Unix 系统上，GCC 首先在 `/usr/local/lib` 中搜索库，然后在 `/usr/lib` 中搜索。随后，它按照命令行上指定的顺序在 `-L` 参数指定的目录中搜索库。GCC 加载器 `ld` 也会在这些标准位置查找共享库文件。

如果我们在标准位置安装了共享库，请确保文件权限正确。例如：

```bash
$ chmod 0755 /usr/lib/libfoo.so
```

# 使用 rpath 设置共享库位置

rpath（或运行路径）是一种将共享库的位置嵌入可执行文件本身的方法，而不是依赖于默认位置或环境变量。我们在链接阶段执行此操作。

```bash
gcc -L/home/username/foo -Wl,-rpath=/home/username/foo -Wall -o test main.c -lfoo
```

注意 `-Wl,-rpath=/home/username/foo` 选项。

# rpath 选项

rpath（或运行路径）是一种将共享库的位置嵌入可执行文件本身的方法，而不是依赖于默认位置或环境变量。我们在链接阶段执行此操作。

```bash
gcc -L/home/username/foo -Wl,-rpath=/home/username/foo -Wall -o test main.c -lfoo
```

注意 `-Wl,-rpath=/home/username/foo` 选项。

# 更新加载器配置

一旦我们在标准位置放置了共享库，并确保权限是正确的，我们通过更新缓存来告诉加载器其可用：

```bash
$ ldconfig
```

# 列出程序使用的共享库

`ldd` 打印程序使用的共享库。

```bash
ldd [-r] myProgram
```

`-v` 选项用于详细模式。它会打印使用的共享库。

```bash
$ ldd -v myProgram
```

# 调试程序

```bash
$ gdb hello
```

# C++ GDB 调试器

## 基础调试

为了调试程序，程序必须带有调试符号。调试符号将程序标识符映射到内存地址和代码行号。调试符号存在于编译器生成的文件中。`-g` 指示编译器生成调试符号：

```bash
$ g++ -g -std=c++20 -o hello.cpp
```

一旦程序带有调试符号进行编译，我们可以启动 `gdb` 调试器：

```bash
$ gdb hello
```

调试器将读取调试符号并停在调试提示符处。

`gdb> ` 是调试提示符。

gdb 的典型用法如下：启动 gdb 后，我们设置断点。断点是希望希望执行暂停的代码位置。每当 gdb 遇到断点时，它会在该处暂停程序执行，让我们检查各种变量的值。当我们到达断点时，可以单步执行（step），这意味着 gdb 每次执行一行代码然后暂停。

`run` 命令导致 gdb 运行程序到下一个断点：

```bash
gdb> run (或 gdb> r)
```

如果我们使用 `start` 选项（`gdb> start`），则 gdb 将在主函数处停止程序执行。

# 命令补全

我们在部分输入命令后按下 Tab 键，gdb 会尝试补全命令。

# 调试已运行的进程

# 设置断点

`break [函数名]` 命令在执行到达命名的函数时暂停运行程序。`break` 命令有以下语法形式：

- `gdb b`
- `gdb> break [函数名]`
- `gdb> break [文件名]:[行号]`
- `gdb> break [行号]`
- `gdb> break *[地址]`
- `gdb> break **上述任何一个参数*** if [条件]`

例如，如果 `square(int x)` 是一个函数，我们可以这样做：

```bash
$ gdb break square if x == 5
```

注意：使用作用域解析操作符可以在作用域函数处设置断点，例如：

```
gdb> b account :: balance
```

我们可以通过以下命令删除所有断点：

```
gdb> delete
or
gdb> d
```

可以使用以下命令删除特定的断点：

- `gdb> clear [line number]`
- `gdb> clear [function_name]`

我们可以通过以下命令获取所有断点的信息：

```
gdb> info
```

注意：GDB 调试器可以用于调试线程。

# 在多次调试会话之间保存断点

如果你正正在进行一个复杂的调试会话，你很可能在多个源文件中设置了多个断点。此外，定位错误可能需要超过一个调试会话。在这种情况下，每次启动新会话时都要重新设置断点，这既令人沮丧又耗时。GDB 提供了一种避免此问题的方法。

首先，按照常规方式设置断点。然后将断点保存到文件中：

```
gdb> save breakpoints breakpoints.txt
```

现在，当你启动一个新的调试会话时，加载保存的断点：

```
gdb> source breakpoints.txt
```

# 单步执行程序

当我们停在断点处时，可以逐行步执行程序。

`next` 和 `step` 命令都告诉 gdb 执行程序的下一行，然后再次暂停。如果该行是一个函数调用，那么 `next` 和 `step` 将产生不同的结果。如果我们使用 `step`，程序将在函数的第一行暂停；如果我们使用 `next`，程序将在函数调用之后的一行暂停。

```
gdb> next      // gdb n
or:
gdb> s       // gdb s
```

# 跳出函数

如果我们已经使用 `step` 进入了某个函数，可以使用 `gdb> finish`（或 `gdb fin`）跳出该函数。

# 列出程序语句

当我们停在断点处时，可以列出我们停止位置的程序行以及周围的几行：

```
gdb> l
```

我们可以通过以下命令查看不同源文件中的程序行：

```
gdb> l filename:line_number
```

我们可以通过以下命令列出函数的几行：

```
gdb> l function_name
```

# 继续调试会话

在我们检查完断点处的代码后，可以使用以下命令继续调试会话：

```
gdb> continue          (or gdb> c)
or
gdb> continue repeat count
```

如果只是单独按回车键，gdb 将重复上一个命令。

# 重启调试会话

我们可以通过以下命令重启整个调试会话：

```
gdb > restart
```

# 检查和设置变量

当我们停在断点处时，可以使用以下命令检查如 `foo` 的变量：

```
gdb> print foo
or
gdb> p foo
```

我们可以显示当前执行函数的所有参数值：

```
gdb> info args
```

可以通过以下命令显示所有局部变量的当前值：

```
gdb> info locals
```

我们可以如下所示设置变量的值：

```
gdb> set var foo = 5
or:
gdb> p foo = 5
```

# 观察变量

在调试会话开始之前或停在断点处时，我们可以如下所示对变量设置观察点：

```
gdb> watch balance
gdb> run or continue
```

调试器将在 `balance` 的值变化的地方停止。

# 退出调试会话

```
gdb> quit
or
gdb> control-d (control-d 是文件结束符)
```

# .gdbinit 文件

每当启动 GDB 调试器时，它都会搜索 `.gdbinit` 文件，首先在用户的家目录中，然后在当前工作目录中。如果找到了该文件，将执行文件中列出的命令。文件中每行放置一个命令。

例如，如果我们希望调试器始终停在 `main()` 处，可以在 `.gdbinit` 中插入以下 GDB 命令：

```
gdb> b main.cpp
```

# 跟踪程序执行

假设我们在程序执行过程中遇到了导致程序崩溃的严重错误。我们可以通过 `backtrace` 命令定位发生该错误的程序语句。在调试器提示符下，输入：

```
gdb> bt
```

`bt` 会跟踪导致严重错误的函数调用。

# 调试核心转储 (Core Dump)

严重错误（如段错误）会终止程序执行并导致调试器输出核心转储。核心转储文件包含了创建程序中止点状态所需的所有信息。我们可以通过将核心转储文件作为第二个参数传递给 gdb 来访问核心转储中的信息：

```
gdb> hello core.file
```

# 调试段错误

考虑以下程序：

```cpp
// foo.cpp
#include <iostream>
using namespace std;
int main()
{
    int x = 7;
    int *p = 0;
    cout << "x = " << x;
    cout << "The pointer points to the value " << *p;
}
```

# SonarLint

Linter（代码检查工具）是一种静态代码分析工具，它通过检查程序语句，并标记那些虽然语法上正确、但不符合 C++ 惯用法，或者有更好、更安全语法结构的语句。使用良好的 linter 是提高代码库质量的极佳方法。

SonarLint 是一款优秀的 linter。SonarLint 与 Visual Code 无缝集成。你可以从 VisualCode 的扩展菜单中安装它。

SonarLint 在你在编辑器中编写代码时检查我们的代码。如果某个表达式不符合 C++ 惯用法，或者其语法可以改进，该表达式下方会出现一条波浪线。如果我们右键点击波浪线，SonarLint 将解释该表达式存在的问题并提供解决方案。

最佳实践是使用像 SonarLint 这样的 linter 来实时监控代码质量。

# C++ main 函数

每个 C 和 C++ 程序必须包含一个 `main` 函数。程序的执行从 `main` 函数开始。`main` 的签名由编译器预定义，如下：

```cpp
int main(void)
or int main(argc, char *argv[])
```



`main` 不能在 C++ 程序内部被调用，也不能带有 `virtual`、`static` 或 `inline` 属性。

`argc` 是 `argv` 中元素的计数。它始终大于或等于一。

第一个元素 `argv[0]` 是启动程序执行的命令。按照惯例，`argv[0]` 是程序的名称。`argv[0]` 不需要指定，它会从命令行隐式获取。`argv` 的其余参数是以空字符结尾的字符串，代表用户通过命令行传递给程序的参数。

# 杂谈：如何在 main 之前调用函数

C 和 C++ 程序在函数 `main()` 处开始执行。以下代码将在 `main()` 执行之前调用函数 `func()`：

```cpp
#include <iostream>

void func() { std::cout << "inside func" << std::endl; }

class Base {
public:
    Base() { func(); }
};

Base foo;

int main() {
    std::cout << "inside main" << std::endl;
    // output
    inside func
    inside main
}
```

全局变量 `foo` 将在调用 `main` 之前由编译器初始化。

我们还可以使用静态全局变量在 `main` 之前调用 `func`：

```cpp
#include <iostream>

int func() {
    std::cout << "in func" << std::endl;
    return 0;
}

static int foo = func();

int main() {
    std::cout << "in main" << std::endl;
    return 0;
}

// output
in func
in main
```

编译器会在调用 `main()` 之前初始化全局变量 `foo`。

# 杂谈：隐藏对象的地址

我们希望防止对象的地址被泄露。有两种方法可以：

- 将类的地址运算符 `&` 为私有 `private`
- 删除对象的地址运算符

以下示例将地址运算符设为私有：

```cpp
#include <iostream>

class base {
public:
    base() { std::cout << "inside base" << std::endl; }
private:
    base* operator(&) {return this};
};

int main() {
    base foo;
    base* bptr = &foo; // 将无法编译
    bptr = nullptr;
}
```

我们也可以删除地址运算符：

```cpp
#include <iostream>

class base {
public:
    base() { std::cout << "inside base" << std::endl; }
    base* operator(&) = delete;
};

int main() {
    base foo;
    base* bptr = &foo; // 将无法编译
    bptr = nullptr;
}
```

# 杂谈：继承与组合

继承是一种“是” `is-a` 的关系。组合是一种“有” `has-a` 的关系。类可以通过继承或组合来与其他类相关。

考虑以下三个类：

```cpp
class Mammal {
    ...
};

class Feet {
    int number_of_feet;
    int number_of_toes;
};

class Dog : public Mammal {
    int number_of_legs;
};
```

# C++ 术语表

## 应用二进制接口 `ABI`

指的是数据布局的方式：

- 函数参数的布局
- 数据的布局
- 类和结构体的布局
- 函数的布局
- 返回类型

## 拷贝消除 `Copy Elision`

消除 `有时被称为返回值优化` 是一种优化技术，在某些情况下，编译器被允许避免拷贝，即使 C++ 标准规定这样做。

考虑以下函数：

```cpp
std::string get_string()
{
return std::string("I am a string.");
}
```

根据 C++ 标准的措辞，此函数会在栈上创建并初始化临时 `std::string` 对象，并在返回语句执行时将对象拷贝到栈上，最后销毁临时对象。标准非常清晰地说明了这种实现方式。

拷贝消除规则允许 C++ 编译器忽略临时对象的创建以及随后的拷贝和销毁。也就是说，编译器可以直接将临时对象的初始化表达式直接放在栈上。

## 工具链 `Toolchain`

将源代码转换为可执行程序的程序序列。

典型的 C 和 C++ 工具链包括：

- 预处理器处理源文件的预处理器符号。
- 编译器从预处理后的源码生成汇编语言。
- 汇编器将汇编文件转换为机器码 `对象文件或 .obj`。
- 链接器连接对象文件创建可执行文件。

## 编译单元 `Translation Unit`

在 C 和 C++ 中，编译单元是 C 或 C++ 编译器的最终输入。编译器处理编译单元并从中生成对象文件。

编译单元由经过 C 或 C++ 预处理器处理后的源文件组成，这意味着 `#include` 指令列出的头文件已被包含，`#ifdef` 块中的代码已被包含，且宏已被展开。单个编译单元会被编译器编译成单个对象文件。
