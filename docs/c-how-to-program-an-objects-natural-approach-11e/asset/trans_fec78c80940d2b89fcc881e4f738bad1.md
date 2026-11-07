
## 多重继承示例

让我们考虑一个使用实现继承的多重继承示例（图 20.21–20.25），以揭示一个并不那么隐蔽的问题。类 Base1（图 20.21）包含

- 一个私有 int 数据成员（m_value；第 11 行），
- 一个构造函数（第 8 行），用于设置 m_value，以及
- 一个公有成员函数 getData（第 9 行），返回 m_value。

```cpp
// Fig. 20.21: Base1.h
// Definition of class Base1
#pragma once

// class Base1 definition
class Base1 {
public:
    explicit Base1(int value) : m_value{value} {}
    int getData() const { return m_value; }
private: // accessible to derived classes via getData member function
    int m_value;
};
```

**图 20.21** | 演示多重继承——Base1.h。

类 Base2（图 20.22）与类 Base1 类似，不同之处在于其私有数据是一个名为 m_letter 的 char（第 11 行）。与类 Base1 一样，Base2 有一个公有成员函数 getData，但该函数返回 m_letter 的值。

```cpp
// Fig. 20.22: Base2.h
// Definition of class Base2
#pragma once

// class Base2 definition
class Base2 {
public:
    explicit Base2(char letter) : m_letter{letter} {}
    char getData() const { return m_letter; }
private: // accessible to derived classes via getData member function
    char m_letter;
};
```

**图 20.22** | 演示多重继承——Base2.h。

类 Derived（图 20.23–20.24）通过多重继承从类 Base1 和 Base2 继承。类 Derived 具有

- 一个名为 m_real 的 double 类型私有数据成员（图 20.23，第 16 行），
- 一个构造函数，用于初始化类 Derived 的所有数据（第 12 行），
- 一个公有成员函数 getReal，返回 m_real 的值（第 13 行），以及
- 一个公有成员函数 toString，返回 Derived 对象的字符串表示（第 14 行）。

其中，一个来自类 Base1，另一个来自类 Base2。通过使用作用域解析运算符，这个问题很容易解决。Base1::getData() 获取从类 Base1 继承的变量（即名为 m_value 的 int 变量）的值，而 Base2::getData() 获取从类 Base2 继承的变量（即名为 m_letter 的 char 变量）的值。

## 测试多重继承层次结构

图 20.25 测试了图 20.21–20.24 中的类。第 10 行创建 Base1 对象 base1，并将其初始化为 int 值 10。第 11 行创建 Base2 对象 base2，并将其初始化为 char 值 'Z'。第 12 行创建 Derived 对象 derived，并将其初始化为包含 int 值 7、char 值 'A' 和 double 值 3.5。

```cpp
// fig20_25.cpp
// Driver for multiple-inheritance example.
#include <format>
#include <iostream>
#include "Base1.h"
#include "Base2.h"
#include "Derived.h"

int main() {
   Base1 base1{10}; // create Base1 object
   Base2 base2{'Z'}; // create Base2 object
   Derived derived{7, 'A', 3.5}; // create Derived object

   // print data in each object
   std::cout << std::format("{} {} {} {}\n",
      "Object base1 contains ", base1.getData(),
      "Object base2 contains ", base2.getData(),
      "Object derived contains ", derived.toString());

   // print data members of derived-class object
   // scope resolution operator resolves getData ambiguity
   std::cout << std::format("{} {} {} {}\n",
      "Data members of Derived can be accessed individually:",
      "int", derived.Base1::getData(),
      "char", derived.Base2::getData(),
      "double", derived.getReal());

   std::cout << "Derived can be treated as an object"
      << " of either base class.\n";

   // treat Derived as a Base1 object
   Base1* base1Ptr{&derived};
   std::cout << std::format("base1Ptr->getData() yields {}\n",
      base1Ptr->getData());

   // treat Derived as a Base2 object
   Base2* base2Ptr{&derived};
   std::cout << std::format("base2Ptr->getData() yields {}\n",
      base2Ptr->getData());
}
```

