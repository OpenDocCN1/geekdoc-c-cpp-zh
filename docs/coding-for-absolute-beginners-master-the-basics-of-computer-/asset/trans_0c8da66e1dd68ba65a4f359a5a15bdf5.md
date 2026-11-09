
```c
#include <stdio.h>
struct Distance
{
    int feet;
    float inch;
} dist1, dist2, sum;
int main()
{
    printf("1st distance\n");
    printf("Enter feet: ");
    scanf("%d", &dist1.feet);
    printf("Enter inch: ");
    scanf("%f", &dist1.inch);
    printf("2nd distance\n");
    printf("Enter feet: ");
    scanf("%d", &dist2.feet);
    printf("Enter inch: ");
    scanf("%f", &dist2.inch);

    sum.feet = dist1.feet + dist2.feet;

    sum.inch = dist1.inch + dist2.inch;

    while (sum.inch >= 12)
    {
        ++sum.feet;
        sum.inch = sum.inch - 12;
    }
    printf("Sum of distances = %d' - %.1f\"", sum.feet, sum.inch);
    return 0;
}
```

```
1st distance
Enter feet: 5
Enter inch: 9
2nd distance
Enter feet: 6
Enter inch: 3
Sum of distances = 12'-0.0"

...Program finished with exit code 0
Press ENTER to exit console.
```

### 将指针传递给结构体

我们还可以在 C 编程语言中定义指向结构体的指针，其定义方式与定义指向其他变量的指针相同。为了通过指针访问结构体的成员，可以考虑以下语法：

```c
Struct_pointer->title;
```

### C 编程文件

编程要求开发者通过使用最有效的方法来处理不同的需求和场景。要在 C 语言中执行文件处理操作，我们可以使用如下操作：

- `fprintf()`
- `fscanf()`
- `fread()`
- `fwrite()`
- `fseek()`

通常，程序终止时所有数据都会丢失，因此我们必须创建一个包含所有数据的特定文件。这也可以节省时间，并让程序员通过输入几条命令从文件中访问数据，以及通过 C 语言运算符将数据从一台计算机传输到另一台计算机。

文件有两种类型，称为文本文件和二进制文件。文本文件是 `.txt` 文件，可以使用记事本创建，编写、维护和更新记录所需的工作量最小。二进制文件是 `.bin` 文件，它们以 0 和 1 的二进制形式存储数据。此外，与文本文件相比，二进制文件可以存储更大量的数据。

在 C 编程语言中，我们可以通过下表中提到的简单命令创建新文件、打开现有文件、从文件读取信息以及向文件写入信息，并关闭文件：

| 操作 | 语法 |
|---|---|
| 打开文件 | `ptr = fopen("fileopen", "mode")` |
| 关闭文件 | `fclose(fptr);` |
| 写入二进制文件 | `fwrite(address_data, size_data, numbers_data, pointer_to_file);` |
| 从二进制文件读取 | `fread(address_data, size_data, numbers_data, pointer_to_file);` |
| 写入文本文件 | `FILE *fptr; fptr = fopen("File address", "w");` |
| 从文本文件读取 | `FILE *fptr; fptr = fopen("File address", "r");` |
| 文件定位 | `fseek(FILE *stream, long int offset, int whence)` |

### 让 C 编程变得简单的必备技巧

对于初学者，建议他们始终通过将重要代码信息写在 `/*` 和 `*/` 之间来注释代码。注释代码的主要部分还可以让你更轻松地进行后续更改并改进程序的功能。此外，始终使用变量来存储数据，例如 `int`、`char` 和 `float`，因为这会让你更轻松地执行不同的操作和计算。

C 语言简单且快速。借助指针、关键字和按位运算符，编写高效的代码对初学者来说肯定不成问题。

![](img/9d932bec53e523b8d8b7b8134cf77ca7_63_0.png)

## 第五章

## C++

