

## 5.1 基本数据类型

### 5.1.1 基本 C 数据类型

C 编程语言支持的基本数据类型包括两种基本算术类型。*整数*类型表示字符或整数，而*浮点*类型表示浮点数，并具有符号位、尾数和指数。

类型前可以加上修饰符，以指定类型是否带符号（仅限整数类型）、大小（`char` 除外，通常始终为 8 位）和精度（仅限浮点类型）。在大多数操作系统上（例如 IRIX 是个例外），整数类型除非另有说明，否则均为带符号：无符号整数可以容纳更大范围的正值。可用的具体类型及其大小取决于编译器。常见类型及其标称大小如下表所示。

| 类型 | 描述 | 大小（字节） |
|---|---|---|
| char | 字符 | 1 |
| short int | 短整数 | 2 |
| int | 整数 | 4 |
| long int | 长整数 | 8 |
| unsigned char | 无符号字符 | 1 |
| unsigned short int | 无符号短整数 | 2 |
| unsigned int | 无符号整数 | 4 |
| unsigned long int | 无符号长整数 | 8 |
| float | 浮点数 | 4 |
| double | 双精度浮点数 | 8 |
| long double | 扩展精度浮点数 | 12 |

此外可能还有其他类型，例如 `long long` 整数类型。标准 C 头文件 `limits.h` 定义了 `char` 的大小（例如 8 位）以及任何实现中允许的其他整数类型的最大值和最小值，以确保每种类型都有最小大小且不大于下一种类型。例如，int 永远不会比 long int 长。同样，头文件 float.h（或等效文件）定义常量，使得浮点类型的精度始终至少等于前一种类型。例如，double 的精度始终至少等于 float。

除了上述基本类型外，C 还定义了 void 类型，用于指定空值，例如用作不返回值的函数的返回类型。

还有枚举，这是一种与一组命名常量整数值关联的唯一类型。

### 5.1.2 基本 AJAX 数据类型

### 5.1.2.1 整数类型

基本 C 数据类型（char 除外）的确切大小和精度取决于实现。为避免这些系统相关限制可能带来的任何潜在问题，AJAX 在 AJAX 文件 ajarch.h 中定义了一组新的基本数据类型，如下所示：

| 类型 | 描述 |
|---|---|
| ajshort | 短整数 |
| ajint | 标准整数 |
| ajlong | 长整数 |
| ajushort | 无符号短整数 |
| ajuint | 无符号标准整数 |
| ajulong | 无符号长整数 |

ajarch.h 中列出的系统之间存在一些差异，但典型定义如下：

```
typedef short ajshort;
typedef int ajint;
typedef long long ajlong;
typedef unsigned int ajuint;
typedef unsigned short ajushort;
typedef unsigned long long ajulong;
```

ajint 通常为 32 位，ajlong 通常为 64 位。如果 32 位足够，请使用 ajint 而不是 int。请使用 ajlong 而不是 long 或 long long。话虽如此，在某些情况下，标准 C int 和 long 应该被使用，例如作为 C 系统库函数的参数。

您应根据需求选择数据类型。例如，如果您使用的是 Alpha 机器，那么 int 和 long 变量都将是 64 位。在这种情况下，不要出于懒惰而只使用 ajlong，因为您的代码在其他平台上可能运行得更慢。

### 5.1.2.2 其他 AJAX 类型

为方便起见，ajdefine.h 还定义了下表中列出的几种数据类型：

| 类型 | 描述 |
| :--- | :--- |
| AjBool | 布尔值 |
| AjStatus | 状态码 |
| AjIntArray | 整数数组（int*） |
| AjFloatArray | 浮点数组（float*） |

**AjBool** 用于存储 true（ajTrue, AJTRUE）和 false（ajFalse, AJFALSE）值。在输出时，转换代码 %b 写入 Y 或 N，而转换代码 %B 写入 Yes 或 No。
还有一个用于测试布尔值的宏：

```c
#define AJBOOL(b) (b ? "TRUE" : "FALSE")
```

**AjStatus** 旨在作为函数的通用返回代码，但目前未使用，因为 AjBool 已足够。它具有常量值，用于指示成功（ajStatusOK）、消息（ajStatusInfo）、警告（ajStatusWarn）、错误（ajStatusError）和致命错误（ajStatusFatal）。

