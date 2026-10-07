
```cpp
process(123);
process(2.2);
process(string("*Test"));
```

该示例的输出如下：

```
123 is an integral type.
2.2 is a non-integral type.
Test is a non-integral type.
```

上一个示例可以使用仅 `process()` 函数模板来编写，但那样并没有演示如何编写其中一个参数为 `true_type` 或 `false_type` 的不同重载。

```cpp
template<typename T>
void process(const T& t)
{
    if (is_integral<T>::value) {
        cout << t << " is an integral type." << endl;
    } else {
        cout << t << " is a non-integral type." << endl;
    }
}
```

## 使用类型关系

有三种类型关系可用：`is_same`、`is_base_of` 和 `is_convertible`。本节提供了如何使用 `is_same` 的示例；其他的用法原理类似。

下面的 `same()` 函数模板使用 `is_same` 类型特质来确定两个参数是否为相同类型，并输出适当的消息。在 `main()` 函数中使用 `same()` 函数模板非常简单：

```cpp
template<typename T1, typename T2>
void same(const T1& t1, const T2& t2)
{
    bool areTypesTheSame = is_same<T1, T2>::value;
    cout << " " << t1 << " and " << t2 << " = " << areTypesTheSame;
    cout << (areTypesTheSame ? "the same types." : "different types.") << endl;
}

int main()
{
    same(1, 32);
    same(1, 3.01);
    same(3.01, string("Test"));
}
```

输出如下：

- '1' and '32' are the same types.

- '1' and '3.01' are different types

- '3.01' and 'Test' are different types

## 使用 enable_if

在使用 `enable_if` 之前先进行介绍。使用 `enable_if` 需要了解一种“替换失败不是错误”（Substitution Failure Is Not Error, SFINAE），这是 C++ 的一个晦涩特性。本节将通过 `enable_if` 示例解释 SFINAE 的基础。

如果你有一组重载函数，可以使用 `enable_if` 根据类型特质选择性地禁用某些重载。`enable_if` 通常用于重载的返回值。`enable_if` 接受两个模板参数。第一个是布尔值，第二个是默认为 `void` 的类型。如果布值为真，则 `enable_if` 有一个可以通过 `::type` 访问的嵌套类型。该嵌套类型的类型就是第二个模板参数提供的类型。如果布尔值为假，则没有嵌套类型。

上一节中 `same()` 函数模板的示例可以使用 `enable_if` 改写为重载的 `check_type()` 函数模板如下。在这个版本中，`check_type()` 根据给定的类型是否相同返回真或假。如果你不想让 `check_type()` 返回任何内容，可以移除 `enable_if` 的第二个模板参数，或将其替换为 `void`。

```cpp
template<typename T1, typename T2>
typename enable_if<is_same<T1, T2>::value, bool>::type
check_type(const T1& t1, const T2& t2)
{
    cout << " " << t1 << " and " << t2 << " = ";
    cout << "are the same types." << endl;
    return true;
}
```

# 22

# 内存管理

本章内容概览

- 使用和管理内存的不同方式

- 数组与指针之间错综复杂的关系

- 内存操作的低级视角

- 智能指针及其使用方法

- 若干内存相关问题的解决方案

WROX.COM 本章下载资源

请注意，本章的所有代码示例均作为该章节代码下载的一部分，可以在书籍网站 `www.wrox.com/go/proc++3e` 的“Download（下载）”选项卡中获取。

（此处为正文翻译）

在许多方面，在 C++ 中进行编程就像在没有道路的情况下开车。当然，你可以去任何你想去的地方，但没有标线或交通灯来引导你免于受伤。C++ 就像 C 语言一样，对程序员采取了“放任不管”的方法。该语言假设你清楚自己在做什么。它允许你进行一些可能会导致问题的操作，因为 C++ 极其灵活，并且为了性能牺牲了安全性。

内存分配是 C++ 编程中一个特别容易出错的领域。为了编写高质量的 C++ 程序，专业的 C++ 程序员需要理解内存背后的工作机制。本章将探索内存管理的方方面。你将学习动态内存的陷阱，以及避免和消除这些陷阱的技术。

本章位于书籍的后期，是因为在现代 C++ 中，你应该尽可能地避免低级内存操作。例如，与其使用动态分配的 C 风格数组，你应该使用 STL 容器（如 `vector`），它们会自动处理所有的内存管理。与其使用指针，你应该使用智能指针（如 `unique_ptr` 和 `shared_ptr`），它们在内存不再需要时会自动释放底层资源（如内存）。基本上，你应该尝试避免在代码中出现诸如 `new` 和 `delete` 的内存分配例程。当然，这可能并非可行，而且在现有的代码中很可能并非如此，因为专业的 C++ 程序员仍然需要知道内存背后的工作机制。

> 警告 在现代 C++ 中，你应该尽可能地避免低级内存操作，转而使用容器和智能指针等现代构造结构。

