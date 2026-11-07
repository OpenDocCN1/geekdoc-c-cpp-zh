
声明。当一个类定义只使用指向另一个类对象的指针或引用时（如本例所示），通常需要包含该另一个类的类头文件（该头文件会揭示该类的私有数据），但此时*不*需要通过 `#include` 包含它。这是因为编译器不需要为该类的对象预留空间。编译器*确实*需要为指针或引用预留空间。指针和引用的大小是编译器所运行硬件平台的特征，因此编译器已经知道这些大小。你只需在文件中使用该类型之前，用*前向类声明*（第 6 行）将该另一个类声明为一种数据类型即可。

```cpp
// Fig. 10.22: Interface.h
// Proxy class Interface definition.
// Client sees this source code, but the source code does not reveal
// the data layout of class Implementation.

class Implementation; // forward class declaration required by line 17

class Interface
{
public:
    Interface( int ); // constructor
    int setValue( int ); // same public interface as
    int getValue() const; // class Implementation has
    ~Interface(); // destructor
private:
    // requires previous forward declaration (line 6)
    Implementation *ptr;
}; // end class Interface
```

**图 10.22** | 代理类 Interface 的定义。

代理类 Interface 的成员函数实现文件（图 10.23）是唯一包含头文件 Implementation.h（第 5 行）的文件，该头文件包含类 Implementation。文件 Interface.cpp（图 10.23）作为预编译目标代码文件提供给客户端，同时提供头文件 Interface.h，其中包含代理类所提供服务的函数原型。由于文件 Interface.cpp 仅以目标代码形式提供给客户端，客户端无法看到代理类与专有类之间的交互（第 9、17、23 和 29 行）。代理类增加了一层额外的函数调用，作为隐藏类 Implementation 私有数据所付出的“代价”。鉴于当今计算机的速度，以及许多编译器能够自动*内联*简单函数调用这一事实，这些额外函数调用对性能的影响通常可以忽略不计。

```cpp
// Fig. 10.23: Interface.cpp
// Implementation of class Interface--client receives this file only
// as precompiled object code, keeping the implementation hidden.
#include "Interface.h" // Interface class definition
#include "Implementation.h" // Implementation class definition
```

**图 10.23** | Interface 类的成员函数定义。（第 1 部分，共 2 部分。）

- 成员对象（第 423 页）按照它们在类定义中声明的顺序构造，并且在其外围类对象构造之前构造。
- 如果没有为成员对象提供成员初始化器，则会隐式调用该成员对象的默认构造函数（第 423 页）。

## 10.4 节 *友元函数与友元类*

- 类的友元函数（第 429 页）定义在该类的作用域之外，但有权访问该类的所有成员。独立函数或整个类都可以声明为友元。
- 友元声明可以出现在类中的任何位置。
- 友元关系既不是对称的，也不是传递的。

## 10.5 节 *使用 this 指针*

- 每个对象都可以通过 this 指针（第 431 页）访问自己的地址。
- 对象的 this 指针不是对象本身的一部分——也就是说，this 指针所占内存的大小不会反映在对该对象执行 sizeof 运算的结果中。
- this 指针作为隐式参数传递给每个非静态成员函数。
- 对象可以隐式地（如到目前为止我们所做的那样）或显式地使用 this 指针来引用其数据成员和成员函数。
- this 指针支持级联成员函数调用（第 433 页），即在同一条语句中调用多个函数。

## 10.6 节 *static 类成员*

- 静态数据成员（第 437 页）表示“类范围”的信息（即类所有实例共享的类属性，而不是类中特定对象的属性）。
- 静态数据成员具有类作用域，可以声明为 public、private 或 protected。
- 类的静态成员即使在该类没有任何对象存在时也存在。
- 当类没有任何对象存在时，要访问公有静态类成员，只需在类成员名称前加上类名和作用域解析运算符（::）。
- 如果成员函数不访问类的非静态数据成员或非静态成员函数，则应将其声明为 static（第 438 页）。与非静态成员函数不同，静态成员函数没有 this 指针，因为静态数据成员和静态成员函数独立于类的任何对象存在。

## 10.7 节 *代理类*

- 为类的客户端提供一个代理类（第 442 页），该代理类只知道该类的公有接口，可使客户端使用类的服务，而不让客户端访问类的实现细节，例如其私有数据。
- 当一个类定义只使用指向另一个类对象的指针或引用时，不需要通过 #include 包含该另一个类的类头文件（该头文件通常会揭示该类的私有数据）。你只需在文件中使用该类型之前，用前向类声明（第 443 页）将该另一个类声明为一种数据类型即可。
- 包含代理类成员函数的实现文件是唯一包含我们要隐藏其私有数据的类的头文件的文件。
- 包含代理类成员函数的实现文件作为预编译目标代码文件提供给客户端，同时提供头文件，该头文件包含代理类所提供服务的函数原型。

## 自测练习

- **10.1** 填写下列各题中的空白：
    - a) 必须使用 ______ 来初始化类的常量成员。
    - b) `nonmember function` 必须声明为类的 ______，才能访问该类的私有数据成员。
    - c) 常量对象必须被 ______；创建后不能修改。
    - d) 一个 ______ 数据成员表示类范围的信息。
    - e) 对象的非静态成员函数可以访问指向该对象的“自指针”，该指针称为 ______ 指针。
    - f) 关键字 ______ 指定对象或变量不可修改。
    - g) 如果没有为类的成员对象提供成员初始化器，则会调用该对象的 ______。
    - h) 如果成员函数不访问 ______ 类成员，则应将其声明为 static。
    - i) 成员对象在 ______ 其外围类对象之前构造。

**10.2** 找出以下类中的错误，并说明如何改正：

```cpp
class Example
{
public:
   Example( int y = 10 )
      : data( y )
   {
      // empty body
   } // end Example's constructor

   int getIncrementedData() const
   {
      return ++data;
   } // end of function getIncrementedData

   static int getCount()
   {
      cout << "Data is " << data << endl;
      return count;
   } // end function getCount
private:
   int data;
   static int count;
}; // end class Example
```

### 自测练习答案

**10.1** a) 成员初始化器。b) 友元。c) 初始化。d) 静态。e) this。f) const。g) 默认构造函数。h) 非静态。i) 之前。

**10.2** *错误：* Example 的类定义中有两个错误。第一个错误出现在函数 getIncrementedData 中。该函数被声明为 const，但它修改了对象。

*改正：* 要改正第一个错误，请从 getIncrementedData 的定义中删除 const 关键字。

*错误：* 第二个错误出现在函数 getCount 中。该函数被声明为 static，因此不允许访问类的任何非静态成员（即 data）。

*改正：* 要改正第二个错误，请从 getCount 定义中删除输出行。

### 练习

- **10.3** *（友元关系）* 解释友元关系的概念。解释文中所述的友元关系的负面方面。

