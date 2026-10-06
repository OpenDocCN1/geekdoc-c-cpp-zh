
注意程序 13-5 在第 6 行有一个针对 `Rectangle.h` 文件的 `#include` 指令。这使得 `Rectangle` 类的声明被包含文件中。要从这里创建一个可执行程序，必须采取以下步骤：

- 必须编译实现文件 `Rectangle.cpp`。`Rectangle.cpp` 不是一个完整的程序，因此你不能从它创建可执行文件。相反，你将 `Rectangle.cpp` 编译为对象文件，该文件包含了 `Rectangle` 类的编译代码。该文件通常命名为 `Rectangle.obj`。
- 必须编译主程序 `Pr13-4.cpp`。该文件也不是一个完整的程序；它不包含 `Rectangle` 类的任何实现代码。因此，你将此文件编译为对象文件，如 `Pr13-4.obj`。
- 将对象文件 `Pr13-4.obj` 和 `Rectangle.obj` 链接在一起创建一个可执行文件，该文件将命名为 `Pr13-4.exe`。

这一过程在图 13-15 中所示。这些步骤如何发生的具体细节在每个 C++ 开发系统中有所不同。幸运的是，大多数系统都会自动为你完成所有这些步骤。例如，在 Visual Studio 中，你创建一个项目，只需将所有文件添加到项目中即可。当你编译项目时，这些步骤就会为你处理好，并生成可执行文件。

将一个类拆分为规格文件和实现文件提供了极大的灵活性。首先，如果你想将你的类交给另一个程序员，你不需要与他们分享所有的源代码。你可以给他们规格文件和用于实现的已编译的对象文件。另一个程序员只需在他的程序中插入必要的 `#include` 指令，对其进行编译，并将其与你的对象文件链接。这防止了可能不了解你代码所有细节的另一个程序员做出引入 bug 的更改。

当必须修改类成员函数时，将类拆分为规格和实现文件会让事情变得更简单。只需要修改实现文件并将其重新编译为新的对象文件。使用该类的程序不需要完全重新编译，只需与新的对象文件链接即可。

## 13.6 内联成员函数

图 13-15 创建可执行文件
![](img/19adf328469566ea7b1008cebdb57840.png)

### 概念

当成员函数被写在类声明内部时，它被声明为内联（inline）的。

当成员函数的函数体较小时，通常将函数的定义（而不是其原型）放在类声明中更为方便。例如，在 `Rectangle` 类中，成员函数 `getWidth`、`getLength` 和 `getArea` 每个都只有一条语句。`Rectangle` 类可以像如下列表所示进行修订（此文件可以在学生源代码文件夹第 13 章的 Rectangle 2. 中找到）。

#### `Rectangle.h` 的内容（版本 2）

```cpp
// Rectangle 类的规格文件

// 此版本使用了一些内联函数

#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle {
private:
    double width;
    double length;
public:
    void setWidth(double);
    void setLength(double);
    double getWidth() const {
        return width;
    }
    double getLength() const {
        return length;
    }
    double getArea() const {
        return width * length;
    }
};

#endif
```

当成员函数在类的声明中定义时，它被称为内联函数。由于函数定义是类的一部分，因此不需要在函数头中使用作用域运算符和类名。

注意 `getWidth`、`getLength` 和 `getArea` 函数被声明为内联的，但 `setWidth` 和 `setLength` 函数不是。它们仍然定义在类声明之外。以下列表显示了修订后的 `Rectangle` 类的实现文件（此文件可以在学生源代码文件夹第 13 章的 Rectangle 2. 中找到）。

#### `Rectangle.cpp` 的内容（版本 2）

```cpp
// Rectangle 类的实现文件。

// 在类的这个版本中，getWidth、getLength，
// 和 getArea 函数在 Rectangle.h 中内联编写的。

#include "Rectangle.h" // Rectangle 类需要
#include <iostream> // cout 需要
#include <cstdlib> // exit 函数需要

using namespace std;

****************************************************
// setWidth 设置成员变量 width 的值。
****************************************************
void Rectangle::setWidth(double w) {
    if (w >= 0)
        width = w;
    else {
        cout << "Invalid width\n";
        exit(EXIT_FAILURE);
    }
}

****************************************************
// setLength 设置成员变量 length 的值。
****************************************************
void Rectangle::setLength(double len) {
    if (len >= 0)
        length = len;
    else {
        cout << "Invalid length\n";
        exit(EXIT_FAILURE);
    }
}
```

### 内联函数与性能

每次调用函数时，有很多工作在“后台”进行。局部变量被创建，参数的值存储在称为栈（stack）的内存区域。这些函数调用的开销会消耗宝贵的 CPU 时间。

内联函数的编译方式与其他函数不同。在可执行代码中，内联函数并不是被“调用”。在一个被称为内联展开的过程中，编译器会将内联函数的调用替换为代码本身。内联函数会导致代码增大，它们会影响性能。

### 检查

- 13.6 为什么要将类变量声明为 private？
- 13.7 当类变量声明为私有时，类外部如何存储或获取这些值？
- 13.8 什么是类的规格文件？什么是类的实现文件？
- 13.9 包含保护（include guard）的作用是什么？
- 13.10 程序中存在以下类组件：
    - BasePay 类声明
    - BasePay 成员函数
    - Overtime 类声明
    - Overtime 成员函数
    你应该在哪些文件中存储这些内容？