# 操作动态内存

内存是计算机的一个低级组件，不幸的是，即使在像 C++ 这样的高级编程语言中，它有时也会现身。许多程序员只了解动态内存以付付。他们逃避使用动态内存的数据结构，或者通过试错来让程序运行。深入理解 C++ 中动态内存到底是如何运作的，对于成为一名专业的 C++ 程序员至关重要。

## 如何构想内存

如果你对对象在内存中长什么样有一个心理模型，那么理解动态内存就会容易得多。在本书中，一个内存单元被显示为一个带有标签的盒子。标签指示了与该内存对应的变量名。盒子内部的数据显示了内存的当前值。

例如，图 22-1 显示了执行以下行后的内存状态。该行代码应该位于一个函数中，这样 `i` 就是一个局部变量：

```cpp
int i = 7;
```

![](img/5dda262a2e4cfd8040434fe81f2b4e78_755_0.png)

图 22-1

当你使用 `new` 关键字时，内存会被分配在堆（heap）上。以下代码在栈上创建一个变量 `ptr`，然后在堆上分配了供 `ptr` 指向的内存。

```cpp
int* ptr;
ptr = new int;
```

图 22-2 显示了执行此代码后的内存状态。注意，即使变量 `ptr` 指向堆，它仍然在栈上。指针只是一个变量，可以存在于栈上也可以存在于堆上，尽管这一事实很容易被忘记。然而，动态内存总是分配在堆上的。

![](img/5dda262a2e4cfd8040434fe81f2b4e78_756_0.png)

图 22-2

下一个示例显示了指针可以同时存在于栈和堆上：

```cpp
int** handle;
handle = new int*;
*handle = new int;
```

前述代码首先声明了一个指向整数的指针作为变量 `handle`。然后，它动态分配了足够的内存来存放一个指向整数的指针，并将该新内存的指针存储在 `handle` 中。接下来，内存（`*handle`）被赋予指向另一个动态内存区域的指针，该区域足够大容纳该整数。22-3 显示了两个级的指针，其中一个指针位于栈上（`handle`），另一个位于堆上（`*handle`）。

![](img/5dda262a2e4cfd8040434fe81f2b4e78_756_1.png)

图 22-3

## 分配与释放

为了为变量创建空间，你使用 `new` 关键字。为了释放空间供程序的其他部分使用，你使用 `delete` 关键字。当然，如果 `new` 和 `delete` 这些简单概念没有几种变体和复杂之处，那它就不是 C++ 了。

### 使用 new 和 delete 分配内存块

当你带有你所需的空间变量类型调用 `new` 时，`new` 会返回一个指向该内存的指针，尽管将该指针存储在变量中取决于你。如果你忽略了 `*new` 的返回值，或者指针变量离开了作用范围，该内存将变成*孤立的*（orphaned），因为你不再有办法访问它。这也被称为*内存泄漏*（memory leak）。

例如，以下代码孤立了足够存放一个 `int` 的内存。

```cpp
void leaky() {
    new int; // 内存泄漏
}

int main() {
    int* p = new int;
    // p 离开作用域，内存变为孤立
    return 0;
}
```

![](img/5dda262a2e4cfd8040434fe81f2b4e78_755_0.png)

图 22-4

### 基础类型的数组

当你的程序为数组分配内存时，它分配的是一段连续的内存块，其中每块内存都足够大以容纳数组的单个元素。例如，在栈上可以如下所示声明一个包含五个 `int` 元素的局部数组：

```
int myArray[5];
```

图 22-5 显示了数组创建后的内存状态。在栈上创建数组时，大小必须是编译时已知的常量值。

> 注意：某些编译器允许在栈上使用变变大小数组。这并不是 C++ 的标准功能，因此当你看到这种写法时，我建议谨慎地避免使用。

![](img/5dda262a2e4cfd8040434fe81f2b4e78_759_0.png)

图 22-5

在堆上声明数组也没有区别，只是你使用指针来引用数组的位置。以下代码为包含五个 `int` 的数组分配了内存，并将内存指针存储在名为 `myArrayPtr` 的变量中。

```
int* myArrayPtr = new int[5];
```

![](img/5dda262a2e4cfd8040434fe81f2b4e78_759_1.png)

图 22-6

图 22-6 说明，基于堆的数组与基于栈的数组类似，但位于不同的位置。`myArrayPtr` 变量指向数组的第 0 个元素。

每个对 `new[]` 调用都应该与 `delete[]` 调用配对以清理内存。例如：

```
delete [] myArray;
```

将数组放在堆上的优势是，你可以使用动态内存并在运行时定义其大小。该函数从一个名为 `addUserNumberOfDocuments()` 的假设函数接收所需的文档数量，并利用该数量创建一个 `Document` 对象的数组。

