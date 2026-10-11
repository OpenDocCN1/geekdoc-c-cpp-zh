
C++11 还支持 Unicode UTF-8 编码方案。在这种方案中，字符根据数值可以存储在 8 位单位（字节）到 4 位单位的任何位置。C++ 使用 `u` 前缀来表示该字符串字面量。

另一个 C++11 的新增特性是原始字符串（raw string）。在原始字符串中，字符直接代表它们本身；序列 `\n` 不会被解释为换行符；它是两个普通的字符，一个反斜杠和一个 `n`，并且会显示为这两个字符。原始字符串可以使用 `R"(...)"` 格式，例如：

```cpp
const char s = R"(c:\windows\temp)";
```

注意，原始字符串的结束符是 `)"`。如果原始字符串内部本身包含 `)"`，则可以使用自定义分隔符，如 `R"delimiter(...)"`。

## 介绍结构

用于新类型。因此，你现在可以像创建 `char` 或 `int` 类型变量一样创建 `inflatable` 类型的变量。接下来，括号之间是结构中要包含的数据类型列表。每个列表项都是声明语句。你可以在这里使用任何 C++ 类型，包括数组和其他结构。此示例使用了 `char` 数组，适用于存储一个字符串、一个 `float` 和一个 `double`。列表中的每个单独项被称为结构成员（structure member），因此 `inflatable` 结构有三个成员（见图 4.6）。简而言之，结构定义定义了一个类型的特征——在这种情况下是 `inflatable` 类型。

```
the struct         the tag becomes the name
keyword             for the new type

struct inflatable
opening and {char name[20];   structure
closing braces  float volume;   members
                 double price;};
terminates the structure declaration
```

图 4.6 结构描述的组成部分。

在定义结构之后，你可以创建该类型的变量：

`inflatable hat;` // hat 是类型为 inflatable 的结构变量

`inflatable woopie-cushion;` // 类型为 inflatable 的变量

`inflatable mainframe;` // 类型为 inflatable 的变量

如果你熟悉 C 结构，你会发现（很高兴地）C++ 允许在声明结构变量时省略 `struct` 关键字：

`struct inflatable goat;` // C 中需要 struct 关键字

`inflatable vincent;` // C++ 中不需要 struct 关键字

在 C++ 中，标签（tag）的使用就像基本类型名称一样。这种变化强调了结构定义定义了一个新类型。它允许从那些引起愤怒的错误列表中省略 `struct`。

由于 `hat` 是 `inflatable` 类型，你使用成员运算符 `.` 来访问各个成员。例如，`hat.volume` 指向结构中的 `volume` 成员，`hat.price` 指向 `price` 成员。同样，`vincent.price` 是 `vincent` 的 `price` 成员。简而言之，名称允许你访问结构的成员，而索引允许你访问数组的元素。由于 `price` 成员被声明为 `double` 类型，`hat.price` 和 `vincent.price` 都等同于 `double` 类型变量，可以像任何普通 `double` 变量一样使用。简而言之，`hat` 是一个结构，但 `hat.price` 是一个 `double`。

访问类成员函数（如 `cin.getline()`）的方法，源于访问结构成员变量（如 `vincent.price`）的方法。

# 在程序中使用结构

现在我们已经涵盖了结构的一些主要特征，是时候将这些思想整合到一个使用结构程序的中中了。列表 4.11 阐述了关于结构的这些点。它还展示了如何初始化结构。

列表 4.11 struct.cpp

```cpp
// struct.cpp -- 一个简单的结构
#include <iostream>
struct inflatable // 结构声明
{
    char name[20];
    float volume;
    double price;
};

int main()
{
    using namespace std;
    inflatable guest = {
        "Glorious Gloria", // name 值
        1.88, // volume 值
        29.99 // price 值
    }; // guest 是类型为 inflatable 的结构变量
    // 它被初始化为指定的值
    inflatable pal = {
        "Audacious Arthur",
        3.12,
        32.99
    }; // pal 是类型为 inflatable 的第二个变量
    // 注意：某些实现要求使用
    // static guest =

    cout << "Expand your guest list with " << guest.name;
    cout << " and " << pal.name << " \!\n";
    // pal.name 是 pal 变量的 name成员
    cout << "You can have both for $";
    cout << guest.price + pal.price << " \!\n";
    return 0;
}
```

这里是列表 4.11 程序的输出：

Expand your guest list with Glorious Gloria and Audacious Arthur!

You can have both for $62.98!

## 程序笔记