- 13.11 什么是内联成员函数？

## 13.7 构造函数

### 概念

构造函数是在类对象创建时自动调用的成员函数。

构造函数是与类名同名的成员函数。当对象在内存中创建或实例化时，它会被自动调用。将构造函数理解为初始化程序对于初始化成员变量或执行其他设置非常有帮助。

为了说明构造函数如何工作，请查看以下 Demo 类：

```cpp
class Demo {
public:
    Demo(); // 构造函数
};
```

```cpp
Demo::Demo() {
    cout << "Welcome to the constructor!\n";
}
```

Demo 类只有一个成员：一个名为 Demo 的函数。这个函数就是构造函数。当定义该类的实例时，Demo 函数会被自动调用。这在程序 13-6 中得到了演示。

### 程序 13-6

```cpp
// 此程序演示了构造函数。

#include <iostream>

using namespace std;

// Demo 类声明。
class Demo {
public:
    Demo(); // 构造函数
};

Demo::Demo() {
    cout << "Welcome to the constructor!\n";
}

int main() {
    Demo demoObject; // 定义一个 Demo 对象
    cout << "This program demonstrates an object\n";
    cout << "with a constructor.\n";
    return 0;
}
```

### 程序输出

欢迎使用构造函数！
此程序演示了一个带有构造函数的对象。

注意，构造函数的函数头与普通成员函数不同。它没有返回类型——即使是 `void` 也没有。这是因为构造函数不是通过函数调用执行的，并且不能返回值。构造函数外部定义的函数头采用如下形式：

```cpp
ClassName::ClassName(ParameterList)
```

在通用格式中，`ClassName` 是类的名称，`ParameterList` 是可选的参数声明列表。

在程序 13-6 中，`demoObject` 的构造函数在对象定义时自动执行。由于对象是在 `main` 函数的 `cout` 语句之前定义的，因此构造函数首先显示其消息信息。假设我们在两个 `cout` 语句之间定义了 `Demo` 对象，如下所示：

```cpp
cout << "This is displayed before the object is created.\n";
Demo demoObject; // 定义一个 Demo 对象。
cout << "In this is displayed after the object is created.\n";
```

这段代码将产生以下输出：

这在对象创建之前显示。
欢迎使用构造函数！
这在对象创建之后显示。

这个简单的示例说明了构造函数执行时会发生什么。更重要的是，你应该理解为什么类应该有一个构造函数。构造函数的目的是初始化对象的属性。由于构造函数在对象一创建时就会执行，因此它可以在其他代码使用这些成员之前，将对象的数据成员初始化为有效值。为每个类编写构造函数是一个良好的习惯。

例如，我们看过的 `Rectangle` 类可以从拥有构造函数中受益。程序可以定义一个 `Rectangle` 对象，然后在为 `width` 和 `length` 设置任何值之前，使用它来调用 `getArea` 函数。由于 `width` 和 `length` 成员变量未初始化，该函数将返回垃圾值。以下代码显示了 `Rectangle` 类更好的版本，配备了构造函数。构造函数将 `width` 和 `length` 都初始化为 `0.0`。（这些文件可以在学生源代码文件夹第 13 章：Rectangle Version 3 中找到）。

#### Rectangle.h 的内容 (版本 3)

```cpp
// Rectangle 类的规范文件
// 此版本包含一个构造函数。
#ifndef RECTANGLE_H
#define RECTANGLE_H

class Rectangle {
private:
    double width;
    double length;
public:
    Rectangle();                    // 构造函数
    void setWidth(double);
    void setLength(double);
    double getWidth() const { return width; }
    double getLength() const { return length; }
    double getArea() const { return width * length; }
};

#endif
```

#### Rectangle.cpp 的内容 (版本 3)

```cpp
// Rectangle 类的实现文件。
// 此版本包含一个构造函数。
#include "Rectangle.h"    // Rectangle 类需要
#include <iostream>          // cout 需要
#include <cstdlib>         // exit 函数需要

using namespace std;

/********************************************************************/
/* 构造函数将 width 和 length 初始化为 0.0。             *
/********************************************************************/
Rectangle::Rectangle() {
    width = 0.0;
    length = 0.0;
}

/********************************************************************/
/* setWidth 设置成员变量 width 的值。             *
/********************************************************************/
void Rectangle::setWidth(double w) {
    if (w >= 0)
        width = w;
    else {
        cout << "Invalid width\n";
        exit(EXIT_FAILURE);
    }
}

/********************************************************************/
/* setLength 设置成员变量 length 的值。            *
/********************************************************************/
void Rectangle::setLength(double len) {
    if (len >= 0)
        length = len;
    else {
        cout << "Invalid length\n";
        exit(EXIT_FAILURE);
    }
}
```

程序 13-7 演示了该类的新版本。它创建了一个 `Rectangle` 对象，并显示 `getWidth`、`getLength` 和 `getArea` 函数返回的值。（该文件可以在学生源代码文件夹 13 Rectangle Version 3 中找到）。

### 程序 13-7

```cpp
// 此程序使用 Rectangle 类的构造函数。
```
