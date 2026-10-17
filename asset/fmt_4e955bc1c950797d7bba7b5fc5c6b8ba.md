
# 创建友元函数

友元函数可以访问其为友元的类的任何成员。你通过在类定义内部列出以关键字 `friend` 开头的函数原型来指定一个函数是类的友元。这就是我在 `Critter` 定义内部所做的，使用以下行表示全局函数 `Peek()` 是 `Critter` 的友元。

```cpp
friend void Peek(const Critter& aCritter);
```

这意味着 `Peek()` 可以访问 `Critter` 的任何成员，即使它不是该类的成员函数。`Peek()` 利用这种关系，通过访问私有数据成员 `m_Name` 来显示传递给该函数的 critter 的名称。

```cpp
void Peek(const Critter& aCritter)
{
    cout << aCritter.m_Name << endl;
}
```

当我在 `main()` 中使用以下行调用 `Peek()` 时，`crit` 的私有数据成员 `m_Name` 被显示，`Poochie` 出现在屏幕上。

```cpp
Peek(crit);
```

# 重载运算符

重载运算符听起来可能像是你想不惜一切代价避免的事情——就像“小心，那个运算符被重载了，她就要爆炸了！”——但事实并非如此。运算符重载让你可以为使用你定义的新类型时使用的内置运算符赋予意义。例如，你可以重载 `*` 运算符，以便当它与两个 3D 矩阵（从你定义的某个类实例化的对象）一起使用时，结果是矩阵的乘法。

要重载运算符，请定义一个名为 `operatorX` 的函数，其中 `X` 是你想要重载的运算符。这就是我在重载 `<<` 运算符时所做的；我定义了一个名为 `operator<<` 的函数。

```cpp
ostream& operator<<(ostream& os, const Critter& aCritter)
{
    os << "Critter Object - ";
    os << "m_Name: " << aCritter.m_Name;
    return os;
}
```

该函数重载了 `<<` 运算符，因此当我使用 `<<` 将 `Critter` 对象发送到 `cout` 时，数据成员 `m_Name` 会被显示出来。本质上，这个函数让我能够轻松地显示 `Critter` 对象。该函数可以直接访问 `Critter` 对象的私有数据成员 `m_Name`，因为我在 `Critter` 中通过以下代码行将该函数设为 `Critter` 类的友元：

```cpp
friend ostream& operator<<(ostream& os, const Critter& aCritter);
```

这意味着我只需使用 `<<` 运算符将 `Critter` 对象发送到 `cout`，就能轻松显示它，这正是我在 `main()` 中通过以下代码行所做的，这行代码会显示文本 “Critter Object - m_Name: Poochie”。

```cpp
cout << crit;
```

## 提示

> 对于游戏程序员来说，尽管有各种工具和调试选项可用，但有时候，简单地显示变量的值才是理解程序中正在发生什么的最佳方式。重载 `<<` 运算符能帮助你做到这一点。

这个函数之所以有效，是因为 `cout` 是 `ostream` 类型的对象，而 `ostream` 已经重载了 `<<` 运算符，因此你可以将内置类型发送到 `cout`。

# 动态分配内存

到目前为止，每当你声明一个变量时，C++ 都会为其分配必要的内存。当创建该变量的函数结束时，C++ 会释放这块内存。这种用于局部变量的内存被称为栈。但还有另一种内存，它独立于程序中的函数而存在。你，作为程序员，负责分配和释放这块内存，这类内存统称为堆（或自由存储区）。

在这一点上，你可能会想：“为什么要费心用另一种类型的内存？栈就挺好的，谢谢。”使用堆的动态内存能带来巨大的好处，可以用一个词概括：效率。通过使用堆，你可以在任何给定时间只使用所需的内存量。如果你有一个关卡有 100 个敌人的游戏，你可以在关卡开始时为敌人分配内存，并在关卡结束时释放内存。堆还允许你在一个函数中创建一个对象，即使该函数结束后你仍能访问它（而不必返回对象的副本）。你可能在一个函数中创建一个屏幕对象并返回对其的访问权。你会发现，动态内存在编写任何大型游戏时都是一个重要的工具。