与列表 4.11 程序相关的一个重要问题是结构声明的位置。对于 `structure.cpp`，你有两种选择。你可以将声明放在 `main()` 函数内部，紧跟在大括号之后。第二种选择（也是这里采用的）是将其放在 `main()` 之外。当声明发生在任何函数之外时，它是外部声明。对于对于两个或多个函数的程序，这两个选择之间没有实际区别。外部声明可以被后续的所有函数使用，而内部声明只能被发现它的函数使用。通常，你希望外部声明，以便所有函数都能使用该类型（见图 4.7）。

```cpp
#include <iostream>
using namespace std;
struct parts
    unsigned long part_number;
    float cost;
};
void main();
int main()
{
    struct perks
        int key_number;
        char car[12];
    };
    parts chicken;
    perks mr_brug;
    ...
}
void mail()
{
    parts studebaker
    ...
}
```

外部声明——可以在所有函数中使用

内部声明——只能在此函数中使用

type parts 变量

type perks 变量

type parts 变量

在这里声明一个类型

type parts 变量

外部结构声明。变量也可以定义在内部或外部，并在函数之间共享（参见第 9 章“内存模型与命名空间”深入探讨此主题）。C++ 实践不鼓励使用外部变量但鼓励使用

# 第 4 章 复合类型

外部结构声明。此外，注意初始化过程：

```cpp
inflatable guest =
{  "Glorious Gloria", // name 值
  1.88, // volume 值
  29.99 // price 值
};
```

与数组类似，使用一对括号逗号分隔的值列表。程序期望每行一个值，但你可以将它们都放在同一行。只需记住用逗号分隔：

```cpp
inflatable duck = {"Daphne", 0.12};
```

你可以将结构的每个成员初始化为适当的数据类型。例如，`name` 成员是字符数组，因此你可以将其初始化为字符串。每个成员被视为变量，`pal.name` 是 `char` 数组。因此，`pal.price` 是 `double` 变量，当程序使用 `cout` 显示 `pal.name` 时，它显示为字符串。由于 `pal.name` 是字符数组，我们可以使用下标访问数组中的单个字符。例如，`pal.name[0]` 是字符 'A'。但 `pal[0]` 是无意义，因为 `pal` 是一个结构而不是数组。

# C++11 结构初始化

与……一样，C++11 扩展了列表初始化的功能。符号是可选的：

`inflatable duck {"Daphne", 0.12, 9.98};` // 在 C++11 中省略 =

接下来，空括号会导致成员设置为 0。例如，以下声明会导致 `major.volume` 和 `major.price` 被设置为 0，并且 `major.name` 中的所有字节被设置为 0：

```cpp
inflatable major {};
```

最后，不允许嵌套。

# 结构可以使用字符串成员吗？

你可以使用字符串对象代替字符数组作为 `name` 成员吗？也就是说，你可以这样声明结构：

```cpp
#include <string>
struct inflatable // 结构定义
{
  std::string name;
  float volume;
  double price;
};
```

答案是肯定的，除非你使用的是不支持字符串成员结构化的过时编译器。

确保结构定义访问 `std` 命名空间。你可以通过使用结构定义上面的 `using` 指令来实现。如前所示，更好的选择是将 `name` 声明为 `std::string`。

# 其他结构属性

C++ 可以尽可能让用户定义类型类似于内置类型。例如，你可以将结构作为参数传递给函数，并可以让函数将其作为返回值。你还可以使用赋值运算符 `=` 将一个赋值给另一个相同类型的。这样做会导致一个结构的每个成员被设置为另一个结构中对应成员的值，即使它是一个数组。这种赋值被称为成员赋值。我们将传递和返回结构推迟到第 7 章“函数：C++ 编程模块”，但我们现在可以快速查看结构赋值。列表 4.12 提供了一个示例。

+ 列表 4.12 assgn_st.cpp

```cpp
// assgn_st.cpp -- 赋值结构
#include <iostream>
struct inflatable
{
    char name[20];
    float volume;
    double price;
};
int main()
{
    using namespace std;
    inflatable bouquet =
        "sunflowers",
        0.20,
        12.49
    ;
    inflatable choice;
    cout << "bouquet: " << bouquet.name << " for $$";
    cout << bouquet.price << endl;

    choice = bouquet; // 将一个结构赋值给另一个
    cout << "choice: " << choice.name << " for $$";
    cout << choice.price << endl;
    return 0;
}
```

# 146 第 4 章 复合类型

这里是列表 4.12 中程序的输出：

bouquet: sunflowers for $12.49

choice: sunflowers for $12.49

如你所见，成员赋值（memberwise assignment）正在起作用，因为 choice 结构体的成员被赋值了存储在 bouquet 结构中的相同值。

