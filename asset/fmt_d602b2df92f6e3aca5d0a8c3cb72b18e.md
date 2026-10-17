
这里 `anotherCell` 已经构造完成，所以编译器调用了 `operator=`。

当你从函数或方法返回对象时，有时很难看出到底发生了哪些拷贝和赋值。假设 `getString()` 的代码如下：

```cpp
string SpreadsheetCell::getString() const
{
  return mString;
}
```
`块似乎不完整（在 `Spreadsheet` 类的定义处截断了），我将针对您提供的这部分内容进行翻译。如果您有完整的文本，请重新提供。

现在考虑以下代码：

```cpp
SpreadsheetCell myCell2(5);
string s1;
s1 = myCell2.getString();
```

当 `getString()` 返回 `mString` 时，编译器实际上会通过调用字符串构造函数创建一个无名的临时字符串对象。当你将它赋值给 `s1` 时，会调用 `s1` 的赋值运算符，并将临时字符串作为参数传递。然后，临时字符串会被销毁。因此，这单行代码调用了构造函数和赋值运算符（针对两个不同的对象）。然而，编译器可以自由实现返回值优化（RVO）来优化这一过程。

如果你还觉得不够困惑，请考虑这段代码：

```cpp
SpreadsheetCell myCell3(5);
string s2 = myCell3.getString();
```

在这种情况下，`getString()` 在返回 `mString` 时创建一个临时的无名字符串对象。但现在 `s2` 获取的是它的拷贝构造函数，而不是赋值运算符。

通过移动语义，编译器可以使用移动构造函数代替拷贝构造函数来从 `getString()` 返回 `mString`。这更高效。移动语义将在第 10 章中讨论。

如果你忘记了这些操作发生的顺序，或者调用了哪个构造函数或运算符，你可以通过在代码中临时添加有用的输出或通过使用调试器单步执行来轻松弄清楚。

## 拷贝构造函数与对象成员

你还应该注意构造函数中赋值和拷贝构造函数区别。如果一个对象包含其他对象，编译器生成的拷贝构造函数会调用每个所包含对象的拷贝构造函数。当你编写自己的拷贝构造函数时，可以使用 c-初始化列表（c-initializer）提供相同的语义，如之前所示。如果你在 c-初始化列表中遗漏了一个数据成员，编译器会在执行你构造函数体中的代码之前，对其执行默认初始化（对对象调用 0 参数构造函数）。因此，当构造函数体开始执行时，所有数据成员都已初始化完毕。

例如，你可以这样写你的拷贝构造函数：

```cpp
SpreadsheetCell::SpreadsheetCell(const Spreadsheet& src)
    : mString(src.mString)
{
    mValue = src.mValue;
```

然而，当你在构造函数体内为数据成员赋值时，你对它们使用的是赋值运算符而不是拷贝构造函数，因为如前所述，它们已经初始化过了。

在这个示例中，`mString` 使用拷贝构造函数初始化，而 `mValue` 则使用赋值运算符进行赋值。

## 总结

本章涵盖了 C++ 面向对象编程设施的基础方面：类和对象。它首先回顾了编写类和使用对象的基本语法，包括访问控制。然后，它涵盖了对象的生命周期：对象何时被构造、析毁和赋值，以及这些操作调用了哪些方法。本章详细说明了构造函数赋值运算符的语法，包括构造函数初始化（ctor）和初始化列表构造函数，并引入了拷贝赋值运算符的概念。它还明确规定了编译器会在什么情况下为你你编写了哪些特定的构造函数，并解释了默认构造函数不需要参数。

对于你们中的某些人来说，这一章大部分是复习。对于其他人来说，希望这一章能开启你们进入 C++ 面向对象编程世界的大门。无论如何，既然你已经精通了对象和类，请阅读第 8 章以学习更多它们的技巧和微妙之处。

# 8 精通类与对象

本章包含内容？

- 如何在对象中使用动态内存分配
- 你可以拥有的不同类型的数据成员（静态、常量、引用）
- 你可以实现的不同类型的方法（静态、常量、内联）
- 方法重载的细节
- 如何处理默认参数
- 如何使用嵌套类
- 如何让类成为其他类的朋友
- 什么是运算符重载
- 如何分离接口类和实现类。

WROX.COM 本章代码下载

请注意，本章的所有代码示例都可以作为该书籍网站（www.wxyz.com/go/proc+3e）上“Download Code”标签页中本章代码下载的一部分。

第 7 章开始了对类和对象的讨论。现在是时候精通它们的微妙之处了，以便你充分发挥它们的潜力。通过阅读本章，你将学习如何操作和利用 C++ 语言一些最强大的特性，以编写安全、高效且实用的类。

本章中的许多概念出现在高级 C++ 编程中，特别是在标准模板库（STL）中。

# 对象中的动态内存分配

有时，你在程序实际运行之前并不知道需要多少内存。正如你所知，解决方案是在程序执行期间动态分配你所需的空间。类也不例外。在编写类时，你并不知道对象需要多少内存。在这种情况下，对象应该动态分配内存。对象中的动态分配内存带来了几项挑战，包括释放内存、处理对象拷贝和处理对象赋值。

## Spreadsheet 类

第 7 章引入了 `SpreadsheetCell` 类。本章将开始编写 `Spreadsheet` 类。与 `Spreadsheet` 类一样，`Spreadsheet` 将在本章中不断演进。因此，各种尝试并不编写每个标题类的最佳方法。首先，`Spreadsheet` 仅仅是 `SpreadsheetCell` 的二维数组，并具有设置和检索特定特定位置单元格的方法。电子表格应用程序在一个方向使用字母在另一个方向使用数字来引用单元格，而这个 `Spreadsheet` 在两个方向都使用数字。以下是简单 `Spreadsheet` 类定义的首次尝试：

```cpp
#include "SpreadsheetCell.h"
class Spreadsheet {
public:
    Spreadsheet(int inWidth, int in);
    void setCellAt(int x, int y, const SpreadsheetCell& cell);
    SpreadsheetCell getCell(int x, int y);
private:
    bool inRange(int val, int);
    int maxWidth, mHeight;
    SpreadsheetCell** mCells;
};
```

> `Spreadsheet` 类使用了普通指针作为 `mCells`。在本章中这样做是为了展示后果并解释如何处理动态内存。在生产代码中，你应该使用 C++ 标准容器，如 `std::vector`，这将极地简化 `Spreadsheet` 的实现，但这样你就无法学会如何处理动态内存。在现代 C++ 中你不应该使用裸指针，但你可能会在现有代码中遇到它，这时你需要知道如何使用。

注意 `Spreadsheet` 类并不包含 `SpreadsheetCell` 的二维数组。相反，它包含一个 `SpreadsheetCell**`。原因是类的构造函数必须根据客户端指定的高度和宽度动态分配二维数组。为了动态分配二维数组，你需要编写以下代码。注意在 C++ 中，与 Java 不同，无法编写 `new SpreadsheetCell[mWidth] [mHeight]`。

```cpp
#include "Spreadsheet.h"
Spreadsheet::Spreadsheet(int inWidth, int inHeight) : mWidth(inWidth), mHeight(inHeight) {
mCells = new SpreadsheetCell [mWidth]
for (int i = 0; i < mWidth; i++) {
    mCells[i] = new SpreadsheetCell[mHeight]
}
```

栈上宽度为四、高度为三的 `Spreadsheet s1` 的结果内存如图 8-1 所示。

![](img/a5a77830a2588caaa564a7658d3af652_226_0.png)

图8-1

设置和检索方法的实现非常直观：

```cpp
void Spreadsheet::setCellAt(int x, int y, const SpreadsheetCell& cell) {
    if (!inRange(x, mWidth) || !inRange(y, mHeight)) {
        throw std::out_of_range("");
    }
    mCells[x][y] = cell;
}
SpreadsheetCell& Spreadsheet::getCellAt(int x, int y) {
    if (!inRange(x, mWidth) || !inRange(y, mHeight)) {
        throw std::out_of_range("");
    }
    return mCells[x][y];
}
```

请注意，这两种方法使用辅助方法 `inRange()` 来检查 x 和 y 是否代表电子表格中的有效坐标。尝试访问超出范围的数组元素会导致程序发生故障。此示例使用了异常，异常在第 1 章中提到，并在第 13 章中进行了详细描述。

## 使用析构函数释放内存

当你完成对动态分配内存的使用时，应该释放它。如果你在对象中动态分配了内存，那么释放内存的地方就在析构函数中。编译器保证在对象销毁时会调用析构函数。以下是之前的 Spreadsheet 类定义，包含一个析构函数：

```cpp
class Spreadsheet {
public:
    Spreadsheet(int inWidth, int inHeight);
    ~Spreadsheet();
    // 为了省略省略代码
}
```

析构函数的名称与类名（以及构造函数）相同，但前面有一个波浪号 (~)。析构函数不接受任何参数，且只能有一个。

以下是 Spreadsheet 类析构函数的实现：

```cpp
Spreadsheet::~Spreadsheet() {
    for (int i = 0; i < mWidth; i++) {
        delete mCells[i];
    }
    delete [] mCells;
    mCells = nullptr;
}
```

该析构函数释放了在构造函数中的内存。然而，并没有规则要求必须在析构函数中释放内存。你可以在析构函数中编写任何想要的代码，但将它用于释放内存或处理其他资源是一个好主意。

## 处理拷贝和赋值

回想第 7 章，如果你自己不写拷贝构造函数和赋值运算符，C++ 会为你编写它们。这些由编译器生成的方法会递归地对对象数据成员调用拷贝构造函数或赋值运算符。对于基本类型（如 `int`、`double` 和指针），它们提供浅拷贝或位拷贝或赋值：它们只是直接将数据成员从源对象拷贝或赋值到目标对象。当你从对象中动态分配内存时，这就会产生问题。例如，下面的代码在 `si` 传递给 `printSpreadsheet()` 函数时，拷贝电子表格 `si` 来初始化 `s`。

```cpp
#include "Spreadsheet.h"
void printSpreadsheet(Spreadsheet s)
{
    // 为了省略代码。
}
int main() {
    Spreadsheet s1(4, 3);
    printSpreadsheet(s1);
    return 0;
}
```

Spreadsheet 包含一个指针变量：mCells。电子表格的浅拷贝会得到 mCells 指针的 de对象拷贝，而不是底层数据的拷贝。因此，你将面临 `s` 和 `s1` 都指向相同数据指针的情况，如图 8-2 所示。

![](img/a5a77830a2588caaa564a7658d3af652_228_0.png)

图 8-2

如果 `s` 更改了 `mCells` 指向的某些内容，该更改也会显示在 `s1` 中。更糟糕，当 `printSpreadsheet()` 函数退出时，会调用 `s` 的析构函数，它释放了 `mCells` 指向的内存。这留下了图 8-3 所示的情况。

![](img/a5a77830a2588caaa564a7658d3af652_229_0.png)

图 8-3

现在 `s1` 拥有一个不再指向有效内存的指针。这被称为悬空指针。难以置信的是，赋值时的问题甚至更糟糕。假设你有以下代码：

```cpp
Spreadsheet s1(2, 2), s2(4, 3);
s1 = s2;
```

在两个对象构造完成后，你将拥有图 8-4 所示的内存布局。

![](img/a5a77830a2588caaa564a7658d3af652_230_0.png)

图 8-4

赋值语句之后，你将拥有图 8-5 所示的布局。

![](img/a5a77830a2588caaa564a7658d3af652_231_0.png)

SpreadsheetCell**mCells

Spreadsheet s2

![](img/a5a77830a2588caaa564a7658d3af652_231_1.png)

SpreadsheetCell**mCells

Spreadsheet s1

图 8-5

现在，不仅 `s1` 和 `s2` 中的 `mCells` 指针指向同一内存，而且你还遗忘了 `s1` 中 `mCells` 原指向的内存。这被称为内存泄漏。这就是为什么在赋值运算符中，你必须先释放左引用的内存，然后进行深拷贝。

如你所见，依赖 C++ 默认拷贝构造函数或赋值运算符并不总是一个好主意。

> 警告 每当你在类中动态分配内存时，你应该编写自己的拷贝构造函数和赋值运算符来提供内存的深拷贝。

## Spreadsheet 拷贝构造函数

以下是 Spreadsheet 类拷贝构造函数的声明：

```cpp
class Spreadsheet
{
public:
    Spreadsheet(int inWidth, int inHeight);
    Spreadsheet(const Spreadsheet& src);
    // 为了省略代码
};
```

以下是拷贝构造函数的实现：

```cpp
Spreadsheet::Spreadsheet(const Spreadsheet& src) {
    mWidth = src.mWidth;
    mHeight = src.mHeight;
    mCells = new SpreadsheetCell*[mWidth];
    for (int i = 0; i < mWidth; i++) {
        mCells[i] = new SpreadsheetCell[mHeight];
        for (int j = 0; j < mHeight; j++) {
            mCells[i][j] = src.mCells[i][j];
        }
    }
}
```

拷贝构造函数执行数据的深拷贝。这意味着它分配了新内存并将源对象的值拷贝到新内存中。

## 赋值运算符

以下是 Spreadsheet 类中赋值运算符的声明：

```cpp
class Spreadsheet
{
public:
    // 为了省略代码
    Spreadsheet& operator=(const Spreadsheet& rhs);
};
```

以下是赋值运算符的实现：

```cpp
Spreadsheet& Spreadsheet::operator=(const Spreadsheet& rhs)
{
    // 检查自赋值。
    if (this == &rhs) {
        return *this;
    }
    // 释放旧内存。
    for (int i = 0; i < mWidth; i++) {
        delete [] mCells[i];
    }
    delete [] mCells;
    mCells = nullptr;
    // 拷贝新内存。
    mWidth = rhs.mWidth;
    mHeight = rhs.mHeight;
    mCells = new SpreadsheetCell*[mWidth];
    for (int i = 0; i < mWidth; i++) {
        mCells[i] = new SpreadsheetCell[mHeight];
        for (int j = 0; j < mHeight; j++) {
            mCells[i][j] = rhs.mCells[i][j];
        }
    }
    return *this;
}
```

注意，这段代码看起来与拷贝构造函数中的代码非常相似。接下来的章节将解释如何避免这种代码重复。

> 警告 当一个类动态分配内存时，请编写析构函数、拷贝构造函数和赋值运算符。

> 注意 除了拷贝之外，C++ 还支持移动语义，这需要移动构造函数和移动赋值运算符。这些特性可以在某些情况下提高性能，并将在第10章中进行详细讨论。

## 拷贝构造函数和赋值运算符的常用辅助例程

拷贝构造函数和赋值运算符非常相似，但将共同的任务提取到一个辅助方法中是方便的。例如，你可以为 `Spreadsheet` 类添加一个 `copyFrom()` 方法，并如下重写拷贝构造函数和赋值运算符：

```cpp
void Spreadsheet::copyFrom(const Spreadsheet& src)
{
  mWidth = src.mWidth;
  mHeight = src.mHeight;
```
