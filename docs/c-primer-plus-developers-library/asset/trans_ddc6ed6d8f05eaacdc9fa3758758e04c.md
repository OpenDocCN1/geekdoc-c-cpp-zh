
## 其他形式的字符串字面量

回想一下，C++除了 `char` 之外还有 `wchar_t` 类型。而 C++11 又增加了 `char16_t` 和 `char32_t` 类型。可以创建这些类型的数组和这些类型的字符串字面量。对于这些类型的字符串字面量，C++分别使用 `L`、`u` 和 `U` 前缀。下面是一个如何使用它们的示例：

```cpp
wchar_t title[] = L"Chief Astrogator";  // wchar_t string
char16_t name[] = u"Felonia Ripova";    // char16_t string
char32_t car[] = U"Humber Super Snipe"; // char32_t string
```

C++11 还支持一种用于 Unicode 字符的编码方案，称为 UTF-8。在这种方案中，一个给定字符可能占用一个 8 位单元（八位组）到四个 8 位单元不等，具体取决于其数值。C++使用 `u8` 前缀来表示该类型的字符串字面量。

C++11 的另一项新增功能是原始字符串。在原始字符串中，字符只代表它们自身。例如，序列 `\n` 不会被解释为表示换行符；相反，它是两个普通字符：反斜杠和 n，并且会在屏幕上显示为这两个字符。再举一个例子，你可以在字符串中使用简单的 `"`，而不是我们在程序清单 4.8 中使用的更别扭的 `\"`。当然，如果允许字符串字面量内部出现 `"`，你就不能再使用它来界定字符串的结束位置。因此，原始字符串使用 `"(` 和 `)"` 作为定界符，并使用 R 前缀将它们标识为原始字符串：

```cpp
cout << R"(Jim "King" Tutt uses "\n" instead of endl.)" << '\n';
```

这将显示如下内容：

```text
Jim "King" Tutt uses \n instead of endl.
```

与之等价的标准字符串字面量如下：

```cpp
cout << "Jim \"King\" Tutt uses \"\\n\" instead of endl." << '\n';
```