**AjIntArray** 一个简单的 C 类型整数数组：

```c
typedef int* AjIntArray;
```

**AjFloatArray** 一个简单的 C 类型浮点数组：

```c
typedef float* AjFloatArray;
```

要使用这些 AJAX 数据类型，必须在代码中包含文件 ajdefine.h 和 ajarch.h。所有应用程序都必须在代码开头包含预处理器指令 #include "emboss.h"（参见第 2 章，您的第一个 EMBOSS 应用程序）。
emboss.h 是主包含文件，导入整个 EMBOSS 接口：它包含 AJAX 和 NUCLEUS C 编程库中的所有头文件，使所有代码可供您使用。如果您检查该文件，会看到包含了 ajax.h：

```c
% more nucleus/emboss.h

#ifndef emboss_h
#define emboss_h

#include "ajax.h"
#include "ajgraph.h"
.
.
```

它本身包含 ajdefine.h，而 ajdefine.h 包含 ajarch.h：

```c
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajdefine_h
#define ajdefine_h

#include "ajarch.h"
.
.
```

如果您开发使用基本类型的库代码，必须显式包含 ajdefine.h。例如，来自 ajstr.h：

```c
#ifdef __cplusplus
extern "C"
{
#endif

#ifndef ajstr_h
#define ajstr_h

#include "ajdefine.h"
#include "ajtable.h"
.
.
```

### 5.1.3 派生类型

可能从基本 C 数据类型派生出无限多的其他类型，如下所示：

- 单一类型对象的数组
- 返回单一类型对象的函数
- 指向给定类型对象的指针
- 各种类型对象的结构
- 能够容纳多个不同数据类型对象之一的联合

这里的“对象”可能指具有原始数据类型的变量、函数、数据结构等。通常，这些方法可以以复合方式应用。例如，可以有一个包含函数数组的数据结构，这些函数都返回指向浮点变量数组的指针。指针提供对特定类型对象的句柄，并在管理对象内存时使用。

在 EMBOSS 下编程时，出于大多数目的，事情被简化了：

- 定义新数据结构及其指针有标准方法。数据结构类型和指针类型分别称为“对象”和“对象指针”。
- 非 void 函数通常返回原始数据类型或对象指针。
- 结构通过引用（对象指针）传递给函数：结构本身从不传递。
- 构造函数和析构函数处理对象内存管理。
- 提供了用于通用内存管理的宏。
- AJAX 实现了常见基本数据类型的动态数组，其内存管理自动处理。其他一些数据类型（例如字符串）的内存管理也自动处理。

### 5.1.4 存储类和链接

C 中有两种存储类：自动和静态。每当进入声明自动对象的代码块时（跳入代码的情况除外），都会按声明顺序对其进行初始化。相比之下，静态对象仅在程序正式启动前初始化一次。对象的存储类取决于其声明的上下文和使用的关键字。

自动对象是块局部的，并在退出块时被丢弃。块中的声明默认是自动的，尽管可以使用 auto 关键字显式声明。使用 register 声明的对象是自动的，并且在可能的情况下，会在最快可用的内存寄存器中处理。

静态对象可能是块局部的，也可能是与函数定义处于同一级别的所有块之外。无论哪种情况，在退出并重新进入块时，它们都会保留其值。它们使用关键字 static 声明。

对所有块外部的对象始终是静态的。在这种情况下，static 关键字赋予它们内部链接，这意味着它们仅在本地文件中可见。否则，它们具有外部链接，这意味着它们对整个程序或其他编译单元是全局的。

在为 EMBOSS 编程时，这里有几个含义。任何私有于库文件或应用程序的联合和 C 数据结构（对象）都应在库或应用程序 C 源代码文件中声明为 static。任何公共（外部）联合和结构都在相应的库头文件中给出，不应包含 static 关键字。同样，库中的所有应用程序函数和私有函数都应声明为 static。库中的公共函数不应包含此关键字。

避免将名称导出到单个 C 源文件之外；也就是说，尽可能将每个函数声明为 static（在库头文件或应用程序代码中）。如果代码仅特定于某个应用程序，则应保留在应用程序 C 源代码文件中，直到它更具通用性之前，不要将其移动到库中。

所有数据类型都应按 EMBOSS 风格定义，并且函数必须使用完整的 ANSI C 样式进行原型声明（参见附录 C，C 编码标准）。