```
Document* createArray() {
    int numDocs = addUserNumberOfDocuments();
    Document* createArray = new Document[numDocs];
    return createArray;
}
```

记住每个对 `new[]` 调用都应该与 `delete[]` 调用配对，因此在这个例子中，`createArray` 的调用者使用 `delete[]` 来清理返回的内存是非常重要的。另一个问题是 C 风格数组无法增加其大小，无论返回的数组中有多少元素。

在前面的函数中，`createArray` 是一个动态分配的数组。不要将其与动态数组混淆。该数组不是动态的，因为一旦分配完成，它的大小就不会改变。动态内存允许你在运行时指定分配块的大小，但它不会自动调整其大小以适应数据。

> 注意：存在某些数据结构（如 STL 容器），它们可以动态调整大小并知道自己的实际大小。你应该使用这些 STL 而不是标准数组，因为它们使用起来安全得多。

C++ 中有一个名为 `realloc()` 的函数，它是 C 语言的遗留。不要使用它！在 C 中，`realloc()` 用于通过为新数据分配内存块来有效地更改数组大小，将所有旧数据复制到新位置，并删除旧内存块。这种方法在 C++ 中是非常危险的，因为用户定义的对象不会对位拷贝产生良好响应。

> 警告：不要在 C++ 中使用 `realloc()`。它可不是你的朋友。

### 对象数组

对象数组与简单类型数组没有区别。当你使用 `new[N]` 分配一个包含 N 个对象的数组时，系统会为 N 个连续块分配足够的空间，每块空间都足够容纳一个对象。使用 `new[]` 时，每个对象的零参数构造函数将被自动调用。通过这种方式，使用 `new[]` 分配对象数组将返回一个指向完全形成并初始化的数组的指针。

例如，考虑以下类：

```
class Simple {
public:
    Simple() { cout << "Simple created" << endl; }
    ~Simple() { cout << "Simple destroyed" << endl; }
};
```

假设我们创建了 `Simple` 数组：

```cpp
Simple* arr = new Simple[5];
```

这会调用 5 次 `Simple` 的构造函数。当我们删除该数组时：

```cpp
delete[] arr;
```

这会调用 5 次 `Simple` 的析构函数。

如果存在派生类：

```cpp
class Base {
public:
    Base() { cout << "Base created" << endl; }
    virtual ~Base() { cout << "Base destroyed" << endl; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived created" << endl; }
    ~Derived() { cout << "Derived destroyed" << endl; }
};
```

如果我们创建一个 `Derived` 数组：

```cpp
Base* arr = new Derived[5];
```

这会调用 5 次 `Base` 构造函数和 5 次 `Derived` 构造函数。但是当我们删除该数组时：

```cpp
delete[] arr;
```

只会调用 5 次 `Base` 的析构函数，而不会调用 `Derived` 的析构函数。这就是为什么在基类中应将析构函数声明为 `virtual` 的原因。

# 对象的数组

对象数组与简单类型数组没有区别。当你使用 `new[N]` 分配一个包含 N 个对象的数组时，系统会为 N 个连续块分配足够的空间，每块空间都足够容纳一个对象。使用 `new[]` 时，每个对象的零参数构造函数将被自动调用。通过这种方式，使用 `new[]` 分配对象数组将返回一个指向完全形成并初始化的数组的指针。

例如，考虑以下类：

```
class Simple {
public:
    Simple() { cout << "Simple created" << endl; }
    ~Simple() { cout << "Simple destroyed" << endl; }
};
```

假设我们创建了 `Simple` 数组：

```cpp
Simple* arr = new Simple[5];
```

这会调用 5 次 `Simple` 的构造函数。当我们删除该数组时：

```cpp
delete[] arr;
```

这会调用 5 次 `Simple` 的析构函数。

如果存在派生类：

```cpp
class Base {
public:
    Base() { cout << "Base created" << endl; }
    virtual ~Base() { cout << "Base destroyed" << endl; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived created" << endl; }
    ~Derived() { cout << "Derived destroyed" << endl; }
};
```

如果我们创建一个 `Derived` 数组：

```cpp
Base* arr = new Derived[5];
```

这会调用 5 次 `Base` 构造函数和 5 次 `Derived` 构造函数。但是当我们删除该数组时：

```cpp
delete[] arr;
```

只会调用 5 次 `Base` 的析构函数，而不会调用 `Derived` 的析构函数。这就是为什么在基类中应将析构函数声明为 `virtual` 的原因。

# 对象的数组

对象数组与简单类型数组没有区别。当你使用 `new[N]` 分配一个包含 N 个对象的数组时，系统会为 N 个连续块分配足够的空间，每块空间都足够容纳一个对象。使用 `new[]` 时，每个对象的零参数构造函数将被自动调用。通过这种方式，使用 `new[]` 分配对象数组将返回一个指向完全形成并初始化的数组的指针。

例如，考虑以下类：