这里我们必须使用 `\\` 来显示一个反斜杠，因为 `\` 会被解释为转义序列的第一个字符。

如果在键入原始字符串时按下 Enter 或 Return 键，这不仅会将屏幕上的光标移到下一行，还会在原始字符串中放入一个回车字符。如果你想在原始字符串中显示组合 `)"` 该怎么办？（谁不想呢？）编译器难道不会把第一次出现的 `)"` 解释为字符串的结尾吗？是的，它会。但原始字符串语法允许你在开头的 `"` 和 `(` 之间放置额外的字符。这意味着在最后的 `)` 和 `"` 之间必须出现相同的额外字符。因此，以 `R"+*(` 开头的原始字符串必须以 `)+*"` 结尾。于是，下面的语句

```cpp
cout << R"+*("(Who wouldn't?)", she whispered.)+*" << endl;
```

将显示如下内容：

```text
"(Who wouldn't?)", she whispered.
```

简而言之，默认的定界符 `"(` 和 `)"` 已被替换为 `"+*(` 和 `)+*"`。除空格、左括号、右括号、反斜杠以及制表符或换行符之类的控制字符外，你可以使用基本字符集中任何成员形式作为定界符的一部分。

R 前缀可以与其他字符串前缀组合，以生成 `wchar_t` 等类型的原始字符串。它可以是复合前缀的第一部分或最后一部分：`Ru`、`uR` 等。

现在让我们继续介绍另一种复合类型——结构。

## 介绍结构

假设你想存储一名篮球运动员的信息。你可能想存储他或她的姓名、薪水、身高、体重、平均得分、罚球命中率、助攻等。你希望有一种数据形式能在一个单元中保存所有这些信息。数组做不到这一点。尽管一个数组可以保存多个项，但每个项都必须是同一类型。也就是说，一个数组可以保存 20 个 int，另一个数组可以保存 10 个 float，但单个数组不能在某些元素中存储 int，而在另一些元素中存储 float。

满足你这种愿望（即存储篮球运动员信息）的答案是 C++ 结构。结构是一种比数组更通用的数据形式，因为单个结构可以保存多种数据类型的数据项。这使你能够将所有相关的篮球信息存储在一个结构变量中，从而统一数据表示。如果你想跟踪整支球队，可以使用结构数组。结构类型也是通向 C++ 面向对象编程（OOP）的中流砥柱——类——的垫脚石。现在稍微学习一点结构知识，就能让你更接近 C++ 的面向对象核心。

结构是一种用户可定义的类型，结构声明用于定义该类型的数据属性。定义好类型之后，就可以创建该类型的变量。因此，创建一个结构分为两步。首先，定义结构描述，用来描述并标记可以存储在结构中的不同数据类型。然后，可以创建遵循该描述方案的结构变量，或者更一般地说，结构数据对象。

例如，假设 Bloataire, Inc. 想要创建一种类型来描述其设计师充气产品系列中的成员。具体来说，该类型应保存物品名称、以立方英尺为单位的体积以及销售价格。下面是一个满足这些需求的结构描述：

```cpp
struct inflatable    // structure declaration
{
    char name[20];
    float volume;
    double price;
};
```

关键字 struct 表明该代码定义了一个结构的布局。标识符 inflatable 是这种形式的名称（或标记）；这使 inflatable 成为新类型的名称。因此，现在你可以像创建 char 或 int 类型的变量一样创建 inflatable 类型的变量。接下来，花括号之间是要在结构中保存的数据类型列表。每个列表项都是一条声明语句。这里可以使用任何 C++ 类型，包括数组和其他结构。这个示例使用了一个 char 数组，适合存储字符串，还使用了 float 和 double。列表中的每个单独项称为成员，因此 inflatable 结构有三个成员（见图 4.6）。简而言之，结构定义定义了一种类型的特征——在本例中就是 inflatable 类型。

![](img/9afc44517b591d64e2e19f623c9308ef_155_0.png)

定义结构之后，就可以创建该类型的变量：

```cpp
inflatable hat;             // hat is a variable of type inflatable
inflatable woopie_cushion;  // type inflatable variable
inflatable mainframe;       // type inflatable variable
```

如果你熟悉 C 结构，你会注意到（很可能是愉快地注意到）C++ 允许在声明结构变量时省略关键字 struct：

```cpp
struct inflatable goose;    // keyword struct required in C
inflatable vincent;         // keyword struct not required in C++
```

在 C++ 中，结构标记的使用方式就像基本类型名一样。这一变化强调结构声明定义了一个新类型。它还使省略 struct 不再被列入令人抓狂的错误清单。

假定 hat 是 inflatable 类型，你可以使用成员运算符（.）来访问各个成员。例如，hat.volume 指结构的 volume 成员，hat.price 指 price 成员。类似地，vincent.price 是 vincent 变量的 price 成员。简而言之，成员名使你能够访问结构的成员，就像索引使你能够访问数组元素一样。由于 price 成员被声明为 double 类型，hat.price 和 vincent.price 都等价于 double 类型变量，可以以普通 double 类型变量可用的任何方式使用。简而言之，hat 是一个结构，但 hat.price 是一个 double。顺便说一句，用于访问类成员函数（如 cin.getline()）的方法，其起源可以追溯到用于访问结构成员变量（如 vincent.price）的方法。

## 在程序中使用结构

现在我们已经介绍了结构的一些主要特性，是时候在一个使用结构的程序中将所有这些想法整合起来了。程序清单 4.11 说明了关于结构的这些要点。它还展示了如何初始化一个结构。

程序清单 4.11    structur.cpp

```cpp
// structur.cpp -- a simple structure
#include <iostream>
struct inflatable   // structure declaration
{
    char name[20];
    float volume;
    double price;
};

int main()
{
    using namespace std;
    inflatable guest =
    {
        "Glorious Gloria",  // name value
        1.88,               // volume value
        29.99               // price value
    };  // guest is a structure variable of type inflatable
// It's initialized to the indicated values
    inflatable pal =
    {
        "Audacious Arthur",
        3.12,
        32.99
    };  // pal is a second variable of type inflatable
// NOTE: some implementations require using
// static inflatable guest =

    cout << "Expand your guest list with " << guest.name;
    cout << " and " << pal.name << "!\n";
// pal.name is the name member of the pal variable
    cout << "You can have both for $";
    cout << guest.price + pal.price << "!\n";
    return 0;
}
```
