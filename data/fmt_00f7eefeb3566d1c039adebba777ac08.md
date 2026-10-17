
```cpp
char8[] = u8"This is UTF-8";
char16_t[] = u16"This is UTF-16";
char32_t[] = u32"This is UTF-32";
```

或者，Unicode 常量可以使用 `\u` 转义序列跟随十六进制值定义。取决于 Unicode 类型（UTF-8、UTF-16 或 UTF-32），例如：

```cpp
char8[] = u8"\u2018";
char16_t[] = u16"\u2018";
char32_t[] = u32"\u2018";
```

Unicode 字符串可以用双引号界定，可以使用原始字符串字面量。

### 3.4.4 'long long int' 类型

C++ 也支持 `long int` 类型。在 32 位系统中，它至少有 64 位。

### 3.4.5 'size_t' 类型

`size_t` 类型不是内置原始整值，而是一种由 POSIX 提升的数据类型，用于回答“多少”和“多少个”非负整值。它不是一个特定的 C++ 类型，但在包含任何系统头文件时隐式定义。在 C++ 环境中定义 `size_t` 的头文件是 `<cstddef>`。

使用 `size_t` 的优点是一个概念性类型，而不是由修饰符修改的标准类型。这使得代码值具有自文档性。可以使用多个后缀（如 `UL`）来显式指定整数常量的 `unsigned int` 表示。同样，后缀 `uz` 或 `zu` 可指定整数常量表示为 `size_t`。

有时函数需要指向无符号整数的指针。例如，在某些架构上，函数需要指向 `unsigned int` 的指针。在这种情况下可以使用 `size_t` 变量，但必须提供地址。不过，存在其他位表示类型。例如，`uint32_t` 保证持有 32 位无符号值。最近 `int32_t` 持有 32 位有符号值。对于 8、16 和 64 位存在相应的类型。这些类型定义在头文件 `<cstdint>` 中，需要指定或使用无符号整数类型时，它们非常有用。

### 3.4.6 'std::byte' 数据类型

字节被广泛用于访问内存位置。传统上使用 `char` 类型，但 `char` 是有符号类型，且当将 `char` 插入流时，使用的是字符的表示而不是它的值。更重要的是文档告知读者，使用 `char` 代替了 8 位值。

与 `char` 类型不同，`std::byte` 仅旨在表示 8 位值。为了使用 `std::byte`，必须包含 `<cstddef>` 头文件。

`byte` 被定义为强类型枚举，简单地嵌入了 `unsigned char`：

```cpp
enum class byte: unsigned char {};
```

## 3.5. 强制转换的新语法

由于 `byte` 是没有预定义值的枚举，赋值只能在 `byte` 变量之间使用。`byte` 变量可以使用大括号包裹现有的 `byte` 或最多 8 位的固定值进行初始化（如下例中的 #1）。如果指定的值不符合 8 位（#2），或者指定的值既不是 `byte` 也不是 `unsigned char` 类型（#3），编译器将报错。

使用括号初始化不符合 8 位的值的 `byte` 的赋值或类赋值初始化也会影响（#4, #5）。在这些情况下，指定的值会被截断为低 8 位。以下是插图：

```cpp
byte value(0x23); // #1（见上文文字）
byte error(0x123); // #2

char ch = 0xfb; // #3
byte error(ch); // n
byte bl = byte(ch); // #4
value = byte(0123); // #5
```

`byte` 类型支持所有位运算，但位运算的右操作数也必须是 `byte`。例如：

```cpp
value &= byte(0xf0);
```

`byte` 类型的值还可以进行排序和等值比较。

遗憾的是，不支持其他操作。例如，`byte` 不能相加，也不能从流中插入，这在某种程度上 `std::byte` 没有普通类型（如 `unsigned int`）有用。C++ 允许我们定义一种行为类似于普通数值类型的类型，包括从中中提取值。在第 11.4 节中开发了这种类型。

### 3.4.7 数字分隔符

为了提高数字的可读性，整数和浮点字面量可以使用数字分隔符。分隔符是单引号，可以插入到字面量的数字之间以增强人类可读性。可以使用多个数字分隔符，但在连续数字之间只能插入一个分隔符。例如：

```cpp
1'000'000
3.141'592'653'589'793'238'5
'123 // 无法编译
1'23 // 也无法编译
```

传统上，C 提供了以下强制转换语法：

```cpp
(typename)expression
```

# 第 3 章 对 C++ 的初印象

这里 `typename` 是一个有效类型的名称，`expression` 是一个表达式。

C 风格的转换在 C++ 程序中应该仅使用新的 C++ 转换，因为它们提供了编译器机制来验证转换的合理性。这些机制是经典的 C 风格转换所不提供的。

转换不应与经常使用的构造函数表示法混淆：

```
typename(expression)
```

构造函数表示法不是转换，而是请求编译器从 `expression` 构建一个类型为 `typename` 的（匿名）变量。

如果确实需要转换，应该使用几种新式转换。这些新式转换将在接后的章节中介绍。

### 3.5.1 'static_cast' 运算符

