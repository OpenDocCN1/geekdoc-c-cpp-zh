
## 第 6 章

- 1. 编写一个程序，通过指针调用此函数，并验证它确实能够工作。你需要在程序中添加一个 #include 指令，包含 `<cstring>` 头文件，以便使用 `strlen()` 函数。

- 2. 编写一组名为 `equal()` 的重载函数，它们接受两个同类型的参数，如果参数相等则返回 1，否则返回 0。提供具有 `char`、`int`、`double` 和 `char*` 参数的版本。（使用运行时库中的 `strcmp()` 函数测试字符串是否相等。如果你不知道如何使用 `strcmp()`，可以在在线帮助中搜索它。你需要在程序中添加一个 #include 指令，包含 `<cstring>` 头文件。）编写测试代码来验证调用了正确的版本。

- 3. 目前，当计算器遇到无效的输入字符时，它会打印一条错误消息，但不会显示错误在该行中的位置。编写一个错误处理例程，打印输入字符串，并在出错字符下方放置一个插入符（^），如下所示：

  ```
  12 + 4,2*3
    ^
  ```

- 4. 向计算器添加一个幂运算符 ^，使其与 * 和 / 并列。以这种方式实现它有哪些限制？你如何克服这些限制？

- 5. （高级）扩展计算器，使其能够处理三角函数和其他数学函数，让你可以输入如下表达式：

  ```
  2 * sin(0.6)
  ```

  数学库函数都以弧度为单位；请提供三角函数的相应版本，让用户可以使用角度，例如：

  ```
  2 * sind(30)
  ```

## 定义你自己的数据类型

本章介绍如何创建适合你自己的特定问题的数据类型，也涉及创建对象——面向对象编程的构建块。对于不了解的人来说，对象可能看起来有点神秘，但正如你将在本章中看到的，对象可以只是你自己的某个数据类型的一个实例。

在本章中，你将了解：

- [ ] 结构体及其用法
- [ ] 类及其用法
- [ ] 类的基本组成部分以及如何定义类类型
- [ ] 创建和使用类的对象
- [ ] 控制对类成员的访问
- [ ] 构造函数及如何创建它们
- [ ] 默认构造函数
- [ ] 类上下文中的引用
- [ ] 复制构造函数及其实现方式
- [ ] C++/CLI 类与原生 C++ 类的差异
- [ ] C++/CLI 类中的属性及其定义和使用方法
- [ ] 字面量字段及其定义和使用方法
- [ ] `initonly` 字段及其定义和使用方法
- [ ] 什么是静态构造函数

### C++ 中的 struct

结构体（structure）是一种使用关键字 `struct` 定义的用户自定义类型，因此它通常被称为 struct。struct 起源于 C 语言，C++ 对 C 语言中的 struct 进行了整合和扩展。在 C++ 中，struct 在功能上可以被类（class）替代，凡是你能用 struct 完成的事情，都可以通过使用类来实现；然而，由于 Windows 是在 C++ 被广泛使用之前用 C 语言编写的，struct 在 Windows 编程中随处可见。时至今日，它仍被广泛使用，因此你确实需要了解一些关于 struct 的知识。在本章中，我们将首先了解（C 风格的）struct，然后再探讨类所提供的更强大的功能。

### struct 是什么？

到目前为止，你见过的几乎所有变量都只能存储单一类型的实体——某种数字、一个字符，或者相同类型元素的数组。现实世界比这要复杂一些，差不多你能想到的任何物理对象，哪怕只是最低限度地描述，也需要若干项数据。想想描述像书这样简单的东西需要哪些信息。你可能会先想到书名、作者、出版社、出版日期、页数、价格、主题或分类，以及 ISBN 号，而且你可能不用费太大劲就能再想出几个。你可以为描述一本书所需的每个参数分别指定变量，但理想情况下，你会希望有一个单一的数据类型，比如说 BOOK，能包含所有这些参数。我相信你听到这不会感到惊讶：这正是 struct 能为你做的事情。

### 定义 struct

我们还是以书为例，假设你只想在书的定义中包含书名、作者、出版社和出版年份。你可以声明一个结构体来容纳这些信息，如下所示：

```
struct BOOK
{
    char Title[80];
    char Author[80];
    char Publisher[80];
    int Year;
};
```

这并没有定义任何变量，但它实际上创建了一个新的变量类型，这个类型的名称是 BOOK。关键字 `struct` 将 BOOK 定义为这样的类型，而构成该类型对象的元素则在花括号内定义。请注意，struct 中定义每个元素的行都以分号结尾，而且右花括号之后也有一个分号。struct 的元素可以是任何类型，但不能是正在定义的 struct 本身的类型。例如，你不能在 BOOK 的结构定义中包含 BOOK 类型的元素。你可能会认为这是一种限制，但请注意，你可以包含一个指向 BOOK 类型变量的指针，稍后你就会看到。

上面定义中花括号内的元素 Title、Author、Publisher 和 Year 也可以称为 BOOK 结构体的成员或字段。每个 BOOK 类型的对象都包含成员 Title、Author、Publisher 和 Year。现在，你可以像创建任何其他类型的变量一样，以完全相同的方式创建 BOOK 类型的变量：

### 试一试

#### 使用 struct

现在再用一个控制台应用程序示例来进一步练习如何引用 struct 的成员。假设你要编写一个程序来处理院子里可能发现的一些物件，比如图 7-1 中经过专业景观美化设计的庭院里所展示的那些。

![](img/2359b0c604600c58fba3539c738a356e_367_0.png)

*图 7-1*

我任意地将坐标 0,0 指定给庭院的左上角。右下角的坐标为 100,120。因此，第一个坐标值是相对于左上角的水平位置度量，从左到右递增；第二个坐标值是从同一参考点测得的垂直位置度量，从上到下递增。

图 7-1 还显示了泳池和两个小屋相对于庭院左上角的位置。由于庭院、小屋和泳池都是矩形的，你可以定义一个 struct 类型来表示其中任何一个对象：

```
struct RECTANGLE
{
    int Left;                      // Top left point
    int Top;                       // coordinate pair

    int Right;                     // Bottom right point
    int Bottom;                    // coordinate pair
};
```

RECTANGLE 结构体类型的前两个成员对应于矩形左上角的坐标，后两个成员则对应于右下角的坐标。你可以在一个处理庭院中对象的简单示例中使用它，如下所示：

```
// Ex7_01.cpp
// Exercising structures in the yard
#include <iostream>
using std::cout;
using std::endl;

// Definition of a struct to represent rectangles
struct RECTANGLE
{
    int Left;                      // Top left point
    int Top;                       // coordinate pair

    int Right;                     // Bottom right point
    int Bottom;                    // coordinate pair
};

// Prototype of function to calculate the area of a rectangle
long Area(RECTANGLE& aRect);

// Prototype of a function to move a rectangle
void MoveRect(RECTANGLE& aRect, int x, int y);

int main(void)
{
    RECTANGLE Yard = { 0, 0, 100, 120 };
    RECTANGLE Pool = { 30, 40, 70, 80 };
    RECTANGLE Hut1, Hut2;

    Hut1.Left = 70;
    Hut1.Top = 10;
    Hut1.Right = Hut1.Left + 25;
    Hut1.Bottom = 30;

    Hut2 = Hut1;                   // Define Hut2 the same as Hut1
    MoveRect(Hut2, 10, 90);        // Now move it to the right position

    cout << endl
```