# 介绍堆程序

堆程序演示了动态内存。该程序在堆上为一个整数变量动态分配内存，为其赋值，然后显示它。接下来，程序调用一个函数，该函数在堆上为另一个整数变量动态分配内存，为其赋值，并返回一个指向它的指针。程序获取返回的指针，用它来显示值，然后释放堆上分配的内存。最后，程序包含两个演示滥用动态内存的函数。我不会调用这些函数，但我用它们来说明使用动态内存时不应该做什么。图 9.3 展示了该程序。

![](img/34f09be0ed6217c465debc4490197d4f_319_0.png)

图 9.3
这两个 `int` 值存储在堆上。

你可以从 Course Technology 网站（www.coursetech.com/downloads）下载此程序的代码。该程序位于第 9 章的文件夹中；文件名为 `heap.cpp`。

```cpp
// Heap
// Demonstrates dynamically allocating memory

#include <iostream>

using namespace std;

int* intOnHeap();  //returns an int on the heap

void leak1();  //creates a memory leak

void leak2();  //creates another memory leak

int main()
{
    int* pHeap = new int;
    *pHeap = 10;
    cout << "*pHeap: " << *pHeap << "\n\n";

    int* pHeap2 = intOnHeap();
    cout << "*pHeap2: " << *pHeap2 << "\n\n";

    cout << "Freeing memory pointed to by pHeap.\n\n";
    delete pHeap;
    cout << "Freeing memory pointed to by pHeap2.\n\n";
    delete pHeap2;

    //get rid of dangling pointers
    pHeap = 0;
    pHeap2 = 0;

    return 0;
}

int* intOnHeap()
{
    int* pTemp = new int(20);
    return pTemp;
}

void leak1()
{
    int* drip1 = new int(30);
}

void leak2()
{
    int* drip2 = new int(50);
    drip2 = new int(100);
    delete drip2;
}
```

# 使用 new 运算符

`new` 运算符在堆上分配内存并返回其地址。你使用 `new`，后面跟上你想要为其保留空间的值的类型。这就是我在 `main()` 的第一行所做的。

```cpp
int* pHeap = new int;
```

语句中的 `new int` 部分在堆上为一个 `int` 分配足够的内存，并返回该块内存在堆上的地址。语句的另一部分，`int* pHeap`，声明了一个局部指针 `pHeap`，它指向堆上新分配的内存块。

通过使用 `pHeap`，我可以操作堆上为整数保留的内存块。这就是我接下来要做的；我向该内存块赋值为 10，然后使用 `pHeap` 显示存储在堆上的该值，就像我使用任何其他指向 `int` 的指针一样。唯一的区别是 `pHeap` 指向堆上的内存块，而不是栈。

## 提示

你可以在分配堆内存的同时对其进行初始化，方法是在类型后面放置一个用括号包围的值。这比听起来更容易。例如，下面这行代码在堆上为一个 `int` 变量分配一块内存并将其赋值为 10。然后该语句将该块内存的地址分配给 `pHeap`。

```cpp
int* pHeap = new int(10);
```

堆内存的一个主要优势是，它可以比在哪个函数中分配的时间更长，意味着你可以在一个函数中创建堆上的对象，并返回指向它的指针或引用。这就是我用下面这行代码演示的：

```cpp
int* pHeap2 = intOnHeap();
```

该语句调用函数 `intOnHeap()`，该函数在堆上为 `int` 分配一块内存并为其赋值为 20。

```cpp
int* intOnHeap()
{
    int* pTemp = new int(20);
    return pTemp;
}
```