C++ 是一种自由形式的中级编程语言，由 Bjarne Stroustrup 于 1979 年开发。作为 C 编程语言的增强版本，C++ 现在已成为初学者最常用、最适合的语言。该语言提供了大约 7 种不同的编程风格，你可以根据需求选择最合适的风格。作为一种静态类型编程语言，C++ 允许编译器在执行程序之前指出错误或缺陷。此外，使用 C++ 进行面向对象编程可以方便地解决复杂问题，并扩展标准库的用途。C++ 是世界上最流行的编程语言，也广泛用于图形用户界面、操作系统和嵌入式系统。

### 基本语法

C++ 编程语言的基本语法与 C 等其他语言相同。程序员必须遵循预定义的一组规则，包括各种单词、符号、字符、操作和表达式，才能正确执行程序。

以下是我们可以编写的第一个 C++ 入门程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"My First Program in C++";
    return 0;
}
```

程序输出：My First Program in C++。

![](img/9d932bec53e523b8d8b7b8134cf77ca7_64_0.png)

程序详情如下：

- **`#include<iostream>`** = 该语句包含预定义的输入和输出函数，并通知编译器也包含 iostream 文件。
- **`using namespace std;`** = 该语句用于将函数、变量和操作存储于程序中，其中 std 被视为命名空间名称。
- **`int main()`** = 这是程序的主函数，执行从此处开始。`int` 是返回类型，表示编译器返回一个整数值，为此我们还必须在末尾包含 `return 0` 语句。
- **`cout << "My First Program in C++"`** = `cout` 是隶属于 iostream 文件的对象，用于显示内容。
- **`return 0;`** = 该语句从 main() 函数返回 0 值，也负责 main 函数的执行。

### 变量和数据类型

#### 变量

C++ 编程语言中有不同类型的变量。由于它们使用特定关键字定义，我们必须按照如下给出的语法创建变量、指定类型并赋值：

```cpp
Type variable = value;
```

##### 变量类型

- `int` = 用于存储整数和完整数字。例如，1、45、6346。
- `char` = 用于存储单个字符。例如，`'a'` 或 `'Z'`。
- `double` = 用于存储浮点数。例如，50.2、100.2342。
- `bool` = 用于存储具有两种状态的值：`true` 或 `false`。
- `string` = 用于存储文本。例如，`"C++ programming language"`。

要声明变量并为其赋值，我们可以遵循如下所述的语法：

```cpp
int newNum;
newNum = 50;
cout << newNum;
```

C++ 中使用的每个变量都应使用唯一名称来标识，这些名称称为标识符。要构造标识符，名称必须包含字母、数字或下划线，并且区分大小写。

#### 数据类型

C++ 编程语言中的数据类型定义了变量中可以存储的数据类型。通常，C++ 中的数据类型分为三类：内置、派生和用户定义。用户定义的数据类型包括结构体、联合和枚举，而派生数据类型基于数组、函数和指针。

C++ 的内置数据类型：

- `int`
- `char`
- `float`
- `double`
- `bool`

用户定义的数据类型：

- `union`
- `enum`
- `struct`

派生数据类型：

- 函数
- 数组
- 指针

### 修饰符类型和存储类

C++ 编程语言中的修饰符与 `char`、`double` 和 `int` 数据类型一起使用，以更改基类型的含义，从而满足某些编程条件。这些修饰符包括 `signed`、`unsigned`、`long` 和 `short`。

要定义 C++ 程序中变量和函数的作用域，我们可以使用存储类，例如 `auto`、`register`、`extern`、`mutable` 和 `static`。`auto` 存储类是所有局部变量的默认存储类，而 `static` 存储类允许编译器在程序生命周期内存储局部变量，并在其超出作用域时销毁它。

外部存储类提供对全局变量的引用，并在两个或多个文件使用相同的全局函数或变量时使用。对于 `mutable` 存储类，只考虑类对象，而且它们也可以由常量成员函数修改。

### 流程控制

在 C++ 编程中，控制流指的是指令、函数和语句被求值和执行的顺序。
