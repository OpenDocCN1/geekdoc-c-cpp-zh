
```cpp
// class DerivedOne definition
class DerivedOne : public Base {
public:
    // override print function
    void print() const override {std::cout << "DerivedOne\n";}
};

// class DerivedTwo definition
class DerivedTwo : public Base {
public:
    // override print function
    void print() const override {std::cout << "DerivedTwo\n";}
};

// class Multiple definition
class Multiple : public DerivedOne, public DerivedTwo {
public:
    // qualify which version of function print
    void print() const override {DerivedTwo::print();}
};

int main() {
    Multiple both{}; // instantiate a Multiple object
    DerivedOne one{}; // instantiate a DerivedOne object
    DerivedTwo two{}; // instantiate a DerivedTwo object
    std::array<Base*, 3> objects; // create array of base-class pointers

    objects[0] = &both; // ERROR—ambiguous
    objects[1] = &one;
    objects[2] = &two;

    // polymorphically invoke print
    for (int i{0}; i < 3; ++i) {
        objects[i]->print();
    }
}
```

*Microsoft Visual C++ 编译器错误消息：*

```text
fig20_26.cpp(40,22): error C2594: 'a': ambiguous conversions from 'Multiple *' to 'T*'
```

**图 20.26**  尝试多态地调用一个分别继承自两个基类的函数。（第 2 部分，共 2 部分。）

类 Multiple（第 28–32 行）同时继承自类 DerivedOne 和类 DerivedTwo。在类 Multiple 中，函数 print 被重写为调用 DerivedTwo 的 print（第 31 行）。注意，我们必须限定 print 调用——在本例中，我们使用了类名 DerivedTwo——以指定要调用哪个版本的 print。

函数 main（第 34–48 行）声明了类 Multiple（第 35 行）、DerivedOne（第 36 行）和 DerivedTwo（第 37 行）的对象。第 38 行声明了一个 Base* 指针数组。每个元素都被赋以一个对象的地址（第 40–42 行）。当把 both 的地址——一个 `Multiple` 类的对象——赋给 `objects[0]` 时，会发生错误。对象 both 实际上包含两个 Base 子对象。编译器不知道指针 `objects[0]` 应指向哪个子对象，因此会生成一个指示二义性转换的编译错误。

### 20.7.2 使用虚基类继承消除重复子对象

重复子对象的问题通过虚继承得到解决。当一个基类以 virtual 方式继承时，派生类中只会出现一个子对象。图 20.27 修改了图 20.26 的程序，以使用虚基类。

```cpp
// fig20_27.cpp
// Using virtual base classes.
#include <array>
#include <iostream>

// class Base definition
class Base {
public:
   virtual void print() const = 0; // pure virtual
};

// class DerivedOne definition
class DerivedOne : virtual public Base {
public:
   // override print function
   void print() const override {std::cout << "DerivedOne\n";}
};

// class DerivedTwo definition
class DerivedTwo : virtual public Base {
public:
   // override print function
   void print() const override {std::cout << "DerivedTwo\n";}
};

// class Multiple definition
class Multiple : public DerivedOne, public DerivedTwo {
public:
   // qualify which version of function to print
   void print() const override {DerivedTwo::print();}
};

int main() {
   Multiple both; // instantiate Multiple object
   DerivedOne one; // instantiate DerivedOne object
   DerivedTwo two; // instantiate DerivedTwo object
   std::array<Base*, 3> objects{}; // create array of base-class pointers
   objects[0] = &both; // allowed now
   objects[1] = &one;
   objects[2] = &two;

   // polymorphically invoke function print
   for (int i = 0; i < 3; ++i) {
       objects[i]->print();
   }
}
```

```text
DerivedTwo
DerivedOne
DerivedTwo
```

**图 20.27** | 使用虚基类。（第 1 部分，共 2 部分。）

**图 20.27** | 使用虚基类。（第 2 部分，共 2 部分。）

关键变化在于，类 DerivedOne（第 13 行）和 DerivedTwo（第 20 行）都使用 virtual public Base 从 Base 继承。由于这两个类都继承自 Base，因此它们各自包含一个 Base 子对象。直到类 Multiple 从 DerivedOne 和 DerivedTwo 继承（第 27 行）时，虚继承的好处才显现出来。由于每个基类都使用了**虚继承**，编译器确保 Multiple 只继承一个 **Base 子对象**。这消除了图 20.26 中编译器生成的二义性错误。现在，编译器允许在 main 的第 39 行将派生类指针（&both）隐式转换为基类指针 objects[0]。第 44–46 行的 for 语句会多态地调用每个对象的 print。

### 具有 virtual 基类的多重继承层次结构中的构造函数

如果为基类使用默认构造函数，那么实现带有虚基类的层次结构会更简单。图 20.26 和图 20.27 使用编译器生成的默认构造函数。如果虚基类提供了一个需要参数的构造函数，派生类的实现就会变得更复杂。最派生类必须**显式调用虚基类的构造函数**。因此，考虑为虚基类提供默认构造函数，以便可以隐式调用基类构造函数。[^26]

[^26]: “继承——多重继承与虚继承：使用虚继承时，我需要了解哪些特殊注意事项？” 访问于 2023 年 4 月 18 日。https://isocpp.org/wiki/faq/multiple-inheritance#virtual-inheritance-abcs.

### 20.8  public、protected 和 private 继承

你可以选择 public、protected 和 private 继承。public 继承最常见，protected 继承很少见。下图总结了每种继承类型下，基类成员在派生类中的可访问性。第一列包含基类成员的访问说明符。

| 基类访问说明符 | public 继承 | protected 继承 | private 继承 |
|---|---|---|---|
| public | 在派生类中为 public。<br><br>可由成员函数、友元函数和非成员函数直接访问。 | 在派生类中为 protected。<br><br>可由成员函数和友元函数直接访问。 | 在派生类中为 private。<br><br>可由成员函数和友元函数直接访问。 |
| protected | 在派生类中为 protected。<br><br>可由成员函数和友元函数直接访问。 | 在派生类中为 protected。<br><br>可由成员函数和友元函数直接访问。 | 在派生类中为 private。<br><br>可由成员函数和友元函数直接访问。 |
| private | 在派生类中不可访问。<br><br>可通过从基类继承的 public 或 protected 成员函数，由成员函数和友元函数访问。 | 在派生类中不可访问。<br><br>可通过从基类继承的 public 或 protected 成员函数，由成员函数和友元函数访问。 | 在派生类中不可访问。<br><br>可通过从基类继承的 public 或 protected 成员函数，由成员函数和友元函数访问。 |

使用 public 继承时

- public 基类成员成为 public 派生类成员，并且
- protected 基类成员成为 protected 派生类成员。

基类的 private 成员在派生类中永远不能直接访问，但可以通过调用继承来的、旨在访问这些 private 成员的 public 和 protected 基类成员函数来访问。

使用 protected 继承派生类时，public 和 protected 基类成员会成为 protected 派生类成员。使用 private 继承时，public 和 protected 基类成员会成为 private 派生类成员。

使用 private 和 protected 继承创建的类与其基类不具有 is-a 关系，因为派生类的客户端代码无法访问基类的 public 成员。

### 类与 struct 的默认继承

class 和 struct（在第 9.21 节中定义）都可以定义新类型。然而，class 与 struct 之间存在两个关键区别。第一个区别是，默认情况下，class 成员是 private，而 struct 成员是 public。另一个区别在于默认继承类型。如下所示的类定义：

```cpp
class Derived : Base {
  // ...
};
```
