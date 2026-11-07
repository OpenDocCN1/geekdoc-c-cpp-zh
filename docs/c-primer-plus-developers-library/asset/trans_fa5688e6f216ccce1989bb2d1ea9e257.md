
下面是程序清单4.11中程序的输出：

```text
Expand your guest list with Glorious Gloria and Audacious Arthur!\nYou can have both for $62.98!
```

## 程序说明

与程序清单4.11中的程序相关的一个重要问题是结构声明放在哪里。对于 `struct.cpp`，有两种选择。你可以将声明放在 `main()` 函数内部，就在左花括号之后。第二种选择（也是这里采用的选择）是将其放在外部并位于 `main()` 之前。当声明出现在任何函数之外时，称为外部声明。对于这个程序，两种选择没有实际差别。但对于由两个或更多函数组成的程序，这种差别可能至关重要。外部声明可供其后的所有函数使用，而内部声明只能由声明所在的函数使用。大多数情况下，你会希望使用外部结构声明，以便所有函数都能使用该类型的结构（见图4.7）。

![](img/9afc44517b591d64e2e19f623c9308ef_157_0.png)

图4.7 局部和外部结构声明。

变量也可以在内部或外部定义，其中外部变量可在函数之间共享。（第9章“内存模型和命名空间”将进一步探讨该主题。）C++ 实践不鼓励使用外部变量，但鼓励使用外部结构声明。此外，通常将符号常量声明为外部也是合理的。

接下来，注意初始化过程：

```cpp
inflatable guest =
{
    "Glorious Gloria",  // name value
    1.88,                // volume value
    29.99                // price value
};
```

与数组一样，你使用一对花括号括起来的、以逗号分隔的值列表。该程序每行放置一个值，但你可以将它们全部放在同一行。只需记住用逗号分隔各项：

```cpp
inflatable duck = {"Daphne", 0.12, 9.98};
```

你可以将结构的每个成员初始化为相应类型的数据。例如，name 成员是字符数组，因此可以将其初始化为字符串。

每个结构成员都被视为该类型的变量。因此，`pal.price` 是一个 double 变量，而 `pal.name` 是一个 char 数组。当程序使用 `cout` 显示 `pal.name` 时，它会将该成员显示为字符串。顺便说一句，由于 `pal.name` 是字符数组，我们可以使用下标访问数组中的单个字符。例如，`pal.name[0]` 是字符 A。但 `pal[0]` 没有意义，因为 `pal` 是结构，而不是数组。

## C++11 结构初始化

与数组一样，C++11 扩展了列表初始化的特性。= 号是可选的：

```cpp
inflatable duck {"Daphne", 0.12, 9.98};  // can omit the = in C++11
```

接下来，空花括号会使各个成员被设置为 0。例如，下面的声明会使 `mayor.volume` 和 `mayor.price` 被设置为 0，并使 `mayor.name` 中的所有字节被设置为 0：

```cpp
inflatable mayor {};
```

最后，不允许窄化。

## 结构可以使用 `string` 类成员吗？

你能用 string 类对象代替字符数组作为 name 成员吗？也就是说，你能像下面这样声明结构吗：

```cpp
#include <string>
struct inflatable   // structure definition
{
    std::string name;
    float volume;
    double price;
};
```

下面是程序清单4.12中程序的输出：

```text
bouquet: sunflowers for $12.49
choice: sunflowers for $12.49
```

如你所见，逐成员赋值在起作用，因为 choice 结构的成员被赋予与 bouquet 结构中存储的相同的值。

你可以将结构形式的定义与结构变量的创建合并在一起。为此，在右花括号后跟上变量名（一个或多个）：

```cpp
struct perks
{
    int key_number;
    char car[12];
} mr_smith, ms_jones;   // two perks variables
```

你甚至可以初始化以这种方式创建的变量：

```cpp
struct perks
{
    int key_number;
    char car[12];
} mr_glitz =
{
    7,                 // value for mr_glitz.key_number member
    "Packard"          // value for mr_glitz.car member
};
```

然而，将结构定义与变量声明分开通常会使程序更易于阅读和理解。

