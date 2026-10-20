

另一个在 C# 程序中总是出现的东西是 Main 方法。花括号 {} 内的任何代码都将被执行。你不必理解 Main 前后出现的关键字。在阅读本教程时，你会一点一点地了解它们。

Console 是 System 命名空间的一个类，它有一个 WriteLine() 方法用于输出/打印文本。在我们的示例中它将输出 "Hello World!"。

如果你省略 using System 行，你就必须写 System.Console.WriteLine() 来打印/输出文本。

注意：每个 C# 语句都以分号 ; 结尾

注意：C# 区分大小写："MyClass" 和 "myclass" 有不同的含义。

注意：与 Java 不同，C# 文件名不必与类名匹配，但它们通常是匹配的（为了更好的组织）。保存文件时，使用适当的名称保存，并在文件名末尾添加 ".cs"。要在你的电脑上运行上面的示例，请确保 C# 已正确安装。

## 2.3 WriteLine 或 Write

在 C# 中输出内容最常用的方法是 WriteLine()，但你也可以使用 Write()。

区别在于 WriteLine() 每次都在新行打印输出，而 Write() 在同一行打印（请注意，你应该在需要时记得添加空格，以提高可读性）：

**示例：**

```
Console.WriteLine("Hello World!");
Console.WriteLine("I will print on a new line.");
Console.Write("Hello World! ");
Console.Write("I will print on the same line.");
```

**结果：**

![](img/e7ca4af023a4148a909dd82c11f81893_45_0.png)

## 2.4 C# 注释

注释可用于解释 C# 代码，使其更易读。它也可以用于在测试替代代码时防止执行。

### 2.4.1 单行注释

单行注释以两个正斜杠 (//) 开始。

// 与行尾之间的任何文本都将被 C# 忽略（不会被执行）。

此示例在代码行前使用单行注释：

**示例：**

```
// This is a comment
Console.WriteLine("Hello World!");
```

### 2.4.2 C# 多行注释

多行注释以 /* 开始并以 */ 结束。

/* 与 */ 之间的任何文本都将被 C# 忽略。

此示例使用多行注释（注释块）来解释代码：

**示例：**

```
/* The code below will print the words Hello World
To the screen, and it is amazing */
Console.WriteLine("Hello World!");
```

## 2.5 C# 变量

变量是用于存储数据值的容器。

在 C# 中，有不同类型的变量（使用不同的关键字定义），例如：

- **int** - 存储整数（整数），无小数，如 123 或 -123
- **double** - 存储浮点数，带小数，如 19.99 或 -19.99
- **char** - 存储单个字符，如 'a' 或 'B'。Char 值用单引号包围
- **string** - 存储文本，如 "Hello World"。String 值用双引号包围
- **bool** - 存储两种状态的值：true 或 false

### 声明（创建）变量

要创建变量，你必须指定类型并为其分配值：

### 语法

```
Type variableName = value;
```

其中 type 是 C# 类型（如 int 或 string），variableName 是变量的名称（如 x 或 name）。等号用于为变量分配值。

要创建应存储文本的变量，请看以下示例：

**示例：**

创建一个名为 name 的 string 类型变量并为其分配值 "John"：

```
string name = "John";
Console.WriteLine(name);
```

要创建应存储数字的变量，请看以下示例：

**示例：**

创建一个名为 mynum 的 int 类型变量并为其分配值 15：

```
int mynum = 15;
Console.WriteLine(mynum);
```

## 2.6 常量

然而，如果你不想让其他人（或你自己）覆盖现有值，可以添加 const 关键字（这将声明变量为“常量”，意味着不可更改且只读）：

**示例：**

```
const int mynum = 15;
mynum = 20; // error
```

const 关键字在你希望变量始终存储相同的值时很有用，这样其他人（或你自己）就不会搞乱你的代码。常量的一个常见例子是 PI（3.14159...）。

注意：你不能在不分配值的情况下声明常量变量。如果这样做，会发生错误：A const field requires a value to be provided.

**示例：**

```
string firstname = "John ";
string lastname = "Doe";
string fullname = firstname + lastname;
Console.WriteLine(fullname);
```

对于数值，+ 字符作为数学运算符（请注意，我们在这里使用 int（整数）变量）：

**示例：**

```
int x = 5;
int y = 6;
Console.WriteLine(x + y); // Print the value of x + y
```

## 2.7 声明多个变量

要声明多个相同类型的变量，请使用逗号分隔的列表：

**示例：**

```
int x = 5, y = 6, z = 50;
Console.WriteLine(x + y + z);
```

**示例：**

```
int x, y, z;
x = y = z = 50;
Console.WriteLine(x + y + z);
```

## 2.8 C# 标识符

所有 C# 变量都必须用唯一名称标识。

这些唯一名称称为标识符。

标识符可以是简短的名称（如 x 和 y）或更具描述性的名称（age、sum、totalVolume）。

注意：建议使用描述性名称以创建可理解且可维护的代码：

**示例：**

```
// Good
int minutesPerHour = 60;

// OK, but not so easy to understand what m actually is
int m = 60;
```

## 2.9 C# 数据类型

如变量章节所述，C# 中的变量必须指定数据类型：

```
int mynum = 5; // Integer (whole number)
double myDoubleNum = 5.99D; // Floating point number
char myLetter = 'D'; // Character
bool myBool = true; // Boolean
string myText = "Hello"; // String
```

数据类型指定变量值的大小和类型。使用正确的数据类型对应变量非常重要；以避免错误，节省时间和内存，但它也会使你的代码更易于维护和阅读。最常见的数据类型是：

| Data Type | Size | Description |
|-----------|------|-------------|
| int | 4 bytes | Stores whole numbers from -2,147,483,648 to 2,147,483,647 |
| long | 8 bytes | Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| float | 4 bytes | Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits |
| double | 8 bytes | Stores fractional numbers. Sufficient for storing 15 decimal digits |
| bool | 1 byte | Stores true or false values |
| char | 2 bytes | Stores a single character/letter, surrounded by single quotes |
| string | 2 bytes per character | Stores a sequence of characters, surrounded by double quotes |

### 数字

数字类型分为两组：

整数类型存储没有小数的整数，正数或负数（如 123 或 -456）。有效类型为 int 和 long。你应该使用哪种类型取决于数值。

浮点类型表示带小数部分、包含一个或多个小数的数字。有效类型为 float 和 double。

### 整数类型

#### Int

int 数据类型可以存储从 -2147483648 到 2147483647 的整数。一般来说，在本教程中，当我们创建具有数值的变量时，int 数据类型是首选数据类型。

**示例：**

```
int mynum = 100000;
Console.WriteLine(mynum);
```

#### Long

long 数据类型可以存储从 -9223372036854775808 到 9223372036854775807 的整数。这在 int 不足以存储值时使用。请注意，你应该在值后加上 "L"：

**示例：**

```
long mynum = 15000000000L;
Console.WriteLine(mynum);
```

### 浮点类型

每当你需要带小数的数字，如 9.99 或 3.14515 时，你应该使用浮点类型。

#### Float

float 数据类型可以存储从 3.4e-038 到 3.4e+038 的分数数。请注意，你应该在值后加上 "F"：

**示例：**

```
float mynum = 5.75F;
Console.WriteLine(mynum);
```

#### Double

double 数据类型可以存储从 1.7e-308 到 1.7e+308 的分数数。请注意，你可以以 "D" 结尾值（尽管不是必需的）：

**示例：**

```
double mynum = 19.99D;
Console.WriteLine(mynum);
```
