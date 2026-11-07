

![](img/b217c421655b51e7494cf3b89bb5432d_700_0.png)

## 第10章

## 类与数据抽象

**本章你将：**

1. 了解类
2. 了解类的私有、保护和公有成员
3. 探索类是如何实现的
4. 认识访问器函数和修改器函数
5. 考查构造函数和析构函数
6. 了解抽象数据类型（ADT）
7. 探索如何使用类实现 ADT
8. 认识结构体和类之间的区别
9. 了解信息隐藏
10. 探索信息隐藏在 C++ 中如何实现
11. 认识类的内联函数
12. 了解类的静态成员

在第 9 章中，你学习了如何使用 `struct` 对不同类型的数​​据项进行分组。第 9 章给出的 `struct` 定义类似于 C 结构体的定义。然而，C++ `struct` 的成员既可以是数据项，也可以是函数。C++ 提供了另一种结构化数据类型，称为 `class`，它专门用于对数据和函数进行分组。本章首先介绍类并说明如何使用它们，然后讨论 `struct` 和 `class` 之间的异同。

> **注意**
> 第 9 章不是本章的先修内容。事实上，`struct` 和 `class` 具有相似的能力，本章“`struct` 与 `class`”一节对此进行了讨论。

### 类

第 1 章介绍了一种称为**面向对象设计（OOD）**的问题求解方法。在 OOD 中，第一步是识别组件，这些组件称为**对象**。对象将数据和作用于这些数据的操作组合成一个单元。在 C++ 中，允许你将数据和作用于这些数据的操作组合成一个单元的机制称为类。现在你已经知道如何在计算机内存中存储和操作数据，以及如何构造自己的函数，因此可以学习对象是如何构造的。本章及后续章节将使用 OOD 开发和实现程序。本章首先解释如何定义类并在程序中使用它。

**类**是固定数量组件的集合。类的组件称为类的**成员**。

定义类的一般语法是：

```cpp
class classIdentifier
{
    classMembersList
};
```

其中 **classMembersList** 由变量声明和/或函数组成。也就是说，类的成员可以是变量（用于存储数据）或函数（用于操作数据）。

例如，以下语句定义了 `class` `courseType`，其中包含变量和函数，用于实现课程的基本属性。

```cpp
class courseType
{
public:
    void setCourseInfo(string cName, string cNo, int credits);
    void print() const;
    int getCredits();
    string getCourseNumber();
    string getCourseName();

private:
    string courseName;
    string courseNo;
    int courseCredits;
};
```

请注意以下几点：

- 如果类的成员是变量，就像声明任何其他变量一样声明它。另外，在 C++11 之前的 C++ 版本中，在类的定义中，不能在声明变量时初始化它。
- 如果类的成员是函数，通常使用函数原型来声明该成员。
- 如果类的成员是函数，它可以（直接）访问该类的任何成员——成员变量和成员函数。也就是说，当你编写成员函数的定义时，可以直接访问该类的任何成员变量，而不需要将其作为参数传递。唯一条件是必须先声明标识符才能使用它。

在 C++ 中，class 是保留字，并且它只定义一种数据类型；不分配内存。它宣告一个类的声明。此外，注意右花括号后的分号（;）。分号是语法的一部分。因此，缺少分号将导致语法错误。

类的成员分为三类：private、public 和 protected。本章主要讨论前两种类型：private 和 public。

在 C++ 中，private、protected 和 public 是保留字，称为**成员访问说明符**。

以下是关于类的 public 和 private 成员的一些事实：

- 默认情况下，类的所有成员都是 private。
- 如果类的成员是 private，则不能从类外部直接访问它。（示例 10-1 说明了这一概念。）
- public 成员可在类外部访问。（示例 10-1 说明了这一概念。）
- 要使类的成员成为 public，使用成员访问说明符 public 加冒号 :。

假设我们想定义一个类，在程序中实现一天中的时间。因为时钟给出一天中的时间，我们把这个类称为 **clockType**。此外，为了在计算机内存中表示时间，我们使用三个 **int** 变量：一个表示小时，一个表示分钟，一个表示秒。

假设这三个变量是：

```cpp
int hr;
int min;
int sec;
```

我们还希望对时间执行以下操作：

1. 设置时间。
2. 获取时间。
3. 打印时间。
4. 将时间增加一秒。
5. 将时间增加一分钟。
6. 将时间增加一小时。
7. 比较两个时间是否相等。

为了实现这七个操作，我们将编写七个函数——setTime、getTime、printTime、incrementSeconds、incrementMinutes、incrementHours 和 equalTime。

从上述讨论可以清楚地看出，类 clockType 有 10 个成员：三个成员变量和七个成员函数。

类 clockType 的一些成员将是 private；另一些将是 public。决定哪个成员设为 public、哪个设为 private 取决于成员的性质。一般规则是，任何需要在类外部直接访问的成员都声明为 public；任何不应由用户直接访问的成员都应声明为 private。例如，用户应能够设置时间和打印时间。因此，设置时间和打印时间的成员应声明为 public。

类似地，用于增加时间和比较时间是否相等的成员应声明为 public。另一方面，为了防止直接操作成员变量 hr、min 和 sec，我们将它们声明为 private。此外，请注意，如果用户可以直接访问成员变量，则不需要 setTime 之类的成员函数。本章第二部分（从“信息隐藏”一节开始）解释了为什么一些成员需要是 public，而另一些成员应是 private。

以下语句定义了类 clockType：

```cpp
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

private:
    int hr;
    int min;
    int sec;
};
```

在此定义中：

- 类 `clockType` 有七个成员函数：`setTime`、`getTime`、`printTime`、`incrementSeconds`、`incrementMinutes`、`incrementHours` 和 `equalTime`。它有三个成员变量：`hr`、`min` 和 `sec`。
- 三个成员变量——`hr`、`min` 和 `sec`——是类的 `private` 成员，不能在类外部访问。（示例 10-1 说明了这一概念。）
- 七个成员函数——`setTime`、`getTime`、`printTime`、`incrementSeconds`、`incrementMinutes`、`incrementHours` 和 `equalTime`——是 `public` 成员，可以在类外部直接访问。它们也可以直接访问成员变量（`hr`、`min` 和 `sec`）。换句话说，当我们编写这些函数的定义时，不把这些成员变量作为参数传递给成员函数。
- 在函数 `equalTime` 中，形参是常量引用参数。也就是说，在调用函数 `equalTime` 时，形参接收实参的地址，但形参不能修改实参的值。你本可以把形参声明为值参数，但那样会要求形参复制实参的值，可能导致性能不佳。（解释见本章“引用参数和类对象（变量）”一节。）
- 成员函数 `getTime`、`printTime` 和 `equalTime` 末尾的 `const` 一词规定，这些函数不能修改 `clockType` 类型变量的成员变量。

> **注意**
> `private` 和 `public` 成员可以按任意顺序出现。如果愿意，你可以先声明 `private` 成员，再声明 `public` 成员。本章“类的 public 和 private 成员的顺序”一节讨论了这一问题。

> **注意**
> 在类 `clockType` 的定义中，所有成员变量都是 `private`，所有成员函数都是 `public`。然而，成员函数也可以是 `private`。例如，如果一个成员函数只用于实现该类的其他成员函数，而用户不需要访问这个函数，就把它设为 `private`。类似地，类的成员变量也可以是 `public`。

注意，我们还没有编写该类成员函数的定义。你很快就会学习如何编写它们。