对于结构，你还可以做另一件事：创建没有类型名的结构。为此，在定义结构形式和变量的同时省略标记名：

```cpp
struct       // no tag
{
    int x;    // 2 members
    int y;
} position;  // a structure variable
```

这会创建一个名为 position 的结构变量。你可以使用成员运算符访问其成员，如 position.x，但该类型没有通用名称。之后你不能再创建相同类型的其他变量。本书不使用这种受限的结构形式。

除了 C++ 程序可以将结构标记用作类型名这一点之外，C 结构具有到目前为止为 C++ 结构讨论的所有特性，只是不包括 C++11 的变更。但 C++ 结构更进一步。例如，与 C 结构不同，C++ 结构除了成员变量外还可以有成员函数。不过这些更高级的特性通常用于类而不是结构，因此我们将在从第10章“对象和类”开始介绍类时讨论它们。

```cpp
using namespace std;
inflatable guests[2] =          // initializing an array of structs
{
    {"Bambi", 0.5, 21.99},       // first structure in array
    {"Godzilla", 2000, 565.99}   // next structure in array
};

cout << "The guests " << guests[0].name << " and " << guests[1].name
     << "\nhave a combined volume of "
     << guests[0].volume + guests[1].volume << " cubic feet.\n";
return 0;
}
```

下面是程序清单4.13中程序的输出：

```text
The guests Bambi and Godzilla
have a combined volume of 2000.5 cubic feet.
```

## 结构中的位字段

C++ 与 C 一样，允许你指定占用特定比特数的结构成员。这对于创建例如与某个硬件设备上的寄存器相对应的数据结构很方便。字段类型应为整型或枚举类型（枚举将在本章后面讨论），冒号后跟一个数字表示要使用的实际比特数。你可以使用未命名字段来提供间距。每个成员称为*位字段*。下面是一个示例：

```cpp
struct toggle_register
{
    unsigned int SN : 4;    // 4 bits for SN value
    unsigned int : 4;       // 4 bits unused
    bool goodIn : 1;        // valid input (1 bit)
    bool goodToPgl : 1;     // successful toggling
};
```

你可以按通常方式初始化字段，并使用标准结构表示法访问位字段：

```cpp
toggle_register tr = { 14, true, false };
...
if (tr.goodIn)   // if statement covered in Chapter 6
...
```

位字段通常用于底层编程。通常，使用整型类型以及附录 E“其他运算符”中列出的按位运算符可提供另一种方法。

## 共用体

共用体是一种数据格式，可以保存不同的数据类型，但一次只能保存一种类型。也就是说，结构可以保存例如一个 int、一个 long 和一个 double，而共用体可以保存一个 int 或一个 long 或一个 double。其语法与结构类似，但含义不同。例如，考虑下面的声明：

```cpp
union one4all
{
    int int_val;
    long long_val;
    double double_val;
};
```

你可以使用 one4all 变量保存一个 int、一个 long 或一个 double，只要是在不同时间这样做即可：

```cpp
one4all pail;
pail.int_val = 15;        // store an int
cout << pail.int_val;
pail.double_val = 1.38;   // store a double, int value is lost
cout << pail.double_val;
```

因此，pail 可以在一种场合充当 int 变量，而在另一种场合充当 double 变量。成员名标识该变量当前以何种身份起作用。

由于共用体一次只保存一个值，因此它必须有足够的空间来容纳其最大成员。因此，共用体的大小是其最大成员的大小。

共用体的一种用途是，在数据项可以使用两种或更多格式但绝不会同时使用这些格式时节省空间。例如，假设你管理一个混合的 widget 库存，其中一些具有整数 ID，另一些具有字符串 ID。在这种情况下，你可以使用以下代码：

```cpp
struct widget
{
char brand[20];
int type;
union id              // format depends on widget type
{
    long id_num;       // type 1 widgets
    char id_char[20];  // other widgets
} id_val;
};
...
widget prize;
...
if (prize.type == 1)                 // if-else statement (Chapter 6)
    cin >> prize.id_val.id_num;      // use member name to indicate mode
else
    cin >> prize.id_val.id_char;
```
