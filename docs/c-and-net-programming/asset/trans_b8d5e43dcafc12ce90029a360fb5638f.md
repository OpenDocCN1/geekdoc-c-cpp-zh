
| decimal | int | sbyte | virtual |
|---|---|---|---|
| Default | interface | sealed | volatile |
| delegate | internal | short | void |
| Do | is | sizeof | while |
| Double | lock | stackalloc |  |
| Else | long | static |  |
| Enum | namespace | string |  |

- 9. **上下文关键字** — 上下文关键字仅在有限的程序上下文中具有特殊含义，并且在该上下文之外可用作标识符。

| Add | alias | ascending |
|---|---|---|
| Async | await | descending |
| Dynamic | from | get |
| Global | group | into |
| Join | let | orderby |
| partial(type) | partial(method) | remove |
| Select | set | value |
| Var | Where (generic type constraint) | Where (query clause) |
| Yield |  |  |

表 2.3.1 上下文关键字

## 2.4 字面量和常量

### 2.4.1 字面量

### 概念

- 1. 字面量是表示存储在变量中的值的方式。
- 2. 字面量是程序中使用的常量值。

### 解释

- 3. 常量是固定值。常量指的是程序在执行期间不可更改的固定值。
- 4. 常量可以是任何基本数据类型，例如整数常量、浮点常量、字符常量或字符串字面量。此外还有枚举常量。
- 5. 此外，变量可以声明为常量，其值在程序执行期间不能更改。字面量分类如下，

![](img/3005a4307e6d8f3bb7e76eea28a92357_54_0.png)

### 2.4.2 字面量类型

### 1. 整数字面量

- a. 整数字面量是数字序列。
- b. 整数字面量可以指定为不带任何小数部分的数字。
- c. 整数字面量可以是 int、uint、long 或 ulong 类型。
- d. 要指定 uint、long 和 ulong，分别使用后缀 u/U、l/L 和 ul/UL。int 不使用后缀。
- e. 整数字面量可以是十六进制、八进制或十进制。
- f. 要指定十六进制和八进制整数字面量，分别使用前缀 0x/0X 和 o/O。十进制不使用前缀。

### 示例

```csharp
261079 // decimal
0xAD10 // hexadecimal
0576 // octal
67u // unsigned int
12ul // unsigned long
98L // long
25 // int
```

- g. 后缀类型整数字面量

| 后缀类型 | 字符 | 示例 |
|---|---|---|
| unsigned int | U | uint x = 100U; |
| long | L | long x = 100L; |
| unsigned long | UL | ulong x = 100UL; |
| float | F | float x = 100F; |
| double | D | double x = 100D; |
| decimal | M | decimal x = 100M; |

- h. 小写后缀：可以指定小写后缀，例如 u、l、ul、f、d 和 m。但这些后缀更容易与数字混淆。字母 'l' 有时会被看作数字 1。

### 小写后缀示例

小写后缀：`long x = 10000l;` // 这是 100001 还是 10000l？
大写后缀：`long x = 10000L;` // 这是 10000L。

```csharp
// C# program that uses literal number suffixes

using System;

class Program
{
    static void Main()
    {
        // Use long suffix.
        long l1 = 10000L;

        // Use double suffix.
        double d1 = 123.764D;

        // Use float suffix.
        float f1 = 100.50F;

        // Use unsigned suffix.
        uint u1 = 1000U;

        // Use decimal suffix.
        decimal m2 = 4000.1234M;

        // Use unsigned suffix and long suffix.
        ulong u2 = 100020003000400050000UL;
    }
}
```

### 2. 实数字面量

- a. 包含小数点的数字称为实数字面量，或者说，一个整数后跟小数点和分数部分称为实数字面量。
- b. 浮点字面量可以是 float 和 double 类型。
- c. 要指定 float 字面量，使用后缀 f/F；要指定 double 字面量，使用后缀 d/D。
- d. 浮点字面量可以指定为四种类型。
  - 整数
  - 小数部分
  - 指数
  - 十进制部分
- e. C# 还允许对浮点数使用科学计数法，其中指数部分也会添加到浮点数中。

### 示例

```csharp
3.14f // float value
3.123456d // double value
314.e54 // exponent floating value
```

### 3. 布尔字面量

C# 中有两种布尔字面量值。

- true
- false

### 4. 字符字面量

- a. C# 中的字符字面量用单引号括起来。例如 'a' 或 'B'。
- b. 字符字面量是不可变的，不能更改，但存储这些值的变量仅仅表示存储位置。
- c. 字符字面量可以是简单的单个字符或转义序列。
- d. **单字符字面量**：单字符字面量包含用单引号（' '）括起来的单个字符。