然后，该函数返回指向这块内存的指针。回到 `main()` 中，赋值语句将堆上这块内存的地址赋给 `pHeap2`。接下来，我使用返回的指针显示该值。

```cpp
cout << "*pHeap2: " << *pHeap2 << "\n\n";
```

## 提示

到目前为止，如果你想返回在函数中创建的值，你必须返回该值的副本。但是通过使用动态内存，你可以在函数中创建堆上的对象，并返回指向新对象的指针。

# 使用 delete 运算符

与栈上局部变量的存储不同，你在堆上分配的内存必须显式释放。当你用完使用 `new` 分配的内存时，应该用 `delete` 释放它。这就是我用下面这行代码所做的，它释放了堆上存储 10 的那块内存。

```cpp
delete pHeap;
```

该内存被返回给堆以供将来使用。其中存储的数据不再可用。接下来，我释放更多内存，释放堆上存储 20 的那块内存。

```cpp
delete pHeap2;
```

该内存被返回给堆以供将来使用，其中存储的数据不再可用。请注意，就 `delete` 而言，我在程序中分配要删除的堆内存的位置没有区别。

## 技巧

因为你需要在用完分配的内存后释放它，一个好的经验法则是每个 `new` 都应该有一个对应的 `delete`。事实上，一些程序员尽可能在写完 `new` 语句后立即写 `delete` 语句，以免忘记。

这里要理解的一个重要点是，前面两条语句释放了堆上的内存，但它们并不直接影响局部变量 `pHeap` 和 `pHeap2`。这会产生一个潜在问题，因为 `pHeap` 和 `pHeap2` 现在指向已返还给堆的内存，这意味着它们指向计算机在任何时候都可能以其他方式使用的内存。像这样的指针被称为悬空指针，它们相当危险。你绝不应该尝试解引用悬空指针。处理悬空指针的一种方法是将 0 分配给它们，这就是我用下面几行代码所做的，这两行代码重新赋值这两个悬空指针，使它们不再指向它们不应该指向的某些内存。

```cpp
pHeap = 0;
pHeap2 = 0;
```

处理悬空指针的另一种好方法是为它分配一个有效的内存地址。

## 陷阱

> 对悬空指针使用 `delete` 可能会导致程序崩溃。一定要将悬空指针设置为 0，或者重新分配它，使其指向新的、有效的内存块。

# 避免内存泄漏

允许程序员分配和释放内存的一个问题是，他可能会分配内存后失去访问它的任何途径，从而永远无法释放它。当内存像这样丢失时，就称为内存泄漏。如果泄漏足够大，程序可能会耗尽内存并崩溃。作为游戏程序员，避免内存泄漏是你的责任。

我在堆程序中编写了两个故意造成内存泄漏的函数，以向你展示在使用动态内存时不应该做什么。第一个函数是 `leak1()`，它只是在堆上为一个 `int` 值分配一块内存，然后结束。

```cpp
void leak1()
{
    int* drip1 = new int(30);
}
```

如果我调用这个函数，内存将永远丢失。（好吧，它会在程序结束前一直丢失。）问题在于 `drip1`，它是堆上新获取的内存块的唯一连接，是一个局部变量，并在函数 `leak1()` 结束时不复存在。因此，没有办法释放分配的内存。请查看图 9.4，了解泄漏发生的视觉表示。

![](img/34f09be0ed6217c465debc4490197d4f_324_0.png)

**Figure 9.4** The memory that stores 30 can no longer be accessed to be freed, so it has leaked out of the system.

为避免此内存泄漏，我可以做两件事中的一件。我可以在 `leak1()` 中使用 `delete` 来释放内存，或者我可以返回指针 `drip1` 的副本。如果我选择第二个选项，我必须确保在程序的其他部分释放此内存。

创建内存泄漏的第二个函数是 `leak2()`。

```cpp
void leak2()
{
    int* drip2 = new int(50);
    drip2 = new int(100);
    delete drip2;
}
```
