
# Sams 每天一小时自学 C++，第八版 (ROBIN ROBIN LN's Library)

![](img/9780134449210.jpg)

![cover-image](img/9780134449210.jpg)

# 关于本电子书

EPUB 是一种开放的行业标准电子书格式。然而，不同阅读设备和应用程序对 EPUB 及其许多支持的支持不同。请使用您的设备或应用设置来按您的喜自定义显示。您可以自定义的设置通常包括字体、字体大小、单栏或双栏、横屏或竖屏模式，以及可以点击或触摸放大的图形。有关您的阅读设备或应用上的设置和功能的更多信息，请访问设备制造商的网站。

许多书籍包含编程代码或配置示例。为了优化这些元素的显示，请在单栏横屏模式下查看电子书，并将字体大小调整为最小设置。除了以重流文本格式显示代码和配置外，我们还包含了模仿印刷版显示效果的代码图像；因此，当重流格式可能会损害代码列表的显示时，您将看到“点击此处查看代码图像”链接。点击该链接查看高保真代码图像。要返回之前查看的页面，请点击设备或应用上的返回按钮。

Siddhartha Rao

![Image](img/pub.jpg)

800 East 96th Street, Indianapolis, Indiana 46240 USA

```
10: };

11:

12: int main()

13: {

14:     cout << "Displaying directions and their symbolic values" << endl;

15:     cout << "North: " << North << endl;

16:     cout << "South: " << South << endl;

17:     cout << "East: " << East << endl;

18:     cout << "West: " << West << endl;

19:

20:     CardinalDirections windDirection = South;

21:     cout << "Variable windDirection = " << windDirection << endl;

22:

23:     return 0;

24: }
```

输出 ![Image](img/arrow.jpg)

```
Displaying directions and their symbolic values
North: 25
South: 26
East: 27
West: 28
Variable windDirection = 26
```

### 提示

你可能想看一眼第 6 节中的列表 6.4 和 6.5。它们使用 `enum` 来枚举周的几天，并使用条件处理来告知用户选择的日期的名称。

### 使用 `#define` 定义常量

首先，如果你在编写新程序，请不要使用这种方法。本书分析使用 `#define` 定义常量的唯一理由是为了帮助你理解某些使用这种语法定义如 `pi` 等常量的旧程序：

```cpp
#define pi 3.14286
```

`#define` 是一个预处理器宏，这里的操作是将此后所有对 `pi` 的引用替换为 `3.14286` 以供编译器处理。注意，这是由预处理器执行的文本替换（即：非智能替换）。编译器既不知道也不关心所涉及常数的实际类型。

### 注意事项

通过 `#define` 使用预处理器定义常量已过时，不应再使用这种方法。

## 你不能作为变量或常量命名的关键字

某些单词被 C++ 保留了，你不能将它们作为变量名。这些关键字对 C++ 编译器有特殊含义。关键字包括 `if`、`while`、`for` 和 `main`。C++ 定义的关键字列表可以在表 3.2 以及附录 B 中的“C++ 关键字。”中找到。你的编译器可能还有额外的保留字，因此你应该检查其手册以获取完整列表。

![Image](img/03tab02.jpg)

**表 3.2** 主要 C++ 关键字

## 应该

**应该** 给变量起具有描述性的名称，即使这些名称很长。

**应该** 初始化变量，并使用列表初始化来避免收窄转换错误。

**应该** 确保变量名能够解释其用途。

**应该** 把自己置于尚未见过你代码的人的处地，思考这个名称对他们来说是否有意义。

**应该** 检查你的团队是否遵循了某些命名规范，并遵循这些规范。

### 不要

**不要** 给出过于短或仅包含一个字符的名称。

**不要** 使用只有你自己懂的奇特缩写词作为名称。

**不要** 使用 C++ 保留的关键字作为名称，因为这些将无法编译。

### 总结

在本节中，你学习了如何使用内存并在变量和常量中临时存储值。你学习了变量的大小由其类型决定，并且可以使用 `sizeof` 运算符来确定其大小。你了解了不同类型的变量，如 `bool`、`int` 等，以及它们被用于包含不同类型的数据。在有效的编程中，正确选择变量类型至关重要，选择一个与用途不符的过小的变量可能会导致回绕错误或溢出情况。你学习了关键字 `auto`，它让编译器根据变量的初始化值为你决定数据类型。

你还学习了不同类型的常量，以及通过使用 `const`、`constexpr` 和 `enum` 关键字使用其中最重要的常量。

### 问答

**Q 既然可以使用普通变量代替常量，为什么还要定义常量呢？**

**A** 常量，特别是使用 `const` 关键字声明的常量，是你告诉编译器某个变量的值是固定的且不允许更改的一种方式。因此，编译器会始终确保常量变量永远不会被赋予另一个值，即使另一个程序员接手了你的工作并无意中尝试覆盖该值。所以，在你知道变量值不应该改变时声明常量是一种良好的编程实践，并可以提高应用程序的质量。

**Q 为什么我应该初始化变量的值？**

**A** 如果你不进行初始化，你就不知道变量的初始值是什么。初始值只是为该变量预留的内存位置的内容。像这里这样的初始化：

```cpp
int myFavoriteNumber = 0;
```

会在变量 `myFavoriteNumber` 创建时，立即将你选择的初始值（在此例中为 0）写入为该变量预留的内存位置。在某些情况下，你会根据变量的值进行条件处理（通常检查是否非零）。如果没有初始化，这种逻辑无法可靠地运行，因为未赋值或未初始化的变量包含通常非零且随机的垃圾数据。

**Q 为什么 C++ 给我提供了使用 `short int`、`int` 和 `long int` 的选项？为什么不一直使用那种允许存储最大数值的整数类型？**

**A** C++ 是一种用于各种应用程序的编程语言，许多程序运行在计算能力或内存资源有限的设备上。简单的旧手机就是一个例子，其处理能力和可用内存都是有限的。在这种情况下，如果不需要高数值，通过选择正确的变量类型通常可以节省内存、提高速度或两者兼顾。如果你在普通的桌面电脑或高端智能手机上编程，选择一种整数类型而非另一种所带来的性能提升或节省的内存可能微乎其微，在某些情况下甚至不存在。

**Q 为什么我不应该频繁使用全局变量？难道它们在我的整个应用程序中都是可用的，这样我可以节省在函数间传递值时所花费的时间吗？**

**A** 全局变量可以全局读取和赋值。后者是问题所在，因为它们可以在全局范围内被更改。假设你正在与团队中的其他几个程序员合作一个项目。你将你的整数和其他变量声明为全局变量。如果你团队中的任何程序员在他们的代码中无意中更改了你的整数值——这甚至可能是在你使用的不同的 `.CPP` 文件中——你代码的可靠性就会受到影响。因此，节省几秒钟不应该是标准，你不应该盲目使用全局变量，以确保你代码的稳定性。

**Q C++ 给我提供了使用应该包含正值和零的无符号整数的选项。如果我减少零值会发生什么？**

**A** 你会看到回绕现象。对包含 0 的无符号整数减 1 意味着它绕到了它可以持有的最大值！`unsigned short` 可以包含 0 到 65535 的值。所以，声明一个 `unsigned short` 并对其减法看看意外的结果：

```cpp
unsigned short myShortInt = 0; // 初始值
myShortInt = myShortInt - 1; // 减 1
std::cout << myShortInt << std::endl; // 输出: 65535!
```

注意，这不是 `unsigned short` 的问题，而是你使用它的方式。当规范允许负值时，不应使用无符号整数（或短型、长型）。如果 `myShortInt` 用于访问内存位置的索引，你的应用程序极可能会访问一个外部位置并崩溃！

### 练习

工作练习提供了问答题，以帮助你巩固对涵盖内容的理解，并提供了练习题以让你获得使用所学知识的经验。在查看附录 E 中的答案之前，请尝试回答问答和练习题，并在继续下一节课程之前确保你已经理解了这些答案。

### 问答题

**1.** 有符号整数和无符号整数之间的区别是什么？

**2.** 为什么不应该使用 `#define` 来声明常量？

**3.** 你为什么需要初始化变量？

**4.** 考虑下面的 `enum`。`Queen` 的值是多少？

```cpp
enum YourCards {Ace, Jack, Queen, King};
```

**5.** 这个变量名有什么问题？

```cpp
int Integer = 0;
```

### 练习题

**1.** 修改练习题 4 中的 `enum YourCards`，以证明 `Queen` 的值可以是 45。

**2.** 编写一个程序，证明无符号整数和普通整数的大小是相同的，且两者的尺寸都小于长整型（long integer）。

**3.** 编写一个程序，根据用户输入的半径计算圆的面积和周长。

**4.** 在练习 3 中，如果将面积和周长存储在整数中，输出会有什么不同？

**5.** 找错（BUGBUSTERS）：以下初始化中有什么错误：

```cpp
auto Integer;
```

# 第 4 节：数组与字符串的管理

在之前的课程中，你声明了用于包含单个 `int`、`char` 或 `string` 的变量（仅举几个例子）。然而，你可能想要声明一个对象集合，例如 20 个 `int` 或一个用于存储名字的字符串。

在本节中，你将学习到：

- ![Image](img/square.jpg) 什么是数组以及如何声明和使用它们
- ![Image](img/square.jpg) 什么是字符串以及如何使用字符数组来创建它们
- ![Image](img/square.jpg) `std::string` 的简要介绍

## 什么是数组？

`array`（数组）的字典定义非常接近我们想要理解的概念。根据韦氏-韦斯特词典（Merriam Webster），数组是“形成完整单元的元素组，例如太阳能电池板数组”。

以下是数组的特征：

- ![Image](img/square.jpg) 数组是元素的集合。
- ![Image](img/square.jpg) 数组中包含的所有元素都是相同类型的。
- ![Image](img/square.jpg) 该集合形成了一个完整的集合。

在 C++ 中，数组允许你以顺序且有序的方式在内存中存储某种类型的数据元素。

### 数组的必要性

想象你正在编写一个程序，用户可以输入五个整数，你将它们返回给用户。一种方法是让你的程序声明五个独立的唯一整数变量，并使用它们来存储和显示值。声明看起来如下：

点击此处查看代码图像

```cpp
int firstNumber = 0;
int secondNumber = 0;
int thirdNumber = 0;
int fourthNumber = 0;
int fifthNumber = 0;
```

如果你的用户希望程序在稍后的阶段存储并显示 500 个整数，你需要使用上述系统声明 500 个这样的整数。在耐心和时间充足的情况下，这仍然是可以行的。但是，想象一下用户要求你支持 500,000 个整数而不是 5 个——你会怎么做？

你应该正确且聪明地这样做，从声明一个五个整数的数组开始，每个整数初始化为零，如下：

```cpp
int myNumbers [5] = {0};
```

因此，如果你被要求支持 500,000 个整数，你的数组会非常迅速扩展，如下：

点击此处查看代码图像

```cpp
int manyNumbers [500000] = {0};
```

五个字符的数组定义为：

```cpp
char myCharacters [5];
```

此类数组被称为 `static arrays`（静态数组），因为它们包含的元素数量以及数组消耗的内是在编译时就固定的。

### 声明和初始化静态数组

在前面的代码行中，你声明了一个名为 `myNumbers` 的数组，它包含五个 `int` 类型（即整数）的元素——这些都初始化为值 0。因此，C++ 中的数组声明遵循简单的语法：

点击此处查看代码图像

```cpp
ElementType ArrayName [constant_number of elements] = {optional initial values};
```

你甚至可以逐元素地声明一个数组并初始化其内容，就像这个整数数组，五个整数中的每一个都分别初始化为五个不同的整数值：

点击此处查看代码图像

```cpp
int myNumbers [5] = {34, 56, -21, 5002, 365};
```

你可以将数组中的所有元素都初始化为零（编译器为数值类型提供的默认值），如下：

点击此处查看代码图像

```cpp
int myNumbers [5] = {}; // 将所有整数初始化为 0
```

你也可以部分初始化数组中的元素，如下：

点击此处查看代码图像

```cpp
int myNumbers [5] = {34, 56};
// 将前两个元素初始化为 34 和 56，其余初始化为 0
```

你可以定义数组的长度（即元素的数量），如下：

点击此处查看代码图像

```cpp
const int ARRAY_LENGTH = 5;
int myNumbers [ARRAY_LENGTH] = {34, 56, -21, 5002, 365};
```

如果你知道初始值，可以省略数组的长度，如下：

点击此处查看代码图像

```cpp
int myNumbers[] = {34, 56, -21, 5002, 365};
```

当要求访问索引为 `N` 的元素时，编译器使用第一个元素（位于索引 0）的内存地址作为起点，然后通过添加计算为 `N*sizeof(element)` 的偏移量来跳过 `N` 个元素，到达包含第 (N+1) 个元素的地址。C++ 编译器不会检查该索引是否在数组实际定义的边界内。你可以尝试在一个只有 10 个元素的数组中获取索引为 1001 的元素，这会使你的程序的安全性和稳定性面临风险。确保数组不越界访问的完全在于程序员。

### 警告

访问越界数组会导致不可预知的行为。在许多情况下，这会导致你的程序崩溃。应该尽一切努力避免访问越界数组。

Listing 4.1 展示了如何声明一个整数数组，初始化其元素为整数值，并访问它们将它们显示在屏幕上。

**列表 4.1** 声明整数数组并访问其元素

点击此处查看代码图像

```cpp
0:  #include <iostream>
1:
2:  using namespace std;
3:
4:  int main ()
5:  {
6:    int myNumbers [5] = {34, 56, -21, 5002, 365};
7:
8:    cout << "First element at index  0: " << myNumbers [0] << endl;
9:    cout << "Second element at index  1: " << myNumbers [1] << endl;
10:     cout << "Third element at index  2: " << myNumbers [2] << endl;
11:     cout << "Fourth element at index  3: " << myNumbers [3] << endl;
12:     cout << "Fifth element at index  4: " << myNumbers [4] << endl;
13:
14:     return 0;
15:  }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
First element at index  0: 34
Second element at index  1: 56
Third element at index  2: -21
Fourth element at index  3: 5002
Fifth element at index  4: 365
```

分析 ![Image](img/arrow.jpg)

第 6 行声明了一个包含五个整数的数组，并为每个元素指定了初始值。后续行简单地使用 `cout` 和数组变量 `myNumbers` 相应的索引来显示这些整数。

### 注意

为了让你熟悉用于访问数组元素的零基索引概念，我们从 Listing 4.1 及之后开始对代码行进行编号，第一行编号为 Line 0。

## 修改存储在数组中的数据

在之前的代码列表中，你没有向数组中输入用户定义的数据。为该数组中的元素分配整数的语法与为整数变量分配整数值非常相似。

例如，给整数赋值值 2016 如下：

```cpp
int thisYear;
thisYear = 2016;
```

给你的数组中的第四个元素赋值值 2016 如下：

点击此处查看代码图像

```cpp
myNumbers [3] = 2016; // Assign 2016 to the fourth element
```



# 为数组元素赋值

`Listing 4.2` 展示了在声明数组长度时使用常量，以及如何在程序执行期间为单个数组元素赋值。

**列表 4.2** 为数组中的元素赋值

```cpp
0: #include <iostream>
1: using namespace std;
2: constexpr int Square(int number) { return number*number; }
3:
4: int main()
5: {
6:   const int ARRAY_LENGTH = 5;
7:
8:   // 使用 const 化的 5 个整数数组
9:   int myNumbers [ARRAY_LENGTH] = {5, 10, 0, -1, 20};
10:  // 使用 constexpr 处理 25 个整数数组
11:  int moreNumbers [Square(ARRAY_LENGTH)];
12:   cout << "Enter index of the element to be changed: ";
13:   int elementIndex = 0;
14:   cin >> elementIndex;
15:
16:   cout << "Enter new value: ";
17:   int newValue = 0;
18:   cin >> newValue;
19:
20:   myNumbers[elementIndex] = newValue;
21:   moreNumbers[elementIndex] = newValue;
22:
23:   cout << "Element " << elementIndex << " in myNumbers is: ";
24:   cout << myNumbers[elementIndex] << endl;
25:
26:   cout << "Element " << elementIndex << " in moreNumbers is: ";
27:   cout << moreNumbers[elementIndex] << endl;
28:
29:   return 0;
30: }
```

输出

```
Enter index of the element to be changed: 3
Enter new value: 101
Element 3 in myNumbers is: 101
Element 3 in moreNumbers is: 101
```

## 分析

数组长度需要是一个常量。这可以通过第 9 行使用的常量`ARRAY_LENGTH`或第 12 行使用的常量表达式`Square()`来指定。因此，数组`myNumbers`被声明长度为 5，而数组`moreNumbers`为 25。第 14-20 行要求用户输入要修改的元素索引以及要存储在该索引的新值。第 22 和 23 行演示了根据索引修改数组中的特定元素。第 26-29 行演示了根据索引访问数组元素。注意，修改索引为 3 的元素实际上修改的是数组中的第四个元素，因为索引是从零开始的。你必须习惯。

### 注意

许多初学者 C++ 程序员会在五个整数的数组中为索引 5 赋值。注意，这超出了数组的边界，因为编译后的代码尝试访问数组边界之外的第六个元素。

这种错误被称为“栅栏错误”（`fence-post error`）。它的名字是因为建造栅栏所需的柱子数量比栅栏间隔的数量多。

### 警告

`Listing 4.2` 中缺少了基础内容：它没有检查用户输入的索引是否在数组边界内。之前的程序应该验证`elementIndex`对于`myNumbers`是否在 0 到 4 之间，对于`moreNumbers`是否在 0 到 24 之间，并拒绝所有其他输入。这种缺失的检查允许用户赋值并访问数组边界之外的值。这可能导致应用程序崩溃，在极端的情况下会导致系统崩溃。

执行检查在 Lesson 6“控制程序流”中解释。

## 使用循环访问数组元素

当顺序处理数组及其元素时，你应该使用循环来访问它们（换句话说是迭代）。参见 Lesson 6，特别是 `Listing 6.10`，以快速学习如何使用`for`循环高效地插入或访问数组中的元素。

### 应当

- **应当** 始终初始化数组，否则它们将包含垃圾值。
- **应当** 始终确保你的数组在定义的边界内使用。

### 不要

- **不要** 永远不要在包含 N 个元素的数组中使用索引 N 访问第 N 个元素。请使用索引 (N–1)。
- **不要** 忘记数组中的第一个元素是使用索引 0 访问的。

## 多维数组

我们目前为止看到的数组类似于书架上的书。较长的书架可以放更多的书，较短的书架书较少。也就是说，书架的长度是定义书架容量的唯一维度，因此是一维的。现在，如果我们使用数组来模拟太阳能板阵列会怎样，如图 4.3 所示。

**图 4.3** 屋顶上的太阳能板阵列。

如你在图 4.3 中所示，六块太阳能板以两行三列的二维排列方式放置。从一个角度来看，你可以将这种排列看作是一个包含两个元素的数组，每个元素本身又是一个包含三个面板的数组——换句话说，这是一个数组的数组。在 C++ 中，你可以模拟二维数组，但并不局限于二维。根据你的需求和应用程序的性质，你也可以在内存中模拟多维数组。

## 多维数组的声明与初始化

C++ 允许你通过指定每个维度上保留的元素数量来声明多维数组。因此，表示图 4.3 中太阳能板的二维整数数组如下：

```cpp
int solarPanels [2][3];
```

注意，在图 4.3 中，你还为太阳能阵列中的六块面板分配了一个从 0 到 5 的 ID。如果你按照相同的顺序初始化该整数数组，它看起来像所示：

```cpp
int solarPanels [2][3] = {{0, 1, 2}, {3, 4, 5}};
```

如你所见，使用的初始化语法实际上与初始化两个一维数组的相似。一个包含三行三列的数组看起来如下：

```cpp
int threeRowsThreeColumns [3][3] = {{-501, 206, 2016}, {989, 101, 206}, {303, 456, 596}};
```

***

**注意**

尽管 C++ 允许我们模拟多维数组，但包含数组的内存是一维的。因此，编译器将多维数组映射到内存空间中，该空间只向一个方向扩展。

如果你愿意，你也可以像如下所示初始化名为`solarPanels`的数组，它在相应元素中仍包含相同的值：

```cpp
int solarPanels [2][3] = {0, 1, 2, 3, 4, 5};
```

然而，前面的方法提供了一个更好的例子，因为它更容易将多维数组想象并理解为“数组的数组”。

***

## 访问多维数组中的元素

将多维数组想象成一个由数组元素组成的数组。因此，在处理一个包含三行三列且每列都包含整数的二维数组时，将其视觉化为处理一个包含三个元素的数组，其中每个元素都是一个包含三个整数的数组。

当你需要访问数组中的某个整数时，你需要使用第一个下标来定位该整数所在的数组，使用第二个下标来定位数组中的该整数。考虑这个数组：

```cpp
int threeRowsThreeColumns [3][3] = {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
```

它的初始化方式可以让你视觉化出三个数组，每个数组包含三个整数。在这里，值为`205`的整数元素位于位置`[0][1]`。值为`456`的元素位于位置`[2][1]`。列表 4.3 解释了如何访问此数组中的整数元素。

**列表 4.3** 访问多维数组中的元素

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     int threeRowsThreeColumns [3][3] = \
6:     {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
7:
8:     cout << "Row  0: " << threeRowsThreeColumns [0][0] << " " \
9:                          << threeRowsThreeColumns [0][1] << " " \
10:                            << threeRowsThreeColumns [0][2] << endl;
11:
12:
13:    cout << "Row  1: " << threeRowsThreeColumns [1][0] << " " \
14:                          << threeRowsThreeColumns [1][1] << " " \
15:                            << threeRowsThreeColumns [1][2] << endl;
16:
17:    cout << "Row  2: " << threeRowsThreeColumns [2][0] << " " \
18:                          << threeRowsThreeColumns [2][1] << " " \
19:                            << threeRowsThreeColumns [2][2] << endl;
20:
21:    return 0;
22: }
```

输出

```
Row  0: -501 205 2016
Row  1: 989 101 206
Row  2: 303 456 596
```

***

如你所见，在图 4.3 中，六块太阳能板以两行三列的二维排列方式放置。从一个角度来看，你可以将这种排列看作是一个包含两个元素的数组，每个元素本身又是一个包含三个面板的数组——换句话说，这是一个数组的数组。在 C++ 中，你可以模拟二维数组，但并不局限于二维。根据你的需求和应用程序的性质，你也可以在内存中模拟多维数组。

## 多维数组的声明与初始化

C++ 允许你通过指定每个维度上保留的元素数量来声明多维数组。因此，表示图 4.3 中太阳能板的二维整数数组如下：

```cpp
int solarPanels [2][3];
```

注意，在图 4.3 中，你还为太阳能阵列中的六块面板分配了一个从 0 到 5 的 ID。如果你按照相同的顺序初始化该整数数组，它看起来像所示：

```cpp
int solarPanels [2][3] = {{0, 1, 2}, {3, 4, 5}};
```

如你所见，使用的初始化语法实际上与初始化两个一维数组的相似。一个包含三行三列的数组看起来如下：

```cpp
int threeRowsThreeColumns [3][3] = {{-501, 206, 2016}, {989, 101, 206}, {303, 456, 596}};
```

***

**注意**

尽管 C++ 允许我们模拟多维数组，但包含数组的内存是一维的。因此，编译器将多维数组映射到内存空间中，该空间只向一个方向扩展。

如果你愿意，你也可以像如下所示初始化名为`solarPanels`的数组，它在相应元素中仍包含相同的值：

```cpp
int solarPanels [2][3] = {0, 1, 2, 3, 4, 5};
```

然而，前面的方法提供了一个更好的例子，因为它更容易将多维数组想象并理解为“数组的数组”。

***

## 访问多维数组中的元素

将多维数组想象成一个由数组元素组成的数组。因此，在处理一个包含三行三列且每列都包含整数的二维数组时，将其视觉化为处理一个包含三个元素的数组，其中每个元素都是一个包含三个整数的数组。

当你需要访问数组中的某个整数时，你需要使用第一个下标来定位该整数所在的数组，使用第二个下标来定位数组中的该整数。考虑这个数组：

```cpp
int threeRowsThreeColumns [3][3] = {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
```

它的初始化方式可以让你视觉化出三个数组，每个数组包含三个整数。在这里，值为`205`的整数元素位于位置`[0][1]`。值为`456`的元素位于位置`[2][1]`。列表 4.3 解释了如何访问此数组中的整数元素。

**列表 4.3** 访问多维数组中的元素

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     int threeRowsThreeColumns [3][3] = \
6:     {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
7:
8:     cout << "Row  0: " << threeRowsThreeColumns [0][0] << " " \
9:                          << threeRowsThreeColumns [0][1] << " " \
10:                            << threeRowsThreeColumns [0][2] << endl;
11:
12:
13:    cout << "Row  1: " << threeRowsThreeColumns [1][0] << " " \
14:                          << threeRowsThreeColumns [1][1] << " " \
15:                            << threeRowsThreeColumns [1][2] << endl;
16:
17:    cout << "Row  2: " << threeRowsThreeColumns [2][0] << " " \
18:                          << threeRowsThreeColumns [2][1] << " " \
19:                            << threeRowsThreeColumns [2][2] << endl;
20:
21:    return 0;
22: }
```

输出

```
Row  0: -501 205 2016
Row  1: 989 101 206
Row  2: 303 456 596
```

***

**注意**

尽管 C++ 允许我们模拟多维数组，但包含数组的内存是一维的。因此，编译器将多维数组映射到内存空间中，该空间只向一个方向扩展。

如果你愿意，你也可以像如下所示初始化名为`solarPanels`的数组，它在相应元素中仍包含相同的值：

```cpp
int solarPanels [2][3] = {0, 1, 2, 3, 4, 5};
```

然而，前面的方法提供了一个更好的例子，因为它更容易将多维数组想象并理解为“数组的数组”。

***

## 访问多维数组中的元素

将多维数组想象成一个由数组元素组成的数组。因此，在处理一个包含三行三列且每列都包含整数的二维数组时，将其视觉化为处理一个包含三个元素的数组，其中每个元素都是一个包含三个整数的数组。

当你需要访问数组中的某个整数时，你需要使用第一个下标来定位该整数所在的数组，使用第二个下标来定位数组中的该整数。考虑这个数组：

```cpp
int threeRowsThreeColumns [3][3] = {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
```

它的初始化方式可以让你视觉化出三个数组，每个数组包含三个整数。在这里，值为`205`的整数元素位于位置`[0][1]`。值为`456`的元素位于位置`[2][1]`。列表 4.3 解释了如何访问此数组中的整数元素。

**列表 4.3** 访问多维数组中的元素

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     int threeRowsThreeColumns [3][3] = \
6:     {{-501, 205, 2016}, {989, 101, 206}, {303, 456, 596}};
7:
8:     cout << "Row  0: " << threeRowsThreeColumns [0][0] << " " \
9:                          << threeRowsThreeColumns [0][1] << " " \
10:                            << threeRowsThreeColumns [0][2] << endl;
11:
12:
13:    cout << "Row  1: " << threeRowsThreeColumns [1][0] << " " \
14:                          << threeRowsThreeColumns [1][1] << " " \
15:                            << threeRowsThreeColumns [1][2] << endl;
16:
17:    cout << "Row  2: " << threeRowsThreeColumns [2][0] << " " \
18:                          << threeRowsThreeColumns [2][1] << " " \
19:                            << threeRowsThreeColumns [2][2] << endl;
20:
21:    return 0;
22: }
```

输出

```
Row  0: -501 205 2016
Row  1: 989 101 206
Row  2: 303 456 596
```



13:    cout << "Row  1: " << threeRowsThreeColumns [1][0] << " " \

14:                          << threeRowsThreeColumns [1][1] << " " \

15:                            << threeRowsThreeColumns [1][2] << endl;

16:

17:    cout << "Row  2: " << threeRowsThreeColumns [2][0] << " " "\

18:                          << threeRowsThreeColumns [2][1] << " " \

19:                            << threeRowsThreeColumns [2][2] << endl;

20:

21:    return 0;

22: }

```

***

## 动态数组

考虑一个存储医疗记录的应用程序。程序员没有很好的方法知道应用程序可能需要的记录上限。在这种情况下，使用动态数组来根据需求调整内存是更安全的。

C++ 以`std::vector`的形式提供了方便且易于使用的动态数组，如列表 4.4 所示。

**列表 4.4** 创建动态整数数组并动态插入值

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <vector>
2:
3: using namespace std;
4:
5: int main()
6: {
7:     vector<int> dynArray (3); // 动态整数数组
8:
9:     dynArray[0] = 365;
10:    dynArray[1] = -421;
11:    dynArray[2]= 789;
12:
13:    cout << "Number of integers in array: " << dynArray.size() << endl;
14:
15:    cout << "Enter another element to insert" << endl;
16:    int newValue = 0;
17:    cin >> newValue;
18:    dynArray.push_back(newValue);
19:
20:    cout << "Number of integers in array: " << dynArray.size() << endl;
21:    cout << "Last element in array: ";
22:    cout << dynArray[dynArray.size() - 1] << endl;
23:    return 0;
24:
25: }
```

不要担心列表 4.4 中的语法，因为还没有解释`vector`和模板。尝试观察输出并将其与代码联系起来。根据输出结果，数组的初始大小为 3，这与第 7 行中数组的声明（`std::vector`）一致。在了解此点的，你仍然在第 15 行要求用户输入第四个数字，有趣的是，你能够在第 18 行使用`push_back()`将此数字插入数组末尾。`vector`会动态调整自身大小以容纳更多数据。这从数组大小增加到 4 可以看出。注意使用熟悉的静态数组语法来访问`vector`中的数据。第 22 行使用从 0 开始的索引访问最后一个元素（根据运行时计算的位置，无论它在哪里），最后一个元素位于索引“`size() – 1`”。`size()`是返回`vector`中包含的元素（整数）总数的函数。

***

### 注意

要使用动态数组类`std::vector`，你需要包含头文件`vector`，这在列表 4.4 的第 1 行中也有显示。

```cpp
#include <vector>
```

将在第 17 节中详细介绍矢量。

***

### C 风格字符串

C 风格字符串是字符数组的一种特殊情况。你已经在代码中以字符串字面量的形式看到了一些 C 风格字符串的示例：

```cpp
std::cout << "Hello World";
```

等等于使用数组声明：

点击查看代码图像

```cpp
char sayHello[] = {'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '\0'};
std::cout << sayHello << std::endl;
```

注意数组中的最后一个字符是空字符`\0`。这也被称为字符串终止符，因为它告诉编译器字符串已结束。此类 C 风格字符串是字符数组的特殊情况，因为最后一个字符始终位于空终止符`\0`之前。当你在代码中嵌入字符串字面量时，编译器会在其后添加一个`\0`。

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。

***

### 注意

`'\0'`对你来说可能像两个字符，它们确实是使用键盘输入的两个字符。然而，反斜杠是一个编译器理解的特殊转义代码，`\0`意味着空——也就是说，它要求编译器在该处插入一个空值或零。

你不能直接写`'0'`，因为那会被接受为字符零，其非零 ASCII 码为 48。

请检查附录 D 中的表格“ASCII 码，”以查看此值和其他 ASCII 值。

***

**列表 4.5** 分析 C 风格字符串中的空终止符

点击查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     char sayHello[] = {'H','e','l','l','o',' ','W','o','r','l','d','\0'};
6:     cout << sayHello << endl;
7:     cout << "Size of array: " << sizeof(sayHello) << endl;
8:
9:     cout << "Replacing space with null" << endl;
10:     sayHello[5] = '\0';
11:     cout << sayHello << endl;
12:     cout << "Size of array: " << sizeof(sayHello) << endl;
13:
14:     return 0;
15: }
```

***

输出 ![Image](img/arrow.jpg)

点击查看代码图像

Hello World

Size of array: 12

Replacing space with null

Hello

Size of array: 12

Analysis ![Image](img/arrow.jpg)

第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

### 分析

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

### 警示

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

### 警示

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

### 警示

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

如果你在数组中间任何地方插入`'\0'`，它不会改变数组的大小；它仅意味着使用该数组作为输入进行字符串处理会在该点停止。列表 4.5 演示了这一点。第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

（代码块部分略）

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     char sayHello[] = {'H','e','l','l','o',' ','W','o','r','l','d','\0'};
6:     cout << sayHello << endl;
7:     cout << "Size of array: " << sizeof(sayHello) << endl;
8:
9:     cout << "Replacing space with null" << endl;
10:     sayHello[5] = '\0';
11:     cout << sayHello << endl;
12:     cout << "Size of array: " << sizeof(sayHello) << endl;
13:
14:     return 0;
15: }
```

第 10 行是我们用空终止符替换“Hello World”中空格的地方。注意，数组现在有两个空终止符，但是第一个导致第 11 行显示字符串的那个。

`size()`是返回`vector`中包含的元素（整数）总数的函数。

```cpp
11:    string firstLine;
12:    getline(cin, firstLine);
14:    cout << "Enter another: " << endl;
15:    string secondLine;
16:    getline(cin, secondLine);
18:    cout << "Result of concatenation: " << endl;
19:    string concatString = firstLine + " " + secondLine;
20:    cout << concatString << endl;
22:    cout << "Copy of concatenated string: " << endl;
23:    string aCopy;
24:    aCopy = concatString;
25:    cout << aCopy << endl;
27:    cout << "Length of concat string: " << concatString.length() << endl;
29:    return 0;
30: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

Hello `std::string`!

输入一行文本：

I love

输入另一行：

C++ strings

连接结果：

I love C++ strings

连接字符串的副本：

I love C++ strings

连接字符串的长度：18

分析 ![Image](img/arrow.jpg)

尝试理解输出并与代码中的各种元素相关起来。在这个阶段，不要让新的语法特征困扰你。程序开始显示一个在第 7 行初始化为`“Hello std::string”`的字符串。然后它要求用户输入两行文本，这些存储在第 12 行和第 16 行的变量`firstLine`和`secondLine`中。实际的连接非常简单，看起来就像第 19 行中的算术加法，其中在第一行后面还添加了一个空格。复制操作是第 24 行的一个简单赋值操作。字符串的长度通过在第 27 行对其调用`length()`方法来确定。

注意

要使用 C++ 字符串，你需要包含头文件`string:`：

```cpp
#include <string>
```

这在列表 4.7 的第 1 行也是可见的。

要详细学习`std::string`的各种函数，请快速查看第 16 节，“STL `string`类”。由于你还没有学习过类和模板，请忽略该课程中看起来陌生的部分，并专注于理解示例的要点。

### 总结

本节向你教授了数组的基础知识、它们是什么以及它们可以用什么地方。你学习了如何声明它们、初始化它们、访问数组中的元素以及向数组中的元素写入值。你学习了不超出数组边界是多么重要。这被称为`buffer overflow`（缓冲区溢出），在用于索引元素之前对输入进行检查有助于确保不会越界数组的限制。

动态数组是指程序员不需要在编译时固定数组最大长度的数组，在实际量少于预期最大值的情况下，它们允许更好的内存管理。

你还学习了 C 风格字符串是`char`数组的一种特殊情况，其中字符串的结束由空终止字符`'\0'`标记。更重要的是，你学习了 C++ 在`std::string`中提供了一个更好的选择，它提供了方便的实用函数，让你能够确定长度、进行连接并执行类似的操作。

### 问答

**Q 为什么要费劲初始化静态数组的元素？**

**A** 除非初始化，否则与任何其他类型的变量不同，数组包含垃圾数据和不可预测的值，因为该位置的内在此之前的操作后没有被触动。初始化数组可以确保其中的信息具有明确且可预测的初始状态。

**Q 你是否需要由于第一个问题中提到的原因初始化动态数组的元素？**

**A** 实际上，不需要。动态数组是非常智能的数组。除非与应用程序相关的特定需要在数组中具有某些初始值，否则数组中的元素不需要初始化为默认值。

**Q 如果有选择，你会使用需要空终止符的 C 风格字符串吗？**

**A** 会，但除非有人拿枪指你的头。C++ `std::string`安全得多，提供的特性应该让任何优秀的程序员都远离使用 C 风格字符串。

**Q 字符串的长度包含末尾的空终止符吗？**

**A** 不包含。字符串“Hello World”的长度为 11，包括空格但不包含结尾的空字符。

## 工作坊

工作坊提供了测验题帮助你巩固材料，并提供了练习让你获得使用所学知识的经验。

### 测验

**1.**](#05.html_ch04ans01) 该数组中第一个和最后一个元素的索引是多少？`char`数组？

**2.**](#05.html_ch04ans02) 如果你需要输入字符串，你会使用 C 风格字符串吗？

**3.**](#05.html_ch04ans03) 在编译器看来，`'\0'`中有多少个字符？

**4.**](#05.html_ch04ans04) 你忘记用空终止符结束你的 C 风格字符串。当你使用它时会发生什么？

**5.**](#05.html_ch04ans05) 查看列表 4.4 中 vector 的声明并尝试组合动态数组。

### 练习

**1.**](#05.html_ch04ex01) 声明一个表示棋盘格格的数组；其类型为定义占据这些格子的枚举`enum`。

提示：`enum`将包含常量（`Rook`、`Bishop`等），从而限制了元素可以持值的范围。不要忘记单元格也可以是空的！

**2.**](#05.html_ch04ex02) **错误查找**：这段代码片段哪里有问题？

```cpp
int myNumbers[5] = {0};
myNumbers[5] = 450;
```

**3.**](#05.html_ch04ex03) **错误查找**：这段代码片段哪里有问题？

```cpp
int myNumbers[5];
cout << myNumbers[3];
```

使用`cout`的语句会在屏幕上的控制台上显示文本。C++ 中的所有语句都以分号（`;`）结束，分号定义了语句的边界。这类似于你在英语句子末尾添加的句号（`.`）。下一条语句可以紧跟在分号之后立即开始，但为了方便和可读性，你通常会将连续的语句写在连续的行上。换句话说，这实际上是同一行中的两个语句：

点击此处查看代码图像

```
cout << "Hello World" << endl; cout << "Another hello" << endl;
```

***

### 注意
空白字符通常对编译器是不可见的。这包括空格、制表符、换行符、回车符等。然而，字符串字面量内的空白字符会对输出产生影响。

***

以下内容是无效的：

点击此处查看代码图像

```cpp
cout << "Hello

      World" << endl; // 字符串字面量内不允许换行
```

此类代码通常会导致错误，指示编译器在第一行缺少闭合引号（`"`）和结束语句的分号（`;`）。如果由于某些原因你需要将一个语句跨越两行，你可以在末尾插入反斜杠（`\`）来实现：

点击此处查看代码图像

```cpp
cout << "Hello \

      World" << endl; // 分拆成两行是可以的
```

将上述语句分两行的另一种方法是编写两个字符串字面量而不是一个：

点击此处查看代码图像

```cpp
cout << "Hello "
```



`"World" << endl;` // 两个字符串字面量也可以的

在前面的示例中，编译器会注意到两个相邻的字符串字面量并为你合并它们。

### 注意

当你有长文本元素或由许多变量组成的复杂表达式时，这使得语句长度远超大多数显示器允许的范围，将语句拆分为多行是有用的。

### 复合语句或块

当你将语句分组在花括号 `{...}` 内部时，你就创建了一个复合语句或块。

```cpp
{
    int daysInYear = 365;
    cout << "Block contains an int and a cout statement" << endl;
}
```

块通常将许多语句分组，以表示它们属于整体。在编写条件`if`语句或循环时，块特别有用，这些内容将在第 6 节中的“控制程序流”中解释。

### 使用运算符

运算符是 C++ 提供的工具，让你能够对数据进行操作、转换、处理，并可能在此基础上做出决策。

### 赋值运算符 (`=`)

赋值运算符是你已经在书中直觉地使用的一种：

```cpp
int daysInYear = 365;
```

前面的语句使用赋值运算符将整数初始化为 365。赋值运算符将左侧操作数（通俗地称为 l 值）包含的值替换为右侧的值（称为 r 值）。

### 理解 L 值和 R 值

L 值通常指内存中的位置。前一个示例中如`daysInYear`的变量实际上是内存位置的句柄，是一个 l 值。相反，r 值可以是内存位置的具体内容。

因此，所有的 l 值都可以是 r 值，但不是所有的 r 值都可以 l 值。为了更好地理解它，请看下面的示例，它逻辑上不通，因此无法编译：

```cpp
365 = daysInYear;
```

### 加法 (`+`)、减法 (`-`)、乘法 (`*`)、除法 (`/`) 和取模 (`%`) 运算符

你可以通过使用`+`加法、`-`减法、`*`乘法、`/`除法以及`%`取模运算在两个操作数之间执行算术运算：

```cpp
int num1 = 22;
int num2 = 5;
int addNums = num1 + num2; // 27
int subtractNums = num1 – num2; // 17
int multiplyNums = num1 * num2; // 110
int divideNums = num1 / num2; // 4
int moduloNums = num1 % num2; // 2
```

注意，除法运算符 (`/`) 返回两个操作数之间的除法结果。然而，在整数的情况下，结果不包含小数，因为根据定义整数不能包含小数数据。取模运算符 (`%`) 返回除法运算符的余数，且它只适用于整数值。列表 5.1 是一个简单的程序，演示了如何对用户输入的两个数字执行算术函数的应用。

**列表 5.1** 在用户输入的整数上演示算术运算符

```cpp
  0: #include <iostream>
  1: using namespace std;
  2:
  3: int main()
  4: {
  5:     cout << "Enter two integers:" << endl;
  6:     int num1, num2;
  7:     cin >> num1 >> num2;
  8:     cout << "Sum: " << num1 + num2 << endl;
  9:     cout << "Difference: " << num1 - num2 << endl;
  10:    cout << "Product: " << num1 * num2 << endl;
  11:    cout << "Quotient: " << num1 / num2 << endl;
  12:    cout << "Remainder: " << num1 % num2 << endl;
  13:    return 0;
  14: }
```

注意除法运算符 (`/`) 返回两个操作数之间的除法结果。然而，在整数的情况下，结果不包含小数，因为根据定义整数不能包含小数数据。取模运算符 (`%`) 返回除法运算符的余数，且它只适用于整数值。列表 5.1 是一个简单的程序，演示了如何对用户输入的两个数字执行算术函数的应用。

```cpp
  0: #include <iostream>
  1: using namespace std;
  2:
  3: int main()
  4: {
  5:     cout << "Enter two integers:" << endl;
  6:     int num1, num2;
  7:     cin >> num1 >> num2;
  8:     cout << "Sum: " << num1 + num2 << endl;
  9:     cout << "Difference: " << num1 - num2 << endl;
  10:    cout << "Product: " << num1 * num2 << endl;
  11:    cout << "Quotient: " << num1 / num2 << endl;
  12:    cout << "Remainder: " << num1 % num2 << endl;
  13:    return 0;
  14: }
```

```cpp
  0: #include <iostream>
  1: using namespace std;
  2:
  3: int main()
  4: {
  5:     int startValue = 101;
```

```cpp
cout << "Start value of integer being operated: " << startValue << endl;

int postfixIncrement = startValue++;
cout << "Result of Postfix Increment = " << postfixIncrement << endl;
cout << "After Postfix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixIncrement = ++startValue;
cout << "Result of Prefix Increment = " << prefixIncrement << endl;
cout << "After Prefix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int postfixDecrement = startValue--;
cout << "Result of Postfix Decrement = " << postfixDecrement << endl;
cout << "After Postfix Decrement, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixDecrement = --startValue;
cout << "Result of Prefix Decrement = " << prefixDecrement << endl;
cout << "After Prefix Decrement, startValue = " << startValue << endl;

return 0;
```

Output ![Image](img/arrow.jpg)

此处点击查看代码图像

被操作整数的起始值: 101
Result of Postfix Increment = 101
After Postfix Increment, startValue = 102
Result of Prefix Increment = 102
After Prefix Increment, startValue = 102
Result of Postfix Decrement = 101
After Postfix Decrement, startValue = 100
Result of Prefix Decrement = 100
After Prefix Decrement, startValue = 100

## 分析 ![Image](img/arrow.jpg)

结果显示，后置运算符与前缀运算符的不同之处在于，第 8 行和第 18 行中赋值的左值（l-values）包含了该整数在实际执行增 1 或减操作之前的原始值。相比之下，第 13 行和第 23 行的前缀操作导致左值被赋值为增 1 或减 1 后的值。这是在选择正确的运算符类型时需要注意的最区别。

请注意，在以下语句中，前缀或后置运算符对程序的输出没有影响：

```cpp
startValue++; // 等同于...
++startValue;
```

这是因为没有对初始值进行赋值，两种情况的最终结果都是整数`startValue`增了 1。

### 注意事项

你经常听到出于更好的性能考虑而倾向于使用前缀增或或减运算符的情况。即，`++startValue`优于`startValue++`。

这至少在理论上是正确的，因为对于后置运算符，编译器在需要赋值时需要临时存储初始值。对于整数来说，这种情况下这种情况对性能的影响微乎其微，但在某些类的情况下，这个论点可能是有意义的。智能编译器可能会优化这些差异。

### 等价运算符 (`==`) 和 (`!=`)

通常在执行某个操作之前，你可能需要检查某个条件是否满足或未满足。等价运算符`==`（操作数相等）和`!=`（操作数不相等）正好帮助你实现这一点。

等价检查的结果是一个`bool`类型——即`true`或`false`。

```cpp
int personAge = 20;
bool checkEquality = (personAge == 20); // true
bool checkInequality = (personAge != 100); // true
bool checkEqualityAgain = (personAge == 200); // false
bool checkInequalityAgain = (personAge != 20); // false
```

### 关系运算符

除了等价检查外，你可能想检查某个变量与某个值之间是否不等。为了帮助你实现这一点，C++ 包含了关系运算符（参见表 5.1）。

![Image](img/05tab01.jpg)

**表 5.1** 关系运算符

如表 5.1 所示，比较操作的结果始终是`true`或`false`，换句话说是一个`bool`。以下示例代码展示了如何使用表 5.1 中引入的关系运算符：

```cpp
int personAge = 20;
bool checkLessThan = (personAge < 100); // true
bool checkGreaterThan = (personAge > 100); // false
bool checkLessThanEqualTo = (personAge <= 20); // true
bool checkEqualTo = (personAge >= 20); // true
bool checkGreaterThanAgain = (personAge >= 100); // false
```

列表 5.3 是一个程序，通过在屏幕上显示结果来演示使用这些运算符的效果。

**列表 5.3** 展示等价和关系运算符

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Enter two integers:";
    int num1, num2;
    cin >> num1 >> num2;

    bool isEqual = (num1 == num2);
    cout << "Result of equality test: " << isEqual << endl;

    bool isUnequal = (num1 != num2);
    cout << "Result of inequality test: " << isUnequal << endl;

    bool isLessThan = (num1 < num2);
    cout << "Result of less than test: " << isLessThan << endl;

    bool isGreaterThan = (num1 > num2);
    cout << "Result of greater than test: " << isGreaterThan << endl;

    bool isLessThanEqual = (num1 <= num2);
    cout << "Result of less than or equal test: " << isLessThanEqual << endl;

    bool isGreaterEqual = (num1 >= num2);
    cout << "Result of greater than or equal test: " << isGreaterEqual << endl;

    return 0;
}
```

```cpp
cout << "Start value of integer being operated: " << startValue << endl;

int postfixIncrement = startValue++;
cout << "Result of Postfix Increment = " << postfixIncrement << endl;
cout << "After Postfix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixIncrement = ++startValue;
cout << "Result of Prefix Increment = " << prefixIncrement << endl;
cout << "After Prefix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int postfixDecrement = startValue--;
cout << "Result of Postfix Decrement = " << postfixDecrement << endl;
cout << "After Postfix Decrement, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixDecrement = --startValue;
cout << "Result of Prefix Decrement = " << prefixDecrement << endl;
cout << "After Prefix Decrement, startValue = " << startValue << endl;

return 0;
```



```cpp
cout << "Start value of integer being operated: " << startValue << endl;

int postfixIncrement = startValue++;
cout << "Result of Postfix Increment = " << postfixIncrement << endl;
cout << "After Postfix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixIncrement = ++startValue;
cout << "Result of Prefix Increment = " << prefixIncrement << endl;
cout << "After Prefix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int postfixDecrement = startValue--;
cout << "Result of Postfix Decrement = " << postfixDecrement << endl;
cout << "After Postfix Decrement, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixDecrement = --startValue;
cout << "Result of Prefix Decrement = " << prefixDecrement << endl;
cout << "After Prefix Decrement, startValue = " << startValue << endl;

return 0;
```

Output ![Image](img/arrow.jpg)

此处点击查看代码图像

被操作整数的起始值：101

Result of Postfix Increment = 101

After Postfix Increment, `startValue` = 102

Result of Prefix Increment = 102

After Prefix Increment, `startValue` = 102

Result of Postfix Decrement = 101

After Postfix Decrement, `startValue` = 100

Result of Prefix Decrement = 100

After Prefix Decrement, `startValue` = 100

## 分析 ![Image](img/arrow.jpg)

结果显示，后置运算符与前缀运算符的不同之处在于，第 8 行和第 18 行中赋值的左值（l-values）包含了该整数在实际执行增或减操作之前的原始值。相比之下，第 13 行和第 23 行的前缀操作导致左值被赋值为增 1 或减后的值。这是在选择正确的运算符类型时需要注意的最区别。

请注意，在以下语句中，前缀或后置运算符对程序的输出没有影响：

此处点击查看代码图像

```cpp
startValue++; // 等同于...

++startValue;
```

这是因为没有对初始值进行赋值，两种情况的最终结果都是整数 `startValue` 增了 1。

### 注意事项

你经常听到出于更好的性能考虑而倾向于使用前缀增或减运算符的情况。即，`++startValue` 优于 `startValue++`。

这至少在理论上是正确的，因为对于后置运算符，编译器在需要赋值时需要临时存储初始值。对于整数来说，这种情况下对性能的影响微乎其微，但在某些类的情况下，这个论点可能是有意义的。智能编译器可能会优化这些差异。

### 等价运算符（`==`）和（`!=`）

通常在执行某个操作之前，你可能需要检查某个条件是否满足或未满足。等价运算符 `==`（操作数相等）和 `!=`（操作数不相等）正好帮助你实现这一点。

等价检查的结果是一个 `bool` 类型——即 `true` 或 `false`。

此处点击查看代码图像

```cpp
int personAge = 20;
bool checkEquality = (personAge == 20); // true
bool checkInequality = (personAge != 100); // true
bool checkEqualityAgain = (personAge == 200); // false
bool checkInequalityAgain = (personAge != 20); // false
```

### 关系运算符

除了等价检查外，你可能想检查某个变量与某个值之间是否不等。为了帮助你实现这一点，C++ 包含了关系运算符（参见表 5.1）。

![Image](img/05tab01.jpg)

**表 5.1** 关系运算符

如表 5.1 所示，比较操作的结果始终是 `true` 或 `false`，换句话说是一个 `bool`。以下示例代码展示了如何使用表 5.1 中引入的关系运算符：

此处点击查看代码图像

```cpp
int personAge = 20;
bool checkLessThan = (personAge < 100); // true
bool checkGreaterThan = (personAge > 100); // false
bool checkLessThanEqualTo = (personAge <= 20); // true
bool checkEqualTo = (personAge >= 20); // true
bool checkGreaterThanAgain = (personAge >= 100); // false
```

列表 5.3 是一个程序，通过在屏幕上显示结果来演示使用这些运算符的效果。

**列表 5.3** 展示等价和关系运算符

```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "Enter two integers:";
    int num1, num2;
    cin >> num1 >> num2;

    bool isEqual = (num1 == num2);
    cout << "Result of equality test: " << isEqual << endl;

    bool isUnequal = (num1 != num2);
    cout << "Result of inequality test: " << isUnequal << endl;

    bool isLessThan = (num1 < num2);
    cout << "Result of less than test: " << isLessThan << endl;

    bool isGreaterThan = (num1 > num2);
    cout << "Result of greater than test: " << isGreaterThan << endl;

    bool isLessThanEqual = (num1 <= num2);
    cout << "Result of less than or equal test: " << isLessThanEqual << endl;

    bool isGreaterEqual = (num1 >= num2);
    cout << "Result of greater than or equal test: " << isGreaterEqual << endl;

    return 0;
}
```



```
*(注：由于原文文本中代码块与输出描述之间存在逻辑差异，翻译时严格遵循“不翻译代码块”原则，仅对描述性文本进行翻译。)*
```



```cpp
cout << "Start value of integer being operated: " << startValue << endl;

int postfixIncrement = startValue++;

cout << "Result of Postfix Increment = " << postfixIncrement << endl;

cout << "After Postfix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset

int prefixIncrement = ++startValue;

cout << "Result of Prefix Increment = " << prefixIncrement << endl;

cout << "After Prefix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset

int postfixDecrement = startValue--;

cout << "Result of Postfix Decrement = " << postfixDecrement << endl;

cout << "After Postfix Decrement, startValue = " << startValue << endl;

startValue = 101; // Reset

int prefixDecrement = --startValue;

cout << "Result of Prefix Decrement = " << prefixDecrement << endl;

cout << "After Prefix Decrement, startValue = " << startValue << endl;

return 0;
```

输出 ![图像](img/arrow.jpg)

此处点击查看代码图像

被操作整数的起始值: 101  
后缀递增的结果 = 101  
后缀递增后，`startValue` = 102  
前缀递增的结果 = 102  
前缀递增后，`startValue` = 102  
后缀递减的结果 = 101  
后缀递减后，`startValue` = 100  
前缀递减的结果 = 100  
前缀递减后，`startValue` = 100

### 分析 ![图像](img/arrow.jpg)

结果显示，后缀运算符与前缀运算符不同：第 8 行和第 18 行中被赋值的左值包含整数在实际递增或递减操作之前的原始值。另一方面，第 13 行和第 23 行中的前缀操作会将递增或递减后的值赋给左值。这是在选择正确运算符类型时需要牢记的最重要区别。

请注意，在以下语句中，前缀或后缀运算符对程序输出没有影响：

此处点击查看代码图像

```cpp
startValue++; // Is the same as...

++startValue;
```

这是因为没有对初始值进行赋值，在这两种情况下，最终结果都只是整数`startValue`被递增。

### 注意事项

你经常听到出于性能考虑而优先使用前缀递增或递减运算符的说法。也就是说，倾向于使用`++startValue`而不是`startValue++`。

这至少在理论上是正确的，因为使用后缀运算符时，编译器需要临时存储初始值，以备需要将其赋值的情况。对于整数而言，这些情况下对性能的影响可以忽略不计；但对于某些类来说，这种说法可能有一定道理。智能编译器可能会优化掉其中的差异。

### 等价运算符（`==`）和（`!=`）

通常在执行操作之前，你可能需要检查某个条件是否满足或未满足。等价运算符`==`（操作数相等）和`!=`（操作数不相等）正好帮助你实现这一点。

等价检查的结果是一个`bool`类型——即`true`或`false`。

此处点击查看代码图像

```cpp
int personAge = 20;

bool checkEquality = (personAge == 20); // true

bool checkInequality = (personAge != 100); // true

bool checkEqualityAgain = (personAge == 200); // false

bool checkInequalityAgain = (personAge != 20); // false
```

### 关系运算符

除了等价检查外，你可能想检查某个变量与某个值之间是否不等。为了帮助你实现这一点，C++ 包含了关系运算符（参见表 5.1）。

![图像](img/05tab01.jpg)

**表 5.1** 关系运算符

如表 5.1 所示，比较操作的结果始终是`true`或`false`，换句话说是一个`bool`。以下示例代码展示了如何使用表 5.1 中引入的关系运算符：

此处点击查看代码图像

```cpp
int personAge = 20;

bool checkLessThan = (personAge < 100); // true

bool checkGreaterThan = (personAge > 100); // false

bool checkLessThanEqualTo = (personAge <= 20); // true

bool checkEqualTo = (personAge >= 20); // true

bool checkGreaterThanAgain = (personAge >= 100); // false
```

列表 5.3 是一个程序，通过在屏幕上显示结果来演示使用这些运算符的效果。

**列表 5.3** 展示等价和关系运算符



```cpp
cout << "Start value of integer being operated: " << startValue << endl;

int postfixIncrement = startValue++;
cout << "Result of Postfix Increment = " << postfixIncrement << endl;
cout << "After Postfix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixIncrement = ++startValue;
cout << "Result of Prefix Increment = " << prefixIncrement << endl;
cout << "After Prefix Increment, startValue = " << startValue << endl;

startValue = 101; // Reset
int postfixDecrement = startValue--;
cout << "Result of Postfix Decrement = " << postfixDecrement << endl;
cout << "After Postfix Decrement, startValue = " << startValue << endl;

startValue = 101; // Reset
int prefixDecrement = --startValue;
cout << "Result of Prefix Decrement = " << prefixDecrement << endl;
cout << "After Prefix Decrement, startValue = " << startValue << endl;

return 0;
```

输出 ![Image](img/arrow.jpg)

此处点击查看代码图像

被操作整数的起始值：101

`Result of Postfix Increment = 101`

`After Postfix Increment, startValue = 102`

`Result of Prefix Increment = 102`

`After Prefix Increment, startValue = 102`

`Result of Postfix Decrement = 101`

`After Postfix Decrement, startValue = 100`

`Result of Prefix Decrement = 100`

`After Prefix Decrement, startValue = 100`

## 分析 ![Image](img/arrow.jpg)

结果显示，后置运算符与前缀运算符的不同之处在于，第 8 行和第 18 行中赋值的左值（l-values）包含了该整数在实际执行增或减操作之前的原始值。相比之下，第 13 行和第 23 行的前缀操作导致左值被赋值为增 1 或减后的值。这是在选择正确的运算符类型时需要注意的最区别。

请注意，在以下语句中，前缀或后置运算符对程序的输出没有影响：

此处点击查看代码图像

```cpp
startValue++; // 等同于...

++startValue;
```

这是因为没有对初始值进行赋值，两种情况的最终结果都是整数 `startValue` 增了 1。

### 注意事项

你经常听到出于更好的性能考虑而倾向于使用前缀增或减运算符的情况，即 `++startValue` 优于 `startValue++`。

这至少在理论上是正确的，因为对于后置运算符，编译器在需要赋值时需要临时存储初始值。对于整数来说，这种情况下对性能的影响微乎其微，但在某些类的情况下，这个论点可能是有意义的。智能编译器可能会优化这些差异。

### 等价运算符（`==` 和 `!=`）

通常在执行某个操作之前，你可能需要检查某个条件是否满足或未满足。等价运算符 `==`（操作数相等）和 `!=`（操作数不相等）正好帮助你实现这一点。

等价检查的结果是一个 `bool` 类型，即 `true` 或 `false`。

此处点击查看代码图像

```cpp
int personAge = 20;
bool checkEquality = (personAge == 20); // true
bool checkInequality = (personAge != 100); // true
bool checkEqualityAgain = (personAge == 200); // false
bool checkInequalityAgain = (personAge != 20); // false
```

### 关系运算符

除了等价检查外，你可能想检查某个变量与某个值之间是否不等。为了帮助你实现这一点，C++ 包含了关系运算符（参见表 5.1）。

![Image](img/05tab01.jpg)

**表 5.1** 关系运算符

如表 5.1 所示，比较操作的结果始终是 `true` 或 `false`，换句话说是一个 `bool`。以下示例代码展示了如何使用表 5.1 中引入的关系运算符：

此处点击查看代码图像

```cpp
int personAge = 20;
bool checkLessThan = (personAge < 100); // true
bool checkGreaterThan = (personAge > 100); // false
bool checkLessThanEqualTo = (personAge <= 20); // true
bool checkEqualTo = (personAge >= 20); // true
bool checkGreaterThanAgain = (personAge >= 100); // false
```

列表 5.3 是一个程序，通过在屏幕上显示结果来演示使用这些运算符的效果。

**列表 5.3** 展示等价和关系运算符

其他运算符如 `AND`、`OR` 和 `XOR` 需要两个操作数。逻辑与操作只有在每个操作数的值都为 `true` 时，结果才为 `true`。表 5.3 展示了逻辑与操作的功能。

![Image](img/05tab03.jpg)

**表 5.3** 逻辑与操作的真值表

逻辑与操作由运算符 `&&` 支持。

逻辑或操作当至少有一个操作数的值为 `true` 时，结果为 `true`，如表 5.4 所示。

![Image](img/05tab04.jpg)

**表 5.4** 逻辑或操作的真值表

逻辑或操作由运算符 `||` 支持。

异或（缩写为 `XOR`）操作与逻辑或略有不同，它在任意一个操作数为 `true` 但不同均不为 `true` 时，结果为 `true`，如表 5.5 所示。

![Image](img/05tab05.jpg)

**表 5.5** 逻辑异或操作的真值表

C++ 以运算符 `^` 的形式提供了位异或。该运算符有助于评估通过对操作数的位进行异或运算产生的结果。

### 使用 C++ 逻辑运算符 NOT（`!`）、AND（`&&`）和 OR（`||`）

考虑以下语句：

![Image](img/square.jpg) “如果下雨了且如果没有公车，我就无法上班了。”

![Image](img/square.jpg) “如果有深度折扣或者如果我获得了一笔破纪录奖金，我就可以买下那辆车。”

在编程中，您需要这样的逻辑结构，其中两个操作的结果将在逻辑上下文中用于决定程序的程序的未来流程。C++ 提供了逻辑与和逻辑或运算符，您可以在条件语句中使用它们，从而根据条件地改变程序的流程。

列表 5.4 展示了逻辑与和逻辑或运算符的工作。

**列表 5.4** 分析 C++ 逻辑运算符 `&&` 和 `||`

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Enter true(1) or false(0) for two operands:" << endl;
6:     bool op1 = false, op2 = false;
7:     cin >> op1;
8:     cin >> op2;
9:
10:     cout << op1 << " AND " << op2 << " = " << (op1 && op2) << endl;
11:     cout << op1 << " OR " << op2 << " = " << (op1 || op2) << endl;
12:
13:     return 0;
14: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`Enter true(1) or false(0) for two operands:`

`1`

`0`

`1 AND 0 = 0`

`1 OR 0 = 1`

下次运行：

点击此处查看代码图像

`Enter true(1) or false(0) for two operands:`

`1`

`1`

`1 AND 1 = 1`

`1 OR 1 = 1`

## 分析 ![Image](img/arrow.jpg)

程序实际上指示了运算符如何向您提供逻辑与和逻辑或功能。程序没有做的是向您展示如何在做决策中使用它们。

列表 5.5 展示了一个程序，该程序使用条件语句处理和逻辑运算符，根据变量中包含的值执行不同的代码行。

**列表 5.5** 在 `if` 语句中使用逻辑非（`!`）和逻辑与（`&&`）运算符进行条件处理

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Use boolean values(0 / 1) to answer the questions" << endl;
6:     cout << "Is it raining? ";
7:     bool isRaining = false;
8:     cin >> isRaining;
9:
10:     cout << "Do you have buses on the streets? ";
11:     bool busesPly = false;
12:     cin >> busesPly;
13:
14:     // Conditional statement uses logical AND and NOT
15:     if (isRaining && !busesPly)
16:     cout << "You cannot go to work" << endl;
17:     else
18:     cout << "You can go to work" << endl;
19:
20:     if (isRaining && busesPly)
21:     cout << "Take an umbrella" << endl;
22:
23:     if ((isRaining) && busesPly)
24:     cout << "Enjoy the sun and a nice day" << endl;
25:
26:     return 0;
27: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

（注：此处原文内容重复，已按要求翻译翻译）

由于您提供的原文在后续部分出现了乱码或重复，我已根据逻辑进行了对齐翻译。如果需要完整的后续翻译，请提供完整文本。

如果你获得了折扣或获得了一笔丰厚的奖金（或两者都有），该程序会建议买车。否则，它会建议等待。它在第 19 行使用了逻辑非操作来提醒你汽车没有折扣。第 14 行使用了 `if` 结构，并在第 16 行配有相应的 `else`。当条件 `(onDiscount || fantasticBonus)` 求值为 `true` 时，`if` 结构会执行第 15 行的后续语句。该表达式包含逻辑或运算符，当你喜欢的汽车有折扣或你收到了一笔丰厚的奖金时，该表达式为 `true`。当表达式为 `false` 时，将执行第 17 行 `else` 之后的语句。

### 位非（`~`）、位与（`&`）、位或（`|`）和位异或（`^`）运算符

逻辑运算符与位运算符的区别在于位运算符不返回布尔结果。相反，它们提供一个结果，其中每个比特位都是通过对操作数的位执行运算符来控制的。C++ 允许你在位模式下执行如非、或、与和异或（即 XOR）操作，你可以通过使用 `~` 取反、使用 `|` 进行或运算、使用 `&` 进行与运算以及使用 `^` 进行异或运算来操作单个比特位。后三种操作是针对你选择的数字（通常是位掩码）执行的。

在整数包含位位的某些情况下，某些位操作非常有用——例如，每个位可以指定某个标志的状态。因此，一个 32 位的整数可以用来携带 32 个布尔标志。列表 5.7 展示了位运算符的使用。

**列表 5.7** 演示如何使用位运算符对整数中的单个比特位进行非、与、或和异或操作

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <bitset>
2: using namespace std;
3:
4: int main()
5: {
6:     cout << "Enter a number (0 - 255): ";
7:     unsigned short inputNum = 0;
8:     cin >> inputNum;
9:
10:     bitset<8> inputBits (inputNum);
11:     cout << inputNum << " in binary is " << inputBits << endl;
12:
13:     bitset<8> bitwiseNOT = (~inputNum);
14:     cout << "Logical NOT ~" << endl;
15:     cout << "~" << inputBits  << " = " << bitwiseNOT << endl;
16:
17:     cout << "Logical AND, & with 00001111" << endl;
18:     bitset<8> bitwiseAND = (0x0F & inputNum); // 0x0F is hex for 0001111
19:     cout << "0001111 & " << inputBits  << " = " << bitwiseAND << endl;
20:
21:     cout << "Logical OR, | with 00001111" << endl;
22:     bitset<8> bitwiseOR = (0x0F | inputNum);
23:     cout << "00001111 | " << inputBits  << " = " << bitwiseOR << endl;
24:
25:     cout << "Logical XOR, ^ with 00001111" << endl;
26:     bitset<8> bitwiseXOR = (0x0F ^ inputNum);
27:     cout << "00001111 ^ " << inputBits  << " = " << bitwiseXOR << endl;
28:
29:     return 0;
30: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`Enter a number (0 - 255): 181`

`181 in binary is 10110101`

`Logical NOT ~`

`~10110101 = 01001010`

`Logical AND, & with 00001111`

`0001111 & 10110101 = 00000101`

`Logical OR, | with 00001111`

`00001111 | 10110101 = 10111111`

`Logical XOR, ^ with 00001111`

`00001111 ^ 10110101 = 10111010`

## 分析 ![Image](img/arrow.jpg)

该程序使用了 `bitset`——一种你尚未见过的类型——来让显示二进制数据变得容易。`std::bitset` 在此的作用纯粹是为了帮助显示，仅此而已。在第 10、13、18 和 22 行中，你实际上将一个整数赋值给 `bitset` 对象，该对象用于以二进制模式显示相同的整数数据。操作是在整数上完成的。首先，重点关注输出，它向你展示了用户输入的整数 181 的二进制格式，然后演示了各种位操作的效果。

# 列表 5.9：使用复合赋值运算符进行加法、减法、除法、取模、位移以及位或、位与和异或

点击此处查看代码图像



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Enter a number: ";
6:     int value = 0;
7:     cin >> value;
8:
9:     value += 8;
10:     cout << "After += 8, value = " << value << endl;
11:     value -= 2;
12:     cout << "After -= 2, value = " << value << endl;
13:     value /= 4;
14:     cout << "After /= 4, value = " << value << endl;
15:     value *= 4;
16:     cout << "After *= 4, value = " << value << endl;
17:     value %= 1000;
18:     cout << "After %= 1000, value = " << value << endl;
19:
20:     // Note: henceforth assignment happens within cout
21:     cout << "After <<= 1, value = " << (value <<= 1) << endl;
22:     cout << "After >>= 2, value = " << (value >>= 2) << endl;
23:
24:     cout << "After |= 0x55, value = " << (value |= 0x55) << endl;
25:     cout << "After ^= 0x55, value = " << (value ^= 0x55) << endl;
26:     cout << "After &= 0x0F, value = " << (value &= 0x0F) << endl;
27:
28:     return 0;
29: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter a number: 440
After += 8, value = 448
After -= 2, value = 446
After /= 4, value = 111
After *= 4, value = 444
After %= 1000, value = 444
After <<= 1, value = 888
After >>= 2, value = 222
After |= 0x55, value = 223
After ^= 0x55, value = 138
After &= 0x0F, value = 10
```

## 分析 ![Image](img/arrow.jpg)

注意 `value` 在整个程序过程中通过各种赋值运算符被不断修改。每个操作都是使用 `value` 执行的，操作的结果被赋值回它。因此，在第 9 行，用户输入的 440 加上 8，结果为 448 并赋值回 `value`。在第 11 行的随后的操作中，从 448 中减去 2，得到 446，然后赋值回 `value`，以此此类推。

## 使用运算符 `sizeof` 确定变量占用的内存

该运算符告诉您特定类型或变量所消耗的字节（bytes）内存量。`sizeof` 的用法如下：

```cpp
sizeof (variable);
```

或：

```cpp
sizeof (type);
```

### 注意

`sizeof(...)` 看起来像是一个函数调用，但它并不是函数。`sizeof` 是一个运算符。有趣的是，这个运算符不能由程序员定义，因此不能被重载。

你可以在第 12 节“运算符类型与运算符重载”学习更多关于定义自定义运算符的知识。

列表 5.10 展示了使用 `sizeof` 来确定数组占用的内存空间。此外，你可能想重新回顾列表 3.4，分析 `sizeof` 在确定最常见变量类型所消耗内存方面的用法。

**列表 5.10** 使用 `sizeof` 确定包含 100 个整数的数组及其每个元素占用的字节数

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Use sizeof to determine memory used by arrays" << endl;
6:     int myNumbers [100] = {0};
7:
8:     cout << "Bytes used by an int: " << sizeof(int) << endl;
9:     cout << "Bytes used by myNumbers: " << sizeof(myNumbers) << endl;
10:    cout << "Bytes used by an element: " << sizeof(myNumbers[0]) << endl;
11:
12:     return 0;
13: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Use sizeof to determine memory used by arrays
Bytes used by an int: 4
Bytes used by myNumbers: 400
Bytes used by an element: 4
```

你已经学习了运算符的优先级，以及使用括号编写让其他程序员也能理解的代码是多么重要。你还了解了整数溢出的概述，以及避免溢出在实际上是有多重要。

### 问答

**Q** 为什么有些程序使用 `unsigned int`，而 `unsigned short` 占内存更少且也能编译？

**A** `unsigned short` 通常有一个限制为 65535，如果对其进行加 1，它会溢出为 0。为了避免这种行为，良好的应用程序在不确定数值是否会远低于此限值时，会选择 `unsigned int`。

**Q** 我需要计算一个数字在除以 3 之后的两倍。那么，你认为以下代码有什么问题吗：

点击此处查看代码图像

```cpp
int result = Number / 3 << 1;
```

**A** 有的！你为什么不直接使用括号让这行代码对其他程序员来说更容易读呢？增加一两行注释也没有坏处。

**Q** 我的应用程序将两个整数值 5 和 2 相除：

点击此处查看代码图像

```cpp
int num1 = 5, num2 = 2;
int result = num1 / num2;
```

**执行时，结果包含值 2。这不不对吗？**

**A** 完全不是。整数并不是为了包含小数数据的。因此，该操作的结果是 2 而不是 2.5。如果你期望的结果是 2.5，请将所有数据类型改为 `float` 或 `double`。这些类型是用来处理浮点（小数）操作的。

## 工作坊

工作坊提供了测验题来帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用所学知识的经验。在检查附录 E 中的答案之前，请尝试回答测验和练习题，并确保在继续下一节之前你理解了这些答案。

### 测验

**1.** 我正在编写一个除法数字的应用程序。哪种数据类型更合适：`int` 还是 `float`？

**2.** 32 / 7 的值是多少？

**3.** 32.0/7 的值是多少？

**4.** `sizeof(...)` 是一个函数吗？

**5.** 我需要计算一个数字的倍倍，对其加上 5，然后再再次倍倍。这正确吗？

点击此处查看代码图像

```cpp
int result = number << 1 + 5 << 1;
```

**6.** 当异或操作数都结果为真时，异或操作的结果是什么？

### 练习

**1.** 改进测验题 5 中的代码，使用括号来提高清晰度。

**2.** 由此表达式存储的 `result` 的值是多少：

点击此处查看代码图像

```cpp
int result = number << 1 + 5 << 1;
```

**3.** 编写一个程序，要求用户输入两个布尔值，并演示各种位运算符在它们上操作的结果。

# 第 6 节 控制程序流

大多数应用程序在面对新情况或不同用户输入时会有不同的行为。为了让你的应用程序做出不同的反应，你需要编写条件语句，以便在不同情况下执行不同的代码段。

在本节中，你将了解到：

- ![图像](img/square.jpg) 如何让你的程序在某些条件下表现得不同
- ![图像](img/square.jpg) 如何在循环中重复执行一段代码
- ![图像](img/square.jpg) 如何在循环中更好地控制执行流

## 使用 `if ... else` 进行条件执行

你目前所看到和编写的程序都是顺序执行的——从上到下。每一行都被执行了，没有任何一行代码被忽略。但在大多数应用程序中，按从上到下的顺序执行所有代码行很少发生。

想象你想要一个程序，如果用户按下 `m` 则将两个数字相乘，如果按下其他键则将数字相加。

正如图 6.1 所示，并不是所有的代码路径在每次运行中都会执行。如果用户按下 `m`，就会执行乘以两个数字的代码。如果他输入 `m` 以外的任何内容，就会执行执行加法的代码。不存在两者同时执行的情况。

![图像](img/06fig01.jpg)

**图 6.1** 根据用户输入所需的条件处理示例。

### 使用 `if ... else` 进行条件编程

C++ 使用 `if ... else` 结构来实现代码的条件执行，结构如下：

点击此处查看代码图像

```cpp
if (expression)
    // 当表达式为真时执行
else
    // 当表达式为假时执行
```

所以，`if ... else` 结构允许程序在用户输入 `m` 时进行乘法，否则进行加法，如下所示：

点击此处查看代码图像

```cpp
if (userSelection == 'm')
    result = num1 * num2;
else
    result = num1 + num2;
```

注意，表达式评估为 `true` 意味着表达式不为 `false`。

让我们分析列表 6.1 中的此结构，它允许用户决定是相乘还是相加。

**列表 6.1** 根据输入对整数进行乘法运算

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "输入整数：" << endl;
    int num1 = 0, num2 = 0;
    cin >> num1;
    cin >> num2;
    cout << "输入 'm' 乘法，其他为加法：";
    char userSelection = '\0';
    cin >> userSelection;
    int result = 0;
    if (userSelection == 'm')
        result = num1 * num2;
    else
        result = num1 + num2;
    cout << "结果为：" << result << endl;
    return 0;
}
```

输出 ![图像](img/arrow.jpg)

点击此处查看代码图像

输入整数：

25

56

输入 'm' 乘法，其他为加法：m

结果为：1400

下次运行：

点击此处查看代码图像

输入整数：

25

56

输入 'm' 乘法，其他为加法：a

结果为：81

## 分析 ![图像](img/arrow.jpg)

注意第 15 行的 `if` 和第 17 行的 `else`。我们指示编译器在跟随 `if` 后的表达式 `(userSelection == 'm')` 评估为 `true` 时执行第 15 行的乘法，或者在评估为 `false` 时执行加法。`(userSelection == 'm')` 是一个在用户输入字符 `m`（区分大小写）时评估为 `true` 的表达式，否则它评估为 `false`。因此，这个简单的程序模拟了图 6.1 中的流程图，并演示了你的应用程序如何在不同情况下表现不同。

### 注意

`if ... else` 结构的 `else` 部分是可选的，在失败时无需要执行操作的情况下不需要使用。

### 注意

如果在列表 6.1 中，第 15 行是：

点击此处查看代码图像

```cpp
if (userSelection == 'm');
```

那么 `if` 结构是没有意义的，因为它在同一行内被一个空语句（分号）终止了。请小心并避免这种情况，因为在这些情况下你不会得到编译错误。

在这种情况下，某些良好的编译器可能会向你警告存在一个“空控制语句”。

## 条件执行多条语句

如果你想在条件成功或失败时执行多条语句，你需要将它们封装在语句块中。这些块本质上是使用大括号 `{...}` 括起来了多个待执行的语句。例如：

点击此处查看代码图像

```cpp
if (condition)
{
   // 条件成功块
   Statement 1;
   Statement 2;
}
else
{
   // 条件失败块
   Statement 3;
   Statement 4;
}
```

此类块也被称为*复合语句*。

列表 6.2 是第 4 节中列表 4.6“管理数组和字符串”的安全性版本。它使用了一个复合语句，当用户输入的长度在数组边界内时，将用户输入复制到静态字符数组中。

**列表 6.2** 在复制字符串到 `char` 数组之前检查边界

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <string>
2: #include <string.h>
3: using namespace std;
4: int main()
5: {
6:     cout << "Enter a line of text: " << endl;
7:     string userInput;
8:     getline (cin, userInput);
9:
10:      char copyInput[20] = { '\0' };
11:      if (userInput.length() < 20) // 检查边界
12:      {
13:          strcpy(copyInput, userInput.c_str());
14:          cout << "copyInput contains: " << copyInput << endl;
15:      }
16:      else
17:         cout << "Bounds exceeded: won't copy!" << endl;
18:
19:      return 0;
20: }
```

输出 ![图像](img/arrow.jpg)

点击此处查看代码图像

输入一行文本：

This fits buffer!

copyInput contains: This fits buffer!

下次运行：

点击此处查看代码图像

输入一行文本：

This doesn't fit the buffer!

Bounds exceeded: won't copy!

## 分析 ![图像](img/arrow.jpg)

注意在第 11 行中复制到缓冲区之前，是如何检查字符串长度与缓冲区长度的。此 `if` 检查的特殊之处在于，当检查结果为 `true` 时，第 12 行到 15 行存在一个语句块（也称为复合语句）。

## 嵌套 `if` 语句

你经常会遇到需要验证许多不同条件的情况，其中许多条件依赖于前一个条件的评估结果。C++ 允许你嵌套 `if` 语句来处理此类需求。

嵌套的 `if` 语句类似于如下：

点击此处查看代码图像

```cpp
if (expression1)
{
   DoSomething1;
   if (expression2)
       DoSomething2;
   else
       DoSomethingElse2;
}
else
    DoSomethingElse1;
```

考虑类似于列表 6.1 的应用程序，用户可以通过按下命令字符 `d` 或 `m` 来指示应用程序进行除法或乘法。现在，只有在除数不为零时才允许除法。因此，除了检查用户输入的预定命令外，当用户指示程序进行除法时，检查除数是否为零也是重要的。列表 6.3 使用了嵌套的 `if` 结构。

**列表 6.3** 在数字的乘法或除法中使用嵌套 `if` 语句

点击此处查看代码图像



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Enter two numbers: " << endl;
6:     float num1 = 0, num2 = 0;
7:     cin >> num1;
8:     cin >> num2;
9:
10:    cout << "Enter 'd' to divide, anything else to multiply: ";
11:    char userSelection = '\0';
12:    cin >> userSelection;
13:
14:    if (userSelection == 'd')
15:    {
16:        cout << "You wish to divide!" << endl;
17:        if (num2 != 0)
18:            cout << num1 << " / " << num2 << " = " << num1 / num2 << endl;
19:        else
20:            cout << "Division by zero is not allowed" << endl;
21:    }
22:    else
23:    {
24:        cout << "You wish to multiply!" << endl;
25:        cout << num1 << " x " << num2 << endl;
26:    }
27:
28:    return 0;
29: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入两个数字：

45

9

`'d'` to divide, anything else to multiply: m

You wish to multiply!

45 x 9

下次运行：

点击此处查看代码图像

输入两个数字：

22

7

`'d'` to divide, anything else to multiply: d

You wish to divide!

22 / 7

最后运行：

点击此处查看代码图像

输入两个数字：

36

0

`'d'` to divide, anything else to multiply: d

You wish to divide!

Division by zero is not allowed

## 分析 ![Image](img/arrow.jpg)

输出是针对三种不同输入运行程序的结果，你可以看到程序对这三种运行执行了不同的路径。此 `if` 条件与列表 6.1 不同，该程序接受浮点数，这在进行除法时非常重要。

提示：你在代码中插入的嵌套缩进（空格）是可选的，但它们显著提高了嵌套 `if` 语句的可读性。许多现代 IDE 会自动缩进代码。

注意 `if...else` 结构也可以组合在一起。列表 6.4 是一个向用户询问星期，然后使用分组的 `if...else` 结构告诉用户该星期几名的程序。

**列表 6.4** 使用分组的 `if...else` 结构

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     enum DaysOfWeek
6:     {
7:         Sunday = 0,
8:         Monday,
9:         Tuesday,
10:        Wednesday,
11:        Thursday,
12:        Friday,
13:        Saturday
14:    };
15:
16:    cout << "Find what days of the week are named after!" << endl;
17:    cout << "Enter a number for a day (Sunday = 0): ";
18:
19:    int dayInput = Sunday; // 初始化为 Sunday
20:    cin >> dayInput;
21:
22:    if (dayInput == Sunday)
23:        cout << "Sunday was named after the Sun" << endl;
24:    else if (dayInput == Monday)
25:        cout << "Monday was named after the Moon" << endl;
26:    else if (dayInput == Tuesday)
27:        cout << "Tuesday was named after Mars" << endl;
28:    else if (dayInput == Wednesday)
29:        cout << "Wednesday was named after Mercury" << endl;
30:    else if (dayInput == Thursday)
31:        cout << "Thursday was named after Jupiter" << endl;
32:    else if (dayInput == Friday)
33:        cout << "Friday was named after Venus" << endl;
34:    else if (dayInput == Saturday)
35:        cout << "Saturday was named after Saturn" << endl;
36:
37:    return 0;
38: }
```

```cpp
35:         cout << "Saturday was named after Saturn" << endl;
36:     else
37:         cout << "Wrong input, execute again" << endl;
38:
39:     return 0;
40: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：5

星期五是用金星命名的

下次运行：

点击此处查看代码图片

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：9

输入错误，重新执行

## 分析 ![Image](img/arrow.jpg)

注意第 22 到 37 行中使用的 `if-else-if` 结构，它用于检查用户输入并产生相应的输出。第二次运行的输出表明，当用户输入超出预期范围 0–6 的数字时，程序能够告知用户，因此该数字不对应星期中的任何一天。这种结构的优势在于，它非常适合验证互斥的条件，也就是说，星期一永远可能是星期二，且无效输入不可能是星期中的任何一天。该程序中另一个值得注意的有趣点是使用了第 5 行声明的枚举 `DaysOfWeek`，它在整个 `if` 语句中都被使用。你本简单地将用户输入与整数值（如星期日的 0 等）进行比较。然而，使用枚举器 `Sunday` 使代码更具可读性。

## 使用 `switch-case` 进行条件处理

`switch-case` 的目的是允许你将一个特定表达式与一系列可能的常量进行比较，并可能为这些不同的值执行不同的操作。你会在此类结构中经常遇到的新 C++ 关键字有 `switch case`、`default` 和 `break`。

以下是 `switch-case` 结构的语法：

点击此处查看代码图片

```cpp
switch(expression)
{
case LabelA:
    DoSomething;
    break;
case LabelB:
    DoSomethingElse;
    break;
// 等此类推...
default:
    DoStuffWhenExpressionIsNotHandledAbove;
    break;
}
```

发生的情况是，生成的代码求值 `expression`，并与其后的每个 case 标签进行相等性检查。每个 case 标签需要是一个常量。然后它执行该标签后的代码。当 `expression` 的求值不为 `LabelA` 时，它会检查 `LabelB`。如果该检查结果为 `true`，则执行 `DoSomethingElse`。这种检查会持续进行，直到遇到 `break`。这是我们第一次使用 `break` 关键字。`break` 会导致执行退出代码块。`break` 并不是强制的；但是，如果没有 `break`，执行将简单继续检查下一个标签，依此类推，而这正是你在这种情况下想要避免的。`default` 也是可选的，当表达式不等于 `switch-case` 结构中的任何标签时，将执行该 case。

**提示**

`switch-case` 结构非常适合与枚举器一起使用。关键字 `enum` 引入于第 3 课，“使用变量、声明常量。](#ch03.html_ch03)”

列表 6.5 是列表 6.4 中程序的 `switch-case` 等效版本，它告诉人们星期中的一天是如何命名的，并使用了枚举常量。

**列表 6.5** 使用 `switch-case`、`break` 和 `default` 查找星期中的某天是如何命名的

点击此处查看代码图片

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     enum DaysOfWeek
6:     {
7:         Sunday = 0,
8:         Monday,
9:         Tuesday,
10:        Wednesday,
11:        Thursday,
12:        Friday,
13:        Saturday
14:    };
15:
16:     cout << "Find what days of the week are named after!" << endl;
17:     cout << "Enter a number for a day (Sunday = 0): ";
18:
19:     int dayInput = Sunday; // 初始化为星期日
20:     cin >> dayInput;
21:
22:     switch(dayInput)
23:     {
24:         case Sunday:
25:         cout << "Sunday was named after the Sun" << endl;
26:         break;
27:
28:         case Monday:
29:         cout << "Monday was named after the Moon" << endl;
30:         break;
31:
32:         case Tuesday:
33:         cout << "Tuesday was named after Mars" << endl;
34:         break;
35:
36:         case Wednesday:
37:         cout << "Wednesday was named after Mercury" << endl;
38:         break;
39:
40:         case Thursday:
41:         cout << "Thursday was named after Jupiter" << endl;
42:         break;
43:
44:         case Friday:
45:         cout << "Friday was named after Venus" << endl;
46:         break;
47:
48:         case Saturday:
49:         cout << "Saturday was named after Saturn" << endl;
50:         break;
51:
52:         default:
53:         cout << "Wrong input, execute again" << endl;
54:         break;
55:     }
56:     return 0;
57: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：5

星期五是用金星命名的

下次运行：

点击此处查看代码图片

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：9

输入错误，重新执行

## 分析 ![Image](img/arrow.jpg)

第 22 到 55 行包含了 `switch-case` 结构，它根据用户输入的 `dayInput` 产生不同的输出。当用户输入数字 5 时，程序会将 `switch` 表达式 `dayInput` 与其后的每个标签进行相等性检查。这种结构的优势在于，它非常适合验证互斥的条件，也就是说，星期一永远可能是星期二，且无效输入不可能是星期中的任何一天。该程序中另一个值得注意的有趣点是使用了第 5 行声明的枚举 `DaysOfWeek`，它在整个 `switch` 语句中都被使用。你本简单地将用户输入与整数值（如星期日的 0 等）进行比较。然而，使用枚举器 `Sunday` 使代码更具可读性。

## 使用 `switch-case` 进行条件处理

`switch-case` 的目的是允许你将一个特定表达式与一系列可能的常量进行比较，并可能为这些不同的值执行不同的操作。你会在此类结构中经常遇到的新 C++ 关键字有 `switch case`、`default` 和 `break`。

以下是 `switch-case` 结构的语法：

点击此处查看代码图片

```cpp
switch(expression)
{
case LabelA:
    DoSomething;
    break;
case LabelB:
    DoSomethingElse;
    break;
// 等此类推...
default:
    DoStuffWhenExpressionIsNotHandledAbove;
    break;
}
```

发生的情况是，生成的代码求值 `expression`，并与其后的每个 case 标签进行相等性检查。每个 case 标签需要是一个常量。然后它执行该标签后的代码。当 `expression` 的求值不为 `LabelA` 时，它会检查 `LabelB`。如果该检查结果为 `true`，则执行 `DoSomethingElse`。这种检查会持续进行，直到遇到 `break`。这是我们第一次使用 `break` 关键字。`break` 会导致执行退出代码块。`break` 并不是强制的；但是，如果没有 `break`，执行将简单继续检查下一个标签，依此类推，而这正是你在这种情况下想要避免的。`default` 也是可选的，当表达式不等于 `switch-case` 结构中的任何标签时，将执行该 case。

**提示**

`switch-case` 结构非常适合与枚举器一起使用。关键字 `enum` 引入于第 3 课，“使用变量、声明常量。](#ch03.html_ch03)”

列表 6.5 是列表 6.4 中程序的 `switch-case` 等效版本，它告诉人们星期中的一天是如何命名的，并使用了枚举常量。

**列表 6.5** 使用 `switch-case`、`break` 和 `default` 查找星期中的某天是如何命名的

点击此处查看代码图片



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     enum DaysOfWeek
6:     {
7:         Sunday = 0,
8:         Monday,
9:         Tuesday,
10:        Wednesday,
11:        Thursday,
12:        Friday,
13:        Saturday
14:    };
15:
16:     cout << "Find what days of the week are named after!" << endl;
17:     cout << "Enter a number for a day (Sunday = 0): ";
18:
19:     int dayInput = Sunday; // 初始化为星期日
20:     cin >> dayInput;
21:
22:     switch(dayInput)
23:     {
24:         case Sunday:
25:         cout << "Sunday was named after the Sun" << endl;
26:         break;
27:
28:         case Monday:
29:         cout << "Monday was named after the Moon" << endl;
30:         break;
31:
32:         case Tuesday:
33:         cout << "Tuesday was named after Mars" << endl;
34:         break;
35:
36:         case Wednesday:
37:         cout << "Wednesday was named after Mercury" << endl;
38:         break;
39:
40:         case Thursday:
41:         cout << "Thursday was named after Jupiter" << endl;
42:         break;
43:
44:         case Friday:
45:         cout << "Friday was named after Venus" << endl;
46:         break;
47:
48:         case Saturday:
49:         cout << "Saturday was named after Saturn" << endl;
50:         break;
51:
52:         default:
53:         cout << "Wrong input, execute again" << endl;
54:         break;
55:     }
56:     return 0;
57: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片。

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：5

星期五是用金星命名的。

下次运行：

点击此处查看代码图片。

查找星期中的某天是如何命名的！

输入一个天的数字（星期日 = 0）：9

输入错误，重新执行。

## 使用运算符（`?:`）进行条件执行

C++ 有一种有趣且强大的运算符，被称为条件运算符，它类似于一种紧凑的 `if-else` 结构。

条件运算符也称为三元运算符，因为它接受三个操作数：

```cpp
(条件表达式求值为 bool) ? expression1 如果真 : expression2 如果假;
```

这种运算符可以紧凑地评估两个数字中的较大值，如下所示：

```cpp
int max = (num1 > num2) ? num1 : num2; // max 包含 num1 和 num2 中的较大值
```

列表 6.6 是使用运算符（`?:`）进行条件处理的演示。

```cpp
12:      << num2 << " is: " << max << endl;
13:
14:    return 0;
15: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

输入两个数字：

365

-1

365 和 -1 的较大值是：365

分析 ![Image](img/arrow.jpg)

第 10 行是我们关注的代码。它包含一个紧凑的语句，用于判断输入的两个数字中哪一个更大。这一行是使用 `if-else` 实现以下逻辑的另一种方式：

```cpp
int max;

if (num1 > num2)
    max = num1;
else
    max = num2;
```

因此，条件运算符节省了几行代码！然而，节省代码行不应该是首要任务。有些程序员倾向于使用条件运算符，而另一些则不然。以易于理解的方式编写条件运算符至关重要。

### 应该（DO）

**应该**在 `switch` 表达式中使用枚举符来提高代码的可读性。

**应该**记得处理 `default` 情况，除非被认为完全没有必要。

**应该**检查是否在无意中忘记在每个 `case` 语句中插入 `break`。

### 不要（DON’T）

**不要**添加两个具有相同标签的 `case` 情况——这没有意义而且无法通过编译。

**不要**通过包含不带 `break` 的 `case` 并依赖执行顺序来使你的 `case` 语句复杂化。在未来，当你在不十分注意顺序的情况下移动 `case` 语句时，这会破坏代码或功能。

**不要**在使用条件运算符（`?:`）时使用复杂的条件或表达式。

### 提示（Tip）

C++17 预计将引入使用 `if constexpr` 的条件编译，以及 `if` 和 `switch` 结构中的初始化器。在第 29 节“向前展望”（`ch29.html_ch29`）中学习更多这些特性。

## 在循环中执行代码

到目前为止，你已经看到如何让程序在某些变量包含不同值时产生不同的行为——例如在列表 6.1 中，当用户按下 *m* 时我们执行乘法；否则执行加法。然而，如果用户不想让程序结束呢？如果他想执行另一个加法或乘法操作，或者再执行五次呢？这时你需要重复执行已有的代码。

这就是你需要编写循环的时候。

### 使用 `goto` 的原始循环

顾名思义，`goto` 指令执行从代码中特定标记点继续。你可以用它重新执行某些语句。

`goto` 语句的语法为：

```cpp
SomeFunction()
{
Start: // 标签
    CodeThatRepeats;
    goto Start;
}
```

你定义了一个名为 `Start` 的标签，并使用 `goto` 从该点开始重复执行，如列表 6.7 所示。除非你在给定一个特定情况下可能求为 `false` 的条件下调用 `goto`，或者除非重复的代码包含一个在特定条件下执行的 `return` 语句，否则 `goto` 命令与标签之间的代码将无限重复，并导致程序无法结束。

**列表 6.7** 使用 `goto` 询问用户是否想要重复计算：

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5: Start:
6:     int num1 = 0, num2 = 0;
7:
8:     cout << "Enter two integers: " << endl;
9:     cin >> num1;
10:    cin >> num2;
11:
12:    cout << num1 << " x " << num2 << " = " << num1 * num2 << endl;
13:    cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;
14:
15:    cout << "Do you wish to perform another operation (y/n)?" << endl;
16:    char repeat = 'y';
17:    cin >> repeat;
18:    if (repeat == 'y')
19:    goto Start;
20:    cout << "Goodbye!" << endl;
21:    return 0;
22: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

输入两个整数：

56

25

56 x 25 = 1400

56 + 25 = 81

你是否想要执行另一个操作（y/n）？

y

输入两个整数：

95

-47

95 x -47 = -4465

95 + -47 = 48

你是否想要执行另一个操作（y/n）？

n

再见！

分析 ![Image](img/arrow.jpg)

第 10 行是我们关注的代码。它包含一个紧凑的语句，用于判断输入的两个数字中哪一个更大。这一行是使用 `if-else` 实现以下逻辑的另一种方式：

```cpp
int max;

if (num1 > num2)
    max = num1;
else
    max = num2;
```

因此，条件运算符节省了几行代码！然而，节省代码行不应该是首要任务。有些程序员倾向于使用条件运算符，而另一些则不然。以易于理解的方式编写条件运算符至关重要。

### `while` 循环

C++ 关键字 `while` 可以帮助实现 `goto` 所做的功能，其语法如下：

```cpp
while(expression)
{
    // Expression evaluates to true
    StatementBlock;
}
```

语句块重复执行，只要 `expression` 的结果为 `true`。因此，重要的是编写一个在某些情况下变为 `false` 的条件，否则 `while` 循环将不会结束。列表 6.8 是 `goto` 的等效形式，但使用了更优雅的方式。

**列表 6.8** 使用 `while` 循环帮助用户重新计算：

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     char userSelection = 'm'; // 初始值
6:
7:     while (userSelection != 'x')
8:     {
9:         cout << "Enter two integers: " << endl;
10:        int num1 = 0, num2 = 0;
11:        cin >> num1;
12:        cin >> num2;
13:
14:        cout << num1 << " x " << num2 << " = " << num1 * num2 << endl;
15:        cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;
16:
17:        cout << "Press x to exit(x) or any other key to recalculate" << endl;
18:        cin >> userSelection;
19:     }
20:
21:     cout << "Goodbye!" << endl;
22:     return 0;
23: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

输入两个整数：

56

25

56 x 25 = 1400

56 + 25 = 81

按下 x 退出（x）或按下其他按键重新计算：

r

输入两个整数：

365

-5

365 x -5 = -1825

365 + -5 = 360

按下 x 退出（x）或按下其他按键重新计算：

x

再见！

第 7–19 行中的 `while` 循环包含了程序中的大部分逻辑。注意 `while` 是如何检查表达式 `(userSelection != 'x')` 的，只有当该表达式求值为 `true` 时才会继续。为了能够首次运行，你在第 5 行将字符变量 `userSelection` 初始化为 `'m'`。此值需要是任何不是 `'x'` 的值（否则条件在第一次循环时就会失败，应用程序将在未让用户进行任何建设性操作的情况下退出）。第一次运行非常简单，但程序在第 17 行询问用户是否希望再次执行另一组计算。第 18 行包含用户的输入，你在此处修改 `while` 评估的表达式，从而让程序获得继续或终止的机会。当第一次循环完成后，执行返回到第 7 行 `while` 语句中对 `expression` 的评估，如果用户没有按下 `x`，则重复。当用户在循环结束时按下 `x` 时，第 7 行对表达式的下次评估结果为 `false`，执行退出 `while` 循环，最终在显示告别语句后结束应用程序。

> ### Note
>
> 循环也被称为*迭代*（iteration）。涉及 `while`、`do...while` 和 `for` 的语句也称为*迭代语句*（iterative statements）。

### `do...while` 循环

在某些情况下（如列表 6.8 所示），你需要确保某段代码在循环中重复并至少执行一次。这就是 `do...while` 循环大显用场。

`do...while` 循环的语法为：

```cpp
do
{
    StatementBlock; // 至少执行一次
} while(condition); // 如果条件求值为 false 则结束循环
```



注意包含`while(expression)`的那一行以分号结尾。这与之前的`while`循环不同，在之前的循环中，`while`后的分号将实际上在这一行就终止循环，导致产生空语句。

列表 6.9 展示了如何通过至少执行一次执行语句来实现`do...while`循环。

**列表 6.9** 使用`do...while`重复执行代码块

点击查看代码图片

***

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     char userSelection = 'x';   // 初始值
6:     do
7:     {
8:         cout << "Enter the two integers: " << endl;
9:         int num1 = 0, num2 = 0;
10:          cin >> num1;
11:          cin >> num2;
12:
13:          cout << num1 << " x " << num2 << " = " << num1 * num2 << endl;
14:          cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;
15:
16:          cout << "Press x to exit(x) or any other key to recalculate" << endl;
17:          cin >> userSelection;
18:     } while (userSelection != 'x');
19:
20:     cout << "Goodbye!" << endl;
21:
22:     return 0;
23: }
```

***

输出 ![Image](img/arrow.jpg)

点击查看代码图片

```text
Enter the two integers:
654
-25
654 x -25 = -16350
654 + -25 = 629
Press x to exit(x) or any other key to recalculate
m
Enter the two integers:
909
101
909 x 101 = 91809
909 + 101 = 1010
Press x to exit(x) or any other key to recalculate
x
Goodbye!
```

分析 ![Image](img/arrow.jpg)

该程序的行为和输出与列表 6.8 相似。事实上，唯一的区别是第 6 行的`do`关键字以及后续第 18 行对`while`的使用。代码执行按顺序进行，逐行执行，直到到达第 18 行的`while`。在这里`while`评估表达式`(userSelection != 'x')`。当表达式求值为`true`时（即用户没有按下字符`x`退出），循环执行重复。当表达式求值为`false`时（即用户按了`x`），执行退出循环并继续执行告别和结束应用程序。

### `for`循环

`for`语句是一种更复杂的循环，因为它允许执行一次的初始化语句（通常用于初始化计数器）、检查退出条件（通常使用该计数器），并在每次循环结束时执行一个操作（通常是增加或修改该计数器）。

`for`循环的语法为：

点击查看代码图片

```cpp
for (initialization; condition; increment)
{
    statement;
}
```

`for`循环项功能允许程序员定义一个带有初始值的计数器变量、根据退出条件进行检查，并在每次循环结束时更改该值。列表 6.10 展示了使用`for`循环访问数组元素的有效方法。

**列表 6.10** 使用`for`访问数组元素

点击查看代码图片

***

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     const int ARRAY_LENGTH = 5;
6:     int myNums[ARRAY_LENGTH];
7:
8:     cout << "Populate array of " << ARRAY_LENGTH << " integers" << endl;
9:     for (int counter = 0; counter < ARRAY_LENGTH; ++counter)
10:     {
11:         cout << "Enter integer for element " << counter << ": ";
12:         cin >> myNums[counter];
13:     }
14:
15:     cout << "Display contents of the array:" << endl;
16:     for (int counter = 0; counter < ARRAY_LENGTH; ++counter)
17:     {
18:         cout << "Element " << counter << " = " << myNums[counter] << endl;
19:     }
20:
21:     return 0;
22: }
```

```cpp
using namespace std;

int main()
{
    // 没有循环表达式（缺少第三个表达式）
    for(char userSelection = 'm'; (userSelection != 'x');)
    {
        cout << "Enter the two integers: " << endl;
        int num1 = 0, num2 = 0;
        cin >> num1;
        cin >> num2;

        cout << num1 << " x " << num2 << " = " << num1 * num2 << endl;
        cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;

        cout << "Press x to exit or any other key to recalculate" << endl;
        cin >> userSelection;
    }

    cout << "Goodbye!" << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```text
Enter the two integers:
56
25
56 x 25 = 1400
56 + 25 = 81
Press x to exit or any other key to recalculate
m
Enter the two integers:
789
-36
789 x -36 = -28404
789 + -36 = 753
Press x to exit or any other key to recalculate
x
Goodbye!
```

分析 ![Image](img/arrow.jpg)

该程序与使用`while`循环的 Listing 6.8 相同；唯一的区别是它在第 6 行使用了`for`结构。这个`for`循环的有趣之处在于，它只包含初始化表达式和条件表达式，忽略了在每次循环结束时更改变量的选择。

### 注意

你可以在`for`循环的第一个执行一次的初始化表达式中初始化多个变量。Listing 6.11 中带有多个初始化的`for`循环看起来如下所示：

点击此处查看代码图片

```cpp
for (int counter1 = 0, counter2 = 5; // 初始化
      counter1 < ARRAY_LENGTH;   // 检查
      ++counter1, --counter2)  // 增，减
```

注意新添加的变量`counter2`，它被初始化为 5。

有趣的是，我们还可以在循环表达式中对其递减，每次循环执行一次。

### 基于范围的`for`循环

C++11 引入了`for`循环的新变体，使得对值范围（例如数组包含的值）进行操作的代码更加简单且易读。

基于范围的`for`循环的语法也使用了相同的关键字`for`：

点击此处查看代码图片

```cpp
for (VarType varName : sequence)
{
    // 使用包含 sequence 中元素的 varName
}
```

例如，给出一个整数数组`someNums`，你将使用基于范围的`for`循环来读取数组包含的元素，如下所示：

点击此处查看代码图片

```cpp
int someNums[] = { 1, 101, -1, 40, 2040 };
for (int aNum : someNums) // 基于范围的 for
    cout << "The array elements are " << aNum << endl;
```

### 提示

你可以通过通过关键字`auto`使用自动变量类型推导功能来进一步简化此`for`语句，组合出一个通用的`for`循环，该循环适用于任何类型的数组`elements`：

点击此处查看代码图片

```cpp
for (auto anElement : elements) // 基于范围的 for
    cout << "Array elements are " << anElement << endl;
```

关键字`auto`和自动变量类型推断功能是在第 3 Lesson 中引入的。

Listing 6.12 展示了针对不同类型范围的基于范围的`for`循环。

### 列表 6.12 遍历数组和`std::string`的基于范围的`for`循环

点击此处查看代码图片

```cpp
#include<iostream>
#include <string>
using namespace std;

int main()
{
    int someNums[] = { 1, 101, -1, 40, 2040 };
    for (const int& aNum : someNums)
        cout << aNum << ' ';
    cout << endl;

    for (auto anElement : { 5, 222, 110, -45, 2017 })
        cout << anElement << ' ';
    cout << endl;

    char charArray[] = { 'h', 'e', 'l', 'l', 'o' };
    for (auto aChar : charArray)
        cout << aChar << ' ';
    cout << endl;

    double moreNums[] = { 1, 101, -1, 40, 2040 };
    for (auto anElement : moreNums)
        cout << anElement << ' ';
    cout << endl;

    return 0;
}
```

如果你想结束一个`infinite loop`（例如前面的示例中操作系统需要关闭），你可以通过插入`break`（通常用于`if (condition)`块内部）来实现。

以下是使用`break`退出无限`while`循环的示例：

点击此处查看代码图像

```cpp
while(true)   // while condition fixed to true
{
    DoSomethingRepeatedly;
    if(expression)
        break;  // 当 expression 求值为为 true 时退出循环
}
```

在无限的`do...while`中使用`break`：

点击此处查看代码图像

```cpp
do
{
    DoSomethingRepeatedly;
    if(expression)
        break;  // 当 expression 求值为为 true 时退出循环
} while(true);
```

在无限的`for`循环中使用`break`：

点击此处查看代码图像

```cpp
for (;;)   // no condition supplied = unending for
{
    DoSomethingRepeatedly;
    if(expression)
        break;  // 当 expression 求值为为 true 时退出循环
}
```

Listing 6.13 展示了如何使用`continue`和`break`控制退出标准来编写无限循环。

**列表 6.13** 使用`continue`重启和使用`break`退出无限`for`循环

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     for(;;)   // an infinite loop
6:     {
7:         cout << "Enter two integers: " << endl;
8:         int num1 = 0, num2 = 0;
9:         cin >> num1;
10:         cin >> num2;
11:
12:         cout << "Do you wish to correct the numbers? (y/n): ";
13:         char changeNumbers = '\0';
14:         cin >> changeNumbers;
15:
16:         if (changeNumbers == 'y')
17:             continue;  // restart the loop!
18:
19:         cout << num1 << " x " << num2 << " = " << num1 * num2 << endl;
20:         cout << num1 << " + " << num2 << " = " << num1 + num2 << endl;
21:
22:         cout << "Press x to exit or any other key to recalculate" << endl;
23:         char userSelection = '\0';
24:         cin >> userSelection;
25:
26:         if (userSelection == 'x')
27:             break;   // exit the infinite loop
28:     }
29:
30:     cout << "Goodbye!" << endl;
31:
32:     return 0;
33: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Enter two integers:

560

25

Do you wish to correct the numbers? (y/n): y

Enter two integers:

56

25

Do you wish to correct the numbers? (y/n): n

56 x 25 = 1400

56 + 25 = 81

Press x to exit or any other key to recalculate

r

Enter two integers:

95

-1

Do you wish to correct the numbers? (y/n): n

95 x -1 = -95

95 + -1 = 94

Press x to exit or any other key to recalculate

x

Goodbye!
```

分析 ![Image](img/arrow.jpg)

第 5 行的`for`循环与 Listing 6.11 中的不同之处在于，它是一个无限`for`循环，不包含在每次迭代中都求值的条件表达式。换句话说，如果不执行`break`语句，此循环（以及该程序）永远不会退出。注意输出，它与你之前看到的其他输出不同，它允许用户在程序继续计算和和乘法之前对输入进行修正。这种逻辑是通过第 16 行和第 17 行对特定条件的求值使用`continue`实现的。当用户在询问是否修正数字时按下`y`，第 16 行的条件求值为`true`，执行后续的`continue`。遇到`continue`时，执行跳转到循环顶部，再次要求输入整数。同样，在循环结束当用户被询问是否退出时，其输入会在第 26 行与`'x'`进行比对，如果是，则执行后续的`break`，结束无限循环。

注意 Listing 6.13 使用空的`for(;;)`创建无限循环。你可以用`while(true)`或`do...while(true);`来替换它。

### 做

- 当循环逻辑需要至少执行一次时使用`do...while`。
- 使用带有良好定义表达式的`while`、`do...while`或`for`循环。
- 缩进循环中的代码以提高可读性。

### 不要做

- 使用`goto`。
- 随意地使用`continue`和`break`。



除非绝对必要，否则使用`break`编写无限循环。

## 嵌套循环

正如你在课程开头看到的嵌套`if`语句，你经常需要将一个循环嵌套另一个。假设有两个整数数组。如果你想找到`array1`中每个数字与`array2`中每个数字的乘积，可以使用嵌套循环。第一个循环遍历`array1`，而第二个循环在第一个循环内部遍历`array2`。

Listing 6.14 展示了嵌套循环的使用。

**列表 6.14** 使用嵌套循环将数组中的每个元素与另一个相乘

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     const int ARRAY1_LEN = 3;
6:     const int ARRAY2_LEN = 2;
7:
8:     int myNums1[ARRAY1_LEN] = {35, -3, 0};
9:     int myNums2[ARRAY2_LEN] = {20, -1};
10:
11:     cout << "Multiplying each int in myNums1 by each in myNums2:" << endl;
12:
13:     for(int index1 = 0; index1 < ARRAY1_LEN; ++index1)
14:         for(int index2 = 0; index2 < ARRAY2_LEN; ++index2)
15:             cout << myNums1[index1] << " x " << myNums2[index2] << \
16:             << " = " << myNums1[index1] * myNums2[index2] << endl;
17:
18:     return 0;
19: }
```

输出 ![Image](img/arrow.jpg)

```text
Multiplying each int in myNums1 by each in myNums2:

35 x 20 = 700

35 x -1 = -35

-3 x 20 = -60

-3 x -1 = 3

0 x 20 = 0

0 x -1 = 0
```

在第 4 Lesson 中，你学习了多维数组。实际上，在列表 4.3 中，你访问了一个三行三列二维数组中的元素。你所做的是逐个访问数组中的每个元素，每行一个。这并没有实现自动化，而且如果需要扩大数组，除了更改数组维度以访问其元素外，你还需要编写大量的代码。然而，使用循环可以改变这一切，正如列表 6.15 所示。

## 列表 6.15 使用嵌套循环遍历整数二维数组中的元素

点击此处代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     const int NUM_ROWS = 3;
6:     const int NUM_COLUMNS = 4;
7:
8:     // 2D array of integers
9:     int MyInts[NUM_ROWS][NUM_COLUMNS] = { {34, -1, 879, 22},
10:                                     {24, 365, -101, -1},
11:                                     {-20, 40, 90, 97} };
12:
13:     // iterate rows, each array of int
14:     for (int row = 0; row < NUM_ROWS; ++row)
15:     {
16:         // iterate integers in each row (columns)
17:         for (int column = 0; column < NUM_COLUMNS; ++column)
18:         {
19:             cout << "Integer[" << row << "][" << column \
20:                   << "] = " << MyInts[row][column] << endl;
21:         }
22:     }
23:
24:     return 0;
25: }
```

输出 ![Image](img/arrow.jpg)

点击此处代码图像

```text
Integer[0][0] = 34
Integer[0][1] = -1
Integer[0][2] = 879
Integer[0][3] = 22
Integer[1][0] = 24
Integer[1][1] = 365
Integer[1][2] = -101
Integer[1][3] = -1
Integer[2][0] = -20
Integer[2][1] = 40
Integer[2][2] = 90
Integer[2][3] = 97
```

## 分析 ![Image](img/arrow.jpg)

第 14–22 行包含两个`for`循环，你需要通过它们访问并遍历整数二维数组。二维数组实际上是一个整数数组的数组。注意第一个`for`循环如何访问行（每一行都是整数数组），而第二个循环如何访问该数组中的每个元素——即访问其中的列。

注意：列表 6.15 使用大括号包裹嵌套的`for`仅仅是为了提高可读性。这种嵌套循环不使用大括号也能正常工作，因为循环语句只是要执行的单个语句（而不是必须使用大括号包裹的复合语句）。

## 使用嵌套循环计算斐波那契数列

著名的斐波那契数列是一组从 0 和 1 开始的数字，序列中的每一个后续数字都是前两个数字之和。因此，一个斐波那契数列从如下序列开始：0, 1, 1, 2, 3, 5, ... 等。列表 6.16 展示了如何创建一个包含任意数量数字的斐波那契数列（受存储最后一个数字的整数的数据类型限制）。

## 列表 6.16 使用嵌套循环计算序列

点击此处代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     const int numsToCalculate = 5;
6:     cout << "This program will calculate " << numsToCalculate \
7:             << " Fibonacci Numbers at a time" << endl;
8:
9:     int num1 = 0, num2 = 1;
10:    char wantMore = '\0';
11:    cout << num1 << " " << num2 << " ";
12:
13:    do
14:     {
15:         for (int counter = 0; counter < numsToCalculate; ++counter)
16:         {
17:             cout << num1 + num2 << " ";
18:
19:             int num2Temp = num2;
20:             num2 = num1 + num2;
21:             num1 = num2Temp;
22:         }
23:
24:         cout << endl << "Do you want more numbers (y/n)?
25:         cin >> wantMore;
26:     }while (wantMore == 'y');
27:
28:     cout << "Goodbye!" << endl;
29:     return 0;
30: }
```

输出 ![Image](img/arrow.jpg)

点击此处代码图像

```text
This program will calculate 5 Fibonacci Numbers at a time
0 1 1 2 3 
Do you want more numbers (y/n)? y
5 8 13 21 34 
Do you want more numbers (y/n)? y
55 89 144 233 377 
Do you want more numbers (y/n)? y
610 987 1597 2584 4181 
Do you want more numbers (y/n)? y
... (省略)
...
n
Goodbye!
```

## 分析 ![Image](img/arrow.jpg)

第 13 行的外部`do...while`循环基本上是一个查询循环，如果用户想要更多数字，就会重复。第 15 行的内部`for`循环负责计算下一个斐波那契数字并一次显示五个数字。在第 19 行，你将`num2`的值存储在临时变量`num2Temp`中，以便在第 21 行使用。注意，如果不存储这个临时值，你将直接将第 20 行修改后的值赋予`num1`，这并不是你想要的。当用户按下‘y’以获取更多数字时，`do...while`循环再次执行，从而执行嵌套的`for`循环生成另外五个斐波那契数字。

### 练习

练习提供了测验来帮助你巩固对所涵盖内容的理解，并通过练习题提供使用所学知识的机会。在查看附录 E 中的答案之前，尝试回答测验和练习题，并在继续下一节之前确保你理解了这些答案。

### 测验

1. 既然即使没有缩进也可以编译，为什么还要对语句块、嵌套`if`和嵌套循环中的代码进行缩进呢？
2. 你可以使用`goto`实现快速修复。但为什么你仍然应该避免它呢？
3. 是否可以写一个计数器递减的`for`循环？它看起来是什么样的？
4. 下述循环有什么问题？

点击此处查看代码图像

```cpp
for (int counter=0; counter==10; ++counter)
    cout << counter << " ";
```

### 练习

1. 编写一个`for`循环以反序访问数组中的元素。
2. 编写一个等同于 Listing 6.14 的嵌套循环，以反序相两个数组中的元素。
3. 编写一个程序，类似于 Listing 6.16 显示斐波那契数字，但会询问用户想要计算多少个数字。
4. 编写一个`switch-case`结构，判断颜色是否在彩虹中。使用枚举常量。
5. 漏洞终结（BUG BUSTERS）：这段代码哪里错了？

点击此处查看代码图像

```cpp
for (int counter=0; counter=10; ++counter)
    cout << counter << " ";
```

6. 漏洞终结（BUG BUSTERS）：这段代码哪里错了？

点击此处查看代码图像

```cpp
int loopCounter = 0;
while(loopCounter <5);
{
    cout << loopCounter << " ";
    loopCounter++;
}
```

7. 漏洞终结（BUG BUSTERS）：这段代码哪里错了？

点击此处查看代码图像

```cpp
cout << "Enter a number between 0 and 4" << endl;
int input = 0;
cin >> input;
switch (input)
{
case 0:
case 1:
case 2:
case 3:
case 4:
cout << "Valid input" << endl;
default:
    cout << "Invalid input" << endl;
}
```

## 第 7：使用函数组织代码

到目前为止，你已经了一些简单的程序，所有的编程工作都包含在`main()`中。这对于非常小的程序和应用程序非常好。随着你的程序变得越来越复杂，`main()`的内容也会变得越来越长，除非你使用函数来结构化你的程序。

函数为你提供了一种划分和组织程序执行逻辑的方法。它们允许你将应用程序的内容拆分成逻辑块，并按顺序调用它们。

因此，函数是一个子程序，可以可选地接收参数并返回值，并且需要调用来执行其任务。在本节中，你将学习：

- 程序函数的需要
- 函数声明和函数定义
- 向函数传递参数并返回值
- 函数重载
- 递归函数
- C++11 lambda 函数

## 函数的需求

考虑一个要求用户输入圆形半径然后计算周长和面积的应用程序。实现此点的方法是将其全部放在`main()`中。另一种方法是将此应用程序拆分为逻辑块：特别是两个根据给定半径计算面积和周长的部分。参见 Listing 7.1。

**LISTING 7.1** 给定半径计算圆面积和周长的两个函数

点击此处查看代码图像

```cpp
  0: #include <iostream>
  1: using namespace std;
  2:
  3: const double Pi = 3.14159265;
  4:
  5: // 函数声明（原型）
  6: double Area(double radius);
  7: double Circumference(double radius);
  8:
  9: int main()
  10: {
  11:     cout << "Enter radius: ";
  12:     double radius = 0;
  13:     cin >> radius;
  14:     cout << "Area: " << Area(radius) << endl;
  15:     cout << "Circumference: " << Circumference(radius) << endl;
  16:     return 0;
  17: }
  18:
  19: double Area(double radius) {
  20:     return Pi * radius * radius;
  21: }
  22:
  23: double Circumference(double radius) {
  24:     return 2 * Pi * radius;
  25: }
```

调用函数与执行（invoking）函数是相同的。当函数声明中包含参数时，函数调用需要发送`arguments`（参数）。参数是函数在其参数列表中请求的值。让我们来分析列表 7.1 中对`Area()`的调用：

点击此处查看代码图像

```cpp
16:cout << "Area is: " << Area(radius) << endl;
```

在这里，`Area(radius)`是函数调用，其中`radius`是发送给函数`Area()`的参数。当函数被调用时，执行流会跳转到函数`Area()`，该函数使用发送的半径来计算圆的面积。

### 编写带有多个参数的函数

假设你正在编写一个计算圆柱表面积的程序，如图图 7.2 所示。

![Image](img/07fig02.jpg)

**图 7.2** 一个圆柱。

你使用的公式如下：

点击此处查看代码图像

圆柱面积 = 上圆面积 + 下圆面积 + 侧面面积

= `Pi * radius² + Pi * radius² + 2 * Pi * radius * height`

= `2 * Pi * radius² + 2 * Pi * radius * height`

因此，在计算圆柱面积时，你需要处理两个变量：`radius`（半径）和`height`（高度）。在这种情况下，在编写计算圆柱表面积的函数时，你需要在函数声明的参数列表中指定至少两个参数。你通过逗号隔开各个参数来实现这一点，如列表 7.2 所示。

**列表 7.2** 接受两个参数以计算圆柱表面积的函数

点击此处查看代码图像



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159265;
4:
5: // Declaration contains two parameters
6: double SurfaceArea(double radius, double height);
7:
8: int main()
9: {
10:     cout << "Enter the radius of the cylinder: ";
11:     double radius = 0;
12:     cin >> radius;
13:     cout << "Enter the height of the cylinder: ";
14:     double height = 0;
15:     cin >> height;
16:
17:     cout << "Surface area: " << SurfaceArea(radius, height) << endl;
18:
19:     return 0;
20: }
21:
22: double SurfaceArea(double radius, double height)
23: {
24:     double area = 2 * Pi * radius * radius + 2 * Pi * radius * height;
25:     return area;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter the radius of the cylinder: 3
Enter the height of the cylinder: 6.5
Surface Area: 179.071
```

分析 ![Image](img/arrow.jpg)

第 6 行包含了函数 `SurfaceArea()` 的声明，带有两个参数：`radius` 和 `height`，类型均为 `double`，并用逗号分隔。第 22–26 行显示了定义——即 `SurfaceArea()` 的实现。如你所示，输入参数 `radius` 和 `height` 用于计算存储在局部变量 `area` 中的值，然后返回给调用者。

### 注意

函数参数类似于局部变量。它们仅在函数作用域内有效。因此，在列表 7.2 中，函数 `SurfaceArea()` 的参数 `radius` 和 `height` 是 `main()` 中同名变量的副本。

### 编写无参数或无返回值的函数

如果你将打印“Hello World”的任务委托给一个只做这一件事而不做其他任何事的函数，你可以使用一个不需要任何参数的函数（因为它除了说“Hello”之外不需要做任何事情），并且可能使用一个不返回任何值的函数（因为你并不期望这样的函数返回任何有用信息）。列表 7.3 展示了这样一个函数。

**列表 7.3** 无参数且无返回值的函数

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: void SayHello();
4:
5: int main()
6: {
7:     SayHello();
8:     return 0;
9: }
10:
11: void SayHello()
12: {
13:     cout << "Hello World" << endl;
14: }
```

输出 ![Image](img/arrow.jpg)

```
Hello World
```

分析 ![Image](img/arrow.jpg)

注意第 3 行声明了 `SayHello()` 函数，其返回类型为 `void`，这意味着它不返回任何值。在第 11–14 行的定义中，没有 `return` 语句。因此，`SayHello()` 是一个无返回值的函数。

### 带有默认值的参数

如果你将 `Pi` 固定为常量且从不给用户更改它的机会，那么你可能无法获得更精确的读数。如何编写一个带有默认值的函数呢？

一种方法是在列表 7.1 中为参数提供默认值，如下：

```cpp
double Area(double radius, double pi = 3.14);
```

在这种情况下，如果调用 `Area(radius)`，第二个参数 `pi` 将默认为 `3.14`。如果调用时传入了第二个参数，例如 `Area(radius, 3.14159)`，则默认值会被覆盖。列表 7.4 展示了：

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: // Function declarations (otypes)
4: double Area(double radius, double pi = 3.14);
5:
6: int main()
7: {
8:     cout << "Enter radius: ";
9:     double radius = 0;
10:     cin >> radius;
11:
12:     // Call function with default value
13:     cout << "Area with default pi: " << Area(radius) << endl;
14:
15:
16:     cout << "Enter custom pi: ";
17:     double customPi = 3.14159;
18:     cin >> customPi;
19:
20:     // Call function with custom pi value
21:     cout << "Area with custom pi: " << Area(radius, customPi) << endl;
22:
23:     return 0;
24: }
25:
26: // Function definitions (implementations)
27: double Area(double radius, double pi)
28: {
29:     return pi * radius * radius;
30: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter radius: 5
Area with default pi: 78.5
Enter custom pi: 3.14159
Area with custom pi: 78.53975
```

在两次运行中，用户输入的半径是相同的——1。然而，在第二次运行中，用户选择了更改 Pi 的精度，因此计算出的面积略有不同。请注意，在上述两种情况下，如第 22 行和第 25 行所示，你调用了同一个函数。第 25 行调用了 `Area()` 但没有提供第二个参数 `pi`。在这种情况下，`Area()` 中的参数 `pi` 包含值 3.14，这是在第 4 行的声明中作为默认提供的。

### 注意

你可以拥有多个带有默认值的参数；但这些参数都应该位于参数列表的末尾。

### 递归——调用自身的函数

在某些情况下，你实际上可以让函数调用自己。这种函数被称为递归函数。注意，递归函数应该有一个非常明确定义的退出条件，在该条件下它返回且不再再次调用自身。

### 警告

如果没有退出条件，或者退出条件中出现错误，你的程序执行将卡在不会停止调用自身的递归函数上，这最终会在发生“栈溢出”时停止，导致应用程序崩溃。

在确定斐波那契数列中的数字时，递归函数是非常有用的，如列表 7.5 所示。该数列从两个数字 0 和 1 开始：

`F(0) = 0`

`F(1) = 1`

数列中后续数字的值是前两个数字之和。因此，*n* 个值（当 `n > 1` 时）由以下递归公式确定：

点击此处查看代码图像

`Fibonacci(n) = Fibonacci(n - 1) + Fibonacci(n - 2)`

结果是斐波那契数列扩展为

点击此处查看代码图像

`F(2) = 1`

`F(3) = 2`

`F(4) = 3`

`F(5) = 5`

`F(6) = 8`，依此类推。

**列表 7.5** 使用递归函数计算斐波那契数列中的数字

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int GetFibNumber(int fibIndex)
4: {
5:     if (fibIndex < 2)
6:         return fibIndex;
7:     else // 如果 fibIndex >= 2 则递归
8:         return GetFibNumber(fibIndex - 1) + GetFibNumber(fibIndex - 2);
9: }
10:
11: int main()
12: {
13:     cout << "Enter 0-based index of desired Number: ";
14:     int index = 0;
15:     cin >> index;
16:
17:     cout << "Fibonacci number is: " << GetFibNumber(index) << endl;
18:     return 0;
19: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入所需的数字（从 0 开始索引）: 6

斐波那契数字是: 8

分析 ![Image](img/arrow.jpg)

在第 3-9 行定义的函数 `GetFibNumber()` 是递归的，因为它在第 8 行调用了自己。第 5 行和第 6 行编写的退出条件确保了当 `fibIndex` 小于二时函数将返回。因此，`GetFibNumber()` 使用减小的 `fibIndex` 值调用自身。它最终会达到满足退出条件的状态，递归结束，并确定斐波那契值并返回给 `main()`。

### 多重返回的函数

你并不限于函数中只能有一个 `return` 语句。你可以从函数的任何点返回，并且如果你需要，可以多次返回，如列表 7.6 所示。取决于逻辑和应用程序的需求，这可能是坏实践，也可能不是坏实践。

**列表 7.6** 在一个函数中使用多个返回语句

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2: const double Pi = 3.14159265;
3:
4: void QueryAndCalculate()
5: {
6:     cout << "Enter radius: ";
7:     double radius = 0;
8:     cin >> radius;
9:
10:    cout << "Area: " << Pi * radius << endl;
11:
12:    cout << "Do you wish to calculate circumference (y/n)? ";
13:    char calcCircum = 'n';
14:    cin >> calcCircum;
15:
16:    if (calcCircum == 'n')
17:        return;
18:
19:    cout << "Circumference: " << 2 * Pi * radius << endl;
20:    return;
21: }
22:
23: int main()
24: {
25:     QueryAndCalculate();
26:
27:     return 0;
28: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入半径: 1

面积: 3.14159

你想计算周长吗 (y/n)? y

周长: 6.28318

分析 ![Image](img/arrow.jpg)

在第 3-9 行定义的函数 `GetFibNumber()` 是递归的，因为它在第 8 行调用了自己。第 5 行和第 6 行编写的退出条件确保了当 `fibIndex` 小于二时函数将返回。因此，`GetFibNumber()` 使用不断减小的 `fibIndex` 值调用自身。它最终会达到满足退出条件的状态，递归结束，并确定一个斐波那契值返回给 `main()`。

### 多重返回的函数

你并不限于函数中只能有一个 `return` 语句。你可以从函数的任何点返回，并且如果你需要，可以多次返回，如列表 7.6 所示。取决于逻辑和应用程序的需求，这可能是坏实践，也可能不是坏实践。

**列表 7.6** 在一个函数中使用多个返回语句

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2: const double Pi = 3.14159265;
3:
4: void QueryAndCalculate()
5: {
6:     cout << "Enter radius: ";
7:     double radius = 0;
8:     cin >> radius;
9:
10:    cout << "Area: " << Pi * radius << endl;
11:
12:    cout << "Do you wish to calculate circumference (y/n)? ";
13:    char calcCircum = 'n';
14:    cin >> calcCircum;
15:
16:    if (calcCircum == 'n')
17:        return;
18:
19:    cout << "Circumference: " << 2 * Pi * radius << endl;
20:    return;
21: }
22:
23: int main()
24: {
25:     QueryAndCalculate();
26:
27:     return 0;
28: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入半径: 1

面积: 3.14159

你想计算周长吗 (y/n)? y

周长: 6.28318

分析 ![Image](img/arrow.jpg)

函数 `QueryAndCalculate()` 包含了多个 `return` 语句：分别在第 17 行和第 20 行。如果用户按 'n' 计算周长，程序将通过 `return` 语句退出。对于其他值，它将继续计算周长并返回。

### 警告

在函数中使用多个返回要小心。一个从顶部开始并在底部返回的函数，比一个在中间多次返回的函数更容易理解和遵循。

在列表 7.6 中，通过简单地更改 `if` 条件来测试 'y'，就可以避免使用多次返回：

### 使用函数处理不同形式的数据

函数并不限制你一次传递一个值；你可以传递数组。你可以创建具有相同名称和返回值的函数，使其参数不在函数调用期间创建和销毁；相反，你可以使用在函数退出后仍然有效的引用，以便允许你进行更多操作。

### 函数重载

具有相同名称和返回类型但参数不同的函数被称为重载函数。重载函数在需要根据特定参数产生特定输出的应用程序中非常有用。假设你需要编写一个计算圆面积和圆柱面积的应用程序。计算圆面积的函数需要一个参数——半径。计算圆柱面积的另一个函数除了半径还需要高度。两个函数都需要返回相同类型的数据（面积）。因此，C++ 允许你定义两个都名为 `Area` 的函数，一个接受半径，另一个接受高度和半径作为输入参数，如列表 7.7 所示。

**列表 7.7** 使用重载函数计算圆或圆柱的面积

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159265;
4:
5: double Area(double radius); // 用于圆
6: double Area(double radius, double height); // 用于圆柱
7:
8: int main()
9: {
10:    cout << "Enter z for Cylinder, c for Circle: ";
11:    char userSelection = 'z';
12:    cin >> userSelection;
13:
14:    cout << "Enter radius: ";
15:    double radius = 0;
16:    cin >> radius;
17:
18:    if (userSelection == 'z')
19:    {
```



```cpp
20:         cout << "Enter height: ";
21:         double height = 0;
22:         cin >> height;
24:         // Invoke overloaded variant of Area for Cyclinder
25:         cout << "Area of cylinder is: " << Area (radius, height) << endl;
26:     }
27:     else
28:         cout << "Area of cylinder is: " << Area (radius) << endl;
30:
     return 0;
31: }

33: // for circle
34: double Area(double radius)
35: {
36:     return Pi * radius * radius;
37: }

39: // overloaded for cylinder
40: double Area(double radius, double height)
41: {
42:     // reuse the area of circle
43:     return 2 * Area (radius) + 2 * Pi * radius * height;
44: }
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图片。

输入圆柱输入 z，圆圆输入 c: z

输入半径: 2

输入高度: 5

圆柱面积为: 87.9646

下一次运行：

点击此处查看代码图片。

输入圆柱输入 z，圆圆输入 c: c

输入半径: 1

圆柱面积为: 3.14159

## 分析

![Image](img/arrow.jpg)

第 5 行和第 6 行声明了 `Area()` 重载形式的原型：第一个重载版本接受单个参数——圆的半径 `radius`。下一个版本接受两个参数——圆柱的半径 `radius` 和高度 `height`。该函数被称为重载函数，是因为有两个具有相同名称 `Area()`、相同返回类型 `double` 但不同参数集合的原型。重载函数的定义在第 34–44 行中，其中两个函数分别根据半径确定圆的面积，以及根据半径和高度确定圆柱的面积。有趣的是，由于圆柱的面积是由它包含的两个圆（顶部一个，底部一个）的面积加上侧面积组成的，因此圆柱的重载版本能够如第 43 行所示，重用用于圆的 `Area()` 函数。

### 传递值数组

显示整数的函数可以如下所示表示：

点击此处查看代码图片。

`void DisplayInteger(int Number);`

可以显示整数数组的函数原型略有不同：

点击此处查看代码图片。

`void DisplayIntegers(int[] numbers, int Length);`

第一个参数告诉函数输入的数据是一个数组，而第二个参数提供了数组的长度 `length`，通过你可以使用该数组而不跨越其边界。请参阅列表 7.8。

**列表 7.8 接受数组作为参数的函数**

点击此处查看代码图片。

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: void DisplayArray(int numbers[], int length)
4: {
5:     for (int index = 0; index < length; ++index)
6:     cout << numbers[index] << " ";
7:
8:     cout << endl;
9: }
10:
11: void DisplayArray(char characters[], int length)
12: {
13:     for (int index = 0; index < length; ++index)
14:     cout << characters[index] << " ";
15:
16:     cout << endl;
17: }
18:
19: int main()
20: {
21:     int myNums[4] = {24, 58, -1, 245};
22:     DisplayArray(myNums, 4);
23:
24:     char myStatement[7] = {'H', 'e', 'l', 'l', 'o', '!', '\0'};
25:     DisplayArray(myStatement, 7);
26:
27:     return 0;
28: }
```

Output ![Image](img/arrow.jpg)

24 58 -1 245

H e l o !

## 分析

![Image](img/arrow.jpg)

这里有两个名为 `DisplayArray()` 的重载函数：一个用于显示整数数组元素的内容，另一个用于显示字符数组的内容。在第 22 行和第 25 行中，分别使用整数数组和字符数组作为输入调用了这两个函数。请注意，在第 24 行声明并初始化字符数组时，你特意包含了空字符（`\0`）——这是一个最佳实践和良好习惯——尽管在该应用程序中，该数组并没有作为字符串用于 `cout` 语句（如 `cout << myStatement;`）。

### 按引用传递参数

再次查看列表 7.1 中的函数，该函数根据半径计算圆的面积：

点击此处查看代码图片。

```cpp
24: // 函数定义
25: double Area(double radius)
26: {
27:     return Pi * radius * radius;
28: }
```

在这里，当在 `main()` 中调用函数时，参数 `radius` 包含的值被复制：

点击此处查看代码图片。

```cpp
15:     // 调用函数
16:     cout << "Area is: " << Area(radius);
```

这意味着 `main()` 中的变量 `radius` 不受影响，因为函数操作的是 `radius` 的副本。在某些情况下，你可能需要函数操作外部的变量，这时你需要声明一个按引用传递的参数。按引用传递面积的 `Area()` 函数如下：

点击此处查看代码图片。

```cpp
// 输出参数 result
void Area(double radius, double& result)
{
    result = Pi * radius;
}
```

注意这种形式的 `Area()` 接受两个参数。不要错过第二个参数 `result` 旁边的符号 `&`。该符号告诉编译器第二个参数不应复制到函数中。由于函数不再作为返回值提供面积，而是作为输出参数，因此返回类型已改为 `void`。这在列表 7.9 中得到了演示，该列表计算圆的面积。

**列表 7.9 通过参数而非返回值获取圆面积**

点击此处查看代码图片。

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.1416;
4:
5: // 输出参数 result 按引用
6: void Area(double radius, double& result)
7: {
8:     result = Pi * radius * radius;
9: }
10:
11: int main()
12: {
13:     cout << "Enter radius: ";
14:     double radius = 0;
15:     cin >> radius;
16:
17:     double areaFetched = 0;
18:     Area(radius, areaFetched);
19:
20:     cout << "The area is: " << areaFetched << endl;
21:     return 0;
22: }
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图片。

输入半径: 2

面积为: 12.5664

## 注意事项

函数使用 `return` 语句只能返回一个值。因此，如果你的函数需要执行影响调用者所需的许多值的操作，按引用传递参数是函数将这些许多修改提供回调用模块的方法之一。

虽然确切知道函数调用在微处理器层级是如何实现的并非极端重要，但你可能会觉得很有趣。理解这有助于你理解为什么 C++ 为你提供了编程内联函数（inline functions）的选项，我们将在本节后面对其进行解释。

函数调用本质上意味着微处理器跳转到位于非连续内存位置的、执行属于被调用函数的下一条指令。在执行完函数中的指令后，它会返回到之前离开的地方。为了实现这一逻辑，编译器会将你的函数调用转换为微处理器的 `CALL` 指令。该指令附带了下一条指令需要跳转的内存地址——该地址属于你的函数例程。当微处理器遇到 `CALL` 时，它会将函数调用后要执行的指令位置保存在栈上，并跳转到 `CALL` 指令包含的内存位置。

## 理解栈

栈是一个后进先出（Last-In-First-Out）的内存结构，非常像一堆盘子，你取最上面的那个盘子，而它是最后被放在栈上的那一个。将数据放入栈中被称为 `push` 操作。从栈中取出数据被称为 `pop` 操作。随着栈向上增长，栈指针始终随着增长而递增，并指向栈顶。参见图 7.3。

![Image](img/07fig03.jpg)

**图 7.3** 包含三个整数的栈的视觉化表示。

栈的特性使其非常适合处理函数调用。当函数被调用时，所有局部变量都会在栈上实例化——也就是说，被推入栈中。当函数结束时，它们简单地从栈中弹出，栈指针返回到原始位置。

此内存位置包含属于函数的指令。微处理器执行这些指令，直到遇到 `RET` 语句（你编写的、用于 `return` 的微处理器代码）。`RET` 语句会导致微处理器从栈中弹出在执行 `CALL` 指令期间存储的那个地址。该地址包含了调用函数中需要继续执行的位置。因此，微处理器回到了调用者处，并从之前离开的地方继续执行。

### 内联函数

普通的函数调用被翻译为 `CALL` 指令，导致栈操作以及微处理器的执行转移到函数处等。这听起来后台发生了大量工作，但对于大多数情况，它的发生非常快。然而，如果你的函数是一个像下面这样简单的函数呢？

点击此处查看代码图像。

```cpp
double GetPi()
{
    return 3.14159;
}
```

对于实际执行 `GetPi()` 所花费的时间来说，对这执行实际函数调用的开销可能很大。这就是为什么 C++ 编译器允许程序员将此类函数声明为内联。关键字 `inline` 是程序员的请求，要求这些函数在被调用处进行内联展开。

点击此处查看代码图像。

```cpp
inline double GetPi()
{
    return 3.14159;
}
```

执行诸如数字倍增等简单操作的函数也是内联的候选。列表 7.10 展示了其中一种情况。

**列表 7.10** 使用使整数倍倍的内联函数

点击此处查看代码图像。

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: // 定义一个将数字倍增的内联函数
4: inline long DoubleNum (int inputNum)
5: {
6:     return inputNum * 2;
7: }
8:
9: int main()
10: {
11:     cout << "Enter an integer: ";
12:     int inputNum = 0;
13:     cin >> inputNum;
14:
15:     // 调用内联函数
16:     cout << "Double is: " << DoubleNum(inputNum) << endl;
17:
18:     return 0;
19: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

Enter an integer: 35

Double is: 70

## 分析

![Image](img/arrow.jpg)

所讨论的关键字是第 4 行中的 `inline`。编译器通常将此关键字视为一种请求，将函数 `DoubleNum()` 的内容直接放在函数被调用的地方——第 16 行——这增加了代码的执行速度。

将函数分类为内联也可能导致代码膨胀，特别是当内联的函数执行大量复杂的处理时。使用 `inline` 关键字应尽可能少。

> **注意**
>
> 现代 C++ 编译器提供了各种优化选项。某些编译器（例如微软）允许你针对大小或速度进行优化。针对大小的优化可能有助于内存可能紧张的设备。当针对速度进行优化时，编译器可能会拒绝许多内联请求。

### 自动返回类型

你学习了使用变量、声明常量。你不需要指定返回类型，而是使用 `auto` 让编译器来推断。列表 7.11 展示了在计算圆面积的函数中使用 `auto`。

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: const double Pi = 3.14159265;
4:
5: auto Area(double radius)
6: {
7:     return Pi * radius;
8: }
9:
10: int main()
11: {
12:     cout << "Enter radius: ";
13:     double radius = 0;
14:     cin >> radius;
15:
16:     cout << "Area is: " << Area(radius) << endl;
17:
18:     return 0;
19: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

Enter radius: 2

Area is: 12.5664

## 分析

关注的行是第 5 行，它使用 `auto` 作为函数 `Area()` 的返回类型。编译器根据返回表达式推断返回类型。因此，尽管使用了 `auto`，列表 7.11 中的 `Area()` 编译出的结果与列表 7.1 中返回类型为 `double` 的 `Area()` 并没有不同。

> **注意**
>
> 依赖自动返回类型推断的函数需要在调用它们之前定义（即实现）。这是因为编译器在调用函数时需要知道其返回类型。如果此类函数有多个返回语句，它们需要推断出同一种类型。递归调用需要至少跟随一个返回语句。

## Lambda 函数

这一部分只是对一个对初学者来说并不易理解的概念的介绍。因此，请快速浏览一遍，并尝试学习这个概念，不要因为没有完全掌握而感到失望。

Lambda 函数是在 C++11 中引入的，有助于在使用 STL 算法对数据进行排序或处理。通常，`sort` 函数要求你提供一个二元谓词（binary predicate）。这是一个比较两个参数的函数，如果其中一个小于另一个，则返回 `true`，否则返回 `false`，从而帮助决定排序操作中元素的顺序。此类谓词通常实现为类中的运算符，这会导致编写一些繁琐的代码。Lambda 函数可以紧凑谓词的定义，如列表 7.12 所示。

**列表 7.12 使用 Lambda 函数显示数组中的元素并对其排序**

点击此处查看代码图像。

```cpp
0: #include <iostream>
1: #include <algorithm>
2: #include <vector>
3: using namespace std;
4:
5: void DisplayNums(vector<int>& dynArray)
6: {
7:     for_each (dynArray.begin(), dynArray.end(), \
8:                 [](int Element) {cout << Element << " ";} );
9:
10:     cout << endl;
11: }
12:
13: int main()
14: {
15:     vector<int> myNums;
16:     myNums.push_back(501);
17:     myNums.push_back(-1);
18:     myNums.push_back(25);
19:     myNums.push_back(-35);
20:
21:     DisplayNums(myNums);
22:
23:     cout << "Sorting them in descending order" << endl;
24:
25:     sort (myNums.begin(), myNums.end(), \
26:             [](int Num1, int Num2) {return (Num2 < Num1); } );
27:
28:     DisplayNums(myNums);
29:
30:     return 0;
31: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

501 -1 25 -35

Sorting them in descending order

501 25 -1 -35

## 分析

![Image](img/arrow.jpg)

程序在第 15–19 行包含了推送到由 C++ 标准库以 `std::vector` 形式提供的动态数组中的整数。`DisplayNums()` 函数使用 STL 算法 `for_each` 遍历数组中的每个元素并显示其值。在此过程中，它在第 8 行使用了一个 Lambda 函数。第 25 行使用的 `std::sort` 也使用了一个 Lambda 函数形式的二元谓词（第 26 行），如果第二个数字小于第一个数字，则返回 `true`，从而有效地对集合进行升序排序。



Lambda 函数的语法如下：

点击此处查看代码图像

```cpp
optional parameters { statements; }
```

---

### 注意事项

谓词及其在 `sort` 等算法中的用法将在第 23 节“STL 算法”中详细讨论，特别是列表 23.6 是一个在算法中使用 Lambda 和非 Lambda 变体的代码示例，从而允许你比较 Lambda 函数引入的编程效率。

---

### 总结

在本节中，你学习了模块化编程的基础知识。你学习了函数如何帮助你更好地组织代码，并帮助你重用编写的算法。你学习了函数可以接受参数并返回值，参数可以具有调用者可以覆盖的默认值，还可以包含通过引用传递的参数。你学习了如何传递数组，还学习了如何编写具有相同名称和返回值但参数列表不同的重载函数。

最后但同样重要的是，你预览了什么是 Lambda 函数。Lambda 函数对于 C++11 来说是全新的，它们潜力改变以后 C++ 程序的编程方式，特别是在使用 STL 时。

### 问答

**Q** 如果我编写了一个不会结束的递归函数会发生什么？

**A** 程序执行不会结束。这本身可能并不坏，对于一个

**Q** 为什么不对每个函数都进行内联？

**A** 这取决于情况。然而，内联每个函数会导致代码在

**Q** 我可以为所有参数提供默认值吗？

**A** 是的，这是可能的也是推荐的

**Q** 我有两个函数，名称和返回值都相同。这可行吗？

**A** 我需要两个相同名称和返回值的函数来进行重载，到栈。

**Q** 函数中声明的变量的作用范围是什么？

**Q** 传递给此的值的性质是什么？

**Q** 我有一个调用自己的函数。这种函数叫什么？

**A**

**Q** 我声明了两个名称不同的函数。这些是什么？

**Q** 栈指向栈的顶部、中间还是底部？

## 工作坊

工作坊提供了测验来帮助你理解材料，并提供了练习来提供经验。

### 测验

**Q** 函数中声明的变量的作用范围是什么？

**Q** 传递给此的值的性质是什么？

**Q** 我有一个调用自己的函数。这种函数叫什么？

**Q** 我声明了两个名称不同的函数。这些是什么？

**Q** 栈指向栈的顶部、中间还是底部？

### 练习

**Q1** 编写重载函数来计算球体和圆体的体积。公式如下：

```text
Volume of sphere = (4 * Pi * radius * radius) / 3
Volume of cylinder = Pi * radius * height
```

**Q2** 编写一个接受 `double` 数组输入的函数。

**Q3** 错：以下代码哪里有问题？

```cpp
#include <iostream>

using namespace std;

const double Pi = 3.1416;

void Area(double radius, double result)
{
    result = Pi * radius * radius;
}

int main()
{
    cout << "Enter radius: ";
    double radius = 0;
    cin >> radius;
    double areaFetched = 0;
    Area(radius, areaFetched);
    cout << "The area is: << areaFetched << endl;
    return 0;
}
```

**Q4** 错：以下函数声明哪里有问题？

```cpp
double Area(double Pi = 3.14, double radius);
```

**Q5** 编写一个返回类型为 `void` 的函数，在提供半径时仍帮助调用者计算圆的面积和周长。

![Image](img/square.jpg) 如何使用运算符 `new` 和 `delete` 来分配内存和释放内存

![Image](img/square.jpg) 如何使用指针和动态分配编写稳定的应用程序

![Image](img/square.jpg) 什么是引用

![Image](img/square.jpg) 指针和引用之间的区别

![Image](img/square.jpg) 何时使用指针，何时使用引用

## 什么是指针？

`pointer`（指针）也是一种变量——它存储内存中的地址。正如 `int` 类型的变量用于包含整数值一样，指针变量被用于包含内存地址，如图 8.1 所示。

![Image](img/08fig01.jpg)

**图 8.1** 指针的可视化。

因此，指针是一个变量，和所有变量一样，指针在内存中占用空间（在图 8.1 中，地址为 `0x101`）。指针的特殊之处在于，指针中所包含的值（在本例中为 `0x558`）被解释为内存地址。所以，指针是一个特殊的变量，指向内存中的某个位置。

---

### 注意

内存位置通常使用 `hexadecimal`（十六进制）表示法进行编号。这是一种 16 进制的计数系统，即包含 16 个不同符号：0–9 后面跟着 A–F。在显示十六进制数时，习惯加上前缀 `0x`。因此，`0xA` 是十进制 10 的十六进制；`0xF` 是十进制 15 的十六进制；`0x10` 是十进制 16 的十六进制。更多信息请参阅附录 A，“处理数字：二进制与十六进制。”

---

### 声明指针

指针作为变量也需要声明。你通常会声明一个指针指向特定的值类型（例如，`int`）。这意味着指针中包含的地址指向内存中存储整数的位置。你也可以指定一个指向内存块的指针（也称为空指针）。

指针作为变量，需要像所有变量一样进行声明：

点击此处查看代码图像

```cpp
PointedType * PointerVariableName;
```

和大多数变量一样，除非你初始化指针，否则它将包含一个随机值。你不希望访问随机的内存地址，因此将指针初始化为 `NULL`。`NULL` 是一个可以被检查的值，且它不是一个内存地址：

点击此处查看代码图像

```cpp
PointedType * PointerVariableName = NULL; // 初始化值
```

因此，声明一个整数指针将是：

```cpp
int *pointsToInt = NULL;
```

---

### 警告

指针和你学过的所有数据类型一样，除非经过初始化，否则它包含一个垃圾值。这种垃圾值在指针情况下特别危险，因为指针的值预期包含一个地址。未初始化的指针会导致你的程序访问无效的内存位置，从而导致崩溃。

---

### 使用引用运算符（`&`）确定变量的地址

变量是语言提供的用于处理内存中数据的工具。这一概念在第 3 节“使用变量、声明常量”中有详细解释。

如果 `varName` 是一个变量，`&varName` 给出其值所在的内存地址。

所以，如果你声明了一个整数，使用你熟悉的语法，例如：

```cpp
int age = 30;
```

`&age` 就是值（`30`）放置的内存地址。列表 8.1 演示了整数变量内存地址的概念，该地址用于存储其包含的值。

**列表 8.1** 确定 `int` 和 `double` 的地址

点击此处查看代码图像

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age = 30;
    const double Pi = 3.1416;

    // 使用 & 查找内存地址
    cout << "Integer age is located at: 0x" << &age << endl;
    cout << "Double Pi is located at: 0x" << &Pi << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Integer age is located at: 0x...

Double Pi is located at: 0x...
```

## 使用指针存储地址

你已经学习如何声明指针以及如何确定变量的地址。现在是使用指针存储地址了。

假设你有一个变量：

```cpp
int age = 30;
```

要将该变量的地址存储在指针中，你需要这样声明指针：

```cpp
int* pointsToInt = &age;
```

在列表 8.2 中，你可以看到如何使用指针存储地址。

**列表 8.2** 演示指针的声明与初始化

点击此处查看代码图像

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age = 30;
    int* pointsToInt = &age; // 初始化指针为 &age

    // 显示指针的值
    cout << "Integer age is at: 0x" << hex << pointsToInt << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Integer age is at: 0x0045FE00
```

### 分析

上述代码段的输出显示了指针如何存储变量的内存地址。

现在你已经知道如何在指针变量中存储地址，很容易想象，同一个指针变量可以被重新分配不同的内存地址，并使其指向不同的值，如列表 8.3 所示。

**列表 8.3** 将指针重新赋值给另一个变量

点击此处查看代码图像

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age = 30;

    int* pointsToInt = &age;
    cout << "pointsToInt points to age now" << endl;

    // Displaying the value of pointer
    cout << "pointsToInt = 0x" << hex << pointsToInt << endl;

    int dogsAge = 9;
    pointsToInt = &dogsAge;
    cout << "pointsToInt points to dogsAge now" << endl;

    cout << "pointsToInt = 0x" << hex << pointsToInt << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
pointsToInt points to age now
pointsToInt = 0x002EFB34
pointsToInt points to dogsAge now
pointsToInt = 0x002EFB1C
```

### 分析

该程序演示了一个指向整数的指针 `pointsToInt` 可以指向任何整数。在第 7 行中，它被初始化为 `&age`，因此包含了变量 `age` 的地址。在第 14 行中，同一个指针被赋值为 `&dogsAge`，指向内存中包含 `dogsAge` 的另一个位置。相应地，输出表明指针的值（即指向的地址）发生了变化，因为两个整数 `age` 和 `dogsAge` 显然存储在内存中的不同位置，分别为 `0x002EFB34` 和 `0x002EFB1C`。

### 使用解引用运算符（`*`）访问指向的数据

你有一个指向数据的指针，其中包含一个有效地址。你如何访问该位置——即如何获取或设置该位置的数据呢？答案在于使用解引用运算符（`*`）。本质上，如果你有一个有效指针 `pData`，使用 `*pData` 来访问存储在指针所包含地址处的值。列表 8.4 演示了该运算符（`*`）。

**列表 8.4** 演示使用解引用运算符（`*`）访问整数值

点击此处查看代码图像

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age = 30;
    int dogsAge = 9;

    cout << "Integer age = " << age << endl;
    cout << "Integer dogsAge = " << dogsAge << endl;

    int* pointsToInt = &age;
    cout << "pointsToInt points to age" << endl;

    // Displaying the value of pointer
    cout << "pointsToInt = 0x" << hex << pointsToInt << endl;

    // Displaying the value at the pointed location
    cout << "*pointsToInt = " << dec << *pointsToInt << endl;

    pointsToInt = &dogsAge;
    cout << "pointsToInt points to dogsAge now" << endl;

    cout << "pointsToInt = 0x" << hex << pointsToInt << endl;
    cout << "*pointsToInt = " << dec << *pointsToInt << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Integer age = 30
Integer dogsAge = 9
pointsToInt points to age
pointsToInt = 0x0025F788
*pointsToInt = 30
pointsToInt points to dogsAge now
pointsToInt = 0x0025F77C
*pointsToInt = 9
```

### 分析

除了像之前的示例列表 8.3 中那样更改指针内部存储的地址外，这个示例还使用同一个指针变量 `pointsToInt` 通过解引用运算符（`*`）打印了这两个地址的不同值。注意第 18 行和第 24 行。在这两行中，都使用解引用运算符（`*`）访问了 `pointsToInt` 指向的整数。由于 `pointsToInt` 在第 20 行更改了地址，赋值后的同一个指针访问了变量 `dogsAge`，显示为 9。

使用解引用运算符（`*`）时，应用程序本质上使用存储在指针中的地址作为起点，从内存中获取整数所需的 4 个字节（因为这是一个指向整数的指针，且 `sizeof(int)` 为 4）。因此，指针中地址的有效性至关重要。通过在第 11 行将指针初始化为 `&age`，你确保了指针包含一个有效地址。如果你不初始化指针，它可能包含任何随机值（存在指针变量所在内存位置中的值），而对该指针进行解引用通常会导致访问冲突（Access Violation）——即访问了应用程序无权访问的内存位置。

---

### 注意

解引用运算符（`*`）也称为间接运算符（indirection operator）。

---

你在上一个示例中使用指针从内存位置读取（获取）值。列表 8.5 显示了当使用 `pointsToInt` 而不仅仅是赋值时会发生什么。

**列表 8.5** 使用指针和解引用运算符操作数据

点击此处查看代码图像

```cpp
#include <iostream>

using namespace std;

int main()
{
    int age = 30;
    int dogsAge = 9;

    cout << "Integer age = " << age << endl;
    cout << "Integer dogsAge = " << dogsAge << endl;

    int* pointsToInt = &age;
    cout << "pointsToInt points to age" << endl;

    // Displaying the value of pointer
    cout << "pointsToInt = 0x" << hex << pointsToInt << endl;

    // Displaying the value at the pointed location
    cout << "*pointsToInt = " << dec << *pointsToInt << endl;
}
```



```cpp
20:     pointsToInt = &dogsAge;

21:     cout << "pointsToInt points to dogsAge now" << endl;

22:

23:     cout << "pointsToInt = 0x" << hex << pointsToInt << endl;

24:     cout << "*pointsToInt = " << dec << *pointsToInt << endl;

25:

26:     return 0;

27: }
```

```cpp
11:    cout << "sizeof(char*) = " << sizeof(char*) << endl;

12:    cout << "sizeof(int*) = " << sizeof(int*) << endl;

13:    cout << "sizeof(double*) = " << sizeof(double*) << endl;

14:

15:    return 0;

16: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

### 基本类型的大小

```text
sizeof(char) = 1
sizeof(int) = 4
sizeof(double) = 8
```

### 指向基本类型指针的大小

```text
sizeof(char*) = 4
sizeof(int*) = 4
sizeof(double*) = 4
```

### 分析

输出清晰地显示，尽管 `sizeof(char)` 是 1 字节而 `sizeof(double)` 是 8 字节，但 `sizeof(char*)` 和 `sizeof(double*)` 都是 4 字节。这是因为存储地址的指针所消耗的内存量是相同的，无论地址处的内存包含 1 字节还是 8 字节的数据。

### 注意

列表 8.6 显示指针的 `sizeof` 为 4 字节的输出可能与你在系统上看到的不同。该输出是在使用 32 位编译器编译代码时生成的。如果你使用 64 位编译器并在 64 位系统上运行程序，你可能会发现你的指针变量的 `sizeof` 是 64 位——即 8 字节。

## 动态内存分配

当你编写一个包含数组声明的程序时：

```cpp
int myNums[100]; // 一个包含 100 个整数的静态数组
```

你的程序存在两个问题：

1. 你实际上限制了程序的容量，因为它无法存储超过 100 个数字。
2. 在只需要存储 1 个数字的情况下，你为 100 个数字预留了空间，从而降低了系统的性能。

这些问题的存在是因为按之前声明的数组内存分配是静态的，并由编译器固定。

为了编写一个能够根据用户需求优化消耗内存资源的应用程序，你需要使用动态内存分配。这允许你在需要更多内存时分配更多内存，并在内存过余时释放内存。C++ 提供了两个运算符 `new` 和 `delete` 来帮助你更好地管理应用程序的内存消耗。指针作为存储内存地址的变量，在高效的动态内存分配中起着至关重要的作用。

### 使用运算符 `new` 和 `delete` 动态分配和释放内存

你使用 `new` 来分配新的内存块。`new` 最常用的形式在成功时返回指向请求内存的指针，否则抛出异常。使用 `new` 时，你需要指定为何种数据类型分配内存：

```cpp
Type* Pointer = new Type; // 为一个元素请求内存
```

你还可以指定想要为该内存分配的元素数量（当你需要为多个一个元素分配内存时）：

```cpp
Type* Pointer = new Type[numElements]; // 为 numElements 请求内存
```

因此，如果你需要分配整数，请使用以下语法：

```cpp
int* pointToAnInt = new int;      // 获取一个整数的指针
int* pointToNums = new int[10];   // 指向包含 10 个整数的块的指针
```

### 注意

注意 `new` 表示对内存的请求。不能保证分配调用总是成功，因为这取决于系统状态和内存资源的可用性。

每个使用 `new` 的分配最终都需要通过 `delete` 进行对等且相反的去分配操作来释放：

```cpp
Type* Pointer = new Type; // 分配内存

delete Pointer;           // 释放上面分配的内存
```

此规则也适用于你请求多个元素的内存时：

```cpp
Type* Pointer = new Type[numElements]; // 分配一个块

delete[] Pointer;                      // 释放上面分配的块
```

### 注意

注意在使用 `new[...]` 分配块时使用 `delete[]`，以及在使用 `new` 分配单个元素时使用 `delete`。

如果你在停止使用分配的内存后不释放它，该内存将保持保留并分配给你的应用程序。这反过来减少了应用程序可用的系统内存量，甚至可能让你的应用程序运行变慢。这被称为*泄漏*（leak），应该避免。列表 8.7 演示了这一点。

### 列表 8.7 使用 `new` 分配内存并通过 `*` 使用 `delete` 释放

点击此处查看代码图像。

```cpp
#include <iostream>

using namespace std;

int main() {

    // 为 int 请求内存

    int* pointsToAge = new int;

    // 使用间接引用访问值

    cout << "Enter dog’s age: ";

    cin >> *pointsToAge;

    // 显示值

    cout << "Age " << *pointsToAge << " is stored at 0x" << hex << pointsToAge << endl;

    // 释放内存

    delete pointsToAge;

    return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

```text
Enter dog’s age: 9
Age 9 is stored at 0x
```

### 分析

注意 `new` 返回指针，这就是为什么它被赋值的原因。用户输入的年龄存储在新分配的内存中。

### 注意

运算符 `delete` 不能作用于任何地址，而是由 `new` 返回且尚未释放的地址。列表 8.6 包含有效地址，但不应使用 `delete` 释放。

注意当使用 `new[...]` 分配一组元素时，应使用 `delete[]` 进行去分配，如列表 8.8 所示。

### 列表 8.8 使用 `new[...]` 分配并使用 `delete[]` 释放

点击此处查看代码图像。

```cpp
#include <iostream>

#include <string>

using namespace std;

int main() {

    cout << "How many integers shall I reserve memory for?" << endl;

    int numEntries = 0;

    cin >> numEntries;

    int* myNumbers = new int[numEntries];

    cout << "Memory allocated at: 0x" << hex << myNumbers << endl;

    // 退出前去分配

    delete[] myNumbers;

    return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

```text
How many integers shall I reserve memory for?

5001
Memory allocated at: 0x00C71578
```

问题中最重要的代码行是分别用在第 10 行和第 15 行的 `new[]` 和 `delete[]` 运算符。此示例与列表 8.7 的不同之处在于，它动态分配了一块可以容纳用户请求数量整数的内存。在执行期间，我们请求了 5001 个整数的空间。在另一次运行中，可能是 20 或 55000。该程序将根据用户输入在每次执行时分配不同数量的内存。元素数组的此类分配在完成后需要使用 `delete[]` 进行释放以释放内存。

### 注释

`new` 和 `delete` 运算符从空闲存储（free store）分配内存。空闲存储是以内存池形式存在的内存抽象，你的应用程序可以在其中分配（即预留）内存并向其释放（即回收）内存。

## 增增和减运算符（`++` 和 `--`）对指针的影响

指针包含一个内存地址。例如，列表 8.3 中指向整数的指针包含 `0x002EFB34`——该整数所在的地址。整数本身长度为 4 字节，因此在内存中占据从 `0x002EFB34` 到 `0x002EFB37` 的四个位置。使用运算符（`++`）增加此指针不会导致指针指向 `0x002EFB35`，因为指向整数的中间实际上毫无意义。

指针的递增或递减操作被编译器解释为你需要指向内存块中的下一个值（假设其具有相同类型），而不是下一个字节（除非值类型的大小为 1 字节，例如 `char`）。

因此，递增列表 8.3 中看到的类似 `pointsToInt` 的指针会导致其增加 4 字节，即一个 `int` 的 `sizeof`。在此指针上使用 `++` 是告诉编译器你希望它指向下一个连续的整数。因此，递增后，指针将指向 `0x002EFB38`。同样，对此指针加 2 将导致其向前移动 2 个整数，即向前移动 8 字节。随后你会发现指针展示的这种行为与数组中使用的索引之间存在关联。

使用运算符（`--`）递减指针展示了相同的效果——指针中包含的地址值减少了其所指向的数据类型的 `sizeof`。

### 当你递增或递减指针时发生了什么？

指针中包含的地址根据所指向类型的 `sizeof` 增加或减少（而不一定是一个字节）。通过这种方式，编译器确保指针永远不会指向内存中放置数据的中间或结尾；它只指向开头。

如果指针被声明为：

```cpp
Type* pType = Address;
```

`++pType` 意味着 `pType` 包含（并指向）`Address + sizeof(Type)`。

参见列表 8.9，它解释了递增指针或对其添加偏移量的影响。

### 列表 8.9 使用偏移值和运算符递增和递减指针

点击此处查看代码图像。

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: int main()

4: {

5:     cout << "How many integers you wish to enter? ";

6:     int numEntries = 0;

7:     cin >> numEntries;

8:

9:     int* pointsToInts = new int [numEntries];

10:

11:     cout << "Allocated for " << numEntries << " integers" << endl;

12:     for(int counter = 0; counter < numEntries; ++counter)

13:     {

14:         cout << "Enter number "<< counter << ": ";

15:         cin >> *(pointsToInts + counter);

16:     }

17:

18:     cout << "Displaying all numbers entered: " << endl;

19:     for(int counter = 0; counter < numEntries; ++counter)

20:         cout << *(pointsToInts++) << " ";

21:

22:     // ... logic continues

23:

24:

25:

26:     delete[] pointsToInts;

27:

28:     return 0;

29: }
```

![Image](img/square.jpg) 指针中包含的地址和所指向的值都是常量，不能更改（限制性最大的变体）：

点击此处查看代码图像。

```cpp
int hoursInDay = 24;

const int* const pHoursInDay = &hoursInDay;

*pHoursInDay = 25; // Not OK! Cannot change data being pointed to

int daysInMonth = 30;

pHoursInDay = &daysInMonth; // Not OK! Cannot change address
```

这些不同的 `const` 在将指针传递给函数时特别有用。函数参数需要声明为支持最高级别（限制性最大）的 `const` 属性，以确保函数在不应该修改时不修改所指向的值。这可以防止应用程序的程序员对指针值或数据进行意外的更改。

## 将指针传递给函数

指针是向函数传递包含相关数据的内存空间的有效方式。共享的内存空间也可以返回操作的结果。在与函数一起使用指针时，确保被调函数仅允许修改你希望它修改的参数，而不是其他参数，变得至关重要。例如，一个通过指针传递半径并计算圆面积的函数不应该被允许修改半径。这就是你使用 `const` 关键字来控制函数允许和不允许修改的内容，如列表 8.10 所示。

### 列表 8.10 在计算圆面积时使用 `const` 关键字

点击此处查看代码图像。

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: void CalcArea(const double* const ptrPi, // const pointer to const data

4:             const double* const ptrRadius, // i.e. no changes allowed

5:             double* const ptrArea)  // can change data pointed to

6: {

7:     // check pointers for validity before using

8:     if (ptrPi && ptrRadius && ptrArea)

9:         *ptrArea = (*ptrPi) * (*ptrRadius) * (*ptrRadius);

10: }

11:

12: int main()

13: {

14:     const double Pi = 3.1416;

15:

16:     cout << "Enter radius of circle: ";

17:     double radius = 0;

18:     cin >> radius;

19:

20:     double area = 0;

21:     CalcArea (&Pi, &radius, &area);

22:

23:     cout << "Area is = " << area << endl;

24:

25:     return 0;

26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

```text
Enter radius of circle: 10.5
Area is = 346.361
```

## 分析

第 3–5 行演示了 `const` 的两种形式，其中 `ptrRadius` 和 `ptrPi` 作为“指向数据的常量指针”，因此指针地址和所指向的数据都不能被修改。`ptrArea` 显然是用于存储输出的参数，因为指针（地址）的值不能修改，但所指向的数据可以。第 8 行显示了在使用前对函数的指针参数进行有效性检查。你不希望调用者不小心发送 NULL 指针作为三个参数之一，因为会导致访问违规并引发应用程序崩溃。

## 数组与指针的相似之处

你不认为列表 8.9 中的示例（通过从零开始的索引增加指针来访问内存中的下一个整数）与数组索引的方式有太多相似之处吗？当你声明一个整数数组时：

```cpp
int myNumbers[5];
```

你告诉编译器分配固定数量的内存来存储五个整数，并给你一个指向该数组中第一个元素的指针，换句话说，`myNumbers` 是指向第一个元素 `myNumbers[0]` 的指针。列表 8.11 强调了这一点。

### 列表 8.11 证明数组变量是一个指针

点击此处查看代码图像。

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: int main()

4: {

5:     // Static array of 5

6:     int myNumbers[5];

7:

8:     // Pointer to int

9:     int* pointNums = myNumbers;

10:

11:     // Address contained in
```



12:     cout << "pointNums = 0x" << hex << pointNums << endl;

13:

14:     // Address of first element

15:     cout << "&myNumbers[0] = 0x" << hex << &myNumbers[0] << endl;

16:

17:     return 0;

18: }

```

因此，该程序演示了数组`myNumbers`和指针`pointToNums`实际上都表现出指针行为。换句话说，数组声明类似于创建一个指针，该指针将在固定范围内存范围内操作。请注意，你可以像第 11 行那样将数组赋值给指针，但不能将指针赋值给数组。因为从本质上说，像`myNumbers`这样的数组是静态的，不能作为左值。`myNumbers`无法修改。

### 注意

重要的是，使用`new`运算符动态分配的指针仍然需要使用`delete`运算符进行释放，即使你使用了通常用于静态数组的语法来访问数据。

如果你忘记了这一点，你的应用程序就会发生内存泄漏，这是糟糕的。

### 使用指针时的常见编程错误

C++ 允许你动态分配内存，以便优化和控制应用程序的内存消耗。与 C# 和 Java 等基于运行时环境的较新语言不同，C++ 并不具备自动垃圾回收器来清理程序分配但无法使用的内存。这种通过指针对内存资源进行管理的惊人控制力，也伴随着许多犯错的机会。

### 内存泄漏

这可能是 C++ 应用程序中最常见的问题之一：运行时间越长，消耗的内存就越多，系统运行得越慢。这通常发生在程序员没有确保在内存块不再需要时，通过与之匹配的`delete`调用来释放使用`new`动态分配的内存。

这由你——程序员——来负责，确保所有分配的内存都由你的应用程序释放。这种情况永远不应该发生：

```cpp
int* pointToNums = new int[5]; // initial allocation

// use pointToNums

...

// 忘记使用 delete[] 释放 pointToNums;

...

// 进行另一次分配并覆盖

pointToNums = new int[10]; // 泄漏了之前分配的内存
```

#### 当指针未指向有效的内存位置时

当你使用运算符（`*`）对指针进行解引用以访问指向的值时，你需要确保指针包含一个有效的内存位置，否则你的程序将崩溃或运行异常。尽管这听起来很合逻辑，但无效指针是应用程序崩溃的常见原因。指针可能由于多种原因而无效，主要是由于糟糕的内存管理不当。指针可能无效的一个典型案例如列表 8.13 所示。

**列表 8.13** 使用指针存储布尔值的程序中糟糕的指针卫生习惯

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: int main()

4: {

5:     // 未初始化的指针（坏）

6:     bool* isSunny;

7:

8:     cout << "Is it sunny (y/n)? ";

9:     char userInput = 'y';

10:     cin >> userInput;

11:

12:     if (userInput == 'y')

13:     {

14:         isSunny = new bool;

15:         *isSunny = true;

16:     }

17:

18:     // 如果用户输入 'n'，isSunny 包含无效值

19:     cout << "Boolean flag sunny says: " << *isSunny << endl;

20:

21:     // 在 new 未调用时也调用了 delete

22:     delete isSunny;

23:

24:     return 0;

25: }
```

Output ![Image](img/arrow.jpg)

Is it sunny (y/n)? y

Boolean flag sunny says: 1

第二次运行：

Is it sunny (y/n)? n

<CRASH!>

Analysis ![Image](img/arrow.jpg)

程序中有许多问题，其中一些已经在代码中注释过。注意第 14 行中是如何分配内存并赋值给指针的，该代码在用户按下‘y’表示是时按条件执行的。对于用户的其他所有输入，此`if`块都不会执行，指针`isSunny`保持为无效状态。因此，当用户在第二次运行中按下‘n’时，应用程序崩溃了，因为`isSunny`包含一个无效的内存地址，在第 19 行对无效指针进行解引用导致了问题。

同样，如第 22 行所示，对这个没有通过`new`分配的指针调用`delete`同样是错误的。注意，如果你有一个指针的副本，你只需要对其中一个调用`delete`（你还需要避免让指针的副本四处漂浮）。

该程序的一个更好（更安全、更稳定）的版本是：对指针进行初始化，仅在值有效时使用，并且仅在有效时释放一次。

#### 悬空指针（也称为野指针或随机指针）

注意，任何有效指针在通过`delete`释放后都是无效的。换句话说，即使是列表 8.13 中的有效指针`isSunny`在第 22 行调用`delete`后也会失效，且在此点之后不应再次使用。

为了避免这个问题，一些程序员遵循一种约定：在初始化指针或在删除指针后给其赋值`NULL`。他们在使用运算符（`*`）解引用指针之前，总是会通过与`NULL`比较来检查指针的有效性。

在了解了使用指针时的一些典型问题后，是时候修正列表 8.13 中的错误代码了，如列表 8.14 所示。

**列表 8.14** 更安全的指针编程，对列表 8.13 的修正

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: int main()

4: {

5:     cout << "Is it sunny (y/n)? ";

6:     char userInput = 'y';

7:

8:     cin >> userInput;

9:

10:     // 声明指针并初始化

11:     bool* const isSunny = new bool;

12:     *isSunny = true;

13:

14:     if (userInput == 'n')

15:         *isSunny = false;

16:

17:     cout << "Boolean flag sunny says: " << *isSunny << endl;

18:

19:     // 释放有效内存

20:     delete isSunny;

21:

22:     return 0;

23: }
```

Output ![Image](img/arrow.jpg)

Is it sunny (y/n)? y

Boolean flag sunny says: 1

下次运行：

Is it sunny (y/n)? n

Boolean flag sunny says: 0

（无论用户输入什么都不会崩溃。）

Analysis ![Image](img/arrow.jpg)

微小的重构使得代码对于所有用户输入都更加安全。注意指针在第 10 行声明时是如何初始化为有效内存地址的。我们使用`const`来确保所指向的数据可以修改，但指针值（包含的地址）保持固定且不可更改。我们还在第 11 行将所指向的布尔值初始化为`true`。这种数据初始化并没有增加程序的稳定性，但增加了输出的可靠性。这些步骤确保了指针在程序的剩余部分是有效的，并且在每种输入组合下都在第 19 行安全释放。

#### 检查使用`new`的分配请求是否成功

在我们目前为止的代码中，我们假设`new`会返回一个指向内存块的有效指针。事实上，`new`通常会成功，除非应用程序请求了异常大量的内存，或者系统处于这样一种关键状态，以至于没有空闲内存。某些应用程序需要请求大块内存（例如，数据库应用程序）。此外，不简单地假设内存分配请求总是成功的是好的。C++ 为你提供了两种可能的方法，以在你在使用指针之前确保它是有效的。默认方法——即我们迄今为止一直使用的方法——使用`exceptions`（异常），其中分配失败会导致`throw`（抛出）一个类型为`std::bad_alloc`的异常。异常会导致应用程序的执行被中断，除非你编写了`exception handler`（异常处理程序），否则你的应用程序将以一种不优雅的方式结束，并显示错误消息“unhandled exception”（未处理异常）。

异常在第 28 节“异常处理”中进行了详细解释。列表 8.15 让你预览如何使用异常处理来检查失败的分配请求。如果在这个阶段觉得异常处理扑朔迷离，不要太担心——在这里提到它只是为了内存分配主题的完整性。你可以在学习完第 28 节后再次查看此示例。

**列表 8.15** 处理异常，当`new`失败时优雅退出

```cpp
#include <iostream>

using namespace std;

// 移除 try-catch 块以查看此程序的崩溃

int main()

{

    try

    {

        // 请求大量的内存！

        int* pointsToManyNums = new int [0x1fffffff];

        // 使用分配的内存

        delete[] pointsToManyNums;

    }

    catch (bad_alloc)

    {

        cout << "Memory allocation failed. Ending program" << endl;

    }

    return 0;

}
```

输出 ![Image](img/arrow.jpg)

Memory allocation failed. Ending program

分析 ![Image](img/arrow.jpg)

此程序在你的计算机上执行情况可能会不同。我的环境未能成功为 536870911 个整数分配请求的空间！如果我没有编写异常处理程序（你在 14–17 行看到的`catch`块），程序将非常狼狈地结束。你可以通过注释第 6、7 行和 13–17 行来实验在没有异常处理程序的情况下程序的行为。在使用 Microsoft Visual Studio 构建的调试模式二进制文件时，程序执行结果如图 8.2 所示。

![Image](img/08fig02.jpg)

**图 8.2** 列表 8.15 中缺少异常处理时的程序崩溃（使用 MSVC 编译器的调试版本）。

异常处理`try-catch`结构因此帮助应用程序在通知用户内存分配问题阻碍正常执行后，进行受控退出。

对于那些不想依赖异常的人，有一种`new`的变体称为`new(nothrow)`。这种变体在分配失败时不会抛出异常，而是导致运算符`new`返回`NULL`。因此，在使用赋值的指针之前可以相对于`NULL`检查其有效性。参见列表 8.16。

**列表 8.16** 使用`new(nothrow)`在分配失败时返回`NULL`

```cpp
#include <iostream>

using namespace std;

int main()

{

    // 请求大量的内存空间，使用 nothrow

    int* pointsToManyNums = new(nothrow) int [0xfffffff];

    if (pointsToManyNums) // 检查 pointsToManyNums != NULL

    {

        // 使用分配的内存

        delete[] pointsToManyNums;

    }

    else

    {

        cout << "Memory allocation failed. Ending program" << endl;

    }

    return 0;

}
```

输出 ![Image](img/arrow.jpg)

Memory allocation failed. Ending program

分析 ![Image](img/arrow.jpg)

列表 8.16 与列表 8.15 的函数相同，区别在于它使用了`new(nothrow)`。由于这种变体形式`new`在分配失败时返回`NULL`，因此我们在第 8 行在使用之前检查了指针。`new`的两种变体都是好的，选择由你决定。

### 指针最佳实践

在应用程序中使用指针时，有一些基本规则会让你的生活变得更容易。

### 应该 (DO)

**应该** 始终初始化指针变量，否则它们将包含垃圾值。

**应该** 确保在使用指针之前内存是有效的。

**应该** 记住在不再需要内存时释放内存。

#### 不要 (DON'T)

**不要** 在指针未初始化时使用它。

**不要** 在指针释放后访问它。

**不要** 忘记释放不再需要的内存。

## 什么是引用？

引用是变量的别名。当你声明引用时，你需要对其进行初始化。因此，引用是访问存储在变量中的数据的另一种方式。

你会使用引用运算符`&`来声明引用，如下所示：

```
VarType original;

VarType& Reference = original;
```

要进一步了解如何声明和使用引用，请参见列表 8.17。

**列表 8.17** 证明引用是赋值值的别名

```cpp
#include <iostream>

using namespace std;

int main()

{

    int original = 30;

    cout << "original = " << original << endl;

    cout << "original is at address: " << hex << &original << endl;

    int& ref1 = original;

    cout << "ref1 is at address: " << hex << &ref1 << endl;

    int& ref2 = ref1;

    cout << "ref2 is at address: " << hex << &ref2 << endl;

    cout << "Therefore, ref2 = " << dec << ref2 << endl;

    return 0;

}
```

输出 ![Image](img/arrow.jpg)

original = 30

original is at address: 0099F764

ref1 is at address: 0099F764

ref2 is at address: 0099F764

Therefore, ref2 = 30

分析 ![Image](img/arrow.jpg)

输出证明了引用，无论是像第 12 行那样初始化为引用，都指向原始变量所在的相同内存位置。因此，引用是真正的别名——也就是说，`original`的另一个名称。在第 14 行使用`ref2`显示值与第 6 行使用`original`获取的值相同，因为`ref2`别名`original`并且位于相同的内存位置。

### 为什么引用很有用？

引用（References）允许你对初始化所在的内存位置进行操作。这使得引用在编写函数时特别有用。正如你在第 7 节中所学的，“使用函数组织代码”，一个典型的函数声明如下：

```
ReturnType DoSomething(Type parameter);
```

函数`DoSomething()`的调用方式如下：

```
ReturnType Result = DoSomething(argument); // 函数调用
```

上述代码会导致`argument`被复制到`Parameter`中，然后由函数`DoSomething()`使用。如果涉及的`argument`消耗大量内存，这个复制步骤可能会产生相当大的开销。同样，当`DoSomething()`返回一个值时，它会被再次复制到`Result`。如果我们能够避免或消除这些复制步骤，让函数直接处理调用者栈中的数据，那将是理想的。引用恰恰允许你做到这一点。

不包含复制步骤的版本如下：

```
ReturnType DoSomething(Type& parameter); // 注意引用&
```

该函数的调用方式如下：

```
ReturnType Result = DoSomething(argument);
```

由于参数是通过引用传递的，`Parameter`并不是`argument`的副本，而是后者的一个别名，就像列表 8.17 中的`Ref`一样。此外，接受引用作为参数的函数可以选择使用引用参数来返回值。请参考列表 8.18 以了解函数如何使用引用代替返回值。

### 列表 8.18 通过引用参数返回计算平方的函数

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: void GetSquare(int& number)



4: {

5:     number *= number;

6: }

7:

8: int main()

9: {

10:     cout << "Enter a number you wish to square: ";

11:     int number = 0;

12:     cin >> number;

13:

14:     GetSquare(number);

15:     cout << "Square is: " << number << endl;

16:

17:     return 0;

18: }

```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

Enter a number you wish to square: 5

Square is: 25

## 分析 ![Image](img/arrow.jpg)

执行平方操作的函数位于第 3–6 行。注意它是如何通过引用参数接收待平方的数字并以相同方式返回结果的。如果你忘记将参数 `number` 标记为引用（`&`），结果将无法到达调用函数 `main()`，因为 `GetSquare()` 将会在 `number` 的本地副本上执行操作，该副本会在函数退出时被销毁。使用引用，你可以确保 `GetSquare()` 在 `main()` 中定义 `number` 的相同地址空间内运行。因此，即使在函数 `GetSquare()` 退出后，`main()` 中依然可用。

在该示例中，包含用户发送数字的输入参数被修改了。如果你需要两个值（原始值和平方值），可以让函数接受两个参数：一个包含输入，另一个提供平方值。

### 在引用上使用 `const` 关键字

你可能需要某些不允许更改所别名原始变量值的引用。在声明此类引用时使用 `const` 是实现该目标的方法：

点击此处查看代码图像

```cpp

int original = 30;

const int& constRef = original;

constRef = 40; // 不允许：constRef 无法改变 original 中的值

int& ref2 = constRef; // 不允许：ref2 不是 const

const int& constRef2 = constRef; // 允许

```

#### 将参数通过引用传递给函数

引用的主要优势之一是它们允许被调用函数直接处理未从调用者函数复制的参数，从而显著提高性能。然而，由于被调用函数是直接在调用者函数的栈上使用参数工作，因此确保被调用函数无法更改调用者端变量的值通常是重要的。

### 列表 8.19 使用 `const` 引用确保调用函数无法修改值

点击此处查看代码图像

* *

```cpp

0: #include <iostream>

1: using namespace std;

2:

3: void GetSquare(const int& number, int& result)

4: {

5:     result = number * number;

6: }

7:

8: int main()

9: {

10:     cout << "Enter a number you wish to square: ";

11:     int number = 0;

12:     int square = 0;

13:     cin >> number;

14:

15:     GetSquare(number, square);

16:     cout << "Square is: " << square << endl;

17:

18:     return 0;

19: }

```

* *

点击此处查看代码图像

```cpp

int* pointToAnInt = new int;

int* pCopy = pointToAnInt;

```

### 我难道不应该对两者都调用 `delete` 以确保内存被释放吗？

**A** 这种做法是错误的。你只允许对由 `new` 返回的地址调用一次 `delete`。此外，理想情况下，你应该避免让两个指针指向同一个地址，因为对其中任何一个执行 `delete` 都会使另一个失效。你的程序编写方式也不应该导致你对所用指针的有效性产生任何不确定性。

### Q 我在什么时候应该使用 `new(nothrow)`？

**A** 如果你不想处理 `std::bad_alloc` 异常，你可以使用 `nothrow` 版本的 `new` 运算符，如果请求的内存分配失败，它将返回 `NULL`。

### Q 我可以使用以下两种方法调用函数来计算面积：

点击此处查看代码图像

```cpp

void CalculateArea (const double* const ptrRadius, double* const ptrArea);

void CalculateArea (const double& radius, double& area);

```

### 我应该优先选择哪种变体？

**A** 使用后者的引用方法，因为引用不会失效，而指针可能会。此外，这种方式也更简单。

## Q 我有一个指针：

点击此处查看代码图像

```cpp

int number = 30;

const int* pointToAnInt = &number;

```

### 我明白由于 `const` 声明，我无法通过指针 `pointToAnInt` 改变 `number` 的值。我可以将 `pointToAnInt` 赋值给非 `const` 指针，然后使用它来操作整数 `number` 包含的值吗？

**A** 不，你不能改变指针的 `const` 属性：

点击此处查看代码图像

```cpp

int* pAnother = pointToAnInt; // 不能将 const 指针赋值给非 const 指针

```

### Q 我为什么要要费劲通过引用向函数传递值？

**A** 只要它不对你的程序性能产生太大影响，你就不需要这样做。然而，如果你的函数参数接收的对象非常沉重（字节数很大），那么按值传递将是非常昂贵的操作。使用引用会让你的函数调用效率高得多。记住大量地使用 `const`，除非函数需要将结果存储在变量中。

### Q 这两个声明处声明之间有什么区别：

点击此处查看代码图像

```cpp

int myNumbers[100];

int* myArrays[100];

```

**A** `myNumbers` 是一个整数数组——也就是说，`myNumbers` 是一个指向包含 100 个整数的内存位置的指针，指向索引 0 的第一个。它是以下形式的静态替代：

点击此处查看代码图像

```cpp

int* myNumbers = new int [100]; // 动态分配的数组

// 使用 myNumbers

delete[] myNumbers;

```

`myArrays` 另一方面是一个包含 100 个指针的数组，每个指针都可以指向一个整数或一个整数数组。

## 工作坊

工作坊提供了测验题，以帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用所学内容的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，并在继续下一节之前确保你已经理解了这些答案。

### 测验

**1.** 为什么你不能将 `const` 引用赋值给非 `const` 引用？

**2.** `new` 和 `delete` 是函数吗？

**3.** 指针变量中包含的值的本质是什么？

**4.** 你应该使用什么运算符来访问指针指向的数据？

### 练习题

**1.** 执行这些语句时显示的内容是：

点击此处查看代码图像

```cpp

0: int number = 3;

1: int* pNum1 = &number;

2: *pNum1 = 20;

3: int* pNum2 = pNum1;

4: number *= 2;

5: cout << *pNum2;

```

**2.** 这三个重载函数之间的相似点和不同之处是：

点击此处查看代码图像

```cpp

int DoSomething(int num1, int num2);

int DoSomething(int& num1, int& num2);

int DoSomething(int* pNum1, int* pNum2);

```

**3.** 如何修改第 1 行的声明，使得第 3 行的赋值无效？（提示：这与指针指向的数据有关）

**4.** **错误查找：** 以下代码哪里出了问题？

点击此处查看代码图像

```cpp

#include <iostream>

using namespace std;

int main()

{

    int *pointToAnInt = new int;

    pointToAnInt = 9;

    cout << "The value at pointToAnInt: " << *pointToAnInt;

    delete pointToAnInt;

    return 0;

}

```

**5.** **错误查找：** 以下代码哪里出了问题？

点击此处查看代码图像

```cpp

#include <iostream>

using namespace std;

int main()

{

    int *pointToAnInt = new int;

    pointToAnInt = 9;

    cout << "The value at pointToAnInt: " << *pointToAnInt;

    delete pointToAnInt;

    return 0;

}

```

**6.** 修正后上述程序的输出是什么？

# 第二部分：面向对象编程基础

# 第 9 节：类与对象

到目前为止，你已经探索了从 `main()` 开始、包含局部变量和常量、并将执行逻辑组织成接受参数并返回值的简单程序。我们到为止的风格是*过程化的*，我们还没有观察过面向对象的方法。换句话说，现在你需要学习使用 C++ 进行面向对象编程的基础。

## 类与对象的概念

想象你正在编写一个模拟人类的程序，就像你自己一样。这个人类需要一个身份：姓名、出生日期、出生地和性别——这些是使他独特的信息。此外，人类还可以执行某些功能，如说话和介绍自己等。因此，人类也可以像图 9.1 (#ch09.html_ch09fig01) 所示进行建模。

**图 9.1** 人类的宽泛表示。

点击此处查看代码图像

```cpp

class Human

{

   // 成员属性：

   string name;

   string dateOfBirth;

   string placeOfBirth;

   string gender;

   // 成员函数：

   void Talk(string textToTalk);

   void IntroduceSelf();

   ...

};

```

不言而喻，`IntroduceSelf()` 使用了 `Talk()` 以及封装在 `class Human` 内部的一些数据属性。因此，在 `class` 关键字中，C++ 为你提供了一种创建自定义数据类型的强大方式，允许你封装可以使用这些属性的属性和函数。在这种情况下，类的所有属性（例如 `name`、`dateOfBirth`、`placeOfBirth` 和 `gender`）以及在其中声明的所有函数（即 `Talk()` 和 `IntroduceSelf()`）被称为类 `Human` 的成员。

封装是将数据和使用数据的函数在逻辑上分组的能力，是面向对象编程的一个重要特性。

***

**注意**

你经常会遇到 *method*（方法）一词——这些本质上是 `class` 的成员函数。

***

### 作为类实例的对象

类就好比一个蓝图，单独声明一个类对程序的执行没有影响。类在程序执行时在现实世界中的化身是 *object*（对象）。要使用类的功能，你通常会创建该类的实例，称为对象。你使用该对象来访问其成员方法和属性。

创建一个 `class Human` 类型的对象与创建另一个类型的实例（例如 `double`）类似：

点击此处查看代码图像

```cpp

double pi= 3.1415;  // 一个 double 类型的变量

Human  firstMan;  // firstMan: 一个 Human 类的对象

```

或者，你也可以使用 `new` 动态创建一个 `class Human` 的实例，就像创建另一个类型（例如 `int`）一样：

点击此处查看代码图像

```cpp

int* pointsToNum = new int;  // 动态分配的整数

delete pointsToNum;  // 使用后释放内存

Human* firstWoman = new Human(); // 动态分配的 Human

delete firstWoman;  // 释放内存

```

### 使用点运算符 (`.`) 访问成员

人类的一个可以是 Adam，男性，1970 年出生于阿拉巴马州。实例 `firstMan` 是 `class Human` 的对象，是该类在现实中（即运行时）存在的化身：

点击此处查看代码图像

```cpp

Human  firstMan;  // 一个 Human 的实例即对象

```

正如类声明所示，`firstMan` 拥有如 `dateOfBirth` 等属性，可以使用点运算符 (`.`) 进行访问：

点击此处查看代码图像

```cpp

firstMan.dateOfBirth = "1970";

```

这是因为属性 `dateOfBirth` 属于类 `Human`，正如类声明所示，它是其蓝图的一部分。该属性只有在对象被实例化后才在现实中（即在运行时）存在。点运算符 (`.`) 帮助你访问对象的属性。

对于 `IntroduceSelf()` 等方法也是如此：

点击此处查看代码图像

```cpp

firstMan.IntroduceSelf();

```

如果你有一个指向 `class Human` 实例的指针 `firstWoman`，你可以直接使用指针运算符 (`->`) 访问成员（如下一节所示），也可以使用间接运算符 (`*`) 引用对象：

点击此处查看代码图像

```cpp

(*firstWoman).IntroduceSelf();

```

***

**注意**

命名规范同样适用。类名和成员函数使用帕命名命名（Pascal case），例如 `IntroduceSelf()`。类属性使用驼峰命名法（camel case），例如 `dateOfBirth`。

当我们实例化一个类时，我们声明了一个类型为该类的变量。因此我们使用了一直以来用于变量的驼峰命名法，例如 `firstMan`。

***

### 使用指针运算符 (`->`) 访问成员

如果对象是使用 `new` 分配在堆上的，或者你有一个指向对象的指针，那么你可以使用指针运算符 (`->`) 来访问成员属性和函数：

点击此处查看代码图像

```cpp

Human* firstWoman = new Human();

firstWoman->dateOfBirth = "1970";

firstWoman->IntroduceSelf();

delete firstWoman;

```

一个带有 `public` 关键字的可编译形式 `class Human` 由 列表 9.1 所示。

**列表 9.1 可编译的类-Human**

点击此处查看代码图像

***

```cpp

#include <iostream>

#include <string>

using namespace std;

class Human {

public:

    string name;

    int age;

    void IntroduceSelf() {

        cout << "I am " << name << " and " << age << " years old" << endl;

    }

};

int main() {

    Human firstMan;

    firstMan.name = "Adam";

    firstMan.age = 30;

    Human firstWoman;

    firstWoman.name = "Eve";

    firstWoman.age = 28;

    firstMan.IntroduceSelf();

    firstWoman.IntroduceSelf();

}

```

**输出：**

```

I am Adam and 30 years old

I am Eve and 28 years old

```

假设有一个名为 `eve` 的 `Human` 类实例：

```cpp

Human eve;

```

当该实例的用户尝试访问成员 `age` 时：

点击此处查看代码图像

```cpp

cout << eve.age; // 编译错误

```

此时，用户将得到一个编译错误，内容类似于“错误：`Human::age`——无法访问在类 `Human` 中声明的私有成员。”。获取 `age` 的唯一许可方式是通过 `class Human` 提供的公共方法 `GetAge()` 来请求它，而该方法的实现方式是由类的程序员认为的暴露 `age` 的恰当方式决定的：

点击此处查看代码图像

```cpp

cout << eve.GetAge(); // OK



如果`Human`类的程序员有此意，他可以使用`GetAge()`让Eve显示出的年龄比实际年龄要年轻！换句话说，这意味着C++允许类来控制它想要暴露的属性以及以什么方式暴露这些属性。如果`class Human`没有实现`GetAge()`公共成员方法，那么该类实际上确保了用户无法查询`age`。这一特性在本文节稍后解释的情况下可能非常有用。

同样地，`Human::age`也无法直接赋值：

```cpp
eve.age = 22; // 编译错误
```

设置年龄的唯一许可方式是通过方法`SetAge()`：

```cpp
eve.SetAge(22); // OK
```

这有许多优势。`SetAge()`的当前实现只是直接设置成员变量`Human::age`。然而，你可以使用`SetAge()`来验证所设置的`age`是否为零且非负，从而对对外部输入进行验证：

```cpp
class Human
{
private:
   int age;

public:
   void SetAge(int humansAge)
   {
      if (humansAge > 0)
         age = humansAge;
   }
};
```

因此，C++允许类设计者控制类的数据属性如何被访问和操作。

## 通过关键字`private`实现数据抽象

C++在允许你设计一个类作为封装数据和操作这些数据的方法的容器的同时，也赋予了你权力，通过`private`关键字来决定哪些信息对外部世界是不可访问的（即在类外部不可用）。同时，你也有可能通过声明为`public`的方法，允许对被声明为`private`的信息进行受控访问。因此，你对类的实现可以抽象出该类外部类和函数不需要访问的成员信息。

回到关于`Human::age`是私有成员的示例，你知道即使在现实中，许多人也不喜欢透露真实年龄。如果要求`class Human`提供一个比当前年龄小两岁的年龄，它可以通过公共函数`GetAge()`轻松实现，该函数使用`Human::age`参数，将其减二，并提供结果，如列表9.2所示。

**列表9.2** 类`Human`的模型，其中真实的`age`被用户抽象，并报告了一个较年轻的`age`

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Human
4: {
5: private:
6:     // 私有成员数据：
7:     int age;
8:
9: public:
10:     void SetAge(int inputAge)
11:     {
12:         age = inputAge;
13:     }
14:
15:     // Human 关于他/她的年龄撒谎（如果超过 30 岁）
16:     int GetAge()
17:     {
18:         if (age > 30)
19:             return (age - 2);
20:         else
21:             return age;
22:     }
23: };
24:
25: int main()
26: {
27:     Human firstMan;
28:     firstMan.SetAge(35);
29:
30:     Human firstWoman;
31:     firstWoman.SetAge(22);
32:     cout << "Age of firstMan " << firstMan.GetAge() << endl;
33:     cout << "Age of firstWoman " << firstWoman.GetAge() << endl;
34:     return 0;
35: }
```

输出：
```
Age of firstMan 33
Age of firstWoman 22
```

分析：注意第16行的公共方法`Human::GetAge()`。由于私有成员`Human::age`中包含的实际年龄无法直接访问，该类的用户在查询`class Human`对象的属性时，唯一的途径就是`GetAge()`。因此，私有成员`Human::age`中的实际年龄对外部世界是抽象的。事实上，我们的`Human`对于大于30岁的人在年龄上撒了谎。

抽象是面向对象语言中的一个重要概念。它赋予了程序员决定哪些类属性对类是可见的（（那些声明为“朋友”的成员除外）。

## 构造函数

构造函数是一个在实例化类时调用的特殊函数（或方法），用于构造对象。就像函数一样，构造函数也可以重载。

### 声明和实现构造函数

构造函数是一个没有返回类型且没有返回值的特殊函数。因此`class Human`的构造函数声明如下：

```cpp
class Human
{
public:
   Human();
```

构造函数可以在类内联实现，也可以在类外部实现。在类内部实现如下：

```cpp
class Human
{
public:
   Human()
   {
   }
};
```

在类外定义构造函数的变体如下：

```cpp
class Human
{
public:
   Human(); // 构造函数声明
};

// 构造函数实现
Human::Human()
{
}
```

注意`::`称为作用域运算符。例如，`Human::dateOfBirth`指的是`Human`类作用域内的变量`dateOfBirth`。而`::dateOfBirth`则指向全局作用域下的另一个变量`dateOfBirth`。

#### 何时以及如何使用构造函数

构造函数在对象创建、类实例化时总是会被调用。这使得构造函数成为你初始化整数、指针等类成员变量的理想位置。再次查看列表9.2。注意，如果你忘记调用`SetAge()`，整数变量`Human::age`可能包含未知值，因为它没有初始化（尝试注释掉第28行和第31行）。列表9.3使用构造函数实现了一个更好的`class Human`版本，变量`age`已经初始化。

```cpp
34: int main()
{
    Human firstWoman;
    firstWoman.SetName("Eve");
    firstWoman.SetAge (28);
    firstWoman.IntroduceSelf();
}
```

输出：
```
构造了一个`Human`类的实例
我是Eve，今年28岁
```

### 分析

在输出中，你看到一行表示对象构造的新行。现在，观察第34–41行定义的`main()`。你会发现输出的第一行是第36行创建（构造）对象`firstWoman`的结果。第11–15行中的构造函数`Human::Human()`包含了产生该输出的`cout`语句。注意构造函数是如何将整数`age`初始化为0的。如果你忘记在新构造的对象上调用`SetAge()`，你可以放心，构造函数已经确保了变量`age`中包含的值不是随机整数（那看起来可能是有效的），而是0。

### 注意

不带参数的情况下调用的构造函数被称为默认构造函数。编写默认构造函数是可选的。

如果你没有编写任何构造函数，如列表9.1所示，编译器会为你创建一个（它会构造成员属性，但不会将普通数据类型如`int`）初始化为任何特定的非零值）。

### 构造函数的重载

构造函数可以像函数一样被重载。因此，我们可以写一个在实例化`Human`时需要将名称作为参数的构造函数，例如：

```cpp
class Human
{
public:
    Human()
    {
        // 此处是默认构造函数的代码
    }

    Human(string humansName)
    {
        // 此处是重载构造函数的代码
    }
};
```

重载构造函数的应用在列表9.4中通过，通过在构造时提供名称来创建`Human`类的对象。

**列表9.4** 具有多个构造函数的`Human`类

```cpp
0: #include <iostream>
1: #include <string>
2: using namespace std;
3:
4: class Human
5: {
6: private:
7:     string name;
8:     int age;
9:
10: public:
11:     Human() // 默认构造函数
12:     {
13:         age = 0; // 初始化以确保没有垃圾值
14:         cout << "Default constructor: name and age not set" << endl;
15:     }
16:
17:     Human(string humansName, int humansAge) // 重载
18:     {
19:         name = humansName;
20:         age = humansAge;
21:         cout << "Overloaded constructor creates ";
22:         cout << name << " of " << age << "years" << endl;
23:     }
24: };
25:
26: int main()
27: {
28:     Human firstMan; // 使用默认构造函数
29:     Human firstWoman ("Eve", 20); // 使用重载构造函数
30: }
```

输出：
```
Default constructor: name and age not set
Overloaded constructor creates Eve of 20 years
```

### 分析

第26–30行的`main()`函数非常简单，创建了两个`Human`类的实例。`firstMan`使用默认构造函数，而`firstWoman`使用重载构造函数，在实例化时提供了名称和年龄。输出仅是对象构造的结果！你可能会体会到，如果`class Human`选择不支持默认构造函数，那么`main()`将没有选项使用以名称和年龄为先决条件的重载构造函数来构造每个`Human`对象——这使得在不提供名称或年龄的情况下无法创建`Human`。

### 提示

你可以选择不实现默认构造函数，以强制使用某些最小参数进行对象实例化，正如下一节解释的那样。

### 没有默认构造函数的类

在列表9.5中，请看没有默认构造函数的`class Human`如何强制创建者提供名称和年龄作为创建对象的的先决条件。

**列表9.5** 具有重载构造函数且没有默认构造函数的类

```cpp
0: #include <iostream>
1: #include <string>
2: using namespace std;
3:
4: class Human
5: {
6: private:
7:     string name;
8:     int age;
9:
10: public:
11:     Human(string humansName, int humansAge)
12:     {
13:         name = humansName;
14:         age = humansAge;
15:         cout << "Overloaded constructor creates ";
16:     }
17:
18:     void IntroduceSelf()
19:     {
20:         cout << "I am " << name;
21:         cout << age << " years old" << endl;
22:     }
23: };
24:
25: int main()
26: {
27:     Human firstMan("Adam", 25);
28:     Human firstWoman("Eve", 28);
29:
30:     firstMan.IntroduceSelf();
31:     firstWoman.IntroduceSelf();
32: }
```

输出：
```
Overloaded constructor creates Adam of 25
Overloaded constructor creates Eve of 28
I am Adam and 25 years old
I am Eve and 28 years old
```

### 分析

此版本的`class Human`只有一个接受`string`和`int`输入的构造函数。没有默认构造函数，且由于存在重载构造函数，C++编译器不会为你生成默认构造函数。这很好地模拟了现实世界的场景；你出生时就有名字，但没有人有权限更改它。

### 带有默认值的构造函数参数

就像函数可以带有默认参数一样，构造函数也可以。你在接下来的代码中看到的是列表9.5第11行的略微修改版本，其中`age`参数具有默认值25：

```cpp
class Human
{
private:
    string name;
    int age;

public:
    // 重载构造函数（无默认构造函数）
    Human(string humansName, int humansAge = 25)
    {
        name = humansName;
        age = humansAge;
        cout << "Overloaded constructor creates " << name;
        cout << " of age " << age << endl;
    }
    // ... 其他成员
};
```

此类类可以使用以下语法实例化：

`Human adam("Adam");` // `adam.age`被赋予默认值25

`Human eve("Eve", 18);` // `eve.age`被赋予指定的18

### 注意

注意，默认构造函数是指可以在不带参数的情况下实例化的函数，而不一定是不带参数的。因此，这个带有两个默认值的值的构造函数就是默认构造函数：

```cpp
class Human
{
private:
    string name;
    int age;

public:
    // 两个参数都有默认值
    Human(string humansName = "Adam", int humansAge = 25)
    {
        name = humansName;
        age = humansAge;
    }
}
```

```cpp
        cout << "Overloaded constructor creates ";
        cout << name << " of age " << age;
    }
};
```

原因是`class Human`仍然可以在不带参数的情况下实例化：

`Human adam;` // `Human`使用默认名称"Adam"，`age 25`

### 使用初始化列表的构造函数

你已经见过构造函数在初始化成员变量时是多么用的。初始化成员的另一种方法是使用*初始化列表*（initialization lists）。列表9.5中初始化列表的构造函数变体如下所示：

```cpp
class Human
{
private:
   string name;
   int age;

public:
   // 用于初始化成员 age 和 name 的两个参数
   Human(string humansName, int humansAge)
       :name(humansName), age(humansAge)
   {
      cout << "Constructed a human called " << name;
      cout << ", " << age << " years old" << endl;
   }
// ... 其他类成员
};



因此，初始化列表的特征是在包含在括号 `(...)` 中的参数声明后跟一个冒号（`:`），然后是一个单独的成员变量及其初始化值。该初始化值可以是参数（如`humansName`），甚至可以是固定值。初始化列表也可以用于带特定参数调用基类构造函数。这些将在第 10 节“实现继承”中再次讨论。

你可以在列表 9.6 中看到一个带有参数默认构造函数、默认值和初始化列表的`class Human`版本。

**列表 9.6** 接受带有默认值的参数的、并使用初始化列表设置成员的默认构造函数

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <string>
2: using namespace std;
3: 
4: class Human
5: {
6: private:
7:     int age;
8:     string name;
9: 
10: public:
11:     Human(string humansName = "Adam", int humansAge = 25)
12:         :name(humansName), age(humansAge)
13:     {
14:         cout << "Constructed a human called " << name;
15:         cout << ", " << age << " years old" << endl;
16:     }
17: };
18: 
19: int main()
20: {
21:     Human adam;
22:     Human eve("Eve", 18);
23: 
24:     return 0;
25: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Constructed a human called Adam, 25 years old
Constructed a human called Eve, 18 years old
```

分析 ![Image](img/arrow.jpg)

带有初始化列表的构造函数可见第 11–16 行，其中你也可以看到为`name`给了默认值`"Adam"`，为`age`给了默认值`25`。因此，当第 21 行创建一个名为`adam`的`class Human`实例且不带参数时，其成员会自动分配默认值。相反，`eve`则如第 22 行所示提供了参数——这些参数在构造期间变为赋值给`Human::name`和`Human::age`的值。

### 注意

也可以使用关键字`constexpr`同样将构造函数定义为常量表达式。在从性能角度来看这种结构有用的特殊情况下，你会在构造函数声明处使用它。

点击此处查看代码图像

```cpp
class Sample
{
const char* someString;
public:
   constexpr Sample(const char* input)
       :someString(input)
   { // 构造函数 }
};
```

## 析构函数

析构函数与构造函数一样，是一个特殊的函数。构造函数在实例化时被调用，而析构函数在对象销毁时自动被调用。

### 声明和实现析构函数

析构函数看起来是一个接收类名的函数，但其前面有一个波浪号（`~`）。因此，`class Human`将有一个如下声明的析构函数：

点击此处查看代码图像

```cpp
class Human
{
   ~Human(); // 析构函数的声明
};
```

该析构函数可以在类内内联实现，也可以在类声明之外实现。类内的实现或定义如下所示：

点击此处查看代码图像

```cpp
class Human
{
public:
   ~Human()
   {
      // 析构函数代码
   }
};
```

允许你在类声明外定义析构函数的变体如下：

点击此处查看代码图像

```cpp
class Human
{
public:
   ~Human(); // 析构函数声明
};

// 析构函数定义（实现）
::~Human()
{
   // 析构函数代码
}
```

如你所见，析构函数的声明与构造函数的声明略有不同，它包含一个波浪号（`~`）。然而，析构函数的作用与构造函数的作用完全相反。

#### 何时以及如何使用析构函数

当类的对象离开作用域或通过`delete`删除而被销毁时，析构函数总是会被调用。这一属性使得析构函数成为重置变量以及释放动态分配的内存和其他资源的理想位置。

本书建议优先使用`std::string`而不是`char*`缓冲区，这样你就不需要担心内存分配和及时释放。`std::string`和其他工具无非是利用构造函数和析构函数的类（此外还有你将在第 12 节所示的示例`MyString`类，它在构造函数中分配内存，在析构函数中释放内存。

**列表 9.7** 通过析构函数确保内存释放的字符缓冲区的简单类

该类基本上在`MyString::buffer`中封装了一个 C 风格字符串，并免除了你手动分配内存的任务；每当你需要使用字符串时，它都会释放该内存。我们最感兴趣的几行是第 9–18 行的构造函数`MyString()`以及第 20–25 行的析构函数`~MyString()`。构造函数通过一个强制性的输入参数强制执行带有输入字符串的构造，然后在第 13 行使用`new`和`strlen`为其分配内存后，将其拷贝到字符数组`buffer`中。`strlen`是标准库提供的一个函数，有助于确定输入字符串的长度。`strcpy`是第 14 行中使用的标准库函数，用于从源`initString`拷贝到由`buffer`指向的新分配内存中。如果类的用户为`initString`提供了`NULL`，则`MyString::buffer`也会初始化为`NULL`（以防止该指针包含随机值，这在访问内存位置时可能是危险的）。析构函数代码的作用是确保在构造函数中分配的内存自动返回给系统。它检查`MyString::buffer`是否为`NULL`，如果是，则对它执行`delete[]`，这与构造函数中的`new`相对应。请注意，在`main()`函数中，程序员从未执行过`new`或`delete`。除了从用户那里抽象出内存管理的实现外，`class MyString`还确保了释放分配内存的逻辑正确性。析构函数`~MyString()`在`main`结束时会被自动调用，这在执行析构函数中的`cout`语句的输出中得到了证明。

处理字符串的类是析构函数的许多适用场景之一。第 26 节“理解智能指针”演示了析构函数在以更智能的方式处理指针时起着怎样的关键作用。

### Note

析构函数不能被重载。一个类只能有一个析构函数。如果你忘记实现析构函数，编译器将创建并调用一个虚拟析构函数，即一个空析构函数（它不对动态分配的内存进行任何清理）。

### 拷贝构造函数

在 第 7 节“使用函数组织代码”中，你学习了传递给类似`Area()`函数（如列表 7.1 所示）的参数会被拷贝：

```cpp
double Area(double radius);
```

因此，当调用`Area()`时，作为参数`radius`发送的内容会被拷贝。这条规则适用于对象，即类的实例。

### 浅拷贝及相关问题

如列表 9.7 所示的`MyString`等类包含一个指针成员`buffer`，它指向动态分配的内存，该内是在构造函数中使用`new`分配，并在析构函数中使用`delete[]`释放。当该类的对象被拷贝时，指针成员会被拷贝，但所指向的内存不会拷贝，导致两个对象指向内存中同一个动态分配缓冲区。当一个对象被析构时，`delete[]`会释放内存，从而使另一个对象持有的指针拷贝失效。这种拷贝是*浅拷贝*的，对程序的稳定性构成了威胁，如列表 9.8 所示。

**列表 9.8** 按值传递如`MyString`等类对象的问题

点击此此处查看代码图片

```cpp
0: #include <iostream>
1: #include <string.h>
2: using namespace std;
3: class MyString
4: {
5: private:
6:     char* buffer;
7: 
8: public:
9:     MyString(const char* initString) //构造函数
10:     {
11:         buffer = NULL;
12:         if(initString != NULL)
13:         {
14:             buffer = new char [strlen(initString) + 1];
15:             strcpy(buffer, initString);
16:         }
17:     }
18: 
19:     ~MyString() // 析构函数
20:     {
21:         cout << "Invoking destructor, clearing up" << endl;
22:     }
```

因此，拷贝构造函数接受一个同类对象的引用作为参数。该参数是源对象的别名，是你用来编写自定义拷贝代码时所使用的句柄。如列表 9.9 所示，你会使用拷贝构造函数来确保源对象中所有缓冲区（buffers）都完成深拷贝（deep copy）。

### 列表 9.9 定义拷贝构造函数以确保对动态分配的缓冲区进行深拷贝

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <string.h>
2: using namespace std;
3: class MyString
4: {
5: private:
6:     char* buffer;
7: 
8: public:
9:     MyString(const char* initString) // 构造函数
10:     {
11:         buffer = NULL;
12:         cout << "Default constructor: creating new MyString" << endl;
13:         if(initString != NULL)
14:         {
15:             buffer = new char [strlen(initString) + 1];
16:             strcpy(buffer, initString);
17: 
18:             cout << "buffer points to: 0x" << hex;
19:             cout << (unsigned int*)buffer << endl;
20:         }
21:     }
22: 
23:     MyString(const MyString& copySource) // 拷贝构造函数
24:     {
25:         buffer = NULL;
26:         cout << "Copy constructor: copying from MyString" << endl;
27:         if(copySource.buffer != NULL)
28:         {
29:             // 分配自己的缓冲区
30:             buffer = new char [strlen(copySource.buffer) + 1];
31: 
32:             // 从源对象深拷贝到本地缓冲区
33:             strcpy(buffer, copySource.buffer);
34: 
35:             cout << "buffer points to: 0x" << hex;
36:             cout << (unsigned int*)buffer << endl;
37:         }
38:     }
39: 
40:     // 析构函数
41:     ~MyString()
42:     {
43:         cout << "Invoking destructor, clearing up" << endl;
44:         delete [] buffer;
45:     }
46: 
47:     int GetLength()
48:     { return strlen(buffer); }
49: 
50:     const char* GetString()
51:     { return buffer; }
52: };
53: 
54: void UseMyString(MyString str)
55: {
56:     cout << "String in MyString is " << str.GetLength();
57:     cout << " characters long" << endl;
58: 
59:     cout << "buffer contains: " << str.GetString() << endl;
60:     return;
61: }
62: 
63: int main()
64: {
65:     MyString sayHello("Hello from Class");
66:     UseMyString(sayHello);
67:     return 0;
68: }
```

**输出**

```
Default constructor: creating new MyString
buffer points to: 0x1232D9
Copy constructor: copying from MyString
buffer points to: 0x1232DD
String in MyString is 17 characters long
buffer contains: Hello from Class
Invoking destructor, clearing up
Invoking destructor, clearing up
```

### 分析

大部分代码与列表 9.8 相似，不同在于第 23–38 行创建了新副本。首先，让我们关注`main()`函数，它（和之前一样）在第 65 行创建了对象`sayHello`。创建`sayHello`会导致输出的第一行产生，这是来自`MyString`构造函数的第 12 行输出。为了方便起见，构造函数还显示了`buffer`指向的内存地址。随后，`main()`在第 66 行通过值传递将`sayHello`传递给函数`UseMyString()`，如输出所示，这会自动导致拷贝构造函数的调用。拷贝构造函数中的代码与构造函数中的代码相似。基本思想相同：在第 30 行检查拷贝源中包含的 C 风格字符串`buffer`的长度，在自己的`buffer`实例中分配等比例的内存，然后在第 33 行使用`strcpy`从源拷贝到目标。这并不是指针值的浅拷贝（shallow copy）。这是一种深拷贝，即被指向的内容被拷贝到属于该对象的新分配缓冲区中，如图 9.4 所示。

![Image](img/09fig04.jpg)

**图 9.4** 调用函数`UseMyString()`时，将参数`sayHello`深拷贝到参数`str`的示意。

列表 9.9 中的输出表明，拷贝后的`buffer`指向的内存地址是不同的——也就是说两个对象没有指向同一个动态内存地址。因此，当函数`UseMyString()`返回且参数`str`被销毁时，析构函数代码会对拷贝构造函数中分配且属于该对象的内存地址执行`delete[]`。通过这样做，它没有触及`main()`中`sayHello`所指向的内存。因此，两个函数都结束了，它们各自的对象也成功且和平地被销毁，而没有导致应用程序崩溃。

### 注意

拷贝构造函数已经在像函数调用这样的情况下确保了深拷贝：

点击此处查看代码图像

```cpp
MyString sayHello("Hello from Class");
UseMyString(sayHello);
```

然而，如果你尝试通过赋值来拷贝会怎样：

点击此处查看代码图像

```cpp
MyString overwrite("who cares? ");
overwrite = sayHello;
```

这仍然是一个浅拷贝，因为你还没有提供拷贝赋值运算符`operator=`。在没有提供该运算符的情况下，编译器为你提供了一个执行浅拷贝的默认实现。

拷贝赋值运算符将在 12 节中讨论。列表 12.8 是一个实现了相同功能的`MyString`：

点击此处查看代码图像

```cpp
MyString&operator= (const MyString& copySource)
{
    //... 拷贝赋值代码
}
```




### 注意

在拷贝构造函数声明中使用 `const` 可以确保拷贝构造函数修改被引用的对象。

此外，拷贝构造函数的参数必须以引用传递。如果不是引用，拷贝构造函数本身就会调用拷贝，从而递归调用，直到系统耗尽内存。

### 做

- 当你的类包含原始指针成员（`char*` 等）时，务必编写拷贝构造函数和拷贝赋值运算符。
- 务必使用 `const` 引用编写拷贝构造函数。
- 使用 `explicit` 关键字避免隐式转换。
- 使用 `std::string` 等字符串类和智能指针类作为成员，而不是原始指针，因为它们已经实现了拷贝构造，可以节省你的精力。

### 不要

- 除非绝对避免，否则不要使用原始指针作为成员。

### 注意

带有原始指针成员 `char* buffer` 的 `MyString` 类被用作示例来解释拷贝构造函数的需要。

如果你编写一个需要包含存储名称等数据的类，使用 `std::string` 而不是 `char*`，在没有原始指针的情况下可能不需要拷贝构造函数。这是因为编译器插入的默认拷贝构造函数会确保调用成员对象（如 `std::string`）的所有可用拷贝构造函数。

## 移动构造函数提高性能

由于语言及其需求，某些情况下对象会自动执行拷贝步骤。考虑以下内容：

点击此处查看代码图像

```cpp
class MyString
{
    // 取列表 9.9 中的实现
};

MyString Copy(MyString& source) // 函数
{
    MyString copyForReturn(source.GetString()); // 创建拷贝
    return copyForReturn; // 返回值调用拷贝构造函数
}

int main()
{
    MyString sayHello("Hello World of C++");
    MyString sayHelloAgain(Copy(sayHello)); // 调用 2 次拷贝构造函数
    return 0;
}
```

正如注释所示，在 `sayHelloAgain` 的实例化过程中，拷贝构造函数被调用了两次，因此由于我们调用了按值返回 `MyString` 的函数 `Copy(sayHello)`，导致执行了两次深拷贝。然而，这个返回的值是极短存存的，在表达式表达式之外是不可用的。因此，C++ 编译器善意调用的拷贝构造函数对性能是一种负担。如果我们的类包含大型尺寸的对象，这种影响将变得非常显著。

为了避免这种性能瓶颈，从 C++11 开始的 C++ 版本除了拷贝构造函数外还增加了**移动构造函数**（move constructor）。移动构造函数的语法如下：

点击此处查看代码图像

```cpp
// move constructor
MyString(MyString&& moveSource)
{
    if (moveSource.buffer != NULL)
    {
        buffer = moveSource.buffer; // 获取所有权，即“移动”
        moveSource.buffer = NULL; // 将移动源设置为 NULL
    }
}
```

当编写了移动构造函数时，编译器会自动选择该方式来“移动”临时资源，从而避免深拷贝步骤。实现移动构造函数后，注释应相应更改为以下内容：

点击此处查看代码图像

```cpp
MyString sayHelloAgain(Copy(sayHello)); // 触发 1 次拷贝和 1 次移动构造函数
```

移动构造函数通常与移动赋值运算符一起实现，将在第 12 节中进行详细讨论。列表 12.11 是 `class MyString` 的改进版本，它实现了移动构造函数和移动赋值运算符。

## 构造函数与析构函数的不同用途

在这一节中，你学习了一些重要的基础概念，例如构造函数、析构函数以及通过 `public` 和 `private` 等关键字对数据和方法进行抽象。这些概念让你能够创建可以控制其如何被创建、拷贝、销毁或暴露数据的类。

让我们来看一些帮助解决许多重要设计问题的有趣模式。

### 不允许拷贝的类

你被要求为你国家的宪法建模。你的宪法允许存在一位总统。你的 `class President` 存在着以下风险：

点击此处查看代码图像

```cpp
President ourPresident;

DoSomething(ourPresident); // 按值传递时创建了副本

President clone;

clone = ourPresident; // 通过赋值创建了副本
```

显然，你需要避免这种情况。除了建模特定的宪法外，你可能正在编写一个操作系统，并需要建模一个局域网、一个处理器等。你需要确保某些资源不能被拷贝或复制。如果你不声明拷贝构造函数，C++ 编译器会为你插入一个默认的公共拷贝构造函数。这破坏了你的设计并威胁到了你的实现。然而，这种语言为这种设计范式提供了一个解决方案。

你可以通过声明一个 `private` 拷贝构造函数来确保你的类不能被拷贝。这确保了函数调用 `DoSomething(ourPresident)` 将导致编译失败。为了避免赋值，你声明了一个 `private` 赋值运算符。

因此，解决方案如下：

点击此处查看代码图像

```cpp
class President
{
private:
    President(const President&); // 私有拷贝构造函数
    President& operator=(const President&); // 私有拷贝赋值运算符

    // ... 其他属性
};
```

不需要实现私有的拷贝构造函数或赋值运算符。只需将它们声明为私有就足以实现你确保 `class President` 对象不可拷贝的目标。

### 允许单个实例的单例类

之前讨论的 `class President` 很好，但它有一个缺点：它无法帮助通过实例化多个对象来创建多个总统：

```cpp
President One, Two, Three;
```

得益于 `private` 拷贝构造函数，它们单独都是不可拷贝的，但你理想需要的是一个拥有且仅有一个真实世界表现的 `class President`——也就是说，只有一个对象，并禁止创建额外的对象。欢迎来到单例（singleton）概念，它使用私有构造函数、私有赋值运算符和静态实例成员来创建这种（具有争议的）强大的模式。

---

**提示**

当在类数据成员上使用 `static` 关键字时，它确保该成员在所有实例之间共享。

当 `static` 用在函数作用域内声明的局部变量上时，它确保该变量在函数调用之间保留其值。

当 `static` 用在成员函数（方法）上时，该方法在类的所有实例之间共享。

---

`static` 关键字是创建单例类的关键要素，如列表 9.10 所示。

**列表 9.10** 禁止拷贝、赋值和多实例创建的单例 `class President`

点击此处查看代码图像

```cpp
#include <iostream>
#include <string>

using namespace std;

class President
{
private:
    President() {}; // 私有构造函数
    President(const President&); // 私有拷贝构造函数
    const& operator=(const President&); // 赋值运算符

    string name;

public:
    static President& GetInstance()
    {
        static President onlyInstance; // 仅构造一次
        return onlyInstance;
    }

    string GetName()
    {
        return name;
    }

    void SetName(string InputName)
    {
        name = InputName;
    }
};

int main()
{
    President& onlyPresident = GetInstance();
    onlyPresident.SetName("Abraham Lincoln");

    // 取消注释以查看编译失败
    // President second; // 无法访问构造函数
    // President* third = new President(); // 无法访问构造函数
    // President fourth = onlyPresident; // 无法访问拷贝构造函数
    // onlyPresident = GetInstance(); // 无法访问运算符

    cout << "The name of the President is: ";
    cout << GetInstance().GetName() << endl;

    return 0;
}
```

---

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

The name of the President is: Abraham Lincoln

分析 ![Image](img/arrow.jpg)

快速查看第 28–43 行的 `main()`，那里有一系列注释掉的代码，展示了创建 `class President` 的新实例或副本的所有无法编译的组合。让我们逐一分析：

点击此处查看代码图片

```cpp
34: // President second; // 无法访问构造函数
35: // President* third = new President(); // 无法访问构造函数
```

第 34 行和 35 行分别尝试在栈和堆上创建对象并使用默认构造函数，由于它在第 7 行声明为 `private`，因此是不可用的。

点击此处查看代码图片

```cpp
36: // President fourth = onlyPresident; // 无法访问拷贝构造函数
```

第 36 行尝试通过拷贝构造函数创建现有对象的副本（创建时的赋值会触发拷贝构造函数），这在 `main()` 中是不可用的，因为它在第 8 行声明为 `private`：

点击此处查看代码图片

```cpp
37: // OnlyPresident = GetInstance(); // 无法访问运算符=
```

第 37 行尝试通过赋值来创建副本，由于赋值操作符在第 9 行被声明为 `private`，这种方法行不通。因此，`main()` 永远无法创建 `class President` 的实例，唯一的选择如第 30 行所示，即使用静态函数 `GetInstance()` 来获取 `class President` 的实例。由于 `GetInstance()` 是一个静态成员，它就像一个全局函数，可以在没有对象作为句柄的情况下调用。`GetInstance()` 实现在第 14–19 行，它使用静态变量 `onlyInstance` 来确保只创建一个且仅创建一个 `class President` 实例。为了更好地理解这一点，请想象第 17 行只执行一次（静态初始化），因此无论调用多少次 `President::GetInstance()`，`GetInstance()` 都会返回那唯一的可用的 `class President` 实例。

---

### 注意事项

仅在绝对必要时才使用单例模式，并考虑到应用程序及其功能的未来增长。请注意，单例模式这种限制创建多个实例的特性本身，当出现需要该类的多个实例的用例时，可能会成为架构瓶颈。

例如，如果我们的项目从模拟一个国家变为模拟联合国（目前由 193 个成员国组成，每个成员国家都有自己的主席），鉴于一个只允许存在一个实例的单例 `class President`，我们显然将会遇到架构问题。

---

## 禁止在栈上实例化的类

栈空间通常是有限的。如果你正在编写一个内部结构可能包含数 TB（terabytes）数据的数据库，你可能希望确保该类的客户端不能在栈上实例化它；相反，它被强制只能在自由存储（free store）上创建实例。确保此点的关键是将析构函数声明为 `private`：

```cpp
class MonsterDB
{
private:
    ~MonsterDB(); // 私有析构函数

    // ... 消耗大量数据的成员变量
};
```

点击此处查看代码图像

声明私有析构函数可以确保不允许像这样创建实例：

```cpp
int main()
{
    MonsterDB myDatabase; // 编译错误

    // ... 更多代码

    return 0;
}
```

点击此处查看代码图像

此实例如果成功构造，将位于栈上。当栈回退时，栈上的所有对象都会被弹出，因此编译器需要在 `main()` 结束时编译并调用析构函数 `~MonsterDB()`。然而，该析构函数是私有的，因此无法访问，导致编译失败。

`private` 析构函数并不会阻止你在堆上实例化：

```cpp
int main()
{
    MonsterDB* myDatabase = new MonsterDB(); // 无错误

    // ... 更多代码

    return 0;
}
```

点击此处查看代码图像

如果你在该处看到了内存泄漏，你并没有看错。由于无法从 `main` 访问析构函数，你无法执行 `delete`。`class MonsterDB` 类需要的是一个 `public static` 成员函数，用于销毁实例（类成员将拥有访问私有析构函数的权限）。请参见列表 9.11。

**列表 9.11** 仅允许在自由存储上（使用 `new`）创建对象的数据库 `class MonsterDB`

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class MonsterDB
4: {
5: private:
6:     ~MonsterDB() {}; // 私有析构函数防止栈上实例化
7:
8: public:
9:     static void DestroyInstance(MonsterDB* pInstance)
10:     {
11:         delete pInstance; // 成员可以调用私有析构函数
12:     }
13:
14:     void DoSomething() {} // 示例空成员方法
15: };
16:
17: int main()
18: {
19:     MonsterDB* myDB = new MonsterDB(); // 在堆上
20:     myDB->DoSomething();
21:
22:     // 注消下一行查看编译失败
23:     // delete myDB; // 私有析构函数无法调用
24:
25:     // 使用静态成员释放内存
26:     MonsterDB::DestroyInstance(myDB);
27:
28:     return 0;
29: }
```

---

输出 ![Image](img/arrow.jpg)

代码段没有产生输出。

分析 ![Image](img/arrow.jpg)

这段代码的目的仅是为了演示禁止在栈上创建实例的类的编程。第 6 行所示的 `private` 析构函数是关键。第 9–12 行的静态函数 `DestroyInstance()` 用于释放内存，因为 `main()` 无法对 `myDB` 执行 `delete`。你可以通过取消第 23 行的注释测试这一点。

## 使用构造函数进行类型转换

在本节之前，你已经学习了构造函数可以被重载，也就是说它们可以接受一个或多个参数。此功能通常用于将一种类型转换为另一种类型。让我们考虑一个具有重载构造函数的 `class Human`，该构造函数接受一个整数：

```cpp
class Human
{
    int age;

public:
    Human(int a) : age(a) {}
};

// 接受 Human 参数的函数
void DoSomething(Human person)
{
    cout << "Human sent something" << endl;
    return;
}

int main()
{
    Human kid(10); // 整数转换为 Human
    DoSomething(kid); // OK
    return 0;
}
```

点击此处查看代码图像

这种构造函数允许转换：

```cpp
Human kid(10); // 转换为 Human

DoSomething(kid);
```

点击此处查看代码图像

---

### 注意事项

转换构造函数允许隐式转换：

```cpp
Human anotherKid = 11; // int 转换为 Human
DoSomething(10); // 10 转换为 Human
```

点击此处查看代码图像

我们声明 `DoSomething(Human person)` 是一个接受 `Human` 类型的函数，而不接受 `int`！那么，为什么那行代码有效了？编译器知道 `class Human` 支持接受整数的构造函数并执行了隐式转换。

为了避免隐式转换，在声明构造函数时使用 `explicit`：

```cpp
class Human
{
    int age;

public:
    explicit Human(int a) : age(a) {}
};
```




点击此处查看代码图像

`explicit` 不是先决条件，但在许多情况下是一种良好的做法。示例列表 9.12 演示了一个不允许隐式转换的 `class Human` 版本。

***

**列表 9.12** 使用 `explicit` 关键字阻止无意的隐式转换

```cpp
0: #include<iostream>
1: using namespace std;
2:
3: class Human
4: {
5:   int age;
6: public:
7:   // explicit 构造函数阻止隐式转换
8:   explicit Human(int humansAge) : age(humansAge) {}
9: };
10:
11: // 接受 Human 的函数
12: void DoSomething(Human person)
13: {
14:   cout << "Human sent something" << endl;
15:   return;
16: }
17:
18: int main()
19: {
20:   Human kid(10);   // 显式转换 OK
21:   Human anotherKid = Human(11); // 显式，OK
22:   DoSomething(kid); // OK
23:
24:   // Human anotherKid2 = 11; // 失败：不允许隐式转换
25:   // DoSomething(10); // 隐式转换
26:
27:   return 0;
28: }
```

不对输出没有贡献的代码行与有贡献的行同样重要。第 17–27 行的 `main()` 包含了 `class Human` 实例化的变体，该类在第 8 行使用带有 `explicit` 的构造函数进行了声明。能够编译的行是显式转换的尝试，其中使用 `int` 来实例化 `Human`。第 23 和 24 行是涉及隐式转换的变体。这些被注释掉的行在我们移除第 8 行的 `explicit` 关键字后将可以通过编译。因此，此示例演示了 `explicit` 关键字如何防止隐式转换。

### 提示
隐式转换问题以及使用 `explicit` 关键字避免这些转换也适用于运算符。在编写第 12 Lesson 中向你介绍的转换操作符时，记得注意 `explicit` 的用法。

### `this` 指针

C++ 中的一个重要概念，`this` 是一个保留关键字，适用于类作用域，并包含对象的地址。换句话说，`this` 的值是 `&object`。在类成员方法中，当你调用另一个成员方法时，编译器会将 `this` 指针作为一个隐式的、不可见的参数传递给函数调用：

点击此处查看代码图像

```cpp
class Human
{
private:
    void Talk (string Statement)
    {
      cout << Statement;
    }
public:
    void IntroduceSelf()
    {
      Talk("Bla bla"); // same as Talk(this, "Bla Bla")
    }
};
```

你在这里看到的是 `IntroduceSelf()` 方法使用私有成员 `Talk()` 在屏幕上打印一条语句。实际上，编译器在调用 `Talk` 时嵌入了 `this` 指针，即被调用为 `Talk(this, "Bla bla")`。

从编程的角度来看，`this` 并没有太多的应用，除了那些通常是可选的情况。例如，如 Listing 9.2 所示，在 `SetAge()` 中访问 `age` 的代码可以有一个变体：

点击此处查看代码图像

```cpp
void SetAge(int humansAge)
{
    this->age = humansAge;   // same as age = humansAge
}
```

### 注意
注意，`this` 指针不会传递给声明为 `static` 的类方法，因为静态函数与类的实例不相连。相反，它们被所有实例共享。

要在静态函数中使用实例变量，你需要显式地声明一个参数并将 `this` 指针作为参数传递。

### 类的 `sizeof()`

你已经学习了使用 `class` 关键字定义你自定义类型的基础知识，这使你能够封装数据属性和操作该数据的方法。运算符 `sizeof()` 涵盖在第 3 Lesson 中的“使用变量、声明常量”中有所介绍，用于确定特定类型的内存需求（以字节为单位）。该运算符也适用于类，基本上报告类声明中包含的每个数据属性所消耗的字节和。取决于你使用的编译器，`sizeof()` 可能会包含或不包含某些属性在字边界上的填充（padding）。注意，成员函数及其局部变量在定义类的 `sizeof()` 时并不起作用。参见 Listing 9.13。

**LISTING 9.13** 在类及其实例上使用 `sizeof` 的结果

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <string.h>
2: using namespace std;
3: class MyString
4: {
5: private:
6:     char* buffer;
7:
8: public:
9:     MyString(const char* initString) // default constructor
10:     {
11:         buffer = NULL;
12:         if(initString != NULL)
13:         {
14:             buffer = new char [strlen(initString) + 1];
15:             strcpy(buffer, initString);
16:         }
17:     }
18: 
19:     MyString(const MyString& copySource) // copy constructor
20:     {
21:         buffer = NULL;
22:         if(copySource.buffer != NULL)
23:         {
24:             buffer = new char [strlen(copySource.buffer) + 1];
25:             strcpy(buffer, copySource.buffer);
26:         }
27:     }
28: 
29:     ~MyString()
30:     {
31:         delete [] buffer;
32:     }
33: 
34:     int GetLength()
35:     { return strlen(buffer); }
36: 
37:     const char* GetString()
38:     { return buffer; }
39: };
40: 
41: class Human
42: {
43: private:
44:     int age;
45:     bool gender;
46:     MyString name;
47: 
48: public:
49:     Human(const MyString& InputName, int InputAge, bool gender)
50:     name(InputName), age(InputAge), gender(gender) {}
51: 
52:     int GetAge ()
53:     { return age; }
54: };
55: 
56: int main()
57: {
58:     MyString mansName("Adam");
59:     MyString womansName("Eve");
60: 
61:     cout << "sizeof(MyString) = " << sizeof(MyString) << endl;
62:     cout << "sizeof(mansName) = " << sizeof(mansName) << endl;
63:     cout << "sizeof(womansName) = " << sizeof(womansName) << endl;
64: 
65:     Human firstMan(mansName, 25, true);
66:     Human firstWoman(womansName, 18, false);
67: 
68:     cout << "sizeof(Human) = " << sizeof(Human) << endl;
69:     cout << "sizeof(firstMan) = " << sizeof(firstMan) << endl;
70:     cout << "sizeof(firstWoman) = " << sizeof(firstWoman) << endl;
71:     return 0;
72: }
```

点击此处查看代码图像

```cpp
struct Human
{
   // 构造函数，默认公有（因为未指定访问权限）
   Human(const MyString& humansName, int humansAge, bool humansGender)
      : name(humansName), age (humansAge), Gender(humansGender) {}

   int GetAge ()
   {
      return age;
   }

private:
   int age;
   bool gender;
   MyString name;
};
```

如你所见，`struct Human` 与 `class Human` 相似，`struct` 类型对象的实例化也与 `class` 类型相似：

点击此处查看代码图像

`Human firstMan("Adam", 25, true);` // struct Human 的一个实例

### 声明类的 `friend`（友元）

类不允许外部访问其声明为 `private` 的数据成员和方法。但对于声明为 `friend` 类或友类函数，这一规则是被豁免的，如列表 9.14 所示，使用了 `friend` 关键字。

**列表 9.14** 使用 `friend` 关键字允许外部函数 `DisplayAge()` 访问私有数据成员

点击此处查看代码图像

* * *

```cpp
   0: #include <iostream>
   1: #include <string>
   2: using namespace std;
   3:
   4: class Human
   5: {
   6: private:
   7:     friend void DisplayAge(const Human& person);
   8:     string name;
   9:     int age;
   10:
   11: public:
   12:     Human(string humansName, int humansAge)
   13:     {
   14:         name = humansName;
   15:         age = humansAge;
   16:     }
   17: };
   18:
   19: void DisplayAge(const Human& person)
   20: {
   21:     cout << person.age << endl;
   22: }
   23:
   24: int main()
   25: {
   26:     Human firstMan("Adam", 25);
   27:     cout << "Accessing private member age via friend function: ";
   28:     DisplayAge(firstMan);
   29:
   30:     return 0;
   31: }
```

* * *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

通过友元函数访问私有成员 age: 25

分析 ![Image](img/arrow.jpg)

第 7 行包含一个声明，告知编译器全局作用域内的函数 `DisplayAge()` 是一个 `friend`，因此被允许特殊访问 `class Human` 的私有成员。你可以注释掉第 7 行，以查看第 22 行的编译失败。

与函数一样，外部类也可以被指定为受信任的友元，如列表 9.15 所示。

**列表 9.15** 使用 `friend` 关键字允许外部类 `Utility` 访问私有数据成员

点击此处查看代码图像

* * *

```cpp
   0: #include <iostream>
   1: #include <string>
   2: using namespace std;
   3:
   4: class Human
   5: {
   6: private:
   7:     friend class Utility;
   8:     string name;
   9:     int age;
   10:
   11: public:
   12:     Human(string humansName, int humansAge)
   13:     {
   14:         name = humansName;
   15:         age = humansAge;
   16:     }
   17: };
   18:
   19: class Utility
   20: public:
   21:     static void DisplayAge(const Human& person)
   22:     {
   23:         cout << person.age << endl;
   24:     }
   25: };
   26:
   27: int main()
   28: {
   29:     Human firstMan("Adam", 25);
   30:     cout << "Accessing private member via friend class: ";
   31:     Utility::DisplayAge(firstMan);
   32:
   33:     return 0;
   34: }
```

* * *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

通过友元类访问私有成员: 25

分析 ![Image](img/arrow.jpg)

第 7 行表示 `class Utility` 是 `class Human` 的友元。该友元声明允许 `class Utility` 中的所有方法访问 `class Human` 中的私有数据成员和方法。

### `union`: 一种特殊的存储机制

`union` 是一种特殊的类类型，其中非静态数据成员在同一时刻只有一个激活状态。因此，`union` 可以像类一样容纳多个数据成员，不同之处在于其中只有一个成员可以被实际使用。

#### 声明联合体 (Union)

使用 `union` 声明联合体，随后紧跟联合体的名称及其在花括号内的数据成员：

点击此处查看代码图像

```cpp
union UnionName
{
   Type1 member1;
   Type2 member2;
   ...
   TypeN memberN;
};
```

你可以像这样实例化和使用 `union`：

点击此处查看代码图像

```cpp
UnionName unionObject;
unionObject.member2 = value; // 选择 member2 为激活成员
```

注意：与 `struct` 类似，`union` 的成员默认是公有的。与 `struct` 不同，`union` 不能用于继承体系中。此外，`union` 的大小固定为该 `union` 中最大成员的大小——即使该成员在 `union` 实例中处于未状态。

#### 你会使用 `union` 吗？

`union` 通常作为 `struct` 的成员来构建复杂数据类型。在某些实现中，`union` 将内存空间解释为另一种类型的能力用于类型转换——这种做法是有争议的。列表 9.16 展示了 `union` 的声明和用法。

**列表 9.16** 声明、实例化和 `sizeof()` Union

点击此处查看代码图像

* * *

```cpp
   0: #include <iostream>
   1: #include <string>
   2: using namespace std;
   3:
   4: SimpleUnion
   5: {
   6:     int num;
   7:     char alphabet;
   8: };
   9:
   10: struct ComplexType
   11: {
   12:     enum DataType
   13:         Int,
   14:         Char
```



```cpp
} Type;

union Value
{
    int num;
    char alphabet;

    Value() {}
    ~Value() {}
} value;
};

void DisplayComplexType(const ComplexType& obj)
{
    switch (obj.Type)
    {
        case ComplexType::Int:
            cout << "Union contains number: " << obj.value.num << endl;
            break;

        case ComplexType::Char:
            cout << "Union contains character: " << obj.value.alphabet << endl;
            break;
    }
}

int main()
{
    SimpleUnion u1, u2;
    u1.num = 2100;
    u2.alphabet = 'C';
    cout << "sizeof(u1) containing integer: " << sizeof(u1) << endl;
    cout << "sizeof(u2) containing character: " << sizeof(u2) << endl;

    ComplexType myData1, myData2;
    myData1.Type = ComplexType::Int;
    myData1.value.num = 2017;

    myData2.Type = ComplexType::Char;
    myData2.value.alphabet = 'X';

    DisplayComplexType(myData1);
    DisplayComplexType(myData2);

    return 0;
}
```

该示例表明，`sizeof()` 联合体对象 `u1` 和 `u2` 返回的两个对象预留的内存是相同的，尽管 `u1` 用于存储整数而 `u2` 用于存储 `char`，且 `char` 的尺寸比 `int` 小。这是因为编译器为联合体预留的内存等于其包含的最大对象所消耗的内存。

第 9–25 行定义的 `struct` `ComplexType` 实际上包含一个枚举 `DataType`，用于指示联合体中存储对象的性质，此外还有一个名为 `Value` 的 `union` 类型数据成员。这种由一个用于存储类型信息的枚举和一个用于存储值的 `union` 构成的 `struct` 组合是联合体的一种流行应用。例如，Windows 应用程序编程中广泛使用的 `VARIANT` 结构就遵循了类似的方法。

第 27–39 行定义的函数 `DisplayComplexType()` 也使用了这种组合，它在提供的 `switch-case` 结构中通过枚举来执行正确的分支。例如，我们在该联合体包含了一个构造函数和析构函数——由于该联合体包含简单旧数据（Plain-Old-Data）类型，这些函数在列表 9.16 中是可选的，但如果联合体包含另一个用户定义的类型（如 `class` 或 `struct`），则可能是需要的。

### 提示

C++17 预计将引入 `union` 的类型安全替代方案。要了解 `std::variant`，请访问第 29 节“展望未来（ch29.html_ch29）”。

## 在类和结构体上使用聚合初始化

以下初始化语法被称为*聚合初始化*（aggregate initialization）语法：

`Type objectName = {argument1, ..., argumentN};`

或者自 C++11 起：

`Type objectName {argument1, ..., argumentN};`

聚合初始化可以应用于聚合体，因此了解哪些数据类型属于这一类别是非常重要的。

你已经在第 4 节“数组和字符串的管理（ch04.html_ch04）”中的数组初始化中见过聚合初始化的示例。

```cpp
int myNums[] = { 9, 5, -1 }; // myNums is int[3]

char hello[6] = { 'h', 'e', 'l', 'l', 'o', '\0' };
```

然而，“聚合”（aggregate）一词不仅限于整数或字符等简单类型的数组，也扩展到了类（因此包括结构体和联合体）。标准对可以称为聚合体的 `struct` 或 `class` 的规范实施了限制。这些限制根据你所引用的 C++ 标准版本而有所细微差别。

尽管如此，可以说：包含公共非静态数据成员、不包含私有或保护数据成员、不包含虚成员函数、具有无或仅公共继承（即没有私有、保护或虚继承）且没有用户定义构造函数的类或结构体也是聚合体，并且可以作为聚合体进行初始化。

### 提示

继承在第 10 节“实现继承（ch10.html_ch10）”和第 11 节“多态性（ch11.html_ch11）”中进行了详细解释。

因此，下面的 `struct` 满足聚合体的前提条件，因此可以作为聚合体初始化：

```cpp
struct Aggregate1
{
    int num;
    double pi;
};
```

初始化：

`Aggregate1 a1{ 2017, 3.14 };`

另一个示例：

```cpp
struct Aggregate2
{
    int num;
    char hello[6];
    int impYears[5];
};
```

初始化：

`Aggregate2 a2 {42, {'h', 'e', 'l', 'l', 'o'}, {1998, 2003, 2011, 2014, 2017}};`

列表 9.17 是一个展示将聚合初始化应用于类和结构体的示例。

**列表 9.17** 类类型上的聚合初始化

```cpp
0: #include <iostream>
1: #include<string>
2: using namespace std;

3:
4: class Aggregate1
5: {
6: public:
7:     int num;
8:     double pi;
9: };

10:
11: struct Aggregate2
12: {
13:     char hello[6];
14:     int impYears[3];
15:     string world;
16: };

17:
18: int main()
19: {
20:     int myNums[] = { 9, 5, -1 }; // myNums is int[3]
21:     Aggregate1 a1{ 2017, 3.14 };
22:     cout << "Pi is approximately: " << a1.pi << endl;
23:     Aggregate2 a2 {42, {'h', 'e', 'l', 'l', 'o'}, {1998, 2003, 2011, 2014, 2017}};
24:     return 0;
25: }
```

### 类与对象的 `constexpr`

我们在第 3 节中介绍了 `constexpr`，在那里它提供了一种提高 C++ 应用程序性能的强大方法。通过将对常量或 `constexpr` 表达式的操作函数标记为 `constexpr`，我们指示编译器评估这些函数并插入其结果，而不是在应用程序执行时插入计算结果的指令。

该关键字也可以用于评估为常量的类和对象，如列表 9.18 所示。注意，当函数或类与非常量实体一起使用时，编译器将忽略 `constexpr`。

## 分析

注意第 3–9 行中 `class Human` 的微小修改。它现在在构造函数的声明和成员函数 `GetAge()` 中使用了 `constexpr`。这个小的添加告诉编译器在可能的情况下将 `class Human` 实例的创建和使用视为常量表达式。

第 13 行的 `somePerson` 被声明为常量实例并在第 14 行中作为常量使用。因此，该实例可能会被编译器评估，并且代码在执行时经过性能优化。第 16 行的实例 `another-Person` 未声明为常量，因此它的实例化或使用可能不会被编译器视为常量表达式。

## 总结

本节课程教授了 C++ 中最基础的关键字和概念之一：类（class）。你学习了类如何封装成员数据以及操作这些数据的成员函数。你看到了诸如 `public` 和 `private` 等访问修饰符如何帮助你抽象类外部实体不需要的数据和功能。

你学习了拷贝构造函数的概念，以及 C++11 引入的移动构造函数，它们有助于减少不必要的拷贝步骤。你看到了一些特殊情况，在这些情况下，这些元素共同作用，帮助你实现如单例（singleton）等的设计模式。

## 问答

**Q 类的实例（instance）和类的对象（object）有什么区别？**

**A** 本质上没有。当你实例化一个类时，你会得到一个也可以称为对象的实例。

**Q 访问成员的更好方法是什么：使用点运算符（`.`）还是使用指针运算符（`->`）？**

**A** 如果你有一个指向对象的指针，指针运算符最为合适。如果你将对象实例化为堆栈上的局部变量，那么点运算符最为合适。

**Q 我应该总是编写拷贝构造函数吗？**

**A** 如果你的类数据成员是编写良好的智能指针、字符串类或 STL 容器（如 `std::vector`），那么编译器插入的默认拷贝构造函数会确保相应的拷贝构造函数被调用。然而，如果你的类拥有原始指针成员（例如用于动态数组的 `int*` 而不是 `std::vector<int>`），你需要提供一个编写正确的拷贝构造函数，以确保在类对象按值传递的函数调用期间，对数组进行深拷贝。

**Q 我的类只有一个定义了带默认值参数的构造函数。这仍然是默认构造函数吗？**

**A** 是的。如果类的实例可以在不带参数的情况下创建，则该类具有默认构造函数。一个类只能有一个默认构造函数。

**Q 为什么本节中的某些示例使用 `SetAge()` 等函数来设置整数 `Human::age`？为什么不把 `age` 设公共并根据需要赋值？**

**A** 从技术角度来看，将 `Human::age` 设为 `public` 成员同样可行。但从设计角度来看，保持成员数据为私有是一个好主意。`GetAge()` 或 `SetAge()` 等访问函数是访问这些私有数据的精细且扩展的方法，允许你在设置或重置 `Human::age` 值之前对实例进行错误检查。

**Q 为什么拷贝构造函数的参数是取拷贝源的引用？**

**A** 首先，编译器期望拷贝构造函数是那样的。背后的原因是，如果拷贝构造函数按值接受拷贝源，它将调用自己，导致无限的拷贝循环。

## 工作坊

工作坊提供了测试题来帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用所学知识的经验。尝试在查看附录 E 中的答案之前回答测试练习题，并在继续下一节之前确保你理解了答案。

### 测试题

1. 当我使用 `new` 创建类实例时，类是在哪里创建的？
2. 我的类有一个原始指针 `int*`，包含一个动态分配的整数数组。`sizeof` 会根据动态数组中整数的数量报告不同的大小吗？
3. 我类的所有成员都是私有的，且我的类不包含任何声明的友元（friend）类或函数。谁可以访问这些成员？
4. 一个类的成员方法可以调用另一个吗？
5. 构造函数有什么用？
6. 析构函数有什么用？

### 练习题

1. **找错：** 下面的 `class` 声明中哪里错了？

```cpp
class Human
{
    int age;
    string name;

public:
    Human() {}
}
```

2. 练习 1 中类的用户将如何访问成员 `Human::age`？
3. 编写练习 1 所示类的更优版本，使用初始化列表初始化所有参数。
4. 编写一个 `class Circle`，根据在实例化时作为参数传递给类的半径计算面积和周长。Pi 应该包含在一个常量私有成员中，该成员无法从圆外部访问。

## 第 10 节：实现继承

面向对象的编程基于四个重要方面：封装、抽象、继承和多态。继承是复用属性的一种强大方式，也是通向多态的基石。

在本节中，你将了解到：

- 编程背景下的继承
- C++ 的继承语法
- `public`、`private` 和 `protected` 继承
- 多重继承
- 隐藏基类方法和切片（slicing）引起的问题

## 继承的基础

Tom Smith 从祖先那里继承的首要姓氏，这让他成为一名 Smith。此外，他还继承了父母教给他的某些价值观以及一项木雕技能，这项技能是 Smith 家族世世代代相传的。这些属性共同定义了 Tom 是 Smith 家族树的后代。

在编程术语中，你经常面临管理组件具有相似属性的情况，但在细节或行为上存在细微差异。解决此问题的方法之一是将每个组件制作成类，每个类实现所有属性并重新实现公共部分。

另一种解决方案是使用继承，允许相似的类派生自一个包含公共属性并实现公共功能的基类，通过覆盖这些基类功能来实现每个类独特的行为。后者通常是首选方法。欢迎来到面向对象编程的世界，如图 10.1 所示。

![图 10.1 类之间的继承](img/10fig01.jpg)

**图 10.1** 类之间的继承。

### 继承与派生

图 10.1 显示了基类与其派生类之间的图示关系。现在可能很难想象基类或派生类可以是什么。尝试理解派生类继承自基类，在那种意义上它也是基类（就像 Tom 是一个 Smith 一样）。

派生类与其基类之间的“是一个”（is-a）关系仅适用于 `public` 继承。本节将从公共继承开始，以理解继承的概念以及最常见的继承形式，然后再转向 `private` 或 `protected` 继承。

## 理解继承概念

为了方便理解这一概念，可以想象一个基类 `class Bird`（鸟）。从 `Bird` 派生的类有 `class Crow`（乌鸦）、`class Parrot`（鹦鹉）或 `class Kiwi`（奇异鸟）。

`class Bird` 会定义鸟类最基本的属性，例如“有羽毛”、“有翅膀”、“产蛋”、“会飞”等。派生类如 `Crow`、`Parrot` 或 `Kiwi` 继承这些属性并对其进行自定义（例如，代表不会飞行鸟的 `class Kiwi` 不包含 `Fly()` 的实现）。表 10.1 展示了更多几个继承的例子。

![表 10.1 取自生活的公共继承示例](img/10tab01.jpg)

**表 10.1** 取自生活的公共继承示例。

这些例子说明，当你戴上面向对象编程的眼镜时，你会在周围许多物体中看到继承的例子。`Fish`（鱼）是 `Tuna`（金枪鱼）的基类，因为 `Tuna` 和 `Carp`（鲤鱼）一样都是 `Fish`，并且具有所有鱼类的特征，如冷血。

然而，`Tuna` 与 `Carp` 在外观、游泳方式以及作为咸鱼这一点上有所不同。因此，`Tuna` 和 `Carp` 从共同的基类 `Fish` 继承共同特征，但通过特化基类属性来区分彼此。这在图 10.2 中所示。

![图 10.2 金枪鱼、鲤鱼和鱼之间的层次关系](img/10fig02.jpg)

**图 10.2** 金枪鱼、鲤鱼和鱼之间的层次关系。

鸭嘴兽会游泳，但它是一种具有哺乳动物特征的特殊动物（如用奶喂养幼崽）、具有鸟类特征（因为它产蛋）以及爬行动物特征（因为它有爬行动物的特征）。因此，可以想象 `class Platypus`（鸭嘴兽）继承两个基类 `class Mammal`（哺乳动物）和 `class Bird`（鸟），以继承哺乳和鸟类特征。这种继承形式被称为多重继承，将在本节后文中讨论。

## C++ 派生语法

你如何从 `class Fish` 继承 `class Carp`，或者通过从 `class Base` 继承 `class Derived`？C++ 实现此点的语法如下：

```cpp
class Base
{
    // ... 基类成员
};
```



```cpp
class Derived: access-specifier Base
{
   // ... 派生类成员
};
```

`access-specifier`（访问限定符）可以是 `public`（最常用），表示“派生类是一个基类”的关系；`private` 或 `protected` 则表示“派生类有一个基类”的关系。

派生自 `class Fish` 的 `class Carp` 的继承层次表示如下：

点击此处查看代码图片

```cpp
class Fish // 基类
{
   // ... Fish 的成员
};

class Carp:public Fish // 派生类
{
   // ... Carp 的成员
};
```

派生自 `class Fish` 的 `class Carp` 和 `class Tuna` 的可编译声明如列表 10.1 所示。

---

## 术语说明

在阅读关于继承的内容时，你会遇到如 `inherits from`（继承自）或 `derives from`（派生自）等术语，它们的本质含义相同。

同样，基类也被称为 `super class`（超类）。派自基类的类也称为 `derived class`（派生类），也可以被称为 `subclass`（子类）。

---

**列表 10.1** 由鱼类世界展示的简单继承体系

点击此处查看代码图片

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Fish

4: {

5: public:

6:     bool isFreshWaterFish;

7:

8:     void Swim()

9:     {

10:         if (isFreshWaterFish)

11:             cout << "Swims in lake" << endl;

12:         else

13:             cout << "Swims in sea" << endl;

14:     }

15: };

16:

17: class Tuna: public Fish

18: {

19: public:

20:     Tuna()

21:     {

22:         isFreshWaterFish = false;

23:     }

24: };

25:

26: class Carp: public Fish

27: {

28: public:

29:     Carp()

30:     {

31:         isFreshWaterFish = true;

32:     }

33: };

34:

35: int main()

36: {

37:     Carp myLunch;

38:     Tuna myDinner;

39:

40:     cout << "About food:" << endl;

41:     myLunch.Swim();

42:     cout << "Dinner: " << endl;

43:     myDinner.Swim();

44:     return 0;

45: }
```

```cpp
class Tuna: public Fish
{
public:
    Tuna()
    {
        isFreshWaterFish = false; // 设置基类中的保护成员
    }
};

class Carp: public Fish
{
public:
    Carp()
    {
        isFreshWaterFish = false;
    }
};

int main()
{
    Carp myLunch;
    Tuna myDinner;

    cout << "About my food" << endl;
    cout << "Lunch: ";
    myLunch.Swim();

    cout << "Dinner: ";
    myDinner.Swim();

    // 取消下行的注释以查看保护成员
    // 无法从类体系外部访问
    // myLunch.isFreshWaterFish = false;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

关于我的食物

午餐: 在湖中游泳  
晚餐: 在海中游泳

## 分析 ![Image](img/arrow.jpg)

尽管列表 10.2 的输出与列表 10.1 相同，但第 3–16 行定义的 `class Fish` 发生了许多根本性的变化。第一个也是最明显的变化是，布尔成员 `Fish::isFreshWaterFish` 现在是一个 `protected` 属性，因此，如第 51 行所示，无法通过 `main()` 访问（取消注释将看到编译器错误）。尽管如此，`Fish` 中这个访问修饰符为 `protected` 的成员可以从派生类 `Tuna` 和 `Carp` 访问，分别如第 23 行和 32 行所示。这个小程序有效地演示了使用 `protected` 关键字的作用，即确保需要继承的基类属性受到保护，防止类体系外部访问。

这是面向对象编程的一个重要方面，它结合了数据抽象和继承，确保派生类可以安全地继承基类属性，而这些属性不会被该层次系统之外的任何人篡改。

### 基类初始化——向基类传递参数

如果基类包含一个在实例化时需要参数的重载构造函数会怎样？在构造派生类时，这样的基类将如何被实例化呢？线索在于使用初始化列表，并通过派生类的构造函数调用相应的基类构造函数，如下代码所示：

点击此处查看代码图片

```cpp
class Base
{
public:
    Base(int someNumber) // 重载构造函数
    {
        // 使用 someNumber
    }
};

Class Derived: public Base
{
public:
    Derived(): Base(25)  // 使用参数 25 实例化 Base
    {
        // 派生类构造函数代码
    }
};
```

这种机制在 `class Fish` 中非常有用，通过向 `Fish` 的构造函数提供一个布尔输入参数来初始化 `Fish::isFreshWaterFish`，该基类 `Fish` 就可以确保每个派生类都必须说明 `Fish` 是淡水鱼还是咸水鱼，如列表 10.3 所示。

**列表 10.3** 使用初始化列表的派生类构造函数

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

class Fish
{
protected:
    bool isFreshWaterFish; // 仅派生类访问

public:
    // Fish 构造函数
    Fish(bool isFreshWater) : isFreshWaterFish(isFreshWater){}

    void Swim()
    {
        if (isFreshWaterFish)
            cout << "Swims in lake" << endl;
        else
            cout << "Swims in sea" << endl;
    }
};

class Tuna: public Fish
{
public:
    Tuna(): Fish(false) {} // 基类构造函数
};

class Carp: public Fish
{
public:
    Carp(): Fish(true) {}
};

int main()
{
    Carp myLunch;
    Tuna myDinner;

    cout << "About my food" << endl;
    cout << "Lunch: ";
    myLunch.Swim();

    cout << "Dinner: ";
    myDinner.Swim();

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

关于我的食物

午餐: 在湖中游泳  
晚餐: 在海中游泳

## 分析 ![Image](img/arrow.jpg)

`Fish` 现在有一个带有默认参数的构造函数，用于初始化 `Fish::isWaterFish`。因此，创建 `Fish` 对象的唯一可能是通过提供一个初始化保护成员的参数。通过这种方式，`class Fish` 确保了保护成员不会包含随机值，特别是当派生类忘记设置它时。派生类 `Tuna` 和 `Carp` 现在被强制定义一个构造函数，用正确的参数（true 或 false，表示淡水或其他）来实例化基类 `Fish` 实例，分别如第 24 行和第 30 行所示。

### 注意事项

在列表 10.3 中，你看到 `Fish::isFreshWaterFish` 成员仅供派生类访问，尽管它是 `protected` 的，它是通过 `Fish` 的构造函数设置的。为了确保最大的安全性，如果派生类不需要访问该属性，请将其标记为 `private`。因此，`Fish` 的一个改进版本将使用该属性。参见列表 10.4。

### 派生类重写基类方法

如果 `class Derived` 实现了与它继承的 `class Base` 相同的返回值和签名的函数，那么它有效地重写了基类的方法，如下所示：

点击此处查看代码图片

```cpp
class Base
{
public:
    void DoSomething()
    {
        // 实现代码... 做某些
    }
};

class Derived:public Base
{
public:
    void DoSomething()
    {
        // 实现代码... 做别的
    }
};
```

因此，如果使用 `Derived` 实例调用 `DoSomething()`，它不会调用 `class Base` 中的功能。

如果 `Tuna` 和 `Carp` 类实现了在基类 `Fish::Swim()` 中也存在的 `Swim()` 方法，那么在列表 10.3 节选的 `main()` 中调用 `Swim` 将导致调用本地实现，这本质上重写了基类的 `Swim()` 方法。这通过列表 10.4 所示。

**列表 10.4** 派生类 `Tuna` 和 `Carp` 重写基类 `Fish` 中的 `Swim()`

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

class Fish
{
private:
    bool isFreshWaterFish;

public:
    Fish(bool isFreshWater) : isFreshWaterFish(isFreshWater){}

    void Swim()
    {
        if (isFreshWaterFish)
            cout << "Swims in lake" << endl;
        else
            cout << "Swims in sea" << endl;
    }
};

class Tuna: public Fish
{
public:
    Tuna(): Fish(false) {}

    void Swim()
    {
        cout << "Tuna swims real fast" << endl;
    }
};

class Carp: public Fish
{
public:
    Carp(): Fish(true) {}
};
```

```cpp
39:         cout << "Carp swims real slow" << endl;
40:     }
41: };

43: int main()
44: {
45:     Carp myLunch;
46:     Tuna myDinner;
48:     cout << "About my food" << endl;
50:     cout << "Lunch: ";
51:     myLunch.Swim();
53:     cout << "Dinner: ";
54:     myDinner.Swim();
56:     return 0;
57: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

关于我的食物

午餐：鲤鱼游得非常慢  
晚餐：金枪鱼游得非常快

## 分析 ![Image](img/arrow.jpg)

输出表明，第 51 行的 `myLunch.Swim()` 调用了第 37–40 行定义的 `Carp::Swim()`。同样，第 54 行的 `myDinner.Swim()` 调用了第 26–29 行定义的 `Tuna::Swim()`。换句话说，如第 12–18 行所示，基类 `Fish` 中 `Fish::Swim()` 的实现被派自 `Fish` 的类 `Tuna` 和 `Carp` 中定义的相同函数 `Swim()` 所重写。调用 `Fish::Swim()` 的唯一方法是在 `main()` 中使用作用域解析运算符（`::`）来显式调用 `Fish::Swim()`，如本节后文所示。

#### 调用基类的重写方法

在列表 10.4 中，你看到了一个派生类 `class Tuna` 通过实现其相同版本来重写 `Fish` 中的 `Swim()` 函数的示例。本质上：

点击此处查看代码图片

```cpp
Tuna myDinner;

myDinner.Swim(); // 将调用 Tuna::Swim()
```

如果你想在列表 10.4 中通过 `main()` 调用 `Fish::Swim()`，你需要在以下语法中使用作用域解析运算符（`::`）：

点击此处查看代码图片

```cpp
myDinner.Fish::Swim(); // 使用 Tuna 实例调用 Fish::Swim()
```

紧随其后的列表 10.5 展示了如何使用派生类实例来调用基类成员。

#### 在派生类中调用基类方法

通常，`Fish::Swim()` 会包含一个通用的游泳实现，适用于包括它们在内的所有鱼类、金枪鱼和鲤鱼。如果你在 `Tuna::Swim()` 和 `Carp::Swim()` 中的特化实现需要复用基类的通用实现 `Fish::Swim()`，则可以像下面的代码所示使用作用域解析运算符（`::`）：

点击此处查看代码图片

```cpp
class Carp: public Fish
{
public:
    Carp(): Fish(true) {}

    void Swim()
    {
        cout << "Carp swims real slow" << endl;
        Fish::Swim();  // 使用运算符:: 调用基类函数
    }
};
```

这在列表 10.5 中得到了证明。

**列表 10.5** 使用作用域解析运算符（`::`）从派生类和 `main()` 调用基类函数

点击此处查看代码图片

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Fish
{
5: private:
6:     bool isFreshWaterFish;

7:
8: public:
9:     // Fish 构造函数
10:     Fish(bool isFreshWater) : isFreshWaterFish(isFreshWater){}

12:     void Swim()
13:     {
14:         if (isFreshWaterFish)
15:             cout << "Swims in lake" << endl;
16:         else
17:             cout << "Swims in sea" << endl;
18:     }
19: };

21: class Tuna: public Fish
{
23: public:
24:     Tuna(): Fish(false) {}

26:     void Swim()
27:     {
28:         cout << "T swims real fast" << endl;
29:     }
30: };

32: class Carp: public Fish
{
34: public:
35:     Carp(): Fish(true) {}

37:     void Swim()
38:     {
39:         cout << "Carp swims real slow" << endl;
40:         Fish::Swim();
41:     }
42: };

44: int main()
45: {
46:     Carp myLunch;
```



```cpp
47:     Tuna myDinner;

48:

49:     cout << "About my food" << endl;

50:     cout << "Lunch: ";

51:     myLunch.Swim();

53:     cout << "Dinner: ";

54:     myDinner.Swim();

56:     return 0;

57: }
```

所以，当你创建一个派生自`class Fish`的`class Tuna`对象时，`Tuna`的构造函数是在`Fish`类的构造函数之前还是之后调用的？此外，在类层次结构的对象实例化过程中，诸如`Fish::isFreshWaterFish`等成员属性的顺序怎样的？

幸运的是，实例化序列是标准化的。基类对象在派生类之前实例化。因此，`Tuna`的`Fish`部分首先被构造，这样成员属性——尤其是`class Fish`中包含的受保护和公共属性——在`class Tuna`实例化时就已经准备就绪供使用了。

在`class Fish`和`class Tuna`的实例化过程中，成员属性（如`Fish::isFreshWaterFish`）在构造函数`Fish::Fish()`被调用之前实例化，这确保了成员属性在构造函数处理它们之前已经准备就绪。这同样适用于`Tuna::Tuna()`。

### 析构顺序

当`Tuna`实例离开作用域时，其析构顺序与构造顺序相反。Listing 10.7 是演示构造与析构顺序的一个简单示例。

**LISTING 10.7** 基类、派生类及其成员的构造与析构顺序

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class FishDummyMember

4: {

5: public:

6:     FishDummyMember()

7:     {

8:         cout << "FishDummyMember constructor" << endl;

9:     }

10:

11:     ~FishDummyMember()

12:     {

13:         cout << "FishDummyMember destructor" << endl;

14:     }

15: };

16:

17: class Fish

18: {

19: protected:

20:     FishDummyMember dummy;

21:

22: public:

23:     // Fish constructor

24:     Fish()

25:     {

26:         cout << "Fish constructor” << endl;

27:     }

28:

29:     ~Fish()

30:     {

31:         cout << "Fish destructor" << endl;

32:     }

33: };

34:

35: class TunaDummyMember

36: {

37: public:

38:     TunaDummyMember()

39:     {

40:         cout << "TunaDummyMember constructor" << endl;

41:     }

42:

43:     ~TunaDummyMember()

44:     {

45:         cout << "TunaDummyMember destructor" << endl;

46:     }

47: };

48:

49:

50: class Tuna: public Fish

51: {

52: private:

53:     TunaDummyMember dummy;

54:

55: public:

56:     Tuna()

57:     {

58:         cout << "Tuna constructor" << endl;

59:     }

60:     ~Tuna()

61:     {

62:         cout << "Tuna destructor" << endl;

63:     }

64:

65: };

66:

67: int main()

68: {

69:     Tuna myDinner;

70: }
```

**Output**

```text
FishDummyMember constructor
Fish constructor
TunaDummyMember constructor
Tuna constructor
Tuna destructor
TunaDummyMember destructor
Fish destructor
FishDummyMember destructor
```

### 分析

如第 67–70 行所示，`main()`对于其生成的输出量来说非常短。`Tuna`的实例化就足够生成这些行了，因为你已经在所有涉及对象的构造函数和析构函数中插入了`cout`语句。

为了理解成员变量是如何实例化和析构的，你定义了两个虚拟类`FishDummyMember`和`TunaDummyMember`，并在它们的构造函数和析构函数中使用了`cout`。

输出表明，当实例化`class Tuna`对象时，实例化实际上是从层次结构的顶部开始的。因此，`class Tuna`的基类`class Fish`部分首先实例化，在此过程中，`Fish`的成员——即`Fish::dummy`——首先被实例化。

随后是构造函数`Fish`，它在诸如`dummy`等成员属性被构造后执行是理所当然的。在基类构造完成后，`Tuna`的实例化继续对成员`Tuna::dummy`进行实例化，最后是构造函数`Tuna::Tuna()`的执行。输出证明了析构顺序恰恰相反。

### 私有继承

私有继承与公共继承（你目前为止所看到的）的区别在于，在派生类声明其派自基类的那行代码中，使用了`private`关键字：

```cpp
class Base
{
    // ... 基类成员和方法
};

class Derived: private Base // 私有继承
{
    // ... 派生类成员和方法
};
```

基类的私有继承意味着基类的所有公共成员和属性对于任何拥有派生类实例的人来说都是私有的（即不可访问的）。换句话说，即使是`class Base`的公共成员和方法，也只能由`Derived`实例使用。

这与你一直关注的`Tuna`和`Fish`示例形成鲜明对比。[Listing 10.1] 中的`main()`可以调用`Tuna`实例的`Fish::Swim()`，因为`Fish::Swim()`是一个公共方法，且`class Tuna`是通过公共继承派自`class Fish`。

因此，对于继承结构之外的世界，私有继承并不意味着“是一个”（is-a）关系（想象一条不会游泳的金鱼！）。由于私有继承允许基类属性和方法仅供派生它的子类使用，这种关系被称为“有一个”（has-a）关系。日常生活中你周围有一些私有继承的示例（参见 [Table 10.2]）。

**TABLE 10.2** 生活中的私有继承示例

让我们可视化汽车与其引擎之间的私有继承关系。参见 [Listing 10.8]。

**LISTING 10.8** 通过私有继承与`class Motor`相关的`class Car`

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Motor

4: {

5: public:

6:     void SwitchIgnition()

7:     {

8:         cout << "Ignition ON" << endl;

9:     }

10:     void PumpFuel()

11:     {

12:         cout << "Fuel in cylinders" << endl;

13:     }

14:     void FireCylinders()

15:     {

16:         cout << "Vroooom" << endl;

17:     }

18: };

19:

20: class Car:private Motor // 私有继承

21: {

22: public:

23:     void Move()

24:     {

25:         SwitchIgnition();

26:         PumpFuel();

27:         FireCylinders();

28:     }

29: };

30:

31: int main()

32: {

33:     Car myDreamCar;

34:     myDreamCar.Move();

35:

36:     return 0;

37: }
```

**Output**

```text
Ignition ON
Fuel in cylinders
Vroooom
```

如果另一个`class RaceCar`必须继承自`Car`，那么无论`RaceCar`和`Car`之间的继承性质如何，`RaceCar`都无法访问基类`Motor`的任何公共成员或函数。这是因为`Car`和`Motor`之间的关系是`private`（私有）继承，这意味着在使用`Car`的实例时，除`Car`之外的所有实体对`Base`的`public`和`protected`成员都只有`private`权限（即无访问权限）。

换句话说，在编译器计算一个类是否应该有权访问基类的`public`或`protected`成员时，限制性最大的访问修饰符占据主导地位。

### 保护继承（Protected Inheritance）

保护继承与公共继承的区别在于，在派生类声明继承自基类的行中使用了`protected`关键字：

```cpp
class Base
{
    // ... base 类成员方法
};

class Derived: protected Base     // 保护继承
{
    // ... derived class members 方法
};
```

保护继承在以下方面与私有继承相似：

- 它也表示一种“拥有”（has-a）的关系。
- 它还允许派生类访问`Base`的所有`public`和`protected`成员。
- 拥有`Derived`实例的继承层次之外的实体无法访问`Base`的公共成员。

然而，当涉及到被继承的派生类时，保护继承又有些不同：

```cpp
class Derived2: protected Derived
{
    // 可以访问 Base 的 public & protected 成员
};
```

保护继承层次允许子类中的子类（即`Derived2`）访问`Base`的`public`和`protected`成员，如列表 10.9 所示。如果`Derived`和`Base`之间的继承是`private`，那么将是不可能的。

**列表 10.9** 使用`protected`继承派自`class Car`，而`class Car`又派自`class Motor`的`class RaceCar`

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Motor

4: {

5: public:

6:     void SwitchIgnition()

7:     {

8:         cout << "Ignition ON" << endl;

9:     }

10:     void PumpFuel()

11:     {

12:         cout << "Fuel in cylinders" << endl;

13:     }

14:     void FireCylinders()

15:     {

16:         cout << "Vroooom" << endl;

17:     }

18: };

19:

20: class Car:protected Motor

21: {

22: public:

23:     void Move()

24:     {

25:         SwitchIgnition();

26:         PumpFuel();

27:         FireCylinders();

28:     }

29: };

30:

31: class RaceCar:protected Car

32: {

33: public:

34:     void Move()

35:     {

36:         SwitchIgnition();  // RaceCar 有权访问成员

37:         PumpFuel();  // 由于 "protected" 继承，访问基类 Motor

38:         FireCylinders(); // 存在于 RaceCar & Car, Car & Motor 之间

39:         FireCylinders();

40:         FireCylinders();

41:     }

42: };

43:

44: int main()

45: {

46:     RaceCar myDreamCar;

47:     myDreamCar.Move();

48:

49:     return 0;

50: }
```

**输出**

```text
Ignition ON
Fuel in cylinders
Vroooom
Vroooom
```

### 分析

`class Car`如第 20 行所示使用`protected`继承自`Motor`。`class RaceCar`如第 31 行所示使用`protected`继承自`class Car`。

如你所见，`RaceCar::Move()`的实现使用了在基类`Motor`中定义的公共方法。通过中间基类`Car`访问最终基类`Motor`的行为受`Car`和`Motor`之间关系的制约。如果这是`private`而不是`protected`，那么`SuperClass`将无法访问`Motor`的公共成员，因为编译器会选择相关访问修饰符中限制性最大的那个。

请注意，`Car`和`RaceCar`类之间的关系性质对访问`Motor`没有影响，而`Car`和`Motor`之间的关系则有。因此，即使你将第 31 行的`protected`改为`public`或`private`，该程序的命运也保持不变。

只有在必须时才使用`private`或`protected`继承。在大多数使用私有继承的情况下（例如`Car`和`Motor`的情况），基类完全可以作为`class Car`的一个成员属性，而不是超类。

Listing 10.10 展示了`Platypus`中多重继承的一种实现方式。

**列表 10.10** 使用多重继承来模拟一个兼具哺乳动物、鸟类和爬行动物特征的鸭嘴兽

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Mammal

4: {

5: public:

6:     void FeedBabyMilk()

7:     {

8:         cout << "Mammal: Baby says glug!" << endl;

9:     }

10: };

11:

12: class Reptile

13: {

14: public:

15:     void SpitVenom()

16:     {

17:         cout << "Reptile: Shoo enemy! Spits venom!" << endl;

18:     }

19: };

20:

21: class Bird

22: {

23: public:

24:     void LayEggs()

25:     {

26:         cout << "Bird: Laid my eggs, am lighter now!" << endl;

27:     }

28: };

29:

30: class Platypus: public Mammal, public Bird, public Reptile

31: {

32: public:

33:     void Swim()

34:     {

35:         cout << "Platypus: Voila, I can swim!" << endl;

36:     }

37: };

38:

39: int main()

40: {

41:     Platypus realFreak;

42:     realFreak.LayEggs();

43:     realFreak.FeedBabyMilk();

44:     realFreak.SpitVenom();

45:     realFreak.Swim();

46:
```



```cpp
47:     return 0;

48: }
```

***

## 输出 ![Image](img/arrow.jpg)

点击查看代码图像

Bird: Laid my eggs, am lighter now!  
Mammal: Baby says glug!  
Reptile: Shoo enemy! Spits venom!  
Platypus: Voila, I can swim!

## 分析 ![Image](img/arrow.jpg)

`class Platypus` 在第 30–37 行中采用了非常紧凑的定义。它本质上所做的只是继承自 `Mammal`、`Reptile` 和 `Bird` 三个类。第 41–44 行中的 `main()` 函数能够通过名为 `realFreak` 的派生类 `class Platypus` 对象调用这些各个基类的三个特征。除了调用继承自 `Mammal`、`Bird` 和 `Reptile` 的函数外，`main()` 在第 45 行还调用了 `Platypus::Swim()`。该程序演示了多重继承的语法，展示了派生类如何暴露其多个基类的所有公共属性（在本例中为公共成员函数）。

### 使用 `final` 避免继承

从 C++11 开始，编译器支持 `final` 饰符。它用于确保声明为 `final` 的类不能作为基类使用。例如在列表 10.10 中，`class Platypus` 代表一个演化完全的物种。因此，你可能希望确保该类是 `final` 的，从而阻止所有继承它的可能性。从列表 10.10 中截取并声明为 `final` 的 `class Platypus` 版本如下所示：

点击查看代码图像

```cpp
class Platypus final: public Mammal, public Bird, public Reptile
{
public:
    void Swim()
    {
        cout << "Platypus: Voila, I can swim!" << endl;
    }
};
```

除了防止继承外，`final` 还可以防止“是一个...”的关系。这将在下一节中讨论。

## 4. `using` 关键字在继承体系中是如何帮助我的我的？

## 5. `class Derived` 从 `class Base` 继承了 `private`。另一个 `class SubDerived` 从 `class Derived` 继承了 `public`。`SubDerived` 能访问 `class Base` 的公共成员吗？

### 练习题

1. 如列表 10.10 所示，`class Platypus` 的构造函数按什么顺序被调用？
2. 展示 `class Polygon`、`class Triangle` 和 `class Shape` 之间是如何相互相关的。
3. `class D2` 继承自 `class D1`，`class D1` 继承自 `class Base`。为了防止 `D2` 访问 `Base` 中的 `public` 成员，你会使用哪种访问修饰符？在哪里使用它？
4. 这段代码片段的继承本质是什么？

点击此处查看代码图像

```cpp
class Derived: Base
{
   // ... Derived members
};
```

5. **BUG 查找：** 这代码中存在什么问题：

点击此处查看代码图像

```cpp
class Derived: public Base
{
   // ... Derived members
};

void SomeFunc (Base value)
{
   // ...
}
```

# 第 11 Lesson：多态

在学习了继承的基础、创建继承体系，并理解了公共继承本质上模拟了一种“是一种”（is-a）关系后，是时候运用这些知识来学习面向对象编程的圣杯：多态了。

在本节中，你将了解到：

- ![Image](img/square.jpg) 多态的真正含义是什么
- ![Image](img/square.jpg) 虚函数的作用是什么以及如何使用它们
- ![Image](img/square.jpg) 什么是抽象基类以及如何声明它们
- ![Image](img/square.jpg) 虚继承意味着什么以及在何处需要它

## 多态的基础

“Poly”是希腊语中“*多*”的意思，而“morph”意味着“*形式*”。多态是面向对象语言的一种特性，允许不同类型的对象以相似的方式对待。本节重点关注通过 C++ 继承体系实现的多态行为，也称为*子类型多态*。

### 多态行为的需求

在 Lesson 10 “[实现继承，”中，你发现了 `Tuna` 和 `Carp` 是如何如列表 10.1 所示从 `Fish` 继承公共方法 `Swim()`。然而，`Tuna` 和 `Carp` 也可能提供自己的 `Tuna::Swim()` 和 `Carp::Swim()` 方法，使它们成为不同的游泳者。尽管如此，由于它们每一个也是 `Fish`，如果一个拥有 `Tuna` 实例的用户使用基类类型来调用 `Fish::Swim()`，他最终只执行了通用的部分 `Fish::Swim()` 而不是 `Tuna::Swim()`，即使该基类实例 `Fish` 是 `Tuna` 的一部分。这个问题在列表 11.1 中得到了演示。

***

> 注意
>
> 本节中的所有代码示例已精简到解释相关主题所需的最核心内容，并尽可能减少代码行数以提高可读性。
>
> 在编写程序时，你应该正确地编写类并创建有意义的继承体系，同时考虑到应用程序的设计和目的。

***

**列表 11.1** 使用属于 `Tuna` 的基类 `Fish` 实例来调用方法

点击此处查看代码图像

***

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     void Swim()
7:     {
8:         cout << "Fish swims! " << endl;
9:     }
10: };
11:
12: class Tuna:public Fish
13: {
14: public:
15:     // override Fish::Swim
16:     void Swim()
17:     {
18:         cout << "una swims!" << endl;
19:     }
20: };
21:
22: void MakeFish(Fish& inputFish)
23: {
24:     // calling Fish::Swim
25:     inputFish.Swim();
26: }
27:
28: int main()
29: {
30:     Tuna myDinner;
31:
32:     // calling Tuna::Swim
33:     myDinner.Swim();
34:
35:     // sending Tuna as Fish
36:     MakeFishSwim(myDinner);
37:
38:     return 0;
39: }
```

***

## 输出 ![Image](img/arrow.jpg)

```text
una swims!
Fish swims!
```

## 分析 ![Image](img/arrow.jpg)

`class Tuna` 通过如第 12 行所示的公共继承特化了 `class Fish`。它还重写了 `Fish::Swim()`。`main` 函数通过属于 `Tuna` 的基类 `Fish` 实例调用方法，如第 33 行所示。`MakeFishSwim` 将 `Tuna` 作为 `Fish` 传递，如第 25 行所示，它最终只执行了通用的部分 `Fish::Swim()` 而不是 `Tuna::Swim()`，即使该基类实例 `Fish` 是 `Tuna` 的一部分。

***

## 通过虚函数实现多态

你通过 `Fish` 指针或 `Fish&` 引用访问 `Fish` 类型的对象，如下：

```cpp
pFish->Swim();

myFish.Swim();
```

你期望的是一个 `Tuna` 类型的对象执行 `Swim()`，即使它被声明为 `Fish`。

在 `Fish` 类中将 `Swim()` 声明为 `virtual`，可以让编译器在调用时执行正确的变体，如列表 11.2 所示。

**列表 11.2** 将 `Fish::Swim()` 声明为 `virtual` 方法的效果

点击此处查看代码图像

***

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     virtual void Swim()
7:     {
8:         cout << "Fish swims!" << endl;
9:     }
10: };
11:
12: class Tuna:public Fish
13: {
14: public:
15:     // override Fish::Swim
16:     void Swim()
17:     {
18:         cout << "Tuna swims!" << endl;
19:     }
20: };
21:
22: class Carp:public Fish
23: {
24: public:
25:     // override Fish::Swim
26:     void Swim()
27:     {
28:         cout << "Carp swims!" << endl;
29:     }
30: };
31:
32: void MakeFish(Fish& inputFish)
33: {
34:     // calling virtual method Swim()
35:     inputFish.Swim();
36: }
37:
38: int main()
39: {
40:     Tuna myDinner;
41:     Carp myLunch;
42:
43:     // sending Tuna as Fish
44:     MakeFish(myDinner);
45:
46:     // sending Carp as Fish
47:     MakeFish(myLunch);
48:
49:     return 0;
50: }
```

函数 `MakeFishSwim(Fish&)` 的实现自列表 11.1 以来没有发生任何变化。然而，它产生的输出截然不同。其一，`Fish::Swim()` 完全没有被调用，因为存在重写的变体 `Tuna::Swim()` 和 `Carp::Swim()`，这些它们的优先级高于 `Fish::Swim()`，因为后者被声明为 `virtual`（虚）函数。这是一个非常重要的进展。这意味着即使不知道正在处理的 `Fish` 的确切类型，仅凭一个基类实例，实现 `MakeFishSwim()` 也可以调用在不同派生类中定义的不同 `Swim()` 实现。

这就是多态性：将不同的鱼视为一种共同类型 `Fish`，同时确保执行由派生类型提供的正确 `Swim()` 实现。

## 虚析构函数的必要性

列表 11.1 中展示的特性还有一个更阴险的一面——当存在特化版本时，无意中调用了派生类型实例的基类功能。当一个函数使用类型为 `Base*` 的指针调用运算符 `delete`，而该指针实际上指向类型为 `Derived` 的实例时，会发生什么？

将调用哪个析构函数？参见列表 11.3。

**列表 11.3** 一个在 `Base*` 上调用运算符 `delete` 的函数

点击此处查看代码图像

***

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     Fish()
7:     {
8:         cout << "Constructed Fish" << endl;
9:     }
10:    ~Fish()
11:    {
12:         cout << "Destroyed Fish" << endl;
13:    }
14: };
15:
16: class Tuna:public Fish
17: {
18: public:
19:     Tuna()
20:     {
21:         cout << "Constructed Tuna" << endl;
22:     }
23:     ~Tuna()
24:     {
25:         cout << "Destroyed Tuna" << endl;
26:     }
27: };
28:
29: void DeleteFishMemory(Fish* pFish)
30: {
31:     delete pFish;
32: }
33:
34: int main()
35: {
36:     cout << "Allocating a Tuna on the free store:" << endl;
37:     Tuna* pTuna = new Tuna;
38:     cout << "Deleting the Tuna: " << endl;
39:     DeleteFishMemory(pTuna);
40:
41:     cout << "Instantiating a Tuna on the stack:" << endl;
42:     Tuna myDinner;
43:     cout << "Automatic destruction as it goes out of scope: " << endl;
44:
45:     return 0;
46: }
```

***

## 输出 ![Image](img/arrow.jpg)

点击查看代码图像

```text
Allocating a Tuna on the free store:

Constructed Fish

Constructed Tuna

Deleting the Tuna:

Destroyed Fish

Instantiating a Tuna on the stack:

Constructed Fish

Constructed Tuna

Automatic destruction as it goes out of scope:

Destroyed Tuna

Destroyed Fish
```

## 分析 ![Image](img/arrow.jpg)

`main()` 在第 37 行使用 `new` 在自由存储上创建了一个 `Tuna` 实例，并在第 39 行使用服务函数 `DeleteFishMemory()` 后立即释放了分配的内存。为了对比，另一个 `Tuna` 实例作为局部变量 `myDinner` 创建在栈上，并在 `main()` 结束时离开作用域。输出是由 `Fish` 和 `tuna` 类构造函数和析构函数中的 `cout` 语句产生的。注意，虽然 `Tuna` 和 `Fish` 都由于 `new` 在自由存储上被构建了，但在 `delete` 期间没有调用 `Tuna` 的析构函数，只调用了 `Fish` 的。这与局部变量 `myDinner` 的构建和析构形成鲜明对比，后者的所有构造函数和析构函数都被调用了。第 10 行在列表 10.7 中演示了继承层次结构中类的构建和析构正确顺序，显示所有析构函数都需要被调用，包括 `~Tuna()`。显然，有些不对。

这个缺陷意味着如果使用 `new` 在自由存储上实例化一个派生类，然后使用类型为 `Base*` 的指针调用 `delete`，该析构函数将不会被调用。这可能导致资源未释放、内存泄漏等，这是一个不容忽视的问题。

为了避免这个问题，你使用如列表 11.4 所示的 `virtual` 析构函数。

**列表 11.4** 使用 `virtual` 析构函数确保在删除类型为 `Base*` 的指针时调用派生类中的析构函数

点击此处查看代码图像

***



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Fish
4: {
5: public:
6:     Fish()
7:     {
8:         cout << "Constructed Fish" << endl;
9:     }
10:    virtual ~Fish() // 虚析构函数
11:    {
12:         cout << "Destroyed Fish" << endl;
13:    }
14: };
15:
16: class Tuna:public Fish
17: {
18: public:
19:     Tuna()
20:     {
21:         cout << "Constructed Tuna" << endl;
22:     }
23:     ~Tuna()
24:     {
25:         cout << "Destroyed Tuna" << endl;
26:     }
27: };
28:
29: void DeleteFishMemory(Fish* pFish)
30: {
31:     delete pFish;
32: }
33:
34: int main()
35: {
36:     cout << "Allocating a Tuna on the free store:" << endl;
37:     Tuna* pTuna = new Tuna;
38:     cout << "Deleting the Tuna: " << endl;
39:     DeleteFishMemory(pTuna);
40:
41:     cout << "Instantiating a Tuna on the stack:" << endl;
42:     Tuna myDinner;
43:     cout << "Automatic destruction as it goes out of scope: " << endl;
44:
45:     return 0;
46: }
```

***

## 输出

![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Allocating a Tuna on the free store:

Constructed Fish

Constructed Tuna

Deleting the Tuna:

Destroyed Tuna

Destroyed Fish

Instantiating a Tuna on the stack:

Constructed Fish

Constructed Tuna

Automatic destruction as it goes out of scope:

Destroyed Tuna

Destroyed Fish
```

## 分析

列表 11.4 相比列表 11.3 的唯一改进是在第 10 行声明基类 `Fish` 析构函数时增加了 `virtual` 关键字。注意，这一微小的变化使得对实际指向 `Tuna` 的 `Fish*` 调用 `delete` 时，编译器除了执行 `Fish::~Fish()` 外还执行了 `Tuna::~Tuna()`，如第 31 行所示。现在，此输出也证明了无论 `Tuna` 类型对象是在第 37 行使用 `new` 在自由存储上实例化，还是在第 42 行作为局部变量在栈上实例化，构造和析构顺序都是相同的。

**注意**：始终将基类析构函数声明为 `virtual`。

点击此处查看代码图像

```cpp
class Base
{
public:
    virtual ~Base() {};
};
```

这确保了拥有 `Base*` 指针的人无法通过 `delete` 导致派生类实例无法正确析构。

考虑一个声明了 `N` 个虚函数的基类 `Base`：

点击此处查看代码图片

```cpp
class Base
{
public:
    virtual void Func1()
    {
      // Func1 实现
    }
    virtual void Func2()
    {
      // Func2 实现
    }
    // .. 以此类推
    virtual void FuncN()
    {
      // FuncN 实现
    }
};
```

继承自 `Base` 的派生类 `Derived` 重写了 `Base::Func2()`，直接暴露了 `Base` 中的其他虚函数：

点击此处查看代码图片

```cpp
class Derived: public Base
{
public:
    virtual void Func1()
    {
      // Func2 重写了 Base::Func2()
    }
    // Func2() 没有实现
    virtual void FuncN()
    {
      // FuncN 实现
    }
};
```

编译器看到了一个继承层次结构，并理解到 `Base` 定义了某些在 `Derived` 中被重写的虚函数。编译器现在做的是为每个实现了虚函数的类或重写了虚函数的派生类创建一个名为虚函数表（Virtual Function Table, VFT）的表。换句话说，类 `Base` 和 `Derived` 获得了各自的虚函数表实例。当实例化这些类的对象时，一个隐藏的指针（我们称之为 `VFT*`）会被初始化为相应的 `VFT`。虚函数表可以可视化为一个包含函数指针的静态数组，每个指针都指向感兴趣的虚函数（或重写函数），如图 11.1。

**图 11.1** 类 `Derived` 和 `Base` 的虚函数表可视化图。

因此，每个表都由函数指针组成，每个指针都指向虚函数的可用实现。在类 `Derived` 的情况下，其 VFT 中除一个函数指针外，所有的指针都指向 `Derived` 中该虚方法的本地实现。`Derived` 没有重写 `Base::Func2()`，因此该函数指针指向类 `Base` 中的实现。

这意味着当类 `Derived` 的用户调用：

点击此处查看代码图片

```cpp
Derived objDerived;
objDerived.Func2();
```

编译器会确保在类 `Derived` 的 VFT 中进行查找，并确保调用实现 `Base::Func2()`。这同样适用于使用了虚函数重写方法的调用：

点击此处查看代码图片

```cpp
void DoSomething(Base& objBase)
{
    objBase.Func1();   // 调用 Derived::Func1
}

int main()
{
    Derived objDerived;
    DoSomething(objDerived);
};
```

在这种情况下，尽管 `objDerived` 是通过 `objBase` 解释为类 `Base` 的实例，但该实例中的 VFT 指针仍然指向为类 `Derived` 创建的同一个表。因此，通过此 VFT 执行的 `Func1()` 无疑是 `Derived::Func1()`。

这就是虚函数表如何帮助 C++ 中（子类型）多态的实现。

隐藏虚函数表指针存在的证明通过列表 11.5 展示，该列表比较了两个相同类的 `sizeof`——一个有一个虚函数，而另一个没有。

**列表 11.5** 通过比较两个相同但仅在一个函数上声明为虚函数的类，证明隐藏 VFT 指针的存在。

点击此处查看代码图片

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class SimpleClass
4: {
5:     int a, b;
6:
7: public:
8:     void DoSomething() {}
9: };
10:
11: class Base
12: {
13:     int a, b;
14:
15: public:
16:     virtual void DoSomething() {}
17: };
18:
19: int main()
20: {
21:     cout << "sizeof(SimpleClass) = << sizeof(SimpleClass) << endl;
22:     cout << "sizeof(Base) = " << sizeof(Base) << endl;
23:     return 0;
24: }
```

### 使用 32 位编译器的输出

![Image](img/arrow.jpg)

点击此处查看代码图片

```text
sizeof(SimpleClass) = 8
sizeof(Base) = 12
```

### 使用 64 位编译器的输出

![Image](img/arrow.jpg)

点击此处查看代码图片

```text
sizeof(SimpleClass) = 8
sizeof(Base) = 16
```

## 分析

这是一个被精简到极限的示例。你看到两个类，`SimpleClass` 和 `Base`。

## 抽象基类与纯虚函数

无法被实例化的类被称为抽象基类（Abstract Base Class）。C++ 允许使用纯虚函数创建抽象基类。当虚函数被声明为纯虚函数时，如下所示：

点击此处查看代码图片

```cpp
class AbstractBase
{
public:
    // 定义纯虚函数
    virtual void DoSomething() = 0;
};
```

这本质上告诉编译器，派生自 `AbstractBase` 的类必须提供 `DoSomething()` 的实现：

点击此处查看代码图片

```cpp
class Derived: public AbstractBase
{
public:
    void DoSomething() // 必须实现
    {
      cout << "实现了虚函数" << endl;
    }
};
```

因此，`AbstractBase` 类的作用是强制 `Derived` 类提供虚方法的实现。这种基类可以强制派生类提供特定名称和签名的方法，这被称为接口（Interface）。再次考虑 `Fish` 类。想象一个 `Tuna`（金枪鱼）由于没有重写 `Fish::Swim()` 而无法快速游动。

让 `Fish` 成为带有 `Swim` 虚函数的抽象基类，可以确保派生自 `Fish` 的 `Tuna` 实现了 `Tuna::Swim()` 并像 `Tuna` 一样游动，而不是像任何 `Fish` 一样。参见列表 11.6。

```cpp
36:    Tuna myDinner;
38:    MakeFishSwim(myLunch);
39:    MakeFishSwim(myDinner);
41:    return 0;
42: }
```

### 输出

![Image](img/arrow.jpg)

点击此处查看代码图像

```text
鲤鱼在湖里游得很慢！

金枪鱼在海里游得很快！
```

## 分析

`main()` 函数中第 34 行（被注释掉的行）非常重要。它证明编译器不允许你实例化一个抽象基类（`ABC`）`Fish` 的实例。它期望一个具体的类，例如 `Fish` 的特化类——例如 `Tuna`——这在现实世界的物体安排中是有意义的。得益于第 7 行声明的纯虚函数 `Fish::Swim()`，`Tuna` 和 `Carp` 都被强制实现 `Tuna::Swim()` 和 `Carp::Swim()`。第 27–30 行实现了 `MakeFishSwim(Fish&)`，这证明了即使抽象基类不能实例化，你也可以将其作为引用或指针。因此，抽象基类是一种非常好的机制，用于声明你期望派生类实现并完成的函数。如果派生自 `Fish` 的类 `Trout` 忘记实现 `Trout::Swim()`，编译也会失败。

### 注意

抽象基类（Abstract Base Classes）通常简单称为 ABCs。

ABCs 有助于对你的程序执行某些设计约束。

## 使用 `virtual` 继承解决菱形问题

在第 10 章中，你看到了鸭嘴兽的奇特案例，它既是哺乳动物，又是鸟类，还是爬行动物。这是一个类 `Platypus` 需要继承自类 `Mammal`、类 `Bird` 和类 `Reptile` 的例子。然而，这些类又分别继承自一个更通用的类 `Animal`，如图 11.2 所示。

![Image](img/11fig02.jpg)

**图 11.2** 展示多继承的鸭嘴兽类图。

那么，当你实例化一个 `Platypus` 时会发生什么？对于一个 `Platypus` 实例，会被创建多少个 `Animal` 类实例？列表 11.7 有助于回答这个问题。

**列表 11.7** 检查一个 `Platypus` 实例对应的基类 `Animal` 实例数量。

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Animal
4: {
5: public:
6:     Animal()
7:     {
8:         cout << "Animal constructor" << endl;
9:     }
10:
11:     // sample member
12:     int age;
13: };
14:
15: class Mammal:public Animal
16: {
17: };
18:
19: class Bird:public Animal
20: {
21: };
22:
23: class Reptile:public Animal
24: {
25: };
26:
27: class Platypus:public Mammal, public Bird, public Reptile
28: {
29: public:
30:     Platypus()
31:     {
32:         cout << "Platypus constructor" << endl;
33:     }
34: };
35:
36: int main()
37: {
38:     Platypus duckBilledP;
39:
40:     // 取消注释查看编译失败
41:     // age 是模糊的，因为有三个基类实例
42:     // duckBilledP.age = 25;
43:
44:     return 0;
45: }
```

### 输出

![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Animal constructor

Animal constructor

Platypus constructor
```

## 分析

输出所示，由于多重继承以及 `Platypus` 的所有基类都继承自 `Animal`，对于每个 `Platypus` 实例都会创建三个 `Animal` 实例，如第 38 行所示。这很荒谬，因为 `Platypus` 仍然是一个继承了 `Mammal` 和 `Reptile` 特定属性的动物。`Animal` 实例数量的问题不仅限于内存。`Animal` 有一个整数 `Animal::age`（为了解释已保持为 public）。当你想要通过 `Platypus` 实例访问 `Animal::age` 时（如第 42 行所示），你会得到编译错误，这仅仅是因为编译器不知道你想设置的是 `Mammal::age` 还是 `Bird::age` 还是 `Reptile::age`。它可以变得更荒谬——如果你这样做，你可以设置所有三个：

```cpp
duckBilledP.Mammal::age = 25;
duckBilledP.Bird::age = 25;
duckBilledP.Reptile::age = 25;
```

显然，一只鸭嘴兽应该只有一个 `age`。然而你又希望 `Platypus` 既是 `Mammal`、`Bird` 和 `Reptile`。解决方案是虚继承。如果你期望一个派生类被用作基类，那么使用 `virtual` 关键字来定义它与基类的关系可能是一个好主意：

```cpp
class Derived1: public virtual Base
{
  // ... members and functions
};

class Derived2: public virtual Base
{
  // ... members and functions
};
```

一个更好的 `Platypus` 类（实际上是更好的 `Mammal` 类、`Bird` 类和 `Reptile` 类）在列表 11.8 中。

**列表 11.8** 继承中的 `virtual` 关键字如何帮助将基类 `Animal` 的实例数量限制为一个。

点击此处查看代码图像



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Animal
4: {
5: public:
6:     Animal()
7:     {
8:         cout << "Animal constructor" << endl;
9:     }
10:
11:     // sample member
12:     int age;
13: };
14:
15: class Mammal:public Animal
16: {
17: };
18:
19: class Bird:public Animal
20: {
21: };
22:
23: class Reptile:public Animal
24: {
25: };
26:
27: class Platypus:public Mammal, public Bird, public Reptile
28: {
29: public:
30:     Platypus()
31:     {
32:         cout << "Platypus constructor" << endl;
33:     }
34: };
35:
36: int main()
37: {
38:     Platypus duckBilledP;
39:
40:     // 因为只有一个 Age 实例，不再有编译错误
41:     duckBilledP.age = 25;
42:
43:     return 0;
44: }
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图像：

```text
Animal constructor

Platypus constructor
```

## 分析 ![Image](img/arrow.jpg)

对比之前的列表 11.7 的输出，你会发现构造的 `Animal` 类实例数量减少到了一个，这最终反映了只构造了一个 `Platypus` 的事实。这是因为在 `Mammal`、`Bird` 和 `Reptile` 类之间的关系使用了 `virtual` 关键字，它确保了当这些类组合在 `Platypus` 下时，共同的基类 `Animal` 仅存在一个实例。这解决了许多问题，其中之一是第 41 行现在不需要歧义消除即可编译。此外注意第 27 行使用 `final` 关键字，以确保 `Platypus` 类不能被用基类。

### 注意

C++ 中的 `virtual` 关键字通常在不同的语文中用于不同的目的。（我最好的猜测是有人想节省时间去发明一个恰当的关键字。）这里有一个总结：

我们在 `class BluefinTuna` 的声明中也使用了 `final`。这确保了 `class BluefinTuna` 不能用作基类。因此，以下操作将导致错误：

点击此处查看代码图像：

```cpp
class FailedDerivation:public BluefinTuna
{
};
```

除了通过虚函数 `Fish::Clone()` 展示虚拷贝构造函数外，Listing 11.9 还演示了关键字 `override` 和 `final` 的用法——后者同样适用于虚函数和类。它在第 8 行为 `class Fish` 备了一个虚析构函数。`main()` 函数中的第 52–56 行演示了如何声明一个指向基类 `Fish*` 的静态指针数组，并将各个元素分别赋值给新创建的 `Tuna`、`Carp`、`Tuna` 和 `Carp` 类型对象。注意这个名为 `myFishes` 的数组如何能够收集看似不同的类型，而这些类型都通过共同的基类型 `Fish` 相关联。与书中之前大部分为简单单调类型 `int` 的数组相比，这已经很酷了。如果这还不够酷，你还可以像第 60 行所示，在循环中使用通过虚函数 `Fish::Clone()` 将其拷贝到一个名为 `myNewFishes` 的 `Fish*` 类型新数组中。请注意你的数组非常小，只有四个元素。它可以更长，但对拷贝逻辑不会产生太大影响，只需要调整循环结束条件参数即可。第 64 行是实际检查之处，你对新数组中的每个存储元素调用了虚函数 `Fish::Swim()`，以验证 `Clone()` 是否将 `Tuna` 拷贝为了 `Tuna` 而不仅仅是 `Fish()`。输出证明了它确实如预期那样拷贝了 `Tuna` 和 `Carp`。另外注意，在 `BluefinTuna` 实例上使用的 `Swim()` 输出与 `Tuna` 相同，因为 `Tuna::Swim()` 被声明为 `final`。因此，`BluefinTuna` 不允许重写 `Swim()`，编译器为它执行了 `Tuna::Swim()`。

***

### DO（要做的）

- 务必记住将需要派生类重写的基类函数标记为 `virtual`。
- 务必记住纯虚函数会让你的类变成抽象基类（Abstract Base Class），这些函数必须由派生类实现。
- 务必在派生类中对意图重写基类功能的函数使用 `override` 关键字。
- 务必使用虚继承来解决菱形继承（Diamond Problem）。

### DON’T（不要做的）

- 不要忘记为你的基类提供一个虚析构函数。
- 不要忘记编译器不允许你创建抽象基类的独立实例。
- 不要忘记虚继承是为了确保菱形层次结构中的公共基类只有一个实例。
- 不要将 `virtual` 关键字在创建继承层次结构时使用的功能，与在声明基类函数时使用的功能混为一谈。

### Summary（总结）

在本节中，你学习了如何通过使用多态来在 C++ 代码中利用创建继承层次结构的力量。你学习了如何声明和编写虚函数——以及它们如何确保即使使用基类实例来调用虚方法，派生类的实现也能重写基类中的实现。你看到了纯虚函数是虚函数的一种特殊类型，它们确保了基类本身不能直接被实例化，从而成为定义派生类必须履行的接口的完美位置。最后，你看到了多重继承引起的菱形问题，以及 `virtual` 继承是如何帮助你解决它的。

### Q&A（问答）

**Q 为什么代码在没有它的情况下也能编译，基类函数还需要 `virtual` 关键字？**

**A** 没有 `virtual` 关键字，你无法确保调用 `objBase.Function()` 的地方会被重定向到 `Derived::Function()`。此外，代码编译并不是衡量其质量的唯一标准。

**Q 编译器为什么要创建虚函数表（Virtual Function Table）？**

**A** 为了存储函数指针，确保调用正确版本的虚函数。

**Q 基类是否应该始终有一个虚析构函数？**

**A** 理想情况下是这样的。只有这样你才能确保某人对一个...

点击此处查看代码图片：

```cpp
Base* pBase = new Derived();
delete pBase;
```

对类型为 `Base*` 的指针执行 `delete` 会导致析构函数 `~Derived()`。这在析构函数 `~Base()` 被声明为 `virtual` 时发生。

**Q 当我甚至无法独立实例化它时，抽象基类（Abstract Base Class）有什么用？**

**A** 抽象基类并不是为了作为独立对象被实例化的；相反，它总是为了被派生。它包含了纯虚函数，定义了派生类需要实现的最小蓝图，从而充当了接口的角色。

**Q 给定一个继承层次结构，我需要在所有虚函数的声明处使用 `virtual` 关键字，还是只需要在基类中使用？**

**A** 只需将函数声明为 `virtual` 一次，但该声明必须在基类中。

**Q 我可以在抽象基类中定义成员函数并拥有成员属性吗？**

**A** 当然可以。请记住，你仍然无法实例化抽象基类，因为它至少有一个需要派生类实现的纯虚函数。

### Workshop（工作坊）

工作坊提供了测验题帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用已知识的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题。

### Quiz（测试）

**1.** 你正在建模形状——圆形和三角形，并希望每个形状强制实现 `Area()` 和 `Print()`。你会如何做？

**2.** 编译器会为所有类创建虚函数表吗？

**3.** `class Fish` 有两个公共方法、一个纯虚函数和一些成员属性。它仍然是抽象基类吗？

### Exercises（练习题）

**1.** 一个实现了测验中圆形和三角形题目的继承层次结构。

**2. BUG BUSTERS（漏洞排查）：** 以下代码中的问题是什么：

点击此处查看代码图片：

```cpp
class Vehicle
{
public:
  Vehicle() {}
  ~Vehicle(){}
};

class Car: public Vehicle
{
public:
  Car() {}
  ~Car() {}
};
```

**3.** 在练习 2 的（未修复）代码中，如果这样创建并销毁 `car` 实例，构造函数和析构函数的执行顺序是怎样的：

点击此处查看代码图片：

```cpp
Vehicle* pMyRacer = new Car;
delete pMyRacer;
```

## 第 12 节 运算符类型与运算符重载（Lesson 12. Operator Types and Operator Overloading）

除了封装数据和方法外，类还可以封装*运算符*，使得对类实例的操作变得简单。你可以使用这些运算符对类对象执行赋值或加法操作，就像你在第 5 节](#ch05.html_ch05)“处理表达式、语句和运算符”中对整数的操作一样。就像函数一样，运算符也可以被重载。在本节中，你将学习：

- 使用 `operator` 关键字
- 一元运算符和二运算符
- 转换运算符
- 移动赋值运算符
- 不能重定义的运算符

## C++ 中的运算符是什么？

在语法层面上，运算符与函数之间几乎没有区别，只是使用了 `operator` 关键字。运算符的声明看起来非常像函数声明：

点击此处查看代码图片：

```cpp
return_type operator operator_symbol (...parameter list...);
```

在此例中，`operator_symbol` 可以是程序员定义的几种运算符类型中的任何一种。它可以是 `+`（加法）或 `&&`（逻辑与）等。操作数帮助帮助编译器区分不同的运算符。那么，既然 C++ 也支持函数，为什么还要提供运算符呢？

考虑一个名为 `Date`（日期）的工具类，它封装封装了日、月、年：

点击此处查看代码图片：

```cpp
Date holiday (12, 25, 2016);  // 初始化为 2016 年 12 月 25 日
```

假设你想增加一天并让实例包含下一天——即 2016 年 12 月 26 日——以下两个选项中哪一个更直观？

![Image](img/square.jpg) 选项 1（使用递增运算符）：

```cpp
++ holiday;
```

![Image](img/square.jpg) 选项 2（使用成员函数 `Increment()`）：

点击此处查看代码图片：

```cpp
holiday.Increment();  // 2016 年 12 月 26 日
```

显然，选项 1 的得分高于方法 `Increment()`。基于运算符的机制通过提供易用性和直观性方便了使用。在 `Date` 类中实现运算符（`<`）可以帮助你像这样比较两个 `class Date` 实例：

点击此处查看代码图片：

```cpp
if(date1 < date2)
{
    // 执行某些操作
}
else
{
    // 执行其他操作
}
```

运算符的使用场景比仅仅管理日期的类更广泛。在列表 9.9 的第 9 节“类与对象，](#ch09.html_ch09)”中介绍的 `MyString` 字符串工具类中，引入加法运算符（`+`）可以方便地进行拼接：

点击此处查看代码图片：

```cpp
MyString sayHello ("Hello ");
MyString sayWorld (" world");
MyString sumThem (sayHello + sayWorld); // 如果 MyString 支持 operator+
MyString
```

***

> 注意
>
> 实现相关运算符所付出的努力将通过类的易用性获得回报。

***

在宏观上，C++ 中的运算符可以分为两类：一元运算符和二元运算符。

### 一元运算符

正如名称所示，作用于单个操作数的运算符被称为一元运算符。在全局命名空间中实现或作为类的静态成员函数实现的一元运算符使用以下结构：

点击此处查看代码图片：

```cpp
return_type operator operator_type (parameter_type)
{
    // ... 实现
}
```

作为类的（非静态）成员的一元运算符具有类似的结构，但缺少参数，因为它所作用的单一参数是类实例本身（`*this`）：

点击此处查看代码图片：

```cpp
return_type operator operator_type ()
{
    // ... 实现
}
```

### 一元运算符的类型

可以重载（或重定义）的一元运算符如表 12.1。

**表 12.1** 一元运算符

#### 编写一元递增/减运算符

一元前缀递增运算符（`++`）可以在类声明中使用以下语法编写：

点击此处查看代码图片：

```cpp
// 一元递增运算符（前缀）
Date& operator ++ ()
{
    // 运算符实现代码
    return *this;
}
```

另一方面，后置递增运算符（`++`）具有不同的返回值和一个输入参数（该参数并不总是使用）：

点击此处查看代码图片：

```cpp
Date operator ++ (int)
{
    // 在递增日期之前，存储对象状态拷贝
    Date copy (*this);
    // 递增实现代码
    // 返回递增前的状态（因为是后置）
    return copy;
}
```

前缀和后置减运算符与递增运算符的语法相似，只是在看到 `++` 的地方包含 `--`。列表 12.1 显示了一个简单的 `Date` 类，它允许使用运算符（`++`）递增日期。

**列表 12.1** 一个处理日、月、年并允许递增和递减日的日历类

点击此处查看代码图片：

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Date
4: {
5: private:
6:     int day, month, year;
7:
8: public:
9:     Date(int d, int m, int y) : day(d), month(m), year(y) {}
10:    void DisplayDate()
{
11:        cout << month << "/" << day << "/" << year << endl;
12:    }
13:
14:    Date& operator ++ ()
15:    {
16:        day++;
17:        return *this;
18:    }
19:
20:    Date operator ++ (int)
21:    {
22:        Date copy (*this);
23:        day++;
24:        return copy;
25:    }
26:
27:    Date& operator -- ()
28:    {
29:        day--;
30:        return *this;
31:    }
32:
33:    Date operator -- (int)
34:    {
35:        Date copy (*this);
36:        day--;
37:        return copy;
38:    }
39: };
40:
41: int main ()
42: {
43:     Date holiday (12, 25, 2016);
44:     holiday.DisplayDate();
45:     ++holiday;
46:     holiday.DisplayDate();
47:     holiday ++;
48:     holiday.DisplayDate();
49:     --holiday;
50:     holiday.DisplayDate();
51:     holiday --;
52:     holiday.DisplayDate();
53:
54:     return 0;
55: }
```

点击此处查看代码图像：

```cpp
cout << holiday; // 缺少转换操作符导致错误
```

该代码会导致以下编译失败：`error: binary '<<' : no operator found which takes a right-hand operand of type 'Date' (or there is no acceptable conversion)`。此错误本质上表示 `cout` 不知道如何解释 `Date` 类的实例，因为 `class Date` 不支持将其内容转换为 `cout` 能够接受的类型的运算符。

我们知道 `cout` 可以与 `const char*` 良好地工作：

点击此处查看代码图像：

```cpp
std::cout << "Hello world"; // const char* 可以工作！
```

因此，让 `cout` 与 `Date` 类型的实例一起工作，可能简单只需要添加一个返回 `const char*` 版本的运算符即可：

点击此处查看代码图像：

```cpp
operator const char*()
{
    // 返回 char* 的运算符实现
}
```



列表 12.2 是此转换操作符的简单实现。

**列表 12.2** 为`class Date`实现转换操作符`const char*`

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <sstream> // 为 ostringstream 新增头文件
2: #include <string>
3: using namespace std;
4:
5: class Date
6: {
7: private:
8:     int day, month, year;
9:     string dateInString;
10:
11: public:
12:     Date(int inMonth, int inDay, int inYear)
13:         : month(inMonth), day(inDay), year(inYear) {};
14:
15:     operator const char*()
16:     {
17:         ostringstream formattedDate; // 辅助字符串构造
18:         formattedDate << month << " / " << day << " / " << year;
19:
20:         dateInString = formattedDate.str();
21:         return dateInString.c_str();
22:     }
23: };
24:
25: int main ()
26: {
27:     Date Holiday (12, 25, 2016);
28:
29:     cout << "Holiday is on: " << Holiday << endl;
30:
31:     // string strHoliday (Holiday); // OK!
32:     // strHoliday = Date(11, 11, 2016); // 也 OK!
33:
34:     return 0;
35: }
```

输出 ![Image](img/arrow.jpg)

```text
Holiday is on: 12 / 25 / 2016
```

## 分析 ![Image](img/arrow.jpg)

如第 15 行到 23 行所示，实现运算符`const char*`的好处在`main()`函数的第 29 行中可见。现在，`class Date`的实例可以直接在`cout`语句中使用，利用了`cout`理解`const char*`的特性。编译器会自动使用适当（在本例中是唯一可用）运算符的输出，传递给`cout`，从而在屏幕上显示日期。在你的运算符`const char*`实现中，你使用`std::ostringstream`将成员整数转换为`std::string`对象，如第 18 行所示。你本可以可以直接返回`formattedDate.str()`，但你在第 20 行中将其副本存储在私有成员`Date::dateInString`中，因为`formattedDate`是一个局部变量，它在运算符返回时会被销毁。因此，通过`str()`获取的指针在函数返回后将失效。

该运算符为使用`class Date`开启了新的可能性。它允许你直接将`Date`实例赋值给`string`：

点击此处查看代码图像

```cpp
string strHoliday (holiday);
strHoliday = Date(11, 11, 2016);
```

### 注意事项

注意，此类赋值会导致隐式转换，也就是说编译器使用了可用的转换操作符（在此例中为`const char*`），允许无预期的赋值无错误通过编译。为了避免隐式转换，请在运算符的开头使用`explicit`关键字，如下所示：

```cpp
explicit operator const char*()
{
    // 转换代码
}
```

使用`explicit`将强制程序员使用类型转换来断言转换意图：

```cpp
string strHoliday(static_cast<const char*>(Holiday));
strHoliday=static_cast<const char*>(Date(11,1,2016));
```

类型转换包括`static_cast`将在第 13 节“转换操作符”中详细讨论。

> **注意**
>
> 根据你认为你的类会被使用的次数，编写尽可能的操作符。如果你的应用程序需要整数表示形式，你可以这样编写：
>
> ```cpp
> explicit operator int()
> {
>     return day;
> }
> ```
>
> 这允许`Date`实例被转换为整数：
>
> ```cpp
> int d = static_cast<int>(Date(12, 25, 2016));
> ```
>
> 在本节中展示了与字符串使用的运算符。

### 解引用运算符`*`和成员运算符`->`

解引用运算符`*`和成员运算符`->`最常用于智能指针。智能指针是包装普通指针并简化内存管理的类。智能指针将在第 26 节“智能指针”中详细讨论。本节简要查看运算符重载如何帮助智能指针。

分析列表 12.3 中`unique_ptr`的用法，并理解它是如何通过`*`和`->`像指针一样工作的。

**列表 12.3** 使用`unique_ptr`管理动态分配的`class Date`实例

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <memory>  // 为 unique_ptr 新增头文件
2: using namespace std;
3:
4: class Date
5: {
6: private:
7:     int day, month, year;
8:     string dateInString;
9:
10: public:
11:     Date(int inMonth, int inDay, int inYear)
12:         : month(inMonth), day(inDay), year(inYear) {};
13:
14:     void DisplayDate()
15:     {
16:         cout << month << " / " << day << " / " << year << endl;
17:     }
18: };
19:
20: int main()
21: {
22:     unique_ptr<int> smartIntPtr(new int);
23:     *smartIntPtr = 42;
24:
25:     // 像 int* 一样使用智能指针类型
26:     cout << "Integer value is: " << *smartIntPtr << endl;
27:
28:     unique_ptr<Date> smartHoliday (new Date(12, 25, 2016));
29:     cout << "The new instance of date contains: ";
30:
31:     // 就像使用 Date* 一样使用 smartHoliday
32:     smartHoliday->DisplayDate();
33:
34:     return 0;
35: }
```

此示例演示了智能指针如何允许你使用普通的指针语法，如第 23 行和第 32 行所示。在第 23 行，你能够使用`*smartIntPtr`显示`int`的值，而在第 32 行中，你使用`smartHoliday->DisplayData()`就像这两个变量分别是`int*`和`Date*`一样。其中的奥诀在于`std::unique_ptr`指针类，它是智能的，因为它实现了`operator*`和`operator->`。

### 注意事项

智能指针类的功能远不止于像普通指针那样四处游走，或者在离开作用域时释放内存。请在第 26 节中了解更多关于此主题的知识。

要查看重载了这些运算符的简单智能指针类的实现，你可以简要访问列表 26.1。

## 二元运算符

在两个操作数上执行操作的运算符称为*二元运算符*。作为全局函数或静态成员函数实现的二元运算符的定义如下：

点击此处查看代码图像

```cpp
return_type operator_type (parameter1, parameter2);
```

作为类成员实现的二元运算符的定义为：

点击此处查看代码图像

```cpp
return_type operator_type (parameter);
```

二元运算符的类成员版本只接受一个参数的原因是，第二个参数通常源自类本身的属性。

### 二元运算符的类型

表 12.2 包含了可以在你的 C++ 应用中重载或重定义的二元运算符。

![图像](img/12tab02.jpg)

**表 12.2** 可重载的二元运算符

### 编程二元加法（`a+b`）和减法（`a-b`）运算符

与递//减运算符类似，二元加法和减法在定义后，允许你从实现这些运算符的类对象中加或减支持的数据类型的值。再次看看你的日历类`Date`。虽然你已经实现了增加`Date`的功能，使其让日历向前移动一天，但你仍然不支持让它（例如）向前移动五天。为了实现这一点，你需要实现二元运算符`+`，正如列表 12.4 中的代码所示。

**列表 12.4** 具有二元加法运算符的日历类

点击此处查看代码图像

```cpp
0: #includeinclude <iostream>

1: using namespace std;

2:

3: class Date

4: {

5: private:

6:     int day, month, year;

7:     string dateInString;

8:

9: public:

10:     Date(int inMonth, int inDay, int inYear)

11:         : month(inMonth), day(inDay), year(inYear) {};

12:

13:     Date operator + (int daysToAdd) // binary addition

14:     {

15:         Date newDate (month, day + daysToAdd, year);

16:         return newDate;

17:     }

18:

19:     Date operator - (int daysToSub) // binary subtraction

20:     {

21:         return Date(month, day - daysToSub, year);

22:     }

23:

24:     void DisplayDate()

25:     {

26:         cout << month << " / " << day << " / " << year << endl;

27:     }

28: };

29:

30: int main()

31: {

32:     Date Holiday (12, 25, 2016);

33:     cout << "Holiday on: ";

34:     Holiday.DisplayDate ();

35:

36:     Date PreviousHoliday (Holiday - 19);

37:     cout << "Previous holiday on: ";

38:     PreviousHoliday.DisplayDate();

39:

40:     Date NextHoliday(Holiday + 6);

41:     cout << "Next holiday on: ";

42:     NextHoliday.DisplayDate ();

43:

44:     return 0;
}
```

输出 ![图像](img/arrow.jpg)

点击此处查看代码图像

```text
Holiday on: 12 / 25 / 2016

Previous holiday on: 12 / 6 / 2016

Next holiday on: 12 / 31 / 2016
```

### 分析 ![图像](img/arrow.jpg)

第 13 行到第 22 行包含了二元运算符`+`和`operator(-)`的实现，它们允许在`main()`中第 40 行和第 36 行中看到的简单加减法语法。二元加法运算符在字符串类中也将有用。在第 9 节中，你分析了一个封装了内存管理的简单字符串包装器`MyString`。

### 加法赋值（`+=`）和减法赋值（`-=`）运算符

加法赋值运算符如`a += b;`允许对`Date`对象增加一个整数值。列表 12.5 展示了了给定整数输入。

你的`class Date`类现在允许用户添加或删除天数，就像它们处理整数一样，使用接受`int`作为参数的加或减赋值运算符。你甚至可以为加赋值运算符（`+=`）提供重载版本，使其与虚构类`Days`的实例配合：

点击此处查看代码图片

```cpp
// operator that adds a Days to an existing Date
void operator += (const Days& daysToAdd)
{
    day += daysToAdd.GetDays();
}
```

### 注意事项

乘法赋值`*=`、除法赋值`/=`、取模赋值`%=`、减法赋值`-=`、左移赋值`<<=`、右移赋值`>>=`、异或赋值`^=`、按位包含或赋值`|=`以及按位与赋值`&=`运算符的语法与列表 12.5 中所示的加赋值运算符相似。

虽然重载运算符的最终目标是使类变得易用且直观，但在许多情况下，实现某个运算符可能并没有意义。例如，我们的日历类`Date`完全没有需要使用按位与赋值`&=`运算符。该类的任何用户都不应该期望（甚至考虑）通过像`greatDay &= 20;`这样的操作获得有用结果。

### 重载相等（`==`）和不相等（`!=`）运算符

当`class Date`的用户比较一个实例与另一个实例时，你期望什么：

点击此处查看代码图片

```cpp
if (date1 == date2)
{
    // Do something
}
else
{
    // Do something else
}
```

在缺少相等运算符`==`的情况下，编译器简单地对两个对象进行二值比较，并在它们完全相同时返回`true`。这种二值比较对于包含简单数据类型的类实例（例如目前的`Date`类）有效，但如果涉及的类具有非静态字符串成员（`char*`），例如列表 9.9 中的`MyString`，则无法工作。当两个`class MyString`实例进行比较时，成员属性的二值比较实际上比较的是成员字符串指针的值（`MyString::buffer`）。即使字符串内容相同，这些值也是不等的。涉及两个`MyString`实例的比较将一律返回`false`。你通过定义比较运算符来解决这个问题。相等运算符的通用表达式如下：

点击此处查看代码图片

```cpp
bool operator== (const ClassType& compareTo)
{
    // comparison code here, return true if equal else false
}
```

不相等运算符可以复用相等运算符：

点击此处查看代码图片

```cpp
bool operator!= (const ClassType& compareTo)
{
    // comparison code here, return true if inequal else false
}
```

不相等运算符可以是相等运算符结果的反反（逻辑非）。列表 12.6 展示了由我们的日历类`Date`定义的比较运算符。

**分列表 12.6** 展示了运算符`==`和`!=`

点击此处查看代码图片



```cpp
0: #include <iostream>
1: using namespace std;
2:
3: class Date
4: {
5: private:
6:     int day, month, year;
7:
8: public:
9:     Date(int inMonth, int inDay, int inYear)
10:         : month(inMonth), day(inDay), year(inYear) {}
11:
12:     bool operator== (const Date& compareTo)
13:     {
14:         return ((day == compareTo.day)
15:                 && (month == compareTo.month)
16:                 && (year == compareTo.year));
17:     }
18:
19:     bool operator!= (const Date& compareTo)
20:     {
21:         return !(this->operator==(compareTo));
22:     }
23:
24:     void DisplayDate()
25:     {
26:         cout << month << " / " << day << " / " << year << endl;
27:     }
28: };
29:
30: int main()
31: {
32:     Date holiday1 (12, 25, 2016);
33:     Date holiday2 (12, 31, 2016);
34:
35:     cout << "holiday 1 is: ";
36:     holiday1.DisplayDate();
37:     cout << "holiday 2 is: ";
38:     holiday2.DisplayDate();
39:
40:     if (holiday1 == holiday2)
41:         cout << "Equality operator: The two are on same day" << endl;
42:     else
43:         cout << "Equality operator: The two are on different days" << endl;
44:
45:     if (holiday1 != holiday2)
46:         cout << "Inequality operator: The two are on different days" << endl;
47:     else
48:         cout << "Equality operator: The two are on same day" << endl;
49:
50:     return 0;
51: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
holiday 1 is: 12 / 25 / 2016

holiday 2 is: 12 / 31 / 2016

operator<: holiday1 happens first

operator>: holiday2 happens later

operator<=: holiday1 happens on or before holiday2

operator>=: holiday2 happens on or after holiday1
```

## 分析 ![Image](img/arrow.jpg)

感兴趣的运算符实现在第 12 行到第 50 行，并部分重用了你在列表 12.6 中看到的运算符（`==`）。运算符 `==`、`<` 和 `>` 的实现已被其他部分所消耗。

这些运算符在 `main()` 函数的第 68 行到第 78 行之间被调用，这表明现在比较两个不同的日期是多么简单。

### 重载拷贝赋值运算符（`=`）

在某些情况下，你想要将一个类实例的内容赋值给另一个，例如：

点击此处查看代码图像

```cpp
Date holiday(12, 25, 2016);
Date anotherHoliday(1, 1, 2017);
anotherHoliday = holiday; // 使用拷贝赋值运算符
```

此赋值调用了编译器在你未提供运算符时在你的类中内置的默认拷贝赋值运算符。根据你的类的性质，默认拷贝赋值运算符可能是不足的，特别是当你的类管理一个不会拷贝的资源时。

默认拷贝赋值运算符的这个问题与第 9 节中讨论的默认拷贝构造函数的问题相似。为了像拷贝构造函数一样确保深拷贝，你需要指定一个相应的拷贝赋值运算符：

点击此处查看代码图像

```cpp
ClassType& operator= (const ClassType& copySource)
{
    if(this != &copySource)  // 防止拷贝到自身
    {
        // 拷贝赋值运算符实现
    }
    return *this;
}
```

如果你的类封装了原始指针，如列表 9.9 所示的 `class MyString`，那么深拷贝是非常重要的。为了确保赋值过程中的深拷贝，请如列表 12.8 所示定义一个拷贝赋值运算符。

**列表 12.8** 源自列表 9.9 的改进版 `class MyString`，带有拷贝赋值运算符 `=`

点击此处查看代码图像

```cpp
0: #include <iostream>
1: using namespace std;
2: #include <string.h>
3: class MyString
4: {
5: private:
6:     char* buffer;
7:
8: public:
9:     MyString(const char* initialInput)
10:     {
11:         if(initialInput != NULL)
12:         {
13:             buffer = new char [strlen(initialInput) + 1];
14:             strcpy(buffer, initialInput);
15:         }
16:         else
17:             buffer = NULL;
18:     }
19:
20:     // 拷贝赋值运算符
21:     MyString& operator= (const MyString& copySource)
22:     {
23:         if ((this != &copySource) && (copySource.buffer != NULL))
24:         {
25:             if (buffer != NULL)
26:                 delete[] buffer;
27:
28:             // 通过分配 buffer 确保深拷贝
29:             buffer = new char [strlen(copySource.buffer) + 1];
30:
31:             // 将从源拷贝到本地缓冲区
32:             strcpy(buffer, copySource.buffer);
33:         }
34:
35:         return *this;
36:     }
37:
38:     operator const*
39:     {
40:         return buffer;
41:     }
42:
43:     ~MyString()
44:     {
45:         delete[] buffer;
46:     }
47: };
48:
49: int main()
50: {
51:     MyString string1("Hello ");
52:     MyString string2("World");
53:     cout << "Before assignment: " << string1 << endl;
54:     string2 = string1;
55:     cout << "After assignment: " << string2 << endl;
56:     return 0;
57: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
赋值前: Hello

赋值后: Hello
```

## 分析 ![Image](img/arrow.jpg)

感兴趣的运算符实现在第 12 行到第 50 行，并部分重用了你在列表 12.6 中看到的运算符（`==`）。运算符 `==`、`<` 和 `>` 的实现已被其他部分所消耗。

这些运算符在 `main()` 函数的第 68 行到第 78 行之间被调用，这表明现在比较两个不同的日期是多么简单。

### 重载拷贝赋值运算符（`=`）

在某些情况下，你想要将一个类实例的内容赋值给另一个，例如：

点击此处查看代码图像

```cpp
Date holiday(12, 25, 2016);
Date anotherHoliday(1, 1, 2017);
anotherHoliday = holiday; // 使用拷贝赋值运算符
```

此赋值调用了编译器在你未提供运算符时在你的类中内置的默认拷贝赋值运算符。根据你的类的性质，默认拷贝赋值运算符可能是不足的，特别是当你的类管理一个不会拷贝的资源时。

默认拷贝赋值运算符的这个问题与第 9 节中讨论的默认拷贝构造函数的问题相似。为了像拷贝构造函数一样确保深拷贝，你需要指定一个相应的拷贝赋值运算符：

点击此处查看代码图像

```cpp
ClassType& operator= (const ClassType& copySource)
{
    if(this != &copySource)  // 防止拷贝到自身
    {
        // 拷贝赋值运算符实现
    }
    return *this;
}
```

如果你的类封装了原始指针，如列表 9.9 所示的 `class MyString`，那么深拷贝是非常重要的。为了确保赋值过程中的深拷贝，请如列表 12.8 所示定义一个拷贝赋值运算符。

**列表 12.8** 源自列表 9.9 的改进版 `class MyString`，带有拷贝赋值运算符 `=`

点击此处查看代码图像



```cpp
0: #include <iostream>
1: using namespace std;
2: #include <string.h>
3: class MyString
4: {
5: private:
6:     char* buffer;
7:
8: public:
9:     MyString(const char* initialInput)
10:     {
11:         if(initialInput != NULL)
12:         {
13:             buffer = new char [strlen(initialInput) + 1];
14:             strcpy(buffer, initialInput);
15:         }
16:         else
17:             buffer = NULL;
18:     }
19:
20:     // 拷贝赋值运算符
21:     MyString& operator= (const MyString& copySource)
22:     {
23:         if ((this != &copySource) && (copySource.buffer != NULL))
24:         {
25:             if (buffer != NULL)
26:                 delete[] buffer;
27:
28:             // 通过分配 buffer 确保深拷贝
29:             buffer = new char [strlen(copySource.buffer) + 1];
30:
31:             // 将从源拷贝到本地缓冲区
32:             strcpy(buffer, copySource.buffer);
33:         }
34:
35:         return *this;
36:     }
37:
38:     operator const*
39:     {
40:         return buffer;
41:     }
42:     ~MyString()
43:     {
44:         delete[] buffer;
45:     }
46: };
47: int main()
48: {
49:     MyString string1("Hello ");
50:     MyString string2("World");
51:     cout << "Before assignment: " << string1 << endl;
52:     string2 = string1;
53:     cout << "After assignment: " << string2 << endl;
54:     return 0;
55: }
```

### 下标运算符（`[]`）

允许以数组风格 `[]` 访问类的运算符被称为下标运算符。下标运算符的典型语法为：

点击此处查看代码图像

```cpp
return_type& operator [] (subscript_type& subscript);
```

所以，当你创建一个如 `MyString` 这样封装了 `char* buffer` 内的动态字符数组的类时，下标运算符使得随机访问缓冲区中的单个字符变得非常容易：

点击此处查看代码图像

```cpp
class MyString
{
    // ... 其他类成员
public:
    /*const*/ char& operator [] (int index) /*const*/
    {
        // 返回缓冲区中位置 index 处的字符
    }
};
```

列表 12.9 中的示例展示了下标运算符（`[]`）如何帮助用户使用标准的数组语义遍历 `MyString` 实例中包含的字符。

```cpp
using namespace std;

class MyString
{
private:
    char* buffer;

    // 私有默认构造函数
    MyString() {}

public:
    // 构造函数
    MyString(const char* initialInput)
    {
        if(initialInput != NULL)
        {
            buffer = new char [strlen(initialInput) + 1];
            strcpy(buffer, initialInput);
        }
        else
            buffer = NULL;
    }

    // 拷贝构造函数：在此插入 Listing 9.9
    MyString(const MyString& copySource);

    // 拷贝赋值运算符：在此插入 Listing 12.8
    MyString& operator= (const MyString& copySource);

    const char& operator[] (int index) const
    {
        if (index < GetLength())
            return buffer[index];
    }

    // 析构函数
    ~MyString()
    {
        if (buffer != NULL)
            delete [] buffer;
    }

    int GetLength() const
    {
        return strlen(buffer);
    }

    operator const char*()
    {
        return buffer;
    }
};

int main()
{
    cout << "Type a statement: ";
    string strInput;
    getline(cin, strInput);

    MyString youSaid(strInput.c_str());

    cout << "Using operator[] for displaying your input: " << endl;
    for(int index = 0; index < youSaid.GetLength(); ++index)
        cout << youSaid[index] << " ";
    cout << endl;

    cout << "Enter index 0 - " << youSaid.GetLength() - 1 << ": ";
    int index = 0;
    cin >> index;
    cout << "Input character at zero-based position: " << index;
    cout << " is: "<< youSaid[index] << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入一个语句：Hey subscript operators[] are fabulous

使用 `operator[]` 显示你的输入：

H e y    s u b s c r i p t    o p e r a t o r s [ ]    a r e    f a b u l o u s

输入索引 0 - 37：2

从 0 开始计数的位置上的字符：2 是：y

分析 ![Image](img/arrow.jpg)

这是一个有趣的程序，它接收你输入的句子，如第 61 行所示，使用它构造一个 `MyString` 对象，然后利用 `for` 循环逐个字符地打印字符串。

### 运算符 `()`

运算符 `()` 允许对象像函数一样被调用。这被称为函数对象或仿函数（functor）。这些对象在标准模板库（STL）中频繁使用，因为与普通函数不同，它们可以维护状态。

在下面的示例中，`Display` 类实现了 `operator()` 来打印字符串。

```cpp
#include <iostream>
#include <string>

using namespace std;

class Display
{
public:
    void operator (string input) const
    {
        cout << input << endl;
    }
};

int main()
{
    Display displayFuncObj;

    // 等同于 displayFuncObj.operator () ("Display this string!");
    displayFuncObj ("Display this string!");

    return 0;
}
```

### 注意事项

在实现下标运算符时，如果函数没有修改对象的属性，那么使用 `const` 关键字是非常关重要的。如 Listing 12.9 所示，提供 `operator[]` 的 `const` 版本可以确保该类能与 `const` 对象一起。

### 用于高性能编程的移动构造函数和移动赋值运算符

移动构造函数和移动赋值运算符是性能优化特性，它们已成为 C++11 的一部分，确保了临时值（在语句结束后不再存在的右值）不会被浪费性地复制。这在处理管理动态分配资源的类（例如动态数组类或字符串类）时特别有用。

```cpp
MyString Hello("Hello ");
MyString World("World");
MyString CPP(" of C++");
MyString sayHello(Hello + World + CPP);  // operator+, 构造函数
MyString sayHelloAgain ("overwrite this");
sayHelloAgain = Hello + World + CPP;  // operator+, 拷贝构造函数, 拷贝赋值运算符=
```

这种让三个字符串拼接变得简单的结构使用了二元加法 `operator+`：

点击此处查看代码图像

```cpp
MyString operator+ (const MyString& addThis)
{
   MyString newStr;
   if (addThis.buffer != NULL)
   {
      // 拷贝到 newStr
   }
   return newStr;  // 按值返回，调用拷贝构造函数
}
```

在方便字符串的字符串的同时，加法运算符 `operator+` 可能会导致性能问题。创建 `sayHello` 需要执行两次加法运算符。每次执行 `operator+` 都会导致创建一个临时副本，因为 `MyString` 是按值返回的，从而导致拷贝构造函数的执行。拷贝构造函数执行深拷贝——拷贝到一个临时值，该临时值在表达式结束后就不再存在。因此，此表达式产生了临时副本（对于纯主义者来说是右值），这些副本在语句执行后不再需要，因此是 C++ 强制导致的性能瓶颈。好吧，至少在最近以前如此。

这个问题现在在 C++11 中终于得到了解决，编译器能够特异地识别临时对象，并使用程序员提供的移动构造函数和移动赋值运算符。

### 声明移动构造函数和移动赋值运算符

移动构造函数的语法如下：

点击此处查看代码图像

```cpp
class Sample
{
private:
   Type* ptrResource;
public:
   Sample(Sample&& moveSource) // 移动构造函数，注意 &&
   {
      ptrResource = moveSource.ptrResource; // 获取所有权，开始移动
      moveSource.ptrResource = NULL;
   }
   Sample& operator= (Sample&& moveSource)//移动赋值运算符，注意 &&
   {
      if(this != &moveSource)
      {
         delete [] ptrResource;  // 释放自己的资源
         ptrResource = moveSource.ptrResource;  // 获取所有权，开始移动
         moveSource.ptrResource = NULL;  // 释放移动源的所有权
      }
   }
   Sample(); // 默认构造函数
   Sample(const Sample& copySource); // 拷贝构造函数
   Sample& operator= (const Sample& copySource); // 拷贝
};
```

因此，移动构造函数和赋值运算符的声明与普通的拷贝构造函数和拷贝赋值运算符的区别在于输入参数的类型为 `Sample&&`。此外，由于输入参数是移动源，它不能是 `const` 参数，因为它会被修改。返回值保持不变，因为它们分别是构造函数和赋值运算符的重载版本。

符合 C++11 标准的编译器确保对于右值临时对象，使用移动构造函数而不是拷贝构造函数，并调用移动赋值运算符而不是拷贝赋值运算符。在对这两个函数的实现中，你确保不是拷贝，而是简单地将资源从源移动到目标。列表 12.11 展示了这两个新特性在优化 `class MyString` 方面的有效性。

**列表 12.11** 除了拷贝构造函数和拷贝赋值运算符，带有移动构造函数和移动赋值运算符的 `class MyString`

点击此处查看代码图像



```cpp
#include <iostream>
#include <string.h>
using namespace std;

class MyString
{
private:
    char* buffer;

    MyString(): buffer(NULL) // 私有默认构造函数
    {
        cout << "Default constructor called" << endl;
    }

public:
    MyString(const char* initialInput) // 构造函数
    {
        cout << "Constructor for: " << initialInput << endl;
        if(initialInput != NULL)
            buffer = new char [strlen(initialInput) + 1];
            strcpy(buffer, initialInput);
        else
            buffer = NULL;
    }

    MyString(MyString&& moveSrc) // 移动构造函数
    {
        cout << "Move constructor moves: " << moveSrc.buffer << endl;
        if(moveSrc.buffer != NULL)
            {
                buffer = moveSrc.buffer; // 获取所有权即“移动”
                moveSrc.buffer = NULL;  // 释放移动源
            }
    }

    MyString& operator= (MyString&& moveSrc) // 移动赋值运算符
    {
        cout << "Move assignment op. moves: " << moveSrc.buffer << endl;
        if((moveSrc.buffer != NULL) && (this != &moveSrc))
            {
                delete[] buffer; // 释放自己的缓冲区

                buffer = moveSrc.buffer; // 获取所有权即“移动”
                moveSrc.buffer = NULL;  // 释放移动源
            }

        return *this;
    }

    MyString(const MyString& copySrc) // 拷贝构造函数
    {
        cout << "Copy constructor copies: " << copySrc.buffer << endl;
        if (copySrc.buffer != NULL)
            {
                buffer = new char[strlen(copySrc.buffer) + 1];
                strcpy(buffer, copySrc.buffer);
            }
        else
            buffer = NULL;
    }

    MyString& operator= (const MyString& copySrc) // 拷贝赋值
    {
        cout << "Copy assignment op. copies: " << copySrc.buffer << endl;
        if(this != &copySrc)
            {
                delete[] buffer; // 释放自己的缓冲区

                buffer = new char[strlen(copySrc.buffer) + 1];
                strcpy(buffer, copySrc.buffer);
            }

        return *this;
    }

    ~MyString() // 析构函数
    {
        if (buffer != NULL) 
            delete[] buffer;
    }

    int GetLength()
    {
        return strlen(buffer);
    }
};

int main()
{
    MyString Hello("Hello ");
    MyString World("World");
    MyString CPP(" of C++");

    MyString sayHelloAgain ("overwrite this");
    sayHelloAgain = Hello + World + CPP;

    return 0;
}
```

调用构造函数：overwrite this

`operator+` 被调用：

调用默认构造函数

移动构造函数移动：Hello World

`operator+` 被调用：

调用默认构造函数

移动构造函数移动：Hello World of C++

移动赋值运算符移动：Hello World of C++

分析 ![Image](img/arrow.jpg)

这可能是一个很长的代码示例，但大部分内容在之前的示例和课程中已经演示过了。此列表最重要的部分是第 26 行到 48 行，这些行分别实现了移动构造函数和移动赋值运算符。输出中受 C++11 新增特性影响的部分已用粗体标记。注意看，与没有这两个实体的相同类相比，输出发生了巨大的变化。如果你再次查看移动构造函数和移动赋值运算符的实现，你会发现移动语义本质上是通过从移动源 `moveSrc` 获取资源的所有权来实现，如移动构造函数第 31 行和移动赋值运算符第 43 行所示。紧接着，如第 32 行和 44 行所示，将移动指针赋值为 `NULL`。这种对 `NULL` 的赋值确保了作为移动源的实例的析构函数在第 80 行不会通过 `delete` 执行任何内存释放，因为所有权已经转移到了目标对象。注意，在缺少移动构造函数的情况下，会调用拷贝构造函数对指向的字符串进行深拷贝。因此，移动构造函数通过减少不需要的内存分配和拷贝步骤了大量的处理时间。

编写移动构造函数和移动赋值运算符完全可选的。与拷贝构造函数和拷贝赋值运算符不同，编译器不会为你添加默认实现。

使用此特性可以优化指向动态分配资源的类的功能，否则在仅临时需要的情况下，这些资源也会被深拷贝。

### 用户自定义字面量

字面量常量是在第 3 Lesson “使用变量，声明常量.”中引入的。以下是几个示例：

点击此处查看代码图像

```cpp
int bankBalance = 10000;

double pi = 3.14;

char firstAlphabet = ‘a’;

const char* sayHello = "Hello!";
```

在前面的代码中，`10000`、`3.14`、`‘a’` 和 `"Hello!"` 全都是字面量常量！C++11 通过允许你定义自己的字面量扩展了标准的支持。例如，如果你正在开发一个处理热力学的科学应用程序，你可能希望所有温度都使用名为开尔文的比例进行存储和操作。你现在可以使用类似于下面的语法声明所有的温度：

点击此处查看代码图像

```cpp
Temperature k1 = 32.15_F;

Temperature k2 = 0.0_C;
```

使用你定义的字面量 `_F` 和 `_C`，你的应用程序变得更容易阅读，因此也更容易维护。

要定义自己的字面量，你可以这样定义 `operator ""`：

点击此处查看代码图像

```cpp
ReturnType operator "" YourLiteral(ValueType value)
{
    // 此处编写转换代码
}
```

### 注意

根据用户自定义字面量的性质，`ValueType` 参数将被限制为以下类型之一：

- `unsigned long long int` 用于整数字面量
- `long double` 用于浮点字面量
- `char`、`wchar_t`、`char16_t` 和 `char32_t` 用于字符字面量
- `const char*` 用于原始字符串字面量
- `const char*` 配合 `size_t` 用于字符串字面量
- `const wchar_t*` 配合 `size_t` 用于字符串字面量
- `const char16_t*` 配合 `size_t` 用于字符串字面量
- `const char32_t*` 配合 `size_t` 用于字符串字面量

列表 12.12 展示了一个转换类型的用户自定义字面量。

**列表 12.12** 从华华和摄度转换为开尔文标

点击此处查看代码图像

```cpp
#include <iostream>
using namespace std;

struct Temperature
{
    double Kelvin;
    Temperature(long double kelvin) : Kelvin(kelvin) {}
};

Temperature operator"" _C(long double celcius)
{
    return Temperature(celcius + 273);
}

Temperature operator "" _F(long double fahrenheit)
{
    return Temperature((fahrenheit + 459.67) * 5 / 9);
}

int main()
{
    Temperature k1 = 32.15_F;
    Temperature k2 = 0.0_C;

    cout << "k1 is " << k1.Kelvin << " Kelvin" << endl;
    cout << "k2 is " << k2.Kelvin << " Kelvin" << endl;

    return 0;
}
```

A 当编写此类类时，你必须清晰地定义在以下场景下的行为：实例通过赋值直接拷贝到另一个实例，或者通过按值传递给函数进行间接拷贝。你通常需要实现拷贝构造函数、拷贝赋值运算符和析构函数。如果你想在某些情况下微调该类的性能，还需要实现移动构造函数和移动赋值运算符。为了允许对类实例存储的元素进行类似数组的访问，你需要重载下标运算符 `operator[]`。

Q 我有一个某个类的实例 `object`。我想支持这种语法：`cout << object;`。我需要实现什么运算符？

A 你需要实现一个转换运算符，允许你的类在直接被解释为 `std::cout` 可以处理的类型。一种方法是定义 `operator char*()`，正如你在代码段列表 12.2 中做的那样。

Q 我想创建自己的智能指针类。为了让它具备基本功能，我最少需要实现哪些函数和运算符？

A 智能指针需要提供像 `*pSmartPtr` 或 `pSmartPtr->Func()` 那样作为普通指针使用的能力。为了实现这一点，你需要实现 `operator(*)` 和 `operator(->)`。此外，为了使其具有“智能性”，你还需要通过相应编写析构函数来处理资源的自动释放/返回，并通过实现拷贝构造函数和拷贝赋值运算符来明确定义拷贝或赋值的工作方式，或者通过将这两个声明为 `private` 来禁止它们。

## 工作坊

工作坊包含测验题，帮助你巩固对所涵盖内容的理解，并提供练习以获得使用所学知识。在查看附录 E 中的答案之前，尝试回答测试和练习题，并确保在进入下一节之前理解了答案。

### 测验

**1.** 我的下标运算符 `[]` 可以返回 `const` 和非 `const` 变体的返回类型吗？

点击此处查看代码图片

```cpp
const Type& operator[](int index);
Type& operator[](int index); // 这样可以吗？
```

**2.** 你会将拷贝构造函数或拷贝赋值运算符声明为 `private` 吗？

**3.** 为你的 `class Date` 定义移动构造函数和移动赋值运算符有意义吗？

### 练习

**1.** 为 `Date` 类编写一个转换运算符，将它持有的日期转换为一个唯一的整数。

**2.** 为 `class DynIntegers` 编写一个移动构造函数和移动赋值运算符，该类以私有成员 `int*` 的形式封装了一个动态分配的数组。

## 第 13 节 转换运算符

转换是一种程序员可以临时或永久地改变编译器对对象解释的机制。注意，这并不意味着程序员改变了对象本身——他只是改变了对对象的解释。改变对象解释的运算符被称为强制转换运算符。

在本节中，你将学习：

- ![Image](img/square.jpg) 转换运算符的必要性
- ![Image](img/square.jpg) 为什么 C 风格转换不受某些 C++ 程序员的欢迎
- ![Image](img/square.jpg) 四种 C++ 转换运算符
- ![Image](img/square.jpg) 向上转换和向下转换的概念
- ![Image](img/square.jpg) 为什么 C++ 转换运算符并非一直的首选

## 转换的必要性

在一个由编写良好的 C++ 应用程序组成的完美类型安全且强类型的世界里，本不需要转换和转换运算符。然而，我们生活在一个现实世界中，由许多不同的人和供应商编写且通常使用不同环境的模块必须共同工作。为了实现这一点，编译器经常需要被指示以特定的方式解释数据，以便它们能够编译并让应用程序正常运行。

让我们来看一个现实世界的例子：尽管大多数 C++ 编译器可能支持 `bool` 作为原生类型，但仍在使用许多多年前用 C 语言编写的库。这些为 C 编译器设计的库必须依赖使用整数类型来存储布尔数据。因此，这些编译器上的 `bool` 类似于：

```cpp
typedef unsigned short BOOL;
```

返回布尔数据的函数将声明为：

```cpp
BOOL IsX ();
```

现在，如果要在用最新版本的 C++ 编译器编写的新应用程序中使用此类库，程序员必须找到一种方法，使他的 C++ 编译器函数理解的 `bool` 数据类型与库理解的 `BOOL` 数据类型一致。实现这一点的方法是使用转换：

点击此处查看代码图片

```cpp
bool Result = (bool)IsX (); // C 风格转换
```

C++ 的演进看到了新的 C++ 转换运算符的出现，这在 C++ 编程社区中引发了分裂：一组继续在他们的 C++ 应用程序中使用 C 风格转换，另一组则虔诚地转换为 C++ 编译器引入的转换关键字。前一组的论点是 C++ 转换使用起来繁琐，且有时在功能上的差异微不足道，以至于只有理论价值。后一组（显然由 C++ 纯洁主义者组成）指出了 C 风格转换的缺陷。

由于现实世界存在这两种代码，简单阅读本节、了解每种风格的优缺点并形成自己的观点是好的。

### 为什么 C 风格转换不受某些 C++ 程序员的欢迎

类型安全是 C++ 程序员在赞美这种语言特性时信奉的格言。事实上，大多数 C++ 编译器甚至不允许你这样操作：

点击此处查看代码图片

```cpp
char* staticStr = "Hello World!";
int* intArray = staticStr; // 错误：无法将 char*  int*
```

……确实如此！

现在，C++ 编译器仍然需要向下兼容以保持旧代码编译，因此自动允许如下语法：

点击此处查看代码图片

```cpp
int* intArray = (int*)staticStr; // 解决一个问题，产生另一个
```

这种 C 风格转换实际上强制编译器将其解释为程序员方便选择的类型——在这种情况下，程序员并没有考虑编译器最初报告错误是有充分理由的，而是简单地强迫编译器服从。这显然不能让看到类型安全被强制转换破坏的 C++ 程序员感到舒服。



## C++ 转换运算符

尽管转换有缺点，但转换本身的概念无法被。在许多情况下，转换是解决重要兼容问题的合法要求。C++ 额外提供了一种特定继承场景的转换运算符，这在 C 编程中是不存在的。

四种 C++ 转换运算符为：

- ![Image](img/square.jpg) `static_cast`
- ![Image](img/square.jpg) `dynamic_cast`
- ![Image](img/square.jpg) `reinterpret_cast`
- ![Image](img/square.jpg) `const_cast`

转换运算符的使用语法是一致的：

点击此处查看代码图片

```cpp
destination_type result = cast_operator<destination_type> (object_to_cast);
```

### 使用 `static_cast`

`static_cast` 是一种用于在相关类型之间转换指针的机制，并对于原本会自动或隐式转换的标准数据类型执行显式类型转换。对于指针而言，`static_cast` 实现了基本的编译时检查，以确保指针被转换为相关类型。这是对 C 风格强制转换的改进，C 风格强制转换允许将一个对象的指针转换为完全无关的类型而不产生任何报错。如下代码示例所示，使用 `static_cast` 可以将指针向上转型为基类类型，也可以向下转型为派生类类型。

点击查看代码图像

```cpp
Base* objBase = new Derived ();

Derived* objDer = static_cast<Derived*>(objBase);  // ok!

// class Unrelated 与 Base 并不相关

Unrelated* notRelated = static_cast<Unrelated*>(objBase); // Error

// 由于类型不相关，不允许此类转换
```

### 注意事项

将 `Derived*` 转换为 `Base*` 称为“向上转型”（upcasting），可以在不需要任何显式转换符的情况下完成：

点击查看代码图像

```cpp
Derived objDerived;

Base* objBase = &objDerived; // ok!
```

将 `Base*` 转换为 `Derived*` 称为“向下转型”（downcasting），在不使用显式转换符的情况下无法完成：

点击查看代码图像

```cpp
Derived objDerived;

Base* objBase = &objDerived; // Upcast -> ok!

Derived* objDer = objBase; // Error: Downcast 需要显式转换
```

然而，请注意 `static_cast` 仅验证指针类型是否是相关的。它不会执行任何运行时检查。因此，使用 `static_cast` 时程序员仍然可能写下这种错误：

点击查看代码图像

```cpp
Base* objBase = new Base();

Derived* objDer = static_cast<Derived*>(objBase); // 仍然没有！
```

在这里，`objDer` 实际上指向一个部分的 `Derived` 对象，因为被指向的对象实际上是 `Base()` 类型。由于 `static_cast` 仅执行验证相关类型是否相关的编译时检查，而不执行运行时检查，调用 `objDer->DerivedFunction()` 将通过编译，但在运行时可能会导致意料之外的行为。

除了有助于向上转型或向下转型外，在许多情况下，`static_cast` 可以帮助将隐式转换变为显式转换，并引起程序员或读者的注意：

点击查看代码图像

```cpp
double Pi = 3.14159265;

int num = static_cast<int>(Pi); // 将原本隐式的转换变为显式转换
```

在前面的代码中，`num = Pi` 同样可以正常工作且效果相同。然而，使用 `static_cast` 会让读者注意这种转换的本质，并向（对了解 `static_cast` 的人）表明编译器已经根据编译时可用信息进行了必要的调整，以执行所需的类型转换。当使用用 `explicit` 关键字声明的转换操作符或构造函数时，你也需要使用 `static_cast`。通过 `explicit` 关键字避免隐式转换将在第 9 节 “类与对象(#ch09.html_ch09)”和第 12 节 “操作符类型与运算符重载(#ch12.html_ch12)”中讨论。

### 使用 `dynamic_cast` 和运行时类型识别

动态转换（Dynamic casting）顾如其名，是静态转换的相反，并且实际上是在运行时执行转换——即在应用程序执行期间。`dynamic_cast` 操作的结果可以检查以判断转换尝试是否成功。`dynamic_cast` 操作符的典型用法语法为：

点击查看代码图像

```cpp
destination_type* Dest = dynamic_cast<class_type*>(Source);

if(Dest)    // 检查转换操作是否成功
    Dest->CallFunc ();
```

例如：

点击查看代码图像

```cpp
Base* objBase = new Derived();

// 执行向下转型

Derived* objDer = dynamic_cast<Derived*>(objBase);

if(objDer)    // 检查转换是否成功
    objDer->CallDerivedFunction ();
```

如前面的短示例所示，给定一个指向基类对象的指针，程序员可以求助于 `dynamic_cast` 在继续使用该指针之前验证所指向的目标对象的类型。请注意，在代码段中显而易见目标对象是 `Derived` 类型。因此，该示例仅具有演示价值。然而，情况并非总是如此——例如，当类型为 `Derived*` 的指针传递给接受 `Base*` 类型的函数时。函数在给定基类指针类型的情况下，可以使用 `dynamic_cast` 来检测类型，然后对该类型执行操作。因此，`dynamic_cast` 帮助在运行时检测类型并对类型执行操作。参见列表 13.1，确定 `Fish*` 是 `Tuna*` 还是 `Carp*`。这种这种在运行时识别对象类型的机制被称为运行时类型识别（RTTI）。

### 注意事项

因此，这种在运行时识别对象类型的机制被称为运行时类型识别（RTTI）。

此示例使用了一个层次结构，其中 `Tuna` 和 `Carp` 类继承自 `Fish`。为了方便解释，这两个派生类不仅实现了虚函数 `Swim()`，而且它们各自包含一个特定于其种类型的函数，即 `Tuna::BecomeDinner()` 和 `Carp::Talk()`。此示例的特殊之处在于，给定一个基类 `Fish*` 实例，你能够动态地检测该指针指向的是 `Tuna` 还是 `Carp`。这种动态检测或运行时类型识别发生在第 43-61 行定义的 `DetectFishType()` 函数中。在第 45 行中，使用 `dynamic_cast` 来测试类型为 `Fish*` 的输入基类指针是否为 `Tuna*` 类型。如果该 `Fish*` 指向一个 `Tuna`，则操作符返回一个有效地址，否则返回 `NULL`。因此，`dynamic_cast` 的结果始终需要检查有效性。在第 46 行的检查成功后，你就知道指针 `objTuna` 指向一个有效的 `Tuna`，并可以使用它来调用函数 `Tuna::BecomeDinner()`，如第 49 行所示。对于 `Carp`，你使用该指针调用函数 `Carp::Talk()`，如第 56 行所示。在返回之前，`DetectFishType()` 通过调用 `Fish::Swim()` 对类型进行验证，由于该函数是虚函数，它会将调用重定向到 `Tuna` 或 `Carp` 中实现的 `Swim()` 方法（视情况而定）。

### 注意

`dynamic_cast` 操作的返回值始终应该检查有效性。当转换失败，它为 `NULL`。

### 使用 `reinterpret_cast`

`reinterpret_cast` 是 C++ 转换运算符中最接近 C 风格转换的。它确实允许程序员将一个对象类型转换为另一种类型，无论这些类型是否相关；也就是说，它强制使用示例所示的语法重新解释类型：

点击此处查看代码

```cpp
Base* objBase = new Base ();

Unrelated* notRelated = reinterpret_cast<Unrelated*>(objBase);

// 以上代码可以编译，但不是良好的编程习惯！
```

这种转换实际上强制编译器接受 `static_cast` 通常不会允许的情况。它在某些低级应用中（例如驱动程序）被发现有用，其中数据需要转换为 API（应用程序接口）可以接受的简单类型（例如，某些操作系统级 API 要求数据以字节数组的形式发送，即 `unsigned char*`）：

点击此处查看代码

```cpp
SomeClass* object = new SomeClass();

// 需要将对象作为字节流发送...

unsigned char* bytesFoAPI = reinterpret_cast<unsigned char*>(object);
```

前述代码中转换没有改变源对象的二进制表示，并实际上“欺骗”了编译器，允许程序员查看类型为 `SomeClass` 的对象所包含的单个字节。由于没有其他 C++ 转换运算符允许这种会损害类型安全性的转换，`reinterpret_cast` 是执行这种原本不安全（且不可移植）的转换的最后手段。

### 注意

尽可能，你应该避免在应用程序中使用 `reinterpret_cast`，因为它允许你指示编译器将类型 X 视为一个不相关的类型 Y，这看起来并不是良好的设计或实现。

### 使用 `const_cast`

`const_cast` 允许你关闭对象的 `const` 访问修符。如果你在想为什么这种转换是必要的，那么你的想法可能是正确的。在程序员正确编写类的理想情况下，他们会记住经常地在正确的地方使用 `const` 关键字。遗憾的是，现实世界要不同得是，像如下的代码随处可见：

点击此处查看代码

```cpp
class SomeClass
{
public:
    // ...
    void DisplayMembers(); //问题 - 显示函数不是 const
};
```

所以，当你编写这样一个函数时：

点击此处查看代码

```cpp
void DisplayAllData (const SomeClass& object)
{
    object.DisplayMembers ();  // 编译失败
    // 原因：使用 const 引用调用非 const 成员
}
```

你将 `object` 作为 const 引用传递显然是正确的。毕竟，显示函数应该是只读的，不应该允许调用非 const 成员函数——也就是说，不应该允许调用可以改变对象状态的函数。然而，`DisplayMembers()` 的实现本也应该是 `const` 的，遗憾的是并不是。现在，只要 `SomeClass` 属于你且源代码由你控制，你就可以对 `DisplayMembers()` 进行修正更改。但在许多情况下，它可能属于第三方库，无法对其进行更改。在这些情况下，`const_cast` 就是你的救星。

在这样的场景下，调用 `DisplayMembers()` 的语法为：

点击此处查看代码

```cpp
void DisplayAllData (const SomeClass& object)
{
    const_cast<SomeClass&>(object).DisplayMembers();
}
```

请记住，将 `Base*` 直接强制转换为 `Derived*` 被称为下转型（downcasting），除非你使用 `dynamic_cast` 并检查是否成功，否则这样做是不安全的。

请记住，创建继承层次结构通常是为了拥有虚函数，这样当使用基类指针调用时，可以确保调用的是相应的派生类版本。

### 不要

不要忘记在运行 `dynamic_cast` 后检查指针的有效性。

不要基于 `dynamic_cast` 及其 RTTI（运行时类型识别）来设计你的应用程序。

### 总结

在本节中，你学习了不同的 C++ 强制转换运算符，以及使用它们的优缺点。你还学到，通常情况下你应该避免使用强制转换。

### 问答

**Q: 通过 `const_cast` 将指针或引用转换为非 const 来修改 `const` 对象的内容可以吗？**

**A**: 绝对不可以。这种操作的结果是未定义的，而且绝对不是预期的。

**Q: 我需要一个 `Bird*`，但手里有一个 `Dog*`。编译器不允许我将 `Dog` 对象的指针用作 `Bird*`。然而，当我使用 `reinterpret_cast` 将 `Dog*` 强制转换为 `Bird*` 时，编译器并没有报错，我似乎可以使用这个指针来调用 `Bird` 的成员函数 `Fly()`。这样可以吗？**

**A**: 再次，绝对不可以。`reinterpret_cast` 只改变了指针的解释方式，并没有改变它所指向的对象（那仍然是一个 `Dog`）。在 `Dog` 对象上调用 `Fly()` 函数不会得到你想要的结果，并可能导致应用程序崩溃。

**Q: 我有一个 `Derived` 对象，它被类型为 `Base*` 的 `objBase` 指向。我确定 `objBase` 指向的是一个 `Derived` 对象，那么我真的需要使用 `dynamic_cast` 吗？**

**A**: 既然你确定所指向的对象是 `Derived` 类型，你可以使用 `static_cast` 来节省运行时性能。

**Q: C++ 提供了强制转换运算符，但我被建议尽可能少使用它们。这是为什么呢？**

**A**: 你在家里备着阿斯匹林，但你不会因为有药吃就把它当作主食，对吧？只有在需要的时候才使用强制转换。

## 节工作坊

工作坊包含测验题，帮助你巩固对所涵盖内容的理解，并提供练习让你应用所学知识的机会。在检查附录 E 中的答案之前，尝试回答测验题，并在进入下一节之前确保你理解了答案。

### 测验题

**1.** 你有一个基类对象指针 `objBase`。你会使用哪种强制转换来判断它是 `Derived1` 类型还是 `Derived2` 类型？

**2.** 你有一个指向对象的 `const` 引用，并尝试调用一个你编写的公共成员函数。编译器不允许这样做，因为该函数不是 `const` 成员。你会修正该函数，还是使用 `const_cast`？

**3.** `reinterpret_cast` 应该只在 `static_cast` 不起作用且确定需要且安全的强制转换时使用。正确还是错误？

**4.** true：许多基于 `static_cast` 的转换实例（尤其是简单数据类型之间的转换）会由良好的 C++ 编译器自动完成吗？

### 练习题

**1. 漏洞终结者：**以下代码中的问题是什么？

点击此处查看代码图片

```cpp
void DoSomething(Base* objBase)
{
    Derived* objDer = dynamic_cast <Derived*>(objBase);
    objDer->DerivedClassMethod();
}
```

**2.** 你有一个指针 `objFish*`，它指向 `Tuna` 类的对象。

点击此处查看代码图片

```cpp
Fish* objFish = new Tuna;
Tuna* pTuna = <什么强制转换?>objFish;
```

你会使用哪种强制转换来获取一个指向此 `Tuna` 类型对象的 `Tuna*` 指针？请用代码演示。

## 第 14 节 宏与模板简介

到现在，你应该对基础 C++ 语法有了固定的理解。用 C++ 编写的程序应该是易理解的，你已经准备好学习帮助你高效编写应用程序的语言特征。

在本节中，你将学习：

- ![Image](img/square.jpg) 预处理器简介
- ![Image](img/square.jpg) `#define` 关键字和宏
- ![Image](img/square.jpg) 模板简介
- ![Image](img/square.jpg) 如何编写模板函数和类
- ![Image](img/square.jpg) 宏与模板的区别
- ![Image](img/square.jpg) 如何使用 C++11 引入的 `static_assert` 进行检查

## 预处理器编译器

到现在，你应该对基础 C++ 语法有了固定的理解。用 C++ 编写的程序应该是易理解的，你已经准备好学习帮助你高效编写应用程序的语言特征。

预处理器正如其名，是在编译器开始之前运行的。预处理器指令的特征是它们都以 `#` 开头。例如：

```cpp
#include <iostream>
```

预处理器主要关注代码中的两种预处理器指令：一种使用 `#define` 定义常量，另一种使用 `#define` 定义函数。无论这些指令扮演什么角色，它们都告诉预处理器替换标识符。

### 注意

宏也是关于文本替换。预处理器除了原地替换标识符之外不做任何事情。

### 使用 `#define` 定义常量

使用 `#define` 定义量的语法非常简单：

`#define 标识符 值`

例如，替换为 25 的常量 `ARRAY_LENGTH` 如下：

```cpp
#define ARRAY_LENGTH 25
```

每当预处理器遇到文本 `ARRAY_LENGTH` 时，该标识符现在会被替换为 25：



```cpp
int numbers [ARRAY_LENGTH] = {0};
```

预处理器运行后，这三个对编译器可见的内容：

```cpp
int numbers [25] = {0};
double radiuses [25] = {0.0};
std::string names [25];
```

替换适用于代码的每个部分，包括这样的 `for` 循环：

```cpp
for(int index = 0; index < ARRAY_LENGTH; ++index)
    numbers[index] = index;
```

这个 `for` 循环对编译器可见的内容：

```cpp
for(int index = 0; index < 25; ++index)
    numbers[index] = index;
```

要确切了解这样一个宏是如何工作的，请查看 列表 14.1。

```cpp
14:    cout << "Enter a radius: ";
15:    MY_DOUBLE radius = 0;
16:    cin >> radius;
17:    cout << "Area is: " << PI * radius * radius << endl;
19:    string favoriteWhisky (FAV_WHISKY);
20:    cout << "My favorite drink is: " << FAV_WHISKY << endl;
22:    return 0;
23: }
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图像

Array’s length: 25

Enter a radius: 2.1569

Area is: 14.7154

My favorite drink is: Jack Daniels

## 分析 ![Image](img/arrow.jpg)

`ARRAY_LENGTH`, `PI`， `MY_DOUBLE` 和 `FAV_WHISKY` 分别是第 4 到第 7 行定义的四个宏常量。如你所见，`ARRAY_LENGTH` 用于第 11 行定义数组的长度，这通过第 12 行使用运算符 `sizeof()` 得到了间接确认。`MY_DOUBLE` 用于在第 15 行声明一个类型为 `double` 的变量 `radius`，而 `PI` 用于在第 17 行计算圆面积。最后，`FAV_WHISKY` 用于第 19 行初始化一个 `std::string` 对象，并直接用于第 20 行的 `cout` 语句。所有这些实例展示了预处理器是如何简单地进行文本替换的。

这种“愚笨”的文本替换似乎在 列表 14.1 中找到了无处不在的应用，但它也有缺点。

### 提示

由于预处理器进行的是愚笨文本替换，它并不检查替换的正确性（但编译器总是会检查）。你可以像这样在 列表 14.1 的第 7 行中定义 `FAV_WHISKY`：

点击此处查看代码图像

```cpp
#define FAV_WHISKY 42 // "Jack Daniels"
```

这会导致第 19 行的 `std::string` 实例化出现编译错误，但在没有它的情况下，编译器将继续并打印以下内容：

My favorite drink is: 42

这显然是不合逻辑的，而且重要的是它在未被察觉的情况下就通过了。此外，你对宏定义的常量 `PI` 没有太大的控制权：它是 `double` 还是 `float`？答案是两者都不是。对于预处理器来说，`PI` 只是一个文本替换元素“3.1416”。它从未是一个被定义过的数据类型。

常量使用 `const` 关键字配合数据类型定义会更好。因此，这样好得多：

点击此处查看代码图像

```cpp
const int ARRAY_LENGTH = 25;
const double PI = 3.1416;
const char* FAV_WHISKY = "Jack Daniels";
typedef double MY_DOUBLE; // typedef 为类型创建别名
```

### 使用宏防止多次包含

C++ 程序员通常在名为头文件（header files）的 .H 文件声明类和函数。相应的函数定义在 .CPP 文件中，这些文件通过 `#include<header>` 预处理器指令包含头文件。如果一个头文件——我们称其为 `class1.h`——声明了一个类，该类将另一个在 `class2.h` 中声明的类作为成员，那么 `class1.h` 需要包含 `class2.h`。如果设计很复杂，且另一个类也需要前者，那么 `class2.h` 也会包含 `class1.h`！

然而对于预处理器来说，两个相互包含的头文件是一个具有递归性质的问题。为了避免这个问题，你可以结合预处理器指令 `#ifndef` 和 `#endif` 使用宏。

包含 `<header2.h>` 的 `header1.h` 如下所示：

点击此处查看代码图像

```cpp
#ifndef HEADER1_H_ // 多重包含保护符（multiple inclusion guard）:
#define HEADER1_H_ // 预处理器只会读取此行及后续行
#include <header2.h>
class Class1
{
   // 类成员
};
#endif  // header1.h 的结束
```

`header2.h` 类似类似，但使用了不同的宏定义并包含了 `<header1.h>`：

点击此处查看代码图像

```cpp
#ifndef HEADER2_H_// 多重包含保护符
#define HEADER2_H_
#include <header1.h>
class Class2
{
   // 类成员
};
#endif // header2.h 的结束
```

### 注意

`#ifndef` 可以被读为“如果未定义”（if-not-defined）。这是一种条件处理，指示预处理器只有在标识符未定义时才继续。`#endif` 标记了这种条件处理的结束。

因此，当预处理器第一次运行进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。由此，当预处理器进入 `header1.h` 并遇到 `#ifndef` 时，它注意到宏 `HEADER1_H_` 尚未定义并继续执行。

（注：此处原文逻辑出现了重复，翻译时已根据要求处理，确保不重复输出）

`header1.h` 的结束。`header2.h` 的结束。



预处理器。`header1.h`结束。

## 可以提高性能的性能

**LISTING 14.2 Macro Functions That Calculate the Square of a Number, Area of a Circle, and Min of Two Numbers**

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <string>
2: using namespace std;

3:
4: #define SQUARE(x) ((x) * (x))
5: #define PI 3.1416
6: #define AREA_CIRCLE(r) (PI)*(r))
7: #define MAX(a, b) ((a) > (b)) ? (a) : (b)
8: #define MIN(a, b) ((a) < (b)) ? (a) : (b)

9:
10: int main()
11: {
12:    cout << "Enter an integer: ";
13:    int num = 0;
14:    cin >> num;

15:
16:    cout << "SQUARE(" << num << ") = " << SQUARE(num) << endl;
17:    cout << "Area of a circle with radius " << num << " is: ";
18:    cout << AREA_CIRCLE(num) << endl;

19:
20:    cout << "Enter another integer: ";
21:    int num2 = 0;
22:    cin >> num2;

23:
24:    cout << "MIN(" << num << ", " << num2 << ") = " << MIN(num, num2) << endl;
25:    cout << "MAX(" << num << ", " << num2 << ") = " << MAX(num, num2) << endl;

26:
27:    return 0;
28: }
```

输出：

![Image](img/arrow.jpg)

点击此处查看代码图像

```text
Enter an integer: 36
SQUARE(36) = 1296
Area of a circle with radius 36 is: 4071.51
Enter another integer: -101
MIN(36, -101) = -101
MAX(36, -101) = 36
```

请注意，宏对类型敏感，因此宏函数可能会导致问题。例如，`AREA_CIRCLE`理想情况下应该返回`double`的函数，这样你就能确定计算出的面积的返回值解析，并确保它与输入半径的性质无关。

***

#### 为什么需要这么多括号？

再次看一眼计算圆面积的宏：

```cpp
#define AREA_CIRCLE(r) (PI*(r)*(r))
```

这个计算在使用的括号数量上语法非常奇怪。相比之下，请参考第 7 Lesson“用函数组织代码”中列表 7.1 里的`Area()`函数。

```cpp
// 函数定义（实现）
double Area(double radius)
{
    return Pi * radius * radius;  // 看，没有括号？
}
```

那么，为什么你在宏中使用了过多的括号，而函数中相同的公式看起来大不相同？原因在于宏的评估方式——它是作为由预处理器支持的文本替换机制。

考虑去掉了大部分括号的宏：

```cpp
#define AREA_CIRCLE(r) (PI*r*r)
```

当你使用如下语句调用此宏时，会发生什么：

```cpp
cout << AREA_CIRCLE (4+6);
```

这会被编译器展开为：

```cpp
cout << (PI*4+6*4+6); // 与 PI*10*10 不等
```

因此，根据运算符优先级的规则（乘法在加法之前），编译器实际上这样评估面积的：

```cpp
cout << (PI*4+24+6);  // 42.5664（这是错误的）
```

在没有括号的情况下，纯文本转换破坏了我们的编程逻辑！括号有助于避免这个问题：

```cpp
#define AREA_CIRCLE(r) (PI*(r)*(r))

cout << AREA_CIRCLE (4+6);
```

替换后的表达式被编译器视为：

```cpp
cout << (PI*(4+6)*(4+6)); // PI*10*10，如预期的那样
```

这些括号会自动导致准确面积的计算，使得你的宏代码独立于运算符优先级及其影响。

### 使用宏`assert`验证表达式

虽然在编程后立即测试每个代码路径是好的，但对于非常大的应用程序，这在物理上可能是可能的。然而，可以检查有效的表达式或变量值。

`assert`宏允许你执行此操作。使用`assert`时需要包含`<assert.h>`，语法如下：

```cpp
assert (求值为真或否的表达式);
```



使用`assert()`验证指针内容的示例是：

```cpp
#include <assert.h>

int main()
{
    char* sayHello = new char [25];
    assert(sayHello != NULL); // 如果指针为 NULL，则抛出消息
    // 其他代码
    delete [] sayHello;
    return 0;
}
```

`assert()`确保了你在指针无效时收到通知。为了演示起见，我将`sayHello`初始化为`NULL`，在调试模式下执行时，Visual Studio 立即弹出了你在图 14.1 中看到的屏幕。

![Image](img/14fig01.jpg)

**图 14.1** 当检查指针有效性的`assert`失败时发生。

因此，在 Microsoft Visual Studio 中实现的`assert()`允许你点击“重试”（Retry）按钮返回应用程序，并且调用堆栈会指示哪一行失败了断言测试。这使得`assert()`成为一个方便的调试功能；例如，你可以使用`assert`验证函数的输入参数。这是非常推荐的，并有助于你从长期来看提高代码质量。

### 注意

`assert()`通常在发布（release）模式下被禁用，并且仅在大多数开发环境的调试（debug）构建中为你提供错误消息或信息。

此外，某些环境将其实现为函数而不是宏。

### 警告

由于`assert`不会进入发布版本，因此确保对程序运行至关重要的检查仍然被执行是重要的。

### 使用宏函数的优缺点

宏允许你不分类型地重用某些函数。考虑来自列表 14.2 的以下行代码：

```cpp
#define MIN(a, b) (((a) < (b)) ? (a) : (b
```

你可以在整数上使用此宏：

```cpp
cout << MIN(25, 10) << endl;
```

但你也可以在`double`上重用它：

```cpp
cout << MIN(0.1, 0.2) << endl;
```

请注意，如果`MIN()`是一个普通函数，你将编写它的两个变体：接受`int`并返回`int`的`MIN_INT()`，以及对`double`类型执行相同操作的`MIN_DOUBLE()`。这种减少代码行数的优化是一个微小的优势，并诱导了一些程序员使用宏。这些宏在编译之前被展开，因此简单宏的性能优于普通函数调用。这是因为函数调用需要创建调用堆栈、传递参数等——这些管理开销往往超过了计算本身。

然而，宏不支持任何形式类型安全，这是一个很大的缺点。此外，调试复杂的宏也不容易。

如果你需要编写类型无关但类型安全的泛型函数，你应该编写模板（template）而不是宏。这些将在下一节中解释。如果你需要提升性能，你可以调用该函数为`inline`。

你已经已经在列表 7.10 中介绍了使用`inline`关键字编程内联函数。

**1:** 放置在墙内横梁下方的短段或块，用于分配其重量或压力（如门上方）

**2:** (1): 量规、图案或模具（如薄板或板），用作所制部件形状的引导 (2): 一种分子（如 DNA），作为生成另一个大大分子（如信使 RNA）的模式 b: 叠加层

**3:** 建立或用作模式的某物

最后一种定义可能接近 C++ 术语中`template`（模板）一词的解释。C++ 中的模板允许你定义一种可以应用于不同类型对象的行为。这听起来与宏允许你所做的事情非常相似（参考用于确定两个数字中较大值的简单宏`MAX`），唯一的区别在于，宏是不类型安全的，而模板是类型安全的。

### 模板声明语法

你通过使用`template`关键字后跟一个类型参数列表来开始模板的声明。该声明的格式如下：

```cpp
template <parameter list>
template function / class declaration..
```

`template`关键字标记了模板声明的开始，后面跟着模板参数列表。该参数列表包含`typename`关键字，它定义了模板参数`objType`，使其成为模板实例化时对象`type`的占位符。

```cpp
template <typename T1, typename T2 = T1>
bool TemplateFunction(const T1& param1, const T2& param2);

// 一个模板类
template <typename T1, typename T2 = T1>
class MyTemplate
{
private:
   T1 member1;
   T2 member2;
public:
   T1 GetObj1() {return member1; }
   // ... 其他成员
};
```

你看到的是一个模板函数和一个模板类，它们都分别接受两个模板参数`T1`和`T2`，其中`T2`已经被给定的默认类型为`T1`的类型。

### 模板声明的不同类型

模板声明可以是：

- ![Image](img/square.jpg) 函数的声明或定义
- ![Image](img/square.jpg) 类的声明或定义
- ![Image](img/square.jpg) 模板类中成员函数或成员类的定义
- ![Image](img/square.jpg) 模板类静态数据成员的定义
- ![Image](img/square.jpg) 嵌套在模板类中的类的静态数据成员的定义
- ![Image](img/square.jpg) 类或模板类成员模板的定义

### 模板函数

想象有一个函数可以调整自己适应不同类型的参数。使用模板语法就可以这种函数！让我们分析一个示例模板声明，它等同于之前讨论过的用于返回两个提供的参数中较大值的宏`MAX`：

```cpp
template <typename objType>
const objType& GetMax(const objType& value1, const objType& value2)
{
    if (value1 > value2)
        return value1;
    else
        return value2;
}
```

示例用法：

```cpp
int num1 = 25;
int num2 = 40;
int maxVal = GetMax <int> (num1, num2);

double double1 = 1.1;
double double2 = 1.001;
double maxVal = GetMax <double>(double1, double2);
```

注意在调用`GetMax`时使用的`<int>`细节。它实际上将模板参数`objType`定义为`int`。之前的代码会导致编译器生成模板函数`GetMax`的两个版本，这些版本可以可视化为如下所示：

```cpp
const int& GetMax(const int& value1, const int& value2)
{
    //...
}

const double& GetMax(const double& value1, const double& value2)
{
    // ...
}
```

然而，实际上，模板函数并不一定需要附带类型指定符。因此，以下函数调用工作得完全完美：

```cpp
int maxVal = GetMax(num1, num2);
```

在这种情况下，编译器足够智能，可以理解模板函数是为整数类型调用的。然而对于模板类，你需要显式地指定类型，如 列表 14.3 所示。

**列表 14.3** 模板函数`GetMax`帮助评估两个提供的值中的较大值

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename Type>
const Type& GetMax(const Type& value1, const Type& value2)
{
    if (value1 > value2)
        return value1;
    else
        return value2;
}

template <typename Type>
void DisplayComparison(const Type& value1, const Type& value2)
{
    cout << "GetMax(" << value1 << ", " << value2 << ") = ";
    cout << GetMax(value1, value2) << endl;
}

int main() {
    int num1 = 25;
    int num2 = 40;
    DisplayComparison(num1, num2);

    double d1 = 1.1;
    double d2 = 1.001;
    DisplayComparison(d1, d2);

    string name1("Jack"), name2("John");
    DisplayComparison(name1, name2);

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

```cpp
GetMax(101, 2011) = 2011
GetMax(3.14, 3.1416) = 3.14
GetMax(Jack, John) = John
```

此示例包含两个模板函数：第 4 行到 11 行的`GetMax()`，它被第 13 行到 18 行的`DisplayComparison()`调用。`main()`函数在第 23 行、26 行和 29 行展示了同一个模板函数如何被重用于非常不同的数据类型：`integer`、`double`和`string`。这些模板函数不仅可以重用（就像它们的宏对应一样），而且更容易编程和维护，并且是类型安全的！

注意你也可以用显式类型调用`DisplayComparison`：

```cpp
DisplayComparison<int>(num1, num2);
```

然而，在调用模板函数时这样做是不必要的。你不需要指定模板参数类型，因为编译器可以自动推断。然而，在编写模板类时，你需要这样做。

[第 9 节] “[类与对象]”教过你类是编程单元，它们封装了某些属性以及操作这些属性的方法。属性通常是私有成员，例如`class Human`中的`int Age`。类是设计蓝图，而一个类在现实世界中的表示就是该类的对象。因此，“Tom”可以被看作`class Human`的一个对象，其属性`Age`的值为 15。显然，我们指的是年份。如果由于你应用程序特有的原因，要求将年龄存储为自出生以来的秒数，那么`int`可能就不够了。为了稳妥起见，你可能想使用`long long`。这就是模板类（template classes）大显身用场的地方。模板类是 C++ 类的模板化版本。它们是“蓝图的蓝图”。在使用模板类时，你可以选择指定你为该类特化的“类型”。这使你能够创建某些模板参数`Age`为`long long`的类，另一些为`int`的类，还有一些`Age`为`short`类型整数的类。

一个使用单个参数`T`来持有成员变量的简单模板类可以写如下：

```cpp
template <typename T>
class HoldVarTypeT
{
private:
   T value;
public:
   void SetValue (const T& newValue) { value = newValue; }
   T& GetValue() {return value;}
};
```

变量`value`的类型是`T`，它是在模板被使用时分配的，即*实例化*（instantiated）时。现在让我们来看看这个模板类的示例用法：

```cpp
HoldVarTypeT <int> holdInt; // 对 int 的模板实例化
holdInt.SetValue(5);
cout << "The value stored is: " << holdInt.GetValue() << endl;
```

你使用了这个模板类来持有和检索`int`类型的对象；也就是说，`Template`类是针对`int`类型的模板参数进行了实例化。同样，你可以使用同一个类以类似的方式处理字符字符串：

```cpp
HoldVarTypeT <char*> holdStr;
holdStr.SetValue("Sample string");
cout << "The value stored is: " << holdStr.GetValue() << endl;
```

因此，模板类定义了一种类模式，并帮助在模板可能实例化的不同数据类型上实现该模式。

**提示**

模板类可以使用除`int`等简单类型或标准库提供的类以外的类型进行实例化。你可以使用自己定义的类来实例化模板。例如，当你将定义模板类`HoldVarTypeT`的代码添加到 第 9 节 中的 列表 9.1 中时，你将通过在`main()`后面添加以下代码为`class Human`实例化模板：

```cpp
HoldVarTypeT<Human> holdHuman;
holdHuman.SetValue(firstMan);
holdHuman.GetValue().IntroduceSelf();
```

### 使用多个参数声明模板

模板参数列表可以扩展，以声明多个用逗号隔开的参数。因此，如果你想声明一个泛型类来持有一对类型可能不同的对象，你可以使用如下示例所示的结构来实现（该示例显示了一个带有两个模板参数的模板类）：

```cpp
template <typename T1, typename T2>
class HoldsPair
{
private:
    T1 value1;
    T2 value2;
public:
    // 初始化成员变量的构造函数
   HoldsPair (const T1& val1, const T2& val2)
   {
       value1 = val1;
       value2 = val2;
   };
   // ... 其他成员函数
};
```

在这个例中，`class HoldsPair`接受两个命名为`T1`和`T2`的模板参数。正如你看到的，我们可以使用这个类来持有两个相同类型或不同类型的对象：

```cpp
// 将 int 和 double 配对的模板实例化
HoldsPair <int, double> pairIntDouble (6, 1.99);

// 将 int 和 int 配对的模板实例化
HoldsPair <int, int> pairIntDouble (6, 500);
```

### 使用默认参数声明模板

我们可以修改之前的`HoldsPair <...>`版本，将`int`声明为默认模板参数。

```cpp
template <typename T1=int, typename T2=int>
class HoldsPair
{
 // ... 方法声明
};
```

这在构造上与定义默认参数值的函数相似，不同之处在于在这种情况下我们定义的是类型。`HoldsPair`的第二次用法因此可以简化为：

```cpp
// 默认类型：int 与 int
HoldsPair <> (6, 500);
```

### 模板`HoldsPair`

现在是时候进一步开发目前为止的`HoldsPair`版本了。看看 列表 14.4。

**列表 14.4** 具有成员属性对的模板类

```cpp
#include <iostream>
using namespace std;

// 默认参数：int & double
template <typename T1=int, typename T2=double>
class HoldsPair
{
private:
    T1 value1;
    T2 value2;
public:
    HoldsPair(const T1& val1, const T2& val2) // 构造函数
    : value1(val1), value2(val2) {}

    // 访问函数
    const T1 & GetFirstValue () const
    {
        return value1;
    }

    const T2& GetSecondValue () const
    {
        return value2;
    }
};

int main ()
{
    HoldsPair<> pairIntDouble (300, 10.99);
    HoldsPair<short,const char*>pairShortStr(25,"Learn templates, C++");
```



`cout << "The first object contains -" << endl;`

`cout << "Value 1: " << pairIntDouble.GetFirstValue() << endl;`

`cout << "Value 2: " << pairIntDouble.GetSecondValue() << endl;`

`cout << "The second object contains -" << endl;`

`cout << "Value 1: " << pairShortStr.GetFirstValue() << endl;`

`cout << "Value 2: " << pairShortStr.GetSecondValue() << endl;`

`return 0;`

```

***

**输出** ![Image](img/arrow.jpg)

点击此处查看代码图片

```

The first object contains -

Value 1: 300

Value 2: 10.99

The second object contains -

Value 1: 25

Value 2: Learn templates, C++

```

**分析** ![Image](img/arrow.jpg)

这个简单的程序演示了如何声明模板类 `HoldsPair` 以持有一对类型取决于模板参数列表的值。第一行包含一个模板参数列表，定义了两个模板参数 `T1` 和 `T2`，默认类型分别为 `int` 和 `double`。访问函数 `GetFirstValue()` 和 `GetSecondValue()` 可用于查询对象持有的值。注意 `GetFirstValue` 和 `GetSecondValue` 如何根据模板实例化语法进行调整以返回适当的对象类型。你成功地在 `HoldsPair` 中定义了一种模式，可以利用该模式为不同的变量类型交付相同的逻辑。因此，模板增加了代码的复用性。

模板类是类的蓝图，因此在它以某种形式被使用之前，它在编译器中并不真正存在。也就是说，就编译器而言，你定义了但没有使用的模板类仅仅是被直接忽略的代码。然而，一旦你通过像下面这样提供模板参数来*实例化*（instantiate）一个模板类，例如 `HoldsPair`：

点击此处查看代码图片

```

HoldsPair<int, double> pairIntDbl;

```

你正在指示编译器使用该模板为你创建一个类，并根据指定的为模板参数的类型（在本例中为 `int` 和 `double`）对其进行实例化。因此，在模板的情况下，*实例化*是指使用一个或多个模板参数创建特定类型的行为或过程。

另一方面，可能存在某些情况，要求你在模板被用特定类型实例化时，显式地定义模板的（不同的）行为。这就是为该类型对模板（或其行为）进行特化（specialize）的地方。当模板类 `HoldsPair` 在两个模板参数均为 `int` 类型时实例化时，其特化版本如下：

点击此处查看代码图片

```cpp

template<> class HoldsPair<int, int>

{

   // 此处为实现代码

};

```

不用而说，特化模板的代码必须遵循模板定义。列表 14.5 是模板特化的示例，展示了特化版本与它所特化的模板之间有多大差异。

**列表 14.5** 展示了模板特化

点击此处查看代码图片

```cpp

0: #include <iostream>

1: using namespace std;

2:

3: template <typename T1 = int, typename T2 = double>

4: class HoldsPair

5: {

6: private:

7:     T1 value1;

8:     T2 value2;

9: public:

10:     HoldsPair(const T1& val1, const T2& val2) // 构造函数

11:         : value1(val1), value2(val2) {}

12:

13:     // 访问函数

14:     const T1 & GetFirstValue() const;

15:     const T2& GetSecondValue() const;

16: };

17:

18: // 此处为 int & int 类型特化 HoldsPair

19: template<> class HoldsPair<int, int>

20: {

21: private:

22:     int value1;

23:     int value2;

24:     string strFun;

25: public:

26:     HoldsPair(const int& val1, const int& val2) // 构造函数

27:         : value1(val1), value2(val2) {}

28:

29:     const int & GetFirstValue() const

30:     {

31:         cout << "Returning integer " << value1 << endl;

32:         return value1;

33:     }

34: };

35:

36: int main()

37: {

38:     HoldsPair<int, int> pairIntInt(222, 333);

39:     pairIntInt.GetFirstValue();

40:

41:     return 0;

42: }

```

输出 ![Image](img/arrow.jpg)
Returning integer 222

分析 ![Image](img/arrow.jpg)

显然，当你将列表 14.4 中 `HoldsPair` 类的行为与此处的进行对比时，你会发现模板的行为显著不同。事实上，`GetFirstValue()` 函数在 `HoldsPair<int,int>` 的模板实例化中被修改过，也能显示输出。仔细观察第 18 到 34 行的特化代码可以发现，该版本在第 24 行声明了一个字符串成员 `strFun`——而该成员在 `HoldsPair<>` 的原始模板定义中是缺失。事实上，原始模板甚至没有为访问函数 `GetFirstValue()` 和 `GetSecondValue()` 提供实现，但程序仍然可以编译。这是因为编译器仅需要考虑 `<int, int>` 的模板实例化——而我们为此提供了一个完整的特化实现。因此，这个示例不仅展示了模板特化，还展示了模板代码如何根据其用法被考虑甚至被忽略。

### 模板类与静态成员

我们学习了模板中的代码在用时何时为编译器存在，何时不存在。那么，模板类中的 `static` 成员函数又是怎样的呢？你在第 9 Lesson 中学习过，将类成员声明为 `static` 会导致成员在类的所有实例之间共享。模板类也是如此，不同在于 `static` 成员是在具有相同实例化的模板类对象之间共享。因此，模板类中的 `static` 成员 `X` 对于为 `int` 实例化的类的所有实例都是静态的。同样，`X` 对于为 `double` 实例化的类的所有实例也是静态的，且独立于 `int` 的其他模板实例化。换句话说，你可以想象为编译器在模板类中创建了两个版本的静态变量：用于 `int` 模板实例化的 `X_int` 和用于 `double` 模板实例化的 `X_double`。列表 14.6 展示了这一点。

**列表 14.6** 静态变量对模板类及实例的影响：点击此处查看代码图片

```cpp

0: #include <iostream>

1: using namespace std;

2:

3: template <typename T>

4: class TestStatic

5: {

6: public:

7:     static int staticVal;

8: };

9:

10: // 静态成员初始化

11: template<typename T> int TestStatic<T>::staticVal;

12:

13: int main()

14: {

15:     TestStatic<int> intInstance;

16:     cout << "Setting staticVal for intInstance to 2011" << endl;

17:     intInstance.staticVal = 2011;

18:

19:     TestStatic<double> dblnstance;

20:     cout << "Setting staticVal for Double_2 to 1011" << endl;

21:     dblnstance.staticVal = 1011;

22:

23:     cout << "intInstance.staticVal = " << intInstance.staticVal << endl;

24:     cout << "dblnstance.staticVal = " << dblnstance.staticVal << endl;

25:

26:     return 0;

27: }

```

输出 ![Image](img/arrow.jpg)
点击此处查看代码图片
Setting staticVal for intInstance to 2011
Setting staticVal for Double_2 to 1011
intInstance.staticVal = 2011
dblnstance.staticVal = 1011

在第 17 行和第 21 行，你分别为 `int` 和 `double` 的实例化设置了 `staticVal`。输出表明编译器在两个静态成员中存储了两个不同的值。因此，编译器确保了特定类型模板实例化时静态变量的行为保持完好。

注意
模板类的静态成员实例化语法不应在列表 14.6 的第 11 行被忽略。

点击此处查看代码图片

```cpp

template<typename T> int TestStatic<T>::staticVal;

```

它遵循以下模式：

点击此处查看代码图片

```cpp

template<template parameters> StaticType

ClassName<Template Arguments>::StaticVarName;

```

### 变量模板，也称为变参模板

假设你想写一个增加两个值的泛型函数。模板函数 `Sum()` 就实现了这一点：

点击此处查看代码图片

```cpp

template <typename T1, typename T2, typename T3>

void Sum(T1& result, T2 num1, T3 num2)

{

    result = num1 + num2;

    return;

}

```

这很简单。但如果你被要求编写一个能够处理任意数量值（每个值作为参数传递）的单一函数，你需要在定义此类函数时使用*变量模板*。变量模板或变参模板自 2014 年发布的 C++14 起就是 C++ 的一部分。列表 14.7 展示了在定义此类函数时使用变量模板的方法。

# 列表 14.7 使用变长模板的函数演示了可变参数

点击此处查看代码图像

* * *

```

0: #include <iostream>

1: using namespace std;

2:

3: template <typename Res, typename ValType>

4: void Sum(Res& result, ValType& val)

5: {

6:     result = result + val;

7: }

8:

9: template <typename Res, typename First, typename... Rest>

10: void Sum(Res& result, First val1, Rest... valN)

11: {

12:     result = result + val1;

13:     return Sum(result, valN ...);

14: }

15:

16: int main()

17: {

18:     double dResult = 0;

19:     Sum (dResult, 3.14, 4.56, 1.1111);

20:     cout << "dResult = " << dResult << endl;

21:

22:     string strResult;

23:     Sum (strResult, "Hello ", "World");

24:     cout << "strResult = " << strResult.c_str() << endl;

25:

26:     return 0;

27: }

```

* * *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

dResult = 8.8111

strResult = Hello World

## 分析 ![Image](img/arrow.jpg)

示例演示了我们使用变长模板定义的 `Sum()` 函数不仅可以处理第 19 行和第 23 行所示的完全不同的参数类型，还能处理数量变化的参数。第 19 行调用的 `Sum()` 使用四个参数，而第 23 行使用三个参数，其中一个是 `std::string`，另外两个是 `const char*`。在编译期间，编译器实际上会为适合该调用的正确 `Sum()` 创建代码，并递归执行，直到所有参数都被处理完毕。

* * *

### 注意

你可能已经注意到前面的代码示例使用了省略号 `...`。C++ 中与模板一起使用的省略号告诉编译器，模板类或函数可以接受任意数量、任意类型的模板参数。

* * *

变长模板是 C++ 的一个强大扩展，适用于数学处理以及某些简单任务的完成。使用变长模板的程序员可以避免实现多个重载版本来执行相同任务的重复工作，创建出更短且更易维护的代码。

* * *

### 注意

C++14 为你提供了一个运算符，可以告诉传递给变长模板调用的模板参数数量。在列表 14.7 中，你可以在可以在 `Sum()` 等函数内部使用该运算符，如下：

点击此处查看代码图像

```

int arrNums[sizeof...(Rest)];

// 数组长度使用 sizeof...() 

// 在编译时进行计算

```

你不能混淆 `sizeof...()` 和 `sizeof(Type)`。后者返回类型的大小，而前者返回发送给变长模板的模板参数个数。

* * *

变长模板的支持也引入了对*元组（tuples）*的标准支持。`std::tuple` 是实现元组的类模板。它可以根据不同数量的成员及其类型进行实例化。可以使用标准库函数 `std::get` 单独访问这些元素。列表 14.8 演示了 `std::tuple` 的实例化和使用。

## 列表 14.8 实例化与使用 `std::tuple`

点击此处查看代码图像

* * *

```

0: #include <iostream>

1: #include <tuple>

2: #include <string>

3: using namespace std;

4:

5: template <typename tupleType>

6: void DisplayTupleInfo(tupleType& tup)

7: {

8:     const int numMembers = tuple_size<tupleType>::value;

9:     cout << "Num elements in tuple: " << numMembers << endl;

10:     cout << "Last element value: " << get<numMembers - 1>(tup) << endl;

11: }

12:

13: int main()

14: {

15:     tuple<int, char, string> tup1(make_tuple(101, 's', "Hello Tuple!"));

16:     DisplayTupleInfo(tup1);

17:

18:     auto tup2(make_tuple(3.14, false));

19:     DisplayTupleInfo(tup2);

20:

21:     auto concatTup(tuple_cat(tup2, tup1)); //  tup2, tup1 的成员

22:     DisplayTupleInfo(concatTup);

23:

24:     double pi;

25:     string sentence;

26:     tie(pi, sentence) = tuple_cat(tup2, tup1);

27:     cout << "Pi: " << pi << endl;

28:

29:     return 0;

30: }



编译器注册的抗议在第 6 行中编写。因此，`static_assert` 是 C++11 帮助你保护模板代码免受意外实例化影响的一种方式。

## 在实际 C++ 编程中使用模板

模板的一个重要且强大的应用是标准模板库（STL）。STL 由一组模板类和函数组成，这些类和函数包含了通用工具类和算法。这些 STL 模板类允许你实现动态数组、列表和键值对容器，而算法（如 `sort`）则作用于这些容器并处理它们所包含的数据。

你之前学到的模板语法知识将极大地帮助你使用在本书后续章节中详细介绍的 STL 容器和函数。对 STL 容器和算法有更深入的理解反过来也能帮助你编写出高效的 C++ 程序，使用 STL 经过测试且可靠的实现，并帮助你避免在样板代码细节上浪费时间。

### 应该做的（DO）

- **务必**使用模板来实现通用概念。
- **务必**优先选择模板而不是宏。

### 不要做的（DON'T）

- **不要**在编写模板函数和类时忘记使用 `const` 正确性原则。
- **不要**忘记模板类中包含的静态成员对于该类的每个类型特化版本都是静态的。

### 总结

在本节中，你学习了更多关于使用预处理器的细节。每当你运行编译器时，预处理器都会首先运行，并翻译诸如 `#define` 之类的指令。

预处理器执行文本替换，尽管在使用宏时这些操作可能会变得相当复杂。宏函数根据编译时传递给宏的参数提供复杂的文本替换。在宏中为每个参数加上括号是非常重要的，以确保发生正确的替换。

模板帮助你编写可重用的代码，为开发者提供了一种可以用于各种数据类型的模式。它们还能够实现对 `macros` 的类型安全替换。掌握了在本节中学到的模板知识后，你现在已经准备好学习使用 STL 了！

### 问答（Q&A）

**问：为什么我应该在头文件中使用包含保护符（inclusion guards）？**

**答** 使用 `#ifndef`、`#define` 和 `#endif` 的包含保护符可以防止头文件出现多次包含或递归包含的错误，在某些情况下它们还能加快编译。

**问：如果某个功能既可以用宏函数也可以用模板实现，我什么时候应该倾向于模板而不是宏？**

**答** 理想情况下，你应该始终优先选择模板，因为模板允许通用且类型安全的实现。宏无法实现类型安全的实现，因此最好避免使用。

**问：在调用模板函数时我需要指定模板参数吗？**

**答** 通常不需要，因为编译器可以根据函数调用中使用的参数为你推断出这一点。

**问：对于给定的模板类，存在多少个静态变量实例？**

**答** 这完全取决于该模板类被实例化的类型数量。因此，如果你的类为 `int`、`string` 和自定义类型 `X` 进行了实例化，你可以预期会有三个静态变量实例——每个模板实例化对应一个。

### 工作坊（Workshop）

工作坊提供了测验题来帮助你巩固对所涵盖内容的理解，并提供了练习题让你获得使用所学知识的。在检查附录 E 中的答案之前，尝试回答测验和练习题，并确保你理解了答案。

### 测验（Quiz）

1. 什么是包含保护符（inclusion guard）？

2. 考虑以下宏：

```cpp
#define SPLIT(x) x / 5
```

如果用 20 调用它，结果是什么？

3. 如果用 `10+10` 调用问题 2 中的 `SPLIT` 宏，结果是什么？

4. 你会如何修改 `SPLIT` 宏以避免错误的结果？

### 练习（Exercises）

1. 写一个用于两个数相乘的宏。

2. 写练习 1 中宏的模板版本。

3. 为 `swap` 实现一个模板函数，用于交换两个变量。

4. **错误修复**：你将如何改进以下用于计算数值四分之一的宏？

```cpp
#define QUARTER(x) (x / 4)
```

5. 写一个简单的模板类，它持有通过类参数定义的数组。该类应具有操作元素的访问函数。

6. 写一个 `Display()` 模板函数，它可以接受不同数量和类型的参数，并显示它们。

# 第三部分：学习标准模板库 (STL)

# 第 15 节：标准模板库简介

简单来说，标准模板库（STL）是一组模板类和函数，它们为程序员提供了：

- 用于存储信息的容器
- 用于访问信息的迭代器
- 用于处理内容的算法

在本节中，你将概述 STL 的这三个支柱。

## STL 容器

*容器*是用于存储数据的 STL 类。STL 提供了两种容器类型：

- 顺序容器
- 关联容器

除了这些，STL 还提供了称为*容器适配器*的类，它们是针对特定目的变体。

### 顺序容器

顾其名，这些是以顺序方式持有数据的容器，例如数组和列表。顺序容器的特点是插入速度快，但 `find` 操作较慢。

STL 顺序容器包括：

- `std::vector`：像动态数组一样在末端增长。将 vector 想象成书架，你可以在一端添加或删除书籍。
- `std::deque`：类似于 `std::vector`，但允许在开头也插入或删除元素。
- `std::list`：像双向链表一样工作。将其想象成链链，对象是链中的一个环。你可以在任何位置添加或删除环（即对象）。
- `std::forward_list`：类似于 `std::list`，但它是单向链表，允许仅向一个方向迭代。

`std::vector` 类类似于数组并允许对元素进行随机访问；即，你可以根据位置（下标）使用下标运算符 (`[]`) 直接访问或操作 vector 中的元素。此外，STL `vector` 是一个动态数组，因此可以调整大小以适应应用程序的运行时需求。为了保持在给定位置时能够随机访问元素的属性，大多数 STL `vector` 实现将所有元素存储在连续的位置。因此，取决于所包含的对象类型，经常需要调整大小的 `vector` 可能会降低应用程序的性能。

你可以将 STL `list` 视为 STL 对普通链表的实现。虽然 `list` 中的元素不能像 STL `vector` 中的元素那样进行随机访问，但 `list` 可以将元素组织在非连续的内存区域中。因此，`std::list` 不存在 `vector` 在需要重新分配其内部数组时会面临的性能问题。STL `list` 类在第 18 节“STL `list` 与 `forward_list`](#ch18.html_ch18)”中进行了详细讨论。

### 关联容器

`关联容器`（Associative containers）是指以排序方式存储数据的容器——类似于字典。这导致了插入时间较慢，但在搜索方面具有显著优势。

STL 提供的关联容器有：

- `std::set`——在具有对数复杂度的容器中，根据插入顺序进行排序并存储唯一值。
- `std::unordered_set`——在具有近常数复杂度的容器中，根据插入顺序排序并存储唯一值。从 C++11 开始可用。
- `std::map`——在具有对数复杂度的容器中，根据其唯一的键排序并存储键值对。
- `std::unordered_map`——在具有近常数复杂度的容器中，根据其唯一的键排序并存储键值对。从 C++11 开始可用。
- `std::multiset`——类似于 `set`。此外，支持存储多个具有相同值的项；也就是说，值不需要是唯一的。
- `std::unordered_multiset`——类似于 `unordered_set`。此外，支持存储多个具有相同值的项；也就是说，值不需要是唯一的。从 C++11 开始可用。
- `std::multimap`——类似于 `map`。此外，支持存储键不需要唯一的键值对。
- `std::unordered_multimap`——类似于 `unordered_map`。此外，支持存储键不需要唯一的键值对。从 C++11 开始可用。

* * *

注意

在此处`复杂度`（Complexity）是指容器性能与其包含的元素数量之间的关系。因此，当我们谈论`常数复杂度`（constant complexity）时（如 `std::unordered_map` 的情况），意味着容器的性能与其包含的元素数量无关。这种容器处理一千个元素的时间与处理百万个元素的时间相同。

`对数复杂度`（Logarithmic complexity）如 `std::map` 所示，表示性能与元素数量的对数成比例。这种容器处理百万个元素的时间将是处理一千个元素的两倍。

`线性复杂度`（Linear complexity）意味着性能与元素数量成正比。这种容器处理百万个元素的速度比处理一千个元素慢一千倍。

对于给定的容器，不同操作的复杂度可能不同。也就是说，元素的插入复杂度可能是常数的，但搜索复杂度可能是线性的。因此，除了了解容器的功能外，了解它在不同操作下的表现也是选择正确容器的关键。

* * *

STL 容器的排序标准可以通过编写谓词函数进行自定义。

* * *

提示

某些 STL 的实现还具有关联容器，如 `hash_set`、`hash_multiset`、`hash_map` 和 `std_multimap`。这些与标准支持的 `unordered_*` 容器类似。在某些场景下，`hash_*` 和 `unordered_*` 变体可能更元素搜索，因为它们提供了常数时间操作（独立容器中的元素数量）。通常，这些容器还提供与其标准版本相同的公共方法，因此同样易用。

使用符合标准的变体将使代码更容易在平台和编译器之间迁移，因此应优先考虑。此外，标准容器性能的对数级下降可能不会显著影响应用程序。

* * *

### 容器适配器

`容器适配器`（Container adapters）是顺序和关联容器的变体，其功能有限，旨在实现特定的目的。主要的适配器类有：

- `std::stack`——以后进先出（LIFO）方式存储元素，允许在顶部插入（push）和弹出（pop）。
- `std::queue`——先进先出（FIFO）方式存储元素，允许按照插入顺序移除第一个元素。
- `std::priority_queue`——按排序顺序存储元素，使得值评估为最高的元素始终位于队列首。

这些容器在第 24 节“适配器容器：栈与队列`](ch24.html_ch24)”中进行了详细讨论。

### STL 迭代器

迭代器最简单的例子是指针。给定一个指向数组第一个元素的指针，你可以对其递增以指向下一个元素，或者在许多情况下，操作该位置的元素。

STL 中的迭代器是模板类，在某些方面是指针的泛化。这些模板类为程序员提供了一个句柄，用于处理 STL 容器并对其进行操作。注意，操作可以是模板函数，而迭代器则是桥梁，允许这些模板函数与模板类形式容器以一致且无缝的方式工作。

STL 提供的迭代器可以大致分类为：

- `输入迭代器`（Input iterator）——可以通过解引用引用对象。例如，对象可以在容器中。最纯的输入迭代器只保证读取访问。
- `输出迭代器`（Output iterator）——允许程序员向容器写入数据。最严格的输出迭代器只保证写入访问。

上述列表的基础迭代器类型进一步细分为：

- `前向迭代器`（Forward iterator）——输入和输出迭代器的细化，允许输入和输出。前向迭代器可以是常量的，允许对指向的对象进行只读访问，否则允许读写操作，使其变为可变的。前向迭代器通常用于单链表。
- `双向迭代器`（Bidirectional iterator）——前向迭代器的细化，也可以递减以向后移动。双向迭代器通常用于双向链表。
- `随机访问迭代器`（Random access iterators）——通来说，它是双向迭代器概念的细化，允许加减偏移量，或者允许一个迭代器减去另一个以找到容器中两个对象之间的相对间距或距离。随机迭代器通常用于数组。

* * *

注意

在实现层面，*细化*（refinement）可以视为*继承*（inheritance）或*特化*（specialization）。

* * *

### STL 算法

查找、排序、反转等操作是标准的编程需求，不应要求程序员重新编写实现来实现支持这些功能。这正是 STL 以 STL 算法的形式提供这些函数的原因，它们通过迭代器与容器良好配合，帮助程序员满足一些最常见的需求。

一些常用的 STL 算法有：

- `std::find`——帮助在集合中查找一个值。
- `std::find_if`——帮助根据特定的用户定义谓词在集合中查找一个值。
- `std::reverse`——反转一个集合。
- `std::remove_if`——帮助根据用户定义的谓词从集合中移除某项。
- `std::transform`——帮助将用户定义的转换函数应用于容器中的元素。

这些算法是 `std` 命名空间中的模板函数，需要包含标准头文件 `<algorithm>`。

### 使用迭代器的容器与算法之间的交互

让我们通过一个示例来看迭代器如何无缝地连接容器和 STL 算法。显示 15.1 中的程序使用了 STL 顺序容器 `std::vector`（类似于动态数组）来存储一些整数，然后使用算法 `std::find` 在集合中查找其中一个。注意迭代器是如何形成连接两者的桥梁的。不要担心语法或功能的复杂性。`std::vector` 等容器和 `std::find` 等算法分别在 第 17 节 “STL 动态数组类”和 第 23 节 “STL 算法”中进行了详细讨论。如果你觉得这部分复杂，可以暂时跳过该节。

**列表 15.1** 在 Vector 中查找元素及其位置

```cpp
1: #include <iostream>
2: #include <vector>
3: #include <algorithm>
4: using namespace std;
5:
6: int main ()
7: {
8:     // A dynamic array of integers
9:     vector <int> intArray;
10:
11:     // Insert sample integers into the array
12:     intArray.push_back (50);
13:     intArray.push_back (2991);
14:     intArray.push_back (23);
15:     intArray.push_back (9999);
16:
17:     cout << "The contents of the vector are: " << endl;
18:
19:     // Walk the vector and read values using an iterator
20:     vector <int>::iterator arrIterator = intArray.begin ();
21:
22:     while (arrIterator != intArray.end ())
23:     {
24:             // Write the value to the screen
25:             cout << *arrIterator << endl;
26:
27:             // Increment the iterator to access the next element
28:             ++ arrIterator;
29:     }
30:
31:     // Find an element (say 2991) using the 'find' algorithm
32:     vector <int>::iterator elFound = find (intArray.begin ()
33:                                     intArray.end (), 2991);
34:
35:     // Check if value was found
36:     if (elFound != intArray.end ())
37:     {
38:             // Determine position of element using std::distance
39:             int elPos = distance (intArray.begin (), elFound);
40:             cout << "Found at position: " << elPos << endl;
41:     }
42:
43:     return 0;
44: }
```



输出：
```
The contents of the vector are:
50
2991
23
9999
Found at position: 1
```

在本节中，你学习了 STL 容器、迭代器和算法所基于的概念。你还接触了`basic_string<T>`，我们将在接下来的课程中对其进行详细讨论。容器、迭代器和算法是 STL 中最重要的概念之一，彻底理解这些概念将帮助你在应用程序中高效地使用 STL。第 17 节到第 25 节将更详细地阐述这些概念的实现及其应用。

## 问答

**Q：我需要使用数组。但我不知道它需要包含多少个元素。我应该使用哪种 STL 容器？**

**A**：`std::vector`或`std::deque`完美符合这一需求。它们都能管理内存，并根据应用程序不断增长的需求动态调整自身的大小。

**Q：我的应用有涉及频繁搜索的需求。我应该选择哪种容器？**

**A**：像`std::map`或`std::set`这样的关联容器或它们的无序变体最适合涉及频繁搜索的需求。

**Q：我需要存储键值对以便快速查找。然而，用例可能会导致出现多个不唯一的键。我应该选择哪种容器？**

**A**：类型为`std::multimap`的关联容器适合这种需求。`multimap`可以持有非唯一的键值对，并提供关联容器特有的快速查找功能。

**Q：一个应用程序需要在不同的平台和编译器之间迁移。需要一种可以帮助根据键进行快速查找的容器。我应该使用`std::map`还是`std::hash_map`？**

**A**：可移植性是一个重要的约束条件，使用符合标准的容器是必要的。`hash_map`并不是 C++ 标准的一部分，因此可能在与应用程序相关的所有平台上都不支持。如果你在所有相关平台都使用符合 C++11 标准的编译器，可以使用`std::unordered_map`。

## 工作坊

工作坊包含测试题，旨在帮助你巩固对所涵盖内容的理解。在查看附录 E 中的答案之前，尝试回答这些测试题，并在进入下一节之前确保你已经理解了答案。

### 测验

**1.** 如果容器必须包含一个对象数组，且允许在顶部和底部进行插入，你会选择哪种容器？

**2.** 你需要存储元素以便进行快速查找。你会选择哪种容器？

**3.** 你需要将元素存储在`std::set`中，但仍需根据不一定是元素值的条件来更改存储和查找标准。这可能吗？

**4.** STL 中用哪种特性来连接算法和容器？

**5.** 在需要迁移到不同平台并使用不同 C++ 编译器构建的应用程序中，你会选择使用容器`hash_set`吗？

## 第 16 节. STL String 类

标准模板库（STL）为程序员提供了一个有助于字符串操作和处理的容器类。`string`类不仅能够动态调整自身的大小以适应应用程序的需求，还提供了实用的辅助函数或方法，帮助处理和使用字符串。

因此，它帮助程序员在应用程序中使用标准、可移植且经过测试的功能，并将精力集中在开发至关重要的特性上。

在本节中，你将学习到：

![Image](img/square.jpg) 为什么字符串处理类是必要的

![Image](img/square.jpg) 如何使用 STL `string`类

![Image](img/square.jpg) STL 如何帮助你轻松地连接、追加、查找并执行其他字符串操作

![Image](img/square.jpg) 如何使用基于模板实现的 STL `string`

![Image](img/square.jpg) 自 C++14 起 STL `string`支持的`operator ""s`

### 字符串处理类的必要性

在 C++ 中，`string`是一个字符数组。正如你在第 4 节“管理数组和字符串”中所示，最简单的字符数组可以定义如下：

```cpp
char staticName [20];
```

`staticName`是一个固定为 20 个元素的（因此是静态的）字符数组（也称为字符串）的声明。如你所见，这个缓冲区可以存放有限长度的字符串，如果你尝试在其放入更多的字符，它很快就会溢出。调整这种静态分配的数组是不可能的。为了克服这一限制，C++ 提供了数据的动态分配。因此，`string array`更具动态性的表示方式是：

```cpp
char* dynamicName = new char [arrayLen];
```

`dynamicName`是一个动态分配的字符数组，可以实例化为值`arrayLen`中存储的长度，这可以在运行时确定，因此可以分配来持有变长度的数据。然而，如果你想在运行时更改数组的长度，必须先释放已分配的内存，然后重新分配以持有所需的数据。

如果这些`char*`字符串被用作类的属性，情况就会变得复杂。当一个类的对象赋值给另一个对象时，如果没有正确编写拷贝构造函数和赋值运算符，这两个对象将包含指针的拷贝，本质上指向同一个内存位置。结果是两个对象中包含相同的指针，因此指向内存中的同一位置。第一个对象的析构会导致另一个对象中的指针失效，崩溃迫在眉睫。

字符串类为你解决了这些问题。STL 字符串类建模字符字符串的`string`和建模宽字符字符串的`wstring`从以下方面帮助你：

![Image](img/square.jpg) 减少了字符串创建和处理的努力

![Image](img/square.jpg) 通过内部管理内存分配增加了编写程序的稳定性

![Image](img/square.jpg) 特有的拷贝构造函数和赋值运算符自动确保成员被正确拷贝

![Image](img/square.jpg) 提供实用的工具函数，例如截断、查找和删除等

![Image](img/square.jpg) 提供有助于比较的运算符

![Image](img/square.jpg) 让你将精力放在应用程序的主要需求上，而不是字符串处理细节

**注意**：`std::string`和`std::wstring`实际上是同一个类的模板特化，分别是针对类型`char`和`wchar_t`的`basic_string<T>`。当你学会了使用其中一个，就可以在另一个上使用相同的方法和运算符。

你很快将学习 STL 字符串类提供的一些实用的辅助函数，以`std::string`为例。

### 使用 STL String 类

最常用的字符串函数有：

![Image](img/square.jpg) 拷贝

![Image](img/square.jpg) 连接

![Image](img/square.jpg) 查找字符和子字符串

![Image](img/square.jpg) 截断

![Image](img/square.jpg) 字符串反转和大小写转换，这些是通过标准库提供的算法实现的

要使用 STL 字符串类，必须包含头文件`<string>`。

#### 实例化 STL String 和拷贝

`string`类具有许多重载的构造函数，因此可以用许多不同的方式进行实例化和初始化。例如，你可以简单地将一个常量字符字符串字面量初始化或赋值给一个 STL `std::string`对象：

```cpp
const char* constCStyleString = "Hello String!";
std::string strFromConst (constCStyleString);
```

或者

```cpp
std::string strFromConst = constCStyleString;
```

上述操作类似于：

```cpp
std::string str2 ("Hello String!");
```

显而易见，实例化字符串对象并将其初始化为值不需要提供字符串的长度或内存分配细节——STL string 类的构造函数会自动完成这些操作。

同样，可以使用一个`string`对象来初始化另一个：

```cpp
std::string str2Copy (str2);
```

你还可以指示`string`的构造函数只接受输入字符串的前`n`个字符：

```cpp
// 初始化一个字符串为另一个字符串的前 5 个字符
std::string strPartialCopy (constCStyleString, 5);
```

你还可以初始化一个字符串以包含特定数量的特定字符：

```cpp
// 初始化一个字符串对象包含 10 个 'a'
std::string strRepeatChars (10, 'a');
```

列表 16.1 分析了一些通用的`std::string`实例化和字符串拷贝技术。

**列表 16.1** STL 字符串实例化与拷贝技术

```cpp
0: #include <string>
1: #include <iostream>
2:
3: int main ()
4: {
5:     using namespace std;
6:     const char* constCStyleString = "Hello String!";
7:     cout << "Constant string is: " << constCStyleString << endl;
8:
9:     std::string strFromConst (constCStyleString);  //构造函数
10:    cout << "strFromConst is: " << strFromConst << endl;
11:
12:     std::string str2 ("Hello String!");
13:     std::string str2Copy (str2);
14:     cout << "str2Copy is: " << str2Copy << endl;
15:
16:     // 初始化一个字符串为另一个字符串的前 5 个字符
17:     std::string strPartialCopy (constCStyleString, 5);
18:     cout << "strPartialCopy is: " << strPartialCopy << endl;
19:
20:     // 初始化一个字符串对象包含 10 个 'a'
21:     std::string strRepeatChars (10, 'a');
22:     cout << "strRepeatChars is: " << strRepeatChars << endl;
23:
24:     return 0;
25: }
```

输出 ![Image](img/arrow.jpg)

```
Constant string is: Hello String!
strFromConst is: Hello String!
str2Copy is: Hello String!
strPartialCopy is: Hello
strRepeatChars is: aaaaa
```

上述代码显示了如何实例化一个`string`对象并将其初始化为另一个字符串，创建部分拷贝或将你的`string`对象初始化为一组重复字符。`constCStyleString`是一个包含值的 C 风格字符字符串，在第 6 行初始化。第 9 行显示了`std::string`如何通过构造函数创建拷贝。第 12 行将另一个常量字符串拷贝到`std::string`对象中，第 13 行演示了`std::string`的另一个重载构造函数允许你拷贝一个`std::string`对象以得到`str2Copy`。第 17 行演示了如何实现部分拷贝，第 21 行演示了`std::string`如何实例化并初始化为包含相同字符的出现。此代码示例只是小规模演示了`std::string`及其拷贝构造函数如何让程序员轻松地创建、拷贝和显示字符串。

注意：如果你使用字符字符串从另一个同类型的字符串进行拷贝，则列表 16.1 中第 9 行的对应代码如下：

```cpp
const char* constCStyleString = "Hello World!";
// 为了创建一个拷贝，首先为其中分配内存
char* copy = new char [strlen(constCStyleString) + 1];
strcpy(copy, constCStyleString); // 
delete copy;
```

你可以看到，`string`的内容可以通过迭代器或下标运算符来访问。`string`的表示可以通过成员函数`c_str()`获取。

### 访问 `string` 的内容

**列表 16.2** 访问 `string` 的下标运算符与迭代器

```cpp
0: #include <string>
1: #include <iostream>
2:
3: int main ()
4: {
5:     using namespace std;
6:     string stlString ("Hello String");
7:
8:     // 使用下标运算符
9:     cout << "Display elements in string using array-syntax: " << endl;
10:    for (size_t charCounter = 0; charCounter < stlString.length(); ++charCounter)
11:    {
12:        cout << "Character [" << charCounter << "] is: " << stlString[charCounter] << endl;
13:    }
14:    cout << endl;
15:
16:    // 使用迭代器
17:     cout << "Display elements in string using iterators: " << endl;
18:     int charOffset = 0;
19:     string::const_iterator charLocator;
20:     for (auto charLocator = stlString.cbegin(); charLocator != stlString.cend(); ++charLocator)
21:     {
22:        cout << "Character [" << charOffset++ << "] is: " << *charLocator << endl;
23:     }
24:     cout << endl;
25:
26:     // 以 const char* 输出
27:     cout << "The char* representation of the string is: " << endl;
28:     cout << stlString.c_str () << endl;
29:
30:     return 0;
31: }
```

输出 ![Image](img/arrow.jpg)

```
Display elements in string using array-syntax:
Character [0] is: H
Character [1] is: e
Character [2] is: l
Character [3] is: l
Character [4] is: o

Display elements in string using iterators:
Character [0] is: H
Character [1] is: e
Character [2] is: l
Character [3] is: l
Character [4] is: o

The char* representation of the string is:
Hello String
```

该代码展示了访问`string`内容的多种方法。迭代器的重要性在于，`string`的许多成员函数都以迭代器的形式返回其结果。第 11–17 行通过下标操作符`[]`使用类数组语义来显示`string`中的字符，该操作符由`std::string`类实现。请注意，该操作符需要你提供偏移量（offset），如第 16 行所示。因此，不要越界`string`的边界非常重要；也就是说，你不要读取超出`string`长度的偏移量处的字符。第 24–30 行也使用迭代器逐字符打印`string`的内容。

**提示**：你可以通过使用关键字`auto`来避免第 24 行中看到的繁琐的迭代器声明，从而告诉编译器使用`std::string::cbegin()`的返回值来确定`charLocator`的类型，如下所示：

```cpp
24: // delete line: string::const_iterator charLocator;
25: for (auto charLocator = stlString.cbegin();
26:      charLocator != stlString.cend();
27:      ++ charLocator )
28: {
29:    cout << "Character ["<<charOffset++ << "] is: ";
30:    cout << *charLocator << endl;
31: }
```

### 将一个字符串拼接到另一个字符串

字符串拼接可以使用`+=`操作符或`append()`成员函数来实现：

```cpp



`string sampleStr1 ("Hello");`

`string sampleStr2 (" String! ");`

`sampleStr1 += sampleStr2;` // 使用 `std::string::operator+=`

// 或者使用 `std::string::append()`

`sampleStr1.append (sampleStr2);` // (针对 `char*` 也进行了重载)

`Listing 16.3` 展示了这两种变体的用法。

**列表 16.3** 使用相加赋值符 (`+=`) 或 `append()` 拼接字符串

点击此处查看代码图片

```cpp
0: #include <string>
1: #include <iostream>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     string sampleStr1 ("Hello");
8:     string sampleStr2 (" String!");
9:
10:     // 拼接
11:     sampleStr1 += sampleStr2;
12:     cout << sampleStr1 << endl << endl;
13:
14:     string sampleStr3 (" Fun is not needing to use pointers!");
15:     sampleStr1.append (sampleStr3);
16:     cout << sampleStr1 << endl << endl;
17:
18:     const char* constCStyleString = " You however still can!";
19:     sampleStr1.append (constCStyleString);
20:     cout << sampleStr1 << endl;
21:
22:     return 0;
23: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```
Hello String!

Hello String! Fun is not needing to use pointers!

Hello String! Fun is not needing to use pointers! You however still can!
```

分析 ![Image](img/arrow.jpg)

第 11、15 和 19 行展示了向 STL `string` 拼接的各种方法。请注意 `+=` 操作符的使用以及 `append` 函数的能力，它具有许多重载版本，可以接受另一个 `string` 对象（如第 11 行所示），也可以接受 C 风格的字符字符串。

### 在字符串中查找字符或子字符串

STL `string` 提供了一个 `find()` 成员函数，并带有几个重载版本，帮助在给定的 `string` 对象中查找字符或子字符串。

点击此处查看代码图片

```cpp
// 在 sampleStr 中从位置 0 开始查找子字符串 "day"
size_t charPos = sampleStr.find ("day", 0);

// 检查是否找到了子字符串，与 string::npos 进行比较
if (charPos != string::npos)
    cout << "First instance of \"day\" was found at position " << charPos;
else
    cout << "Substring not found.";
```

`Listing 16.4` 展示了 `std::string::find()` 的用处。

**列表 16.4** 使用 `string::find()` 定位子字符串或 `char`

点击此处查看代码图片

```cpp
0: #include <string>
1: #include <iostream>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     string sampleStr ("Good day String! Today is beautiful!");
8:     cout << "Sample string is:" << endl << sampleStr << endl << endl;
9:
10: // 在 sampleStr 中从位置 0 开始查找子字符串 "day"
11:     size_t charPos = sampleStr.find ("day", 0);
12: // 检查是否找到了子字符串，与 string::npos 进行比较
13:     if (charPos != string::npos)
14:         cout << "First instance of \"day\" was found at position " << charPos;
15:     else
16:         cout << "Substring not found.";
17:
18:     // Locating all instances of "day"
19:     size_t strPos_ = sampleStr.find("day");
20:     while (strPos_ != string::npos) {
21:         cout << "Found instance of \"day\" at position " << strPos_ << endl;
22:         // 从下一个位置开始查找
23:         strPos_ = sampleStr.find("day", strPos_ + 1);
24:     }
25:
26:     return 0;
27: }
```

```cpp
cout << "The original sample string is: " << endl;
cout << sampleStr << endl << endl;

// Delete characters given position and count
cout << "Truncating the second sentence: " << endl;
sampleStr.erase (13, 28);
cout << sampleStr << endl << endl;

// Find character 'S' using find() algorithm
string::iterator iCharS = find (sampleStr.begin (),
                                 sampleStr.end (), 'S');

// If character found, 'erase' to deletes a character
cout << "Erasing character 'S' from the sample string:" << endl;
if (iCharS != sampleStr.end ())
    sampleStr.erase (iCharS);
cout << sampleStr << endl << endl;

// Erase a range of characters using an overloaded version of erase()
cout << "Erasing a range between begin() and end(): " << endl;
sampleStr.erase (sampleStr.begin (), sampleStr.end ());

// Verify the length after the erase() operation above
if (sampleStr.length () == 0)
    cout << "The string is empty" << endl;

return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

原始示例字符串为：
`Hello String! Wake up to a beautiful day!`

截断第二个句子：
`Hello String!`

从示例字符串中删除字符 'S'：
`Hello tring!`

删除 `begin()` 和 `end()` 之间的范围：
字符串为空

## 分析 ![Image](img/arrow.jpg)

该代码列表显示了 `erase()` 函数的三个版本。其中一个版本在提供起始偏移量和计数时删除一组字符，如第 14 行所示。另一个版本在给定指向该字符的迭代器时删除特定字符，如第 24 行所示。最后一个版本通过给定两个提供该范围边界的迭代器来删除范围内的字符，如第 30 行所示。由于该范围的边界是由 `string` 的 `begin()` 和 `end()` 成员函数提供的，这实际上包含了字符串的所有内容，因此对该范围调用 `erase()` 将清空字符串对象的内容。注意，`string` 类还提供了一个 `clear()` 函数，可以有效地清空内部缓冲区并重置 `string` 对象。

### 提示

C++11 帮助简化冗长的迭代器声明，如列表 16.5 所示：

```cpp
点击此处查看代码图像

string::iterator iCharS = find (sampleStr.begin(),
                                 sampleStr.end (), 'S');
```

为了减少这种情况，可以使用第 3 节 中“使用变量、声明常量”中引入的 `auto` 关键字：

```cpp
点击此处查看代码图像

auto iCharS = find (sampleStr.begin(),
                   sampleStr.end (), 'S');
```

编译器根据 `std::find()` 的返回值自动推导出 `iCharS` 的类型。

### 字符串反转

有时反转字符串的内容是非常重要的。假设你想确定用户输入的字符串是否为回文。一种方法是反转该相同字符串的副本，然后比较两者。STL 字符串可以使用通用算法 `std::reverse()` 轻松地反转：

```cpp
点击此处查看代码图像

string sampleStr ("Hello String! We will reverse!");
reverse (sampleStr.begin (), sampleStr.end ());
```

列表 16.6 展示了算法 `std::reverse()` 在 `std::string` 中的应用。

**列表 16.6** 使用 `std::reverse` 反转 STL 字符串

```cpp
点击此处查看代码图像

#include <string>
#include <iostream>
#include <algorithm>

int main () {
    using namespace std;

    string sampleStr ("Hello String! We will reverse!");
    cout << "The original string is: " << endl;
    cout << sampleStr << endl << endl;

    reverse (sampleStr.begin (), sampleStr.end ());

    cout << "After applying the std::reverse algorithm: " << endl;
    cout << sampleStr << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

原始示例字符串为：
`Hello String! We will reverse!`

应用 `std::reverse` 算法后：
`!uoy esrever lliw eW !gnirtS olH`

## 分析 ![Image](img/arrow.jpg)

第 12 行使用的 `std::reverse()` 算法在通过两个输入参数提供的容器边界上工作。在这种情况下，这些边界是 `string` 对象的起始和结束边界，反转了整个字符串的内容。也可以通过输入适当的边界来部分反转字符串。注意，该范围的边界是 `begin()` 和 `end()` 的。

### 字符串转换

字符串转换可以使用算法 `std::transform()` 实现，它对集合的每个元素应用指定的函数。在这种情况下，集合是 `string` 对象本身。列表 16.7 显示了如何切换 `string` 的大小写。

**列表 16.7** 使用 `std::transform()` 转换 STL 字符串的大写

```cpp
点击此处查看代码图像

#include <string>
#include <iostream>
#include <algorithm>

int main () {
    using namespace std;

    cout << "Please enter a string for case-convertion:" << endl;
    cout << "> ";
    string inStr;
    getline (cin, inStr);
    cout << endl;

    transform(inStr.begin(), inStr.end(), inStr.begin(), ::toupper);
    cout << "The string converted to upper case is: " << endl;
    cout << inStr << endl << endl;

    transform(inStr.begin(), inStr.end(), inStr.begin(), ::tolower);
    cout << "The string converted to lower case is: " << endl;
    cout << inStr << endl << endl;

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

请输入一个用于转换转换的字符串：
> `ConverT thIS Str!`

转换为大写的字符串为：
`CONVERT THIS STRING!`

转换为小写的字符串为：
`convert this string!`

## 分析 ![Image](img/arrow.jpg)

第 15 行和第 19 行展示了如何高效地使用 `std::transform()` 更改字符串的内容

### STL 字符串的模板实现

正如你所学的，`std::string` 类实际上是 STL 模板类 `std::basic_string <T>` 的特化。容器 `basic_string` 的模板声明如下：

```cpp
点击此处查看代码图像

template<class _Elem,
    class _Traits,
    class _Ax>
    class basic_string
```

在这个模板定义中，最重要的参数是第一个：`_Elem`。它是 `basic_string` 对象收集的类型。因此，`std::string` 是针对 `_Elem=char` 的模板特化，而 `wstring` 是针对 `_Elem=wchar_t` 的模板特化。换句话说，STL `string` 类定义为：

```cpp
点击此处查看代码图像

typedef basic_string<char, char_traits<char>, allocator<char> >
    string
```

而 STL `wstring` 类定义为：

```cpp
点击此处查看代码图像

typedef basic_string<wchar_t, char_traits<wchar_t>, allocator<wchar_t> >
    string;
```

因此，到为止学习的所有字符串特性和函数实际上都是由 `basic_string` 提供的，因此也适用于 STL 的 `wstring` 类。

* * *

**提示**

在编写需要更好地支持非拉丁字符（如日语或中文字符）的应用程序时，你会使用 `std::wstring`。

* * *

### C++14 中 `std::string` 中的 `operator ""s`

符合 C++14 标准的库版本支持 `operator ""s`，它可以将引号内的字符串完整地转换为 `std::basic_string<t>`。如列表 16.8 所示，这使得某些字符串操作变得直观而简单。

**列表 16.8** 使用 C++14 引入的 `operator ""s`

点击此处查看代码图像

* * *

```cpp
0: #include<string>
1: #include<iostream>
2: using namespace std;
3:
4: int main()
5: {
6:     string str1("Traditional string \0 initialization");
7:     cout << "Str1: " << str1 << " Length: " << str1.length() <<  endl;
8:
9:     string str2("C++14 \0 initialization using literals"s);
```



10:     `cout << "Str2: " << str2 << " Length: " << str2.length() <<  endl;`

11:

12:     `return 0;`

13: }

```

* * *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`Str1: Traditional string Length: 19`

`Str2: C++14 initialization using literals Length: 37`

**分析** ![Image](img/arrow.jpg)

第 6 行从普通字符字面量初始化了一个 `std::string` 实例。注意字符串中间放置的空字符，这导致 `str1` 完全忽略了 `"initialization"` 这个单词。第 9 行使用了 C++14 引入的 `operator ""s`，演示了实例 `str2` 现在如何能够包含（因此也可以操作）包含空字符的字符缓冲区，例如。

* * *

**注意**

C++14 在 `std::chrono` 中引入了字面量 `operator ""s`，如下：

点击此处查看代码图像

```
std::chrono::seconds timeInSec(100s); // 100 秒
std::string timeinText = "100"s; // 字符串 "100"
```

前者表示秒数，是一个整数字面量，而后者给出一个字符串。

* * *

* * *

**提示**

预计 C++17 将引入 `std::string_view`，它有望通过避免不内存分配来提高性能。访问第 29 ，“展望”，以了解此特性以及预计在 C++17 中的其他特性。

* * *

### 总结

在本节中，你学习了 STL `string` 类是标准模板库提供的一个容器，它可以帮助程序员处理许多字符串操作需求。使用该类的优势显而易见，程序员实现内存管理、字符串比较和字符串操作函数的需求已由 STL 框架提供的容器类处理了。

### 问答

**Q 我需要使用 `std::reverse()` 反转字符串。我需要包含哪个头文件才能使用此函数？**

**A** `<algorithm>` 是使用 `std::reverse()` 需要包含的头文件。

**Q 在使用 `tolower()` 函数将字符串转换为小写时，`std::transform()` 起了什么作用？**

**A** `std::transform()` 为 `string` 对象中位于 transform 函数提供的边界范围内的字符调用 `tolower()`。

**Q 为什么 `std::wstring` 和 `std::string` 具有完全相同的行为和成员函数？**

**A** 这是因为它们都是模板类 `std::basic_string` 的模板特化化版本。

**Q STL `string` 类的比较运算符 `<` 产生的结果是大小敏感还是不大小敏感的？**

**A** 结果基于大小敏感的比较。

## 工作坊

工作坊包含测验题，帮助巩固你对涵盖内容的理解，并提供练习以获得使用所学内容的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，并确保在进入下一节之前理解了这些答案。

### 测验

**1.** `std::string` 特化了哪个 STL 模板类？

**2.**

**3.**

### 练习题

**1.** 编写一个程序，告诉用户输入是一个回文。

**2.** 编写一个程序，告知元音数量。

**3.** 将交替字符转换为大写。

**4.** 你的程序应该有四个对象。

**5.** 编写一个程序显示字符串中 'a' 的出现次数。

## 17. 动态数组类

与静态数组不同，动态数组为程序员提供了在未知确切大小的情况下存储数据的灵活性。由于这是经常需要的，标准模板库 (STL) 以 `vector` 类的形式提供了现成的解决方案。在本节中，你学习

![Image](img/square.jpg) `vector` 的特性

![Image](img/square.jpg) 典型的 `vector` 操作

![Image](img/square.jpg) 的大小和容量的概念

![Image](img/square.jpg) STL `deque` 类

### `std::vector` 的特性

`vector` 是一个模板类，提供了动态数组的通用功能并具有以下特点：

![Image](img/square.jpg) 常数时间内向数组末尾添加元素；这意味着插入所需取决于数组的大小。从末尾删除元素也是如此。

![Image](img/square.jpg) 在中间插入或删除元素的时间与后面的元素数量成正比。

![Image](img/square.jpg) 持有的元素数量是动态的，由 `vector` 类管理内存。

*vector* 可以可视如图 17.1](#ch17.html_ch17fig01）所示。

![Image](img/17fig01.jpg)

**图 17.1** vector 的内部结构

* * *

**提示**

使用 `std::vector` 类包含头文件：

```
#include <vector>
```

* * *

### 典型的 vector 操作

`vector` 的行为规范和公共成员由 C++ 标准定义。因此，你在本节中学习的 `vector` 操作由各种标准的 C++ 平台支持。

#### 实例化 Vector

`vector` 是一个模板类，需要按照第 14 节](#ch14.html_ch14)“宏与模板简介](#ch14.html_ch14)”涵盖的模板实例化技术进行实例化。`vector` 的模板实例化需要指定你想在这个动态数组中收集的对象类型。

点击此处查看代码图像

```
std::vector<int> dynIntArray; // 包含整数的 vector
std::vector<float> dynFloatArray; // 包含浮点数的 vector
std::vector<Tuna> dynTunaArray; // 包含金枪的 vector
```

要声明一个指向列表中元素的迭代器，你会使用

点击此处查看代码图像

`std::vector<int>::const_iterator elementInVec;`

如果你需要一个可以修改值或调用非 `const` 函数的迭代器，你应该使用 `iterator` 而不是 `const_iterator`。

鉴于 `std::vector` 有几个重载的构造函数，你还可以选择在实例化 vector 时告诉它初始时应包含的元素数量及其初始值，或者在实例化另一个 vector 时使用一个 vector 的部分或全部。

列表 17.1 展示了几个 vector 的实例化方式。

**列表 17.1** 实例化 `std::vector:` 的不同形式：指定大小、初始值以及从另一个向量拷贝值

点击此处查看代码图像

```cpp
#include <vector>

int main ()
{
    // 整数类型的 vector
    std::vector<int> integers;

    // 使用 C++11 列表初始化化的 vector
    std::vector<int> initVector{ 202, 2017, -1 };

    // 实例化一个包含 10 个元素的 vector（它仍然可以增长）
    std::vector<int> tenElements (10);

    // 实例化一个包含 10 个元素的 vector，每个元素初始化为 90
    std::vector<int> tenElemInit (10, 90);

    // 将 vector 初始化为另一个 vector 的内容
    std::vector<int> copyVector (tenElemInit);

    // 使用迭代器从另一个 vector 初始化为 5 个元素的 vector
    std::vector<int> partialCopy (tenElements.cbegin(),
                                  tenElements.cbegin() + 5);

    return 0;
}
```

分析：前面的代码针对 `int` 类型对 `vector` 类进行了模板特化化；换句话说，它实例化了一个整数 `vector`。这个名为 `integers` 的 `vector` 使用了第 5 行的默认构造函数，这在你不知道容器的最小大小需求时非常有用——即当你不知道想在其中存储多少个整数时。第 8 行所示的第二实例化形式使用了 C++11 引入的列表初始化概念，用三个包含值 202、2017 和 –1 的元素来初始化 `initVector`。第 11 行和第 14 行所示的 `vector` 实例化是程序员知道自己需要一个至少包含 10 个元素的 `vector`。注意，这并不会限制容器的最终 `size`，而只是设置了初始 `size`。最后，第 17 行和第 20 行演示了如何使用 `vector` 来实例化另一个向量的内容——换句话说，创建一个另一个拷贝或其部分的 `vector` 对象。这种构造也适用于所有的 STL 容器。最后一种形式是使用迭代器。`partialCopy` 包含了来自 `vecWithTenElements` 的前五个元素。

注意：第四种构造仅适用于相同类型的对象。因此，你可以实例化一个 `vecArrayCopy`——使用另一个整数对象的 `vector` 来实例化一个整数对象的 `vector`。如果其中一个是例如 `float` 类型的 `vector`，则代码将无法编译。

### 使用 `push_back()` 在末尾插入元素

实例化一个整数 `vector` 后，显而易见的任务是向其中插入元素（整数）。在 `vector` 中的插入发生在数组的末尾，并使用成员函数 `push_back()` 将元素“推”入末部：

点击此处查看代码图像

```cpp
vector <int> integers;  // 一个 int 类型的 vector

// 向 vector 插入示例整数：
integers.push_back (50);
integers.push_back (1);
```

列表 17.2 展示了在向 `std::vector` 动态添加元素时使用 `push_back()`。

**列表 17.2** 使用 `push_back()` 在 Vector 中插入元素

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main ()
{
    vector<int> integers;

    // 向 vector 插入示例整数：
    integers.push_back (50);
    integers.push_back (1);
    integers.push_back (987);
    integers.push_back (1001);

    cout << "The vector contains ";
    cout << integers.size () << " Elements" << endl;

    return 0;
}
```

输出：点击此处查看代码图像
`The vector contains 4 Elements`

分析：如第 9-12 行所示，`push_back()` 是 `vector` 公共成员函数，用于在动态数组的末尾插入对象。注意函数 `size()` 的用法，它返回 `vector` 中的元素个数。

### 列表初始化

C++11 通过类 `std::initialize_list` 提供了初始化列表特性，这种功能允许你像初始化静态数组一样初始化容器。`std::vector` 像大多数容器一样支持这种特性，让你在一行内初始化一个包含多个元素的 vector：

```cpp
vector<int> integers = {50, 1, 987, 1001};
```

这种语法在列表 17.2 中减少了行数。

### 使用 `insert()` 在指定位置插入元素

你使用 `push_back()` 在 vector 的末尾插入元素。如果你想在中间插入呢？许多 STL 容器（包括 `std::vector`）都具有 `insert()` 函数，它有许多重载。

在一种形式中，你可以指定插入元素的位置：

```cpp
integers.insert (integers.begin(), 25);
```

在另一种形式中，你可以同时指定位置以及需要插入的元素个数及其值：

```cpp
integers.insert (integers.end(), 2, 45);
```

你还可以将一个 vector 的内容在指定位置插入另一个：

```cpp
// 另一个包含 2 个 30 元素的 vector
vector <int> another (2, 30);

// 在位置 [1] 插入另一个的所有元素
integers.insert (integers.begin() + 1, another.begin(), another.end());
```

迭代器（通常由 `begin()` 或 `end()` 返回）用于告诉 `insert()` 函数你希望放置新元素的位置。

提示：注意此迭代器也可以是 STL 算法的返回值，例如 `std::find()` 函数，它可以用于查找元素并在该位置插入另一个元素（插入会移动找到的元素）。`find()` 等算法将在第 23 节 中详细讨论，“STL 算法](#ch23.html_ch23)。”

```cpp
23:    integers.insert (integers.begin (), 25);
24:
25:    // Insert 2 numbers of value 45 at the end
26:    integers.insert (integers.end (), 2, 45);
27:
28:    cout << "Vector after inserting elements at beginning and end: ";
29:    DisplayVector(integers);
30:
31:    // Another vector containing 2 elements of value 30
32:    vector <int> another (2, 30);
33:
34:    // Insert two elements from another container in position [1]
35:    integers.insert (integers.begin () + 1,
36:        another.begin (), another.end ());
37:
38:    cout << "Vector after inserting contents from another vector: ";
39:    cout << "in the middle:" << endl;
40:    DisplayVector(integers);
41:
42:    return 0;
43: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`vector 的初始内容：90 90 90 90`
`在开头结尾插入元素后的 vector：25 90 90 90 45 45`
`插入另一个 vector 内容后的 vector：在中间：25 30 90 90 45 45`

### 分析

![Image](img/arrow.jpg)

这段代码演示了 `insert()` 函数的作用，它允许将值放在容器的中间。第 17 行的 vector 包含四个初始化为 90。以这个 vector 为起点，我们使用了 `vector::insert()` 函数的多种重载形式。第 23 行在开头添加了一个元素。第 26 行在结尾添加了两个值为 45 的元素。第 35 行演示了如何从另一个 vector 将元素插入中间（在本例中为偏移量 1 的位置）。

尽管 `vector::insert()` 是一个多功能函数，但 `push_back()` 应该是你向 vector 添加元素的首选方法。这是因为 `insert()` 向 vector 添加元素的方式（当位置不是序列末尾时）效率很低，因为在开头或中间添加元素会导致 vector 类移动所有后续元素。因此，取决于序列中对象的类型，这种移动操作的代价（调用拷贝构造函数或赋值运算符）可能是巨大的。在我们的小示例中，vector 包含 `int` 类型的对象，移动成本较低。

### 提示

如果你的容器需要频繁在中间插入，理想情况下你应该选择 第 18  中解释的 STL list 和 forward_list。

### 使用数组语义访问 Vector 中的元素

可以使用以下方法访问 vector 中的元素：通过下标运算符 (`[]`) 使用数组语义，使用成员函数 `at()`，或使用迭代器。

列表 17.1 演示了如何创建一个初始化了 10 个元素的 vector 实例：

点击此处查看代码图像

```cpp
std::vector <int> tenElements (10);
```

你可以使用数组的语法访问并设置单个元素：

点击此处查看代码图像

```cpp
tenElements[3] = 2011; // 设置第 4 个元素
```

列表 17.4 演示了如何使用下标运算符 (`[]`) 访问 vector 中的元素。

**列表 17.4 使用数组语义访问 vector 中的元素**

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <vector>
2:
```



3: int main ()

4: {

5:    using namespace std;

6:    vector <int> integers{ 50, 1, 987, 1001 };

7:

8:    for (size_t index = 0; index < integers.size (); ++index)

9:    {

10:        cout << "Element[" << index << "] = ";

11:        cout << integers[index] << endl;

12:   }

13:

14:    integers[2] = 2011; // 修改第 3 个元素

15:    cout << "After replacement: " << endl;

16:    cout << "Element[2] = " << integers[2] << endl;

17:

18:    return 0;

19: }

```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Element[0] = 50
Element[1] = 1
Element[2] = 987
Element[3] = 1001
替换后：
Element[2] = 2011
```

分析 ![Image](img/arrow.jpg)

在第 11、14 和 16 行，`vector` 被用于像使用静态数组一样通过 `vector` 的下标运算符（`[]`）访问和分配元素。该下标运算符接受的元素索引与静态数组一样是从 0 开始的。注意第 15 行的 `for` 循环是如何编写的，通过与 `vector::size()` 比较来确保索引不会越 `vector` 的边界。

### 注意事项

使用 `[]` 访问 `vector` 中的元素面临着与访问数组元素相同的危险；即你不应越界容器的边界。如果你使用下标运算符（`[]`）访问超出边界的 `vector` 元素，该操作的结果将是未定义的（可能会发生任何情况）。

更安全的替代方案是使用 `at()` 成员函数：

点击此处查看代码图像

```cpp
// 获取位置 2 的元素
cout << integers.at(2);
```

`at()` 版本会在运行时检查 `size()`，如果越界会抛出异常。下标运算符（`[]`）在如上示例所示是不安全的。

### 使用指针语义访问 Vector 中的元素

你也可以通过迭代器使用指针语义来访问 `vector` 中的元素，如列表 17.5 所示。

**列表 17.5 使用指针语义访问 vector 中的元素（迭代器）**

点击此处查看代码图像

```cpp
0: #include <iostream>
1: #include <vector>
2:
3: int main ()
4: {
5:    using namespace std;
6:    vector <int> integers{ 50, 1, 987, 1001 };
7:
8:    vector <int>::const_iterator element = integers.cbegin();
9:    // auto element = integers.cbegin(); // 类型推导
10:
11:    while (element != integers.end())
12:    {
13:        size_t index = distance (integers.cbegin (), element);
14:
15:        cout << "Element at position ";
16:        cout << index << " is: " << *element << endl;
17:
18:        // 移动到下一个元素
19:        ++ element;
20:    }
21:
22:    return 0;
23: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Element at position 0 is: 50
Element at position 1 is: 1
Element at position 2 is: 987
Element at position 3 is: 1001
```

与 `vector` 通过 `push_back()` 函数在末尾插入元素的特征一样，它也具有通过 `pop_back()` 函数移除末尾元素的功能。使用 `pop_back()` 从 `vector` 中移除元素需要常数时间——O(1)——也就是说，所需的时间与 `vector` 中存储的元素数量无关。接下来的列表 17.6 所示代码演示了如何使用函数 `pop_back()` 来删除 `vector` 末尾的元素。

**列表 17.6** 使用 `pop_back()` 删除最后一个元素

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>
using namespace std;

template <typename T>
void DisplayVector(const vector<T>& inVec)
{
    for (auto element = inVec.cbegin(); // auto 和 cbegin(): C++11
          element != inVec.cend();  // cend() 是 C++11 新引入的
          ++ element )
        cout << *element << ' ';
    cout << endl;
}

int main ()
{
    vector <int> integers;
    // 将示例整数插入 vector 中：
    integers.push_back (50);
    integers.push_back (1);
    integers.push_back (987);
    integers.push_back (1001);

    cout << "Vector contains " << integers.size () << " elements: ";
    DisplayVector(integers);

    // 移除末尾的一个元素
    integers.pop_back ();

    cout << "After a call to pop_back()" << endl;
    cout << "Vector contains " << integers.size () << " elements: ";
    DisplayVector(integers);

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Vector contains 4 elements: 50 1 987 1001
After a call to pop_back()
Vector contains 3 elements: 50 1 987
```

### 分析

![Image](img/arrow.jpg)

输出表明第 29 行使用的 `pop_back()` 函数通过删除插入到 `vector` 中的最后一个元素减少了 `vector` 中的元素。第 32 行再次调用 `size()` 证明了 `vector` 中的元素数量确实减少了一个，如输出所示。

### 注意

第 4–13 行的函数 `DisplayVector()` 在列表 17.6 中采用了模板形式，与之相比，列表 17.3 中它只接受整数类型的 `vector`。这有助于我们将此模板函数复用于 `float` 类型的 `vector`（而不是 `int`）：

点击此处查看代码图像

```cpp
vector <float> vecFloats;
DisplayVector(vecFloats); // 正常工作，作为一个泛型函数
```

`DisplayVector()` 的这种泛形式还支持任何类的 `vector`，只要该类具有一个 `cout` 可以理解的返回值的运算符。

### 理解尺寸和容量的概念

`vector` 的 `size` 是存储在 `vector` 中的元素数量。`vector` 的 `capacity` 是 `vector` 在重新分配内存以容纳更多元素之前，可能存储的元素总数。因此，`vector` 的 `size` 小于或等于其 `capacity`。

你可以通过调用 `size()` 查询 `vector` 的元素数量：

点击此处查看代码图像

```cpp
cout << "Size: " << integers.size ();
```

或者通过调用 `capacity()` 查询其容量：

点击此处查看代码图像

```cpp
cout << "Capacity: " << integers.capacity () << endl;
```

当 `vector` 需要频繁重新分配内部数组的内存时，可能会导致一些性能问题。在很大程度上，这个问题可以通过使用成员函数 `reserve(number)` 来解决。`reserve()` 的本质是增加为 `vector` 内部数组分配的内存量，以便在不需要重新分配内存的情况下容纳 `number` 个元素。根据 `vector` 中存储的对象的类型，减少重新分配的次数也可以减少对象拷贝的次数，从而节省性能。列表 17.7 中的代码示例演示了 `size()` 和 `capacity()` 之间的区别。

**列表 17.7** `size()` 和 `capacity()` 的演示

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>

int main ()
{
    using namespace std;

    // 实例化包含 5 个默认值整数的 vector 对象
    vector <int> integers (5);

    cout << "Vector of integers was instantiated with " << integers.size() << " elements" << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // 插入第 6 个元素
    integers.push_back (6);

    cout << "After inserting the 6th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // 插入第 7 个元素
    integers.push_back (7);

    cout << "After inserting the 7th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // 插入第 8 个元素
    integers.push_back (8);

    cout << "After inserting the 8th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    return 0;
}
```



与`vector`通过`push_back()`函数在末尾插入元素的特征一样，它也具有通过`pop_back()`函数移除末尾元素的功能。使用`pop_back()`从`vector`中移除元素需要常数时间——也就是说，所需的时间与`vector`中存储的元素数量无关。接下来的列表 17.6 所示代码演示了如何使用函数`pop_back()`来删除`vector`末尾的元素。

**列表 17.6** 使用`pop_back()`删除最后一个元素

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>

using namespace std;

template <typename T>
void DisplayVector(const vector<T>& inVec)
{
    for (auto element = inVec.cbegin(); // auto 和 cbegin(): C++11
          element != inVec.cend();  // cend() 是 C++11 新引入的
          ++ element )
        cout << *element << ' ';
    cout << endl;
}

int main ()
{
    vector <int> integers;

    // 将示例整数插入 vector 中：
    integers.push_back (50);
    integers.push_back (1);
    integers.push_back (987);
    integers.push_back (1001);

    cout << "Vector contains " << integers.size () << " elements: ";
    DisplayVector(integers);

    // 移除末尾的一个元素
    integers.pop_back ();

    cout << "After a call to pop_back()" << endl;
    cout << "Vector contains " << integers.size () << " elements: ";
    DisplayVector(integers);

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`Vector contains 4 elements: 50 1 987 1001`

`After a call to pop_back()`

`Vector contains 3 elements: 50 1 987`

### 分析

![Image](img/arrow.jpg)

输出表明第 29 行使用的`pop_back()`函数通过删除插入到`vector`中的最后一个元素减少了`vector`中的元素数量。第 32 行再次调用`size()`证明了`vector`中的元素数量确实减少了一个，如输出所示。

### 注意

第 4–13 行的函数`DisplayVector()`在列表 17.6 中采用了模板形式，与之相比，列表 17.3 中它只接受整数类型的`vector`。这有助于我们将此模板函数复用于`float`类型的`vector`（而不是`int`）：

点击此处查看代码图像

```cpp
vector <float> vecFloats;
DisplayVector(vecFloats); // 正常工作，作为一个泛型函数
```

`DisplayVector()`的这种泛形式还支持任何类的`vector`，只要该类具有一个`cout`可以理解的返回值的运算符。

### 理解尺寸和容量的概念

`vector`的`size`是存储在`vector`中的元素数量。`vector`的`capacity`是`vector`在重新分配内存以容纳更多元素之前，可能存储的元素总数。因此，`vector`的`size`小于或等于其`capacity`。

你可以通过调用`size()`查询`vector`的元素数量：

点击此处查看代码图像

```cpp
cout << "Size: " << integers.size ();
```

或者通过调用`capacity()`查询其容量：

点击此处查看代码图像

```cpp
cout << "Capacity: " << integers.capacity () << endl;
```

当`vector`需要频繁重新分配内部数组的内存时，可能会导致一些性能问题。在很大程度上，这个问题可以通过使用成员函数`reserve(number)`来解决。`reserve()`的本质是增加为`vector`内部数组分配的内存量，以便在不需要重新分配内存的情况下容纳`number`个元素。根据`vector`中存储的对象的类型，减少重新分配的次数也可以减少对象拷贝的次数，从而节省性能。列表 17.7 中的代码示例演示了`size()`和`capacity()`之间的区别。

**列表 17.7** `size()`和`capacity()`的演示

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>

int main ()
{
    using namespace std;

    // instantiate a vector object that holds 5 integers of default value
    vector <int> integers (5);

    cout << "Vector of integers was instantiated with " << integers.size() << " elements" << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // Insert the 6th element
    integers.push_back (6);

    cout << "After inserting the 6th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // Insert the 7th element
    integers.push_back (7);

    cout << "After inserting the 7th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    // Insert the 8th element
    integers.push_back (8);

    cout << "After inserting the 8th element:" << endl;
    cout << "Size: " << integers.size() << endl;
    cout << "Capacity: " << integers.capacity() << endl;

    return 0;
}
```

```cpp
#include<deque>
```

`deque`可以可视化如图 17.2 所示。

![Image](img/17fig02.jpg)

**图 17.2** `deque`的内部结构。

`deque`与`vector`类似，它们支持通过`push_back()`和`pop_back()`函数在末尾进行元素的插入和删除。就像`vector`一样，`deque`也允许你通过下标运算符（`[]`）使用数组语义来访问它。`deque`与`vector`的不同之处在于，它还允许你使用`push_front()`在头部插入元素，并使用`pop_front()`从头部删除元素，如列表 17.8 所示。

**列表 17.8** 实例化一个 STL `deque`并使用`push_front()`和`pop_front()`函数在头部插入和删除元素

点击此处查看代码图像

```cpp
0: #include <deque>
1: #include <iostream>
2: #include <algorithm>
3:
4: int main ()
5: {
6:     using namespace std;
7:
8:     // 定义一个整数类型的 deque
9:     deque<int> intDeque;
10:
11:     // 在数组底部插入整数
12:     intDeque.push_back (3);
13:     intDeque.push_back (4);
14:     intDeque.push_back (5);
15:
16:     // 在数组顶部插入整数
17:     intDeque.push_front (2);
18:     intDeque.push_front (1);
19:     intDeque.push_front (0);
20:
21:     cout << "The contents of the deque after inserting elements ";
22:     cout << "at the top and bottom are:" << endl;
23:
24:     // 在屏幕上显示内容
25:     for (size_t count = 0;
26:         count < intDeque.size ();
27:         ++ count )
28:     {
29:         cout << "Element [" << count << "] = ";
30:         cout << intDeque [count] << endl;
31:     }
32:
33:     cout << endl;
34:
35:     // 删除顶部的元素
36:     intDeque.pop_front ();
37:
38:     // 删除底部的元素
39:     intDeque.pop_back ();
40:
41:     cout << "The contents of the deque after erasing an element ";
42:     cout << "from the top and bottom are:" << endl;
43:
44:     // 再次显示内容：这次使用迭代器
45:     // 如果在旧版编译器上，请移除 auto 并取消注释下一行
46:     // deque <int>::iterator element;
47:     for (auto element = intDeque.begin ();
48:         element != intDeque.end ();
49:         ++ element )
50:     {
51:         size_t Offset = distance (intDeque.begin (), element);
52:         cout << "Element [" << Offset << "] = " << *element << endl;
53:     }
54:
55:     return 0;
56: }
```



输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

在顶部和底部插入元素后 `deque` 的内容：

```text
Element [0] = 0
Element [1] = 1
Element [2] = 2
Element [3] = 3
Element [4] = 4
Element [5] = 5
```

从顶部和底部删除元素后 `deque` 的内容：

```text
Element [0] = 1
Element [1] = 2
Element [2] = 3
Element [3] = 4
```

### 分析

第 9 行是实例化整数 `deque` 的地方。注意这种语法与实例化整数 `vector` 的语法有多相似。第 12–14 行显示了 `deque` 成员函数 `push_back()` 的用法，随后在第 17–19 行使用了 `push_front()`。后者使得 `deque` 相比于 `vector` 变得独特。第 36 行所示的 `pop_front()` 的用法也是如此。第 25–31 行所示的显示 `deque` 内容的第一种机制使用了类数组语法来访问元素，而第 47–53 行演示了迭代器的用法。第 51 行使用 `distance()` 来评估元素在 `deque` 中的偏移量，其方式与你在列表 17.5 中看到的对 `vector` 的处理方式相同。

### 提示

当你需要清空诸如 `vector` 或 `deque` 之类的 STL 容器时（即删除其中包含的所有元素），你会使用成员函数 `clear()`。以下代码删除了 `vector` 整数中的所有元素在顶部和底部删除元素：

```cpp
if (intDeque.empty())
    cout << "The container is empty";
```

### 总结

在本节中，你学习了 `vector` 和 `deque` 作为动态数组的基础知识。解释了大小和容量的概念，并看到了如何优化 `vector` 的用法以减少内部缓冲的重新分配。`vector` 是 STL 容器中最简单的，也是最常用的，而且是效率最高的之一。

**2.** 我的 `vector` 返回的 `size()` 为 `10`，`capacity()` 为 `20`。在不需要触发 `vector` 类触发缓冲区重新分配的情况下，我还能向其中插入多少元素？

**3.** `pop_back()` 函数的作用是什么什么？

**4.** 如果 `vector<int>` 是一个整数的动态数组，那么 `vector<Mammal>` 是什么什么类型的动态数组？

**5.** `vector` 中的元素可以被随机访问吗？如果可以，如何操作？

**6.** 哪种迭代器类型允许对 `vector` 中的元素进行随机访问？

### 练习

**1.** 编写一个交互式程序，接受用户输入的整数并将其保存在 `vector` 中。用户应该能够根据索引随时查询存储在 `vector` 中的某个值。

**2.** 扩展练习 1 中的程序，能够告诉用户其查询的值是否已经存在于 `vector` 中。

**3.** Jack 在 eBay 上销售玻璃罐。为了帮助他进行包装和运输，编写一个程序，让他可以在其中输入每个物品的尺寸，将它们存储在 `vector` 中，并在屏幕上打印出来。

**4.** 编写一个应用程序，将 `deque` 初始化为以下三个字符串：`“Hello”`、`“Containers are cool!”` 和 `“C++ is evolving!”`。你必须使用适用于所有类型 `deque` 的泛函数来显示它们。你的应用程序需要演示 C++11 引入的列表初始化（List Initialization）以及 C++14 引入的 `operator ""`。

## 第 18 own：STL `list` 和 `forward_list`

标准模板库（STL）以模板类 `std::list` 的形式为程序员提供了双向链表。链表的主要优势在于可以快速且恒时间内插入和删除元素。从 C++11 开始，你还可以使用 `std::forward_list` 形式的单向链表，它只能单向遍历。

在本节中，你将学习：

- 如何实例化 `list` 和 `forward_list`
- 如何使用 STL `list` 类，包括插入和删除
- 如何反转和排序元素

### `std::list` 的特性

`linked list`（链表）是一个节点集合，其中每个节点除了包含感兴趣的值或对象外，还指向下一个节点；也就是说，每个节点都连接到下一个和上一个节点，如图 18.1 所示。

**图 18.1** 双向链表的视觉表示。

STL 的 `list` 类实现允许在 `list` 的顶部、底部或中间进行常数时间的插入。

> **提示**
>
> 使用类 `std::list`，请包含头文件：

```cpp
#include <list>
```

### 基本 `list` 操作

要使用 STL 的 `list` 类，请包含头文件 `<list>`。存在于 `std` 命名空间中的模板类 `list` 是一个通用实现，在使用任何实用的成员函数之前，需要对其进行模板实例化。

#### 实例化 `std::list` 对象

`list` 的模板实例化需要指定你想在链表中收集的对象类型。因此，列表的初始化看起来如下所示：

```cpp
std::list<int> linkInts;  // 包含整数的列表

std::list<float> listFloats;  // 包含浮点数的列表

std::list<Tuna> listTunas;  // 包含 Tuna 类型对象的列表
```

要声明一个指向列表中元素的迭代器，你将使用：

```cpp
std::list<int>::const_iterator elementInList;
```

如果你需要一个可以用于修改值或调用非 `const` 函数的迭代器，请使用 `iterator` 而不是 `const_iterator`。

由于 `std::list` 的实现提供了一组重载构造函数，你甚至可以创建初始化为包含指定数量元素的列表，每个元素都初始化为一个特定值，如列表 18.1 所示。

**列表 18.1** 实例化 `std::list` 的不同形式，指定元素数量和初始值

```cpp
0: #include <list>

1: #include <vector>

2:

3: int main ()

4: {

5:     using namespace std;

6:

7:     // 实例化一个空列表

8:     list<int> linkInts;

9:

10:    // 实例化一个包含 10 个整数的列表

11:    list<int> listWith10Integers(10);

12:

13:    // 实例化一个包含 4 个整数的列表，每个值均为 99

14:    list<int> listWith4IntegerEach (10, 99);

15:

16:    // 创建一个现有列表的精确拷贝

17:    list<int> listCopyAnother(listWith4Integer99);

18:

19:    // 一个包含 10 个整数的 vector，每个值为 2017

20:    vector<int> vecIntegers(10, 2017);

21:

22:    // 使用来自另一个容器的值实例化列表

23:    list<int> listCopyOfAnother(vecIntegers.cbegin(),

24:                               vecIntegers.cend());

25:

26:    return 0;

27: }
```

此程序没有输出，并演示了在创建整数列表时使用各种重载构造函数的应用。在第 8 行中，你创建了一个空列表，而在第 11 行中，你创建了一个包含 10 个整数的列表。第 14 行是一个名为 `listWith4Integers99` 的列表，它包含 4 个每个初始化为值 99 的整数。第 17 行演示了创建一个与另一个列表精确拷贝的列表。第 20–24 行令人惊讶且奇奇！你实例化了一个包含 10 个整数的 `vector`，每个整数值为 2017，然后在第 23 行中实例化了一个包含从 `vector` 拷贝的元素的列表，使用了由 `vector::cbegin()` 和 `vector::cend()` 返回的 `const` 迭代器（C++11 新增）。列表 18.1 同时也演示了迭代器如何帮助将一个容器的实现与另一个容器解耦，让你能够通过它们的泛型功能使用来自 `vector` 的值来实例化 `list`，如第 23 和 24 行所示。

> **注意**
>
> 将列表 18.1 与第 17 节“STL 动态数组类”中的列表 17.1 进行对比，你会发现不同类型容器的实例化具有非常明显的模式和相似性。使用的 STL 容器越多，看到的模式就越多，操作也越简单。

#### 在列表头部或尾部插入元素

与 `deque` 类似，头部（取决于视角）的插入通过 `list` 成员方法 `push_front()` 实现。尾部的插入通过成员方法 `push_back()` 完成。这两个方法接受一个输入参数，即要插入的值：

```cpp
linkInts.push_back(-1);

linkInts.push_front(2001);
```

列表 18.2 演示了在整数列表上使用这两种方法的效果。

**列表 18.2** 使用 `push_front()` 和 `push_back()` 在列表中插入元素

```cpp
0: #include <list>

1: #include <iostream>

2: using namespace std;

3:

4: template <typename T>

5: void DisplayContents (const T& container)

6: {

7:     for (auto element = container.cbegin();

8:          element != container.cend();

9:          ++ element )

10:        cout << *element << ' ';

11:

12:    cout << endl;

13: }

14:

15: int main ()

16: {

17:     std::list <int> linkInts{ -101, 42 };

18:

19:     linkInts.push_front (10);
```

```cpp
20:    linkInts.push_front (2011);

21:    linkInts.push_back (-1);

22:    linkInts.push_back (9999);

24:

    DisplayContents(linkInts);

26:

    return 0;

27: }
```

输出 ![Image](img/arrow.jpg)

```text
2011 10 -101 42 -1 9999
```

### 分析

分析 ![Image](img/arrow.jpg)

第 17 行展示了 `int` 类型的 `list` 模板实例化，并使用 C++11 列表初始化语法 `{...}` 来确保 `linkInts` 在构造时包含两个相互连接的整数（-101 和 42）。第 19–22 行演示了 `push_front()` 和 `push_back()` 的用法。作为 `push_front()` 参数提供的值将占据列表的第一个位置，而通过 `push_back()` 发送的值将占据最后一个位置。输出通过泛型模板函数 `DisplayContents()` 显示了列表的内容，展示了插入元素的顺序（并证明它们并不是按照插入顺序存储的）。

### 注意事项

列表 18.2 中第 4–13 行的 `DisplayContents()` 是列表 17.6 中 `DisplayVector()` 方法的更通用版本（注意参数列表发生了变化）。尽管后者仅对 `vector` 有效（尽管将其内部存储的元素类型泛化），但此版本即使跨越容器类型也是真正通用的。

你可以使用 `vector`、`list` 或 `deque` 作为参数调用列表 18.2 中的 `DisplayContents()` 版本，它将运行得非常完好。

### 在列表中间插入元素

`std::list` 的特点是其能力能够在常数时间内在集合中间插入元素。这是通过成员函数 `insert()` 实现的。

`list::insert()` 成员函数三种三种：

![Image](img/square.jpg) **形式 1**

点击此处查看代码图片。

```cpp
iterator insert(iterator pos, const T& x)
```

在这里，`insert` 函数接受插入位置作为第一个参数，接受要插入的值作为第二个参数。该函数返回一个指向列表中最近插入的元素的迭代器。

![Image](img/square.jpg) **形式 2**

点击此处查看代码图片。

```cpp
void insert(iterator pos, size_type n, const T& x)
```

此函数接受插入位置作为第一个参数，接受要插入的值作为最后一个参数，以及变量 `n` 中的元素数量。

![Image](img/square.jpg) **形式 3**

点击此处查看代码图片。

```cpp
template <class InputIterator>

void insert(iterator pos, InputIterator f, InputIterator l)
```

此重载变体是一个模板函数，除了接受位置外，还接受两个输入迭代器，这两个迭代器标记了要插入列表的集合边界。注意输入类型 `InputIterator` 是一个模板参数化类型，因此它可以指向任何集合的边界——无论是数组、`vector` 还是另一个 `list`。

列表 18.3 演示了 `list::insert()` 函数这些重载变体的用法。

**列表 18.3** 在列表中插入元素的各种方法

点击此处查看代码图片。

```cpp
0: #include <list>

1: #include <iostream>

2: using namespace std;

3:

4: template <typename T>

5: void DisplayContents (const T& container)

6: {

7:     for (auto element = container.cbegin();

8:             element != container.cend();

9:             ++ element )

10:          cout << *element << ' ';

11:

12:     cout << endl;

13: }

14:

15: int main ()

16: {

17:     list <int> linkInts1;

18:

19:     // 在开头插入元素...

20:     linkInts1.insert (linkInts1.begin (), 2);

21:     linkInts1.insert (linkInts1.begin (), 1);

22:

23:     // 在末尾插入一个元素...

24:     linkInts1.insert (linkInts1.end (), 3);

25:

26:     cout << "The contents of list 1 after inserting elements:" << endl;

27:     DisplayContents (linkInts1);

28:

29:     list <int> linkInts2;

30:

31:     // 插入 4 个相同值 0 的元素...

32:     linkInts2.insert (linkInts2.begin (), 4, 0);

33:

34:     cout << "The contents of list 2 after inserting " << linkInts2.size() << " elements of value 0:" << endl;

35:     DisplayContents (linkInts2);

36:

37:     list <int> linkInts3;

38:

39:     // 从另一个列表从开头插入元素...

40:     linkInts3.insert (linkInts3.begin (), linkInts1.begin (), linkInts1.end());

41:

42:     cout << "The contents of list 3 after inserting elements from list 1:" << endl;

43:     DisplayContents (linkInts3);

44:

45:     // 从另一个列表从末尾插入元素...

46:     linkInts3.insert (linkInts3.end (), linkInts2.begin(), linkInts2.end());

47:

48:     cout << "The contents of list 3 after inserting elements from list 2:" << endl;

49:     DisplayContents (linkInts3);

50:

51:     return 0;

52: }
```



输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

2011 10 -101 42 -1 9999

### 分析

分析 ![Image](img/arrow.jpg)

第 17 行展示了 `int` 类型的 `list` 模板实例化，并使用 C++11 列表初始化语法 `{...}` 来确保 `linkInts` 在构造时包含两个相互连接的整数（-101 和 42）。第 19–22 行演示了 `push_front()` 和 `push_back()` 的用法。作为 `push_front()` 参数提供的值将占据列表的第一个位置，而通过 `push_back()` 发送的值将占据最后一个位置。输出通过泛型模板函数 `DisplayContents()` 显示了列表的内容，展示了插入元素的顺序（并证明它们并不是按照插入顺序存储的）。

### 注意事项

列表 18.2 中第 4–13 行的 `DisplayContents()` 是列表 17.6 中 `DisplayVector()` 方法的更通用版本（注意参数列表发生了变化）。尽管后者仅对 `vector` 有效（尽管将其内部存储的元素类型泛化），但此版本即使跨越容器类型也是真正通用的。

你可以使用 `vector`、`list` 或 `deque` 作为参数调用列表 18.2 中的 `DisplayContents()` 版本，它将运行得非常完好。

### 在列表中间插入元素

`std::list` 的特点是其能力能够在常数时间内在集合中间插入元素。这是通过成员函数 `insert()` 实现的。

`list::insert()` 成员函数三种形式：

![Image](img/square.jpg) **形式 1**

点击此处查看代码图片

```cpp
iterator insert(iterator pos, const T& x)
```

在这里，`insert` 函数接受插入位置作为第一个参数，接受要插入的值作为第二个参数。该函数返回一个指向列表中最近插入的元素的迭代器。

![Image](img/square.jpg) **形式 2**

点击此处查看代码图片

```cpp
void insert(iterator pos, size_type n, const T& x)
```

此函数接受插入位置作为第一个参数，接受要插入的值作为最后一个参数，以及变量 `n` 中的元素数量。

![Image](img/square.jpg) **形式 3**

点击此处查看代码图片

```cpp
template <class InputIterator>
void insert(iterator pos, InputIterator f, InputIterator l)
```

此重载变体是一个模板函数，除了接受位置外，还接受两个输入迭代器，这两个迭代器标记了要插入列表的集合边界。注意输入类型 `InputIterator` 是一个模板参数化类型，因此它可以指向任何集合的边界——无论是数组、`vector` 还是另一个 `list`。

列表 18.3 演示了 `list::insert()` 函数这些重载变体的用法。

**列表 18.3** 在列表中插入元素的各种方法

点击此处查看代码图片

```cpp
0: #include <list>
1: #include <iostream>
2: using namespace std;
3:
4: template <typename T>
5: void DisplayContents (const T& container)
6: {
7:     for (auto element = container.cbegin();
8:             element != container.cend();
9:             ++ element )
10:          cout << *element << ' ';
11:
12:     cout << endl;
13: }
14:
15: int main ()
16: {
17:     list <int> linkInts1;
18:
19:     // 在开头插入元素...
20:     linkInts1.insert (linkInts1.begin (), 2);
21:     linkInts1.insert (linkInts1.begin (), 1);
22:
23:     // 在末尾插入一个元素...
24:     linkInts1.insert (linkInts1.end (), 3);
25:
26:     cout << "The contents of list 1 after inserting elements:" << endl;
27:     DisplayContents (linkInts1);
28:
29:     list <int> linkInts2;
30:
31:     // 插入 4 个相同值 0 的元素...
32:     linkInts2.insert (linkInts2.begin (), 4, 0);
33:
34:     cout << "The contents of list 2 after inserting " << linkInts2.size() << " elements of value 0:" << endl;
35:     DisplayContents (linkInts2);
36:
37:     list <int> linkInts3;
38:
39:     // 从另一个列表从开头插入元素...
40:     linkInts3.insert (linkInts3.begin (), linkInts1.begin (), linkInts1.end());
41:
42:     cout << "The contents of list 3 after inserting elements from list 1:" << endl;
43:     DisplayContents (linkInts3);
44:
45:     // 从另一个列表从末尾插入元素...
46:     linkInts3.insert (linkInts3.end (), linkInts2.begin(), linkInts2.end());
47:
48:     cout << "The contents of list 3 after inserting elements from list 2:" << endl;
49:     DisplayContents (linkInts3);
50:
51:     return 0;
52: }
```

### 从列表中删除元素

`list` 成员函数 `erase()` 有两种重载形式：一种接受指向该元素的迭代器，另一种接受一个范围并从而从列表中删除该范围内的元素。你可以在列表 18.4 中看到 `erase()` 函数的实际用法，它演示了如何从列表中删除一个元素或一个范围。

```cpp
29:    linkInts.erase(linkInts.begin(), linkInts.end());
30:    cout << "Number of elements after erasing range: ";
31:    cout << linkInts.size() << endl;
32:
33:    return 0;
34: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

列表的初始内容：
2 4 3 5 -1 2017

删除元素 '2' 后：
4 3 5 -1 2017

删除范围后的元素数量：0

## 分析 ![Image](img/arrow.jpg)

当使用 `insert()` 插入一个值时（如第 20 行所示），它会返回一个指向新插入元素的迭代器。该指向值为 2 的元素的迭代器被存储在变量 `val2` 中，以便稍后在第 26 行调用 `erase()` 时使用，从而从 `list` 中删除该元素。第 29 行演示了使用 `erase()` 删除元素范围的用法。你清除了从 `begin()` 到 `end()` 的范围，这实际上删除了整个列表。

### 提示

清空 STL 容器（如 `std::list`）最短且简单的方法是调用成员函数 `clear()`。

因此，在列表 18.4 中，更简单的第 29 行应该是：

```cpp
linkInts.clear();
```

### 注意

列表 18.4 在第 31 行演示了，可以使用列表方法 `size()` 确定 `std::list` 中元素的数量，这与 `vector` 的对应方法非常相似。这种模式适用于所有的 STL 容器类。

### 反转和排序列表中的元素

`list` 有一个特殊属性：指向 `list` 中元素的迭代器即使元素发生了重排或插入了新元素等，仍然保持有效。为了保持这一重要属性完好无，`list` 函数提供了 `sort()` 和 `reverse()` 作为成员方法，尽管 STL 已经提供了这些算法并能够对 `list` 类进行操作。这些算法的成员版本确保了当元素的相对位置被改变时，指向 `list` 中元素的迭代器不会失效。

#### 使用 `list::reverse()` 反转元素

`list` 具有一个成员函数 `reverse()`，该函数不接受参数，并能为程序员反转 `list` 中内容的顺序：

点击此处查看代码图像

```cpp
linkInts.reverse();  // 反转元素顺序
```

`reverse()` 的用法在列表 18.5 中进行了演示。

**列表 18.5** 反转列表中的元素

点击此处查看代码图像

```cpp
0: #include <list>
1: #include <iostream>
2: using namespace std;
3:
4: template <typename T>
5: void DisplayContents(const T& container)
6: {
7:     for (auto element = container.cbegin();
8:             element != container.cend();
9:             ++ element )
10:        cout << *element << ' ';
11:
12:     cout << endl;
13: }
14:
15: int main()
16: {
17:     std::list<int> linkInts{ 0, 1, 2, 3, 4, 5 };
18:
19:     cout << "Initial contents of list:" << endl;
20:     DisplayContents(linkInts);
21:
22:     linkInts.reverse();
23:
24:     cout << "Contents of list after using reverse():" << endl;
25:     DisplayContents(linkInts);
26:
27:     return 0;
28: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

列表的初始内容：
0 1 2 3 4 5

使用 `reverse()` 后列表内容：
5 4 3 2 1 0

## 分析 ![Image](img/arrow.jpg)

如第 22 行所示，`reverse()` 只是反转了 `list` 中元素的顺序。这是一个无参数的简单调用，确保如果程序员保留了指向 `list` 中元素的迭代器，它们在反转后仍然有效。

#### 排序

`list` 成员函数 `sort()` 有一个不接受参数的版本：

```cpp
linkInts.sort(); // 按升序排序
```

另一个版本允许你通过二元谓词作为参数来定义你自己的优先级：

```cpp
bool SortPredicate_Descending (const int& lhs, const int& rhs)
{
    // list::sort 的标准：对于期望的顺序返回 true
    return (lhs > rhs);
}
```

使用谓词排序列表：

```cpp
linkInts.sort (SortPredicate_Descending);
```

这两个变体在列表 18.6 中进行了演示。

**列表 18.6** 排序列表中的整数

```cpp
0: #include <list>
1: #include <iostream>
2: using namespace std;
3:
4: bool SortPredicate_Descending (const int& lhs, const int& rhs)
5: {
6:     // list::sort 的标准：对于期望的顺序返回 true
7:     return (lhs > rhs);
8: }
9:
10: template <typename T>
11: void DisplayContents(const T& container)
12: {
13:     for (auto element = container.cbegin();
14:             element != container.cend();
15:             ++ element )
16:        cout << *element << ' ';
17:
18:     cout << endl;
19: }
20:
21: int main()
22: {
23:     std::list<int> linkInts{ 0, 1, 2, 3, 4, 5 };
24:
25:     cout << "Initial contents of list:" << endl;
26:     DisplayContents(linkInts);
27:
28:     linkInts.reverse();
29:
30:     cout << "Contents of list after using reverse():" << endl;
31:     DisplayContents(linkInts);
32:
33:     linkInts.sort();
34:
35:     cout << "Contents of list after sort():" << endl;
36:     DisplayContents(linkInts);
37:
38:     linkInts.sort(SortPredicate_Descending);
39:
40:     cout << "Contents of list after sort with a predicate:" << endl;
41:     DisplayContents(linkInts);
42:
43:     return 0;
44: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

列表的初始内容：
0 1 2 3 4 5

使用 `sort()` 后列表内容：
0 1 2 3 4 5

使用谓词 `sort()` 后列表内容：
5 4 3 2 1 0

大多数涉及 STL 容器的实际应用很少收集整数；相反，它们收集用户定义的类型，如 `classes`（类）或 `structs`（结构体）。列表 18.7 使用联系人 `list` 的示例演示了这种用法。乍看似乎很长，但大部分都是简单的代码。

### 列表 18.7 类对象列表：创建一个联系人列表

点击此处查看代码图像

```cpp
0: #include <list>
1: #include <string>
2: #include <iostream>
3: using namespace std;
4:
5: template <typename T>
6: void displayAsContents (const T& container)
7: {
8:     for (auto element = container.cbegin();
9:             element != container.cend();
10:               ++ element )
11:       cout << *element << endl;
12:
13:     cout << endl;
14: }
15:
16: struct ContactItem
17: {
18:     string name;
19:     string phone;
20:     string displayAs;
21:
22:     ContactItem (const string& conName, const string & conNum)
23:     {
24:         name = conName;
25:         phone = conNum;
26:         displayAs = (name + ": " + phone);
27:     }
28:
29:     // 用于给定联系人列表项的 list::remove()
30:     bool operator == (const ContactItem& itemToCompare) const
31:     {
```




```cpp
32:         return (itemToCompare.name == this->name);
33:
34:     }
35:
36:     // 用于无带参数的 list::sort()
37:     bool operator < (const ContactItem& itemToCompare) const
38:     {
39:         return (this->name < itemToCompare.name);
40:     }
41:
42:     // 通过 cout 在 displayAsContents 中
43:     operator const char*() const
44:     {
45:         return displayAs.c_str();
46:     }
47: };
48:
49: bool SortOnphoneNumber (const ContactItem& item1,
50:                                     const ContactItem& item2)
51: {
52:     return (item1.phone < item2.phone);
53: }
54:
55: int main ()
56: {
57:     list <ContactItem> contacts;
58:     contacts.push_back(ContactItem("Jack Welsch", "+1 7889879879"));
59:     contacts.push_back(ContactItem("Bill Gates", "+1 97789787998"));
60:     contacts.push_back(ContactItem("Angi Merkel", "+49 234565466"));
61:     contacts.push_back(ContactItem("Vlad Putin", "+7 6645456497"));
62:     contacts.push_back(ContactItem("Ben Affleck", "+1 745641314"));
63:     contacts.push_back(ContactItem("Dan Craig", "+44 12361976"));
64:
65:     cout << "List in initial order: " << endl;
66:     displayAsContents(contacts);
67:
68:     contacts.sort();
69:     cout << "Sorting in alphabetical order via operator<:" << endl;
70:     displayAsContents(contacts);
71:
72:     contacts.sort(SortOnphoneNumber);
73:     cout << "Sorting in order of phone numbers via predicate:" << endl;
74:     displayAsContents(contacts);
75:
76:     cout << "Erasing Putin from the list: " << endl;
77:     contacts.remove(ContactItem("Vlad Putin"));
78:     displayAsContents(contacts);
79:
80:     return 0;
81: }
```

* * *

## 输出

![Image](img/arrow.jpg)

点击此处查看代码图像。

### 初始顺序列表

```text
Jack Welsch: +1 7889879879
Bill Gates: +1 97789787998
Angi Merkel: +49 234565466
Vlad Putin: +7 6645456497
Ben Affleck: +1 745641314
Dan Craig: +44 12361976
```

### 通过 `operator<` 按字母顺序排序

```text
Angi Merkel: +49 234565466
Ben Affleck: +1 745641314
Bill Gates: +1 97789787998
Dan Craig: +44 12361976
Jack Welsch: +1 7889879879
Vlad Putin: +7 6645456497
```

### 通过谓词按电话号码排序

```text
Angi Merkel: +49 234565466
Ben Affleck: +1 745641314
Bill Gates: +1 97789787998
Dan Craig: +44 12361976
Jack Welsch: +1 7889879879
Vlad Putin: +7 6645456497
```

### 从列表中删除 Putin

如示例所示，`forward_list` 在功能上与 `list` 类似。由于 `forward_list` 不支持双向迭代，你可以在迭代器上使用 `operator++`，但不能使用 `operator--`。此示例演示了第 23 行中函数 `remove(2)` 的用法，用于删除所有值为 2 的元素。第 29 行演示了使用 `sort()`，它使用了使用 `std::less<T>` 的默认排序谓词。

`forward_list` 的优势在于由于它是单向链表，其内存消耗略低于 `list`（因为元素只需要知道下一个元素，而不需要上一个元素）。

## DO

- **应当**在频繁插入或删除元素（特别是在中间）时，选择 `std::list` 而不是 `std::vector`——`vector` 需要调整其内部缓冲区以允许数组语义，并会导致昂贵的拷贝操作，而 `list` 只需要连接或断开元素。
- **应当**记住，你可以使用 `push_front()` 或 `push_back()` 成员方法分别在列表的开头或结尾插入元素。
- **应当**记住，对于要在如 `list` 等 STL 容器中类的类，要编写 `operator<` 和 `operator==`，以提供默认的排序或删除谓词。
- **应当**记住，你可以像任何其他 STL 容器类一样，使用 `list::size()` 方法确定 `list` 中的元素数量。
- **应当**记住，你可以像任何其他 STL 容器类一样，使用 `list::clear()` 方法清空 `list`。

## DON’T

- **不要**在仅在末端有频繁插入或删除且中间没有插入或删除的情况下使用列表；在这些情况下，`vector` 或 `deque` 的速度会快得多。
- **不要**忘记在想要列表使用非默认标准进行 `sort()` 或 `remove()` 时，提供一个谓词函数。

## Summary

本节课程教你了 `list` 的属性以及不同的 `list` 操作。你现在了解了一些最实用的 `list` 函数，并可以创建任何对象类型的 `list`。

## Q&A

**Q：为什么 `list` 提供了 `sort()` 和 `remove()` 等成员函数？**

**A：** STL `list` 类被要求遵守这样一个属性：指向 `list` 中元素的迭代器无论元素在 `list` 自身的位置如何都应该保持有效。尽管 STL 算法也可以作用于 `list`，但 `list` 的成员函数确保了上述 `list` 属性得以维持，使得在排序之前指向 `list` 元素的迭代器在排序后仍然指向相同的元素。

**Q：你正在使用一个类型为 `CAnimal` 的类对象列表。为了让列表成员函数能够准确地处理它，`CAnimal` 应该定义哪些运算符？**

**A：** 你必须为任何可用于 STL 容器的类提供默认的比较运算符 `==` 和默认的 `<` 运算符。

**Q：如何在以下行中将关键字 `auto` 替换为显式类型声明：**

点击此处查看代码图片。

```cpp
list<int> linkInts(10);  // 10 个整数的列表

auto firstElement = linkInts.begin();
```

**A：** 你可以用以下显式类型声明替换 `auto`：

点击此处查看代码图片。

```cpp
list<int> linkInts(10);  // 10 个整数的列表

list<int>::iterator firstElement = linkInts.begin();
```

## Workshop

工作坊包含测试题，帮助巩固你对所涵盖内容的理解，并提供练习以获得使用所知识的机会。在检查附录 E 中的答案之前，尝试回答测试题和练习题，并确保在进入下一节之前理解了答案。

### Quiz

1. 与在开头或结尾相比，在 STL `list` 中间插入项会有性能损失吗？
2. 两个迭代器指向 STL `list` 对象中的两个元素，然后在它们之间插入了一个元素。这些迭代器会因为插入操作而失效吗？
3. 如何清空 `std::list` 的内容？
4. 可能在 `list` 中插入多个元素吗？

### Exercises

1. 编写一个短程序，接受用户输入的数字并插入到 `list` 的顶部。
2. 使用一个短程序演示：指向 `list` 中元素的迭代器在在其之前插入了另一个元素后，仍然保持有效，从而改变了原元素的相对位置。
3. 编写一个程序，使用 `list` 的 `insert()` 函数将 `vector` 的内容插入 STL `list` 中。
4. 编写一个对字符串列表 `list` 进行排序的程序。

如果你需要一个可以修改值或调用非 `const` 函数的迭代器，你应该使用 `iterator` 而不是 `const_iterator`。

鉴于 `set` 和 `multiset` 都是在插入时对元素排序的容器，当你不提供排序标准时，它们会使用默认谓词 `std::less`。这确保了你的集合包含按升序排列的元素。

你可以通过定义一个带有 `operator()` 的类来创建一个二元排序谓词，该运算符接收两个类型与集合中包含类型相同的值作为输入，并根据你的标准返回 `true`。其中一种用于按降序排序的排序谓词如下：

点击此处查看代码图像。

```cpp
// used as a template parameter in set / multiset instantiation

template <typename T>
struct SortDescending
{
    bool operator()(const T& lhs, const T& rhs) const
    {
        return (lhs > rhs);
    }
};
```

然后你按照如下方式在实例化 `set` 或 `multiset` 时提供此谓词：

点击此处查看代码图像。

```cpp
// a set and multiset of integers (using sort predicate)

set <int, SortDescending<int>> setInts;
multiset <int, SortDescending<int>> msetInts;
```

除了这些变体外，你始终可以创建一个从另一个容器拷贝或通过提供的范围拷贝的 `set` 或 `multiset`，如列表 19.1 所示。

**列表 19.1** `set` 和 `multiset` 的不同实例化技术

点击此处查看代码图像。

```cpp
0: #include <set>
1:
2: // used as a template parameter in set / multiset instantiation
3: template <typename T>
4: struct SortDescending
5: {
6:     bool operator()(const T& lhs, const T& rhs) const
7:     {
8:         return (lhs > rhs);
9:     }
10: };
11:
12: int main ()
13: {
14:     using namespace std;
15:
16:     // a simple set or multiset of integers (using default sort predicate)
17:     set<int> setInts1;
18:     multiset<int> msetInts1;
19:
20:     // set and multiset instantiated given a user-defined sort predicate
21:     set<int, SortDescending<int>> setInts2;
22:     multiset<int, SortDescending<int>> msetInts2;
23:
24:     // creating one set from another, or part of another container
25:     set<int> setInts3(setInts1);
26:     multiset<int> msetInts3(setInts1.cbegin(), setInts1.cend());
27:
28:     return 0;
29: }
```

分析：此程序没有输出，但展示了 `set` 和 `multiset` 的各种实例化技术，专门用于包含类型 `int`。在第 17 行和第 18 行中，你看到了简单的形式，除类型以外的模板参数被忽略了，导致使用了默认排序谓词，如 `struct`（或 `class`）`std::less<T>` 中实现的。如果你想覆盖默认排序，需要指定一个像第 3-10 行定义并在 `main()` 中第 21 行和第 22 行使用的样的谓词。该谓词确保排序是降序的（默认是升序）。最后，第 25 行和第 26 行展示了实例化技术，其中一个 `set` 是另一个的拷贝，而 `multiset` 则从从 `set` 获取的值范围进行实例化（但也可以是 `vector` 或 `list` 或任何通过 `cbegin()` 和 `cend()` 返回描述边界的迭代器的 STL 容器类）。

### 在 `set` 或 `multiset` 中插入元素

`set` 和 `multiset` 中的大多数函数的工作方式相似。它们接受相似的参数并返回相似的值类型。例如，在这类容器中插入元素可以使用成员函数 `insert()` 完成，它接受要插入的值或从另一个容器获取的范围：

点击此处查看代码图像。

```cpp
setInts.insert (-1);

msetInts.insert (setInts.begin (), setInts.end()));
```

列表 19.2 展示了这些容器中的元素。

**列表 19.2** 在 STL `set` 和 `multiset` 中插入元素

点击此处查看代码图像。

```cpp
0: #include <set>
1: #include <iostream>
2: using namespace std;
3:
4: template <typename T>
5: void DisplayContents(const T& container)
6: {
7:     for (auto element = container.cbegin();
8:         element != container.cend();
9:         ++element)
10:     cout << *element << ' ';
11:
12:     cout << endl;
13:
14: int main ()
15: {
16:     using namespace std;
17:
18:     // a simple set or multiset of integers (using default sort predicate)
19:     set<int> setInts1;
20:     multiset<int> msetInts1;
21:
22:     // set and multiset instantiated given a user-defined sort predicate
23:     set<int, SortDescending<int>> setInts2;
24:     multiset<int, SortDescending<int>> msetInts2;
25:
26:     // creating one set from another, or part of another container
27:     set<int> setInts3(setInts1);
28:     multiset<int> msetInts3(setInts1.cbegin(), setInts1.cend());
29:
30:     return 0;
31: }
```



（注：此处提供的示例原文代码块与翻译文本略有出入，已根据要求仅翻译文本部分并保持代码块不变）

分析：此程序没有输出，但展示了 `set` 和 `multiset` 的各种实例化技术，专门用于包含类型 `int`。在第 17 行和第 18 行中，你看到了简单的形式，除类型以外的模板参数被忽略了，导致使用了默认排序谓词，如 `struct`（或 `class`）`std::less<T>` 中实现的。如果你想覆盖默认排序，需要指定一个像第 3-10 行定义并在 `main()` 中第 21 行和第 22 行使用的谓词。该谓词确保了排序是降序的（默认是升序）。最后，第 25 行和第 26 行展示了实例化技术，其中一个 `set` 是另一个的拷贝，而 `multiset` 则从从 `set` 获取的值范围进行实例化（但也可以是 `vector` 或 `list` 或任何通过 `cbegin()` 和 `cend()` 返回描述边界的迭代器的 STL 容器类）。

### 在 STL `set` 或 `multiset` 中查找元素

`set` 和 `multiset` 或 `map` 和 `multimap` 等关联容器具有 `find()` 函数——一个允许你根据键来查找值的成员函数：

点击此处查看代码图像

```cpp
auto elementFound = setInts.find (-1);

// Check if found...

if (elementFound = setInts.end ())

    cout << "Element " << *elementFound << " found!" << endl;

else

    cout << "Element not found in set!" << endl;
```

`find()` 的用法在列表 19.3 中演示。对于允许多个元素的 `multiset`，该函数会找到第一个与提供的键匹配的值。

**列表 19.3** 使用 `find` 成员函数

点击此处查看代码图像

```cpp
0: #include <set>

1: #include <iostream>

2: using namespace std;

3:

4: int main ()

5: {

6:     set<int> setInts{ 43, 78, -1, 124 };

7:

8:     // Display contents of the set to the screen

9:     for (auto element = setInts.cbegin();

10:         element != setInts.cend ();

11:         ++element )

12:     cout << *element << endl;

13:

14:     // Try finding an element

15:     auto elementFound = setInts.find (-1);

16:

17:     // Check if found...

18:     if (elementFound = setInts.end ())

19:         cout << "Element " << *elementFound << " found!" << endl;

20:     else

21:         cout << "Element not found in set!" << endl;

22: }
```

```cpp
// 查找另一个

auto anotherFind = setInts.find (12345);

// 检查是否找到...

if (anotherFind = setInts.end ())

    cout << "Element " << *anotherFind << " found!" << endl;

else

    cout << "Element 12345 not found in set!" << endl;

return 0;

}
```

***

Output ![Image](img/arrow.jpg)

点击此处查看代码

-1
43
78
124

Element -1 found!

Element 12345 not found in set!

### 分析

分析 ![Image](img/arrow.jpg)

第 15–21 行显示了 `find()` 成员函数的用法。`find()` 返回一个迭代器，需要与 `end()` 进行比较（如第 18 行所示），以验证是否找到了该元素。如果迭代器有效，你可以使用 `*elementFound` 访问它所指向的值。

***

### 注意

Listing 19.3 中的示例对于 `multiset` 同样可以工作；也就是说，如果第 6 行是 `multiset` 而不是 `set`，它不会改变程序的工作方式。由于 `multiset` 可能会在连续位置存储多个相同值的元素，你可以使用 `find()` 返回的迭代器并将其推进 `(count() – 1)` 次，以访问该值的所有元素。成员函数 `count()` 已在 Listing 19.2 中演示。

***

### 在 STL `set` 或 `multiset` 中删除元素

关联容器如 `set`、`multiset` 或 `map` 和 `multimap` 具有 `erase()`——这是一个成员函数，允许你根据键（key）删除值：

```cpp
setObject.erase (key);
```

`erase()` 函数的另一种形式允许根据指向该元素的迭代器来删除特定元素：

```cpp
setObject.erase (element);
```

可以使用提供边界的迭代器从 `set` 或 `multiset` 中删除范围内的元素：

点击此处查看代码

```cpp
setObject.erase (iLowerBound, iUpperBound);
```

Listing 19.4 中的示例演示了如何使用 `erase()` 从 `set` 或 `multiset` 中移除元素。

**代码列表 19.4** 在 `multiset` 上使用 `erase` 成员函数

点击此处查看代码

***

```cpp
#include <set>

#include <iostream>

using namespace std;

template <typename T>

void DisplayContents (const T& Input)

{

    for (auto element = Input.cbegin();

             element != Input.cend ();

             ++ element )

        cout << *element << ' ';

    cout << endl;

}

typedef multiset <int> MSETINT;

int main ()

{

    MSETINT msetInts{ 43, 78, 78, -1, 124 };

    cout << "multiset contains " << msetInts.size () << " elements: ";

    DisplayContents(msetInts);

    cout << "Enter a number to erase from the set: ";

    int input = 0;

    cin >> input;

    cout << "Erasing " << msetInts.count (input) << " instances of value " << input << endl;

    msetInts.erase (input);

    cout << "multiset contains " << msetInts.size () << " elements: ";

    DisplayContents(msetInts);

    return 0;

}
```

***

Output ![Image](img/arrow.jpg)

点击此处查看代码

multiset contains 5 elements: -1 43 78 124
Enter a number to erase from the set: 78
Erasing 2 instances of value 78
multiset now contains 3 elements: -1 43 124

分析 ![Image](img/arrow.jpg)

注意第 15 行中 `typedef` 的用法。第 28 行演示了如何使用 `count()` 来获取具有特定值的元素数量。实际的删除操作发生在第 31 行，它删除了所有匹配特定输入的元素。

***

### 提示

成员函数 `erase()` 是重载的。如果像 Listing 19.4 所示用值调用，它将删除所有评估为相同的元素。如果使用迭代器调用（例如由 `find()` 操作的迭代器），它将删除那一个元素，如下：

```cpp
MSETINT::iterator elementFound = msetInts.find(numberToErase);

if (elementFound != msetInts.end ())

    msetInts.erase(elementFound);

else

    cout << "Element not found!" << endl;
```

你也可以使用 `erase()` 删除 `multiset` 中的一个范围的值：

```cpp
MSETINT::iterator elementFound = msetInts.find(numberToErase);

if (elementFound != msetInts.end ())

    msetInts.erase(elementFound);
```

前面的代码段使用 `erase()` 删除 `multiset` 中的一个范围的值：

```cpp
setObject.erase (iLowerBound, iUpperBound);
```

现在你已经熟悉了 `set` 和 `multiset` 的基本函数，是时候回顾一个使用该容器的实际应用了。

**代码列表 19.5** 使用 `set`、`find` 和 `erase` 的电话目录

`ch19_ima.html_ch19list05`

***

```cpp
#include <set>

#include <iostream>

#include <string>

using namespace std;

struct ContactItem

{

    string name;

    string phoneNum;

    ContactItem (const string& nameInit, const string& phone)

    {

        name = nameInit;

        phoneNum = phone;

        displayAs = name + ": " + phoneNum;

    }

    // 用于排序

    bool operator < (const ContactItem& itemToCompare)

    {

        return this->name < itemToCompare.name;

    }

    // 用于 find

    bool operator == (const ContactItem& itemToCompare)

    {

        return this->name == itemToCompare.name;

    }

    // 用于 cout

    operator char*() const

    {

        return displayAs.c_str();

    }

private:

    string displayAs;

};

template <typename T>

void DisplayContents (const T& container)

{

    for (auto element = container.cbegin();

             element != container.cend();

             ++ element )

        cout << *element << endl;

    cout << endl;

}

int main ()

{

    set<ContactItem> setContacts;

    setContacts.insert(ContactItem("Jack Welsch", "+1 7889 879"));

    setContacts.insert(ContactItem("Bill Gates", "+1 97 7897 879 8"));

    setContacts.insert(ContactItem("Angi Merkel", "+49 23456 5466"));

    setContacts.insert(ContactItem("Vlad Putin", "+7 6645 4564 79"));

    setContacts.insert(ContactItem("John Travolta", "91 234 4564 78"));

    DisplayContents(setContacts);

    cout << "Enter a name you wish to delete: ";

    string inputName;

    getline(cin, inputName);

    auto contactFound = setContacts.find(ContactItem(inputName, ""));

    if(contactFound != setContacts.end())

    {

        setContacts.erase(contactFound);

        cout << "Displaying contents after erasing " << inputName << endl;

        DisplayContents(setContacts);

    }

    else

        cout << "Contact not found" << endl;

    return 0;

}
```



```text
John Travolta: 91 234 4564 789

Vlad Putin: +7 6645 4564 797

输入你想删除的名称：John Travolta

显示删除 John Travolta 后的内容

Angi Merkel: +49 23456 5466

Ben Affleck: +1 745 641 314

Bill Gates: +1 97 7897 8799 8

Jack Welsch: +1 7889 879 879

Vlad Putin: +7 6645 4564 797
```

分析 ![Image](img/arrow.jpg)

这与列表 18.7 类似，该列表按字母顺序排序了 `std::list`，区别在于在 `std::set` 的情况下，排序是在插入时发生的。如输出所示，你不需要调用任何函数来确保 `set` 中的元素是有序的，因为它们在插入时已经使用你在 36–39 行中实现的 `operator<` 完成了排序。你赋予了用户删除条目的选择，第 63 行演示了如何调用 `find()` 来定位该条目，并在第 66 行使用 `erase()` 将其删除。

---

**提示**

> 此电话目录的实现基于 STL `set`，因此不允许包含多个相同值的条目。如果你需要你的电话目录实现允许存储两个同名的人，你应该选择 STL 的 `multiset`。如果 `setContacts` 是一个 `multiset`，之前的代码仍然可以正常工作。为了进一步利用 `multiset` 存储多个相同值条目的能力，你可以使用 `count()` 成员函数来获取持有特定值的数量。

---

### 使用 STL `set` 和 `multiset` 的优缺点

STL `set` 和 `multiset` 在需要频繁查找的应用程序具有显著优势，因为它们的内容是有序的，因此定位速度更快。然而，为了提供这种优势，容器需要在插入时对元素进行排序。因此，插入元素时会有开销，因为元素是经过排序的——如果你经常使用 `find()` 等功能和函数，这种开销可能是值得的折中。

`find()` 利用了内部二叉树结构。这种有序的二叉树结构导致了相对于 `vector` 等顺序容器的另一个隐式劣势。在 `vector` 中，迭代器指向的元素（例如由 `std::find()` 操作返回的元素）可以被新值覆盖。但在 `set` 中，元素由 `set` 类根据其各自的值进行排序，因此绝不应该使用迭代器覆盖元素，即使这在程序上是可行的。

### STL 哈希集合（Hash Set）实现 `std::unordered_set` 和 `std::unordered_multiset`

STL `std::set` 和 STL `std::multiset` 根据 `std::less<T>` 或提供的谓词对元素（同时也是键）进行排序。在有序容器中搜索比在 `vector` 等未排序容器中搜索更快，且 `std::sort()` 提供了对数复杂度。这意味着在 `set` 中查找元素所花费的时间与 `set` 中的元素数量并不成正比，而是与其对对数（LOG）。因此，平均而言，在包含 10,000 个元素的 `set` 中搜索的时间是在包含 100 个元素的 `set` 中的两倍（因为 $100² = 10000$，或 $log(10000) = 2 \times log(100)$）。

然而，相对于未排序容器（搜索与元素数量成正比）这种性能的巨大提升有时是不够的。程序员和数学家都追求常数时间的插入和排序可能性，其中一种方法使用了基于哈希的实现，使用哈希函数来确定排序索引。插入到哈希集合中的元素首先由哈希函数评估生成一个唯一索引，该索引就是它们被放置的*桶*（bucket）索引。

STL 自 C++11 起提供的哈希集合变体是容器类 `std::unordered_set`。

---

**提示**

> 要使用 STL 容器 `std::unordered_set` 或 `std::unordered_multiset`，请包含：

```cpp
#include <unordered_set>
```

---

该类的用法与 `std::set` 相比变化不大：

点击此处查看代码：

```cpp
// 实例化:
unordered_set<int> usetInt;

// 插入元素
usetInt.insert(1000);

// find():
auto elementFound = usetInt.find(1000);

if (elementFound != usetInt.end())
    cout << *elementFound << endl;
```

然而，`unordered_set` 的一个非常重要的特性是提供了负责决定排序的哈希函数：

点击此处查看代码：

```cpp
unordered_set<int>::hasher HFn = usetInt.hash_function();
```

使用 `std::unordered_set` 还是 `std::set` 的决定最好是在涉及真实世界用法的操作和数据量的模拟中测量了相应容器的性能后做出的。列表 19.6 演示了 `std::hash_set` 的一些常用方法的用法。

**列表 19.6 `std::unordered_set` 以及 `insert()`、`find()`、`size()`、`max_bucket_count()` 和 `load_factor()` 的用法**

点击此处查看代码

---

```cpp
#include <unordered_set>

#include <iostream>

using namespace std;

template <typename T>
void DisplayContents(const T& cont) {
    cout << "Unordered set contains: ";

    for (auto element = cont.cbegin(); element != cont.cend(); ++element)
        cout << *element << ' ';

    cout << endl;
    cout << "Number of elements, size() = " << cont.size() << endl;
    cout << "Bucket count = " << cont.bucket_count() << endl;
    cout << "Max load factor = " << cont.max_load_factor() << endl;
    cout << "Load factor: " << cont.load_factor() << endl;
}

int main() {
    unordered_set<int> usetInt{ 1, -3, 2017, 300, -1, 989, -300 };

    DisplayContents(usetInt);

    usetInt.insert(999);
    DisplayContents(usetInt);

    cout << "Enter int you want to check for existence in set: ";

    int input = 0;
    cin >> input;

    auto elementFound = usetInt.find(input);

    if (elementFound != usetInt.end())
        cout << *elementFound << " found in set" << endl;
    else
        cout << input << " not available in set" << endl;

    return 0;
}
```

---

**输出** ![Image](img/arrow.jpg)

点击此处查看代码：

```text
Unordered set contains: 9 1 -3 989 -1 2017 300 -300
Number of elements, size() = 8
Bucket count = 8
Max load factor = 1
Load factor: 1
Unordered set contains: 9 1 -3 989 -1 2017 300 -300 999
Number of elements, size() = 9
Bucket count = 64
Max load factor = 1
Load factor: 0.140625
Enter int you want to check for existence in set: -300
-300 found in set
```

分析 ![Image](img/arrow.jpg)

该示例创建了一个整数类型的 `unordered_set`；在第 23 行使用列表初始化插入值；然后显示内容，包括由 `max_bucket_count()`、`load_factor()` 和 `max_load_factor()` 方法提供的统计数据，如第 15–18 行所示。输出显示桶的数量初始为八，容器中有八个元素，导致负载因子为 1，这与最大负载因子相同。当插入第九个元素到 `unordered_set` 时，它会重新组织，创建 64 个桶并重建哈希表，负载因子随之降低。`main` 函数剩余的代码演示了在 `unordered_set` 中查找元素的语法与 `set` 相似。`find()` 返回一个迭代器，在使用它之前，需要如第 33 行所示检查 `find()` 是否成功。

由于哈希通常用于在哈希表中根据键查找值，请参阅第 20 节中关于 `std::unordered_map` 的节，“STL Map 类](#ch20.html_ch20)。”

`std::unordered_map` 是 C++11 新的哈希表实现。

---

## 要（DO）

**请记住** STL `set` 和 `multiset` 容器针对频繁搜索的情况进行了优化。

**请记住** `std::multiset` 允许多个相同的元素（键），而 `std::set` 仅允许唯一值。

**请使用** `multiset::count(value)` 来查找特定值 `value` 的元素个数。

**请记住** `set::size()` 或 `multiset::size()` 返回的是容器中元素的数量。

---

## 不要（DON’T）

**不要忘记**为可以收纳在 `set` 或 `multiset` 等容器中的类编写 `operator<` 和 `operator==`。前者作为排序谓词，而后者用于 `set::find()` 等函数。

**不要**在频繁插入和低频率搜索的场景下使用 `std::set` 或 `std::multiset`。`std::vector` 或 `std::list` 通常更适合此类情况。

---

## 总结

在本节中，你学习了如何使用 STL `set` 和 `multiset`、它们重要的成员函数以及它们的特性。你还看到了它们在编写简单的基于菜单的电话录中的应用，该电话录还包含搜索和删除功能。

## 问答（Q&A）

**问：如何声明一个按降序排序并存储的整数集合？**

**答：** `set<int>` 是一个整数 `set`。它使用默认的排序谓词 `std::less<T>` 按升序顺序排序项，也可以表示为 `set<int, less<int>>`。若要按降序排序，请将 `set` 定义为 `set<int, greater<int>>`。

**问：如果我在字符串集合中插入两次字符串 "Jack"，会发生什么？**

**答：** `set` 的设计目的不是用于包含非唯一值。该字符串集合将只包含一个 `"Jack"`。

**问：在前面的示例中，如果我想有两个 "Jack" 实例，我应该修改什么？**

**答：** 根据设计，`set` 只持有唯一值。你需要将选择的容器改为 `multiset`。

**问：哪一个 multiset 成员函数返回容器中特定值的计数？**

**答：** `count(value)` 是我们感兴趣的函数。

**问：我使用 `find()` 函数在集合中找到了一个元素并获得了一个指向它的迭代器。我会使用这个迭代器来更改所指向的值吗？**

**答：** 不会。某些 STL 实现可能允许用户通过例如 `find` 返回的迭代器来更改 `set` 内部元素的值。然而，这不是正确的做法。指向 `set` 中元素的迭代器应该作为 `const` 迭代器使用——即使 STL 实现没有强制要求这样做。

## 工作坊（Workshop）

工作坊包含测验题，以帮助你巩固对所涵盖内容的理解，并提供练习让你获得使用所学知识的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，并确保在进入下一节之前理解了答案。

### 测验

**1.** 你声明一个整数 `set` 为 `set<int>`。哪一个函数提供了排序标准？

**2.** 你会在 `multiset` 的哪里找到重复元素？

**3.** 哪一个 `set` 或 `multiset` 函数提供了容器中的元素数量？

### 练习题

**1.** 扩展本节中的电话录示例，以便根据电话号码查找人的姓名。（提示：调整运算符 `<` 和 `==`，并确保项根据电话号码进行排序和比较。）

**2.** 定义一个 `multiset` 来存储输入的单词及其含义；即，让 `multiset` 像字典一样工作。（提示：`multiset` 应该是包含两个字符串的结构之一：单词及其含义。）

**3.** 通过简单的程序演示 `set` 不能接受重复条目，而 `multiset` 可以。

## 第 20 节：STL Map 类

标准模板库（STL）为程序员提供了容器类，有助于需要频繁且快速搜索的应用。

本节涵盖：

- ![Image](img/square.jpg) 如何使用 STL `map` 和 `multimap`、`unordered_map` 以及 `unordered_multimap` 容器来对你有帮助
- ![Image](img/square.jpg) 元素的插入、删除和搜索
- ![Image](img/square.jpg) 插入自定义谓词

### STL 类简介

`map` 和 `multimap` 是键值对容器，允许如图 20.1 所示的查找。

![Image](img/square.jpg) **图 20.1** 持键值的容器

`map` 和 `multimap` 的区别在于后者允许重复，而前者允许唯一键。为了便于快速搜索，`map` 和 `multimap` 的 STL 实现类似于二叉树。这意味着与 `vector` 中位置可以被替换不同，`map` 中的元素是有排序的。

使用类 `std::map` 或 `std::multimap` 需要包含：

```cpp
#include <map>
```

### `std::map` 和 `std::multimap` 操作

STL `map` 和 `multimap` 是模板类，在使用任何函数之前需要实例化。

#### 实例化 `std::map` 或 `std::multimap`

实例化整数作为键、字符串作为值的 `map` 或 `multimap` 需要模板的特化。`map` 的模板实例化需要程序员指定键类型、值类型，以及可选的帮助 `map` 类在插入时排序的谓词。因此，典型的 `map` 语法如下：

```cpp
map<keyType, valueType, Predicate=std::less<keyType>> mapObj;
```

因此，第三模板参数是可选的。当你只提供键类型和值类型而忽略第三模板参数时，`std::map` 和 `std::multimap` 默认使用 `class std::less<>` 来定义排序标准。因此，一个映射整数到字符串的 `map` 或 `multimap` 如下：

```cpp
std::map<int, string> mapIntToStr;

std::multimap<int, string> mmapIntToStr;
```

列表 20.1 详细说明了实例化技术。

**列表 20.1** 实例化映射 `int` 键到 `string` 的 `map` 和 `multimap` 对象

```cpp
#include <map>
#include <string>

template<typename keyType>
struct ReverseSort
{
    bool operator()(const keyType& key1, const keyType& key2)
    {
        return (key1 > key2);
    }
};
```

```cpp
// map and multimap key of type int to value of type string
map<int, string> mapIntToStr1;
multimap<int, string> mmapIntToStr1;

// map and multimap constructed as a copy of another
map<int, string> mapIntToStr2(mapIntToStr1);
multimap<int, string> mmapIntToStr2(mmapIntToStr1);

// map and multimap constructed given a part of another map or multimap
map<int, string> mapIntToStr3(mapIntToStr1.cbegin(), mapIntToStr1.cend());
```



```cpp
multimap<int, string> mmapIntToStr3(mmapIntToStr1.cbegin(), mmapIntToStr1.cend());

// map and multimap with a predicate that inverses sort order

map<int, string, ReverseSort<int>> mapIntToStr4(mapIntToStr1.cbegin(), mapIntToStr1.cend());

multimap<int, string, ReverseSort<int>> mmapIntToStr4(mapIntToStr1.cbegin(), mapIntToStr1.cend());

return 0;

}
```

## 分析 ![Image](img/arrow.jpg)

首先，关注第 12–39 行的`main()`。最简单的从整数键到字符串值的`map`和`multimap`可以在第 17 和 18 行看到。第 25–28 行演示了如何以另一个容器的值范围作为输入初始化`map`或`multimap`。第 31–36 行演示了如何使用自定义的排序准则实例化`map`或`multimap`。

注意，默认排序（在之前的实例化中）使用`std::less<T>`，它会按升序顺序排列元素。如果你想更改这种行为，可以提供一个实现了`operator()`的`class`或`struct`作为谓词。这种谓词结构体`struct ReverseSort`位于第 3–10 行，并已用于第 32 行`map`的实例化和第 35 行`multimap`的实例化。

### 在 STL `map` 或 `multimap` 中插入元素

`map`和`multimap`中的大多数函数工作方式相似。它们接受相似的参数并返回相似的值类型。你可以通过使用`insert`成员函数向两种容器插入元素：

点击此处查看代码图像

```cpp
std::map<int, std::string> mapIntToStr1;

// 使用 make_pair 函数插入键值对

mapIntToStr.insert(make_pair(-1, "Minus One"));
```

由于这两个容器以键值对的形式维护元素，你也可以直接提供一个初始化为要插入的键值的`std::pair`：

点击此处查看代码图像

```cpp
mapIntToStr.insert(pair<int, string>(1000, "One Thousand"));
```

或者，你可以使用类似数组的语法进行插入，这看起来非常用户友好，并且通过下标运算符`operator[]`支持：

点击此处查看代码图像

```cpp
mapIntToStr[1000000] = "One Million";
```

你还可以将`multimap`实例化为`map`的拷贝：

点击此处查看代码图像

```cpp
std::multimap<int, std::string> mmapIntToStr(mapIntToStr.cbegin(), mapIntToStr.cend());
```

列表 20.2 演示了各种实例化方法。

#### 列表 20.2 使用 `insert()` 的重载和通过 `operator[]` 的数组语义在 `map` 和 `multimap` 中插入元素

点击此处查看代码图像

```cpp
#include <map>
#include <iostream>
#include <string>

using namespace std;

// 定义 map 和 multimap 以提高可读性

typedef map<int, string> MAP_INT_STRING;
typedef multimap<int, string> MMAP_INT_STRING;

template <typename T>
void DisplayContents(const T& cont)
{
    for (auto element = cont.cbegin(); element != cont.cend(); ++element)
    {
        cout << element->first << " -> " << element->second << endl;
    }

    cout << endl;
}

int main()
{
    MAP_INT_STRING mapIntToStr;

    // 使用 value_type 向 map 插入键值对
    mapIntToStr.insert(MAP_INT_STRING::value_type(3, "Three"));

    // 使用 make_pair 插入值对
    mapIntToStr.insert(make_pair(-1, "Minus One"));

    // 直接插入值对对象
    mapIntToStr.insert(pair<int, string>(1000, "One Thousand"));

    // 使用类似数组的语法插入键值对
    mapIntToStr[1000000] = "One Million";

    cout << "map 包含 " << mapIntToStr.size() << " 个键值对。它们是：" << endl;

    DisplayContents(mapIntToStr);

    // 实例化一个作为 map 拷贝的 multimap
    MMAP_INT_STRING mmapIntToStr(mapIntToStr.cbegin(), mapIntToStr.cend());

    // insert 函数对 multimap 的工作方式也相同

    // multimap 可以存储重复项 - 插入一个重复项
    mmapIntToStr.insert(make_pair(1000, "Thousand"));

    cout << endl << "multimap 包含 " << mmapIntToStr.size()
         << " 个键值对。它们是：" << endl;
}
```

```cpp
cout << pairFound->second << endl;
}
else
    cout << "Sorry, pair with key " << key << " not in map" << endl;
```

---

### 提示

如果你使用的是符合 C++11 标准的编译器，迭代器的声明可以使用关键字`auto`来简化：

点击此处查看代码图像

```cpp
auto pairFound = mapIntToStr.find(key);
```

编译器通过从`map::find()`声明的返回值自动推断出迭代器的类型。

---

列表 20.3 中的示例演示了`multimap::find()`的用法。

**列表 20.3** 使用`find()`成员函数在`map`中定位键值对

点击此处查看代码图像

```cpp
0: #include <map>
1: #include <iostream>
2: #include <string>
3: using namespace std;
4:
5: template <typename T>
6: void DisplayContents(const T& cont)
7: {
8:     for (auto element = cont.cbegin();
9:             element != cont.cend();
10:             ++element)
11:         cout << element->first << " -> " << element->second << endl;
12:
13:     cout << endl;
14: }
15:
16: int main()
17: {
18:     map<int, string> mapIntToStr;
19:
20:     mapIntToStr.insert(make_pair(3, "Three"));
21:     mapIntToStr.insert(make_pair(45, "Forty Five"));
22:     mapIntToStr.insert(make_pair(-1, "Minus One"));
23:     mapIntToStr.insert(make_pair(1000, "Thousand"));
24:
25:     cout << "The multimap contains " << mapIntToStr.size();
26:     cout << " key-value pairs. They are: " << endl;
27:
28:     // Print the contents of the map to the screen
29:     DisplayContents(mapIntToStr);
30:
31:     cout << "Enter the key you wish to find: ";
32:     int key = 0;
33:     cin >> key;
34:
35:     auto pairFound = mapIntToStr.find(key);
36:     if (pairFound != mapIntToStr.end())
37:     {
38:         cout << "Key " << pairFound->first << " points to Value: ";
39:         cout << pairFound->second << endl;
40:     }
41:     else
42:         cout << "Sorry, pair with key " << key << " not in map" << endl;
43:
44:     return 0;
45: }
```

---

## 输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

The multimap contains 4 key-value pairs. They are:

-1 -> Minus One  
3 -> Three  
45 -> Forty Five  
1000 -> Thousand

Enter the key you wish to find: 45

Key 45 points to Value: Forty Five

接下来，运行（此时`find()`将未找到匹配的键）：

点击此处查看代码图像

The multimap contains 4 key-value pairs. They are:

-1 -> Minus One  
3 -> Three  
45 -> Forty Five  
1000 -> Thousand

Enter the key you wish to find: 45

Sorry, pair with key 45 not in map

## 分析 ![Image](img/arrow.jpg)

`main()`中的第 20–23 行用示例键值对填充了`map`，每个对都将一个整数映射到一个字符串。当用户提供一个要在`map`中查找的键时，第 35 行使用`find()`函数在`map`中查找该键。`map::find()`总是返回一个迭代器，通过将此迭代器与`end()`比较来检查`find()`操作是否成功总是明智的，如第 36 行所示。

如果迭代器确实有效，则使用`second`访问值，如第 39 行所示。在第二次运行中，你输入了一个`map`中不存在的键 45，系统会显示错误信息。

---

### 注意

永远不要在不检查返回的迭代器的情况下直接使用`find()`操作的结果。

### 在 STL `multimap` 中查找元素

如果列表 20.3 是一个`multimap`，由于容器可能包含多个具有相同键的键值对，你需要找到与重复键对应的所有值。因此，在`multiset`的情况下，你会使用`multiset::count()`来查找与键对应的值数量，并递增迭代器以访问这些存储的值。

点击此处查看代码图像

```cpp
auto pairFound = mapIntToStr.find(key);

// 检查 find() 是否成功
if (pairFound != mapIntToStr.end())
{
    // 查找具有相同键的键值对数量
    size_t numPairsMap = mapIntToStr.count(1000);

    for (size_t counter = 0;
         counter < numPairsMap; // 保持在范围内
         ++counter)
    {
        cout << "Key: " << pairFound->first; // key
        cout << ", Value [" << counter << "] = ";
        cout << pairFound->second << endl; // value
        ++pairFound;
    }
}
else
    cout << "Element not found in the multimap";
```

### 从 STL `map` 或 `multimap` 中删除元素

`map`和`multimap`具有成员函数`erase()`，它可以从容器中删除元素。调用`erase()`时使用键作为参数删除所有具有特定键的键值对：

```cpp
mapObject.erase(key);
```

`erase()`函数的另一种形式允许通过指向特定元素的迭代器进行删除：

```cpp
mapObject.erase(element);
```

可以使用提供边界的迭代器从`map`或`multimap`中删除范围元素：

```cpp
mapObject.erase(lowerBound, upperBound);
```

列表 20.4 演示了`erase()`函数的用法。

**列表 20.4** 从`multimap`中删除元素

multimap 现在包含 1 个键值对。它们是：

3 -> Three

## 分析 ![Image](img/arrow.jpg)

第 21–28 行向`multimap`插入了示例值，其中一些值是重复的（因为与`map`不同，`multimap`支持插入具有重复键的键对）。在将`pair`插入`multimap`之后，代码使用`erase`函数的一个版本来删除项，该版本接受一个键并删除所有具有该键的项（-），如第 35 行所示。

`map::erase(key)`的返回值是被删除的元素个数，并显示在屏幕上。在第 39 行中，你使用`find(45)`返回的迭代器从`map`中删除键为 45 的键对。第 48 行和 49 行演示了如何根据`lower_bound()`和`upper_bound()`指定的范围删除具有特定键的键对。

### 传递自定义排序谓词

`map`和`multimap`模板定义包含第三个参数，该参数接受`map`正确运行所需的排序谓词。当未提供此第三参数时（如前面的示例所示），它会被`std::less<>`提供的默认排序标准取代，它本质上使用`operator <`比较两个对象。

要提供不同于键类型本身支持的排序标准，你通常需要以类或结构体的形式使用`operator()`编写一个二元谓词：

点击此处查看代码图像

```cpp
template<typename keyType>
struct Predicate
{
   bool operator()(const keyType& key1, const keyType& key2)
   {
      // 在此处编写你的排序优先级逻辑
   }
};
```

持有`std::string`类型作为键的`map`默认排序标准基于`std::string`类定义的`operator <`，通过默认排序谓词`std::less<T>`触发，因此它是大小敏感的。对于许多应用程序（例如电话簿），提供一个不区分大小的插入和搜索操作是非常重要的。

解决这一需求的方法之一为`map`提供一个排序谓词，该谓词根据不区分大小的比较返回`true`或`false`：

点击此处查看代码图像

```cpp
map<keyType, valueType, Predicate> mapObject;
```

列表 20.5 详细解释了这一点。

**列表 20.5** 传递自定义排序谓词——电话簿

点击此处查看代码图像

```cpp
0: #include<map>
1: #include<algorithm>
2: #include<string>
3: #include<iostream>
4: using namespace std;
5:
6: template <typename T>
7: void DisplayContents(const T& cont)
8: {
9:     for (auto element = cont.cbegin();
10:             element != cont.cend();
11:             ++element)
```



`multimap` 现在包含 1 个键-值对。它们是：

```text
3 -> Three
```

分析 ![Image](img/arrow.jpg)

第 21–28 行向 `multimap` 插入了示例值，其中一些值是重复的（因为与 `map` 不同，`multimap` 支持插入具有重复键的键对）。在将 `pair` 插入 `multimap` 之后，代码使用 `erase` 函数的一个版本来删除项，该版本接受一个键并删除所有具有该键的项（-），如第 35 行所示。`map::erase(key)` 的返回值是被删除的元素个数，并显示在屏幕上。在第 39 行中，你使用 `find(45)` 返回的迭代器从 `map` 中删除键为 45 的键对。第 48 行和 49 行演示了如何根据 `lower_bound()` 和 `upper_bound()` 指定的范围删除具有特定键的键对。

### 传递自定义排序谓词

`map` 和 `multimap` 模板定义包含第三个参数，该参数接受 `map` 正确运行所需的排序谓词。当未提供此第三参数时（如前面的示例所示），它会被 `std::less<>` 提供的默认排序标准取代，它本质上使用 `operator<` 比较两个对象。

要提供不同于键类型本身支持的排序标准，你通常需要以类或结构体的形式使用 `operator()` 编写一个二元谓词：

点击此处查看代码图像

```cpp
template<typename keyType>
struct Predicate
{
    bool operator()(const keyType& key1, const keyType& key2)
    {
        // 在此处编写你的排序优先级逻辑
    }
};
```

持有 `std::string` 类型作为键的 `map` 默认排序标准基于 `std::string` 类定义的 `operator<`，通过默认排序谓词 `std::less<T>` 触发，因此它是大小敏感的。对于许多应用程序（例如电话簿），提供一个不区分大小的插入和搜索操作是非常重要的。解决这一需求的方法之一为 `map` 提供一个排序谓词，该谓词根据不区分大小的比较返回 `true` 或 `false`：

点击此处查看代码图像

```cpp
map<keyType, valueType, Predicate> mapObject;
```

列表 20.5 详细解释了这一点。

**列表 20.5** 传递自定义排序谓词——电话簿

点击此处查看代码图像

```cpp
#include <map>
#include <algorithm>
#include <string>
#include <iostream>

using namespace std;

template <typename T>
void DisplayContents(const T& cont)
{
    for (auto element = cont.cbegin();
         element != cont.cend();
         ++element)
        cout << element->first << " -> " << element->second << endl;

    cout << endl;
}

struct PredIgnoreCase
{
    bool operator()(const string& str1, const string& str2) const
    {
        string str1NoCase(str1), str2NoCase(str2);

        transform(str1.begin(), str1.end(), str1NoCase.begin(), ::tolower);
        transform(str2.begin(), str2.end(), str2NoCase.begin(), ::tolower);

        return (str1NoCase < str2NoCase);
    }
};

typedef map<string, string> DIR_WITH_CASE;
typedef map<string, string, PredIgnoreCase> DIR_NOCASE;

int main()
{
    // 区分大小的字符串键目录起作用
    DIR_WITH_CASE dirWithCase;

    dirWithCase.insert(make_pair("John", "234567"));
    dirWithCase.insert(make_pair("JOHN", "234567"));
    dirWithCase.insert(make_pair("Sara", "423676"));
    dirWithCase.insert(make_pair("Jack", "324358"));

    cout << "Displaying contents of the case-sensitive map:" << endl;
    DisplayContents(dirWithCase);

    // 不区分大小写的字符串键 map 影响搜索
    DIR_NOCASE dirNoCase(dirWithCase.begin(), dirWithCase.end());

    cout << "Displaying contents of the case-insensitive map:" << endl;
    DisplayContents(dirNoCase);

    // 搜索一个名字
    cout << "Search for a name: ";

    string name;
    cin >> name;

    // 区分大小的 map
    auto it1 = dirWithCase.find(name);

    if (it1 != dirWithCase.end())
        cout << "Found: " << it1->first << " -> " << it1->second << endl;
    else
        cout << "Not found" << endl;

    // 不区分大小的 map
    auto it2 = dirNoCase.find(name);

    if (it2 != dirNoCase.end())
        cout << "Found: " << it2->first << " -> " << it2->second << endl;
    else
        cout << "Not found" << endl;

    return 0;
}
```



一个未排序的 `vector` 在搜索时呈现出线性复杂度，这意味着如果它包含 10,000 个元素而不是 100 个，它的速度将慢 100 倍。

---

因此，虽然对数复杂度看起来已经很不错，但人们应该记住，`map`（或 `multimap`、`set` 或 `multiset`）中的插入也会变慢，因为这些容器在插入时会排序。因此，对更快容器的搜索仍在继续，数学家和程序员都在寻找具有常数时间插入和搜索的容器“圣杯”。哈希表（Hash Table）就是这样一种容器，在给定键的情况下，独立于容器的大小，承诺常数时间的插入和（在大多数情况下）接近常数时间的搜索。

### STL 基于哈希表的键值容器

从 C++11 开始，STL 支持以 `std::unordered_map` 类的形式提供哈希映射。要使用此模板容器类，请包含：

```cpp
#include <unordered_map>
```

`unordered_map` 承诺对容器中任意元素的平均常数时间插入、删除和查找。

#### 哈希表如何工作

虽然详细讨论这个主题不在本书的范围之内（因为这已经是一个过多的博士论文的主题了），但让我们尝试理解让哈希表运行的基本原理。

哈希表可以看是一个键值对的集合，给定一个键，表就能找到一个值。哈希表与简单 `map` 的区别在于，哈希表将键值对存储在桶（buckets）中，每个桶都有一个定义其在表中的相对位置的索引（类似于数组）。该索引由一个使用键作为输入的 `hash-function`（哈希函数）决定：

点击此处查看代码图片

```cpp
Index = HashFunction(key, TableSize);
```

当给定键执行 `find()` 操作时，会再次使用 `HashFunction()` 来确定元素的位置，表返回该位置的值，就像数组返回存储在其的元素一样。在 `HashFunction()` 程序得不够优化的情况下，可能会有多个元素具有相同的 `Index`（此处原文为 Index，对应代码中的 `Index`），落在同一个桶中——这在内部是一个元素列表。在这种情况下，被称为 `collisions`（冲突），搜索将变慢，且不再是常数时间。

#### 使用 `unordered_map` 和 `unordered_multimap`

从 C++11 开始引入的这两个实现哈希表的容器分别与 `std::map` 和 `std::multimap` 并不太大。实例化、插入和 `find` 遵循相似的模式：

点击此处查看代码图片

```cpp
// 实例化一个 int 到 string 的 unordered_map:
unordered_map<int, string> umapIntToStr;

// insert()
umapIntToStr.insert(make_pair(1000, "Thousand"));

// find():
auto pairFound = umapIntToStr.find(1000);

cout << pairFound->first << " - " << pairFound->second << endl;

// 使用数组语义查找值:
cout << "umapIntToStr[1000] = " << umapIntToStr[1000] << endl;
```

然而，`unordered_map` 的一个重要特性是可以使用哈希函数，该函数负责决定排序顺序：

点击此处查看代码图片

```cpp
unordered_map<int, string>::hasher hFn =
    umapIntToStr.hash_function();
```

你可以通过调用键的哈希函数来查看分配给键的优先级：

点击此处查看代码图片

```cpp
size_t hashingVal = hFn(1000);
```

由于 `unordered_map` 将键值对存储在桶中，当 map 中的元素数量达到或趋于桶的数量时，它会进行自动负载均衡：

点击此处查看代码图片

```cpp
cout << "Load factor: " << umapIntToStr.load_factor() << endl;
cout << "Max load factor = " << umapIntToStr.max_load_factor() << endl;
cout << "Max bucket count = " << umapIntToStr.max_bucket_count() << endl;
```

`load_factor()`（负载因子）是 `unordered_map` 中桶填充程度的指标。当由于插入导致 `load_factor()` 超过 `max_load_factor()` 时，`map` 会重新组织自己以增加可用桶的数量并重建哈希表，如列表 20.6 所示。

---

**提示**

`std::unordered_multimap` 与 `unordered_map`，它支持具有相同键的多个对。

---

**列表 20.6** 实例化 STL 哈希表实现 `unordered_map`，使用 `insert()`、`find()`、`size()`、`max_bucket_count()`、`load_factor()` 和 `max_load_factor()`

点击此处查看代码图片

```cpp
0: #include<iostream>
1: #include<string>
2: #include<unordered_map>
3: using namespace std;
4:
5: template <typename T1, typename T2>
6: void DisplayUnorderedMap(unordered_map<T1, T2>& cont)
7: {
8:     cout << "Unordered Map contains: " << endl;
9:     for (auto element = cont.cbegin();
10:          element != cont.cend();
11:          ++ element )
12:         cout << element->first << " -> " << element->second << endl;
13:
14:     cout << "Number of pairs: " << cont.size() << endl;
15:     cout << "Bucket count = " << cont.bucket_count() << endl;
16:     cout << "Current load factor: " << cont.load_factor() << endl;
17:     cout << "Max load factor = " << cont.max_load_factor() << endl;
18: }
19:
20: int main()
21: {
22:     unordered_map<int, string> umapIntToStr;
23:     umapIntToStr.insert(make_pair(1000, "Thousand"));
24:     umapIntToStr.insert(make_pair(1, "One"));
25:     umapIntToStr.insert(make_pair(45, "Forty Five"));
26:     umapIntToStr.insert(make_pair(1001, "One Thousand"));
27:     umapIntToStr.insert(make_pair(-2, "Minus Two"));
28:     umapIntToStr.insert(make_pair(12, "Twelve"));
29:     umapIntToStr.insert(make_pair(100, "One Hundred"));
30:     umapIntToStr.insert(make_pair(-100, "Minus One"));
31:
32:     DisplayUnorderedMap(umapIntToStr);
33:
34:     cout << "Inserting one element" << endl;
35:     umapIntToStr.insert(make_pair(300, "Three Hundred"));
36:     DisplayUnorderedMap(umapIntToStr);
37:
38:     cout << "Enter key to find: ";
39:     int Key;
40:     cin >> Key;
41:     auto element = umapIntToStr.find(Key);
42:     if (element != umapIntToStr.end())
43:         cout << "Found! Key pairs with value " << element->second << endl;
44:     else
45:         cout << "Key has no corresponding value!" << endl;
46:
47:     return 0;
48: }
```

### 注意事项

不要依赖 `unordered_map`（顾名思义）中元素的顺序，无论键是什么。map 中某个元素相对于其他元素的顺序取决于许多因素，包括其键、插入顺序以及桶（buckets）的数量等。

这些容器针对搜索性能进行了优化，当你在遍历它们时，不要依赖于元素的顺序。

## 备注

`std::unordered_map` 提供的插入和搜索（在不发生冲突的情况下）几乎是常数时间复杂度，这与包含的元素数量无关。然而，这并不意味着 `std::unordered_map` 优于 `std::map`，因为 `std::map` 在所有情况下都提供对数复杂度。常数项可能大得多，导致前者在元素数量较少的情况下速度较慢。

在进行模拟真实场景使用的特定基准测试后，根据容器的类型做出决策是非常关重要的。

## 建议（DO）

- 在需要键唯一的键值对的情况下，务必使用 `map`。
- 在需要键可以重复的键值对（例如，电话簿）的情况下，务必使用 `multimap`。
- 务必记住 `map` 和 `multimap` 与其他 STL 容器一样，都具有成员方法 `size()`，它可以告诉你它们包含多少键值对。
- 当常数时间插入和搜索至关重要时（通常是元素数量非常多时），务必使用 `unordered_map` 或 `unordered_multimap`。

## 避免（DON’T）

- 不要忘记 `multimap::count(key)` 可以告诉你容器中使用 `key` 索引的键值对数量。
- 不要忘记通过将 `find()` 操作的结果与容器的 `end()` 进行比较来检查结果。

### 总结

在本节中，你学习了如何使用 STL `map` 和 `multimap`、它们重要的成员函数及其特性。你还学习了这些容器具有对数复杂度，并且 STL 以 `unordered_map` 和 `unordered_multimap` 的形式提供了哈希表容器。它们在 `insert()` 和 `find()` 操作中的性能与容器大小无关。你还学习了使用谓词自定义排序标准的重要性，正如在 Listing 20.5 的目录应用程序中所演示的那样。

### 问答

**Q：如何声明一个按数值降序排序或存储的整数 map？**

**A：** `map <int>` 定义了一个整数的 `map`。它使用默认的排序谓词 `std::less <T>` 按数值升序对项目进行排序，也可以表示为 `map <int, less <int>>`。要按数值降序排序，请将 `map` 定义为 `map <int, greater <int>>`。

**Q：如果我在字符串 map 中插入两次字符串 "Jack" 会发生什么？**

**A：** `map` 不用于插入非唯一值。因此，该 map 仍然只包含一个键名为 "Jack" 的键值对。

# 第四部分：更多 STL

## 第 21 节：理解函数对象

函数对象或仿函数（functors）听起来可能奇异或令人生畏，但它们是 C++ 中的实体，你可能已经见过甚至在使用，而并没有意识到。在本节中，你将学习到：

- 函数对象的概念
- 函数对象作为谓词用法
- 如何使用函数对象实现一元和二元谓词

### 函数对象和谓词的概念

在概念层，函数对象是像函数一样工作的对象。但在实现层，函数对象是实现了 `operator()` 的类对象。虽然函数和函数指针也可以被归类为函数对象，但正是实现 `operator()` 的类对象携带 `state`（即类成员属性中的值）的能力，使得它在标准模板库（STL）算法中非常有用。

返回 `boolean` 类型的函数对象自然适用于辅助决策的算法。`find()` 和 `sort()` 是你之前在课程中学习过的两种算法。组合两个函数对象的函数对象被称为“自适应函数对象”（`adaptive function object`）。

### 函数对象的典型应用

可以用数页的理论解释来介绍函数对象，也可以通过微小的示例程序来理解它们的外观和工作原理。让我们采取实用的方法，直接进入函数对象或仿函数（functors）的 C++ 编程世界！

#### 一元函数

对单个参数的操作称为一元函数。一元函数可以执行非常简单的操作——例如，在屏幕上显示一个元素。可以按如下方式编写：

点击此处查看代码图像

```cpp
// A unary function

template <typename elementType>

void FuncDisplayElement (const elementType& element)

{

    cout << element << ' ';

};
```

函数 `FuncDisplayElement` 接受一个模板类型 `elementType` 的参数，并使用控制台输出语句 `std::cout` 将其显示。该函数也可以有另一种表示，即函数的实现实际上包含在 `class` 或 `struct` 的 `operator()` 中：

点击此处查看代码图像

```cpp
// Struct that can behave as a unary function

template <typename elementType>

struct DisplayElement

{

    void operator () (const elementType& element) const

    {

        cout << element << ' ';

    }

};
```

**提示**

注意 `DisplayElement` 是一个 `struct`。如果它是一个 `class`，则需要给 `operator()` 一个 `public` 访问修饰符。`struct` 类似于 `class`，其成员默认是 `public` 的。

这两种实现方式都可以与 STL 算法 `for_each()` 配合，将集合的内容逐个打印到屏幕上，如列表 21.1 所示。

**列表 21.1** 使用一元函数在屏幕上显示集合的内容

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <list>
4: using namespace std;
5:
6: // struct that behaves as a unary function
7: template <typename elementType>
8: struct DisplayElement
9: {
10:     void operator () (const elementType& element) const
11:     {
12:         cout << element << ' ';
13:     }
14: };
15:
16: int main ()
17: {
18:     vector <int> numsInVec{ 0, 1, 2, 3, -1, -9, 0, -999 };
19:      cout << "Vector of integers contains: " << endl;
20:
21:     for_each (numsInVec.begin (),    // Start of range
22:                 numsInVec.end (),         // End of range
23:                   DisplayElement<int> () ); // Unary function object
24:
25:     // Display the list of characters
26:     list <char> charsInList{ 'a', 'z', 'k', 'd' };
27:     cout << endl << "List of characters contains: " << endl;
28:
29:     for_each (charsInList.begin(),
30:                   charsInList.end(),
31:                   DisplayElement<char> () );
32:
33:     return 0;
34: }
```



## 输出

![Image](img/arrow.jpg)

点击此处查看代码图像。

Vector of integers contains:

```text
0 1 2 3 -1 -9 0 -999
```

List of characters contains:

```text
a z k d
```

## 分析

![Image](img/arrow.jpg)

第 8–14 行包含函数对象 `DisplayElement`，它实现了 `operator()`。该函数对象的使用在第 21–23 行的 STL `std::for_each()` 中可见。`for_each()` 接受三个参数：第一个是范围的起始点，第二个是范围的终点，第三个是范围内每个元素被调用的函数。换句话说，该代码为 `numsInVec` 中的每个元素调用了 `DisplayElement::operator()`。

### 注意

在 Listing 21.1 中，你可以选择使用 `FuncDisplayElement` 代替 `struct DisplayElement` 以达到相同的效果。

点击此处查看代码图像。

```cpp
for_each (charsInList.begin(),
          charsInList.end(),
          FuncDisplayElement<char>);
```

### 提示

C++11 引入了 lambda 表达式，它是无名的函数对象。来自 Listing 21.1 的 `DisplayElement<T>` 的 lambda 表达式版本压缩了整个代码，包括 `struct` 的定义。

C++11 引入了 lambda 表达式，它是无名的函数对象。一个 lambda 表达式版本的 `DisplayElement<T>`（源自 Listing 21.1）压缩了整个代码，包括 `struct` 的定义。

此示例与 Listing 21.1 中的示例最大的区别在于将 `DisplayElementKeepCount()` 作为 `for_each()` 的返回值。在 `struct DisplayElementKeepCount` 中实现的 `operator()` 会被算法 `for_each()` 为容器中的每个元素调用。它显示该元素并增加存储在成员属性 `count` 中的内部计数器。在 `for_each()` 完成后，你使用 `Line \ 29` 中的对象来显示元素被打印的次数。请注意，在这种场景下，如果使用普通函数而不是在 `struct` 中实现的函数，将无法以这种如此直接的方式提供此功能。

### 一元谓词（Unary Predicate）

返回 `bool` 的一元函数称为**谓词**（predicate）。这类函数可以帮助为 STL 算法做出决策。Listing 21.3 是一个示例谓词，用于判断输入元素是否为某个初始值的倍数。

**LISTING 21.3** 一个判断数字是否为另一个数字倍数的一元谓词

点击此处查看代码图像。

```cpp
0: // 作为一元谓词的结构
1: template <typename numberType>
2: struct IsMultiple
3: {
4:     numberType Divisor;
5:
6:     IsMultiple (const numberType& divisor)
7:     {
8:         Divisor = divisor;
9:     }
10:
11:     bool operator () (const numberType& element) const
12:     {
13:         // 检查元素是否是除数的倍数
14:         return ((element % Divisor) == 0);
15:     }
16: };
```

## 分析

![Image](img/arrow.jpg)

在这里，`operator()` 返回 `bool` 并可以作为一元谓词。该结构体有一个构造函数并在 `Line \ 8` 中初始化为除数的值。存储在对象中的该值随后用于判断发送比较的元素是否能被其整除，正如你在 `operator()` 的实现中所看到的，在 `Line \ 14` 使用了数学取模运算 `%` 返回除法运算的余数。谓词将该余数与零比较，以确定该数字是否为倍数。

在 Listing 21.4 中，我们利用之前在 Listing 21.3 中看到的谓词，来判断集合中的数字是否为用户输入的除数的倍数。

**LISTING 21.4** 使用 `std::find_if()` 通过一元谓词 `IsMultiple` 在 `vector` 中查找用户提供的除数的倍数元素

点击此处查看代码图像。

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3: using namespace std;
4: // 在此处插入 Listing 21.3 的代码
5:
6: int main ()
7: {
8:     vector <int> numsInVec{ 25, 26, 27, 28, 29, 30, 31 };
9:     cout << "The vector contains: 25, 26, 27, 28, 29, 30, 31" << endl;
10:
11:     cout << "Enter divisor (> 0): ";
12:     int divisor = 2;
13:     cin >> divisor;
14:
15:     // 找到第一个是除倍数的元素
16:     auto element = find_if (numsInVec.begin (),
17:                             numsInVec.end (),
18:                             IsMultiple<int>(divisor) );
19:     if (element != numsInVec.end ())
20:     {
21:         cout << "First element in vector by " << divisor;
22:         cout << ": " << *element << endl;
23:     }
24:
25:     return 0;
26: }
```

## 输出

![Image](img/arrow.jpg)

点击此处查看代码图像。

```text
The vector contains: 25, 26, 27, 28, 29, 30, 31
Enter divisor (> 0): 4
First element in vector by 4: 28
```

## 分析

![Image](img/arrow.jpg)

该示例以一个整数 `vector` 容器开始。一元谓词的使用如 `Line \ 16` 所示位于 `find_if()` 中。在这里，函数对象 `IsMultiple()` 初始化为用户提供的除数并存储在 `Divisor` 中。`find_if()` 的工作原理为指定范围内的每个元素调用一元谓词 `IsMultiple::operator()`。当 `operator()` 返回 `true` 时（当该元素能被除数整除时发生），`find_if()` 返回该迭代器。正如你在 `operator()` 的实现中所看到的，在 `Line \ 14` 使用了数学取模运算 `%` 返回除法运算的余数。谓词将该余数与零比较，以确定该数字是否为倍数。

在 Listing 21.4 中，我们利用之前在 Listing 21.3 中看到的谓词，来判断集合中的数字是否为用户输入的除数的倍数。

```cpp
45:      cout << vecResult [index] << ' ';

47:      return 0;

48: }
```

## 输出

![Image](img/arrow.jpg)

点击此处查看代码图像。

第一个 vector 内容为：

```text
0 1 2 3 4
```

第二个 vector 内容为：

```text
100 101 102 103 104
```

乘法的结果为：

```text
0 101 204 309 416
```

## 分析

![Image](img/arrow.jpg)

第 4–13 行包含了 `Multiply` 类，如上一个代码段所示。在此示例中，你使用 `std::transform()` 算法将两个范围的内容相乘，并存储在第三个范围中。在这种情况下，涉及的范围存储在 `std::vector` 中，分别为 `multiplicands`（乘数）、`multipliers`（乘因子）和 `vecResult`。你在第 27–31 行中使用 `std::transform()` 将 `multiplicands` 中的每个元素与其在 `multipliers` 中对应的元素相乘，并将乘法结果存储在 `vecResult` 中。乘法本身是由二进制函数 `Multiply::operator()` 完成的，该函数为构成源和目标范围的向量中的每个元素调用。`operator()` 的返回值存储在 `vecResult` 中。

因此，此示例演示了二元函数在对 STL 容器元素执行算术操作的应用。下一个示例也使用了 `std::transform()`，但用于使用函数 `tolower()` 将字符串转换为小写。

### 二元谓词

接受两个参数并返回 `bool` 的函数是二元谓词。此类函数应用于 STL 函数，例如 `std::sort()`。列表 21.6 展示了二元谓词的使用，在将两个字符串都转换为小写后对其进行比较。例如，这种谓词可以用于 `string` 的 `vector` 执行不区分大小写的排序。

**列表 21.6** 用于不区分大小写字符串排序的二元谓词

点击此处查看代码图像。

```cpp
0: #include <algorithm>
1: #include <string>
2: using namespace std;
3:
4: class CompareStringNoCase
5: {
6: public:
7:     bool operator () (const string& str1, const string& str2) const
8:     {
9:         string str1LowerCase;
10:
11:         // 分配空间
12:         str1LowerCase.resize (str1.size ());
13:
14:         // 将每个字符转换为小写
15:         transform (str1.begin (), str1.end (), str1LowerCase.begin (),
16:                    ::tolower);
17:
18:         string str2LowerCase;
19:         str2LowerCase.resize (str2.size ());
20:         transform (str2.begin (), str2.end (), str2LowerCase.begin (),
21:                    ::tolower);
22:
23:         return (str1LowerCase < str2LowerCase);
24:     }
25: };
```

## 分析

![Image](img/arrow.jpg)

在 `operator()` 中实现的二元谓词首先使用算法 `std::transform()`（如第 15 和 20 行所示）将输入字符串转换为小写，然后使用字符串的比较运算符 `operator <` 返回比较结果。

你可以将此二元谓词与算法 `std::sort()` 一起使用，对 `vector<string>` 中的动态数组进行排序，如列表 21.7 所示。

**列表 21.7** 使用函数对象 `class CompareStringNoCase` 对 `vector<string>` 执行不区分大小写的排序

点击此处查看代码图像。

```cpp
0: // 在此处插入列表 21.6 中的 classStringNoCase

1: #include <vector>
2: #include <iostream>
3:
4: template <typename T>
5: void DisplayContents (const T& container)
6: {
7:     for (auto element = container.cbegin();
8:          element != container.cend ();
9:          ++ element )
10:     cout << *element << endl;
11: }
12:
13: int main ()
14: {
15:     // 定义一个存储名称的 string vector
16:     vector <string> names;
17:
18:     // 将示例名称插入 vector
19:     names.push_back ("jim");
20:     names.push_back ("Jack");
21:     names.push_back ("Sam");
22:     names.push_back ("Anna");
23:
24:     cout << "按插入顺序排列的 vector 中的名称: " << endl;
25:     DisplayContents(names);
26:
27:     cout << "使用默认 std::less<> 排序后的名称: " << endl;
28:     sort(names.begin(), names.end());
29:     DisplayContents(names);
30:
31:     cout << "使用不区分大小写谓词排序后的名称: " << endl;
32:     sort(names.begin(), names.end(), CompareStringNoCase());
33:     DisplayContents(names);
34:
35:     return 0;
36: }
```

# 3. 编写一个辅助升序排序的二元谓词

## 第 22 节 Lambda 表达式

Lambda 表达式是一种定义和构造无名函数对象的简洁方式。这些表达式是在 C++11 中引入的。在本节中，你将了解到：

- ![Image](img/square.jpg) 如何编写 lambda 表达式
- ![Image](img/square.jpg) 如何将 lambda 表达式作为谓词
- ![Image](img/square.jpg) 什么是 C++14 通用 lambda 表达式
- ![Image](img/square.jpg) 如何编写可以持有并操作状态的 lambda 表达式

### 什么是 Lambda 表达式？

Lambda 表达式可以可视化为带有公共 `operator()` 的无名 `struct`（或 `class`）的紧凑版本。从这个意义上说，lambda 表达式是一个函数对象，类似于第 21 节中“理解函数对象”中的对象。在深入分析 lambda 函数的编程之前，先以列表 21.1（来自第 21 节）中的函数对象作为示例：

点击此处查看代码。

```cpp
// 行为类似于一元函数的结构体
template <typename elementType>
struct DisplayElement
{
    void operator () (const elementType& element) const
    {
        cout << element << ' ';
    }
};
```

该函数对象使用 `cout` 在屏幕上显示对象 `element`，通常用于 `std::for_each()` 等算法：

点击此处查看代码。

```cpp
// 显示 vector 中包含的每个整数
for_each (numsInVec.cbegin (),       // 范围开始
          numsInVec.cend (),         // 范围结束
          DisplayElement <int> ());  // 一元函数对象
```

Lambda 表达式将包括函数对象定义在整个代码压缩为三行：

点击此处查看代码。

```cpp
// 使用 lambda 表达式显示 vector 中包含的每个整数。
for_each (numsInVec.cbegin (),   // 范围开始
          numsInVec.cend (),     // 范围结束
          [](const int& element) { cout << element << ' '; } );
```

当编译器看到 lambda 表达式时，在此情况下：

```cpp
[](const int& element) { cout << element << ' '; }
```

它会自动将此表达式展开为类似于 `struct DisplayElement<int>` 的表示形式：

点击此处查看代码。

```cpp
struct NoName
{
```



```cpp
void operator () (const int& element) const
{
    cout << element << ' ';
}
```

> **提示**
>
> Lambda 表达式也称为 Lambda 函数。

## 如何定义 Lambda 表达式

Lambda 表达式的定义必须以方括号`[]`开始。这些括号本质上是告诉编译器 Lambda 表达式已经开始。其后是参数列表，这与在你不使用 Lambda 表达式时为`operator()`的实现提供的参数列表相同。

## 用于一元函数的 Lambda 表达式

接收一个参数的一元`operator(Type)`的 Lambda 版本如下：

点击此处查看代码

```cpp
[](Type paramName) {
    // 此处为 Lambda 表达式代码
}
```

请注意，如果你需要，可以按引用传递参数：

点击此处查看代码

```cpp
[](Type& paramName) {
    // 此处为 Lambda 表达式代码
}
```

请使用列表 22.1 学习如何使用 Lambda 函数通过算法`for_each()`显示标准模板库（STL）容器的内容。

**列表 22.1** 通过由 Lambda 表达式而非函数对象调用的算法`for_each()`显示容器中的元素

点击此处查看代码

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <list>
4:
5: using namespace std;
6:
7: int main ()
8: {
9:     vector<int> numsInVec{ 101, -4, 500, 21, -1 };
10:
11:    list<char> charsInList{ 'a', 'h', 'z', 'l' };
12:    cout << "Display elements in a vector using a lambda: " << endl;
13:
14:    // 显示整数数组
15:    for_each (numsInVec.cbegin (),   // 范围开始
16:             numsInVec.cend (),      // 范围结束
17:             [](const int& element) {cout << element << ' '; } ); // lambda
18:
19:    cout << endl;
20:    cout << "Display elements in a list using a lambda: " << endl;
21:
22:    // 显示字符列表
23:    for_each (charsInList.cbegin (),   // 范围开始
24:             charsInList.cend (),      // 范围结束
25:             [](const int& element) {cout << element << ' '; } );
```

```cpp
3: using namespace std;
4:
5: int main()
{
    vector<int> numsInVec{ 25, 101, 2017, -50 };

    auto evenNum = find_if(numsInVec.cbegin(),
                           numsInVec.cend(),  // 要查找的范围
                           [](const int& num){return ((num % 2) == 0); } );

    if (evenNum != numsInVec.cend())
        cout << "Even number in collection is: " << *evenNum << endl;

    return 0;
}
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图像

集合中的偶数是: -50

## 分析 ![Image](img/arrow.jpg)

第 11 行了作为一元谓元的 Lambda 函数。算法`find_if()`会对范围内的每个元素调用一元谓词。当谓词返回`true`时，`find_if()`通过返回指向该元素的迭代器`evenNum`来报告找到。在这种情况下，谓词是一个 Lambda 表达式，当`find_if()`用偶数整数调用它时，它返回`true`（即与 2 取模运算的结果为 0）。

### 注意

列表 22.2 不仅演示了作为一元谓元的 Lambda 表达式，还演示了在 Lambda 表达式中使用`const`。

记住对输入参数使用`const`，特别是当它们是引用时，以避免无意修改容器元素的值。

## 通过捕获列表`[...]`使用状态的 Lambda 表达式

在列表 22.2 中，你创建了一个一元谓元，如果整数能被 2 整除则返回`true`——即该整数是偶数。如果你想要一个更通用的函数，当数字能被用户选择的除数整除时返回`true`怎样？你需要在表达式中维护该“状态”——除数：

点击此处查看代码图像

```cpp
int divisor = 2; // 初始值

...

auto element = find_if(begin of a range,
                       end of a range,
                       divisor{return (dividend % divisor) == 0; });
```

作为状态变量传递的参数列表`[...]`也称为 Lambda 的捕获列表。

### 注意

这种 Lambda 表达式是列表 21.3 中看到的 16 行代码的等效写法，该代码定义了一元谓元`struct IsMultiple<>`。

因此，C++11 引入的 Lambda 飞跃式地提升了编程效率！

列表 22.3 演示了在给定状态变量的一元谓元的情况下，在集合中寻找用户提供的除数的倍数的数字应用。

**列表 22.3** 演示使用持有状态的 Lambda 表达式来检查一个数是否被另一个数整除

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3: using namespace std;
4:
5: int main()
{
    vector <int> numsInVec{25, 26, 27, 28, 29, 30, 31};
    cout << "The vector contains: {25, 26, 27, 28, 29, 30, 31}";
    cout << endl << "Enter divisor (> 0): ";

    int divisor = 2;
    cin >> divisor;

    // 找到第一个是除数倍数的元素
    vector <int>::iterator element;

    element = find_if (numsInVec.begin ()
                      numsInVec.end ()
                      divisor{return (dividend % divisor) == 0; );

    if (element != numsInVec.end ())
    {
        cout << "First element in vector divisible by " << divisor;
        cout << ": << << *element << endl;
    }

    return 0;
}
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图像

```text
The vector contains: {25, 26, 27, 28, 29, 30, 31}
Enter divisor (> 0): 4
First element in vector divisible by 4: 28
```

## 分析 ![Image](img/arrow.jpg)

第 18 行了包含状态并作为谓元的 Lambda 表达式。`divisor`是状态变量，类似于你在列表 21.3 中看到的`IsMultiple::Divisor`。因此，状态变量类似于你在 C++1 出现之前的几天就已组合的函数对象类中的成员。你现在能够向你的 Lambda 函数传递状态，并在此基础上自定义它的用法。

### 注意

列表 22.2 演示了作为一元谓元的 Lambda 表达式，还演示了在 Lambda 表达式中使用`const`。

## Lambda 表达式的通用语法

Lambda 表达式总是以方括号开始，并可以使用逗号处理多个状态变量，捕获列表`[]`：

点击此处查看代码图像

```cpp
stateVar1, stateVar2 {
    // lambda here;
}
```

如果你想在 Lambda 内部修改状态变量，请添加`mutable`关键字：

点击此处查看代码图像

```cpp
stateVar1, stateVar2 mutable
```

如果你想确保对 Lambda 内部的修改在外部也有效，你需要使用引用：

点击此处查看代码图像

```cpp
&stateVar1, &stateVar2
```

Lambda 可以接受多个输入参数，用逗号分隔：

点击此处查看代码图像

```cpp
stateVar1, stateVar2 {
    // here;
}
```

如果你想指定返回类型而不是让编译器歧义，你可以使用`->`，如下：

点击此处查看代码图像

```cpp
stateVar1, stateVar2 -> ReturnType
```

最后，复合语句`{}`可以包含多个语句，每条语句用`;`分隔，如下：

点击此处查看代码图像

```cpp
stateVar1, stateVar2 -> ReturnType
{
    Statement 1;
    Statement 2;
    return (value or expression);
}
```

### 注意

如果你的 Lambda 表达式跨多行，你需要提供显式的返回类型。

列表 22.5 在本课程稍后演示了一个指定返回类型并跨多行的 Lambda 函数。

因此，Lambda 函数是如下函数对象的紧凑全功能替代品：

点击此处查看代码图像

```cpp
template<typename Type1, typename Type2>
struct IsTooLong
{
    // 状态变量
    Type1 var1;
    Type2 var2;

    // 构造函数
    IsTooLong(const Type1& in1, Type2& in2): var1(in1), var2(in2) {};

    // 实际目的
    ReturnType operator()
    {
        Statement 1;
        Statement 2;
        return (value or expression);
    }
};
```

## 二元函数的 Lambda 表达式

二元函数接受两个参数并可选返回返回值。相同的 Lambda 表达式是：

点击此处查看代码图像

```cpp
... {
    // here;
}
```

使用`std::transform()`逐元素相乘两个等长的向量，并将结果存储在第三个向量中的 Lambda 函数在列表 22.4 中所示。

```cpp
#include <vector>
#include <iostream>
#include <algorithm>

int main ()
{
    using namespace std;

    vector <int> vecMultiplicand{ 0, 1, 2, 3, 4 };
    vector <int> vecMultiplier{ 100, 101, 102, 103, 104 };

    // Holds the result of multiplication
    vector <int> vecResult;

    // Make space for the result of the multiplication
    vecResult.resize(vecMultiplier.size());

    transform (vecMultiplicand.begin (), // range of multiplicands
               vecMultiplicand.end (), // end of range
               vecMultiplier.begin (),  // multiplier values
               vecResult.begin (), // range that holds result
               [](int a, int b) {return a * b; }  // lambda

    cout << "The contents of the first vector are: " << endl;
    for (size_t index = 0; index < vecMultiplicand.size(); ++index)
        cout << vecMultiplicand[index] << ' ';
    cout << endl;

    cout << "The contents of the second vector are: " << endl;
    for (size_t index = 0; index < vecMultiplier.size(); ++index)
        cout << vecMultiplier[index] << ' ';
    cout << endl;

    cout << "The result of the multiplication is: " << endl;
    for (size_t index = 0; index < vecResult.size(); ++index)
        cout << vecResult[index] << ' ';

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

第一个 vector 的内容是：

```text
0 1 2 3 4
```

第二个 vector 的内容是：

```text
100 101 102 103 104
```

乘法结果是：

```text
0 101 204 309 416
```

## 分析 ![Image](img/arrow.jpg)

所涉及的 Lambda 表达式在第 17 行中作为`std::transform()`的参数显示。该算法接受两个范围作为输入，并应用包含二元函数的转换算法。二元函数的返回值存储在目标容器中。该二元函数是一个 Lambda 表达式，接受两个整数作为输入，并通过返回值返回乘法结果。该返回值由`std::transform()`存储在`vecResult`中。输出了两个容器的内容以及它们逐元素相乘的结果。

### 注意

列表 22.4 展示了列表 21.5 中函数对象`class Multiply<>`的 Lambda 等效实现。

## 二元谓元的 Lambda 表达式

返回`true`或`false`以帮助决策的二元函数称为“二元谓词”（binary predicate）。这些谓词用于排序算法，例如`std::sort()`，该算法会为容器中的任意两个值调用二元谓词，以确定哪一个应该放在另一个后面。二元谓词的通用语法为：

点击此处查看代码图像

```cpp
[](Type1& param1, Type2& param2) {
    // return bool;
}
```

列表 22.5 展示了一个用于排序的 Lambda 表达式。

### 列表 22.5 在`std::sort()`中作为谓元的 Lambda 表达式，以实现忽略大小写的排序

点击此处查看代码图像



```cpp
#include <algorithm>
#include <string>
#include <vector>
#include <iostream>
using namespace std;

template <typename T>
void DisplayContents (const T& input)
{
    for (auto element = input.begin(); element != input.cend(); ++ element )
        cout << *element << endl;
}

int main ()
{
    vector <string> namesInVec{ "jim", "Jack", "Anna" };

    cout << "按插入顺序在 vector 中的名称: " << endl;
    DisplayContents(namesInVec);

    cout << "区分大小敏感排序后的顺序: " << endl;
    sort(namesInVec.begin(), namesInVec.end());
    DisplayContents(namesInVec);

    cout << "忽略大小写排序后的顺序:" << endl;
    sort(namesInVec.begin(), namesInVec.end(),
        [](const string& str1, const string& str2) -> bool // lambda
        {
            string str1LC; // LC = 小写

            // 分配空间
            str1LC.resize (str1.size ());

            // 将每个字符转换为小写
            transform(str1.begin(), str1.end(), str1LC.begin(),::tolower);

            string str2LC;
            str2LC.resize (str2.size ());
            transform(str2.begin(), str2.end(), str2LC.begin(),::tolower);

            return (str1LC < str2LC);
        } // lambda 结束
    ); // sort 结束

    DisplayContents(namesInVec);

    return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

按插入顺序在`vector`中的名称：

jim

Jack

Sam

Anna

区分大小敏感排序后的顺序：

Anna

Jack

Sam

jim

忽略大小写排序后的顺序：

Anna

Jack

jim

Sam

## 分析 ![Image](img/arrow.jpg)

这展示了一个非常大的 lambda。输出了两个容器的内容以及它们逐元素相乘的结果。所涉及的 lambda 表达式在第 17 行中作为`std::transform()`的参数显示。最后，在第 28–43 行可以看到一个忽略大小写的`sort()`，它首先将字符串转换为小写，然后进行比较`return(str1LC < str2LC)`。

### 提示

列表 22.5 中这个异常巨大的 lambda 是列表 21.6 `class CompareStringNoCase` 的 lambda 版本，已用于列表 21.7。显然，这个例子还展示了，如在列表 21.6 所示，函数对象在多个`std::sort()`语句中是可以复用的，而 lambda 则在每次需要使用时都需要重写。

在本节中，你学习了 C++11 引入的一项重要特性：lambda 表达式。你已经看到 lambda 质质上是不命名的函数对象，它们可以接受参数、拥有状态、有返回值，并且可以是多行的。你学习了如何在 STL 算法中使用 lambda 代替函数对象，帮助`find()`、`sort()`或`transform()`等。Lambda 让 C++ 编程变得快速且高效，你应该在适用的地方尝试使用它们。

### 问答 (Q&A)

**问：我应该总是优先使用 lambda 而不是函数对象吗？**

**答：** 正如列表 22.5 所示，跨越多行的 lambda 可能并不像易于重用的函数对象那样有助于提高编程效率。

**问：lambda 的状态参数是如何传递的？按值传递还是按引用传递？**

**答：** 当使用如下捕获列表编写 lambda 时：

点击此处查看代码图像

```cpp
Var1, Var2, ... N { ...expression ;}
```

状态参数`Var1`和`Var2`被拷贝了（而不是作为引用提供）。如果你想让它们作为引用参数，请使用此语法：

点击此处查看代码图像

```cpp
&Var1, &Var2, ... &N { ...expression ;}
```

在这种情况下，你需要格外小心，因为在捕获列表中提供的状态变量的修改会在 lambda 外部持续。

**问：我可以在 lambda 中使用函数中的局部变量吗？**

**答：** 你可以在捕获列表中传递局部变量：

点击此处查看代码图像

```cpp
Var1, Var2, ... N { ...expression ;}
```

如果你想捕获所有变量，可以使用此语法：

点击此处查看代码图像

```cpp
= { ...expression ;}
```

### 工作坊 (Workshop)

工作坊提供了测验题帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用所学内容的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，确保在进入下一节之前理解了答案。

#### 测验 (Quiz)

1. 编译器如何识别 lambda 表达式的开始？
2. 你如何将状态变量传递给 lambda 函数？
3. 如果你需要在 lambda 中提供返回值，应该如何做？

#### 练习 (Exercises)

1. 编写一个 lambda 二元谓词，帮助按降序排列容器中的元素。
2. 编写一个 lambda 函数，当在`for_each()`中使用时，它向像`vector`等容器中的值加上用户指定的值。

## 第 23 章 STL 算法

标准模板库 (STL) 的重要部分是一组由`<algorithm>`头文件提供的泛型函数，这些函数可以帮助操作或处理容器的内容。在本节中，你将学习算法的用法，这些算法通过减少样板代码来帮助你：

- ![Image](img/square.jpg) 从容器中计数、搜索、查找、拷贝和删除元素
- ![Image](img/square.jpg) 将范围内元素的值设置为生成器函数的返回值或预定义常量
- ![Image](img/square.jpg) 对范围内的元素进行排序或分区
- ![Image](img/square.jpg) 在排序范围的正确位置插入元素

### 什么是 STL 算法？

查找、搜索、删除和计数是一些广泛应用于各种程序中的通用算法活动。STL 以泛型模板函数的形式解决了这些以及许多其他需求，这些函数通过迭代器在容器上工作。要使用 STL 算法，程序员首先必须包含`<algorithm>`头文件。

> **注意**
>
> 尽管大多数算法通过容器上的迭代器工作，但并非所有算法都一定构作用于容器，因此并非所有算法都需要迭代器。某些算法（如`swap()`）只需接受一对值进行交换。同样，`min()`和`max()`也直接对值操作。

### STL 算法的分类

STL 算法大致分为两类：非修改算法和变异算法。

#### 非修改算法

既不改变容器顺序也不改变内容的算法被称为非修改算法。一些突出的非修改算法如表 23.1 所示。

![Image](img/23tab01.jpg)

**表 23.1** 非修改算法快速参考

#### 变异算法

变异算法是改变其操作序列的内容或顺序的算法。STL 提供的最实用的变异算法如表 23.2 所示。

![Image](img/23tab02.jpg)

![Image](graphics/square.jpg)

**表 23.2** 变异算法快速参考

### STL 算法的用法

查找、搜索、删除和计数是一些广泛应用于各种程序中的通用算法活动。STL 以泛型模板函数的形式解决了这些以及许多其他需求，这些函数通过迭代器在容器上工作。要使用 STL 算法，程序员首先必须包含`<algorithm>`头文件。

> **注意**
>
> 尽管大多数算法通过容器上的迭代器工作，但并非所有算法都一定作用于容器，因此并非所有算法都需要迭代器。某些算法（如`swap()`）只需接受一对值进行交换。同样，`min()`和`max()`也直接对值操作。

#### STL 算法的用法

表 23.1 和 23.2 中提到的 STL 算法的用法最好通过实际操作来学习。为了这个这一点，请通过练习代码并开始应用它们。

#### 给定值或条件查找元素

给定一个如`vector`的容器，STL 算法`find()`和`find_if()`分别帮助你找到匹配某个值或满足某个条件的元素。`find()`的用法遵循此模式：

```cpp
auto element = find (numsInVec.cbegin(), // 起始
                    numsInVec.cend(),  // 结束
                    numToFind);         // 要查找的元素
```

`find_if()`类似，它要求提供一个单元谓词（返回`true`或`false`的单元函数）作为第三参数。

```cpp
auto evenNum = find_if (numsInVec.cbegin(), // 起始
                       numsInVec.cend(),  // 结束
                       [](int element) { return (element % 2) == 0;
```

这两个查找函数都返回一个迭代器，你需要与容器的`end()`或`cend()`进行比较以验证查找操作是否成功。如果检查成功，你可以使用该迭代器。列表 23.1 展示了使用`find()`在 vector 中查找值，以及使用`find_if()`查找第一个值。

**列表 23.1** 在`vector`中使用`find()`查找整数值，在 lambda 表达式中使用`find_if`查找给定单元谓词的第一个数字

```cpp
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    using namespace std;
    vector<int> numsInVec{ 2017, 0, -1, 42, 10101, 25 };

    cout << "在集合中查找数字：";
    int numToFind = 0;
    cin >> numToFind;

    auto element = find (numsInVec.cbegin(), // 范围起始
                        numsInVec.cend(),  // 范围结束
                        numToFind);         // 要查找的元素

    // 检查查找是否成功
    if (element != numsInVec.cend ())
        cout << "找到值 " << *element << "!" << endl;
    else
        cout << "没有元素包含值 " << numToFind << endl;

    cout << "使用 find_if 查找第一个偶数：" << endl;

    auto evenNum = find_if (numsInVec.cbegin(), // 范围起始
                          numsInVec.cend(),  // 范围结束
                          [](int element) { return (element % 2) == 0; });

    if (evenNum != numsInVec.cend())
        cout << "找到结果!" << endl;
}
```

```cpp
27: [](int element) { return (element % 2) == 0; } );

29: if (evenNum != numsInVec.cend ())
   {
      cout << "Number '" << *evenNum << "' found at position [";
      cout << distance (numsInVec.cbegin (), evenNum) << "]" << endl;
   }

35: return 0;
36: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

输入要在集合中查找的数字：42

找到值 42！

使用 find_if 查找第一个偶数：

在位置 [1] 找到数字 '0'

下次运行：

点击此处查看代码图像

输入要在集合中查找的数字：2016

未找到值为 2016 的元素

使用 find_if 查找第一个偶数：

在位置 [1] 找到数字 '0'

### 分析

`main()`起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std::distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std::count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std::count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin (), numsInVec.cend (), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std::count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std::count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量

点击此处查看代码图像



```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于`*_if`函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()`起于初始化一个整数向量，以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std::distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std::count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std::count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像。

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std::count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像。

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std::count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像。

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于`*_if`函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()`起于初始化一个整数向量，以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std::distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像。

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像。

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像。

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于`*_if`函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()`起于初始化一个整数向量，以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像。



```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std::count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std::count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std::distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std::count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std::count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std::count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std::count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std::distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std::count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std::count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std::count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std::count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)



点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

列表 23.2 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()`起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

列表 23.2 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像



```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像



### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。



点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用`find()`来查找用户输入的数字。第 25–27 行显示了在给定范围内使用`find_if()`定位第一个偶数。第 27 行是作为 Lambda 表达式提供给`find_if()`的一元谓词。该 Lambda 表达式在`element`可被 2 整除时返回`true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法`std.distance()`来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对`find()`或`find_if()`返回的迭代器相对于`cend()`进行有效性检查。这种检查不应跳过，因为它表示了`find()`操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()`和`count_if()`是帮助在给定范围内计算元素的算法。`std.count()`帮助你计算匹配某个值的元素数量（通过等价运算符`operator==`测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()`帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用`std.count()`确定具有特定值的元素数量，以及使用`count_if()`确定满足条件的元素数量。

点击此处查看代码图像



```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像



```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

'0' 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量。

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```



输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

点击此处查看代码图像

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);

cout << "Number of instances of '0': " << numZeroes << endl;
```

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
```

`cout << "Number of instances of '0': " << numZeroes << endl;`

`std.count_if()` 帮助你计算满足参数提供的一元谓词的元素数量（该谓词可以是函数对象或 Lambda 表达式）：

点击此处查看代码图像

```cpp
// 一元谓词：
template <typename elementType>
bool IsEven (const elementType& number)
{
   return ((number % 2) == 0); // 如果是偶数则为 true
}
...

// 使用一元谓词 IsEven 使用 count_if 算法：
size_t numEvenNums = count_if (numsInVec.cbegin(),
                               numsInVec.cend(), IsEven <int> );
cout << "Number of even elements: " << numEvenNums << endl;
```

列表 23.2 中的代码演示了这些函数的用法。

**列表 23.2** 展示了使用 `std.count()` 确定具有特定值的元素数量，以及使用 `count_if()` 确定满足条件的元素数量

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: 用于 *_if 函数的一元谓词
5: template <typename elementType>
6: bool IsEven (const elementType& number)
7: {
8:     return ((number % 2) == 0); // 如果是偶数则为 true
9: }
10:
11: int main ()
12: {
13:     using namespace std;
14:     vector <int> numsInVec{ 27, 0, -1, 42, 101, 25 };
15:
16:     size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
17:     cout << "Number of instances of '0': " << numZeroes << endl;
18:
19:     size_t numEvenNums = count_if (numsInVec.cbegin(),
                                       numsInVec.cend(), IsEven <int> );
20:
21:     cout << "Number of even elements: " << numEvenNums << endl;
22:     cout << "Number of odd elements: ";
23:     cout << numsInVec.size () - numEvenNums << endl;
24:
25:     return 0;
26: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

`'0'` 的实例数量：1

偶数元素数量：2

奇数元素数量：4

分析 ![Image](img/arrow.jpg)

`main()` 起于初始化一个整数向量以对第 7 行中的值进行采样。你在第 13–15 行使用 `find()` 来查找用户输入的数字。第 25–27 行显示了在给定范围内使用 `find_if()` 定位第一个偶数。第 27 行是作为 Lambda 表达式提供 `find_if()` 的一元谓词。该 Lambda 表达式在 `element` 可被 2 整除时返回 `true`，从而告知算法该元素满足正在检查的准则。注意第 32 行中使用算法 `std.distance()` 来查找找到的元素相对于容器起始位置的相对位置。

### 注意事项

注意列表 23.1 如何始终对 `find()` 或 `find_if()` 返回的迭代器相对于 `cend()` 进行有效性检查。这种检查不应跳过，因为它表示了 `find()` 操作成功，而这不被视为所当然。

### 给定值或条件计数元素

`std.count()` 和 `count_if()` 是帮助在给定范围内计算元素的算法。`std.count()` 帮助你计算匹配某个值的元素数量（通过等价运算符 `operator==` 测试）：

```cpp
size_t numZeroes = count (numsInVec.cbegin(), numsInVec.cend(), 0);
```

```cpp
37: cout << "Sequence in list found in vector at position: ";
38: cout << distance (numsInVec.cbegin(), range) << endl;
39: }
41: cout << "Searching {9, 9, 9} in vector using search_n(): " << endl;
42: auto partialRange = search_n (numsInVec.cbegin(), // Start range
                                                              numsInVec.cend(),   // End range
                                                              3,  // Count of item to be searched for
                                                              9 );   // Item to search for
47: if (partialRange != numsInVec.end())
48: {
49: cout << "Sequence {9, 9, 9} found in vector at position: ";
50: cout << distance (numsInVec.cbegin(), partialRange) << endl;
51: }
53: return 0;
54: }
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

示例 `vector` 的内容为：



2017 0 -1 42 10101 25 9 9 9

示例`list`的内容为：

-1 42 10101

使用`search()`在`vector`中查找`list`的内容：

在`vector`中找到`list`序列的位置为: 2

使用`search_n()`在`vector`中查找{9, 9, 9}:

在`vector`中找到序列{9, 9, 9}的位置为: 6

## 分析 ![Image](img/arrow.jpg)

示例从两个示例容器开始，一个`vector`和一个`list`，它们最初被填充了示例整数值。使用`search()`来查找`list`的内容是否存在于`vector`中，如第 29 行所示。由于你想在整个`vector`中搜索整个`list`的内容，因此你提供了由两个容器类的`cbegin()`和`cend()`成员方法对应的迭代器返回的范围。这实际上演示了迭代器如何有效地将算法与容器连接起来。提供这些迭代器的容器的物理特性对算法没有意义，因为算法无缝地在`vector`中搜索`list`的内容，它们只与迭代器工作。第 42 行使用`search_n()`在`vector`中查找序列{9, 9, 9}的首次出现

### 将容器中的元素初始化为特定值

`fill()`和`fill_n()`是帮助将给定范围的内容设置为指定值的 STL 算法。`fill()`根据给定的范围边界和要插入的值来重写范围内的元素：

点击此处查看代码图像

```cpp
vector <int> numsInVec (3);
// 将容器中的所有元素填充为值 9
fill (numsInVec.begin (), numsInVec.end (), 9);
```

顾如名，`fill_n()`重置指定的 n 个值。它需要一个起始位置、一个计数和一个填充值：

点击此处查看代码图像

```cpp
fill_n (numsInVec.begin () + 3, /*计数*/ 3, /*填充值*/ -9);
```

列表 23.4 演示了这些算法如何让初始化`vector<int>`中的元素变得简单。

**列表 23.4** 使用`fill()`和`fill_n()`设置容器中的初始值

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3:
4: int main ()
5: {
6:   using namespace std;
7:
8:   // 初始化包含 3 个元素的示例 vector
9:   vector <int> numsInVec (3);
10:
11:  // 将容器中的所有元素填充为值 9
12:   fill (numsInVec.begin (), numsInVec.end (), 9);
13:
14:   // 增加 vector 的大小以容纳 6 个元素
15:   numsInVec.resize (6);
16:
17:   // 从偏移量 3 开始的三个元素填充为值 -9
18:   fill_n (numsInVec.begin () + 3, 3, -9);
19:
20:   cout << "Contents of the vector are: " << endl;
21:   for (size_t index = 0; index < numsInVec.size (); ++ index)
22:   {
23:     cout << "Element [" << index << "] = ";
24:     cout << numsInVec [index] << endl;
25:   }
26:
27:   return 0;
28: }
```

Output ![Image](img/arrow.jpg)

点击此处查看代码图像

vector 的内容为：

Element [0] = 9

Element [1] = 9

Element [2] = 9

Element [3] = -9

Element [4] = -9

Element [5] = -9

如第 9 行所示，使用当前时间作为种子初始化随机数生成器，意味着输出在应用程序每次运行时都可能不同。列表 23.5 使用第 12 行的`generate()`填充`vector`中的所有元素，并使用第 21 行的`generate_n()`使用生成器函数`rand()`提供的随机值填充`list`的前三个元素。注意，`generate()`函数接受一个范围作为输入，并因此对范围内的每个元素调用指定的函数对象`rand()`。相比之下，`generate_n()`仅接受起始位置。它会根据`count`参数指定的次数调用指定的函数对象`rand()`，以覆盖相应数量元素的内容。容器中超出指定偏移量的元素将保持不变。

### 使用`for_each()`处理范围内的元素

`for_each()`算法将指定的一元函数对象应用于所给范围内的每个元素。`for_each()`的用法如下：

点击此处查看代码图像

```cpp
fnObjType retValue = for_each (start_of_range,
                                 end_of_range,
                                 unaryFunctionObject);
```

该一元函数对象也可以是一个接受一个参数的 lambda 表达式。

返回值表示`for_each()`返回了用于处理所给范围内每个元素的函数对象（也称为仿函数）。该规范的含义是，使用`struct`或`class`作为函数对象可以帮助存储状态信息，你可以在稍后`for_each()`完成时查询这些信息。列表 23.6 演示了这一点，它使用函数对象显示范围内的元素，并使用它来统计显示的元素数量。

**列表 23.6** 使用`for_each()`显示序列内容

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <iostream>
2: #include <vector>
3: #include <string>
4: using namespace std;
5:
6: template <typename elementType>
7: struct DisplayElementKeepcount
8: {
9:     int count;
10:     DisplayElementKeepcount (): count (0) {}
11:
12:     void operator () (const elementType& element)
13:     {
14:         ++ count;
15:         cout << element << ' ';
16:     }
17: };
18:
19: int main ()
20: {
21:     vector <int> numsInVec{ 2017, 0, -1, 42, 10101, 25 };
22:
23:     cout << "Elements in vector are: " << endl;
24:     DisplayElementKeepcount<int> functor =
25:         for_each (numsInVec.cbegin(),   // Start of range
26:                     numsInVec.cend (),     // End of range
27:                     DisplayElementKeepcount<int> ());// functor
28:     cout << endl;
29:
30:     // 使用 for_each 返回值中存储的状态!
31:     cout << "'" << functor.count << "' elements displayed" << endl;
32:
33:     string str ("for_each and strings!");
34:     cout << "Sample string: " << str << endl;
35:
36:     cout << "Characters displayed using lambda:" << endl;
37:     int numChars = 0;
38:     for_each (str.cbegin(),
39:                 str.cend(),
40:                 &numChars { cout << c << ' '; ++numChars; }
41:     cout << endl;
42:     cout << "'" << numChars << "' characters displayed" << endl;
43:
44:     return 0;
45: }
```

![Image](img/arrow.jpg) 点击此处查看代码图像

Elements in vector are: 2017 0 -1 42 10101 25

'6' elements displayed

Sample string: for_each and strings!

Characters displayed using lambda: for_each and strings!

'21' characters displayed

![Image](img/arrow.jpg) 代码示例演示了第 25 行和 38 行调用的`for_each()`的用途，且`for_each()`返回的函数对象`functor`被设计为将其调用次数存储在`count`中。代码包含两个示例范围，一个包含整数向量`numsInVec`中，另一个是`std::string`对象`str`。第一次调用`for_each()`使用`DisplayElementKeepCount`作为一元谓词，第二次则使用 lambda 表达式。`for_each()`对所给范围内的每个元素调用`operator()`，这反过来会将元素打印到屏幕上并增加一个内部计数器。`for_each()`完成后返回该函数对象，成员`count`告诉该对象被使用的次数。这种在算法返回的对象中存储信息（或状态）的功能在实际编程中非常有用。第 38 行的`for_each()`对`std::string`的操作与第 25 行的对应项完全相同，只是使用了 lambda 表达式而不是函数对象。

### 使用`std::transform()`对范围进行转换

`std::for_each()`和`std::transform()`的相似之处在于它们都会对源范围内的每个元素调用函数对象。然而，`std::transform()`有两个版本。第一个版本接受一个一元函数，常用于使用`toupper()`或`tolower()`函数将字符串转换为大或小写：

点击此处查看代码图像

```cpp
string str ("THIS is a TEst string!");
transform (str.cbegin(), // start source range
           str.cend(), // end source range
           strLowerCaseCopy.begin(), // start range
           ::tolower); // unary function
```

第二个版本接受一个二元函数，允许`transform()`处理取自两个不同范围的一对元素：

点击此处查看代码图像

```cpp
// 将两个向量的元素求并将结果存储在 deque 中
transform (numsInVec1.cbegin(), // start of source range 1
           numsInVec1.cend(),   // end of source range 1
           numsInVec2.cbegin(), // start of source range 2
           sumInDeque.begin(), // store result in a deque
           plus<int>()); // binary function plus
```

`transform()`的两个版本总是将指定转换函数的结果赋值给提供的目标范围，而`for_each()`不同，后者只作用于单一范围。`std::transform()`的用法在列表 23.7 中所示。

**列表 23.7** 使用一元和二元函数`std::transform()`

点击此处查看代码图像

```cpp
0: #include <algorithm>
1: #include <string>
2: #include <vector>
3: #include <iostream>
4: #include <functional>
5:
6: int main()
7: {
8:     using std;
9:
10:    string str ("THIS is a TEst string!");
11:    cout << "The string is: " << str << endl;
12:    string strLowerCaseCopy;
13:    strLowerCaseCopy.resize(str.size());
14:
15:    transform (str.cbegin(), // start range
16:               str.cend(), // end source range
17:               strLowerCaseCopy.begin(), // start range
18:               ::tolower); // unary function
19:
20:    cout << "Result of 'transform' on the string with 'tolower':" << endl;
21:    cout << "\"" << strLowerCaseCopy << "\"" << endl << endl;
22:
23:    // 两个整数向量...
24:    vector<int> numsInVec1{ 2017, 0, -1, 42, 10101, 25 };
25:    vector<int> numsInVec2 (numsInVec1.size(), -1);
26:
27:    // 用于存储加法结果的目标范围
28:    deque <int> sumInDeque (numsInVec1.size());
29:
30:    transform (numsInVec1.cbegin(), // start of source range 1
31:               numsInVec1.cend(),   // end of source range 1
32:               numsInVec2.cbegin(), // start of source range 2
33:               sumInDeque.begin(), // store result in a deque
34:               plus<int>()); // binary function plus
```

标签中。

```cpp
35:             sumInDeque.begin(),   // start of dest range
36:             plus<int>());              // binary function
37:
38:      cout << "Result of 'transform' using binary function 'plus': " << endl;
39:      cout << "Index   Vector1 + Vector2 = Result (in Deque)" << endl;
40:      for (size_t index = 0; index < numsInVec1.size(); ++ index)
41:      {
42:          cout << index << "     \t " << numsInVec1 [index]   << "\t+   ";
43:          cout << numsInVec2 [index]  << " \t  =    ";
44:          cout << sumInDeque [index] << endl;
45:      }
46:
47:      return 0;
48: }
```

Listing 23.8 展示了`remove()`和`remove_if()`都返回一个指向容器新末尾的迭代器。然而，容器`numsInVec`尚未被调整大小。元素已经通过`remove`算法被删除，其他元素已向前移动，但`size()`保持不变，这意味着向量（vector）的末尾仍然存在值。若要调整容器的大小（这非常重要，否则末尾会产生多余的值），你需要在随后的`erase()`调用中使用`remove()`或`remove_if()`返回的迭代器，如代码所示的第 41 行和第 46 行所示。

***

## 替换值和根据条件替换元素

### 替换值和根据条件替换元素



`replace()` 和 `replace_if()` 分别是 STL 算法，可以替换集合中与给定值相等或满足给定条件的元素。`replace()` 根据比较操作符（`==`）的返回值替换元素：

```cpp
cout << "Using 'std::replace' to replace value 5 by 8" << endl;
replace (numsInVec.begin (), numsInVec.end (), 5, 8);
```

`replace_if()` 期望一个用户指定的一元谓词，该谓词对每个需要替换的值返回 `true`：

```cpp
cout << "Using 'std::replace_if' to replace even values by -1" << endl;
replace_if (numsInVec.begin (), numsInVec.end (),
    [](int element) {return ((element % 2) == 0); }, -1);
```

这些函数的用法在 Listing 23.9 中给出。

**列表 23.9** 使用 `replace()` 和 `replace_if()` 替换指定范围内的值

```cpp
0: #include <iostream>
1: #include <algorithm>
2: #include <vector>
3: using namespace std;
4:
5: template <typename T>
6: void DisplayContents(const T& container)
7: {
8:     for (auto element = container.cbegin();
9:             element != container.cend();
10:             ++ element)
11:         cout << *element << ' ';
12:
13:     cout << "| Number of elements: " << container.size() << endl;
14: }
15:
16: int main ()
17: {
18:     vector <int> numsInVec (6);
19:
20:     // 用值 8 填充前 3 个元素，后 3 个填充 5
21:     fill (numsInVec.begin (), numsInVec.begin () + 3, 8);
22:     fill_n (numsInVec.begin () + 3, 3, 5);
23:
24:     // 打乱容器
25:     random_shuffle (numsInVec.begin (), numsInVec.end ());
26:
27:     cout << "The initial contents of vector: " << endl;
28:     DisplayContents(numsInVec);
29:
30:     cout << endl << "'std::replace' value 5 by 8" << endl;
31:     replace (numsInVec.begin (), numsInVec.end (), 5, 8);
32:
33:     cout << "'std::replace_if' even values by -1" << endl;
34:     replace_if (numsInVec.begin (), numsInVec.end (),
35:         [](int element) {return ((element % 2) == 0); }, -1);
36:
37:     cout << endl << "Vector after replacements:" << endl;
38:     DisplayContents(numsInVec);
39:
40:     return 0;
41: }
```

vector 的初始内容:

`5 8 5 8 5 | Number of elements: 6`

`std::replace` value 5 by 8

`std::replace_if` even values by -1

替换后的 vector:

`-1 -1 -1 -1 -1 | Number of elements: 6`

示例使用示例值填充了 `vector<int>`，然后使用 STL 算法 `random_shuffle()` 对其进行洗乱，如第 25 行所示。第 31 行演示了如何使用 `replace()` 将所有 5 替换为 8。因此，当第 34 行的 `replace_if()` 将所有偶数替换为 -1 时，最终结果是该集合包含六个元素，且所有元素都包含相同的值 -1，如输出所示。

### 在排序集合中排序和查找以及删除重复项

对排序范围进行排序和查找（出于性能考虑）是应用中经常出现的需求。通常你有一个需要排序的信息数组，例如为了演示的目的。你可以使用 STL 的 `sort()` 算法对容器进行排序：

```cpp
sort (numsInVec.begin (), numsInVec.end()); // 升序
```

`sort()` 的这个版本使用 `less<>` 谓词，它是由类型实现的。你可以提供自己的谓词来更改 vector 的排序顺序：

```cpp
sort (numsInVec.begin (), numsInVec.end (),
    [](int lhs, int rhs) {return lhs > rhs;} // 降序
```

同样，在显示集合之前需要删除相邻的重复值，请使用 `unique()`：

```cpp
auto newEnd = unique (numsInVec.begin (), numsInVec.end ());
numsInVec.erase (newEnd, numsInVec.end()); // resize
```

为了快速查找，STL 提供了 `binary_search()`，它仅对排序后的容器有效：

```cpp
bool elementFound = binary_search (numsInVec.begin (), numsInVec.end (), "John");
if (elementFound)
    cout << "Element found in the vector!" << endl;
```

Listing 23.10 展示了 STL 算法：`sort()` 可以对范围进行排序，`binary_search()` 可以在排序范围上进行查找，而 `unique()` 可以消除在 `sort()` 操作后相邻的重复值。

**列表 23.10** 使用 `sort()`、`binary_search()` 和 `unique()`

（代码块见上文）

前面的代码首先在第 26 行对样本向量 `vecNames` 进行排序，然后使用第 30 行的 `binary_search()` 在其中查找 `"John"`。同样，第 39 行使用 `std::unique()` 来删除相邻重复元素的第二次出现的项。请注意，`unique()` 像 `remove()` 一样，不会调整容器的大小。它会导致值发生移动，但不会减少元素的总数。为了确保容器末尾没有多余或未定义的值，请务必在调用 `unique()` 之后，使用 `unique()` 返回的迭代器跟随调用 `vector::erase()`，如第 40 行所示。

### 注意事项

`binary_search()` 等算法仅在排序过的容器中有效。在未排序的向量上使用此算法可能会导致不符合预期的结果。

### 备注

`stable_sort()` 的用法与你之前看到过的 `sort()` 相同。`stable_sort()` 确保了排序后元素的相对顺序保持不变。保持相对顺序是以性能为代价的——这是一个需要牢记的因素，特别是当元素的相对顺序并非至关重要时。

### 划分范围

`std::partition()` 有助于将输入范围划分为两个部分：一个满足一元谓词的部分以及另一个不满足的部分：

```cpp
bool IsEven (const int& num)  // 一元谓词

{
    return ((num % 2) == 0);
}

...

partition (numsInVec.begin(), numsInVec.end(), IsEven);
```

然而，`std::partition()` 不保证每个划分区域内元素的相对顺序。当相对顺序很重要时，为了保持它，你应该使用 `std::stable_partition()`：

```cpp
stable_partition (numsInVec.begin(), numsInVec.end(), IsEven);
```

列表 23.11 展示了这些算法的用法。

**列表 23.11** 使用 `partition()` 和 `stable_partition()` 将整数范围划分为偶数和奇数值

```cpp
0: #include <algorithm>
1: #include <vector>
2: #include <iostream>
3: using namespace std;
4:
5: bool IsEven (const int& num) // 一元谓词
6: {
7:     return ((num % 2) == 0);
8: }
9:
10: template <typename T>
11: void DisplayContents(const T& container)
12: {
13:     for (auto element = container.cbegin();
14:     element != container.cend();
15:     ++element)
16:     cout << *element << ' ';
17:
18:     cout << "| Number of elements: " << container.size() << endl;
19: }
20: int main ()
21: {
22:     vector<int> numsInVec{ 2017, 0, -1, 42, 10101, 25 };
23:
24:     cout << "The initial contents: " << endl;
25:     DisplayContents(numsInVec);
26:     vector<int> vecCopy (numsInVec);
27:
28:     cout << "The effect of partition():" << endl;
29:     partition (numsInVec.begin(), numsInVec.end(), IsEven);
30:     DisplayContents(numsInVec);
31:
32:     cout << "The effect of stable_partition():" << endl;
33:     stable_partition (vecCopy.begin(), vecCopy.end(), IsEven);
34:     DisplayContents(vecCopy);
35:
36:     return 0;
37: }
```

输出：

初始内容:

`2017 0 -1 42 10101 25 | Number of elements: 6`

partition() 的效果:

`42 0 -1 2017 10101 25 | Number of elements: 6`

stable_partition() 的效果:

`0 42 2017 -1 10101 25 | Number of elements: 6`

分析：

该代码将包含在向量 `numsInVec` 中的整数范围划分为偶数和奇数值。这种划分首先通过 `std::partition()` 完成（如第 31 行所示），然后在第 35 行使用 `stable_partition()` 在副本上重复。为了比较，你将样本范围 `numsInVec` 复制到 `vecCopy` 中，前者使用 `partition()`，后者使用 `stable_partition()`。使用 `stable_partition()` 而不是 `partition` 的效果在输出中是显而易见的。`stable_partition()` 保持了每个划分区域元素的相对顺序。请注意，保持这种顺序是以性能为代价的，在某些情况下这种代价可能是很小的，取决于范围中元素的类型。

### 备注

`stable_partition()` 比 `partition()` 慢，因此只有当元素的相对顺序很重要时你才使用它。

### 在排序集合中插入元素

确保在排序集合的正确位置插入元素是重要的。STL 提供了如 `lower_bound()` 和 `upper_bound()` 等函数来满足这一需求：

```cpp
auto minInsertPos = lower_bound(names.begin(), names.end(),
                               "Brad Pitt");
// 也可以：
auto maxInsertPos = upper_bound (names.begin(), names.end(),
                               "Brad Pitt");
```

因此，`lower_bound()` 和 `upper_bound()` 返回的迭代器指向可以在不破坏排序的情况下插入元素的最小和最大位置。

列表 23.12 展示了在排序集合中使用 `lower_bound()`。

一个元素可以插入到有序集合的两个潜在位置：一个由 `lower_bound()` 返回，它是最低位置（最接近集合起始位置的）；另一个是另一个 `upper_bound()` 返回的迭代器，它是最高位置（距离集合起始位置最远的位置）。在列表 23.12 中，如果插入到有序集合的字符串 `"Brad"` 已经存在于集合中，则下界和上界是不同的（否则它们将是相同的）。这些函数的用法分别在第 24 行和第 29 行所示。如输出所示，当使用 `lower_bound()` 返回的迭代器用于第 35 行所示的将字符串插入 `list` 时，结果是列表保持其有序状态。因此，这些算法可以帮助你在集合的某处进行插入，而不会破坏内容的有序性。使用 `upper_bound()` 返回的迭代器同样可以良好工作。

## DO

**务必**记得在使用算法 `remove()`、`remove_if()` 或 `unique()` 之后，使用容器的 `erase()` 成员方法来调整容器的大小。

**务必**在使用 `find()`、`find_if()`、`search()` 或 `search_n()` 函数返回的迭代器之前，通过将其与容器的 `end()` 进行比较来检查其有效性。

**务必**仅在排序元素的相对顺序重要时才选择 `stable_partition()` 代替 `partition()`，以及选择 `stable_sort()` 代替 `sort()`，因为稳定版本可能会降低应用程序的性能。

## DON’T

**不要**忘记在调用 `unique()` 移除相邻重复值之前，先使用 `sort()` 对容器进行排序。`sort()` 将确保所有相同值的元素都相邻排列，使 `unique()` 有效。

**不要**在随机选择的位置向有序容器中插入元素，而应使用由 `lower_bound()` 或 `upper_bound()` 返回的位置进行插入，以确保元素的有序顺序不受干扰。

**不要**忘记 `binary_search()` 仅用于有序容器。

### 总结

在本节中，你学习了 STL 最重要且最强大的方面之一：算法。你洞察了不同类型的算法，示例应该让你对算法的应用有了更清晰的理解。

### 问答

**Q 我会在关联容器（如 `std::set`）上使用变异算法（如 `std::transform()`）吗？**

**A** 即使可行，也不应该这样做。关联容器的内容应该被视为常数。这是因为关联容器在插入元素时会对其元素进行排序，且元素的相对位置在 `find()` 等函数以及容器的效率中都起着重要作用。因此，不应在 STL 集合上使用 `std::transform()` 等变异算法。

**Q 我需要将顺序容器每个元素的内容设置为特定值。我会为此活动使用 `std::transform()` 吗？**

**A** 虽然可以使用此活动，但 `fill()` 或 `fill_n()` 更适合这项任务。

**Q `copy_backward()` 是否反转了目标容器中元素的内容？**

**A** 不。STL 算法 `copy_backward()` 反转的是元素复制的顺序，而不是元素存储的顺序；也就是说，它从范围的末尾开始并到达顶部。要反转集合的内容，你应该使用 `std::reverse()`。

**Q 我应该在列表上使用 `std::sort()` 吗？**



**A** `std::sort()` 在列表上的用法与它在任何顺序容器上的用法相同。然而，列表需要保持一个特殊属性，即对列表的操作不会使现有的迭代器失效——这是 `std::sort()` 无法保证维持的属性。因此，STL `list` 以成员函数 `list::sort()` 的形式提供了 `sort()` 算法，应该使用它，因为它保证了即使元素在列表中的相对位置发生了变化，指向这些元素的迭代器也不会失效。

**Q 为什么向有序范围插入元素时使用 `lower_bound()` 或 `upper_bound()` 等函数很重要？**

**A** 这些函数分别提供了第一个和最后一个位置，在这些位置可以将元素插入到有序集合而不破坏排序。

## 工作坊

工作坊包含测验题，帮助巩固你对所涵盖内容的理解，并提供练习提供使用所学知识的机会。在检查附录 E 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你理解了答案。

### 测验

1. 你需要从列表中移除满足特定条件的项。你会使用 `std::remove_if()` 还是 `list::remove_if()`？
2. 你有一个类类型 `ContactItem` 的列表。在没有显式指定二元谓词的情况下，`list::sort()` 函数如何对该类型的项排序？
3. STL 算法 `generate()` 运行 `generator()` 的频率是多少？
4. `transform()` 与 `for_each()` 之间有什么区别？

### 练习

1. 编写一个接受字符串并根据不区分大小写进行二元谓词。
2. 演示 `copy()` 如何使用迭代器在不同容器之间进行复制。
3. 你正在编写一个记录按顺序在地平线上出现的星星特征的应用程序。在天文学中，星星的大小以及它们升落序列的信息非常重要。如果你根据大小对这些星星进行排序，你会使用 `std::sort` 还是 `std::stable_sort`？

队列（Queue）是 FIFO（先进先出）系统，元素可以插入到前一个元素的后面，而先插入的元素先被移除。队列可以被可视化为邮局等候盖章的人排队的队伍——越早加入队列的人越早离开。这种涉及“从尾部添加但从前端删除”的元素组织方法在图 24.2 中进行了说明。

![Image](img/24fig02.jpg)

**图 24.2** 队列上的操作。

队列的这种行为在通用 STL 容器 `std::queue` 中得到了模拟。

> **提示**
>
> 要使用类 `std::queue`，请包含头文件：

```cpp
#include <queue>
```

# 使用 STL `stack` 类

STL `stack` 是一个模板类，需要包含头文件 `<stack>`。它是一个通用类，允许在栈顶插入和删除元素，不允许对中间的元素进行任何访问或检查。从这个意义上说，`std::stack` 的行为与一叠盘子非常相似。

## 实例化栈

`std::stack` 在某些 STL 实现中定义为：

点击此处查看代码图像

```cpp
template <
   class elementType,
   class Container = deque<Type>
> class stack;
```

参数 `elementType` 是栈收集的对象的类型。第二个模板参数 `Container` 是栈的默认底层容器实现类。`std::deque` 是栈内部数据存储的默认容器，可以被 `std::vector` 或 `std::list` 替换。因此，整数栈的实例化看起来如下：

点击此处查看代码图像

```cpp
std::stack <int> numsInStack;
```

如果你想创建一个任何类型对象的栈，例如类 `Tuna`，你将使用以下代码：

点击此处查看代码图像

```cpp
std::stack <Tuna> tunasInStack;
```

要创建一个使用不同底层容器的栈，请使用：

```cpp
std::stack <double, vector <double>> doublesStackedInVec;
```

列表 24.1 展示了不同的实例化技术。

**列表 24.1** STL 栈的实例化

点击此处查看代码图像

```cpp
0: #include <stack>
1: #include <vector>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     // 一个整数栈
8:     stack <int> numsInStack;
9:
10:     // 一个双精度数栈
11:     stack <double> dblsInStack;
12:
13:     // 一个包含在 vector 中的双精度数数栈
14:     stack <double, vector <double>> doublesStackedInVec;
15:
16:     // 将一个栈初始化为另一个栈的拷贝
17:     stack <int> numsInStackCopy(numsInStack);
18:
19:     return 0;
20: }
```

**分析** ![Image](img/arrow.jpg)

该示例没有产生输出，但演示了 STL `stack` 的模板实例化。第 8 行和第 11 行实例化两个 `stack` 对象，分别持有 `int` 和 `double` 类型的元素。第 14 行也实例化了一个 `double` 类型的 `stack`，但指定了第二个模板参数——`stack` 内部使用的集合类类型，即 `vector`。如果不提供此第二个模板参数，`stack` 将自动默认使用 `std::deque`。最后，第 17 行演示了一个 `stack` 对象可以作为另一个栈的拷贝来构造。

## 栈的成员函数

`stack` 适配于另一个容器（如 `deque`、`list` 或 `vector`），它通过限制元素插入或删除的方式来实现其功能，从而提供严格符合栈机制预期的行为。表 24.1 解释了 `stack` 类的公共成员函数并演示了它们在整数栈中的用法。

![Image](img/24tab01.jpg)

**表 24.1** `std::stack` 的成员函数

如表所示，栈的公共成员函数仅暴露允许符合栈行为的位置进行插入和删除的方法。也就是说，即使底层容器可能是 `deque`、`vector` 或 `list`，该容器的功能也没有被暴露，以强制执行栈的行为特征。

### 使用 `push()` 和 `pop()` 在栈顶插入和删除

元素的插入通过方法 `stack<T>::push()` 完成：

点击此处查看代码图像

```cpp
numsInStack.push(25); // 25 位于栈顶
```

栈通过方法 `top()` 允许对栈顶元素的访问：

```cpp
cout << numsStack.top() << endl;
```

如果你想移除栈顶的元素，可以使用 `pop()` 函数：

```cpp
numsInStack.pop(); // 移除栈顶元素
```

列表 24.2 演示了使用 `push()` 和 `pop()` 在栈顶进行插入和删除。

**列表 24.2** 使用 `push()` 操作整数栈



提示

要使用类 `std::queue`，请包含头文件：

```cpp
#include <queue>
```

# 使用 STL `stack` 类

STL `stack` 是一个模板类，需要包含头文件 `<stack>`。它是一个通用类，允许在栈顶插入和删除元素，不允许对中间的元素进行任何访问或检查。从这个意义上说，`std::stack` 的行为与一叠盘子非常相似。

## 实例化栈

`std::stack` 在某些 STL 实现中定义为：

点击此处查看代码图像

```cpp
template <
   class elementType,
   class Container = deque<Type>
> class stack;
```

参数 `elementType` 是栈收集的对象的类型。第二个模板参数 `Container` 是栈的默认底层容器实现类。`std::deque` 是栈内部数据存储的默认容器，可以被 `std::vector` 或 `std::list` 替换。因此，整数栈的实例化看起来如下：

点击此处查看代码图像

```cpp
std::stack <int> numsInStack;
```

如果你想创建一个任何类型对象的栈，例如类 `Tuna`，你将使用以下代码：

点击此处查看代码图像

```cpp
std::stack <Tuna> tunasInStack;
```

要创建一个使用不同底层容器的栈，请使用：

点击此处查看代码图像

```cpp
std::stack <double, vector <double>> doublesStackedInVec;
```

列表 24.1 演示了不同的实例化技术。

**列表 24.1** STL 栈的实例化

点击此处查看代码图像

```cpp
0: #include <stack>
1: #include <vector>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     // A stack of integers
8:     stack <int> numsInStack;
9:
10:     // A stack of doubles
11:     stack <double> dblsInStack;
12:
13:     // A stack of doubles contained in a vector
14:     stack <double, vector <double>> doublesStackedInVec;
15:
16:     // initializing one stack to be a copy of another
17:     stack <int> numsInStackCopy(numsInStack);
18:
19:     return 0;
20: }
```

分析 ![Image](img/arrow.jpg)

该示例没有产生输出，但演示了 STL `stack` 的模板实例化。第 8 行和第 11 行实例化两个 `stack` 对象，分别持有 `int` 和 `double` 类型的元素。第 14 行也实例化了一个 `double` 类型的 `stack`，但指定了第二个模板参数——`stack` 内部使用的集合类类型，即 `vector`。如果不提供此第二个模板参数，`stack` 将自动默认使用 `std::deque`。最后，第 17 行演示了一个 `stack` 对象可以作为另一个栈的拷贝来构造。

## 栈成员函数

`stack` 适配于另一个容器（如 `deque`、`list` 或 `vector`），它通过限制元素插入或删除的方式来实现其功能，从而提供严格符合栈机制预期的行为。表 24.1 解释了 `stack` 类的公共成员函数并演示了它们在整数栈中的用法。

![Image](img/24tab01.jpg)

**表 24.1** `std::stack` 的成员函数

如表所示，栈的公共成员函数仅暴露允许符合栈行为的位置进行插入和删除的方法。也就是说，即使底层容器可能是 `deque`、`vector` 或 `list`，该容器的功能也没有被暴露，以强制执行栈的行为特征。

### 使用 `push()` 和 `pop()` 在栈顶插入和删除

元素的插入通过方法 `stack<T>::push()` 完成：

点击此处查看代码图像

```cpp
numsInStack.push(25); // 25 is atop the stack
```

栈通过方法 `top()` 允许对栈顶元素的访问：

点击此处查看代码图像

```cpp
cout << numsStack.top() << endl;
```

如果你想移除栈顶的元素，可以使用 `pop()` 函数：

点击此处查看代码图像

```cpp
numsInStack.pop(); // 移除栈顶元素
```

列表 24.2 演示了使用 `push()` 和 `pop()` 在栈顶进行插入和删除。

**列表 24.2** 使用 `push()` 操作整数栈

## 使用 STL `queue` 类

STL `queue` 是一个模板类，需要包含 `<queue>` 头文件。它是一个通用类，允许仅在末尾插入元素并仅在头部删除元素。`queue` 不允许对中间的元素进行任何访问或检查；然而，可以访问开头和结尾的元素。从某种意义上说，`std::queue` 的行为与超市收银台前排队的队列非常相似！

### 实例化队列

`std::queue` 定义为：

点击此处查看代码图像

```cpp
template <
   class elementType,
   class Container = deque<Type>
> class queue;
```

在这里，`elementType` 是队列对象收集的元素类型。`Container` 是 `std::queue` 类用于维护其数据的集合类型。`std::list`、`vector` 和 `deque` 都是该模板参数的可能候选类型，而 `deque` 是默认值。

整数队列最简单的实例化方式如下：

```cpp
std::queue <int> numsInQ;
```

如果你想创建一个在 `std::list` 中（而不是默认的 `deque`）包含 `double` 类型元素的队列，请使用以下代码：

点击此处查看代码图像

```cpp
std::queue <double, list <double>> dblsInQInList;
```

就像栈一样，队列也可以实例化为另一个队列的拷贝：

点击此处查看代码图像

```cpp
std::queue<int> copyQ(numsInQ);
```

列表 24.3 演示了 `std::queue` 的各种实例化技术。

**列表 24.3** 实例化 STL 队列

```cpp
0: #include <queue>
1: #include <list>
...
int main ()
{
   using namespace std;

   // 一个整数队列
   queue <int> numsInQ;

   // 一个双精度浮数队列
   queue <double> dblsInQ;

   // 一个内部存储在 list 中的双精度浮数队列
   queue <double, list <double>> dblsInQInList;

   // 作为另一个队列拷贝创建的队列
   queue<int> copyQ(numsInQ);

   return 0;
}
```

分析：示例演示了如何实例化通用 STL 类 `queue` 来创建一个整数队列（如第 8 行所示），或用于 `double` 类型对象的队列（如第 11 行所示）。在第 14 行实例化的 `dblsInQInList` 是一个 `queue`，你显式指定了 `queue` 用于管理其内部的适配底层容器为 `std::list`，正如第二个模板参数所指定的。在没有第二个模板参数的情况下（如前两个队列），使用 `std::deque` 作为 `queue` 内容的默认底层容器。

### `queue` 的成员函数

`std::queue` 与 `std::stack` 一样也基于 STL 容器（如 `vector`、`list` 或 `deque`）来实现实现。`queue` 仅暴露实现队列行为特征的成员函数。表格 24.2 解释了使用 `numsInQ` 的成员函数，而列表 24.3 演示了这是一个整数 `queue`。

STL `queue` 不具备 `begin()` 和 `end()` 函数，这些函数是由大多数 STL 容器（包括 `queue` 类使用的底层 `deque`、`vector` 或 `list`）提供的。这是刻意为，以确保 `queue` 上唯一允许的操作是符合 `queue` 行为特征的操作。

### 通过 `push()` 和 `pop()` 在 `queue` 的末尾插入和头部删除

队列中元素的插入发生在末尾，并使用成员方法 `push()` 完成：

点击此处查看代码图像

```cpp
numsInQ.push (5); // 元素插入在末尾
```

相反，删除通过 `pop()` 在头部发生：

点击此处查看代码图像

```cpp
numsInQ.pop (); // 移除头部元素
```

与 `stack` 不同，`queue` 允许两端的元素（即 `front` 和 `back`）被检查：

```cpp
cout << "Element at front: " << numsInQ.front() << endl;
cout << "Element at back: " << numsInQ.back () << endl;
```

插入、删除和检查在列表 24.4 中演示。

**列表 24.4** 在整数 `queue` 中插入、删除和检查元素

```cpp
#include <queue>
#include <iostream>

int main ()
{
   using namespace std;
   queue<int> numsInQ;

   cout << "Inserting {10, 5, -1, 20} into queue" << endl;
   numsInQ.push(10);
   numsInQ.push(5);
   numsInQ.push(-1);
   numsInQ.push(20);

   cout << "Queue contains " << numsInQ.size() << " elements" << endl;
   cout << "Element at front: " << numsInQ.front() << endl;
   cout << "Element at back: " << numsInQ.back () << endl;

   while (numsInQ.size() != 0)
   {
      cout << "Deleting element: " << numsInQ.front() << endl;
      numsInQ.pop(); // removes element at front
   }

   if (numsInQ.empty())
   {
      cout << "The queue is now empty!" << endl;
   }
   return 0;
}
```

分析：元素通过 `push()` 添加到 `numsInQ`，该操作在队列的末尾（`back`），如第 9-12 行所示。第 18-22 行的 `while` 循环显示队列头部元素，然后在第 21 行将其移除。输出显示元素按插入顺序从队列中删除，因为元素是从队列头部删除的。

## 使用 STL 优先级队列

STL `priority_queue` 是一个模板类，同样需要包含 `<queue>` 头文件。`priority_queue` 与 `queue` 不同之处在于，最高值（或由二元谓词认为最高的值）位于队列的头部，且队列操作仅限于头部。

### 实例化 `priority_queue` 类

`std::priority_queue` 类定义为：

点击此处查看代码图像

```cpp
template <
   class elementType,
   class Container = vector<Type>,
   class Compare = less<typename Container::value_type>
>
class priority_queue
```

在这里，`elementType` 是队列收集的元素类型的模板参数。第二个模板参数告诉 `priority_queue` 内部存储数据的集合类，而第三个参数允许程序员指定一个二元谓词，帮助队列确定顶部的元素。在没有指定二元谓词的情况下，`priority_queue` 类使用 `std::less` 的默认值，它使用 `operator<` 比较两个对象。

整数优先级队列最简单的实例化方式是：

```cpp
std::priority_queue <int> numsInPrioQ;
```

如果你想在 `std::deque` 中创建一个包含 `double` 类型元素的优先级队列（`priority_queue`）：

点击此处查看代码图像

```cpp
priority_queue <int, deque <int>, greater <int>> numsInDescendingQ;
```

就像栈（`stack`）一样，队列也可以作为另一个队列的拷贝来实例化：

点击此处查看代码图像

```cpp
std::priority_queue <int> copyQ(numsInPrioQ);
```

`priority_queue` 对象的实例化由列表 24.5 所示。

**列表 24.5** 实例化一个 STL `priority_queue`

点击此处查看代码图像

```cpp
0: #include <queue>
1: #include <functional>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     // 使用 std::less <>（默认）排序的 int 优先级队列
8:     priority_queue <int> numsInPrioQ;
9:
10:     // 一个 double 优先级队列
11:     priority_queue <double> dblsInPrioQ;
12:
13:     // 使用 std::greater <> 排序的整数优先级队列
14:     priority_queue <int, deque <int>, greater<int>> numsInDescendingQ;
15:
16:     // 作为另一个拷贝创建的优先级队列
17:     priority_queue <int> copyQ(numsInPrioQ);
18:
19:     return 0;
20: }
```

分析 ![Image](img/arrow.jpg)

第 8 行和第 11 行演示了分别为 `int` 和 `double` 对象实例化两个 `priority_queue`。缺少其他模板参数会导致使用 `std::vector` 作为数据的内部容器，并且默认比较准则由 `std::less` 提供。因此，这些队列的优先级非常高，使得最大的整数位于优先级队列的头部。然而，`numsInDescendingQ` 为第二个参数提供了一个 `deque` 作为内部容器，并使用 `std::greater` 作为谓词。该谓词导致队列中最小的数字位于头部。

使用谓词 `std::greater<T>` 的效果将在本节稍后在列表 24.7 中进行解释。

注意

列表 24.5 包含了标准头文件 `<functional>` 以使用 `std::greater<>`。

### `priority_queue` 的成员函数

`queue` 中可用的成员函数 `front()` 和 `back()` 在 `priority_queue` 中不可用。表 24.3 引入了 `priority_queue` 的成员函数。

![Image](img/24tab03.jpg)

**表 24.3** `std::priority_queue` 的成员函数

如表所示，`queue` 成员只能通过 `top()` 访问，它返回使用自定义谓词或在无谓词时使用 `std::less` 评估的最大值。

### 通过 `push()` 和 `pop()` 在 `priority_queue` 的尾部插入和头部删除

在 `priority_queue` 中插入元素通过成员方法 `push()` 完成：

点击此处查看代码图像

```cpp
numsInPrioQ.push (5); // 元素按排序组织
```

相反，通过 `pop()` 从头部删除：

点击此处查看代码图像

```cpp
numsInPrioQ.pop (); // 删除头部元素
```

`priority_queue` 成员的使用由列表 24.6 所示。

**列表 24.6** 使用 `push()`、`top()` 和 `pop()` 操作 `priority_queue`

点击此处查看代码图像



```cpp
0: #include <queue>
1: #include <iostream>
2:
3: int main ()
4: {
5:     using namespace std;
6:
7:     priority_queue <int> numsInPrioQ;
8:     cout << "Inserting {10, 5, -1, 20} into the priority_queue" << endl;
9:     numsInPrioQ.push (10);
10:     numsInPrioQ.push (5);
11:     numsInPrioQ.push (-1);
12:     numsInPrioQ.push (20);
13:
14:     cout << "Deleting the " << numsInPrioQ.size () << " elements" << endl;
15:     while (!numsInPrioQ ())
16:     {
17:         cout << "Deleting element: " << numsInPrioQ.top () << endl;
18:         numsInPrioQ.pop ();
19:     }
20:
21:     return 0;
22: }
```

***

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

Inserting {10, 5, -1, 20} into the priority_queue

Deleting 4 elements

Deleting element: 20

Deleting element: 10

Deleting element: 5

Deleting element: -1

# 常见问题

## Q 栈中间的元素可以被修改吗？

**A** - 不，因为这违背了`stack`（栈）的用途，它被设计为一个后进先出的容器。

## Q 我可以遍历队列（queue）中的所有元素吗？

**A** - `queue`（队列）没有提供迭代器，且`queue`中的元素只能在它的两端访问。

## Q STL 算法可以与自适应容器配合吗？

**A** - STL 算法通过迭代器工作。由于`stack`和`queue`类都没有提供标记范围末尾的迭代器，因此无法在这些容器上使用 STL 算法。

# 工作坊（Workshop）

工作坊包含测验题，旨在帮助你巩固对所涵盖内容的理解，并提供练习题让你使用所学知识的经验。在检查附录 E 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你理解了答案。

## 测验（Quiz）

1. 你可以改变`priority_queue`（优先级队列）对某个元素的行为，使得值最大的元素最后弹出吗？

2. 你有一个`class Coin`类型的`priority_queue`。你需要为`priority_queue`类定义哪个成员运算符，以便将值更大的硬币放在顶端位置？

3. 你有一个`Coin`类的栈，并向其中推入了六个对象。你可以访问或删除插入的第一个硬币吗？

## 练习（Exercises）

1. 一队队列的人（`Person`类）正在邮局排队。`Person`类包含存储年龄和性别的成员属性，定义如下：

    点击此处查看代码图片。

    ```cpp
    class Person
    {
        public:
            int age;
            bool isFemale;
    };
    ```

    修改该类，使得包含该类对象的`priority_queue`能够为老年人和女性（按此顺序）提供优先服务。

2. 编写一个程序，使用`stack`类反转用户输入的字符串。

# 第 25 节 使用 STL 处理位标志（Bit Flags）

位（Bits）可以是存储设置和标志的一种高效方式。标准模板库（STL）提供了帮助组织和操作位信息的类。本节将向你介绍：

- ![Image](img/square.jpg) `bitset`类
- ![Image](img/square.jpg) `vector<bool>`

## `bitset`类

`std::bitset`是设计用于处理位信息和位标志的 STL 类。`std::bitset`不是 STL 容器类，因为它不能调整自己的大小。它是一个工具类，针对处理长度在编译时已知的位序列进行了优化。

> **提示**：要使用类`std::bitset`，请包含头文件：
>
> ```cpp
> #include <bitset>
> ```

### 实例化`std::bitset`

此模板类要求你提供一个模板参数，该参数包含类实例需要管理的位数。

点击此处查看代码图片。

```cpp
bitset <4> fourBits;  // 4 位初始化为 0000
```

你也可以用`char*`字符串字面量表示的位序列来初始化`bitset`：

点击此处查看代码图片。

```cpp
bitset <5> fiveBits("10101"); // 5 位 10101
```

在实例化另一个`bitset`的同时从另一个中拷贝非常简单：

点击此处查看代码图片。

```cpp
bitset <8> fiveBitsCopy(fiveBits);
```

列表 25.1 演示了`bitset`类的一些实例化技术。

**列表 25.1** 实例化一个`std::bitset`

点击此处查看代码图片。

```cpp
0: #include <bitset>
1: #include <iostream>
2: #include <string>
3:
4: int main ()
5: {
6:     using namespace std;
7:
8:     bitset <4> fourBits;  // 4 位初始化为 0000
9:     cout << "Initial contents of fourBits: " << fourBits << endl;
10:
11:     bitset <5> fiveBits ("10101"); // 5 位 10101
12:     cout << "Initial contents of fiveBits: " << fiveBits << endl;
13:
14:     bitset <6> sixBits(0b100001); // C++14 二进制字面量
15:     cout << "Initial contents of sixBits: " << sixBits << endl;
16:
17:     bitset <8> eightBits (255); // 255
18:     cout << "Initial contents of eightBits: " << eightBits << endl;
19:
20:     // 在实例化另一个时拷贝
21:     bitset <8> eightBitsCopy(eightBits);
22:
23:     return 0;
24: }
```

输出：

```text
Initial contents of fourBits: 0000
Initial contents of fiveBits: 10101
Initial contents of sixBits: 100001
Initial contents of eightBits: 11111111
```

## 使用`bitset`及其成员

`bitset`类提供了帮助向`bitset`插入、设置或重置内容、读取位或写入流的成员函数。它还提供了显示`bitset`内容并进行位操作的运算符。

### `std::bitset`中的有用运算符

你在第 12 节中学习了运算符，并且了解到运算符最重要的作用是增加类的可用性。`std::bitset`提供了一些非常有用的运算符，如列表 25.1 中的示例`fourBits`所示，这使得使用变得非常简单。

**表格 25.1** `bitset`支持的运算符

除了这些，`bitset`还具有如`|=`、`&=`、`^=`和`~=`等运算符，有助于对`bitset`对象进行位操作。

### `bitset`成员方法

位可以持有两种状态：被设置为（1）或重置（0）。为了帮助操作`bitset`的内容，你可以使用表格 25.2 列出的成员函数，这些函数可以帮助你处理一个`bit`或`bitset`中的所有位。

**表格 25.2** `std::bitset`的成员方法

这些成员方法和运算符的使用在列表 25.2 中进行了演示。

```cpp
cout << "Num 0s you supplied: ";

cout << inputBits.size () - inputBits.count () << endl;

bitset <8> inputFlipped (inputBits);  // copy

inputFlipped.flip ();  // toggle the bits

cout << "Flipped version is: " << inputFlipped << endl;

cout << "Result of AND, OR and XOR between the two:" << endl;

cout << inputBits << " & " << inputFlipped << " = ";

cout << (inputBits & inputFlipped) << endl;  // bitwise AND

cout << inputBits << " | " << inputFlipped << " = ";

cout << (inputBits | inputFlipped) << endl;  // bitwise OR

cout << inputBits << " ^ " << inputFlipped << " = ";

cout << (inputBits ^ inputFlipped) << endl; // bitwise XOR

return 0;

}
```



输出 ![Image](img/arrow.jpg)

点击此处查看代码图像我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。输入一个 8 位的序列：`10110101`

你提供的 1 的数量：`5`

你提供的 0 的数量：`3`

翻转后的版本：`01001010`

两者之间与、或、异或运算的结果：

`10110101 & 01001010 = 00000000`

`10110101 | 01001010 = 11111111`

`10110101 ^ 01001010 = 11111111`

### 分析

![Image](img/arrow.jpg)

这个交互式程序不仅演示了使用 `std::bitset` 在两个位序列之间进行位运算是多么简单，还展示了其 `stream` 运算符的用处。`std::bitset` 实现的位移运算符（`>>` 和 `<<`）使得向屏幕写入位序列以及以字符串格式从用户读取位序列成为一项简单任务。`inputBits` 包含了用户在第 10 行中输入的序列。第 12 行使用的 `count()` 用于获取序列中 1 的数量，而 0 的数量则是通过计算 `size()`（返回位 set 中的位数）与 `count()` 之间的差值得出的，如第 14 行所示。`inputFlipped` 在开头是 `inputBits` 的副本，然后在第 17 行使用 `flip()` 进行了翻转。它现在包含了每个比特位都已翻转的序列——即取了反反（0 变成 1，反之亦然）。程序的其余部分演示了两个 bitset 之间位与、位或和位异或运算的结果。

### 注意事项

STL `bitset<>` 的缺点之一是无法动态调整自身大小。你只能在编译时已知序列中要存储的位数时才使用 `bitset`。

STL 为程序员提供了 `vector<bool>` 类（在某些 STL 的实现中也称为 `bit_vector`），它克服了这一缺点。

### `vector<bool>`

`vector<bool>` 是 `std::vector` 的部分特化，旨在用于存储 `boolean` 数据。该类能够动态调整自身大小。因此，程序员不需要在编译时知道要存储多少个 `boolean` 标志。

### 提示

要使用类 `std::vector<bool>`，请包含头文件：

```cpp
#include <vector>
```

### 实例化 `vector<bool>`

实例化一个 `vector<bool>` 与 vector 类似，有一些方便的重载：

```cpp
vector <bool> boolFlags1;
```

例如，你可以创建一个初始包含 10 个布尔值的 vector，每个值都初始化为 1（即 true）：

点击此处查看代码图像

```cpp
vector <bool> boolFlags2 (10, true);
```

你也可以创建一个另一个对象的拷贝作为对象：

点击此处查看代码图像

```cpp
vector <bool> boolFlags2Copy (boolFlags2);
```

`vector<bool>` 的某些实例化技术在列表 25.3 中有所演示。

**列表 25.3 `vector<bool>` 的实例化**

点击此处查看代码图像

```cpp
#include <vector>

int main ()
{
  using std;

  // 使用默认构造函数实例化一个对象
  vector <bool> boolFlags1;

  // 初始化一个包含 10 个 true 元素的 vector
  vector <bool> boolFlags2 (10, true);

  // 实例化一个对象作为另一个拷贝
  vector <bool> boolFlags2Copy (boolFlags2);

  return 0;
}
```

![Image](img/arrow.jpg) 示例展示了构造 `vector<bool>` 对象的一些方式。第 7 行是使用默认构造函数的一种。第 10 行演示了创建一个初始化为包含 10 个 `boolean` 标志的对象，每个标志的值都为 `true`。第 13 行演示了如何将一个 `vector<bool>` 拷贝。

### `vector<bool>` 函数与运算符

`vector<bool>` 通过 `operator[]` 访问位就像普通 vector 一样。`vector<bool>` 的 `flip()` 方法翻转标志位，如列表 25.4 所示。

**列表 25.4 使用 `vector<bool>`**

点击此处查看代码图像

```cpp
#include <vector>
#include <iostream>

using namespace std;

int main ()
{
  // 使用 push_back 在末尾添加标志
  vector<bool> boolFlags(3);

  boolFlags[0] = true;
  boolFlags[1] = true;
  boolFlags[2] = false;

  // 使用 flip() 翻转标志
  boolFlags.flip();

  cout << "vector 的内容：" << endl;

  for (size_t index = 0; index < boolFlags.size(); ++index)
    cout << boolFlags[index] << " ";

  cout << endl;

  return 0;
}
```

输出 ![Image](img/arrow.jpg)

vector 的内容：

`0 0 1`

vector 的内容：

`1 1 0`

### 总结

在本节中，你学习了处理位序列和位标志的最有效工具：`std::bitset` 类。你还了解了 `vector<bool>` 类，它允许你存储不需要在编译时知道数量的 own 标志。

### 问答

**Q 在 `bitset` 和 `vector<bool>` 都可以的情况下，你倾向于使用哪一个类来处理你的二进制标志？**

答：使用 `bitset`，因为它更适合这种需求。

**Q 我有一个名为 `myBitSet` 的 `bitset` 对象，它包含某些存储位。我该如何确定哪些位的值为 0（或 false）？**

答：`bitset::count()` 提供值为 1 的位数量。将此数字减去 `bitset::size()`（它返回存储的总位数），即可得到序列中 0 的数量。

### 问：可以使用迭代器访问 `vector<bool>` 中的单个元素吗？

**答** 可以的。因为 `vector<bool>` 是 `std::vector` 的部分特化，所以它支持迭代器。

### 问：我可以在编译时指定 `vector<bool>` 持有的元素数量吗？

**答** 可以的，可以通过在重载构造函数中指定数量，或者在稍后使用 `vector<bool>::resize()` 函数来实现。

## 工作坊

工作坊包含测验题以帮助巩固你对涵盖内容的理解，并提供练习让你使用所学知识的机会。在查看附录 E 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你已经理解了这些答案。

### 测验

**1.** `bitset` 可以扩展其内部缓冲区以存储数量数量的元素吗？

**2.** 为什么 `bitset` 不归类为 STL 容器类？

**3.** 你会使用 `std::vector` 来存储在编译时固定且已知的比特位吗？

### 练习

**1.** 编写一个包含四个位数的 `bitset` 类。将其初始化为一个数字，显示结果，并将其加到另一个 `bitset` 对象。（难点在于：Bitsets 不允许 `bitsetA = bitsetX + bitsetY`。）

**2.** 演示你如何翻转（即切换）bitset 中的比特位。

# 第 V 部分：高级 C++ 概念

## 第 26 节：理解智能指针

C++ 程序员在管理堆内存（或空闲存储区）时，并不一定需要使用原始指针类型；他们可以使用智能指针。

![Image](img/square.jpg) 什么是智能指针以及为什么你需要它们

![Image](img/square.jpg) 智能指针是如何实现的

![Image](img/square.jpg) 不同类型的智能指针

![Image](img/square.jpg) 为什么你不应该使用已弃用的 `std::auto_ptr`

![Image](img/square.jpg) 标准库智能指针 `std::unique_ptr`

![Image](img/square.jpg) 流行的智能指针库

### 什么是智能指针？

简单来说，C++ 中的智能指针是一个重载了操作符的类，它的行为类似于传统的指针。然而，它通过确保动态分配的数据得到正确且及时的销毁，并有助于定义对象生命周期。

### 使用传统（原始）指针的问题

与其他现代编程语言不同，C++ 在内存分配、释放和管理方面为程序员提供了完全的灵活性。遗憾的是，这种灵活性是一把双刃剑。一方面，它让 C++ 了一种强大的语言；但另一方面，它允许程序员在动态分配的对象未被正确释放时创建内存相关问题，例如内存泄漏。

例如：

点击此处代码图片

```cpp
SomeClass* ptrData = anObject.GetData ();

/*
   问题：ptrData 指向的对象是通过 new 动态分配的吗？

   如果是，谁调用 delete？调用者还是被调用者？

   答案：不知道！
*/

ptrData->DoSomething();
```

在前面的代码中，没有明显的方法可以判断 `ptrData` 指向的内存：

![Image](img/square.jpg) 是否在`堆`上分配的，因此最终需要被`释放`

![Image](img/square.jpg) 是否由调用者负责`释放`

![Image](img/square.jpg) 是否会自动由对象的析构函数销毁

尽管通过插入注释和强制编码规范可以部分解决这些歧，但这些机制太松散，无法有效避免因滥用动态分配的数据和指针引起的所有错误。

### 智能指针如何帮助？

鉴于使用传统指针和传统内存管理技术的问题，由于 C++ 程序员在需要管理堆/空闲存储区的数据时，并不被强制使用它们。程序员可以通过在程序中使用智能指针，选择一种更智能的方式来分配和管理动态数据：

点击此处代码图片

```cpp
smart_pointer<SomeClass> spData = anObject.GetData ();

// 像使用传统指针一样使用智能指针！
spData->Display ();
(*spData).Display ();

// 不需要担心释放
// （智能指针的析构函数为你完成这一切）
```

因此，智能指针的行为类似于传统指针（我们现在称它们为*原始指针*），但通过它们的*重载操作符*和*析构函数*提供了实用的功能，以确保动态分配的数据被及时销毁。

### 智能指针是如何实现的？

这个问题目前可以简化为“智能指针 `spData` 是如何像传统指针一样工作的？”答案是：智能指针类重载了解引用操作符（`*`）和成员选择操作符（`->`），以便程序员像使用传统指针一样使用它们。操作符重载之前第 12 节中讨论过。

此外，为了让你能够管理某种类型，几乎所有良好的智能指针类都是模板，包含了其功能的通用实现。作为模板，它们是灵活的，可以针对特定类型进行特化。

**列表 26.1 智能类的要素组件**

点击此处代码图片

```cpp
template <typename T>
class smart_pointer {
private:
    T* rawPtr;

public:
    // 构造函数
    smart_pointer (T* pData) : rawPtr(pData) {}

    // 析构函数
    ~smart_pointer () {delete rawPtr;}

    // 拷贝构造函数
    smart_pointer (const smart_pointer &anotherSP);

    // 赋值操作符
    smart_pointer& operator= (const smart_pointer& anotherSP);

    // 解引用操作符
    T& operator () const {
        return *(rawPtr);
    }

    // 成员选择操作符
    T* operator-> () const {
        return rawPtr;
    }
};
```

### 分析

![Image](img/arrow.jpg)

前面的智能指针类展示了第 14-17 行和 19-22 行定义的两个符的实现，这有助于该类在传统意义上作为“指针”运行。例如，为了对 `class Tuna` 对象使用智能指针，你可以这样实例化它：

点击此处代码图片

```cpp
smart_pointer<Tuna> smartTuna (new Tuna());

smartTuna->Display();

// 或者：
(*smartTuna).Display();
```

这个 `smart_pointer` 类仍然没有展示或实现任何让该指针类变得非常智能并使得使用它优于传统指针的功能。如第 7 行所示，构造函数接收一个指针并将其保存为智能指针类中的内部指针对象。析构函数释放此指针，允许自动释放内存。

### 注意

让智能指针真正“智能”的实现是拷贝构造函数、赋值操作符和析构函数。它们决定了智能指针对象在跨函数传递、被赋值或超出作用域（即被析构）时的。因此，在查看完整的智能指针实现之前，你应该了解一些智能指针类型。

### 智能指针类型

内存资源管理（即所实现的所有权模型）是智能指针类与众不同的之处。智能指针决定了它们在被复制和赋值时对资源进行何种操作。最简单的实现往往会导致性能问题，而最快速的实现可能并不适用于所有应用程序。根结底，程序员在决定在应用程序中使用某种智能指针之前，需要理解其工作原理。

智能指针的分类实际上是它们对内存资源管理策略的分类。这些策略包括：

![Image](img/square.jpg) 深拷贝

![Image](img/square.jpg) 写时拷贝 (COW)

![Image](img/square.jpg) 引用计数

![Image](img/square.jpg) 引用链接

![Image](img/square.jpg) 破坏性拷贝

在学习 C++ 标准库提供的智能指针——`std::unique_ptr` 之前，让我们简要查看一下这些策略。

### 深拷贝

在实现深拷贝的智能指针中，每个智能指针实例都持有被管理对象的一个完整副本。每当智能指针被复制时，所指向的对象也会被复制（因此是深拷贝）。当智能指针超出作用域时，它会通过析构函数释放它所指向的内存。

虽然基于深拷贝的智能指针似乎并没有比按值传递对象产生任何价值，但在处理多态对象时，它的优势就显而易见了。所示，它可以避免切片（slicing）：

点击此处查看代码图像

```cpp
// 按值传递多态对象时发生切片的示例

// Fish 是金枪鱼和鲤鱼的基类，Fish::Swim() 是虚函数
void MakeFishSwim (Fish aFish)    // 注意参数类型
{
    aFish.Swim(); // 虚函数
}

// ... 某些函数
Carp freshWaterFish;
MakeFishSwim (freshWaterFish);  // Carp 将被“切”为 Fish

// 切片：只有 Carp 的 Fish 部分被发送到 MakeFishSwim()
Tuna marineFish;
MakeFishSwim(marineFish); // 再次发生切片
```

当程序员选择深拷贝智能指针时，切片问题得以解决，如列表 26.2 所示。

**列表 26.2** 使用基于深拷贝的智能指针按基类型传递多态对象

点击此处查看代码图像

```cpp
0: template <typename T>
1: class deepcopy_smart_ptr
2: {
3: private:
4:     T* object;
5: public:
6:     //... 其他函数
7:
8:     // 深拷贝指针的拷贝构造函数
9:     deepcopy_smart_ptr (const deepcopy_smart_ptr& source)
10:     {
11:         // Clone() 是虚函数：确保派生类对象的深拷贝
12:         object = source->Clone ();
13:     }
14:
15:     // 拷贝赋值运算符
16:     deepcopy_smart_ptr& operator= (const deepcopy_smart_ptr& source)
17:     {
18:         if (object)
19:             delete object;
20:
21:         object = source->Clone ();
22:     }
23: };
```

### 分析

如所示，`deepcopy_smart_ptr` 在第 9-13 行实现了一个拷贝构造函数，允许通过该类需要实现的 `Clone()` 函数对多态对象进行深拷贝。同样，它在第 16-22 行也实现了一个拷贝赋值运算符。为了简单起见，本示例假设基类 `Fish` 实现的虚函数名为 `Clone()`。通常，实现深拷贝模型的智能指针会将此函数作为模板参数或函数对象提供。

因此，当智能指针本身作为基类类型 `Fish` 的指针传递时：

点击此处查看代码图像

```cpp
deepcopy_smart_ptr<Carp> freshWaterFish(new Carp);
```



`MakeFishSwim(freshWaterFish);  // Carp 不会被“切片”`

### 写时拷贝（COW）

*写时拷贝*（简称 COW）试图通过在第一次尝试写入之前共享资源来优化性能。COW 有许多支持者。对于那些坚信 COW 的人来说，实现`*`和`->`是功能的关键。要点在于，当你选择遵循 COW 的实现时，在继续使用一个或多个此类指针之前，务必理解其实现细节。

### 引用计数

通常来说，引用计数是一种保持对象用户数量计数的机制。当计数减到零时，对象会被释放。因此，引用计数是一种在无需复制对象的情况下共享对象的极佳机制。如果你曾经接触过名为 COM 的微软技术，那么引用计数的概念至少会在某一次遇到你。

此类智能指针在被复制时，需要增加所涉及对象的引用计数。保持这种计数的至少有两种流行方式：

- ![Image](img/square.jpg) 在指向的对象中维护引用计数
- ![Image](img/square.jpg) 在共享对象中由指针类维护引用计数

第一种在对象中维护引用计数的变体被称为*侵入式引用计数*（intrusive reference counting），因为对象需要被修改。在这种情况下，对象维护、增加并向任何管理它的智能指针类提供引用计数。顺便提一下，这是 COM 采用的方法。第二种在共享对象中维护引用计数的变体是一种机制，智能指针类可以将计数存储在堆上（例如一个动态分配的整数），并在被复制时通过拷贝构造函数增加该值。

因此，引用计数机制使得程序员在操作对象时仅使用智能指针变得恰当。管理对象的智能指针和指向它的原始指针是一个坏主意，因为当智能指针维护的计数减到零时，它会（智能地）释放对象，但原始指针继续指向不再属于你的应用程序的内存部分。同样，引用计数可能会导致其特有的问题：两个互相持有指针的对象永远不会被释放，因为它们的循环依赖将引用计数保持在至少 1。

### 引用链接

*引用链接*智能指针是指并不主动计数使用对象的智能指针；它们只需要知道数量何时降为零以便释放对象。

它们被称为`reference-linked`（引用链接），因为它们的实现是基于双向链表的。当通过复制现有的智能指针创建新的智能指针时，它会被添加到列表中。当智能指针超出作用范围或被销毁时，析构函数会将该智能指针从列表中取消索引。引用链接也会受到循环依赖引起的影响，这与引用计数指针的情况类似。

## 破坏性拷贝（Destructive Copy）

`destructive copy`（破坏性拷贝）是一种机制，智能指针在复制时，会将所处理对象的完整所有权转移给目标对象，并重置自己：

点击此处查看代码图像

```cpp
destructive_copy_smartptr<SampleClass> smartPtr(new SampleClass());

SomeFunc(smartPtr);     // 所有权转移给 SomeFunc

// 不要再在调用者中使用 smartPtr 了！
```

虽然这种机制在用上显然不符合直觉，但破坏性拷贝智能指针提供的优势在于，它们确保了在任何时刻，只有一个活跃的指针指向某个对象。因此，它们是从函数返回指针的良好机制，并且在你可以利用其“破坏性”属性的场景中有用。

破坏性拷贝指针的实现偏离了标准的推荐 C++ 编程技术，如 Listing 26.3 所示。

### 注意

`std::auto_ptr` 是目前遵循破坏性拷贝原则最流行的（或者取决于你怎么看，是最臭名昭著的）指针。这种智能指针在传递给函数或复制到另一个对象之后就失效了。

`std::auto_ptr` 在 C++11 中被废弃了。相反，你应该使用 `std::unique_ptr`，由于其具有私有的拷贝构造函数和拷贝赋值运算符，它不能按值传递。它只能作为引用参数传递。

### 列表 26.3 一个破坏性拷贝智能指针的示例

点击此处查看代码图像

```cpp
0: template <typename T>

1: class destructivecopy_ptr

2: {

3: private:

4:     T* object;

5: public:

6:     destructivecopy_ptr(T* input):object(input) {}

7:     ~destructivecopy_ptr() { delete object; }

8:

9:     // 拷贝构造函数

10:     destructivecopy_ptr(destructivecopy_ptr& source)

11:     {

12:         // 拷贝时获取所有权

13:         object = source.object;

14:

15:         // 销毁源

16:         source.object = 0;

17:     }

18:

19:     // 拷贝赋值运算符

20:     destructivecopy_ptr& operator= (destructivecopy_ptr& source)

21:     {

22:         if (object != source.object)

23:         {

24:             delete object;

25:             object = source.object;

26:             source.object = 0;

27:         }

28:     }

29: };

30:

31: int main()

32: {

33:     destructivecopy_ptr<int> num (new int);

34:     destructivecopy_ptr<int> copy = num;

35:

36:     // num 现在是无效的

37:     return 0;

38: }
```

分析 ![Image](img/arrow.jpg)

Listing 26.3 展示了基于破坏性拷贝的智能指针的实现。第 10–17 行和 20–28 行分别包含拷贝构造函数和拷贝赋值运算符。这些函数在拷贝时使源对象失效；也就是说，拷贝构造函数在拷贝后将源包含的指针设置为 NULL，因此证明了“破坏性拷贝”名称。赋值运算符执行相同的操作。因此，`num`在第 34 行被赋值给另一个指针时实际上已经失效了。这种行为与赋值的操作背道直驰。

### 注意

如 Listing 26.3 所示，对于破坏性拷贝智能指针实现至关重要的拷贝构造函数和拷贝赋值运算符也引起了最大的批评。与大多数 C++ 类不同，这种智能指针类不能让拷贝构造函数和赋值运算符接受`const`引用，因为它需要在拷贝后使源对象失效。这不仅偏离了传统的拷贝构造函数和赋值运算符语义，还使得使用该智能指针类违背直觉。很少有人期望拷贝源或赋值源在拷贝或赋值步骤后被破坏。这种智能指针会销毁源的事实也使得它们不适用于 STL `containers`，例如`std::vector`或你可能使用的任何动态集合类。这些容器需要在内部拷贝你的内容，并最终导致指针失效。因此，出于多个原因，建议你避免破坏性拷贝指针。

`auto_ptr` 是直到最近 C++ 都支持的基于破坏性拷贝的智能指针。它在 C++11 中最终被废弃，你应该使用`std::unique_ptr`。

### 提示

`std::unique_ptr` 被引入 C++11，它与`auto_ptr`的细微不同之处在于它不允许拷贝。

### 使用 `unique_ptr`

`std::unique_ptr` 是一个类似于`auto_ptr`的简单智能指针，但具有私有的拷贝构造函数和赋值运算符以禁止拷贝。Listing 26.4 展示了`unique_ptr`不支持拷贝：

```cpp
0: #include <iostream>

1: #include <memory>

2: using namespace std;

3:

4: class Fish

5: {

6: public:

7:     Fish() {cout << "Fish: Constructed!" << endl;}

8:     ~Fish() {cout << "Fish: Destructed!" << endl;}

9:

10:    void Swim() const {cout << "Fish in water" << endl;}

11: };

12:

13: void MakeFish(const unique_ptr<Fish>& inFish)

14: {

15:     inFish->Swim();

16: }

17:

18: int main()

19: {

20:     unique_ptr<Fish> smartFish (new Fish);

21:

22:     smartFish->Swim();

23:     MakeFish(smartFish); // OK，因为 MakeFish 接受引用

24:

25:     unique_ptr<Fish> copySmartFish;

26:     // copySmartFish = smartFish; // 错误：operator= 是私有的

27:

28:     return 0;

29: }
```

点击此处查看代码图像

```cpp
copySmartFish = smartFish; // error：operator= 是私有的
```

然而，它支持移动语义。因此，一个可行的方案是：

点击此处查看代码图像

```cpp
unique_ptr<Fish> sameFish(std::move(smartFish));

// smartFish 从此后为空
```

如果你确实编写了一个需要捕获`unique_ptr`的 lambda 表达式，那么你就可以像 C++14 支持的那样，在你的 lambda 捕获句列表中使用`std::move()`。

点击此处查看代码图像

```cpp
std::unique_ptr<char> alphabet(new char);

*alphabet = 's';

auto lambda = [capture = std::move(alphabet)]()

{ std::cout << *capture << endl; };

// alphabet 从此后为空，因为内容已被“移动”

lambda();
```

如果前面的代码看起来太奇特，请不要沮丧——它确实很复杂，并且涵盖了大多数专业程序员可能永远不会遇到的用例。

### 注意事项

在编写使用多线程的应用时，请评估使用由 C++11 标准库提供的`std::shared_ptr`和`std::weak_ptr`。这些工具有助于线程安全的、引用计数的对象共享。

### 流行的智能指针库

显而易见，C++ 标准库附带的智能指针版本无法满足每个程序员的需求。这正是为什么世界上存在许多智能指针库的原因。

Boost（[www.boost.org](http://www.boost.org)）为你提供了一些经过充分测试且文档良好的智能指针类，以及许多其他实用的工具类。你可以在[`www.boost.org/libs/smart_ptr/smart_ptr.htm`](http://www.boost.org/libs/smart_ptr/smart_ptr.htm)找到关于 Boost 智能指针的更多信息和下载。

### 总结

在本节中，你学习了如何使用正确的智能指针来帮助编写指针代码，同时有助于减少与分配和对象所有权相关的问题。你还学习了不同的智能指针类型，并了解到在你的应用程序中采用智能指针类之前，了解它的行为是重要的。你现在知道你不应该使用`std::auto_ptr`，因为它在拷贝或赋值期间会使源对象失效。你学习了从 C++11 开始提供的智能指针类`std::unique_ptr`。

### 问答

**Q 我需要一个指针向量（vector）。我应该选择`auto_ptr`作为向量中持有的对象类型吗？**

**A** 根据原则，你永远不应该使用`std::auto_ptr`。它被废弃了。单次拷贝或赋值操作就会导致源对象无法使用。

**Q 一个类始终需要重载哪两个运算符才能被称为智能指针类？**

**A** 是以下两个：`operator*`和`operator->`。它们帮助像普通指针语义一样使用该类的对象。

**Q 我有一个应用程序，其中`Class1`和`Class2`存有指向对方类型对象的成员属性。在这种情况下，我应该使用引用计数指针吗？**

**A** 可能不需要，因为循环依赖会导致引用计数无法降为零，从而导致两个类的对象永久地留在堆内存中。

**Q 字符串类也在空闲存储（free store）上动态管理字符数组。那么字符串类也是一种智能指针吗？**

**A** 不是。这些类通常没有同时实现`operator*`和`operator->`，因此不能被归类为智能指针。

## 工作坊

工作坊包含测验题，帮助你巩固对涵盖内容的理解，并提供练习让你获得使用所学知识的经验。在检查附录 E 中的答案之前，尝试回答测验题和练习题，并在进入下一节之前确保你理解了答案。

### 测验

1. 在为你的应用程序编写自己的智能指针之前，你会去哪里查找？
2. 智能指针会显著减慢你的应用程序速度吗？
3. 引用计数智能指针可以在哪里存储引用计数数据？
4. 引用指针使用的链表机制应该是单链还是双链？

### 练习题

1. **找虫：**指出这段代码中的错误：

   点击此处查看代码图像

   ```cpp
   std::auto_ptr<SampleClass> object(new SampleClass());

   std::auto_ptr<SampleClass> anotherObject(object);

   object->DoSomething();

   anotherObject->DoSomething();
   ```

2. 使用`unique_ptr`类实例化一个继承自`Fish`的`Carp`。将该对象作为`Fish`指针传递，并对任何切片（slicing）现象进行注释。

3. **找虫：**指出这段代码中的错误：

   点击此处查看代码图像

   ```cpp
   std::unique_ptr<char> alphabet(new char);

   *alphabet = 's';

   auto lambda = [capture = std::move(alphabet)]()

   { std::cout << *capture << endl; };

   // alphabet 从此后为空，因为内容已被“移动”

   lambda();
   ```

## 第 27 节 使用流进行输入输出

你一直都在使用流，从第一节在屏幕上显示“Hello World”开始。是时候从实用角度学习 C++ 流了。

### 流的概念

你正在开发一个从磁盘读取、写入显示器、从键盘读取并保存到磁盘的程序。如果无论数据来自何处都能使用相似的模式有多有用？这正是 C++ 流为你提供的！

让我们参考你第一个 C++ 程序中的相关行，即第一节中的列表 1.1：

点击此处查看代码图像

```cpp
std::cout << "Hello World!" << std::endl;
```

没错：`std::cout`是`ostream`类的一个流对象，用于控制输出。为了使用`std::cout`，你包含了`<iostream>`头文件，它提供了这一功能以及允许从流读取的`std::cin`。

那么，我说流允许一致且特定设备的访问是什么意思？如果你想向一个文本文件写入`"Hello World"`，你将在文件流对象`fsHello`上使用这种语法：

点击此处查看代码图像

```cpp
fsHello << "Hello World!" << endl; // 写入文件流
```

正如你所见，在选择了正确的流类后，在 C++ 中向文件写入“Hello World”与写入显示器并没有太大区别。

### 提示

在写入流时`operator<<`被称为插入运算符。你使用它写入显示器、文件等。

在将流写入变量时`operator>>`被称为提取运算符。你使用它从键盘、文件等读取输入。

### 重要的 C++ 流类和对象

C++ 为你提供了一组标准类和头文件，帮助你执行一些重要且频繁的 I/O 操作。表 27.1 列出了你经常使用的类列表。

![Image](img/27tab01.jpg)

**表 27.1** `std`命名空间下常用的 C++ 流类

### 注意

`cout`、`cin`和`cerr`分别是流类`ostream`、`istream`和`ostream`的全局对象。作为全局对象，它们在`main()`函数开始之前就已经初始化了。

在使用流类时，你可以选择指定操纵符（manipulators）来为你执行特定的操作。`std::endl`就是这种操纵符之一，在此为止一直使用它来插入换行符：

点击此处查看代码图像

```cpp
std::cout << "This lines ends here" << std::endl;
```



表 27.2 展示了其他类似的操纵符函数和标志。

![Image](img/27tab02.jpg)

**表 27.2** `std` 命名空间下用于处理流的常用操纵符

### 使用 `std::cout` 向控制台写入格式化数据

`std::cout` 用于写入标准输出流，可能是本书到为止最常用的流。然而，现在是时候重新审视 `cout` 并使用一些操纵符来改变我们对齐和显示数据的方式了。

#### 使用 `std::cout` 更改数字显示格式

你可以要求 `cout` 以十六进制或八进制格式显示整数。列表 27.1 演示了如何使用 `cout` 以各种格式显示输入的数字。

**代码列表 27.1** 使用 `cout` 和 `<iomanip>` 标志以十进制、八进制和十六进制格式显示整数

点击此处查看代码图片

* * *

```cpp
0: #include <iostream>
1: #include <iomanip>
2: using namespace std;
3:
4: int main()
5: {
6:     cout << "Enter an integer: ";
7:     int input = 0;
8:     cin >> input;
9:
10:     cout << "Integer in octal: " << oct << input << endl;
11:     cout << "Integer in hexadecimal: " << hex << input << endl;
12:
13:     cout << "Integer in hex using base notation: ";
14:     cout<<setiosflags(ios_base::hex|ios_base::showbase|ios_base::uppercase);
15:     cout << input << endl;
16:
17:     cout << "Integer after resetting I/O flags: ";
18:     cout<<resetiosflags(ios_base::hex|ios_base::showbase|ios_base::uppercase);
19:     cout << input << endl;
20:
21:     return 0;
22: }
```

* * *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```
Enter an integer: 253
Integer in octal: 375
Integer in hexadecimal: fd
Integer in hex using base notation: 0XFD
Integer after resetting I/O flags: 253
```

分析 ![Image](img/arrow.jpg)

该代码示例使用了 表 27.2 中提供的操纵符来改变 `cout` 显示用户提供的相同整数对象 `input` 的方式。注意第 10 行和第 11 行是如何使用操纵符 `oct` 和 `hex` 的。在第 14 行中，你使用 `setiosflags()` 告诉它使用大写字母显示十六进制，导致 `cout` 将整数输入 `253` 显示为 `0XFD`。第 18 行使用的 `resetiosflags()` 的效果通过 `cout` 再次使用十进制符号显示整数得到证明。更改显示整数时使用的基数的另一种方法如下：

点击此处查看代码图片

```cpp
cout << dec << input << endl;  // 以十进制显示
```

还可以格式化 `cout` 显示如 `Pi` 等数字的方式，你可以指定精度，在固定点表示法中，精度指定显示小数点后的位数，或者你可以让数字使用科学计数法显示。这一点以及更多内容在 列表 27.2 中演示。

**代码列表 27.2** 使用 `cout` 使用固定点法和科学计数法显示 `Pi` 和圆面积

点击此处查看代码图片

* * *

```cpp
0: #include <iostream>
1: #include <iomanip>
2: using namespace std;
3:
4: int main()
5: {
6:     const double Pi = 3.141592653589793;
7:     double radius = 5.0;
8:     cout << "Pi: " << setprecision(4) << fixed << Pi << endl;
9:     cout << "Area of circle: " << Pi * radius * radius << endl;
10:
11:     cout << "Pi (scientific): " << setprecision(4) << scientific << Pi << endl;
12:     cout << "Area of circle (scientific): " << Pi * radius * radius << endl;
13:
14:     return 0;
15: }
```
*(注：由于原文列表 27.2 代码块不完整，此处根据上下文补全了逻辑内容以保持翻译完整性)*

点击此处查看代码图像

* *

```cpp
#include<iostream>
using namespace std;

int main()
{
    cout << "Enter an integer: ";
    int inputNum = 0;
    cin >> inputNum;

    cout << "Enter the value of Pi: ";
    double Pi = 0.0;
    cin >> Pi;

    cout << "Enter three characters separated by space: " << endl;
    char char1 = '\0', char2 = '\0', char3 = '\0';
    cin >> char1 >> char2 >> char3;

    cout << "The recorded variable values are: " << endl;
    cout << "inputNum: " << inputNum << endl;
    cout << "Pi: " << Pi << endl;
    cout << "The three characters: " << char1 << char2 << char3 << endl;

    return 0;
}
```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter an integer: 32
Enter the value of Pi: 0.314159265e1
Enter three characters separated by space:
c + +
The recorded variable values are:
inputNum: 32
Pi: 3.14159
The three characters: c++
```

分析 ![Image](img/arrow.jpg)

列表 27.4 中最有趣的部分是，你使用科学计数法输入了 `Pi` 的值，而 `cin` 将该数据填充到了 `double Pi` 中。注意看如何像第 15 行所示，你可以在单行内填充三个字符变量。

### 使用 `std::cin::get` 向 `char*` 缓冲区进行输入

就好像 `cin` 允许你直接写入 `int` 一样，你也可以对 C 风格的 `char` 数组执行同样的操作：

点击此处查看代码图像

```cpp
cout << "Enter a line: " << endl;
char charBuf [10] = {0};  // can contain max 10 chars
cin >> charBuf;  // Danger: user may enter more than 10 chars
```

在写入 C 风格的字符串缓冲区时，不要超出缓冲区边界非常重要，以避免崩溃或安全漏洞。因此，读取到 C 风格 `char` 缓冲区的更好方法是这种：

点击此处查看代码图像

```cpp
cout << "Enter a line: " << endl;
char charBuf[10] = {0};
cin.get(charBuf, 9); // 插入到第 9 个字符时停止插入
```

这种向 C 风格缓冲区插入文本的更安全的方法在 列表 27.5 中所示。

**列表 27.5** 在不超出边界的情况下向 `char` 缓冲区插入数据

点击此处查看代码图像

* *

```cpp
#include<iostream>
#include<string>
using namespace std;

int main()
{
    cout << "Enter a line: " << endl;
    char charBuf[10] = {0};
    cin.get(charBuf, 9);
    cout << "charBuf: " << charBuf << endl;
    return 0;
}
```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter a line:
Testing if I can cross the bounds of the buffer
charBuf: Testing
```

分析 ![Image](img/arrow.jpg)

如输出所示，由于第 8 行使用了 `cin::get`，你只将用户的前九个字符放入 `char` 缓冲区。这是处理缓冲区最安全的方法。

* *

提示

尽可能不要使用 `char` 数组。尽可能尽可能使用 `std::string` 代替 `char*`。

* *

### 使用 `std::cin` 向 `std::string` 进行输入

`cin` 是一个多功能工具，你甚至可以用它直接从用户处扫描字符串到 `std::string` 中：

点击此处查看代码图像

```cpp
std::string input;
cin >> input; // 在第一个空格处停止插入
```

列表 27.6 展示了使用 `cin` 向 `std::string` 这种输入。

**列表 27.6** 使用 `cin` 向 `std::string` 插入文本

点击此处查看代码图像

* *

```cpp
#include<iostream>
#include<string>
using namespace std;

int main()
{
    cout << "Enter your name: ";
    string name;
    cin >> name;
    cout << "Hi " << name << endl;
    return 0;
}
```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
Enter your name:
Hi Siddhartha
```



```text
* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

Enter a line:
Testing if I can cross the bounds of the buffer
charBuf: Testing

分析 ![Image](img/arrow.jpg)

如输出所示，由于第 8 行使用了 `cin::get`，你只将用户的前九个字符放入 `char` 缓冲区。这是处理缓冲区最安全的方法。

* *

提示

尽可能不要使用 `char` 数组。尽可能使用 `std::string` 代替 `char*`。

* *

### 使用 `std::cin` 向 `std::string` 进行输入

`cin` 是一个多功能工具，你甚至可以用它直接从用户处扫描字符串到 `std::string` 中：

点击此处查看代码图像

```cpp
std::string input;

cin >> input; // 在第一个空格处停止插入
```

列表 27.6 展示了使用 `cin` 向 `std::string` 这种输入。

**列表 27.6** 使用 `cin` 向 `std::string` 插入文本

点击此处查看代码图像

* *

```cpp
#include<iostream>
#include<string>

using namespace std;

int main()
{
    cout << "Enter your name: ";

    string name;
    cin >> name;

    cout << "Hi " << name << endl;

    return 0;
}
```

* *

点击此处查看代码图像

* *

```cpp
#include<iostream>

using namespace std;

int main()
{
    cout << "Enter an integer: ";

    int inputNum = 0;
    cin >> inputNum;

    cout << "Enter the value of Pi: ";

    double Pi = 0.0;
    cin >> Pi;

    cout << "Enter three characters separated by space: " << endl;

    char char1 = '\0', char2 = '\0', char3 = '\0';
    cin >> char1 >> char2 >> char3;

    cout << "The recorded variable values are: " << endl;
    cout << "inputNum: " << inputNum << endl;
    cout << "Pi: " << Pi << endl;
    cout << "The three characters: " << char1 << char2 << char3 << endl;

    return 0;
}
```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

Enter an integer: 32  
Enter the value of Pi: 0.314159265e1  
Enter three characters separated by space:  
c + +  
The recorded variable values are:  
inputNum: 32  
Pi: 3.14159  
The three characters: c++

分析 ![Image](img/arrow.jpg)

列表 27.4 中最有趣的部分是，你使用科学计数法输入了 `Pi` 的值，而 `cin` 将该数据填充到了 `double Pi` 中。注意看如何像第 15 行所示，你可以在单行内填充三个字符变量。

### 使用 `std::cin::get` 向 `char*` 缓冲区进行输入

就好像 `cin` 允许你直接写入 `int` 一样，你也可以对 C 风格的 `char` 数组执行同样的操作：

点击此处查看代码图像

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};  // can contain max 10 chars

cin >> charBuf;  // Danger: user may enter more than 10 chars
```

在写入 C 风格的字符串缓冲区时，不要超出缓冲区边界非常重要，以避免崩溃或安全漏洞。因此，读取到 C 风格 `char` 缓冲区的更好方法是这种：

点击此处查看代码图像

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};

cin.get(charBuf, 9); // 插入到第 9 个字符时停止插入
```

这种向 C 风格缓冲区插入文本的更安全的方法在列表 27.5 中所示。

**列表 27.5** 在不超出边界的情况下向 `char` 缓冲区插入数据

点击此处查看代码图像

* *

```cpp
#include<iostream>
#include<string>

using namespace std;

int main()
{
    cout << "Enter a line: " << endl;

    char charBuf[10] = {0};
    cin.get(charBuf, 9);

    cout << "charBuf: " << charBuf << endl;

    return 0;
}
```

* *

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

Enter a line:  
Testing if I can cross the bounds of the buffer  
charBuf: Testing

分析 ![Image](img/arrow.jpg)

如输出所示，由于第 8 行使用了 `cin::get`，你只将用户的前九个字符放入 `char` 缓冲区。这是处理缓冲区最安全的方法。

* *

提示

尽可能不要使用 `char` 数组。尽可能使用 `std::string` 代替 `char*`。

* *

### 使用 `std::cin` 向 `std::string` 进行输入

`cin` 是一个多功能工具，你甚至可以用它直接从用户处扫描字符串到 `std::string` 中：

点击此处查看代码图像

```cpp
std::string input;

cin >> input; // 在第一个空格处停止插入
```

列表 27.6 展示了使用 `cin` 向 `std::string` 这种输入。

**列表 27.6** 使用 `cin` 向 `std::string` 插入文本

点击此处查看代码图像

* *

```cpp
#include<iostream>
#include<string>

using namespace std;

int main()
{
    cout << "Enter your name: ";

    string name;
    cin >> name;

    cout << "Hi " << name << endl;

    return 0;
}
```



```cpp
#include<iostream>

using namespace std;

int main()
{
    cout << "Enter an integer: ";

    int inputNum = 0;
    cin >> inputNum;

    cout << "Enter the value of Pi: ";

    double Pi = 0.0;
    cin >> Pi;

    cout << "Enter three characters separated by space: " << endl;

    char char1 = '\0', char2 = '\0', char3 = '\0';
    cin >> char1 >> char2 >> char3;

    cout << "The recorded variable values are: " << endl;
    cout << "inputNum: " << inputNum << endl;
    cout << "Pi: " << Pi << endl;
    cout << "The three characters: " << char1 << char2 << char3 << endl;

    return 0;
}
```

**输出** ![Image](img/arrow.jpg)

```text
Enter an integer: 32
Enter the value of Pi: 0.314159265e1
Enter three characters separated by space:
c + +
The recorded variable values are:
inputNum: 32
Pi: 3.14159
The three characters: c++
```

**分析** ![Image](img/arrow.jpg)

列表 27.4 中最有趣的部分是，你使用科学计数法输入了 `Pi` 的值，而 `cin` 将该数据填充到了 `double Pi` 中。注意看如何像第 15 行所示，你可以在单行内填充三个字符变量。

### 使用 `std::cin::get` 向 `char*` 缓冲区进行输入

就好像 `cin` 允许你直接写入 `int` 一样，你也可以对 C 风格的 `char` 数组执行同样的操作：

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};  // can contain max 10 chars

cin >> charBuf;  // Danger: user may enter more than 10 chars
```

在写入 C 风格的字符串缓冲区时，不要超出缓冲区边界非常重要，以避免崩溃或安全漏洞。因此，读取到 C 风格 `char` 缓冲区的更好方法是这种：

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};

cin.get(charBuf, 9); // 插入到第 9 个字符时停止插入
```

这种向 C 风格缓冲区插入文本的更安全的方法在列表 27.5 中所示。

**列表 27.5** 在不超出边界的情况下向 `char` 缓冲区插入数据

```cpp
#include<iostream>

#include<string>

using namespace std;

int main()
{
    cout << "Enter a line: " << endl;

    char charBuf[10] = {0};
    cin.get(charBuf, 9);

    cout << "charBuf: " << charBuf << endl;

    return 0;
}
```

**输出** ![Image](img/arrow.jpg)

```text
Enter a line:
Testing if I can cross the bounds of the buffer
charBuf: Testing
```

**分析** ![Image](img/arrow.jpg)

如输出所示，由于第 8 行使用了 `cin::get`，你只将用户的前九个字符放入 `char` 缓冲区。这是处理缓冲区最安全的方法。

> **提示**
>
> 尽可能不要使用 `char` 数组。尽可能使用 `std::string` 代替 `char*`。

### 使用 `std::cin` 向 `std::string` 进行输入

`cin` 是一个多功能工具，你甚至可以用它直接从用户处扫描字符串到 `std::string` 中：

```cpp
std::string input;

cin >> input; // 在第一个空格处停止插入
```

列表 27.6 展示了使用 `cin` 向 `std::string` 进行输入。

**列表 27.6** 使用 `cin` 向 `std::string` 插入文本

```cpp
#include<iostream>

#include<string>

using namespace std;

int main()
{
    cout << "Enter your name: ";

    string name;
    cin >> name;

    cout << "Hi " << name << endl;

    return 0;
}
```



列表 27.4 中最有趣的部分是，你使用科学计数法输入了 `Pi` 的值，而 `cin` 将该数据填充到了 `double Pi` 中。注意看如何像第 15 行所示，你可以在单行内填充三个字符变量。

### 使用 `std::cin::get` 向 `char*` 缓冲区进行输入

就好像 `cin` 允许你直接写入 `int` 一样，你也可以对 C 风格的 `char` 数组执行同样的操作：

```cpp
#include<iostream>

using namespace std;

int main()
{
    cout << "Enter an integer: ";

    int inputNum = 0;
    cin >> inputNum;

    cout << "Enter the value of Pi: ";

    double Pi = 0.0;
    cin >> Pi;

    cout << "Enter three characters separated by space: " << endl;

    char char1 = '\0', char2 = '\0', char3 = '\0';
    cin >> char1 >> char2 >> char3;

    cout << "The recorded variable values are: " << endl;
    cout << "inputNum: " << inputNum << endl;
    cout << "Pi: " << Pi << endl;
    cout << "The three characters: " << char1 << char2 << char3 << endl;

    return 0;
}
```

### 输出

```text
Enter an integer: 32
Enter the value of Pi: 0.314159265e1
Enter three characters separated by space:
c + +
The recorded variable values are:
inputNum: 32
Pi: 3.14159
The three characters: c++
```

### 分析

列表 27.4 中最有趣的部分是，你使用科学计数法输入了 `Pi` 的值，而 `cin` 将该数据填充到了 `double Pi` 中。注意看如何像第 15 行所示，你可以在单行内填充三个字符变量。

就好像 `cin` 允许你直接写入 `int` 一样，你也可以对 C 风格的 `char` 数组执行同样的操作：

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};  // can contain max 10 chars

cin >> charBuf;  // Danger: user may enter more than 10 chars
```

在写入 C 风格的字符串缓冲区时，不要超出缓冲区边界非常重要，以避免崩溃或安全漏洞。因此，读取到 C 风格 `char` 缓冲区的更好方法是这种：

```cpp
cout << "Enter a line: " << endl;

char charBuf[10] = {0};

cin.get(charBuf, 9); // 插入到第 9 个字符时停止插入
```

这种向 C 风格缓冲区插入文本的更安全的方法在列表 27.5 中所示。

**列表 27.5** 在不超出边界的情况下向 `char` 缓冲区插入数据

```cpp
#include<iostream>

#include<string>

using namespace std;

int main()
{
    cout << "Enter a line: " << endl;

    char charBuf[10] = {0};
    cin.get(charBuf, 9);

    cout << "charBuf: " << charBuf << endl;

    return 0;
}
```

### 输出

```text
Enter a line:
Testing if I can cross the bounds of the buffer
charBuf: Testing
```

### 分析

如输出所示，由于第 8 行使用了 `cin::get`，你只将用户的前九个字符放入 `char` 缓冲区。这是处理缓冲区最安全的方法。

> **提示**
>
> 尽可能不要使用 `char` 数组。尽可能使用 `std::string` 代替 `char*`。

### 使用 `std::cin` 向 `std::string` 进行输入

`cin` 是一个多功能工具，你甚至可以用它直接从用户处扫描字符串到 `std::string` 中：

```cpp
std::string input;

cin >> input; // 在第一个空格处停止插入
```

列表 27.6 展示了使用 `cin` 向 `std::string` 这种输入。

**列表 27.6** 使用 `cin` 向 `std::string` 插入文本

```cpp
#include<iostream>

#include<string>

using namespace std;

int main()
{
    cout << "Enter your name: ";

    string name;
    cin << name:

    cout << "Hi " << name << endl;

    return 0;
}
```

`ios_base::ate`—将你置于文件末尾，但你可以在文件的任何位置写入数据。

`ios_base::trunc`—导致现有文件被截断；默认选项。

`ios_base::binary`—创建一个二进制文件（默认是文本）。

`ios_base::in`—仅以读取模式打开文件。

`ios_base::out`—仅以读写模式打开文件。

## 使用 `open()` 和 `operator<<` 创建并写入文本文件

在打开文件流后，你可以使用 `operator<<` 向其写入内容，如列表 27.8 所示。

**列表 27.8** 使用 `ofstream` 创建新文本文件并向其中写入文本

```cpp
#include<fstream>

#include<iostream>

using namespace std;

int main()
{
    ofstream myFile;
    myFile.open("HelloFile.txt", ios_base::out);

    if (myFile.is_open())
    {
        cout << "File open successful" << endl;

        myFile << "My first text file!" << endl;
        myFile << "Hello file!";

        cout << "Finished writing to file, will close now" << endl;

        myFile.close();
    }

    return 0;
}
```

### 输出

```text
File open successful
Finished writing to file, will close now
Content of HelloFile.txt:
My first text file!
Hello file!
```

### 分析

第 7 行以 `ios_base::out` 模式打开文件——即专门用于写入。在第 9 行，你测试 `open()` 是否成功，并按照第 13 行和第 14 行所示使用插入运算符 `operator<<` 向文件写入。最后，在第 17 行关闭并返回。

> **注意**
>
> 列表 27.8 展示了你如何以类似于 `cout` 向标准输出（控制台）写入的方式向文件写入内容。这表明 C++ 中的流允许以类似的方式处理不同的设备，通过 `cout` 向显示器写入文本与通过 `ofstream` 向文件写入的方式是相同的。

## 使用 `open()` 和 `operator>>` 读取文本文件

要读取文件，可以使用 `fstream` 并使用标志 `ios_base::in` 打开它，或者使用 `ifstream`。列表 27.9 展示了读取列表 27.8 中创建的 `HelloFile.txt` 文件。

**列表 27.9** 从列表 27.8 创建的文件 `HelloFile.txt` 中读取文本

```cpp
#include<fstream>

#include<iostream>

#include<string>

using namespace std;

int main()
{
    ifstream myFile;
    myFile.open("HelloFile.txt", ios_base::in);

    if (myFile.is_open())
    {
        cout << "File open successful. It contains: " << endl;

        string fileContents;

        while (myFile.good())
        {
            getline(myFile, fileContents);
            cout << fileContents << endl;
        }

        cout << "Finished reading file, will close now" << endl;

        myFile.close();
    }
    else
        cout << "open() failed: check if file is in right folder" << endl;

    return 0;
}
```

### 输出

```text
File open successful. It contains:
My first text file!
Hello file!
Finished reading file, will close now
```

> **注意**
>
> 由于列表 27.9 读取的是使用列表 27.8 创建的文本文件 `"HelloFile.txt"`，你需要将该文件移动到项目的工作目录，或者将此代码合并到之前的代码中。

### 分析

一如既往，你执行 `is_open()` 验证第 8 行的 `open()` 调用是否成功。注意第 18 行中使用提取运算符 `operator>>` 将文件内容直接读取到 `string` 中，然后通过 `cout` 显示。此示例中通过 `getline()` 从文件流中读取输入，这与你在列表 27.7 中从用户读取输入的方式完全相同，一次读取一行。

## 向二进制文件写入和从二进制文件读取

写入二进制文件的实际过程与你目前所学的并没有太大区别。在打开文件时，使用 `ios_base::binary` 作为掩码是非常重要的。你通常使用 `ofstream::write` 或 `ifstream::read`，如列表 27.10 所示。

**列表 27.10** 向二进制文件写入 `struct` 并从相同处重构

```cpp
#include<fstream>

#include<iomanip>

#include<string>

#include<iostream>

using namespace std;

struct Human
{
    Human() {};

    Human(const char* inName, int inAge, const char* inDOB) : age(inAge)
    {
        strcpy(name, inName);
        strcpy(DOB, inDOB);
    }

    char name[30];
    int age;
    char DOB[20];
};

int main()
{
    Human Input("Siddartha Rao", 101, "May 1916");

    ofstream fsOut("MyBinary.bin", ios_base::out | ios_base::binary);

    if (fsOut.is_open())
    {
        cout << "Writing one object of Human to a binary file" << endl;

        fsOut.write(reinterpret_cast<const char*>(&Input), sizeof(Input));
        fsOut.close();
    }

    ifstream fsIn("MyBinary.bin", ios_base::in | ios_base::binary);

    if (fsIn.is_open())
    {
        Human somePerson;

        fsIn.read((char*)&somePerson, sizeof(somePerson));

        cout << "Reading information from binary file: " << endl;
        cout << "Name = " << somePerson.name << endl;
        cout << "Age = " << somePerson.age << endl;
        cout << "Date of Birth = " << somePerson.DOB << endl;
    }

    return 0;
}
```



## 输出

```text
Writing one object of Human to a binary file
Reading information from binary file:
Name = Siddhartha Rao
Age = 101
Date of Birth = May 1916
```

## 分析

在第 22–31 行，你创建了一个包含`name`、`age`和`DOB`的`Human`实例，并使用`ofstream`将其持久化到磁盘上的二进制文件`MyBinary.bin`中。这些信息随后在第 33–44 行使用另一个类型为`ifstream`的流对象进行读取。属性（如`name`）的输出是通过从二进制文件中读取的信息。此示例还展示了`ifstream`和`ofstream`分别通过`ifstream::read`和`ofstream::write`读写文件。注意第 29 行中使用`reinterpret_cast`强制让编译器将`struct`解释为`char*`。在第 38 行，你使用了第 29 行所用方法的 C 风格转换。

## 注意

如果不是为了解释，我更倾向于将`struct Human`的所有属性持久化到 XML 文件。XML 是一种基于文本和标记的存储格式，在信息持久化方式上具有灵活性和扩展性。

如果`struct Human`在此版本中交付，并在交付后向其添加新属性（例如`numChildren`），你将需要担心`ifstream::read`功能能够正确读取使用旧版本创建的二进制数据。

# 使用`std::stringstream`进行字符串转换

你有一个字符串。它包含一个字符串值`45`。你如何将这个字符串值转换为数值为`45`的整数？反之亦然？C++ 提供的最实用工具之一是`class stringstream`，它允许你执行大量的转换操作。

### 提示

要使用`std::stringstream`类，请包含头文件：

```cpp
#include <sstream>
```

列表 27.11 展示了一些简单的`stringstream`操作。

**列表 27.11** 使用`std::stringstream`将整数值转换为字符串表示以及反之亦然

点击此处查看代码图像。

```cpp
0: #include <fstream>
1: #include <sstream>
2: #include <iostream>
3: using namespace std;
4:
5: int main()
6: {
7:     cout << "Enter an integer: ";
8:     int input = 0;
9:     cin >> input;
10:
11:     stringstream converterStream;
12:     converterStream << input;
13:     string inputAsStr;
14:     converterStream >> inputAsStr;
15:
16:     cout << "Integer Input = " << input << endl;
17:     cout << "String gained from integer = " << inputAsStr << endl;
18:
19:     stringstream anotherStream;
20:     anotherStream << inputAsStr;
21:     int Copy = 0;
22:     anotherStream >> Copy;
23:
24:     cout << "Integer gained from string, Copy = " << Copy << endl;
25:
26:     return 0;
27: }
```

## 输出

点击此处查看代码图像。

```text
Enter an integer: 45

Integer Input = 45

String gained from integer = 45

Integer gained from string, Copy = 45
```

## 分析

你要求用户输入一个整数。你首先如第 12 行所示，使用`operator<<`将此整数插入`stringstream`对象中。然后，你使用第 14 行的提取运算符`operator>>`将此整数转换为`string`。之后，你使用此字符串作为起点，获取字符串`inputAsStr`中持有的数值的整数表示`Copy`。

## 应当（DO）

- 当你只想读取文件时，**务必**使用`ifstream`。
- 当你只想写入文件时，**务必**使用`ofstream`。
- **务必**记得在从流插入或提取之前，通过`is_open()`检查文件流是否成功打开。

## 不要（DON'T）

- **不要**忘记在使用完文件流后使用`close()`方法将其关闭。
- **不要**忘记通过`cin >> strData;`从`cin`提取到`string`通常会导致`strData`仅包含到第一个空白字符之前的文本，而不是整行。
- **不要**忘记函数`getline(cin, strData);`会从输入流中获取整行内容，包括空白符。

### 总结

本节从实践角度教了你 C++ 流。你了解到从书的第一开始你就在使用流，如 I/O 流`cout`和`cin`。你现在知道如何创建简单的文本文件以及如何从中读取或写入内容。你学习了`stringstream`如何帮助你将整数等简单类型转换为字符串，反之亦然。

### 问答（Q&A）

**Q：我看到可以使用`fstream`同时对文件进行读写，那么我什么时候应该使用`ofstream`和`ifstream`呢？**

**A：**如果你的代码或模块只需要读取文件，你应该改用`ifstream`。同样，如果它只需要写入文件，请使用`ofstream`。在这两种情况下`fstream`都能正常工作，但为了确保数据和代码的完整性，最好采用类似于使用`const`的限制性策略（尽管后者并非强制性的）。

**Q：我什么时候应该使用`cin.get()`，什么时候应该使用`cin.getline()`？**

**A：**`cin.getline()`确保你捕获用户输入的包括空格在内的整行内容。`cin.get()`帮助你捕获单个字符。

**Q：我什么时候应该使用`stringstream`？**

**A：**`stringstream`提供了一种将整数转换为字符串以及反之亦然的便捷方法。

异常可能由外部因素引起，例如资源不足的系统，也可能由应用程序内部的因素引起，例如尽管包含无效值仍被使用的指针或除以零错误。某些模块的设计目的是通过向调用者抛出异常来通信错误。

> **注意**
>
> 为了保护你的代码免受异常的影响，你需要对异常进行“处理”，从而使你的代码变得是“异常安全的”。

### 通过`try`和`catch`实现异常安全

在实现异常安全方面，`try`和`catch`是 C++ 中最重要的关键字。要使语句具有异常安全，你需要将它们封装在`try`块中，并在`catch`块中处理从`try`块产生的异常。

```cpp
void SomeFunc()
{
    try
    {
        int* numPtr = new int;
        *numPtr = 999;
        delete numPtr;
    }
    catch(...)  // ... 捕获所有异常
    {
        cout << "Exception in SomeFunc(), quitting" << endl;
    }
}
```

#### 使用`catch(...)`处理所有异常

记得在第 8 节中的“指针和引用详解”中，我提到过`new`的默认形式在成功时返回指向内存位置的有效指针，但在失败时抛出异常。列表 28.1 展示了你如何使用`new`使内存分配具有异常安全，并处理计算机无法分配你请求的内存的情况。

**列表 28.1** 在内存分配中使用`try`和`catch`确保异常安全

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: int main()
4: {
5:     cout << "Enter number of integers you wish to reserve: ";
6:     try
7:     {
8:         int input = 0;
9:         cin >> input;
10:
11:         // 请求内存空间并然后返回它
12:         int* numArray = new int [input];
13:         delete[] numArray;
14:     }
15:     catch (...)
16:     {
17:         cout << "Exception occurred. Got to end, sorry!" << endl;
18:     }
19:     return 0;
20: }
```

## 输出

点击此处查看代码图像。

```text
Enter number of integers you wish to reserve: -1
Exception occurred. Got to end, sorry!
```

## 分析

对于这个示例，我使用了`-1`作为我想要保留的整数数量。这个输入是荒谬的，但用户总是在做荒谬的事情。在没有异常处理器的情况下，程序将遇到一个非常糟糕的结局。但多亏了异常处理器，你看到输出显示了一条得体的消息：`Got to end, sorry!`

列表 28.1 展示了`try`和`catch`块的使用。`catch()`接收参数，就像函数一样，而`...`意味着这个`catch`块接受各种异常。然而，在这种情况下，我们可能想专门隔离`std::bad_alloc`类型的异常，因为这些异常是在`new`失败时抛出的。捕获特定类型将帮助你专门处理该类型的问题，例如向用户显示一条消息告诉他们到底发生了什么错误。

#### 捕获特定类型的异常

列表 28.1 中的异常是从 C++ 标准库抛出的。此类异常具有已知类型，捕获特定类型对你来说更好，因为你可以确定位异常的原因，进行更好的清理，或者至少向用户显示一条精确的消息，正如列表 28.2 所示的那样。

**列表 28.2** 捕获类型为`std::bad_alloc`的异常

```cpp
0: #include <iostream>
1: #include <exception> // 包含此以 catch bad_alloc
2: using namespace std;
3:
4: int main()
5: {
6:     cout << "Enter number of integers you wish to reserve: ";
7:     try
8:     {
9:         int input = 0;
10:         cin >> input;
11:
12:         // 请求内存空间并然后返回它
13:         int* numArray = new int [input];
14:         delete[] numArray;
15:     }
16:     catch (std::bad_alloc& exp)
17:     {
18:         cout << "Exception encountered: " << exp.what() << endl;
19:         cout << "Got to end, sorry!" << endl;
20:     }
21:     catch(...)
22:     {
23:     }
24:     return 0;
25: }
```




## 异常处理流程

在列表 28.3 中，你在函数 `Divide()` 中抛出了类型为 `char*` 的异常，该异常在调用函数 `main()` 的 `catch(char*)` 处理器中被捕获。

在抛出异常的地方（使用 `throw`），编译器会插入一个对兼容的 `catch(Type)` 的动态查找，以处理此异常。异常处理逻辑首先检查抛出异常的行是否在 `try` 块内。如果是，它将寻找可以处理该 `Type` 异常的 `catch(Type)`。

如果 `throw` 语句不在 `try` 块内，或者没有与异常类型兼容的 `catch()`，则异常处理逻辑将在调用函数中进行查找。因此，异常处理逻辑会沿着栈一个接一个调用函数向上移动，寻找可以处理该异常的合适的 `catch(Type)`。

在栈展开过程的每一步中，该函数的局部变量都会按照它们构造的反向顺序被销毁。这在列表 28.4 中有所演示。

### 列表 28.4 异常发生时局部对象的析构顺序

点击此处查看代码图像

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: struct StructA

4: {

5:     StructA() {cout << "StructA constructor" << endl; }

6:     ~StructA() {cout << "StructA destructor" << endl;  }

7: };

8:

9: struct StructB

10: {

11:     StructB() {cout << "StructB constructor" << endl; }

12:     ~StructB() {cout << "StructB destructor" << endl; }

13: };

14:

15: void FuncB()  // throws

16: {

17:     cout << "In Func B" << endl;

18:     StructA objA;

19:     StructB objB;

20:     cout << "About to throw up!" << endl;

21:     throw "Throwing for the heck of it";

22: }

23:

24: void FuncA()

25: {

26:     try

27:     {

28:         cout << "In Func A" << endl;

29:         StructA objA;

30:         StructB objB;

31:         FuncB();

32:         cout << "FuncA: returning to caller" << endl;

33:     }

34:     catch(const char* exp)

35:     {

36:         cout << "FuncA: Caught exception: " << exp << endl;

37:         cout << "Handled it, will not throw to caller" << endl;

38:         // throw;  // uncomment this line to throw to main()

39:     }

40: }

41:

42: int main()

43: {

44:     cout << "main(): Started execution" << endl;

45:     try

46:     {

47:         FuncA();

48:     }

49:     catch(const char* exp)

50:     {

51:         cout << "Exception: " << exp << endl;

52:     }

53:     cout << "main(): exiting gracefully" << endl;

54:     return 0;

55: }
```

输出：

```text
main(): Started execution
In Func A
StructA constructor
StructB constructor
In Func B
StructA constructor
StructB constructor
About to throw up!
StructB destructor
StructA destructor
FuncA: Caught exception: Throwing for the heck of it
Handled it, will not throw to caller
main(): exiting gracefully
```

## 分析

在列表 28.4 中，`main()` 调用 `FuncA()`，`FuncA()` 又调用 `FuncB()`，后者在第 21 行抛出异常。两个调用函数 `FuncA()` 和 `main()` 都是异常安全的，因为它们都有一个 `catch(const char*)` 块。

抛出异常的 `FuncB()` 没有 `catch()` 块，因此 `FuncA()` 中第 34–39 行的 `catch` 块是处理来自 `FuncB()` 抛出异常的第一个处理器，因为 `FuncA()` 是 `FuncB()` 的调用者。

注意，`FuncA()` 决定此异常并不严重，因此将其传递给 `main()`。如果你取消第 38 行的注释，异常将抛出给 `FuncB()` 的调用者——即 `main()` 也会接收到它。

输出还指示了对象的创建顺序（与你编写实例化的顺序相同）以及它们在异常发生时立即被销毁的顺序（实例化顺序的反序）。这不仅发生在抛出异常的 `FuncB()` 中，也发生在调用 `FuncB()` 并处理了抛出异常的 `FuncA()` 中。

### 注意

列表 28.4 演示了在发生异常时局部对象的析构函数是如何被调用的。如果由于异常调用的对象的析构函数也抛出了异常，将导致你的应用程序异常终止。

## `std::exception` 类

在列表 28.2 捕获 `bad_alloc` 时，你实际上捕获了由 `new` 抛出的 `bad_alloc` 类对象。`bad_alloc` 是继承自 C++ 标准类 `std::exception` 的类，声明在头文件 `<exception>` 中。

`std::exception` 是以下重要异常的基类：

- `bad_alloc`：使用 `new` 请求内存失败时抛出。
- `bad_cast`：当尝试转换错误的类型（类型之间没有继承关系）时，由 `dynamic_cast` 抛出。
- `ios_base::failure`：由 `iostream` 库中的函数和方法抛出。

基类 `std::exception` 支持一个非常有用且重要的虚方法 `what()`，它可以就导致异常的问题性质提供更详细的描述。在列表 28.2 中，第 18 行的 `exp.what()` 提供了相关信息。

你可以利用 `std::exception` 作为基类，并创建一个捕获所有异常的 `catch(const exception&)`，通过 `exp.what()` 告诉你发生了什么。

```cpp
void SomeFunc()
{
    try
    {
        // code made safe
    }
    catch (const exception& exp)
    {
        cout << "Exception encountered: " << exp.what() << endl;
    }
}
```

## 继承自 `std::exception` 的自定义异常类

你可以抛出任何类型的异常。然而，继承自 `std::exception` 有其好处——`bad_alloc`、`bad_cast` 等类的异常处理器会自动扩展到捕获你的新异常，因为它们具有共同的基类。这在列表 28.5 中演示。

### 列表 28.5 继承自 `std::exception` 的 `CustomException` 类

点击此处查看代码图像

```cpp
0: #include <exception>

1: #include <iostream>

2: #include <string>

3: using namespace std;

4:

5: class CustomException: public std::exception

6: {

7:     string reason;

8: public:

9:     // constructor, needs reason

10:     CustomException(const char* why):reason(why) {}

11:

12:     // redefining virtual function to return 'reason'

13:     virtual char* what() const()

14:     {

15:         return reason.c_str();

16:     }

17: };

18:

19: double Divide(double dividend, double divisor)

20: {

21:     if(divisor == 0)

22:         throw CustomException("CustomException: Dividing by 0 is a crime");

23:

24:     return (dividend / divisor);

25: }

26:

27: int main()

28: {

29:     cout << "Enter dividend: ";

30:     double dividend = 0;

31:     cin >> dividend;

32:     cout << "Enter divisor: ";

33:     double divisor = 0;

34:     cin >> divisor;

35:     try

36:     {

37:         cout << "Result is: " << Divide(dividend, divisor);

38:     }

39:     catch(exception& exp)// catch CustomException, bad_alloc, etc

40:     {

41:         cout << exp.what() << endl;

42:         cout << "Sorry, can't continue!" << endl;

43:     }

44:

45:     return 0;

46: }
```

点击此处查看代码图像

输入被除数：2011

输入除数：0

`CustomException: Dividing by 0 is a crime`

抱歉，无法继续！

### 分析

这是列表 28.3 的一个版本，它在除以零时抛出了简单的 `char*` 异常。然而，这一个版本实例化了第 5–17 行定义的 `class CustomException` 类对象，该类继承自 `std::exception`。

注意，我们的自定义异常类在第 13–16 行中实现了虚函数 `what()`，它本质上返回了抛出异常的原因。`main()` 中第 39–43 行的 `catch(exception&)` 逻辑不仅处理了 `class CustomException`，还处理了具有相同基类 `exception` 的其他 `bad_alloc` 类型异常。

### 注意

请注意列表 28.5 第 13 行中虚方法 `CustomException::what()` 的声明：

点击此处查看代码图像

```cpp
virtual const char* what() const throw()
```

它以 `throw()` 结尾，这意味着预计该函数本身不会抛出异常——对于被用作异常对象的类来说，这是一个非常重要且相关的限制。如果你仍然在该函数中插入 `throw`，你可以预期会有编译器警告。

如果一个函数以 `throw(int)` 结尾，意味着预计该函数会抛出 `int` 类型的异常。

### DO

- **务必**记住 `catch` 类型为 `std::exception` 的异常。
- **务必**记住让你的自定义异常类（如果有）继承自 `std::exception`。
- **务必**抛出异常，但要谨慎。它们不是 `true` 或 `false` 等返回值的替代品。

### DON’T

- **不要**在析构函数中抛出异常。
- **不要**认为内存分配是理所当然；执行 `new` 的代码始终应该是异常安全的，并位于带有 `catch(std::exception&)` 的 `try` 块中。
- **不要**在 `catch()` 块内部插入任何重量级逻辑或资源分配。你不希望在处理异常时又引发了异常。

## Summary

在本节课程中，你学习了实用 C++ 编程的一个重要部分。让你的应用程序在自己的开发环境之外保持稳定，对于客户满意度和直观的用户体验至关重要，而这正是异常能帮助你做到的。

你发现分配资源或内存的代码可能会失败，因此需要使其具有异常安全性。你学习了 C++ 异常类 `std::exception`，并知道如果你需要编写自定义异常类，理想情况下应该继承自这个类。

## Q&A

**Q 为什么要抛出异常而不是返回错误？**

**A** 你并不总是拥有返回错误的权限。如果对 `new` 的调用失败，你需要处理 `new` 抛出的异常，以防止你的应用程序崩溃。此外，如果错误非常严重并导致你的应用程序未来的功能无法实现，你应该考虑抛出异常。

**Q 为什么我的异常类应该继承自 `std::exception`？**

**A** 这当然不是强制性的，但它可以帮助你重用所有已经捕捉 `std::exception` 类型异常的 `catch()` 块。你可以编写不继承自任何其他类的自定义异常类，但你必须在所有相关点插入新的 `catch(MyNewExceptionType&)` 语句。

**Q 我有一个抛出异常的函数。它需要在同一个函数中捕获吗？**

**A** 完全不需要。只需确保抛出的异常类型在调用栈中的某一个调用函数中捕获即可。

**Q 构造函数可以抛出异常吗？**

**A** 构造函数实际上没有选择！它们没有返回值，而抛出异常是表达不同意见的最佳方式。

**Q 析构函数可以抛出异常吗？**

**A** 技术上可以。然而这是一种坏习惯，因为当栈由于异常回溯时也会调用析构函数。因此，一个由于抛出异常而调用的析构函数本身又抛出异常，显然会导致尝试整洁退出的已经不稳定的应用程序陷入非常糟糕的局面。

## Workshop

工作坊包含测验题，帮助你巩固对所涵盖内容的理解，并提供练习让你获得使用所学知识的经验。在检查附录 E 中的答案之前尝试回答测验和练习题，并在进入下一节之前确保你理解了答案。

### Quiz

- **1.** `std::exception` 是什么？
- **2.** 当使用 `new` 分配失败时，抛出的是什么类型的异常？
- **3.** 在异常处理器（`catch` 块）中分配一百万个整数来备份现有数据可以吗？
- **4.** 你将如何捕获一个继承自 `std::exception` 的 `class MyException` 类型异常对象？

### Exercises

#### 1. BUG 查找

下面代码有什么问题？

点击此处查看代码图像

```cpp
class SomeIntelligentStuff
{
   bool isGoneBad;

public:
   ~SomeIntelligentStuff()
   {
     if(isGoneBad)
         throw "Big problem in this class, just FYI";
   }
};
```

#### 2. BUG 查找

下面代码有什么问题？

点击此处查看代码图像

```cpp
int main()
{
   int* millionNums = new int [1000000];

   // 对百万整数进行某些操作
}
```

#### 3. BUG 查找

下面代码有什么问题？

点击此处查看代码图像

```cpp
int main()
{
   try
   {
      int* millionNums = new int [1000000];

      // 对百万整数进行某些操作

      delete []millionNums;
   }
   catch(exception& exp)
   {
      int* anotherMillion = new int [1000000];

      // 将 millionNums 备份到磁盘
   }
}
```




## 第 29 章 展望未来

你已经学习了 C++ 编程的基础。事实上，你已经在理论边界上有所进展，理解了标准模板库（STL）、模板和标准库如何帮助你编写高效简洁的代码。现在是关注性能并获得编程最佳实践视角的时候了。

在本节中，你将学习：

- 如何让你的 C++ 充分利用处理器的能力
- 线程与多线程
- C++ 编程的最佳实践
- C++17 预期的新功能
- 超越本书提升 C++ 技能

### 今天的处理器有什么不同？

在最近之前，计算机通过使用处理速度快的处理器来变快，处理速度以赫兹（Hz）、兆赫（MHz）或吉赫（GHz）衡量。例如，Intel 8086（参见图 29.1）是 1978 年推出的 16 位微处理器，时钟频率约为 10MHz。

那个时代，处理器以规律的速度显著变快，你的 C++ 应用程序也是如此。人们很容易依靠“等待游戏”来利用改进的硬件性能并以此提高软件的响应速度。虽然今天的处理器正在变快，但真正的创新在于它们部署的核心数量。在编写本书时，即使流行的智能手机也配备了四核 64 位处理器，其处理能力超过了十年前的台式电脑。

你可以将多核处理器想象为一个单一芯片，其内部并行运行着多个处理器。每个处理器都有自己的 L1 缓存，并且可以独立于其他处理器工作。

通过更快的处理器来提高应用程序的速度是合乎逻辑的。那么处理器中的多个核心是如何提供帮助的呢？显然，每个核心都具备并行运行应用程序的能力，但除非你编写了程序来利用这种新能力，否则并不一定会让你的应用程序运行得更快。你目前所看到的这类单线程 C++ 在利用多核处理能力方面可能错失了机会。这些应用程序在单个线程中运行，因此只在一个核心上运行，如图 29.2 所示。

![Image](img/29fig02.jpg)

**图 29.2** 多核处理器中的单线程应用程序。

如果你的应用程序按串行执行所有用例，操作系统（OS）可能会只给它与队列中其他应用程序相同的时间，而且它将只占用处理器上的一个核心。换句话说，你的应用程序在多核处理器上的运行方式与过去多年来完全一样。

### 如何更好地使用多核

关键在于创建多线程的应用程序。每个线程并行运行，允许操作系统让线程运行在多个核心上。尽管详细讨论线程和多线程超出了本书的范围，但我可以简单介绍一下这个主题，为你迈向高性能计算打下基础。

#### 什么是线程？

你的应用程序代码始终运行在线程中。线程是一个同步执行实体，线程中的语句一个接一个运行。`main()` 内部的代码被认为执行应用程序的主线程。在这个主线程中，你可以创建可以并行运行的新线程。这种由主线程以及一个或多个并行运行的线程组成的应用程序被称为多线程应用程序。

操作系统规定了如何创建线程，你可以通过直接调用操作系统提供的 API 来创建线程。

> 提示：C++ 自 C++11 起规定了线程函数，它们可以替你调用操作系统 API，使得你的多线程应用程序更具移植性。

如果你计划只为一种操作系统编写应用程序，请检查该操作系统关于创建多线程应用程序的 API。

> 注意：创建线程的实际操作是特定于系统的功能。C++ 试图通过头文件 `<thread>` 中的 `std::thread` 为你提供一种平台无关抽象。

如果你是为一个平台编写代码，那么直接使用特定于系统的线程函数会更好。

如果你在 C++ 应用程序中需要可移植线程，请查看 [www.boost.org](http://www.boost.org) 的 Boost Thread 库。

#### 为什么要编写多线程应用程序？

多线程用于需要并行执行某项活动多次的应用程序。想象一下，你是 10,000 名用户之一，在某一时刻正在 Amazon 门户网站进行购买。Amazon 的 Web 服务器显然无法同时让 9,999 名用户等待。Web 服务器所做的创建多个线程，同时为多个用户服务。如果 Web 服务器运行在多核处理器或多处理器云上，线程可以充分利用可用基础设施的优势，并为用户提供最佳性能。

多线程的另一个常见示例是除了与用户交互外还执行某些任务的应用程序，例如通过进度条。此类应用程序通常被分为显示和更新用户界面并接受用户输入的“用户界面线程”（User Interface Thread），以及在后台执行工作的“工作线程”（Worker Thread）。磁盘碎片整理工具就是这样一种应用程序。当你按下开始按钮后，会创建一个开始扫描和碎片整理的工作线程。同时，用户界面线程会显示进度，并提供取消碎片整理的选项。注意，为了让用户界面线程显示进度，执行整理的工作线程必须定期通信该进度。同样，为了在你取消时停止工作线程，用户界面线程也需要通信该信息。

> 注意：多线程应用程序通常需要线程之间相互“对话”，以便应用程序能够作为一个整体运行（而不是一组互不顾及、各行其事的失控线程）。

顺序同样重要。你不希望用户界面线程在碎片整理的工作线程结束之前就结束。存在一个线程需要等待另一个线程的情况。例如，从数据库读取的线程应该等待执行写入的线程完成。

这种让线程等待另一个线程的行为被称为`thread synchronization`（线程同步）。

#### 线程如何共享数据？

线程可以共享变量。线程可以访问全局数据。创建线程时可以带有一个指向共享对象（包含数据的 `struct` 或 `class`）的指针，如图 29.3 所示。

![Image](img/29fig03.jpg)

**图 29.3** 共享数据的工作线程和用户界面线程。

不同的线程可以通过访问或写入存储在内存某个位置的数据进行通信，该位置可以被它们共同访问因此是共享的。在碎片整理的示例中，工作线程知道进度而用户界面线程需要被告知，工作线程可以不断存储百分比进度，用户界面线程使用其进行显示。

虽然这是一个简单的案例——一个线程创建信息，另一个线程消耗信息。如果多个线程对同一个位置进行读写操作会发生什么呢？某些线程在其他线程尚未完成写入时就可能开始读取数据。这会导致相关数据的完整性将受到破坏。

这就是为什么线程需要同步的原因。

#### 使用互斥锁和信号量同步线程

线程是操作系统级别的实体，你用于同步它们的对象也是由操作系统提供的。大多数操作系统都提供了`semaphores`（信号量）和`mutexes`（互斥锁）来执行线程同步。

你使用互斥锁（一种互斥同步对象）来确保一次只有一个线程访问一段代码。换句话说，互斥锁用于限定一段代码，线程在该处等待直到当前正在执行该代码的另一个线程完成并释放互斥锁。下一个线程获取互斥锁，完成工作，然后释放它。C++ 自 C++11 起通过头文件 `<mutex>` 提供了 `std::mutex` 类的互斥锁实现。

使用信号量，你可以控制执行一段代码的线程数量。允许一次只有一个线程访问的信号量也称为二进制信号量。

#### 多线程引起的问题

多线程需要良好的线程间同步，但当这种同步无效（即：有 Bug）时，可能会导致许多个不眠之夜。多线程应用程序面临的最常见的两个问题如下：

- **竞态条件**——两个或多个线程尝试写入同一份数据。谁胜出？该对象的状态是什么？
- **死锁**——两个线程互相等待对方完成，导致两者都处于“等待”状态。你的应用程序挂起了。

通过良好的同步可以避免竞态条件。通常，当线程允许写入共享对象时，你必须格外小心确保：

- 同一时间只允许一个线程写入。
- 在写入线程完成之前，不允许任何线程读取该对象。

你可以通过确保在任何情况下都不会两个线程互相等待来避免死锁。你可以选择让一个主线程来同步工作线程，或者通过编写程序使任务在线程之间进行分布，从而产生清晰的负载均衡。线程 A 可以等待 B，但 B 永远不应该等待 A。

编写多线程应用程序本身就是一门专业技能。因此，详细向你解释这个有趣且令人兴奋的话题已超出了本书的范围。你应当查阅关于该主题的大量在线文档，或者通过实践编程来学习多线程。一旦你掌握了它，面对未来发布的多核处理器，你将能够自动地让你的 C++ 应用程序处于优化状态。

### 编写出色的 C++ 代码

自最初被构思以来，C++ 不仅发生了巨大的演变，主要编译器制造商的标准化工作以及工具和函数的可用也帮助你编写紧凑整洁的 C++ 代码。编写可读且可靠的 C++ 应用程序是非常容易的。

以下是帮助你创建良好的 C++ 应用程序的最佳实践列表：

- 给你的变量起有意义的名字（对他人也对你而言）。多花几秒钟给变量起更好的名字是值得的。
- 始终初始化如 `int`、`float` 等变量。
- 始终将指针值初始化为 `NULL` 或有效地址——例如由运算符 `new` 返回的地址。
- 使用数组时，永远不要越过数组缓冲区的边界。这被称为缓冲区溢出，可能会被用作安全漏洞。
- 不要使用 `char*` 字符串缓冲区或如 `strlen()` 和 `strcpy()` 等函数。`std::string` 更安全，并提供了许多实用的工具方法，包括帮助你查找长度、复制和追加的方法。
- 仅在你确定它将包含的元素数量时才使用静态数组。如果你不确定，请选择如 `std::vector` 等动态数组。
- 在声明和定义以非 POD（纯旧数据）类型作为输入的函数时，考虑将参数声明为引用参数，以避免在调用函数时产生不必要的拷贝步骤。
- 如果你的类包含原始指针成员（或多个成员），请考虑在拷贝或赋值时如何管理内存资源的所有权。也就是说，考虑编写拷贝构造函数和拷贝赋值运算符。
- 在编写管理动态数组或类似对象的工具类时，记住编写移动构造函数和移动赋值运算符以获得更好的性能。
- 记住让你的代码符合 `const` 规范。一个 `get()` 函数理想情况下不应该能够修改类的成员，因此它应该是 `const` 的。同样地，函数参数应该是 `const` 引用，除非你想改变它们所包含的值。
- 避免使用原始指针。尽可能选择合适的智能指针。
- 在编写工具类时，花精力支持所有能让消费和使用该类变得容易的运算符。
- 在有可选的情况下，选择模板版本而非宏。模板是类型安全且泛型的。
- 当编写一个将被容器（如 `vector` 或 `list`）收集，或用作 `map` 中的键元素使用的类时，记住支持 `operator<`，这将有助于定义默认排序准则。
- 如果你的 lambda 函数变得太大，你可能应该考虑将其转换为一个函数对象——即一个以 `operator()` 作为仿函数的类，这样它是可复用的且具有单一的维护点。
- 永远不要认为运算符 `new` 的成功理所当然。执行资源分配的代码应该总是异常安全的——封装在 `try` 内部并带有相应的 `catch()` 块。
- 永远不要在析构函数中 `throw`。

这不是一个详尽的列表，但它涵盖了一些帮助你编写良好且可维护的 C++ 代码的最要点。

### C++17：预期特性

C++ 的伟大之处之一是标准委员会非常活跃并不断改进这门语言。就像它的前身 C++11 一样，C++17 预计将为语言带来下一波重大新特性。让我们学习一些最有可能在 2017 年新标准正式通过时进入 C++ 的特性。

> **注意**：在接下来的页面中讨论的特性可能会进入标准，但目前还不是标准的一部分——你喜欢的编译器可能部分支持某些特性，而不支持全部。此外，虽然不太可能但并非不可能，C++17 的最终版本可能不支持这里引入的所有特性，尽管在编写本书时预计它是支持的。

#### `if` 和 `switch` 支持初始化

这是对 `if` 和 `switch` 语句语法的一个微小但重要的扩展，可以表示为：

```cpp
if (initializer; condition) {
    // 如果条件为真则执行语句
}
```

或者：

```cpp
switch (initializer; condition) {
    // 分支
}
```

在 `initializer` 中声明的变量在 `if` 语句结束时被销毁。当应用于示例 20.3 中的代码时：

```cpp
auto pairFound = mapIntToStr.find(key);
if (pairFound != mapIntToStr.end()) {
    cout << "Key " << pairFound->first << " points to: ";
    cout << pairFound->second << endl;
}
```

该特性将其改进为：

```cpp
if (auto pairFound = mapIntToStr.find(key); pairFound != mapIntToStr.end()) {
    cout << "Key " << pairFound->first << " points to: ";
    cout << pairFound->second << endl;
}
```

这不仅仅减少了一行代码。它确保了 `if` 块需要的变量 `pairFound` 在块之外不可见，限制了作用域。此外，如果你复制这个改进后的 `if` 块，你就完整获得了所需的逻辑。

#### 拷贝消除保证

当你将变量初始化为函数的返回值时，编译器可能会在初始化变量 `num` 之前为函数 `ReturnInt()` 返回的整数创建一个临时拷贝：

```cpp
int num = ReturnInt();
```

C++17 要求编译器消除这种临时拷贝；即避免这种拷贝。

#### `std::string_view` 避免分配开销

考虑一个接受 `std::string` 作为参数的函数：

```cpp
void DisplayString (const std::string& strIn) {
    cout << strIn << endl;
}
```

当使用字符串字面量调用时，字符串字面量 `"Hello World!"` 首先转换为临时 `std::string` 供函数 `DisplayString()` 使用：

```cpp
DisplayString("Hello World!");
```

这种临时转换是一种性能开销，通过改用 `std::string_view` 可以避免。

```cpp
void DisplayString (std::string_view& strIn) {
    cout << strIn << endl;
}
```

当字符串字面量传递给接受 `std::string_view` 作为参数的函数时，不会产生分配开销。

#### `std::variant` 作为 `union` 的类型安全替代方案

`union` 在第 9 节“类与对象”中进行了了解释。`union` 的问题之一是它允许将其内容被解释为 `union` 支持的任何其他数据类型；例如：

```cpp
union SimpleUnion {
   int num;
   double preciseNum;
};
```

你可能为 `double` 实例化这个 `union`，但却将其作为 `integer` 使用：

```cpp
SimpleUnion u1;
u1.preciseNum = 3.14; // union 存储了一个 double
int num2 = u1.num; // 可以运行，但 u1 包含一个 double！
```

C++17 为程序员提供了 `std::variant`，它是 `union` 的一种类型安全的替代方案：

```cpp
variant<int, double> varSafe;
varSafe = 3.14; // variant 存储 double
double pi = get<double>(varSafe); // 3.14
double pi2 = get<1>(varSafe); // 3.14
get<char>(varSafe); // 编译失败：variant 中没有 char
get<2>(varSafe); // 编译失败：variant 有两种类型，而不是三种
try {
   get<int>(varSafe); // 因为 variant 存储的是 double 而抛出异常
}
catch (bad_variant_access&) { // 异常处理器代码 }
```

#### 使用 `if constexpr` 进行条件代码编译

此功能类似于 `if-else` 结构，不同之处在于 `if` 条件在编译时求值，并且只有当 `if` 块中的代码（或相应的 `else`）在编译时满足条件时才会被编译。

```cpp
#include <type_traits>
#include <iostream>
#include <iomanip>
using namespace std;

template <typename T>
```



`void DisplayData(const T& data)`

```
{
   if constexpr (is_integral<T>::value)
       cout << "Integral data: " << data << endl;
   else if constexpr (is_floating_point<T>::value)
       cout << setprecision(15) << "Floating point data: " << data << endl;
   else
       cout << "Unidentified data: " << data << endl;
}
```

给定 `DisplayData(15)`，符合 C++17 标准的编译器将只编译以下行：

```cpp
cout << "Integral data: " << data << endl;
```

给定 `DisplayData("Hello World!")`，编译器将只编译以下内容，因为函数被调用时使用的类型触发了 `else` 块：

```cpp
cout << "Unidentified data: " << data << endl;
```

结合第 7 节“[使用函数组织代码”中引入的自动返回类型推导，这是一个强大的功能，它允许函数根据编译器执行的路径返回不同类型的值。

### 改进的 Lambda 表达式

Lambda 函数预计会有以下改进：

- 将在 `constexpr` 函数内部被支持。
- 将允许使用 `[*this]` 语法捕获 `*this` 的拷贝。

### 构造函数的自动类型推导

从 C++14 开始，你需要像这样声明一个组合整数和浮点类型的对：

```cpp
std::pair<int, double> pairIntToDb (3, 3.14159265359);
```

C++17 将允许将该行代码简化为：

```cpp
std::pair pairIntToDb (3, 3.14159265359);
```

构造函数模板参数的类型推导将是自动的。

---

2. 我的多线程应用允许极快地访问数据库。然而，有时我发现获取的数据是乱码。我哪里做错了？

# 第六部分：附录

## 附录 A. 数字处理：二进制与十六进制

理解二进制和十六进制系统的原理对于编写更好的 C++ 应用程序并非关键，但它可以帮助你更好地理解底层发生了什么。

### 十进制系统

我们每天使用的数字范围在 0–9 之间。这组数字被称为十进制。由于该系统由 10 个独特的数字组成，因此它是一个基数为 10 的系统。

因此，由于基数是 10，每个数字从 0 开始的位置表示该数字所乘以 10 的幂次。所以：

`957 = 9 x 10² + 5 x 10¹ + 7 x 10⁰ = 9 x 100 + 5 x 10 + 7`

在数字 `957` 中，`7` 从 0 开始的位置是 0，`5` 的位置是 1，`9` 的位置是 2。这些位置索引变成了基数 10 的幂，如示例所示。记住，任何数的 0 次幂都是 1（所以，`10⁰` 等于 `1000⁰`，因为它们计算的值都是 1）。

> 注意
> 十进制系统是一个 10 的幂次最重要的系统。数字中的数位通过乘以 10、100、1000 等来确定数字的大小。

### 二进制系统

基数为 2 的系统被称为二进制系统。由于该系统仅允许两种状态，因此用数字 0 和 1 表示。这些数字在 C++ 中通常被求值为 `false` 和 `true`（`true` 为非零）。

正如十进制系统中的数字被求值为基数 10 的幂一样，二进制中的数字被求值为其基数 2 的幂次：

`101 (二进制) = 1 x 2² + 0 x 2¹ + 1 x 2⁰ = 4 + 0 + 1 = 5 (十进制)`

所以，二进制 `101` 的十进制对应值为 5。

> 注意
> 二进制数中的数字通过乘以 2 的幂次（如 4, 8, 16, 32 等）来确定数字的大小。幂次由该数字从 0 开始的位置决定。

为了更好地理解二进制系统，让我们查看列出各种 2 的幂的表 A.1。

**表 A.1** 2 的幂

### 为什么计算机使用二进制？

与数字系统发现的时间相比，二进制系统的广泛使用相对较新。电子计算机的发展加速了它的使用。电子和电子元件的演变产生了一种能够检测组件处于开启（在显著电位或电压下）或关闭（无或低电位）状态的系统。

这些开启和关闭状态方便地解释为 1 和 0，完全代表了二进制数字集，并使其成为算术运算的首选方法。第 5 课中涵盖的如 `NOT`、`AND` 和 `XOR` 等逻辑操作，以及“表达式与运算符的使用”（位于表 5.2），通过电子门的发展得到了轻松支持。

### 什么是位（Bits）和字节（Bytes）？

`bit` 是计算系统中包含二进制状态的基本单位。因此，如果一个 `bit` 包含 1，则被称为“置位”，如果包含 0 则被称为“重置”。位的集合是一个 `byte`。一个 `byte` 中的位数在理论上是固定的，且取决于硬件。

然而，大多数计算系统都假设一个 `byte` 有 8 个位，简单原因是 8 是 2 的幂。一个 `byte` 中的 8 位还允许多达 2⁸ 种不同的值，即 255 个不同的值，这足够显示 ASCII 集中所有的字符。

### 多少字节组成一个千字节？

1024 字节组成一个千字节。同样，1024 千字节组成一个兆字节。1024 兆字节组成一个字节。

### 十六进制系统

十六进制是一种基数为 16 的数字系统。十六进制系统中的数字范围可以是 0–9 和 A–F。所以，十进制的 10 在十六进制中是 `A`，十进制的 15 在十六进制中是 `F`：

正如十进制系统中的数字被求值为基数 10 的幂，二进制中求值为基数 2 的幂，十六进制中的则求值为基数 16 的幂：

```
3 x 16² + 1 x 16¹ + F x 16⁰
```

> 注意
> 十六进制是

### 为什么我们需要十六进制？

十六进制是计算机表示二进制的更简便的方式。

### 十进制转十六进制

该过程与二进制相同；只是除以 16 而不是除以 2。

### 十进制转二进制

将十进制 33 转换为二进制，减去 2 的最高幂（32）：

```
33 / 2 = 商 16，余 1
16 / 2 = 商 8，余 0
8 / 2 = 商 4，余 0
4 / 2 = 商 2，余 0
2 / 2 = 商 1，余 0
1 / 2 = 商 0，余 1
```

33 的二进制（读取位）：`100001`

同样，156 的二进制对应值为：

```
156 / 2 = 商 78，余 0
78 / 2 = 商 39，余 0
39 / 2 = 商 19，余 1
19 / 2 = 商 9，余 1
9 / 2 = 商 4，余 1
4 / 2 = 商 2，余 0
2 / 2 = 商 1，余 0
1 / 2 = 商 0，余 1
```

156 的二进制：`10011100`

### 十进制转十六进制

该过程与二进制相同；你除以 16 而不是除以 2。

所以，将十进制 5211 转换为十六进制：

```
5211 / 16 = 商 325，余 B[16] (11[10] 是 B[16])
325 / 16 = 商 20，余 5
20 / 16 = 商 1，余 4
1 / 16 = 商 0，余 1
```

`5211[10] = 145B[16]`

---

为了更好地理解不同数字系统的工作原理，你可以编写一个简单的 C++ 程序，类似于第 27 节中的列表 27.1“使用流进行输入和输出”。该程序使用 `std::cout` 配合操符来以十六进制、十进制和八进制格式显示整数。

要以二进制显示整数，可以使用 `std::bitset`，这在第 25 节“使用 STL 处理位标志”中已经介绍过，其灵感源自列表 25.1。

## 附录 B. C++ 关键字

关键字是编译器保留的标识，供语言使用。你不能使用这些关键字作为类、变量或函数的名称。

```
alignas enum return
alignof explicit short
and export signed
and_eq extern sizeof
asm false static
auto float static_assert
bitand for static_cast
bitor friend struct
bool goto switch
break if template
case inline this
catch int thread_local
char long throw
char16_t mutable true
char32_t namespace
class new typedef
compl noexcept type
const not id
const not typename
constexpr not_eq union
const_cast nullptr unsigned
continue operator using
decltype or virtual
default or_eq void
delete private volatile
do protected wchar_t
double public while
dynamic_cast register
else reinterpret_cast
```

### 备注

第 10 节“实现继承”和第 11 节“多态”引入了两个有趣的术语——`final` 和 `override`。它们**不是**保留的 C++ 关键字，你可以用它们来命名你的对象和函数。然而，当伴随特定构造时，它们具有特殊的含义。

## 附录 C. 运算符优先级

使用括号来显式地划分你的操作是一个良好的习惯。在没有这些括号的情况下，编译器将诉诸预定义的优先级顺序来使用运算符。这种运算符优先级如表 C.1 所示，是 C++ 编译器在出现歧义时遵循的依据。

### 表 C.1 运算符优先级

## 附录 D. ASCII 码

计算机使用位和字节工作，这些本质上是数字。为了在这个数值系统中表示字符数据，使用了一种由美国信息交换标准（ASCII）确立的一项标准。ASCII 为拉丁字母 A–Z、a–z、数字 0–9 以及某些特殊字符分配了 7 位数值代码。7 位允许 128 种组合，其中前 32 个（0–31）被保留用作控制字符，用于与外设设备交互。

### ASCII 可打印字符表

ASCII 码 32–127 用于打印字符，如 0–9、A–Z、a–z 以及空格等。下表显示了留给这些符号的十进制和十六进制值。

## 附录 E. 答案

### 第 1 节答案

### 测验

1. 解释器是一种解释你的代码（或中间字节码）并执行某些操作的工具。编译器是以你的代码为输入并生成目标文件的。在 C++ 中，经过编译和链接，你将获得一个可以直接由处理器运行的可执行文件，不需要任何解释。
2. 编译器以 C++ 代码文件作为输入并生成机器语言的目标文件。通常你的代码依赖于其他代码文件中的库和函数。创建这些链接并生成一个集成了你直接或间接编码的所有依赖的可执行文件，是链接器的工作。
3. 代码。编译生成目标文件。链接生成可执行文件。执行进行测试。调试。修复代码中的错误并重复步骤。在许多情况下，编译和链接是一一步完成的。

### 练习

1. 显示 `x` 减去 `y` 的结果、将两者相乘以及将两者相加的结果。

### 第 2 节答案

### 测验

1. C++ 是大小写敏感的。`Int` 对编译器来说是可以接受的。
2. 是的。

```cpp
/* 如果你使用这种注释语法
那么你的注释可以跨行 */
```

### 练习

1. 失败了，因为编译器不认识 `std::Cout`，或者其字符串没有以引号开头。此外，`main` 的声明应该返回一个 `int`。
2. 这里是修复后的版本：

```cpp
#include <iostream>

int main()
{
    std::cout << "这里有 bug 吗?"; // 现在没有 bug 了
    return 0;
}
```

3. 源自列表 2.4 的程序演示了减法和乘法：

```cpp
#include <iostream>
using namespace std;

// 函数声明
int DemoConsoleOutput();

int main()
{
    // 调用函数
    DemoConsoleOutput();
    return 0;
}

// 函数定义
int DemoConsoleOutput()
{
    cout << "减法 10 - 5 = " << 10 - 5 << endl;
    cout << "乘法 10 * 5 = " << 10 * 5 << endl;
    return 0;
}
```

输出：
```
减法 10 - 5 = 5
乘法 10 * 5 = 50
```

### 第 3 节答案

### 测验

1. 符号整数是指其最高位（MSB）作为符号位，用于指示整数值是正还是负。相比之下，无符号整数用于仅包含正整数。
2. `#define` 是一种预处理器指令，指示编译器在看到定义值出现的地方进行文本替换。然而，它不是类型安全的，是定义常量的一种原始方式。因此，应该避免使用。
3. 为了确保它包含一个确定的、非随机的值。
4. 2。
5. 名称缺乏描述性且重复了类型。虽然这种代码可以编译，但这种代码对人类来说难以阅读和维护，应该避免。整数最好使用揭示其目的的名称命名。例如：
`int age = 0;`

### 练习

1. 实现这一点的有许多方法：

```cpp
enum YourCards {Ace = 43, Jack, Queen, King};
// Ace is 43, Jack is 44, Queen is 45, King is 46
// Alternatively..
enum YourCards {Ace, Jack, Queen = 45, King};
// Ace is 0, Jack is 1, Queen is 45 and King is 46
```

**2.** 参考列表 3.4 并对其进行修改（精简内容）以得到该问题的答案。

**3.** 这里有一个程序，它要求你输入圆的半径，并计算面积和周长：

```cpp
#include <iostream>
using namespace std;

int main()
{
   const double Pi = 3.1416;
   cout << "Enter circle's radius: ";
   double radius = 0;
   cin >> radius;
   cout << "Area = " << Pi * radius * radius << endl;
   cout << "Circumference = " << 2 * Pi * radius << endl;
   return 0;
}
```

输出：
```
Enter circle's radius: 4
Area = 50.2656
Circumference = 25.1328
```

**4.** 如果你将计算面积和周长的结果存储在整数中，你会得到一个编译警告（而非错误），且输出如下：

输出：
```
Enter circle's radius: 4
Area = 50
Circumference = 25
```

**5.** `auto` 是一种构造，编译器根据变量初始化的值自动推断出变量可以采用的类型。所涉及的代码没有初始化，因此导致了编译失败。

# 第 4 课答案

### 测验

**1.** 0 和 4 是一个包含五个元素的数组的第一个和最后一个元素的索引（从 0 开始）。

**2.** 不，因为它们被证明是不安全的，特别是在处理用户输入时，这给了用户输入比数组长度长的字符串的机会。

**3.** 一个空终止字符。

**4.** 取决于你如何使用它。例如，如果你在 `cout` 语句中使用它，显示逻辑会读取连续字符寻找终止空字符并跨越数组边界，可能导致你的应用程序崩溃。

**5.** 这只需将 vector 声明中的 `int` 替换为 `char` 即可。

```cpp
vector<char> dynArrChars (3);
```

### 练习

**1.** 给你。该程序针对车（ROOK）初始化，但这对你理解概念已经足够了：

```cpp
int main()
{
   enum Square
   {
      Empty = 0,
      Pawn,
      Rook,
      Knight,
      Bishop,
      King,
      Queen
   };

   Square chessBoard[8][8];

   // 初始化包含车的格子
   chessBoard[0][0] = chessBoard[0][7] = Rook;
```



`chessBoard[7][0] = chessBoard[7][7] = Rook;`

`return 0;`

}

**2.** 要设置数组的第五个元素，你需要访问元素`myNums[4]`，因为这是从 0 开始的索引。

**3.** 数组的第四个元素在从未被初始化或赋值的情况下被访问。结果输出是不可预测的。始终初始化变量和数组；否则它们将包含创建时所在内存位置存储的最后一个值。

# 第 5 课答案

### 测验

**1.** 整数类型无法包含对想要除法两个数字的用户可能相关的的小数值。因此，你应该使用`float`。

**2.** 由于编译器将它们解释为整数，所以结果是 4。

**3.** 由于分子是 32.0 而不是 32，编译器将其解释为浮点数运算，创建一个类似于 4.571 的`float`结果。

**4.** 不，`sizeof`是一个运算符，且无法被重载。

**5.** 它没有按预期工作，因为加法运算符的优先级高于移位，导致移动了 1 + 5 = 6 位，而不是仅仅一个位。

**6.** 异或运算的结果为`false`，如 表 5.5 所示。

### 练习

**1.** 这是一个正确的解：

点击此处查看代码图片

```cpp
int result = ((number << 1) + 5) << 1;
```

**2.** 结果包含了左移 7 位的数字，因为`operator +`的优先级高于`operator <<`。

**3.** 这里有一个程序存储用户输入的两个布尔值，并演示了它们进行位运算的结果：

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

int main()

{

   cout << "Enter a boolean value(1) or false(0): ";

   bool value1 = false;

   cin >> value1;

   cout << "Enter another boolean value(1) or false(0): ";

   bool value2 = false;

   cin >> value2;

   cout << "Result of bitwise operators on these: " << endl;

   cout << "Bitwise AND: " << (value1 & value2) << endl;

   cout << "Bitwise OR: " << (value1 | value2) << endl;

   cout << "Bitwise XOR: " << (value1 ^ value2) << endl;

   return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```
Enter a boolean value(1) or false(0): 1
Enter another boolean value(1) or false(0): 0
Result of bitwise operators on these:
Bitwise AND: 0
Bitwise OR: 1
Bitwise XOR: 1
```

# 第 6 课答案

### 测验

**1.** 缩进不是为了编译器，而是为了可能需要阅读或理解你代码的其他程序员。

**2.** 避免这样做是为了防止你的代码变得不直观且难以维护。

**3.** 查看使用递减运算符的练习 1。

**4.** 由于`for`语句中的条件不满足，循环没有执行一次，其中的`cout`语句从未执行。

### 练习

**1.** 你需要注意数组索引是从 0 开始的，最后一个元素位于 Length – 1：

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

int main()

{

   const int ARRAY_LEN = 5;

   int myNums[ARRAY_LEN]= {-55, 45, 9889, 0, 45};

   for (int index = ARRAY_LEN - 1; index >= 0; --index)

      cout<<"myNums[" << index << "] = "<<myNums[index]<<endl;

   return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```
myNums[4] = 45
myNums[3] = 0
myNums[2] = 9889
myNums[1] = 45
myNums[0] = -55
```

**2.** 列表 6.13 的一个嵌套循环，以反序添加两个数组中的元素，演示如下：

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

int main()

{

   const int ARRAY1_LEN = 3;

   const int ARRAY2_LEN = 2;

   int myNums1[ARRAY1_LEN] = {35, -3, 0};

   int MyInts2[ARRAY2_LEN] = {20, -1};

   cout << "Adding each int in myNums1 by each in MyInts2:" << endl;

   for(int index1 = ARRAY1_LEN - 1; index1 >= 0; --index1)

      for(int index2 = ARRAY2_LEN - 1; index2 >= 0; --index2)

         cout << myNums1[index1] << " + " << MyInts2[index2] \

         << " = " << myNums1[index1] + MyInts2[index2] << endl;

   return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

```
Adding each int in myNums1 by each in MyNums2:
0 + -1 = -1
0 + 20 = 20
-3 + -1 = -4
-3 + 20 = 17
35 + -1 = 34
35 + 20 = 55
```

**3.** 你需要将常量整数`numsToCalculate`替换为固定值为 5 的值，并使用询问用户内容的代码：

点击此处查看代码图片

```cpp
cout << "How Fibonacci numbers you wish to calculate: ";

int numsToCalculate = 0; // no const

cin >> numsToCalculate;
```

**4.** 使用枚举常量的 switch-case 结构判断颜色是否在彩虹中所示所示：

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

int main()

{

   enum Colors

   {

      Violet = 0,

      Indigo,

      Blue,

      Green,

      Yellow,

      Orange,

      Red,

      Crimson,

      Beige,

      Brown,

      Peach,

      Pink,

      White,

   };

   cout << "Here are the available colors: " << endl;

   cout << "Violet: " << Violet << endl;

   cout << "Indigo: " << Indigo << endl;

   cout << "Blue: " << Blue << endl;

   cout << "Green: " << Green << endl;

   cout << "Yellow: " << Yellow << endl;

   cout << "Orange: " << Orange << endl;

   cout << "Red: " << Red << endl;

   cout << "Crimson: " << Crimson << endl;

   cout << "Beige: " << Beige << endl;

   cout << "Brown: " << Brown << endl;

   cout << "Peach: " << Peach << endl;

   cout << "Pink: " << Pink << endl;

   cout << "White: " << White << endl;

   cout << "Choose one by entering code: ";

   int YourChoice = Blue; // initial

   cin >> YourChoice;

   switch (YourChoice)

   {

   case Violet:

   case Indigo:

   case Blue:

   case Green:

   case Yellow:

   case Orange:

   case Red:

      cout << "Bingo, your choice is a Rainbow color!" << endl;

      break;

   default:

      cout << "The color you chose is not in the rainbow" << endl;

      break;

   }

   return 0;

}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像

```
以下是可用颜色：

Violet: 0
Indigo: 1
Blue: 2
Green: 3
Yellow: 4
Orange: 5
RED: 6
Crimson: 7
Beige: 8
Brown: 9
Peach: 10
Pink: 11
White: 12
输入代码选择一个：4
太棒了，你选择的是彩虹色！
```

**5.** 程序员无意中在`for`循环条件语句中赋值 10。

**6.** `while`语句后面紧跟一个同一行的空语句`';'`。因此，预期的在`while`之后的循环永远不会到达，而且因为控制`while`的`loopCounter`从不增加，导致`while`永远不会结束，其后的语句也永远不会被执行。

**7.** 缺少`break`语句（这意味着`default`情况始终执行）。

### 第 7 课答案

### 测验

1. 这些变量的作用域是整个函数的生命周期。
2. `someNumber`是对调用函数中变量的引用。它不持有副本。
3. 递归函数。
4. 函数重载。
5. 栈顶端！想象一叠盘子；位于顶部的盘子是可以提取的，这正是栈指针所指向的。

### 练习题

1. 函数原型将如下：

点击此处查看代码图像

```cpp
double Area (double radius); // 圆形

double Area (double radius, double height); // 圆柱
```

函数实现（定义）使用了问题中提供的相应公式，并将面积作为返回值返回给调用者。

2. 参考 列表 7.8 来给你灵感。函数原型将是：

点击此处查看代码图像

```cpp
void ProcessArray(double numbers[], int length);
```

3. 参数`result`应该是一个引用，以便`Area()`函数才能生效：

点击此处查看代码图像

```cpp
void Area(double radius, double &result)
```

4. 默认参数应该列在末尾，否则你将遇到编译错误。或者，所有参数都应该指定默认值。

5. 函数需要通过引用向调用者返回输出数据：

点击此处查看代码图像

```cpp
void Calculate (double radius, double &Area, double &Circumference)

{

   Area = 3.14 * radius;

   Circumference = 2 * 3.14 * radius;

}
```

### 第 8 课答案

### 测验

1. 如果编译器允许你这样做，它将很容易破坏`const`引用本应保护的内容：被引用的数据不能被更改。
2. 它们是运算符。
3. 内存地址。
4. `operator`。

### 练习题

1. 40。
2. 在第一个重载变中，参数被复制了。在第二个中，它们没有被复制，因为它们是变量的引用，函数可以修改它们。第三种变使用指针，与引用不同，指针可以是 NULL，并且在这种系统中需要确保其有效性。
3. 使用`const`关键字：

点击此处查看代码图像

```cpp
const int* pNum1 = &number;
```

4. 你正在将一个整数赋值给指针（即覆盖指针）。这是将整数赋值给指针的`Human`所示：

点击此处查看代码图像

```cpp
int Age = 25;

int* pAge = &Age;

*pAge = 30;
```

5. 赋值给指针的整数`Human`所示：

```cpp
int Age = 20;
```

6. 30。

### 第 9 课答案

### 测验

1. 如果编译器允许你这样做，它将很容易破坏`const`引用本应保护的内容：被引用的数据不能被更改。
2. 它们是运算符。
3. 内存地址。
4. `operator`。

### 练习

1. `Base`类的成员。`Derived`类与`Base`私有继承关系。因此`Base`的成员在`Derived`中是私有的。
2. 按照类声明中提到的顺序构造：`Mammal - Bird - Reptile - Platypus`。析构按反序。
3. 如下所示：

点击此处查看代码图像

```cpp
class Shape

{

   // ... Shape 成员

};
```




```cpp
   Orange,

   Red,

   Crimson,

   Beige,

   Brown,

   Peach,

   Pink,

   White,

};

   cout << "Here are the available colors: " << endl;

   cout << "Violet: " << Violet << endl;

   cout << "Indigo: " << Indigo << endl;

   cout << "Blue: " << Blue << endl;

   cout << "Green: " << Green << endl;

   cout << "Yellow: " << Yellow << endl;

   cout << "Orange: " << Orange << endl;

   cout << "Red: " << Red << endl;

   cout << "Crimson: " << Crimson << endl;

   cout << "Beige: " << Beige << endl;

   cout << "Brown: " << Brown << endl;

   cout << "Peach: " << Peach << endl;

   cout << "Pink: " << Pink << endl;

   cout << "White: " << White << endl;

   cout << "Choose one by entering code: ";

   int YourChoice = Blue; // initial

   cin >> YourChoice;

   switch (YourChoice)

   {

   case Violet:

   case Indigo:

   case Blue:

   case Green:

   case Yellow:

   case Orange:

   case Red:

      cout << "Bingo, your choice is a Rainbow color!" << endl;

      break;

   default:

      cout << "The color you chose is not in the rainbow" << endl;

      break;

   }

   return 0;

}

```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

以下是可用颜色：

Violet: 0  
Indigo: 1  
Blue: 2  
Green: 3  
Yellow: 4  
Orange: 5  
RED: 6  
Crimson: 7  
Beige: 8  
Brown: 9  
Peach: 10  
Pink: 11  
White: 12  

输入代码选择一个：4

太棒了，你选择的是彩虹色！

5. 程序员无意中在 `for` 循环条件语句中赋值 10。

6. `while` 语句后面紧跟一个同一行的空语句 `';'`。因此，预期的在 `while` 之后的循环永远不会到达，而且因为控制 `while` 的 `loopCounter` 从不增加，导致 `while` 永远不会结束，其后的语句也永远不会被执行。

7. 缺少 `break` 语句（这意味着 `default` 情况始终执行）。

### 第 7 课答案

#### 测验

1. 这些变量的作用域是整个函数的生命周期。
2. `someNumber` 是对调用函数中变量的引用。它不持有副本。
3. 递归函数。
4. 函数重载。
5. 栈顶端！想象一叠盘子；位于顶部的盘子是可以提取的，这正是栈指针所指向的。

#### 练习题

1. 函数原型将如下：

点击此处查看代码图像。

```cpp
double Area (double radius); // 圆形

double Area (double radius, double height); // 圆柱
```

函数实现（定义）使用了问题中提供的相应公式，并将面积作为返回值返回给调用者。

2. 参考列表 7.8 来给你灵感。函数原型将是：

点击此处查看代码图像。

```cpp
void ProcessArray(double numbers[], int length);
```

3. 参数 `result` 应该是一个引用，以便 `Area()` 函数才能生效：

点击此处查看代码图像。

```cpp
void Area(double radius, double &result)
```

4. 默认参数应该列在末尾，否则你将遇到编译错误。或者，所有参数都应该指定默认值。

5. 函数需要通过引用向调用者返回输出数据：

点击此处查看代码图像。

```cpp
void Calculate (double radius, double &Area, double &Circumference)

{

   Area = 3.14 * radius;

   Circumference = 2 * 3.14 * radius;

}
```

### 第 8 课答案

#### 测验

1. 如果编译器允许你这样做，它将很容易破坏 `const` 引用本应保护的内容：被引用的数据不能被更改。
2. 它们是运算符。
3. 内存地址。
4. `operator`。

#### 练习题

1. 40。
2. 在第一个重载变体中，参数被复制了。在第二个中，它们没有被复制，因为它们是变量的引用，函数可以修改它们。第三种变体使用指针，与引用不同，指针可以是 `NULL`，并且在这种系统中需要确保其有效性。
3. 使用 `const` 关键字：

点击此处查看代码图像。

```cpp
const int* pNum1 = &number;
```

4. 你正在将一个整数赋值给指针（即覆盖指针）。这是将整数赋值给指针的 `Human` 所示：

点击此处查看代码图像。

```cpp
int Age = 25;

int* pAge = &Age;

*pAge = 30;
```

5. 赋值给指针的整数 `Human` 所示：

```cpp
int Age = 20;
```




## 第 6 课答案

### 练习题

```cpp
   。。。Here are the available。: "。.。
   。。 "。: ". Violet <<.;
   . << "Indigo: " << Indigo <<.;
   . << "Blue: " << Blue << endl;
   cout << "Green: " << Green << endl;
   cout << "Yellow: " << Yellow << endl;
   cout << "Orange: " << Orange << endl;
   cout << "Red: " << Red << endl;
   cout << "Crimson: " << Crimson << endl;
   cout << "Beige: " << Beige << endl;
   cout << "Brown: " << Brown << endl;
   cout << "Peach: " << Peach << endl;
   cout << "Pink: " << Pink << endl;
   cout << "White: " << White << endl;
   cout << "Choose one by entering code: ";

   int YourChoice = Blue; // initial
   cin >> YourChoice;

   switch (YourChoice)
   {
   case Violet:
   case Indigo:
   case Blue:
   case Green:
   case Yellow:
   case Orange:
   case Red:
      cout << "Bingo, your choice is a Rainbow color!" << endl;
      break;
   default:
      cout << "The color you chose is not in the rainbow" << endl;
      break;
   }

   return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图像。

以下是可用颜色：

- Violet: 0
- Indigo: 1
- Blue: 2
- Green: 3
- Yellow: 4
- Orange: 5
- RED: 6
- Crimson: 7
- Beige: 8
- Brown: 9
- Peach: 10
- Pink: 11
- White: 12

输入代码选择一个：4

太棒了，你选择的是彩虹色！

5. 程序员无意中在 `for` 循环条件语句中赋值 10。

6. `while` 语句后面紧跟一个同一行的空语句 `';'`。因此，预期的在 `while` 之后的循环永远不会到达，而且因为控制 `while` 的 `loopCounter` 从不增加，导致 `while` 永远不会结束，其后的语句也永远不会被执行。

7. 缺少 `break` 语句（这意味着 `default` 情况始终执行）。

## 第 7 课答案

### 测验

1. 这些变量的作用域是整个函数的生命周期。

2. `someNumber` 是对调用函数中变量的引用。它不持有副本。

3. 递归函数。

4. 函数重载。

5. 栈顶端！想象一叠盘子；位于顶部的盘子是可以提取的，这正是栈指针所指向的。

### 练习题

1. 函数原型将如下：

点击此处查看代码图像。

```cpp
double Area (double radius); // 圆形
double Area (double radius, double height); // 圆柱
```

函数实现（定义）使用了问题中提供的相应公式，并将面积作为返回值返回给调用者。

2. 参考列表 7.8 来给你灵感。函数原型将是：

点击此处查看代码图像。

```cpp
void ProcessArray(double numbers[], int length);
```

3. 参数 `result` 应该是一个引用，以便 `Area()` 函数才能生效：

点击此处查看代码图像。

```cpp
void Area(double radius, double &result)
```

4. 默认参数应该列在末尾，否则你将遇到编译错误。或者，所有参数都应该指定默认值。

5. 函数需要通过引用向调用者返回输出数据：

点击此处查看代码图像。

```cpp
void Calculate (double radius, double &Area, double &Circumference)
{
   Area = 3.14 * radius;
   Circumference = 2 * 3.14 * radius;
}
```

## 第 8 课答案

### 测验

1. 如果编译器允许你这样做，它将很容易破坏 `const` 引用本应保护的内容：被引用的数据不能被更改。

2. 它们是运算符。

3. 内存地址。

4. `operator`。

### 练习题

1. 40。

2. 在第一个重载变体中，参数被复制了。在第二个中，它们没有被复制，因为它们是变量的引用，函数可以修改它们。第三种变体使用指针，与引用不同，指针可以是 `NULL`，并且在这种系统中需要确保其有效性。

3. 使用 `const` 关键字：

点击此处查看代码图像。

```cpp
const int* pNum1 = &number;
```

4. 你正在将一个整数赋值给指针（即覆盖指针）。这是将整数赋值给指针的 `Human` 所示：

点击此处查看代码图像。

```cpp
int Age = 25;
int* pAge = &Age;
*pAge = 30;
```

5. 赋值给指针的整数 `Human` 所示：

```cpp
int Age = 20;
```

6. 30。

## 第 9 课答案

### 测验

*（由于原文文本在此处出现大量重复乱码和无意义字符，此处未提供有效翻译）*

### 练习题

*（由于原文文本在此处出现大量重复乱码和无意义字符，此处未提供有效翻译）*

```cpp
class Polygon: public Shape
{
   // ... Polygon members
}

class Triangle: public Polygon
{
   // ... Triangle members
}
```

3. 类 `D1` 和 `Base` 之间的继承关系应该是 `private` 的，以限制 `class D2` 访问 `Base` 的公共成员。

4. 类默认按 `private` 方式继承。如果 `Derived` 是一个 `struct`，则该继承关系将是 `public`。

5. `SomeFunc` 是按值传递 `type Base` 类型的参数。这意味着使用 `Derived` 实例调用此类类型的函数会导致对象切片（slicing），从而导致不稳定性和不可预测的输出：

点击此处查看代码图片。

```cpp
Derived objectDerived;
SomeFunc(objectDerived); // slicing problems
```

## 第 11 课答案

### 问答

1. 声明一个抽象基类 `Shape`，并将 `Area()` 和 `Print()` 为纯虚函数，从而强制 `Circle` 和 `Triangle` 实现相同的函数。它们被强制遵守你关于支持 `Area()` 和 `Print()` 的标准。

2. 不。它只为包含虚函数的类创建虚函数表（VFT）。

3. 是的，因为它仍然无法实例化。只要一个类至少有一个纯虚函数，无论是否存在其他完全定义的函数或参数，它仍然是一个抽象类（ABC）。

### 练习题

1. 使用抽象基类 `Shape` 为类 `Circle` 和 `Triangle` 构建的继承层次结构如下：

点击此处查看代码图像。



```cpp
#include<iostream>

using namespace std;

class Shape
{
public:
   virtual double Area() = 0;
   virtual void Print() = 0;
};

class Circle
{
   double radius;
public:
   Circle(double inputRadius) : radius(inputRadius) {}
   double Area()
   {
      return 3.1415 * radius * radius;
   }
   void Print()
   {
      cout << "Circle says hello!" << endl;
   }
};

class Triangle
{
   double base, height;
public:
   Triangle(double inputBase, double inputHeight) : base(inputBase),
height(inputHeight) {}
   double Area()
   {
      return 0.5 * base * height;
   }
   void Print()
   {
      cout << "Triangle says hello!" << endl;
   }
};

int main()
{
   Circle myRing(5);
   Triangle myWarningTriangle(6.6, 2);
   cout << "Area of circle: " << myRing.Area() << endl;
   cout << "Area of triangle: " << myWarningTriangle.Area() << endl;
   myRing.Print();
   myWarningTriangle.Print();
   return 0;
}
```

2. 缺少虚析构函数！

3. 没有虚析构函数，构造函数的顺序将是`Vehicle()`之后是`Car()`，而而非虚的析构函数只会导致`~Vehicle()`被调用。

## 第 12 课答案

### 问答

1. 不，C++ 不允许两个同名的函数具有不同的返回值。你可以编写两个返回类型完全相同的`operator[]`实现，其中一个是`const`函数，另一个不是。在这种情况下，C++ 会在与赋值相关的活动中选择非`const`版本，在其他情况下选择`const`版本：

点击此处查看代码图片

```cpp
Type& operator[](int Index) const;
Type& operator[](int Index);
```

2. 是的，但仅当我不希望类允许拷贝或赋值时。在编写单例模式（singleton）时，这种限制是必要的，Listing 9.10 展示了仅允许一个实例的类。

3. 由于`class Date`中没有在拷贝构造函数或赋值运算符中导致内存分配和释放的动态资源，因此它不是移动构造函数或移动赋值运算符的候选对象。

### 练习题

1. 转换运算符`int()`如下：

点击此处查看代码图片

```cpp
class Date
{
   int day, month, year;
public:
   explicit operator int()
   {
      return ((year * 1000) + (month * 100) + day);
   }
   // constructor
```

2. 移动构造函数和移动赋值运算符如下：

点击此处查看代码图片

```cpp
class DynIntegers
{
private:
   int* arrayNums;
public:
   // move constructor
   DynIntegers(DynIntegers&& moveSrc)
   {
      arrayNums = moveSrc.arrayNums; // take ownership
      moveSrc.arrayNums = NULL; // release ownership
   }
   // move assignment operator
   DynIntegers& operator=(DynIntegers&& moveSrc)
   {
      if(this != &moveSrc)
      {
         delete [] arrayNums; // release resources
         arrayNums = moveSrc.arrayNums;
         moveSrc.arrayNums = NULL;
      }
      return *this;
   }
   ~DynIntegers() {delete[] arrayNums;} // destructor
   // implement default constructor, copy constructor, assignment operator
```

## 第 13 课答案

### 问答

1. `dynamic_cast`。

2. 当然是该函数。`const_cast`和各种类型转换运算符应该是最后的手段。

3. 正确。

4. 是的，正确。

### 练习题

1. `dynamic_cast`操作的结果应该检查有效性：

点击此处查看代码图片

```cpp
void DoSomething(base* pBase)
{
   Derived* objDerived = dynamic_cast<Derived*>(pBase);
   if(objDerived) // check for validity
      objDerived->DerivedMethod();
}
```

2. 当你知道所指向的对象是`Tuna`类型时使用`static_cast`。以 Listing 13.1 为基类，`main()`函数如下所示：

点击此处查看代码图片

```cpp
int main()
{
   Tuna* pFish = new Tuna;
   Fish* puna = static_cast<Fish*>(pFish);
   puna->virtualDinner();
   delete puna;
   return 0;
}
```

## 第 14 课答案

### 问答

1. 一个阻止你进行乘法的预处理器结构。

2. 10。

3. 10 + 2。

4. 使用括号：`#define SPLIT(x) ((x))`

### 练习题

1. 如下：

点击此处查看代码图片

```cpp
#define MULTIPLY(a,b) ((a)*(b))
```

2. 这是第 4 题问题的模板版本：

点击此处查看代码图片

```cpp
template<typename T> T Split(const T& input)
{
   return (input / 5);
}
```

3. `swap`的模板版本为：

点击此处查看代码图片

```cpp
template <typename T>
void Swap (T& x, T& y)
{
   T temp = x;
   x = y;
   y = temp;
}
```

4. `#define QUARTER(x) ((x)/ 4)`

5. `template`类如下所示：

点击此处查看代码图片

```cpp
template <typename Array1Type, typename Array2Type>
class TwoArrays
{
private:
   Array1Type Array1 [10];
   Array2Type Array2 [10];
public:
   Array1Type& GetArray1Element(int Index){return Array1[Index];}
   Array2Type& GetArray2Element(int Index){return Array2[Index];}
};
```

6. 这是一个完整的示例，包含一个`Display()`函数，该函数展示了变长模板及其用法：

点击此处查看代码图片

```cpp
#include <iostream>

using namespace std;

void Display()
{
}

template <typename First, typename ...Last> void Display(First a, Last... U)
{
   cout << a << endl;
   Display(U...);
}

int main()
{
   Display('a');
   Display(3.14);
   Display('a', 3.14);
   Display('z', 3.14567, "The power of variadic templates!");
   return 0;
}
```

输出 ![Image](img/arrow.jpg)

点击此处查看代码图片

a

3.14

a

3.14

z

3.14567

变长模板的力量！

## 第 15 课答案

### 测验

**1.** `std::deque`。只有`deque`模拟了动态数组，并且允许在容器的头部和尾部进行常数时间的插入。`std::vector`不允许在开头进行插入，因此不适用。

**2.** 如果你有键值对，则使用`std::set`或`std::map`。如果元素也需要支持重复，你将会选择`std::multiset`或`std::multimap`。

**3.** 是的。当你实例化一个`std::set`模板时，你可以选择性地提供第二个模板参数，该参数是一个`set`类用作排序准则的二元谓词。将此二元谓词编写为与你的相关的标准。它需要符合严格弱序（strict-weak ordering）。

**4.** 迭代器构成了算法与容器之间的桥梁，使得前者（泛型）可以在后者上工作，而无需知道（或为每种可能的容器类型进行定制）。

**5.** `hash_set`不是符合 C++ 标准的容器。因此，你不应该在任何将移植性列为要求之一的应用程序中使用它。请改用`std::map`。

## 第 16 课答案

### 测验

**1.** `std::basic_string <T>`

**2.** 将两个字符串拷贝到两个拷贝对象中。将每个拷贝的字符串转换为小写或大写。返回转换后的拷贝字符串比较的结果。

**3.** 不，它们不是。C 风格的字符串实际上是类似于字符数组的原始指针，而 STL `string`是一个实现了各种运算符和成员函数的类，这使得字符串的操作和处理变得尽可能简单。

### 练习题

**1.** 程序需要使用`std::reverse()`：

点击此处查看代码图片

```cpp
#include <string>
#include <iostream>
#include <algorithm>

int main ()
{
    using namespace std;
    cout << "请输入一个单词以进行回文检查:" << endl;
    string strInput;
    cin >> strInput;
    string strCopy (strInput);
    reverse (strCopy.begin (), strCopy.end ());
    if (strCopy == strInput)
        cout << strInput << " 是回文的!" << endl;
    else
        cout << strInput << " 不是回文的." << endl;
    return 0;
}
```

**2.** 使用`std::find()`：

点击此处查看代码图片

```cpp
#include <string>
#include <iostream>
using namespace std;

// 在字符串 "strInput" 中查找字符 'chToFind' 的数量
int GetNumCharacters (string& strInput, char chToFind)
{
    int nNumCharactersFound = 0;
    size_t nCharOffset = strInput.find (chToFind);
    while (nCharOffset != string::npos)
    {
        ++ nNumCharactersFound;
        nCharOffset = strInput.find (chToFind, nCharOffset + 1);
    }
    return nNumCharactersFound;
}

int main ()
{
    cout << "请输入一个字符串:" << endl << "> ";
    string strInput;
    getline (cin, strInput);
    int nNumVowels = GetNumCharacters (strInput, 'a');
    nNumVowels += GetNumCharacters (strInput, 'e');
    nNumVowels += GetNumCharacters (strInput, 'i');
    nNumVowels += GetNumCharacters (strInput, 'o');
    nNumVowels += GetNumCharacters (strInput, 'u');
    // 自定义：也处理大写字母..
    cout << "句子中元音的数量为:" << nNumVowels;
    return 0;
}
```

**3.** 使用函数`toupper()`：

点击此处查看代码图片

```cpp
#include <string>
#include <iostream>
#include <algorithm>

int main ()
{
    using namespace std;
    cout << "请输入一个用于大小写转换的字符串:" << endl;
    cout << "> ";
    string strInput;
    getline (cin, strInput);
    cout << endl;
    for (size_t nCharIndex = 0
        ; nCharIndex < strInput.length ()
        ; nCharIndex += 2)
        strInput [nCharIndex] = toupper (strInput [nCharIndex]);
    cout << "转换为大写的字符串是: " << endl;
    cout << strInput << endl << endl;
    return 0;
}
```

**4.** 这可以简单地编写为：

点击此处查看代码图片

```cpp
#include <string>
#include <iostream>
int main ()
{
    using namespace std;
    const string str1 = "I";
    const string str2 = "Love";
    const string str3 = "STL";
    const string str4 = "String.";
    string strResult = str1 + " " + str2 + " " + str3 + " " + str4;
    cout << strResult;
    return 0;
}
```

**5.** 使用`string::find()`：

点击此处查看代码图片

```cpp
#include <string>
#include <iostream>
int main ()
{
    using namespace std;
    string strInput("The day is beautiful!");
    size_t charPos = strInput.find('a');
    if (charPos != string::npos)
        cout << "Found 'a' at index " << charPos << endl;
    else
        cout << "'a' not found" << endl;
    return 0;
}
```

## 第 17 课答案

### 测验

**1.** 不，它们不是。`vector`只能在尾部以常数时间添加元素。

**2.** 当在尾部插入元素时，会触发重新分配。

**3.** 删除最后一个元素。

**4.** `vector`类型。

**5.** 通过下标运算符`[]` (b) own `at()`。

**6.** 随机访问迭代器。

### 练习题

**1.** 一种方案

点击此处查看代码图片



```cpp
#include <vector>
#include <iostream>
using namespace std;
char DisplayOptions ()
{
    cout << "你想做什么？" << endl;
    cout << "1: 输入一个整数" << endl;
    cout << "2: 给定索引查询值" << endl;
    cout << "3: 显示 vector" << endl;
    cout << "4: 退出!" << endl << "> ";
    char ch;
    cin >> ch;
    return ch;
}

int main ()
{
    vector <int> vecData;
    char chUserChoice = '\0';
    while ((chUserChoice = DisplayOptions ()) != '4')
    {
        if (chUserChoice == '1')
        {
            cout << "请输入要插入的整数: ";
            int nDataInput = 0;
            cin >> nDataInput;
            vecData.push_back (nDataInput);
        }
        else if (chUserChoice == '2')
        {
            cout << "请输入一个 0 到 "; 之间的索引 ";
            cout << (vecData.size () - 1) << ": ";
            size_t index = 0;
            cin >> index;
            if (index < (vecData.size ()))
            {
                cout<<"元素 ["<<index<<"] = "<<vecData[index];
                cout << endl;
            }
        }
        else if (chUserChoice == '3')
        {
            cout << "vector 的内容为: ";
            for (size_t index = 0; index < vecData.size (); ++ index)
                cout << vecData [index] << ' ';
            cout << endl;
        }
    }
    return 0;
}
```

## 2. 使用`std::find()`算法

```cpp
vector <int>::iterator elementFound = std::find (vecData.begin (), vecData.end (), value);
if (elementFound != vecData.end())
    cout << "找到元素!" << endl;
```

## 3. 这是一个可能的解决方案

注意这里使用了`vector`来存储`class Dimensions`类的实例。还要注意`Dimensions`如何实现运算符`const char*`，以便使`std::cout`可以直接对它的实例进行操作。

点击此处查看代码图像。

```cpp
#include <vector>
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

char DisplayOptions()
{
    cout << "你想做什么？" << endl;
    cout << "选择 1: 输入长度和宽度 " << endl;
    cout << "选择 2: 根据索引查询值" << endl;
    cout << "选择 3: 显示所有包裹的尺寸" << endl;
    cout << "选择 4: 退出!" << endl << "> ";
    char ch;
    cin >> ch;
    return ch;
}

class Dimensions
{
    int length, breadth;
    string strOut;
public:
    Dimensions(int inL, int inB) : length(inL), breadth(inB) {}
    operator const char* ()
    {
        stringstream os;
        os << "Length "s << length << ", Breadth: "s << breadth << endl;
        strOut = os.str();
        return strOut.c_str();
    }
};

int main()
{
    vector <Dimensions> vecData;
    char chUserChoice = '\0';
    while ((chUserChoice = DisplayOptions()) != '4')
    {
        if (chUserChoice == '1')
        {
            cout << "请输入长度和宽度：" << endl;
            int length = 0, breadth = 0;
            cin >> length;
            cin >> breadth;
            vecData.push_back(Dimensions(length, breadth));
        }
        else if (chUserChoice == '2')
        {
            cout << "请输入 0 到 "; 之间的索引";
            cout << (vecData.size() - 1) << ": ";
            size_t index = 0;
            cin >> index;
            if (index < (vecData.size()))
            {
                cout << "元素 [" << index << "] = " << vecData[index];
                cout << endl;
            }
        }
        else if (chUser_Choice == (chUserChoice == '3')
        {
            cout << "vector 的内容为：";
            for (size_t index = 0; index < vecData.size(); ++index)
                cout << vecData[index] << ' ';
            cout << endl;
        }
    }
    return 0;
}
```

## 4. C++11 引入的列表初始化使得代码更加简洁

点击此处查看代码图像。

```cpp
#include <deque>
#include <string>
#include <iostream>

using namespace std;

template<typename T>
void DisplayDeque(deque<T> inDQ)
{
    for (auto element = inDQ.cbegin();
    element != inDQ.cend();
    ++element)
    cout << *element << endl;
}

int main()
{
    deque<string> strq{"Hello"s, "Containers are cool"s, "C++ is evolving!"s };
    DisplayDeque(strq);
    return 0;
}
```

## 第 18 课的答案

### 测验

1. 元素可以插入到列表中间，也可以插入到两端。位置的变化不会导致任何收益或损失。

2. 列表的特殊之处在于，这类操作不会使迭代器失效。

3. `theList.clear ();`或`theList.erase(theList.begin(), theList.end());`

4. 是的，`insert()`函数的重载版本允许你从源集合插入一个范围的内容。

### 练习题

1. 这类似于第 17 节中`vector`的练习题 1。唯一的区别是你将使用`list::insert()`函数，如`List.insert(List.begin(),Data);`。

2. 存储列表中两个元素的迭代器。使用列表的`insert`函数在中间插入一个元素。使用迭代器来证明它们仍然能够获取插入前所指向的值。

3. 一个可能的解决方案是：

```cpp
#include <vector>
#include <list>
#include <iostream>

using namespace std;

int main()
{
    vector <int> vecData{ 0, 10, 20, 30 };
    list <int> linkInts;
    // 将 vector 的内容插入到列表开头
    linkInts.insert(linkInts.begin(),
    vecData.begin(), vecData.end());
    cout << "列表的内容为：";
    list <int>::const_iterator element;
    for (element = linkInts.begin();
    element != linkInts.end();
    ++element)
    cout << *element << " ";
    return 0;
}
```

4. 一个可能的解决方案是：

```cpp
#include <list>
#include <string>
#include <iostream>

using namespace std;

int main()
{
    list <string> names;
    cout << "列表的内容为：";
    list <string>::const_iterator element;
    for (element = names.begin();
    element != names.end();
    ++element)
    cout << *element << " ";
    cout << endl;
    names.push_back("Jack");
    names.push_back("John");
    names.push_back("Anna");
    names.push_back("Skate");
    cout << "反转后的内容：";
    names.reverse();
    for (element = names.begin();
    element != names.end();
    ++element)
    cout << *element << " ";
    cout << endl;
    cout << "排序后的内容：";
    names.sort();
    for (element = names.begin();
    element != names.end();
    ++element)
    cout << *element << " ";
    cout << endl;
    return 0;
}
```

## 第 19 课的答案

### 测验

1. 默认排序标准由`std::less<>`指定，如果第一个整数小于第二个则返回`true`。

2. `multiset`在插入时对元素进行排序，并将相同值的元素相邻。

### 练习题

1. 一个解决方案是：

```cpp
#include <set>
#include <iostream>
#include <string>

using namespace std;

struct ContactItem
{
    string name;
    string phoneNum;
    string displayAs;
    ContactItem(const string& nameInit, const string & phone)
    {
        name = nameInit;
        phoneNum = phone;
        displayAs = name + ": " + phoneNum;
    }
    // 用于 set::find() 给定项
    bool operator == (const ContactItem& item) const
    {
        return itemCompare.phoneNum == this->phoneNum;
    }
    // 用于排序
    bool operator < (const ContactItem& itemCompare) const
    {
        return this->phoneNum < itemCompare.phoneNum;
    }
    // 通过 cout 输出 DisplayContents
    operator const char() const
    {
        return displayAs.c_str();
    }
};

template <typename T>
void DisplayDeque(const T& inDQ)
{
    for (auto element = inDQ.cbegin();
    element != inDQ.cend();
    ++element)
    cout << *element << endl;
}

int main()
{
    set<ContactItem> setContacts;
    setContacts.insert(ContactItem("Jack Welsch", "+1 7889 879 879"));
    setContacts.insert(ContactItem("Bill Gates", "+1 97 7897 879 8"));
    setContacts.insert(ContactItem("Angi Merkel", "+49 23456 5466"));
    setContacts.insert(ContactItem("Vlad Putin", "+7 6645 4564 797"));
    setContacts.insert(ContactItem("John Travolta", "+1 234 4564 789"));
    setContacts.insert(ContactItem("Ben Affleck", "+1 745 641 314"));
    DisplayDeque(setContacts);
    cout << "输入你想搜索的号码：";
    string input;
    getline(cin, input);
    auto contactFound = setContacts.find(ContactItem("", input));
    if (contactFound != setContacts.end())
    {
        cout << "该号码属于 " << (*contactFound).name << endl;
        DisplayDeque(setContacts);
    }
    else
    {
        cout << "未找到联系人" << endl;
    }
    return 0;
}
```

2. 结构和`multiset`的定义为：

```cpp
#include <set>
#include <iostream>
#include <string>

using namespace std;

struct PAIR_WORD_MEANING
{
    string word;
};
```



```cpp
string meaning;

PAIR_WORD_MEANING(const string& sWord, const string& sMeaning)
    : word(sWord), meaning(sMeaning) {}

bool operator< (const PAIR_WORD_MEANING& pairAnotherWord) const
{
    return (word < pairAnotherWord.word);
}

bool operator== (const string& key)
{
    return (key == this->word);
}
```

`int main()`
{
    `multiset <PAIR_WORD_MEANING> msetDictionary;`
    `PAIR_WORD_MEANING word1("C++", "A programming language");`
    `PAIR_WORD_MEANING word2("Programmer", "A geek!");`
    `msetDictionary.insert(word1);`
    `msetDictionary.insert(word2);`
    `cout << "Enter a word you wish to find the meaning off" << endl;`
    `string input;`
    `getline(cin, input);`
    `auto element = msetDictionary.find(PAIR_WORD_MEANING(input, ""));`
    `if (element != msetDictionary.end())`
        `cout << "Meaning is: " << (*element).meaning << endl;`
    `return 0;`
}

### 3. 方案是

点击此处查看代码图像

```cpp
#include <set>
#include <iostream>

using namespace std;

template <typename T>
void DisplayContent(const T& cont)
{
    T::const_iterator element;
    for (element = cont.begin(); element != cont.end(); ++element)
        cout << *element << " ";
}

int main()
{
    multiset <int> msetIntegers;
    msetIntegers.insert(5);
    msetIntegers.insert(5);
    msetIntegers.insert(5);
    set <int> setIntegers;
    setIntegers.insert(5);
    setIntegers.insert(5);
    setIntegers.insert(5);
    cout << "Displaying the contents of the multiset: ";
    DisplayContent(msetIntegers);
    cout << endl;
    cout << "Displaying the contents of the set: ";
    DisplayContent(setIntegers);
    cout << endl;
    return 0;
}
```

### 第 20 课答案

### 测验

**1.** 默认排序准则由 `std::less<>` 指定。

**2.** 紧挨在一起。

**3.** `size()`。事实上，这个成员函数会告诉你 STL 提供的每个容器中的元素数量。

**4.** 你不会在 `map` 中找到重复的元素！

### 练习题

**1.** 一种允许重复条目的关联容器。例如，一个 `std::multimap`：

点击此处查看代码图像

```cpp
std::multimap <string, string> mapNamesToNumbers;
```

**2.** 一种允许重复条目的关联容器。

点击此处查看代码图像

```cpp
struct fPredicate
{
    bool operator< (const WordProperty& lsh, const WordProperty& rsh) const
    {
        return (lsh.word < rsh.word);
    }
};
```

**3.** 参考在 第 19 课 中类似解决的练习题 3，“STL Set 类。](#ch19.html_ch19)”

### 第 21 课答案

### 测验

**1.** 一个一元谓词。

**2.** 它可以显示数据（例如），或者简单地计算元素。请参见 列表 21.6 中带有谓词 `tolower()` 的 `std::transform()` 用法。

**3.** 应用程序运行期间的所有实体都是对象。在这种情况下，即使是结构体和类也可以被当作函数使用，因此有了`函数对象`这一术语。注意，函数也可以通过函数指针可用——这些也是函数对象。

### 练习题

**1.** 一个方案是

点击此处查看代码图像

```cpp
template <typename elementType=int>
struct Double
{
    void operator () (const elementType element) const
    {
        cout << element * 2 << ' ';
    }
};
```

这个一元谓词可以这样使用

点击此处查看代码图像

```cpp
#include<vector>
#include<iostream>
#include<algorithm>
using namespace std;

int main()
{
    vector <int> numsInVec;
    for (int count = 0; count < 10; ++count)
        numsInVec.push_back(count);
    cout << "Displaying the vector of integers: " << endl;
    // 显示整数数组
    for_each(numsInVec.begin(), // 范围开始
        numsInVec.end(), // 范围结束
        Double()); // 一元函数对象
    return 0;
}
```

**2.** 添加一个成员整数，每当使用 `operator()` 时，该变量就会加 1：

点击此处查看代码图像

```cpp
template <typename elementType=int>
struct Double
{
    void operator () (const elementType element) const
    {
        cout << element * 2 << ' ';
    }
};
```

**3.** 这个二元谓词是

点击此处查看代码图像

```cpp
template <typename elementType>
class SortAscending
{
public:
    bool operator () (const elementType& lsh, const elementType& rsh) const
    {
        return (lsh < rsh);
    }
};
```

该谓词可以这样使用

点击此处查看代码图像

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
int main()
{
    vector <int> numsInVec;
    for (int sample = 0; sample < 10; ++sample)
        numsInVec.push_back(sample);
    cout << "Displaying the vector of integers: " << endl;
    // 显示整数数组
    for_each(numsInVec.begin(), // 范围开始
        numsInVec.end(), // 范围结束
        SortAscending<int>()); // 二元函数对象
    return 0;
}
```

4. `for_each()` 接受一个一元谓词并返回一个可以用于包含状态信息的函数对象。`std::transform()` 可以与一元或二元谓词一起工作，并具有一个重载版本，因此可以作用于两个输入范围。

### 练习题

1. 这里有一个解决方案：

点击此处查看代码图片

```cpp
struct CaseInsensitiveCompare
{
    bool operator() (const string& str1, const string& str2) const
    {
        string str1Copy (str1), str2Copy (str2);
        transform (str1Copy.begin (),
                      str1Copy.end(), str1Copy.begin (), tolower);
        transform (str2Copy.begin (),
                      str2Copy.end(), str2Copy.begin (), tolower);
        return (str1Copy < str2Copy);
    }
};
```

2. 这里是演示。注意 `std::copy()` 如何在不知道集合性质的情况下工作的。它仅通过迭代器类进行工作：

点击此处查看代码图片

```cpp
#include <vector>
#include <algorithm>
#include <list>
#include <string>
#include <iostream>

using namespace std;

int main ()
{
    list <string> listNames;
    listNames.push_back ("Jack");
    listNames.push_back ("John");
    listNames.push_back ("Anna");
    listNames.push_back ("Skate");
    vector <string> vecNames (4);
    copy (listNames.begin (), listNames.end (), vecNames.begin ());
    vector <string> ::const_iterator iNames;
    for (iNames = vecNames.begin (); iNames != vecNames.end (); ++ iNames)
        cout << *iNames << ' ';
    return 0;
}
```

3. `std::sort()` 和 `std::stable_sort()` 的区别在于后者在排序时能确保对象的相对位置保持不变。由于应用程序需要按照事件发生的顺序存储数据，您应该选择 `stable_sort()` 来保持天体事件之间的相对顺序完好。

#### 第 24 课答案

### 测验

1. 是的，通过提供一个二元谓词。

2. `class Coin` 需要实现 `operator<`。

3. 不，你只能在栈的顶部进行操作。因此你无法访问底部的硬币，即第一个插入的硬币。

### 练习题

1. 二元谓词可以是 `operator<`：

点击此处查看代码图片

```cpp
class Person
{
public:
    int age;
    bool isFemale;
    bool operator<  (const Person& anotherPerson) const
    {
        bool bRet = false;
        if (age > anotherPerson.age)
            bRet = true;
        else if (isFemale && anotherPerson.isFemale)
            bRet = true;
        return bRet;
    }
};
```

2. 将单个字符推入 `stack`。当你弹出数据时，你实际上反转了内容，因为栈是一个后入先出（LIFO）类型的容器。

#### 第 25 课答案

### 测验

1. 不。`bitset` 能包含的比特数在编译时是固定的。

2. 因为 `bitset` 不是一个容器类。它不能像其他容器那样动态扩展自己；它不支持以容器所需的方式提供迭代器。

3. 不。`std::bitset` 最适合此用途。

### 练习题

1. 此处演示了具有实例化、初始化、显示和加法功能的 `std::bitset`：

点击此处查看代码图片

```cpp
#include <bitset>
#include <iostream>
int main()
{
    // 将 bitset 初始化为 1001
    std::bitset<4> fourBits (9);
    cout << "fourBits: " << fourBits << endl;
    // 将另一个 bitset 初始化为 0010
    std::bitset<4> fourMoreBits (2);
    cout << "fourMoreBits: " << fourMoreBits << endl;
    std::bitset<4> addResult(fourBits.to_ulong()+fourMoreBits.to_ulong());
    cout << "The result of the addition is: " << addResult;
    return 0;
}
```

2. 在前一个示例的任何 `bitset` 对象上调用 `flip()` 函数：

点击此处查看代码图片

```cpp
addResult.flip ();
cout << "The result of the flip is: " << addResult << endl;
```

#### 第 26 课答案

### 测验

1. 我会查看 [www.boost.org](http://www.boost.org)。我希望你也会看！

2. 不，通常情况下编写良好（且正确选择的）智能指针不会这样做。

3. 当是内入式时，它们拥有的对象需要持有它；否则它们可以在空存储区上持有这些信息。

4. 列表需要进行双向遍历，因此它需要是双向链表。

### 练习题

1. `object->DoSomething ();` 是错误的，因为指针丢失了所有权。

2. 这种方法会崩溃（或者发生某些不）。代码应该如下所示：

```cpp
#include <memory>
#include <iostream>
using namespace std;
class Fish
{
public:
    Fish() {cout << "Fish: Constructed!" << endl;}
    ~Fish() {cout << "Fish: Destructed!" << endl;}
    void Swim() const {cout << "Fish swims in water" << endl;}
};
class Carp: public Fish
{
};
void MakeFishSwim(const unique_ptr<Fish>& inFish)
{
    inFish->Swim();
}
int main ()
{
    unique_ptr<Fish> myCarp (new Carp); // 注意这里
    MakeFishSwim(myCarp);
    return 0;
}
```

3. 因为其拷贝构造函数和拷贝赋值运算符都是私有的。

#### 第 27 课答案

### 测验

1. 使用 `ofstream` 只写入文件。

2. 你将使用 `cin.getline()`。参见 列表 27.7。

3. 不，因为 `std::string` 包含文本信息，你可以保持默认模式（无需二进制模式）。

4. 为了检查 `open()` 是否成功。如果失败，你可能想显示错误并暂停文件处理。

### 练习题

1. 你打开了文件，但在使用流或关闭它之前没有使用 `is_open()` 检查是否成功。

2. 你不能插入到 `ifstream`，它是为输入设计的而不是输出，因此不支持流插入 `operator<<`。

#### 第 28 课答案

### 测验

1. 一个和其他类一样的类，但被专门创建作为其他异常类（如 `bad_alloc`）的基类。

2. `std::bad_alloc`

3. 这是一个坏主意，因为异常最初可能是由于内存不足而抛出的。

4. 使用同样适用于类型 `bad_alloc` 的 `catch(std::exception& exp)`。

### 练习题

1. 永远不要析构函数中抛出异常。

2. 你忘记让代码异常安全（缺少 `try... catch` 块）。

3. 不要在 catch 块中分配内存！假设 `try` 块中分配的数据已丢失并继续进行损害控制。

#### 第 29 课答案

### 测验



1. 似乎你的应用程序在一个线程中执行所有活动。因此，如果图像处理本身（对比度调整）是计算密集型的，UI 将无响应。你应当将这两种活动拆分为两个线程，以便操作系统切换这两个线程，给 UI 和执行调整的执行线程都分配处理器时间。

2. 你的线程可能同步得不好。你正在同时对一个对象进行写入和读取，导致数据恢复不一致或混乱。插入一个二进制信号量，并确保在修改表格时无法访问它。

- `=`（赋值）运算符，87, 357–360
- `\`（反斜杠），76–78, 86
- `&`（按位与）运算符，100–102, 624
- `>>`（按位右移）运算符，102–104
- `~`（按位取反）运算符，100–102
- `|`（按位或）运算符，100–102, 624
- `^`（按位异异）运算符，100–102, 624
- `{ }`（大括号），48, 87
- `:`（冒号），10, 232
- `//` 注释语法，23, 28
- `/* */` 注释语法，23, 28
- `?:`（条件）运算符，126–127
- `--`（自减）运算符，89, 190–193, 338–341
- `*`（解引用）运算符，183–185, 344–345, 635, 639
- `.`（点）运算符，218–219
- `/`（除法）运算符，88–89
- `...`（省略号），415
- `==`（等等）运算符，92, 352
- `>>`（提取）运算符，27, 624, 649, 663–664
- `>`（大于）运算符，92–94, 354–357
- `>=`（大于等于）运算符，354–357
- `!=`（不等）运算符，92, 352
- `++`（自增）运算符，89, 191–193, 338–341, 26, 624, 649, 662, 624
- `<`（小于）运算符，92–94, 354–357
- `<=`（小于等于）运算符，92–94, 354–357
- `&&`（逻辑与）运算符，95–100
- `||`（逻辑或）运算符，95–100
- `!`（逻辑取反）运算符，95–100
- `->`（成员选择）运算符，219–220, 344–345, 635, 639
- `%`（取模）运算符，88–89
- `*`（乘法）运算符，88–89
- `()`（括号），364–365, 398–399
- `&`（引用）运算符，179–180
- `>>=`（右移）运算符，624
- `[]`（下标）运算符，197–198, 360–364, 462, 555
- `~`（波浪号），234
- `""` 运算符，451–452
- `::`（作用域）运算符，225
- `;`（分号），12, 86, 216
- `’`（单引号），45
- `-`（减法）运算符，88–89, 347–349
- `0x` 前缀，704
- `\0` 字符串终止字符，76–78, 82

### A

- 抽象基类，318–320, 332
- 访问说明符，274
- 适配器，容器，425
- 适配容器，*参见* 队列；栈
- 适配器对象，538
- 加加赋值（`+=`）运算符，442–443
- 加（`+`）运算符，88–89, 347–349
- 变量地址，确定，179–180
- 在指针中存储，180–182
- 相邻的 `find()`，571
- C++ 的优势，6
- 聚合初始化，263–266
- 聚合，296
- 算法，*参见* 容器；特定算法（`for`，`for_each()`），570, 618
- 应该与不要，599
- 解释，426
- 与容器的交互，427–429
- 变异算法，571–573
- 非变异算法，570–571
- 变换，585–588
- 内存分配，*参见* 动态内存
- 美国标准信息交换（ASCII）编码，41, 711–715
- AND 运算符
  - 按位与（`&&`），100–102, 624
  - 逻辑与（`&&`），95–100
- 尖括号（`<>`），19
- 应用类，661
- 应用常量，661
- `append()`，442–443
- `Area()`，152–153, 158–159
- 参数
  - 值数组，165–166
  - 默认值，157–159
  - 定义，19, 154
  - 多参数，155–156
  - 无参数，156–157
  - 引用传递，166–168, 208–209
- 算术运算符，88–89, 347–349
- 数组类，699
- 数组运算符（`[]`），197–198
- 数组，*参见* 字符串类
  - 访问数据，67–68
  - 与指针比较，195–198
  - 定义，64
  - 应该与不要，71
  - 动态数组，66, 74–76, 469–472
  - 解释，65
  - 在其中修改数据，69–71
  - 多维数组，71–73, 145–146
  - 性，64–65
  - 传递给函数，165–166
  - 尺寸，82–83
  - 静态数组，65–66
  - 在其中存储数据，66–67
- `ASCII（美国标准信息交换码）`，41, 711–715
- `assert()` 宏，399–400
- `赋值运算符（=）`，87, 357–360。另见复合赋值运算符
- `关联容器`，423–424
- `ate 常量`，661
- `auto` 关键字，12–13, 48–50, 171–172, 493
- `auto_ptr` 类，640–643
- `自动类型推导`，48–50, 171–172, 698–699

### B

- `back()`，611
- `反斜杠（\）`，76–78, 86
- `bad_alloc` 类，679
- `bad_cast` 类，679
- `基类方法`
  - 隐藏，286
  - 初始化，279–281
  - 调用，283–286
  - 被重写的方法，281–284
- `basic_string` 类，450–451
- `begin()`，481–482
- `最佳实践`，693–694
- `双向迭代器`，426
- `二进制常量`，661
- `二进制文件，读写`，664–665
- `二进制函数`，545–550
- `二进制字面量`，51
- `二进制进制`，702–703, 705
- `二进制运算符`
  - 算术运算符，347–349
  - 复合赋值运算符，350–352
  - 拷贝赋值，357–360
  - 相等/相等，352
  - 解释，346
  - 函数，364–365
  - 移动赋值，365–371
  - 移动构造函数，365–371
  - 关系运算符，354–357
  - 下标 `()`，360–364
- `二进制谓词`，363, 547–550
- `binary_search()`，573, 592–595
- `位`，703
- `bitset` 类，622–627, 706
- `位运算符`，100–104, 624
- `块`，87, 117–118
- `bool` 类型，40
- `布尔变量，声明`，40
- `Boost 线程库`，645, 690
- `大括号（{ }）`，48, 87
- `break` 语句，139–140
- `拆解方法`，705
- `桶`，507
- `虫`，8
- `字节`，703

### C

- `.c` 文件扩展名，9
- `c_str()`，440
- `C++`
  - 优势，6
  - 演变，7
  - 历史，6
  - 新功能，12–13
  - 修订，12–13
- `C++17`，695–699
- `捕获列表`，559–560
- `用用例，转换`，449–450
- `大小写敏感`，20, 398
- `转换`
  - `const_cast` 运算符，385–386
  - C 风格转换，379
  - 做的与不要，388
  - `dynamic_cast` 运算符，381–384
  - 解释，377
  - 需要，378
  - 带来的，386–387
  - `reinterpret_cast` 运算符，384–385
  - `static_cast` 运算符，380–381
  - 向上转型，380
- `catch` 关键字，673–675
- `异常异常`
  - 所有异常，673–674
  - `catch` 关键字，673–675
  - 示例，677–679
  - 类型异常，674–675
  - 内存分配失败，202–204
  - `try` 关键字，673
- `cbegin()`，442
- `cerr` 类，651
- `char 缓冲区，写入`，657–658
- `char` 类型，41
- `字符变量，声明`，41
- `块分隔符`，45
- `cin` 类，26–28, 651, 656–660
- `Circumference()`，152–153
- `类`。另见构造函数；析构函数；继承；单个类（例如，`fstream` 类）
  - 访问成员，218–220
  - 聚合初始化，263–266
  - 聚合，296
  - 与结构体比较，257–258
  - 组合，296
  - `constexpr` 关键字，266–267
  - 声明，216–217
  - 深层拷贝，240–244
  - 解释，216
  - 友类，258–260
  - 实例化，217–218
  - 禁止在栈上实例化，249–251
  - 命名规范，219
- 不可拷贝对象，246
- `private` 关键字，220–224
- `public` 关键字，220–222
- 浅拷贝，237–240
- 单例类，247–249
- `sizeof()`，255–257
- 子类，275
- 父类，275
- 联合体，260–266
- `clear()`，472, 483
- `Clone()`，638
- `CodeGuru`，699
- `CodeProject`，699
- 集合，向其插入元素，597–599
- 冲突，529
- 冒号（`:`），10
- 注释，18, 23, 28
- 编译，8。另见预处理器指令
- 编译器，10–12, 13, 709–710
- 编译时检查，417–418
- 编译时错误，14
- 条件代码编译，697–698
- 示例，10–12
- 运算符优先级，709–710
- 编译型语言，13
- 复杂度，424
- 组合，296
- 复合赋值运算符，104–106, 350–352
- 复合语句，87, 117–118
- 字符串拼接，79–81, 442–443
- 条件代码编译，697–698
- 条件运算符（`?:`），126–127
- 条件编程

### 条件编程

- 条件运算符（`?:`），126–127
- `if` 语句，114–122
- 循环。见循环
- `switch-case` 语句，122–125
- `const` 关键字，52–53, 193–194, 208, 363
- `const_cast` 运算符，385–386
- 常量中的，661
- 复杂度，424
- 常量表达式，53–55
- 常量。另见变量
- 常量表达式，53–55
- 声明常量，52–53
- 定义的，50–51
- 定义，57, 59, 392–394
- 枚举符，55–57
- 字面量常量，51–52, 371–372
- 命名规范，58–59
- `constexpr` 关键字，53–55, 233, 266–267
- 构造顺序，288

## 构造函数

- 自动类型推导，698–699
- 没有默认构造函数的类，228–230
- 转换构造函数，251–253
- 拷贝构造函数，233–244
- 声明，224–225
- 默认构造函数，228–230
- 默认值，230–231
- 初始化列表，231–233
- 移动构造函数，244–245
- 构造顺序，288
- 重载，227–228
- 用途，246–253
- 虚拷贝构造函数，328–331
- 何时使用，225–226

### 容器

- 关联型容器，423–424
- 选择，429–431
- 容器适配器，425
- 定义，422
- 拷贝和删除操作，588–590
- 计数，576–577
- 查找，573–575
- 初始化，580–583
- 插入集合中，597–599
- 分区，595–597
- 处理，583–585
- 替换，590–592
- 搜索，577–579
- 排序，592–595
- 与算法交互，427–429
- 队列，604–618
- 顺序容器，422–423
- 栈，604–608
- `continue` 语句，139–140
- 传统指针，634
- 转换运算符，341–343
- 转换构造函数，251–253
- `copy()`，572, 588–590
- 拷贝赋值运算符，357–360
- 拷贝构造函数，233–244
- 拷贝消除，696
- 写时拷贝（COW），639
- `copy_backward()`，572, 588–590, 600
- `copy_if()`，588–590
- `count()`，500, 570, 576–577, 625
- `count_if()`，570, 576–577
- `cout` 类，651, 653–656, 706

### D

- 野悬指针，200–201
- 死锁，692
- 调试，8
- 进制计数制，702, 705–706
- 递减运算符（`--`），8, 191–193, 338–341
- `deepcopy_smart_ptr` 类，637–639
- 基于深拷贝的智能指针，637–639
- 默认构造函数，228–230
- 默认模板参数，407–408
- 带有默认值的函数参数，157–159
- `#define` 指令，57
- 使用……定义常量，392–394
- 使用……编写宏函数，396–398
- 定义（函数），154
- `delete` 运算符，187–190
- `DemoConsoleOutput()`，24–26
- `deque` 类，422, 469–472
- 解引用运算符（`*`），344–345
- 解引用运算符（`*`），183–185, 635, 639
- 派生，272–276
- `DerivedFunction()`，380
- 析构顺序，288–290
- 破坏性拷贝智能指针，640–643
- 析构函数，635
  - 声明，233–234
  - 析构顺序，288–290
  - 私有析构函数，249–251
  - 虚拟析构函数，310–314
  - 何时使用，234–237
- 指令。参见预处理器指令
- 改变数字格式，653–655
- `DisplayArray()`，165–166
- `DisplayComparison()`，405
- `DisplayContents()`，500
- `ElementCount()`，541–543
- `DisplayTuple()`，416–417
- `DisplayVector()`，467
- 除除运算符（`/`），88–89
- `do...while` 循环，132–133
- 文档，699
- 点运算符（`.`），218–219
- `double` 类型，45
- 动态数组。参见 `vector` 类
  - 声明，74–76
  - 定义，66
  - `deque` 类，469–472
- 动态内存分配
  - `delete` 运算符，187–190
  - 解释，187
  - 内存分配失败，202–204
  - `new` 运算符，187–190
- `dynamic_cast` 运算符，381–384

### E

- Eclipse IDE，8
- 省号（`...`），415
- `empty()`，472, 611, 615
- 空返回值，156–157
- `end()`，481–482
- `#endif` 指令，395–396
- `endl` 操纵符，652
- `ends` 操纵符，652
- 枚举，55–57
- 举员，55–57
- `equal()`，571
- 等于运算符（`==`），92, 352
- `erase()`，445–447, 482–483, 502–506, 522–524
- 错误。参见异常
- 编译器错误，12
- 编译时错误，14
- 调试，8
- 差一错误（fence-post errors），70
- 窄转换错误，48
- 溢出错误，43–44
- 运行时错误，14

## C++ 的进化

- `exception` 类，679–680
- 异常。参见错误（[index.html_index29](index.html_index29)）
- 捕获，673–679
- 异常产生，672
- 自定义类，680–682
- 定义，671
- do...s 和 don...ts，682



- `std::exception` 类，679–680
- 抛出，676–679
- 异或 OR 运算符，95–96
- 生成可执行文件，7–8
- `explicit` 关键字，252–253
- `explicit` 类型声明，493
- 表达式。*参见 lambda 表达式*
- 常量，53–55
- 有效，399–400
- 提取运算符（`>>`），27、624、649、663–664

### F

- 内存分配失败，202–204
- 尔尔假值（false value），94
- 差一错误，70
- 斐波那契数计算，145–146
- 计算斐波那契数，159–161
- 字段宽度设置，655–656
- 文件名扩展，8、9
- `fill()`，571、580
- `fill_n()`，571、580
- 结束指示符，300、327、708
- `find()`，426、444–447、500–502、519–522、571、573–575
- `find_end()`，571
- `find_first_of()`，571
- `find_if()`，426、558、571、573–575
- `fixed` 操纵符，652
- 固定宽度整数类型，47
- 控制流。*参见程序流、控制*
- `for_each()`，554、555–556、572、583–585
- 前向迭代器，425–426
- 正斜杠（`/`），88–89
- `forward_list` 类，422、490–492
- 友类，258–260
- `front()`，611
- `fstream` 类，651
  - 打开/关闭文件，660–661
  - 读取二进制文件，664–665
  - 读取文本文件，663–664
  - 写入二进制文件，664–665
  - 写入文本文件，662–663
- `FuncDisplayElement()`，538–541
- 函数对象
  - 二元函数，545–550、562–563
  - 定义，528
  - 解释，538
  - 一元函数，538–545、555–557
- 函数运算符，364–365
- 函数原型，153–154
- `<functional>`，615
- 函数。*参见参数；函数对象；宏；虚拟函数；特定函数（例如 `count()`）*
  - 自动返回类型推导，171–172
  - 定义，154
  - 解释，23–26
  - 内联函数，169–171
  - 微处理器级实现的，168–169
  - 多重返回语句，161
  - 必要性，152–153
  - 重载，163–164
  - 防止被重写的函数，327
  - 向传递指针，194–195
  - 在指针中存储地址，180–182
  - 原型，153–154
  - 模板函数，403–405
- 仿函数。*参见函数对象*

### G

- `g++` 编译器，8、10
- `generate()`，571、581–583
- `generate_n()`，581–583
- `get()`，668
- `GetFibNumber()`，159
- `GetInstance()`，249
- `getline()`，28、659–660、668
- `GetMax()`，403–405
- `GetPi()`，53–54、169–171
- GHz（千赫），688
- gigabytes，704
- 全局变量，37–38、60
- `goto` 循环，128–130
- 大于（`>`）运算符，92–94、354–357
- 大于等于（`>=`）运算符，354–357
- 分组的 `if...else` 结构，121–122

### H

- 处理异常。*参见异常*
- hash set，507–509
- hash 表，528–533
- `HashFunction()`，529
- 头文件中的包含保护符，419
- Hello World 程序，9–11、18
- 十六进制操作符，652
- 十六进制计数法，178、704–705、706–706
- C++ 历史
- `HoldsPair` 模板，408–409
- 匈牙利命名，38–39
- Hz（赫兹），688

### I

- IDEs（集成开发环境），8–9、38–39
- `if` 语句，114–122、695–696
- `#ifndef` 指令，395–396
- `ifstream` 类，651
- 隐式转换，343
- `#include` 指令，18–19、28
- 包含保护符，395–396、419
- 自增（`++`）运算符，89、191–193、338–341
- 不等（`!=`）运算符，92、352
- 无限循环，141–143
- 使用 `final` 避免继承，300
- 基类方法，279–286
- `do` 的准与不要，301
- 多重继承，297–300
- 构造顺序，288
- 析构顺序，288–290
- 私有继承，291
- `protected`，276–279
- `protected` 继承，293–296
- `public`，273–274
- 切片（slicing），297
- 初始化列表，231–233
- 初始化语句，695–696
- 内联函数，169–171
- `inline` 关键字，169–171
- 输入迭代器，425
- 输入/输出，26–28。*参见流*
- `insert()`，459–462、479–482、499、608
- 插入运算符（`<<`），26、624、649、662
- `int` 关键字，19–20
- `int` 类型，42
- `int8_t` 类型，47
- `int16_t` 类型，47
- `int32_t` 类型，47
- `int64_t` 类型，47
- 整数，60
  - 固定宽度，47
  - 有符号，41–42
  - unsigned，61
- 集成开发环境（IDEs），8–9、38–39
- 国际标准组织（ISO），6、11
- 解释型语言，13
- 侵入式引用，639
- 无效内存地址，199
- `<iomanip>` 操符，652
- iostream 文件，18
- ISO（国际标准组织），6、11
- 迭代语句。*参见循环*
- 迭代器，425–426、429、534–535、630

### J-K-L

- 关键字，列表，58–59、707–708。*另请参见各个关键字（例如 `auto`）*
- 千字节，704–704
- lambda 表达式
  - 用于二元函数，562–563
  - 用于二元谓词，564–566
  - 在 C++17 中，698
  - 准与忌，566
  - 解释，12–13、172–174、554–555
  - 其中的局部变量，567
  - 状态维护，559–560、567
  - 语法，560–562
  - 用于一元函数，555–557
  - 用于一元谓词，557–558
- 内存泄漏，188、198–204
- 左移运算符（`<<`），102–104
- 确定字符串长度，79–81
- 较于，522–524
- 小于（`<`）运算符，92–94、354–357
- 小于等于（`<=`）运算符，92–94、354–357
- `lexicographical_compare()`，571
- 换行，12
- 线性复杂度，424
- 列表，422
  - 捕获列表，559–560
  - 准与忌，492
  - 从中删除元素，482–483
  - 初始化，48、459
  - 初始化列表，231–233
  - 插入元素，478–482
  - 实例化，476–477
  - 从中移除元素，487–490
  - 反转元素，484–485
  - 排序元素，485–486
- 字面量常量，51–52、371–372
- `load_factor()`，509、530
- lambda 表达式中的局部变量，567
- 对数复杂度，424
- 逻辑与（`&&`）运算符，95–100
- 逻辑非（`!`）运算符，95–100
- 逻辑或（`||`）运算符，95–100
- 逻辑异异运算符，95–96
- `long long` 类型，42
- `long` 类型，42
- `for` 循环，133–139
- 循环
  - 访问数组，71
  - `do...while`，132–133
  - 退出，139–140
  - `for`，133–139
  - `goto`，128–130
  - 无限，141–143
  - 嵌套，143–148
  - 恢复执行，139–140
  - `while`，130–132
- `lower_bound()`，573、597–599
- 将字符串转为小写，449–450
- l-值，87–88
- 宏
  - 优点/缺点，400–401
  - `assert()`，399–400
  - 大小敏感性，398
  - 与模板相比，419
  - 准与忌，401
  - 包含保护符中的，395–396
  - 括号中的，398–399
  - 使用……防止多次包含，395–396
  - 元组，415–417
  - 编写，396–398
- `main()`，19–20
- 流操符，651–652
- `map` 类，423
  - 自定义谓词，525–528
  - 从中删除元素，522–524
  - 解释，514
  - 查找元素，517–519
  - 插入元素，519–521
  - 实例化，515–516
- `max_bucket_count()`，509
- `max_load_factor()`，509
- 千字节，704
- 赫兹（Mhz），688
- 成员运算符（`->`），344–345、635、639
- 内存。*参见指针*
- 使用变量访问。*参见变量*
- 动态内存分配，187–190、202–204
- l-值，87–88
- 内存泄漏，188、198–204
- RAM（随机存取内存），32
- 原始指针，634
- r-值，87–88
- 栈，169
- 确定变量地址，179–180
- 方法。*参见函数*
- 赫兹（Mhz），688
- Microsoft Visual Studio Express，8
- MIN 宏，397、400–401
- `mismatch()`，571
- 模运算运算符（`%`），88–89
- 移动赋值运算符，365–371
- 移动构造函数运算符，365–371
- 移动构造函数，244–245
- 多核处理器，688–689
- 多维数组，71–74、145–146
- `multimap` 类，423
  - 自定义排序谓词，525–528
  - 从中删除元素，522–524
  - 在其中查找元素，522
  - 向中插入元素，517–519
  - 实例化，515–516
- 多次包含，防止措施，395–396
- 多重继承，297–300
- 乘法运算符（`*`），88–89
- `MultiplyNumbers()`，35–36
- `multiset` 类，423、496–510
  - 要做与不要，510
  - 在其中删除元素，502–506
  - 详解，496
  - 在其中查找元素，500–502
  - 向中插入元素，499–500
  - 实例化，497–498
  - 优缺点，507
- 多线程，690–693
- 变异算法，571–573
- `mutex` 类，692

### N

- `[N]` 运算符，624
- 命名空间，21–22
- 命名规范
  - 类，219
  - 常量，58–59
  - 变量，34、38–39、58–59
- 窄转换错误，48
- 嵌套 `if` 语句，118–122
- 嵌套循环，143–148
- .NET，6
- `new` 运算符，187–190、202–204
- `new(row)` 运算符，204、210
- 不可拷贝对象，246
- 非变异算法，570–571
- NOT 运算符
  - 按位非（`~`），100–102
  - 逻辑非（`!`），95–100
- 空终止符，76–82
- 数值代码（ASCII），41、711–715

### O

- `.o` 文件扩展，8
- `.obj` 文件扩展，8
- 创建对象，217–218
- `oct` 操符，652
- 八进制数字，705
- OFF 状态，702
- `ofstream` 类，651
- 在线社区，699
- 在线文档，699
- `open()`，660、662–664
- `operator` 关键字，336
- 运算符。另参见二进制运算符；类型转换；重载运算符；一元运算符
  - 声明，336
  - 要做与不要，374
  - 详解，336–337
  - 优先级，108–109、709–710
  - 前缀与后缀，90–91
- 构造顺序，288
- 析构顺序，288–290
- OR 运算符
  - 按位或（`|`），100–102、624
  - 逻辑或（`||`），95–100
- `out` 常量，661
- 输出，26–28。另参见流
- 输出迭代器，425
- 溢出错误，43–44
- 重载构造函数，227–228
- 重载函数，163–164
- 重载运算符，635
  - 拷贝赋值，357–360
  - 等价/不相等，352
  - 不可重载的运算符，373
  - 关系运算符，354–357
- 重写函数，281–284、327
- `override` 标识符，326–327、708

### P

- `partial_sort()`，572
- `partial_sort_copy()`，573
- `partition()`，573、595–597
- POD（Plain Old Data），45、656–657
- 指针运算符（`->`），219–220、344–345
- 指针。另参见智能指针
  - 在其中访问数据，183–185
  - 与数组比较，195–198
  - `const` 关键字，193–194
  - 声明，178–179、180
  - 递减运算符（`--`），191–193
  - 定义，178
  - 要做与不要，205
  - 动态内存分配，187–190
  - 递增运算符（`++`），191–193
  - 传递给函数，194–195
  - 原始指针，634
  - `sizeof()`，185–186
  - `this`，254
- 多态。另参见虚函数
  - 抽象基类，318–320、332
  - 定义，306
  - 要做与不要，331
  - 需要，306–308
- `pop()`，607–608、611–613、616–618
- pop 操作，169
- `pop_back()`，465–466
- `pop_front()`，470–472
- 后缀运算符，90–91
- 运算符优先级，108–109
- 谓词（predicates），363
  - 二元谓词，547–550
  - 自定义排序谓词，522–524
  - 一元谓词，543–545、557–558
- 前缀（prefix），21–22
- 前缀运算符，90–91
- 预处理器（preprocessor），392
- 预处理器指令
  - `#define`，57、392–398
  - `defined`，18
  - `#endif`，395–396，解释，392
  - `#ifndef`，395–396
  - `#include`，18–19
- 可打印字符（ASCII），41、711–715
- `priority_queue` 类，425、613–618
- 私有析构函数，249–251
- 私有继承，291
- `private` 关键字，220–224、291
- 多核处理器，688–689
- 程序流，控制。*另见循环*
  - 条件运算符（`?:`），126–127
  - `if` 语句，114–122
  - `switch-case` 语句，122–125
- 程序
  - 构建，10–11
  - 编译，8、10–12
  - 可执行文件，7–8
  - 执行，10–11
  - 结构，18–28
- 保护继承，276–279、293–296
- `protected` 关键字，276–279、293
- 函数原型，153–154
- 公有继承，273–274
- `public` 关键字，220–222、273–274、527
- 纯虚函数，318–320
- `push()`，607–608、611–613、616–618
- `push` 操作，169
- `push_back()`，76、458、470–472、478–479、608、629
- `push_front()`，470–472、478–479
- Q-队列
  - 解释，425、604–605
  - 运算符，628–629
  - `priority_queue` 类，613–618
  - `queue` 类，425、609–613
- 竞态条件（race conditions），692
- RAM（随机访问），32
- 随机访问迭代器，426
- 基于范围的循环，137–139
- 原始指针，634
- `read()`，664–665
- 递归，159–161
- 引用（references）
  - `const` 关键字，208
  - 解释，205–206
  - 侵入式引用计数，639
  - 引用的必要性，206–208
  - 引用传递，166–168、208–209
  - 引用计数智能指针，639–640
  - 引用链接智能指针，640
  - 引用运算符（`&`），179–180
- 改进（refements），426
- `reinterpret_cast` 运算符，384–385
- 关系运算符，92–94、354–357
- `remove()`，572、590



- `remove_copy()`, 572
- `remove_if()`, 426, 550, 572, 590
- `replace()`, 572, 590
- `replace_if()`, 572, 590
- `reserve()`, 473

## 保留关键字

另见 关键字列表

- `reset()`, 625
- `resetflags()`, 653–654
- `resetiosflag` 操符, 652
- 恢复循环执行, 139–140
- `return` 语句, 161
- `return` 值, 20
- `reverse()`, 448–449
- `reverse` 算法, 426
- 右移运算符 (`>>`), 102–104

## RTTI (类型识别), 318

## 安全 (类型), 405

## 科学操符, 652

## 变量作用域, 35–36

## 作用域解析 (`::`), 225

- `search()`, 570, 577–579
- `search_n()`, 570, 577–579

## 信号量 (semaphores), 692

## 分隔符, 分块, 45

## 顺序性容器, 422–423

- `set()`, 625

## set 类

准与忌, 510
- 删除其中的元素, 502–506
- 解释, 423, 496–510
- 在其中查找元素, 500–502
- 向其中插入元素, 499–500
- 实例化, 497–498
- 优缺点, 507

## `setbase` 操符, 652

- `setfill()`, 652, 655–656
- `setiosflags()`, 652, 653–654

## `setprecision()`, 652

`setw()`, 652, 655–656

浅拷贝, 237–240

`shared_ptr` 类, 645

移位运算符, 102–104

short 类型, 42

有符号整数, 41–42

单引号 (’), 45

单例类, 247–249

`size()`, 611, 615, 625

`sizeof()`, 46–47, 106–107, 185–186, 255–257

切片, 297, 637–638

## 智能指针的优势, 634–635

`auto_ptr`, 640–643
COW (写时拷贝), 639
深拷贝, 637–639
定义, 344, 634
破坏性拷贝, 640–643
实现, 635–636
库, 645
引用计数, 639–640
引用链接, 640
`shared_ptr`, 645
切片问题, 637–638
`unique_ptr`, 643–645
`weak_ptr`, 645

`sort()`, 485–486, 547–550, 564–566, 572, 592–595, 600

特化 (模板), 410–411

SQUARE 宏, 396–397

`stable_partition()`, 573, 595–597

`stable_sort()`, 572, 595

StackOverflow, 699

## 栈, 169, 604

在栈中插入和移除元素, 607–608
实例化, 605–606
成员函数, 606–607
在...禁止实例化, 249–251

`stack` 类, 425, 605–608

ON 状态, 702

## 语句

另参见 循环

块, 87, 117–118
break, 139–140
continue, 139–140
`cout`, 20
解释, 86
`if`, 114–122
初始化, 695–696
return, 161
`switch`, 695–696
`switch-case`, 122–125

静态数组, 65–66

`static` 关键字, 247–248

静态成员, 412–413

`static_assert`, 417–418

`static_cast` 运算符, 380–381

`std` 命名空间, 21–22

野指针指针, 200–201

`strcat()`, 79

`strcpy()`, 79

## 流

`cin` 类, 656–660
类, 651
`cout` 类, 653–656
解释, 649–650
提取运算符 (>>), 649
`fstream` 类, 660–665
插入运算符 (<<), 649
操纵符, 651–652
`stringstream` 类, 665–668

## `string` 类, 79–81, 432

在...中的“”运算符, 451–452
访问, 440–442
拼接, 442–443
转换大小写, 449–450
在...中查找字符, 444–445
实例化, 437–440
需要, 436–437
反转内容, 448–449
基于模板的, 450–451
截断, 445–447
写入到, 658–650

静态字符串, 79

`string_view` 类, 432

`stringstream` 类, 665–668

`strlen()`, 79

结构体, 247–248

减法运算符, 88–89

类型, 449

多态。另参见 循环

同步，线程, 691, 692

## 哈希表, 528–533

虚函数表, 314–318

`template<auto>`, 699

## templates

与宏对比, 419
编译时检查, 417–418
声明, 402–408
做的与不要做的, 418
解释, 402
HoldsPair 示例, 408–409
实例化, 410–411
编程应用的, 418
特化, 410–411
静态成员, 412–413
模板类, 406–407
变量模板, 413–417

# 太字节 (terabytes), 704

# 文件

关闭, 660–661
打开, 660–661
读取, 663–664
写入, 662–663

# this 指针 (this pointer), 254

# 线程 (threads), 689–693

# throw 关键字, 676–677

# 抛出异常 (throwing exceptions), 676–679, 683

# 波浪号 (~), 100–102

# `top()`, 615

# `transform()`, 426, 449–450, 545–547, 562–563, 572, 585–588

# 转换 (transformations), 585–588

# 真值 (true value), 94

# trunc 常量 (trunc constant), 661

# try 关键字, 673

# tuple 类 (tuple class), 415–417

# `TwicePi()`, 53–54

# typedef 关键字, 50

# 类型 (types)

自动类型推导 (automatic type deduction), 48–50, 698–699
bool, 40
类型转换 (casting), 377–388
char, 41
转换 (conversion), 251–253
double, 45
异常类型处理 (exceptions of type, handling), 674–675
显式类型声明 (explicit type declaration), 493
固定宽度整数类型 (fixed-width integer types), 47
float, 45
int, 42
迭代器类型定义 (iterator type definitions), 429
long, 42
long long, 42
溢出错误 (overflow errors), 43–44
RTTI (运行时类型识别), 382
short, 42
表格 (table of), 39–40
类型安全与模板 (type safety, templates and), 405
类型替换 (type substitution), 50
unsigned int, 42–43
unsigned long, 42–43
unsigned long long, 42–43
unsigned short, 42–43

## uint

`uint8_t` 类型, 47
`uint16_t` 类型, 47
`uint32_t` 类型, 47
`uint64_t` 类型, 47

## 单元函数 (unary functions), 53–545

## unary

单元运算符 (unary conversion operators), 341–343
解引用 (dereference), 344–345
解释 (explained), 337–338
自增/自减 (increment/decrement), 89, 338–341
逻辑运算符 (logical operators), 95–100
成员选择 (member selection), 344–345
单元谓词 (unary predicates), 363, 543–545, 557–558

## unions

聚合初始化 (aggregate initialization), 263–266
声明 (declaring), 260–263
类型安全的 (typesafe to), 697
何时使用, 261–263

`unique()`, 572
`unique_copy()`, 572
`unique_ptr` 类 (unique_ptr class), 643–645
`unordered_map` 类 (unordered_map class), 423, 528–533
`unordered_multimap` 类 (unordered_multimap class), 423, 528–533
`unordered_multiset` 类 (unordered_multiset class), 423, 507–509
`unordered_set` 类 (unordered_set class), 423, 507–509
`unsigned int` 类型, 42–43
无符号整数 (unsigned integers), 42–43, 61
`unsigned long long` 类型, 42–43
`unsigned long` 类型, 42–43
`unsigned short` 类型, 42–43
上转型转换 (upcasting), 380
`upper_bound()`, 573, 597–599
字符串转大写 (uppercase, converting strings to), 449–450
用户界面线程 (User Interface Threads), 690
用户定义字面量 (user-defined literals), 52, 371–372
使用关键字 (using keyword), 21–22

## V values

默认值 (default values), 157–159
传递值数组 (passing to arrays of values), 165–166
通过引用传递 (by reference), 166–168

## 可变模板 (variable templates), 413–417

变量。另见 constants; types

## addresses

确定 (determining), 179–180
指针存储 (storing in pointers), 180–182

## declaring

自动类型推断 (declaring automatic type inference), 48–50
布尔 (Boolean), 40
字符 (character), 41
浮点型变量 (floating-point variables), 45
多个变量 (multiple variables), 34
溢出错误 (overflow errors), 43–44
有符号变量 (signed variables), 42
单个变量 (single variables), 32–34
无符号变量 (unsigned variables), 42–43

全局变量 (global variables), 37–38, 60
初始化 (initializing), 60
整数 (integers), 60
列表初始化 (list initialization), 48
局部变量 (local variables), 567
命名规范 (naming conventions), 38–39, 58–59
窄转换错误 (narrowing conversion errors), 48
作用域 (scope), 35–36
大小 (size of), 46–47

## 变变模板 (variadic templates), 413–417

`variant` 类 (variant class), 263, 697

## `vector` 类 (vector class), 74–76, 422

在其中访问元素 (accessing elements in), 462–465
特性 (characteristics of), 455–456
准与禁 (do’s and don’t), 472
初始化 (initialization), 459
向其中插入元素 (inserting elements into), 458–462
实例化 (instantiating), 456–457
从中移除元素 (removing elements from), 465–466
大小和容量 (size and capacity of), 467–469

## `vector<bool>`

使用迭代器访问 (accessing with iterators), 630
解释, 627
函数, 628–629
实例化, 627–628
指定元素数量, 630

虚拷贝构造函数, 328–331
虚析构函数, 310–314
虚函数表, 314–318

## 虚拟函数

抽象基类, 318–320
声明, 308–310
注意事项, 331
final 饰符, 327
继承, 321–325
override 饰符, 326–327
纯虚函数, 318–320
虚函数表, 314–318
虚继承, 321–325
`virtual` 关键字, 318, 324–325, 332

## W-X-Y-Z

警告信息, 13
`weak_ptr` 类, 645
while 循环, 130–132
野指针, 200–201
工作线程, 690
`write()`, 664–665
`wstring` 类, 432, 450–451

## XOR 异或运算符

位异或, 100–102, 624
逻辑异或, 95–96

## 代码片段

![Image](image1)
![Image](image2)
![Image](image3)
![Image](image4)
![Image](image5)
![Image](image6)
![Image](image7)
![Image](image8)
![Image](image9)
![Image](image10)
![Image](image11)
![Image](image12)
![Image](image13)
![Image](image14)
![Image](image15)
![Image](image16)
![Image](image17)
![Image](image18)
![Image](image19)
![Image](image20)
![Image](image21)
![Image](image22)
![Image](image23)
![Image](image24)
![Image](image25)
![Image](image26)
![Image](image27)
![Image](image28)
![Image](image29)
![Image](image30)
![Image](image31)
![Image](image32)
![Image](image33)
![Image](image34)
![Image](image35)
![Image](image36)
![Image](image37)
![Image](image38)
![Image](image39)
![Image](image40)
![Image](image41)
![Image](image42)
![Image](image43)
![Image](image44)
![Image](image45)
![Image](image46)
![Image](image47)
![Image](image48)
![Image](image49)
![Image](image50)
![Image](image51)
![Image](image52)
![Image](image53)
![Image](image54)
![Image](image55)
![Image](image56)
![Image](image57)
![Image](image58)
![Image](image59)
![Image](image60)
![Image](image61)
![Image](image62)
![Image](image63)
![Image](image64)
![Image](image65)
![Image](image66)
![Image](image67)
![Image](image68)
![Image](image69)
![Image](image70)
![Image](image71)
![Image](image72)
![Image](image73)
![Image](image74)
![Image](image75)
![Image](image76)
![Image](image77)
![Image](image78)
![Image](image79)
![Image](image80)
![Image](image81)
![Image](image82)
![Image](image83)
![Image](image84)
![Image](image85)
![Image](image86)
![Image](image87)
![Image](image88)
![Image](image89)
![Image](image90)
![Image](image91)
![Image](image92)
![Image](image93)
![Image](image94)
![Image](image95)
![Image](image96)
![Image](image97)
![Image](image98)
![Image](image99)
![Image](image100)
![Image](image101)
![Image](image102)
![Image](image103)
![Image](image104)
![Image](image105)
![Image](image106)
![Image](image107)
![Image](image108)
![Image](image109)
![Image](image110)
![Image](image111)
![Image](image112)
![Image](image113)
![Image](image114)
![Image](image115)
![Image](image116)
![Image](image117)
![Image](image118)
![Image](image119)
![Image](image120)
![Image](image121)
![Image](image122)
![Image](image123)
![Image](image124)
![Image](image125)
![Image](image126)
![Image](image127)
![Image](image128)
![Image](image129)
![Image](image130)
![Image](image131)
![Image](image132)
![Image](image133)
![Image](image134)
![Image](image135)
![Image](image136)
![Image](image137)
![Image](image138)
![Image](image139)
![Image](image140)
![Image](image141)
![Image](image142)
![Image](image143)
![Image](image144)
![Image](image145)
![Image](image146)
![Image](image147)
![Image](image148)
![Image](image149)
![Image](image150)
![Image](image151)
![Image](image152)
![Image](image153)
![Image](image154)
![Image](image155)
![Image](image156)
![Image](image157)
![Image](image158)
![Image](image159)
![Image](image160)
![Image](image161)
![Image](image162)
![Image](image163)
![Image](image164)
![Image](image165)
![Image](image166)
![Image](image167)
![Image](image168)
![Image](image169)
![Image](image170)
![Image](image171)
![Image](image172)
![Image](image173)
![Image](image174)
![Image](image175)
![Image](image176)
![Image](image177)
![Image](image178)
![Image](image179)
![Image](image180)
![Image](image181)
![Image](image182)
![Image](image183)
![Image](image184)
![Image](image185)
![Image](image186)
![Image](image187)
![Image](image188)
![Image](image189)
![Image](image190)
![Image](image191)
![Image](image192)
![Image](image193)
![Image](image194)
![Image](image195)
![Image](image196)
![Image](image197)
![Image](image198)
![Image](image199)
![Image](image200)
![Image](image201)
![Image](image202)
![Image](image203)
![Image](image204)
![Image](image205)
![Image](image206)
![Image](image207)
![Image](image208)
![Image](image209)
![Image](image210)
![Image](image211)
![Image](image212)
![Image](image213)
![Image](image214)
![Image](image215)
![Image](image216)
![Image](image217)
![Image](image218)
![Image](image219)
![Image](image220)
![Image](image221)
![Image](image222)
![Image](image223)
![Image](image224)
![Image](image225)
![Image](image226)
![Image](image227)
![Image](image228)
![Image](image229)
![Image](image230)
![Image](image231)
![Image](image232)
![Image](image233)
![Image](image234)
![Image](image235)
![Image](image236)
![Image](image237)
![Image](image238)
![Image](image239)
![Image](image240)
![Image](image241)
![Image](image242)
![Image](image243)
![Image](image244)
![Image](image245)
![Image](image246)
![Image](image247)
![Image](image248)
![Image](image249)
![Image](image250)
![Image](image251)
![Image](image252)
![Image](image253)
![Image](image254)
![Image](image255)
![Image](image256)
![Image](image257)
![Image](image258)
![Image](image259)
![Image](image260)
![Image](image261)
![Image](image262)
![Image](image263)
![Image](image264)
![Image](image265)
![Image](image266)
![Image](image267)
![Image](image268)
![Image](image269)
![Image](image270)
![Image](image271)
![Image](image272)
![Image](image273)
![Image](image274)
![Image](image275)
![Image](image276)
![Image](image277)
![Image](image278)
![Image](image279)
![Image](image280)
![Image](image281)
![Image](image282)
![Image](image283)
![Image](image284)
![Image](image285)
![Image](image286)
![Image](image287)
![Image](image288)
![Image](image289)
![Image](image290)
![Image](image291)
![Image](image292)
![Image](image293)
![Image](image294)
![Image](image295)
![Image](image296)
![Image](image297)
![Image](image298)
![Image](image299)
![Image](image300)
![Image](image301)
![Image](image302)
![Image](image303)
![Image](image304)
![Image](image305)
![Image](image306)
![Image](image307)
![Image](image308)
![Image](image309)
![Image](image310)
![Image](image311)
![Image](image312)
![Image](image313)
![Image](image314)
![Image](image315)
![Image](image316)
![Image](image317)
![Image](image318)
![Image](image319)
![Image](image320)
![Image](image321)
![Image](image322)
![Image](image323)
![Image](image324)
![Image](image325)
![Image](image326)
![Image](image327)
![Image](image328)
![Image](image329)
![Image](image330)
![Image](image331)
![Image](image332)
![Image](image333)
![Image](image334)
![Image](image335)
![Image](image336)
![Image](image337)
![Image](image338)
![Image](image339)
![Image](image340)
![Image](image341)
![Image](image342)
![Image](image343)
![Image](image344)
![Image](image345)
![Image](image346)
![Image](image347)
![Image](image348)
![Image](image349)
![Image](image350)
![Image](image351)
![Image](image352)
![Image](image353)
![Image](image354)
![Image](image355)
![Image](image356)
![Image](image357)
![Image](image358)
![Image](image359)
![Image](image360)
![Image](image361)
![Image](image362)
![Image](image363)
![Image](image364)
![Image](image365)
![Image](image366)
![Image](image367)
![Image](image368)
![Image](image369)
![Image](image370)
![Image](image371)
![Image](image372)
![Image](image373)
![Image](image374)
![Image](image375)
![Image](image376)
![Image](image377)
![Image](image378)
![Image](image379)
![Image](image380)
![Image](image381)
![Image](image382)
![Image](image383)
![Image](image384)
![Image](image385)
![Image](image386)
![Image](image387)
![Image](image388)
![Image](image389)
![Image](image390)
![Image](image391)
![Image](image392)
![Image](image393)
![Image](image394)
![Image](image395)
![Image](image396)
![Image](image397)
![Image](image398)
![Image](image399)
![Image](image400)
![Image](image401)
![Image](image402)
![Image](image403)
![Image](image404)
![Image](image405)
![Image](image406)
![Image](image407)
![Image](image408)
![Image](image409)
![Image](image410)
![Image](image411)
![Image](image412)
![Image](image413)
![Image](image414)
![Image](image415)
![Image](image416)
![Image](image417)
![Image](image418)
![Image](image419)
![Image](image420)
![Image](image421)
![Image](image422)
![Image](image423)
![Image](image424)
![Image](image425)
![Image](image426)
![Image](image427)
![Image](image428)
![Image](image429)
![Image](image430)
![Image](image431)
![Image](image432)
![Image](image433)
![Image](image434)
![Image](image435)
![Image](image436)
![Image](image437)
![Image](image438)
![Image](image439)
![Image](image440)
![Image](image441)
![Image](image442)
![Image](image443)
![Image](image444)
![Image](image445)
![Image](image446)
![Image](image447)
![Image](image448)
![Image](image449)
![Image](image450)
![Image](image451)
![Image](image452)
![Image](image453)
![Image](image454)
![Image](image455)
![Image](image456)
![Image](image457)
![Image](image458)
![Image](image459)
![Image](image460)
![Image](image461)
![Image](image462)
![Image](image463)
![Image](image464)
![Image](image465)
![Image](image466)
![Image](image467)
![Image](image468)
![Image](image469)
![Image](image470)
![Image](image471)
![Image](image472)
![Image](image473)
![Image](image474)
![Image](image475)
![Image](image476)
![Image](image477)
![Image](image478)
![Image](image479)
![Image](image480)
![Image](image481)
![Image](image482)
![Image](image483)
![Image](image484)
![Image](image485)
![Image](image486)
![Image](image487)
![Image](image488)
![Image](image489)
![Image](image490)
![Image](image491)
![Image](image492)
![Image](image493)
![Image](image494)
![Image](image495)
![Image](image496)
![Image](image497)
![Image](image498)
![Image](image499)
![Image](image500)
![Image](image501)
![Image](image502)
![Image](image503)
![Image](image504)
![Image](image505)
![Image](image506)
![Image](image507)
![Image](image508)
![Image](image509)
![Image](image510)
![Image](image511)
![Image](image512)
![Image](image513)
![Image](image514)
![Image](image515)
![Image](image516)
![Image](image517)
![Image](image518)
![Image](image519)
![Image](image520)
![Image](image521)
![Image](image522)
![Image](image523)
![Image](image524)
![Image](image525)
![Image](image526)
![Image](image527)
![Image](image528)
![Image](image529)
![Image](image530)
![Image](image531)
![Image](image532)
![Image](image533)
![Image](image534)
![Image](image535)
![Image](image536)
![Image](image537)
![Image](image538)
![Image](image539)
![Image](image540)
![Image](image541)
![Image](image542)
![Image](image543)
![Image](image544)
![Image](image545)
![Image](image546)
![Image](image547)
![Image](image548)
![Image](image549)
![Image](image550)
![Image](image551)
![Image](image552)
![Image](image553)
![Image](image554)
![Image](image555)
![Image](image556)
![Image](image557)
![Image](image558)
![Image](image559)
![Image](image560)
![Image](image561)
![Image](image562)
![Image](image563)
![Image](image564)
![Image](image565)
![Image](image566)
![Image](image567)
![Image](image568)
![Image](image569)
![Image](image570)
![Image](image571)
![Image](image572)
![Image](image573)
![Image](image574)
![Image](image575)
![Image](image576)
![Image](image577)
![Image](image578)
![Image](image579)
![Image](image580)
![Image](image581)
![Image](image582)
![Image](image583)
![Image](image584)
![Image](image585)
![Image](image586)
![Image](image587)
![Image](image588)
![Image](image589)
![Image](image590)
![Image](image591)
![Image](image592)
![Image](image593)
![Image](image594)
![Image](image595)
![Image](image596)
![Image](image597)
![Image](image598)
![Image](image599)
![Image](image600)
![Image](image601)
![Image](image602)
![Image](image603)
![Image](image604)
![Image](image605)
![Image](image606)
![Image](image607)
![Image](image608)
![Image](image609)
![Image](image610)
![Image](image611)
![Image](image612)
![Image](image613)
![Image](image614)
![Image](image615)
![Image](image616)
![Image](image617)
![Image](image618)
![Image](image619)
![Image](image620)
![Image](image621)
![Image](image622)
![Image](image623)
![Image](image624)
![Image](image625)
![Image](image626)
![Image](image627)
![Image](image628)
![Image](image629)
![Image](image630)
![Image](image631)
![Image](image632)
![Image](image633)
![Image](image634)
![Image](image635)
![Image](image636)
![Image](image637)
![Image](image638)
![Image](image639)
![Image](image640)
![Image](image641)
![Image](image642)
![Image](image643)
![Image](image644)
![Image](image645)
![Image](image646)
![Image](image647)
![Image](image648)
![Image](image649)
![Image](image650)
![Image](image651)
![Image](image652)
![Image](image653)
![Image](image654)
![Image](image655)
![Image](image656)
![Image](image657)
![Image](image658)
![Image](image659)
![Image](image660)
![Image](image661)
![Image](image662)
![Image](image663)
![Image](image664)
![Image](image665)
![Image](image666)
![Image](image667)
![Image](image668)
![Image](image669)
![Image](image670)
![Image](image671)
![Image](image672)
![Image](image673)
![Image](image674)
![Image](image675)
![Image](image676)
![Image](image677)
![Image](image678)
![Image](image679)
![Image](image680)
![Image](image681)
![Image](image682)
![Image](image683)
![Image](image684)
![Image](image685)
![Image](image686)
![Image](image687)
![Image](image688)
![Image](image689)
![Image](image690)
![Image](image691)
![Image](image692)
![Image](image693)
![Image](image694)
![Image](image695)
![Image](image696)
![Image](image697)
![Image](image698)
![Image](image699)
![Image](image700)
![Image](image701)
![Image](image702)
![Image](image703)
![Image](image704)
![Image](image705)
![Image](image706)
![Image](image707)
![Image](image708)
![Image](image709)
![Image](image710)
![Image](image711)
![Image](image712)
![Image](image713)
![Image](image714)
![Image](image715)
![Image](image716)
![Image](image717)
![Image](image718)
![Image](image719)
![Image](image720)
![Image](image721)
![Image](image722)
![Image](image723)
![Image](image724)
![Image](image725)
![Image](image726)
![Image](image727)
![Image](image728)
![Image](image729)
![Image](image730)
![Image](image731)
![Image](image732)
![Image](image733)
![Image](image734)
![Image](image735)
![Image](image736)
![Image](image737)
![Image](image738)
![Image](image739)
![Image](image740)
![Image](image741)
![Image](image742)
![Image](image743)
![Image](image744)
![Image](image745)
![Image](image746)
![Image](image747)
![Image](image748)
![Image](image749)
![Image](image750)
![Image](image751)
![Image](image752)
![Image](image753)
![Image](image754)
![Image](image755)
![Image](image756)
![Image](image757)
![Image](image758)
![Image](image759)
![Image](image760)
![Image](image761)
![Image](image762)
![Image](image763)
![Image](image764)
![Image](image765)
![Image](image766)
![Image](image767)
![Image](image768)
![Image](image769)
![Image](image770)
![Image](image771)
![Image](image772)
![Image](image773)
![Image](image774)
![Image](image775)
![Image](image776)
![Image](image777)
![Image](image778)
![Image](image779)
![Image](image780)
![Image](image781)
![Image](image782)
![Image](image783)
![Image](image784)
![Image](image785)
![Image](image786)
![Image](image787)
![Image](image788)
![Image](image789)
![Image](image790)
![Image](image791)
![Image](image792)
![Image](image793)
![Image](image794)
![Image](image795)
![Image](image796)
![Image](image797)
![Image](image798)
![Image](image799)
![Image](image800)
![Image](image801)
![Image](image802)
![Image](image803)
![Image](image804)
![Image](image805)
![Image](image806)
![Image](image807)
![Image](image808)
![Image](image809)
![Image](image810)
![Image](image811)
![Image](image812)
![Image](image813)
![Image](image814)
![Image](image815)
![Image](image816)
![Image](image817)
![Image](image818)
![Image](image819)
![Image](image820)
![Image](image821)
![Image](image822)
![Image](image823)
![Image](image824)
![Image](image825)
![Image](image826)
![Image](image827)
![Image](image828)
![Image](image829)
![Image](image830)
![Image](image831)
![Image](image832)
![Image](image833)
![Image](image834)
![Image](image835)
![Image](image836)
![Image](image837)
![Image](image838)
![Image](image839)
![Image](image840)
![Image](image841)
![Image](image842)
![Image](image843)
![Image](image844)
![Image](image845)
![Image](image846)
![Image](image847)
![Image](image848)
![Image](image849)
![Image](image850)
![Image](image851)
![Image](image852)
![Image](image853)
![Image](image854)
![Image](image855)
![Image](image856)
![Image](image857)
![Image](image858)
![Image](image859)
![Image](image860)
![Image](image861)
![Image](image862)
![Image](image863)
![Image](image864)
![Image](image865)
![Image](image866)
![Image](image867)
![Image](image868)
![Image](image869)
![Image](image870)
![Image](image871)
![Image](image872)
![Image](image873)
![Image](image874)
![Image](image875)
![Image](image876)
![Image](image877)
![Image](image878)
![Image](image879)
![Image](image880)
![Image](image881)
![Image](image882)
![Image](image883)
![Image](image884)
![Image](image885)
![Image](image886)
![Image](image887)
![Image](image888)
![Image](image889)
![Image](image890)
![Image](image891)
![Image](image892)
![Image](image893)
![Image](image894)
![Image](image895)
![Image](image896)
![Image](image897)
![Image](image898)
![Image](image899)
![Image](image900)
![Image](image901)
![Image](image902)
![Image](image903)
![Image](image904)
![Image](image905)
![Image](image906)
![Image](image907)
![Image](image908)
![Image](image909)
![Image](image910)
![Image](image911)
![Image](image912)
![Image](image913)
![Image](image914)
![Image](image915)
![Image](image916)
![Image](image917)
![Image](image918)
![Image](image919)
![Image](image920)
![Image](image921)
![Image](image922)
![Image](image923)
![Image](image924)
![Image](image925)
![Image](image926)
![Image](image927)
![Image](image928)
![Image](image929)
![Image](image930)
![Image](image931)
![Image](image932)
![Image](image933)
![Image](image934)
![Image](image935)
![Image](image936)
![Image](image937)
![Image](image938)
![Image](image939)
![Image](image940)
![Image](image941)
![Image](image942)
![Image](image943)
![Image](image944)
![Image](image945)
![Image](image946)
![Image](image947)
![Image](image948)
![Image](image949)
![Image](image950)
![Image](image951)
![Image](image952)
![Image](image953)
![Image](image954)
![Image](image955)
![Image](image956)
![Image](image957)
![Image](image958)
![Image](image959)
![Image](image960)
![Image](image961)
![Image](image962)
![Image](image963)
![Image](image964)
![Image](image965)
![Image](image966)
![Image](image967)
![Image](image968)
![Image](image969)
![Image](image970)
![Image](image971)
![Image](image972)
![Image](image973)
![Image](image974)
![Image](image975)
![Image](image976)
![Image](image977)
![Image](image978)
![Image](image979)
![Image](image980)
![Image](image981)
![Image](image982)
![Image](image983)
![Image](image984)
![Image](image985)
![Image](image986)
![Image](image987)
![Image](image988)
![Image](image989)
![Image](image990)
![Image](image991)
![Image](image992)
![Image](image993)
![Image](image994)
![Image](image995)
![Image](image996)
![Image](image997)
![Image](image998)
![Image](image999)
![Image](image1000)



![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]

![Image]