### 示例

```csharp
'a',
'8',
';',
' ',
'' etc
```

- e. **反斜杠字符字面量**：转义序列是具有某些预定义含义并以反斜杠字符开头的特殊字符。下表包含各种字符转义序列及其含义：

| 常量 | 含义（名称） |
| --- | --- |
| '\n' | 换行 |
| '\r' | 回车 |
| '\f' | 换页 |
| '\t' | 水平制表符 |
| '\a' | 警报 |
| '\b' | 退格 |
| '\0' | 空 |
| '\v' | 垂直制表符 |
| '\\' | 反斜杠 |
| '\'' | 单引号 |
| '\"' | 双引号 |

表 2.4.1 反斜杠字符字面量

### 示例

```csharp
// C# program that uses character literals

using System;

class Program
{
    static char _literal5 = 'e'; // Static character literal.
    const char _literal6 = '#'; // Constant character literal.

    static void Main()
    {
        //
        // Shows some example character literals.
        // ... Also shows a local constant character literal.
        // ... Then prints them.
        //
        char literal1 = 'A';
        char literal2 = 'b';
        char literal3 = '\\';
        const char literal4 = '_';

        Console.WriteLine(literal1);
        Console.WriteLine(literal2);
        Console.WriteLine(literal3);
        Console.WriteLine(literal4);
        Console.WriteLine(_literal5);
        Console.WriteLine(_literal6);
    }
}
```

### 输出

```text
A
b
\
_
e
#
```

### 5. 字符串字面量

- a. 字符串字面量是用双引号（"）括起来的字符序列。
- b. **字符串字面量**是常量字符串数据。
- c. 字符可以是字母、数字、空格和特殊字符。
- d. 字符串字面量还有一种类似 `@"..."` 的格式。

### 示例

```csharp
"Welcome to India"
"APJ Abdul Kalam"
@"Welcome to India"
"HELLO"
"23"
"4"
"a"
```

```csharp
// C# program showing use of string literals
using System;

class Program
{
    static string  _s1 = "String literal";
    const string  _s2 = "String literal 2";
    const string  _s3 = "String literal 3\r\nAnother line";
    const string  _s4 = @"String literal 4 Another line";
    const string  _s5 = "String literal\t tab";
    const string  _s6 = @"String literal\t tab";

    static void Main()
    {
        // Execution starts here
        string s1 = "String literal \"1\"";
        const string s2 = "String literal 2";
        string s3 = @"String literal ""3""";
        const string s4 = @"String literal 4";
        // Print the string literals.
        Console.WriteLine(
            "{0}\n{1}\n{2}\n{3}\n{4}\n{5}\n{6}\n{7}\n{8}\n{9}",
            _s1, _s2, _s3, _s4, _s5, _s6,
            s1, s2, s3, s4);
    }
}
```

### 输出

```text
String literal
String literal 2
String literal 3
Another line
String literal 4
Another line
```

|  |  |
|---|---|
| 字符串字面量 tab |  |
| 字符串字面量\ttab | （未识别制表符转义序列） |
| 字符串字面量 "1" | （使用引号转义 \"） |
| 字符串字面量 2 |  |
| 字符串字面量 "3" | （使用双引号转义 ""） |
| 字符串字面量 4 |  |

/* 上述程序在 Program 类类型上定义了六个类级字符串。第一个字符串字面量引用是静态变量，这意味着它将在使用它的方法体中的中间语言中被引用。 */

/* 注意：使用静态字符串将要求执行引擎解析元数据中的 _s1 标记。**然而，可以**在程序中任何可访问 _s2 变量的位置重新分配该变量，例如在 Main 方法中。 */

/* 字符串上的 @ 符号。程序中显示的四个字符串字面量在引号前带有 @ 符号前缀。此符号表示使用逐字字符串字面量语法。 */

/* 注意：使用 @ 时，反斜杠被视为字符而不是转义序列。C# 编译器允许在逐字字面量中使用真实换行符。引号应使用双引号进行编码。 */

**该程序写入**屏幕的是整个 Program 类中声明的字符串字面量的内容。请注意引号在 s1 和 s3 变量中如何显示。双引号会作为引号打印。`Console.WriteLine`

**Concat.** 在 C# 程序中，字符串变量的串联是在运行时完成的。另一方面，如果字符串变量是常量并且在编译时已知，编译器将生成移除了串联的中间语言。

**下一步：**此程序似乎串联了三个字符串。编译后，IL 显示只使用了一个字符串。

```csharp
string.Concat
```

### 示例

```csharp
// C# program that concatenates string literals
using System;

class Program
{
    static void Main()
    {
        const string a = "C#";
        const string b = "is ";
```