`static_cast<type>(expression)` 用于在“概念上可比较或相关的类型”之间进行转换。这里和在其他 C++ 风格转换中一样，`type` 是表达式类型应该转换过去的目标类型。

以下是一些可以使用 `static_cast`（或应该使用它）的情况示例：

- *当将 int 转换为 double 时。*

这种情况发生在，例如，当计算两个 int 值的商且不丢失除法的小数部分时。在下面的片段中调用 `sqrt` 函数：

```
int x = 19;
int y = 4;
sqrt(x / y);
```

而在使用 `static_cast<double>(x)` 时，它返回 2.179，如下：

```
sqrt(static_cast<double>(x) / y);
```

这里需要注意的重要点是，`static_cast` 允许将其表达式的表示形式转换为目标类型所使用的表示形式。

还要注意，除法被放在转换表达式之外。如果除法是在转换内部进行的（如 `static_cast<double>(x / y)`），那么在转换有机会将操作数转换为 double 之前，已经执行了整数除法。

- *当将枚举值转换为 int 值（任何方向）。*

这两种类型使用相同的表示，但语义不同。将普通的枚举值赋值给 int 不需要转换，但当枚举是强类型枚举时，则需要转换。相反，将 int 值赋值给某些枚举类型的变量时，需要 `static_cast`。这是一个示例：

```cpp
enum class Enum
{
  VALUE
};
cout << static_cast<int>(Enum::VALUE);  // 显示数值值
```

- *将相关的指针相互转换*

`static_cast` 用于类继承的语境（参见第 13 章），将指向所谓“派生类”的指针转换为指向其“基类”的指针。它不能用于将无关的类型相互转换（例如，`static_cast` 不能用于将指向短整型的指针转换为 int）。

`void *` 是通用指针。它在 C 库中被频繁使用，因为通用指针与任何其他指针相关，应该使用 `static_cast` 将 `void *` 转换为预的目标指针。这从 C 的角度来看有些奇怪，可能只在特定语文中使用。这是一个示例：

C 库中的 `sort` 函数期望两个待排序的 `void *` 参数，因此比较函数必须将 `void const *` 参数转换为要排序数组的元素。如果数组是 `int 数组[]` 且比较函数的参数是 `void const *p1` 和 `void const *p2`，那么比较函数通过以下方式返回要排序的 int 地址：

```
static_cast<int>(*p1);
```

- *当撤销或引入 int 类型变量的符号修饰符时（记住 `static_cast` 允许更改表达式！）*

这是一个示例：C 函数 `tolower` 需要一个表示 `unsigned char` 值的 `int`。默认情况下，它是有符号类型。为了使用可用的 `char ch` 调用 `tolower`，我们应该使用：

```
tolower(static_cast<unsigned char>(ch));
```

### 3.5.2 ‘const_cast’ 运算符

`const` 关键字在转换中有一个特殊地位。通常任何 `const` 都是 `const` 有理由的。尽管如此，可能会遇到忽略 `const` 的情况。对于这些特殊情况，应该使用 `const_cast`。它的语法是：

```
const_cast<type>(expression)
```

`const_cast<type>(expression)` 用于撤销变量的 `const` 属性。

`const_cast` 的需求可能结合标准 C 库中的函数出现，这些函数传统上并不总是像应该的那样 const。例如，可能有 `strfun(char *s)`，它对其 `char *s` 参数执行某些操作，但实际上并没有修改指向 `s` 的字符。将 `const char hello[] = "hello";` 传递给 `strfun` 会产生警告：

```

passing ‘const char * as argument 1 of ‘fun(char *)’ discards const
```

`const_cast` 是防止该警告通过的方法：

```
strfun(const_cast<char *>(hello));
```

### 3.5.3 ‘reinterpret_cast’ 运算符

第三种新式转换用于更改信息的解释：`reinterpret_cast` 类似于 `static_cast`，但当已知定义的信息实际上可以或被解释为完全不同的内容时，应该使用 `reinterpret_cast`。它的语法是：

```
reinterpret_cast<type>(expression)
```

### 3.5.4 ‘dynamic_cast’ 运算符

最后是一种用于结合多态（第 14 章）的风格转换。它的语法是：

```
dynamic_cast<type>(expression)
```

与 `static_cast` 的动作完全在编译时确定不同，`dynamic_cast` 的动作是在运行时确定的，用于将指向另一个类对象（例如 `Base`）的指针转换为指向其所谓类层次结构中更深处的另一个对象（例如 `Derived`）的指针（这也属于向下转换）。

## 3.6. 关键字与保留标识

66 第 3 章 对 C++ 的初印象

catch delete inline public thread_local xor_eq

char do int register throw

注：

- * 自 C++17 标准以来，关键字 `register` 已经不再被使用，但它仍然是一个保留的标识符。换句话说，像如下的定义

  `register int index;`

  会导致编译错误。此外，`register` 不再被视为类说明符（存储类型说明符有 `extern`、`thread_local`、`mutable` 和 `static`）。