**图 20.25** | 演示多重继承。（第 1 部分，共 2 部分。）

```text
Object base1 contains: 10
Object base2 contains the character: Z
Object derived contains: int: 7; char: A; double: 3.5

Data members of Derived can be accessed individually:
int: 7
char: A
double: 3.5

Derived can be treated as an object of either base class:
base1Ptr->getData() yields 7
base2Ptr->getData() yields A
```

图 20.25 | 演示多重继承。（第 2 部分，共 2 部分。）

第 15–18 行显示每个对象的数据值。对于对象 `base1` 和 `base2`，我们调用每个对象的 `getData` 成员函数。尽管此示例中有两个 `getData` 函数，这些调用并不存在歧义。在第 16 行，编译器知道 `base1` 是类 `Base1` 的对象，因此调用类 `Base1` 的 `getData`。在第 17 行，编译器知道 `base2` 是类 `Base2` 的对象，因此调用类 `Base2` 的 `getData`。第 18 行通过调用 `derived` 的 `toString` 成员函数获取其内容。

第 22–26 行使用类 `Derived` 的 `get` 成员函数再次输出 `derived` 的内容。同样，这里存在歧义问题——该对象包含来自类 `Base1` 和类 `Base2` 的 `getData` 函数。表达式 `derived.Base1::getData()` 获取从类 `Base1` 继承的 `m_value` 的值，而 `derived.Base2::getData()` 获取从类 `Base2` 继承的 `m_letter` 的值。

### 演示多重继承中的*是-a*关系

单继承中的*是-a*关系同样适用于多重继承关系。为了演示这一点，第 32 行用 `&derived` 初始化 `Base1` 指针 `base1Ptr`。这是允许的，因为 `Derived` 对象*是一个* `Base1` 对象。第 34 行通过 `base1Ptr` 调用 `Base1` 成员函数 `getData`，以仅获取对象 `derived` 中 `Base1` 部分的值。第 37 行用 `&derived` 初始化 `Base2` 指针 `base2Ptr`。这是允许的，因为 `Derived` 对象*是一个* `Base2` 对象。第 39 行通过 `base2Ptr` 调用 `Base2` 成员函数 `getData`，以仅获取对象 `derived` 中 `Base2` 部分的值。

#### 20.7.1 菱形继承

前面的示例展示了多重继承，即一个类从两个或更多类继承的过程。例如，C++ 标准库中使用多重继承来构成类 `basic_iostream`，如下图所示：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1232_0.png)

类 `basic_ios` 是 `basic_istream` 和 `basic_ostream` 二者的基类。二者均通过单继承形成。类 `basic_iostream` 同时继承自 `basic_istream` 和 `basic_ostream`。这使得类 `basic_iostream` 对象能够提供 `basic_istreams` 和 `basic_ostreams` 的功能。在多重继承层次结构中，此图所描述的继承称为菱形继承。

类 `basic_istream` 和 `basic_ostream` 各自继承自 `basic_ios`，因此 `basic_iostream` 存在一个潜在问题。它可能继承 `basic_ios` 成员的两份副本——一份经由 `basic_istream`，一份经由 `basic_ostream`。这会产生歧义并导致编译错误——编译器将不知道应使用 `basic_ios` 成员的哪一份副本。让我们看看**使用虚基类如何解决这个问题**。

#### 菱形继承中出现歧义时产生的编译错误

图 20.26 演示了菱形继承中可能出现的歧义。类 Base（第 8–11 行）包含纯虚函数 `print`（第 10 行）。类 DerivedOne（第 14–18 行）和 DerivedTwo（第 21–25 行）各自公有继承自 Base，并重写函数 `print`。类 DerivedOne 和类 DerivedTwo 各自包含一个基类子对象——在本示例中即类 Base 的成员。

```cpp
// fig20_26.cpp
// Attempting to polymorphically call a function that is
// inherited from each of two base classes.
#include <array>
#include <iostream>

// class Base definition
class Base {
public:
    virtual void print() const = 0; // pure virtual
};
```

**图 20.26**  |  尝试以多态方式调用分别继承自两个基类的函数。（第 1 部分，共 2 部分。）