你可以将结构体的定义与结构变量的创建结合起来。这样做是在闭大括号后面紧跟变量名或多个变量名：

```cpp
struct perks
{
    int key_number;
    char car[12];
} mr_smith, ms_jones; // 两个 perks 变量
```

你可以以此这种方式初始化创建的变量：

```cpp
struct perks
{
    int key_number;
    char car[12];
} mr_glitz = {
    7, // mr_glitz.key_number 成员的值
    "Packard" // mr_glitz.car 成员的值
};
```

然而，将结构体定义与变量声明分开通常会让程序更易读、更易理解。

你对结构体可以做的另一件事是创建一个没有类型名称的结构体。你可以通过在定义结构和变量的同时省略标签名（tag name）：

```cpp
struct
{
    // 无标签
    int x; // 2 个成员
    int y;
} position; // 一个结构体变量
```

这创建了一个名为 position 的变量。你可以通过成员运算符 `position.x` 访问它的成员，但该类型没有通用的名称。你随后无法创建相同类型的其他变量。本书没有使用这种受限形式的结构体。

除了 C++ 程序可以使用结构体标签作为类型名外，除了 C++11 的变化外，C 结构体拥有目前为止 C++ 结构体的所有功能。C++ 结构体更进一步。例如，与结构体不同，C++ 结构体除了成员变量外还可以有成员函数。但这些更的特性通常用于类（class）而不是结构体，因此我们将在介绍类时讨论它们，从第 10 章“对象与类”开始。

## 结构体数组

`inflatable` 结构体包含一个数组（name array）。也可以创建元素为结构体的数组。这种技术与创建基本类型的数组完全相同。例如，要创建一个包含 100 个 `inflatable` 结构体的数组，你可以这样做：

```cpp
inflatable gifts[100]; // 100 个 inflatable 结构体的数组
```

这使得 `gifts` 成为 inflatable 的数组。因此，数组的每个元素（例如 `gifts[0]` 或 `gifts[99]`）都是一个 `inflatable` 对象，并可以使用成员运算符：

```cpp
cin >> gifts[0].volume; // 使用第一个结构体的 volume
cout << gifts[99].price << endl; // 显示最后一个结构体的 price
```

请记住，如果 `gifts` 本身是一个数组而不是结构体，那么像 `gifts.price` 这样的构造是无效的。

要初始化结构体数组，将初始化数组的规则（每个元素的大括号包围、逗号分隔的值列表）与结构体的规则（每个成员的大括号包围、逗号分隔的值列表）结合起来。因为数组的每个元素都是结构体，值由结构体初始化来表示。因此，你最终得到大括号包围、逗号分隔的值列表，其中每个值本身都是

```cpp
inflatable guests[2] = // 初始化结构体数组
{
    {"Bambi", 0, 21.99}, // 数组中的第一个结构体
    {"Godzilla", 2000, 565.99} // 数组中的下一个结构体
};
```

照常，你可以按照喜欢的任何方式格式化它。例如，两个初始化可以在同一行，或者每个单独的结构体成员初始化可以占一行。

列表 4.13 显示了一个使用结构体数组的短示例。注意，由于 `guests` 是 `inflatable` 数组，`guest[0]` 是 `inflatable` 类型，因此你可以使用点运算符访问 `inflatable` 结构体的成员。

列表 4.13 arrstruct.cpp

```cpp
// arrstruct.cpp -- 结构体数组
#include <iostream>
struct inflatable
{
    char name[20];
    float volume;
    double price;
}
int main()
{
```

# 第 4 章 复合类型

```cpp
using namespace std;
inflatable guests[2] = // 初始化结构体数组
{
    {"Bambi", 0.5, 21.99},
    {"Godzilla", 2000, 565.99} // 数组中的下一个结构体
};

```

cout << "The guests " << guests[0].name << " and " << guests[1].name

    << " have a combined volume of "

    << guests[0].volume + guests[1].volume << " cubic feet.\n";

return 0;

```

这里是列表 4.13 中程序的输出：

The guests Bambi and Godzilla
have a combined volume of 2000.5 cubic feet.

# 结构体中的位域（Bit Fields）

C++ 像 C 一样允许你指定占据特定比特数的结构体成员。这对于创建一个对应于例如硬件设备上寄存器的数据结构非常有用。字段类型应该是整型或枚举（枚举将在本章稍后部分讨论），冒号后跟一个数字表示实际使用的比特数。你可以使用

```cpp
struct bitfield
{
    int a : 1; // 1 个比特
    int b : 1; // 1 个比特
    int c : 3; // 3 个比特
```