- * 运算符关键字：`and`、`and_eq`、`bitand`、`bitor`、`compl`、`not`、`not_eq`、`or_eq`、`xor` 和 `xor_eq` 分别是 `&&`、`=`、`|`、`!`、`!=`、`||`、`^` 和 `^=` 的符号替代方案。

C++ 还识别特殊标识符 `final`、`override`、`transaction_safe` 和 `transaction_safe_override`。这些标识符的特殊之处，它们在声明类或多态函数时会获得特殊的含义。第 14.4 节提供了更多细节。

关键字只能用于它们的预期用途，不能用作其他实体（例如变量、函数、类名等）的。除了关键字外，以下划线开头并位于全局命名空间（即不使用任何显式命名空间指定）或位于 `std` 命名空间的标识符也是保留标识符，它们的使用是实现者的特权。

## 第 4 章

## 命名空间

## 4.1 命名空间

想象一位想要开发交互式数学程序的数学老师。对于这个程序，需要使用 `cos`、`sin`、`tan` 等函数，但接受度数而不是弧度。遗憾的是，函数名 `cos` 已经被占用，而且该函数接受弧度作为参数而不是度数。

这类问题通常通过定义另一个名称来解决，例如函数名 `cosDegrees`。C++ 通过命名空间提供了另一种解决方案。命名空间可以被视为代码中定义标识符的区域或范围。在命名空间中定义的标识符通常不会与在地方定义的名称（即在命名空间之外）冲突。因此，可以在名为 `Degrees` 的命名空间中定义一个期望度数角度的 `cos` 函数，而不是使用期望弧度的标准 `cos` 函数。

### 4.1.1 定义命名空间

命名空间根据以下语法定义：

```cpp
namespace identifier
{
    // 声明或定义的实体
} // (声明区域)
```

定义命名空间时使用的标识符是标准的 C++ 标识符。

在上述代码示例引入的声明区域内，可以定义或声明函数、变量、结构体、类甚至（嵌套）命名空间。然而，可以使用多个命名空间声明来定义命名空间。声明是“开放”的，这意味着命名空间 `CppAnnotations` 可以在文件 `file1.cc` 中定义，也可以在文件 `file2.cc` 中定义。`file1.cc` 和 `file2.cc` 中 `CppAnnotations` 命名空间定义的实体被合并在一个 `CppAnnotations` 命名空间区域。例如：

```cpp
// 在 file1.cc 中
namespace CppAnnotations
{
    double cos(double argInDegrees)
    {
        ...
    }
}
```

```cpp
// 在 file2.cc 中
namespace CppAnnotations
{
    double sin(double argInDegrees)
    {
        ...
    }
}
```

`sin` 和 `cos` 都定义在同一个 `CppAnnotations` 命名空间中。

命名空间实体可以在命名空间之外定义。此主题在 4.1.4.1 节中讨论。

### 4.1.1.1 在命名空间中声明实体

而不是在命名空间中定义实体：

```cpp
namespace CppAnnotations
{
    double cos(double degrees);
    double sin(double degrees);
}
```

### 4.1.1.2 闭合命名空间

可以定义没有名称的命名空间。匿名命名空间将定义的实体可见性限制在定义匿名命名空间的源文件中。

匿名命名空间中定义的实体类似于 C 的静态函数和变量。在 C++ 中仍然可以使用 `static` 关键字，但它的首选用法是在类定义中（参见第 7 章）。在 C 静态变量或函数本可以使用匿名命名空间的情况下，C++ 应该使用匿名命名空间。

匿名命名空间是一个闭合命名空间：无法通过不同的源文件向同一个匿名命名空间添加实体。

## 4.1. 命名空间

### 4.1.2 引用实体

给定一个命名空间及其实体，可以使用作用域解析运算符。要引用命名空间中的实体，请使用作用域解析运算符：

```cpp
namespace CppAnnotations
{
    int x;
}

int main()
{
    int y = CppAnnotations::x;
}
```

### 4.1.2.1 'using' 指令

`using` 声明的通用替代方案是 `using` 指令：

```cpp
using CppAnnotations;
```

遵循此指令后，`CppAnnotations` 中的所有实体的使用就像它们通过 `using` 声明声明的一样。

## 4.1. 命名空间

为了说明，请考虑下面的示例。函数 `FBB::fun(FBB::Value v)` 定义在 `FBB` 命名空间中。可以在不显式提到命名空间的情况下调用它：

```cpp
#include <iostream>
namespace FBB
{
    enum Value // 定义 FBB::Value
    {
        FIRST
    };
    void fun(Value x)
    {
        std::cout << "fun called for " << x << '\n';
    }
}

int main()
{
    fun(FBB::FIRST); // Koenig 查找：无命名空间
    // 指定了 fun()
}
```

> /* 生成输出：

called for 0 */

编译器在处理命名空间时相当智能。如果命名空间 `FBB` 中的 `Value` 被定义为 `using Value = int`，那么 `FBB::Value` 将被识别为 `int`，从而导致 Koenig 查找失败。

另一个例子，请考虑以下程序。这里涉及到两个命名空间，每个都定义了自己的 `fun` 函数。由于不存在歧义，因为参数定义了命名空间且调用了 `FBB::fun`：
