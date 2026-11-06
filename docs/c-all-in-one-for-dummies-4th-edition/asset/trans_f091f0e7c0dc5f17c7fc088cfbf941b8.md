
一根连接到电池的导线。大多数情况下，内部的东西是不允许随意触碰的，除非你正在升级它。

在面向对象术语中，*公有*（public）和*私有*（private）这两个词指的是属性和方法。设计类时，你可能希望让某些属性和方法可供类用户自由访问。你可能希望把其他成员隐藏起来。类用户是应用程序中创建类实例并调用其某个方法的部分。在本章前面的清单 1-2 中，`main()` 就是一个类用户。如果你有一个名为 `FlippyFlop()` 的函数，它创建你的类的一个实例并对该实例做一些事情，例如更改它的某些属性，那么 `FlippyFlop()` 就是类用户。简而言之，用户就是任何访问你的类的函数。

设计类时，你可能只希望特定用户调用某些方法。你可能希望把其他方法隐藏起来，只由类内部的其他方法调用。假设你正在编写一个名为 `Oven` 的类。这个类包含一个名为 `Bake()` 的方法，它接受一个数字作为参数，表示所需的烤箱温度。现在你可能还有一个名为 `TurnOnHeatingElement()` 的方法和一个名为 `TurnOffHeatingElement()` 的方法。

它的工作方式如下。`Bake()` 方法一开始调用 `TurnOnHeatingElement()`。然后它持续跟踪温度，当温度合适时，调用 `TurnOffHeatingElement()`。你不会希望有人走进厨房，什么旋钮都不碰就调用 `TurnOnHeatingElement()` 方法，然后离开房间，任由烤箱在无人看管下越来越热。你只允许类的用户调用 `Bake()`。另外两个方法 `TurnOnHeatingElement()` 和 `TurnOffHeatingElement()` 保留为仅供 `Bake()` 函数使用。

![](img/128ab511de4e7360e167e3b15cdd5dd0_261_0.png)

你通过把特定函数设为*私有*，来阻止用户调用这些函数。你希望允许访问的函数，就把它设为*公有*。设计好类之后，如果你编写一个函数，基于该类实例化一个对象，并试图调用该对象的某个*私有*方法，那么编译时就会遇到编译器错误。编译器不允许你调用它。

清单 1-15 所示的 `Oven` 类示例定义了一个示例 `Oven` 类以及使用它的 `main()`。看一下类定义。它有两个部分：一个是*私有*，另一个是*公有*。函数的代码出现在类定义之后。这两个*私有*函数除了打印一条消息之外没有做太多事情。（不过它们也可以自由调用类中的其他*私有*函数。）*公有*函数 `Bake()` 调用每个*私有*函数，因为它被允许这样做。

### 清单 1-15：使用 public 和 private 关键字隐藏类的部分内容

```cpp
#include <iostream>

using namespace std;

class Oven {
private:
  void TurnOnHeatingElement();
  void TurnOffHeatingElement();
public:
  void Bake(int Temperature);
};

void Oven::TurnOnHeatingElement() {
  cout << "Heating element is now ON! Be careful!" << endl;
}

void Oven::TurnOffHeatingElement() {
  cout << "Heating element is now off. Relax!" << endl;
}

void Oven::Bake(int Temperature) {
  TurnOnHeatingElement();
  cout << "Baking!" << endl;
  TurnOffHeatingElement();
}

int main() {
  Oven fred;
  fred.Bake(875);
  return 0;
}
```

运行此应用程序时，你会看到一些消息：

```text
Heating element is now ON! Be careful!
Baking!
Heating element is now off. Relax!
```

这里没有什么特别复杂的东西。现在，如果你尝试在 `main()` 中加入下面代码中的一行，调用一个私有函数：

```cpp
fred.TurnOnHeatingElement();
```

你会看到一条错误消息，告诉你不能这样做，因为该函数是私有的。在 Code::Blocks 中，你会看到以下消息：

```text
error: 'void Oven::TurnOnHeatingElement()' is private
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_263_0.png)

设计类时，考虑默认把所有函数设为私有，然后只把你希望用户访问的那些函数设为公有。然而，有些人更喜欢反过来：把它们全部设为公有，然后只把你确定不希望用户访问的那些设为私有。两种方法都有充分的理由；不过，本书倾向于只把必须公有的内容设为公有。这种方法可以最大限度地降低风险：使用该类的其他操作因调用程序员并不真正理解的内容而出错。

![](img/128ab511de4e7360e167e3b15cdd5dd0_263_1.png)

你不一定需要先列出私有成员，再列出公有成员。如果你愿意，也可以先列出公有成员。有些人把公有成员放在顶部，这样他们能先看到它们。这很合理。另外，你可以有多个私有部分和多个公有部分。例如，你可以先有一个公有部分、一个私有部分，然后再有一个公有部分，如下面的代码所示：

```cpp
class Oven {
public:
    void Bake(int Temperature);
private:
    void TurnOnHeatingElement();
    void TurnOffHeatingElement();
public:
    void Broil();
};
```

## 使用类和原始指针

本节以及本章其他小节讨论原始指针与对象的使用。在本书第 1 册第 8 章的“理解 C++ 20 中指针的变化”一节中，你会了解到还有其他指针类型，包括智能指针和可选指针。由于大多数代码仍然依赖原始指针来处理对象，本章大部分内容聚焦于它们的使用。

与任何变量一样，你可以有一个指向对象的指针变量。和通常一样，指针变量的类型必须与类的类型匹配。下面的代码创建了一个指向 `Pen` 实例的指针变量：

```cpp
Pen *MyPen;
```

变量 MyPen 是一个指针，它可以指向 `Pen` 类型的对象。变量本身的类型是“指向 `Pen` 的指针”，用 C++ 记法就是 `Pen *`。由于与对象交互时你总是在使用指针，所以变量名中省略了 `ptr`，以节省打字时间，并把注意力集中在变量的用途上——它充当你的个人钢笔。

![](img/128ab511de4e7360e167e3b15cdd5dd0_264_0.png)

像 `Pen *MyPen;` 这样的一行代码会创建一个变量，它充当指向对象的指针。但这一行本身实际上并不会创建实例。它本身不指向任何东西。要创建实例，必须调用 `new`。这是 C++ 程序员常犯的错误；有时人们忘记调用 `new`，然后纳闷为什么应用程序会崩溃。

创建变量 MyPen 之后，你可以创建 `Pen` 类的实例，并使用 `new` 关键字让 MyPen 指向它，如下所示：

```cpp
MyPen = new Pen;
```

或者你可以把 `Pen *MyPen;` 和前面那一行合并起来：

```cpp
Pen *MyPen = new Pen;
```

现在你有两个变量：一个是实际对象，它没有名字，位于堆上。（有关指针和堆的更多信息，请参见本书第 1 册第 8 章的“变量在堆和栈上的分配”一节。）另一个是指针变量，它指向该对象：两个变量协同工作。由于对象位于堆上，访问它的唯一方式就是通过指针。要通过指针访问成员，需要使用一种特殊记法——一个减号后跟一个大于号。它看起来有点像箭头（因此被称为箭头运算符），下面这行代码清楚地说明了这一点：

```cpp
MyPen->InkColor = red;
```

这行代码通过 MyPen 指针把对象的 InkColor 属性设置为 red。

与使用 `new` 创建的其他变量一样，使用完对象后，你应该调用 `delete` 来释放 MyPen 所指向对象占用的内存。为此，先写 `delete`，再写对象指针的名称 MyPen，如下所示：

```cpp
delete MyPen;
```
