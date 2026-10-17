
`DiscountSale`。这是 C++ 中一个非常巧妙的技巧。考虑对于 `DiscountSale` 类对象 `d1` 和 `d2` 的函数调用 `d1.savings(d2)`。`savings` 函数的定义在基类 `Sale` 的实现文件中，而该文件在考虑 `DiscountSale` 类之前就已经编译了。然而，在函数调用 `d1.savings(d2)` 中，调用函数的代码行知道如何使用为 `Sale` 类提供的 `bill` 函数定义。

这是如何运作的？为了编写 C++ 程序，你只需要假设它是魔法发生的，真正的解释已在本节的介绍中给出。当你将一个函数标记为 `virtual` 时，你是在告诉 C++ 环境：“等待这个函数在程序中使用时，然后获取与调用对象相对应的实现。”

显示 15.12 提供了一个示例程序，说明了虚函数 `bill` 以及使用 `bill` 的函数在完整程序中的工作原理。

## 显示 15.12 虚函数的使用（部分 1/2）

```cpp
// 展示虚函数 bill 的性能。
#include <iostream>
#include "sale.h" // 并不真正需要，但由于 ifndef 是安全的
#include "discountsale.h"
using namespace std;
using namespace salesavitch;
```

（续）

## 显示 15.12 虚函数的使用（部分 2/2）

```cpp
int main()
{
    Sale simple(10.00); // 一个 10.00 元的物品。
    DiscountSale discount(11.00, 10); // 一个 11.00 元的物品，折扣为 10%。
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    if (discount < simple) {
        cout << "Discounted item is cheaper.\n";
        cout << "Savings is $" << simple.savings(discount) << endl;
    } else {
        cout << "Discounted item is not cheaper.\n";
    }
    return 0;
}
```

## 示例对话

| 折扣后的商品更便宜。 |
| 节省了 $0.10 | |

为了在 C++ 中使用虚函数，你需要了解一些技术细节。我们在这里列出它们：
- 如果派生类中的定义与基类中的定义不同，且你希望它成为虚函数，则你需要在基类的函数声明中添加 `virtual` 关键字。你不需要在派生类的函数声明中添加保留字 `virtual`。如果一个函数在基类中是虚函数，那么它在派生类中自动也是虚函数。（不过，标记一下是个好习惯……）
- 保留字 `virtual` 被添加到函数声明中而不是函数定义中。
- 除非使用 `virtual` 关键字，否则你无法获得虚函数及其带来的好处。

既然虚函数如此出色，为什么不将所有成员函数都变成虚函数呢？几乎不总是使用虚函数的唯一原因是

**效率**。编译器和运行时环境需要虚函数需要大量工作，因此如果你在不需要时将成员函数标记为虚函数，你的程序效率将会降低。

## 重写 (Overriding)
当派生类中更改函数定义时，C++ 文献对“重定义”（redefined）和“重写”（overridden）进行了区分。如果该函数是虚函数，则被称为重写；如果该函数不是虚函数，则被称为重定义。对于你这个程序员来说，这似乎是一个愚蠢的区分，因为你做的是同样的事情，但编译器对这两种情况的处理不同。

## 多态 (Polymorphism)
多态一术语指的是通过晚绑定（late binding）为一个名称关联多个含义的能力。因此，多态、晚绑定和虚函数实际上都是一回事。

## 自测练习
11. 假设你通过删除保留字 `virtual` 修改了类 15.9 的定义。这会如何改变显示 15.2 的输出？

## 虚函数与扩展兼容性
我们将讨论声明类成员为 `virtual` 的一些进一步后果。C++ 是一种相当强类型的语言。这意味着对象的类型始终会进行检查，如果存在类型不匹配则会发布错误消息。这也意味着通常赋值给变量的值必须与变量的类型匹配，尽管在少数定义的情况下，C++ 会执行自动类型转换（称为强制类型转换），以便你将一种类型的值赋值给另一种类型。例如，C++ 允许将 `char` 或 `int` 的值赋值给 `double` 变量。然而，C++ 不允许将 `double` 或 `float` 的值赋值给任何整数类型（`char, short, int, long`）。

## 继承
然而，尽管强类型很重要，但类型检查干扰了面向对象编程中继承的核心理念。假设你定义了类 `A` 和类 `B`，并定义了类型为 `A` 和 `B` 的对象。你不能总是对这些类型赋值。例如，假设程序或单元包含以下类型声明：

```cpp
class Pet {
public:
    virtual void print();
    string name;
}
class Dog : public Pet {
public:
    virtual void print(); // 需要 virtual 关键字，但为了清晰
    // 放在这里。（这也是良好的风格！）
    string breed;
}
Dog vDog;
Pet pPet;
```

现在关注数据成员 `name` 和 `breed` 为了保持此示例简单，我们将成员变量设为公共。在实际应用程序中，它们应该是私有的并有操作它们的函数）。任何 `Dog` 都是 `Pet`。允许程序将类型为 `Dog` 的值视为 `Pet` 的值似乎是有，因此以下操作应该是允许的：

```cpp
vDog.name = "Tiny"
vDog.breed = "Great Dane"
pPet = vDog;
```

C++ 允许这种赋值。你可以将一个值（例如 `vDog` 的值）赋值给父类类型的变量（如 `pPet`），但不允许执行反向赋值。尽管上述赋值是允许的，但赋值给变量 `pPet` 的值却丢失了它的 `breed` 字段。

## 15.3 多态

这被称为切片问题（slicing problem）。以下访问将产生错误信息：

```cpp
cout << Pet.breed; //非法：类 Pet 中没有名为 breed 的成员
```

你可能会认为这是有道理，因为一旦 `Dog` 被移动到 `Pet` 类型的变量中，它应该被像其他任何 `Pet` 一样对待，而不应该拥有 `Dog` 特有的属性。这引发了一场有趣的哲学辩论，但在编程时它只会带来麻烦。狗 Tiny 仍然是一只大丹犬，即使我们在某个环节将其视为一个 `Pet`，我们仍然希望引用它的品种。

幸运的是，C++ 为我们提供了一种将 `Dog` 视为 `Pet` 而不丢失品种名称的方法。为了做到这一点，我们使用指向动态实例的指针。假设我们添加了以下声明：

```cpp
Pet *pPet;
Dog *pDog;
```

如果我们使用指针和动态变量，就可以在不丢失品种的情况下将 Tiny 视为 `Pet`。以下操作是允许的：

```cpp
pDog = new Dog;
pDog->name = "Tiny";
pDog->breed = "Great Dane";
pPet = pDog;
```

此外，我们仍然可以访问 `pPet` 指向的节点的 `breed` 字段。假设：

```cpp
//使用 iostream
void Dog::print()
{
    cout << "name: " << name << endl;
    cout << "breed: " << breed << endl;
}
```

语句

```cpp
pPet->print();
```

将在屏幕上打印以下内容：

name: Tiny
breed: Great Dane

这是因为 `print()` 是一个虚成员函数。（此处无意双关语。）我们在显示 15.13 中包含了测试代码。

# 第 15 章 / 继承

## 显示 15.13 虚函数的进一步继承（第 1 部分，共 2 部分）

```cpp
// 演示使用虚函数
// 解决切片问题的程序。
#include <string>
#include <iostream>
using namespace std;
class Pet {
public:
    virtual void print();
    string name;
};
class Dog : public Pet {
public:
    virtual void print(); // 关键字 virtual 不需要，但为了清晰
    // 放在这里。（这也是良好的代码风格！）
    string breed;
};
int main() {
    Dog vDog;
    Pet vPet;
    vDog.name = "Tiny";
    vDog.breed = "Great Dane";
    vPet = vDog;
    //vPet.breed; 是非法的，因为类 Pet 中没有名为 breed 的成员
    Dog *pDog;
    pDog = new Dog;
    pDog->name = "Tiny";
    pDog->breed = "Great Dane";
    Pet *pPet;
    pPet = pDog;
    pPet->print(); // 这两个打印出相同的输出：
    pDog->print(); // name: Tiny; breed: Great Dane
    // 以下内容直接访问成员变量
    // 而不是通过虚函数，将产生错误：
    cout << "name: " << pPet->name << " " << pPet->breed << "";
}
```

（续）

## 显示 15.13 虚函数的进一步继承（第 2 部分，共 2 部分）

```cpp
// << pPet->breed << endl;
// 生成错误信息：'class Pet' 没有名为
// 'breed' 的成员
// 关于此点的更多讨论，请参见“不使用虚成员函数”
// 章节。
    return 0;
}
void Dog::print() {
    cout << "name: " << name << endl;
    cout << "breed: " << breed << endl;
}
void Pet::print() {
    cout << "name: " << endl;// 注意这里没有提到 breed
}
```

# 示例对话

| name: Tiny |
| breed: Great Dane |
| name: Tiny |
| breed: Great Dane |

# 陷阱 切片问题

虽然派生类对象赋值给基类变量是合法的，但将派生类对象赋值给基类对象会“切掉”数据。派生类对象中不属于基类的任何数据在赋值时都会丢失。

并通过指针调用成员函数，讨论什么决定了实际调用的是哪个函数——是基类的成员函数还是派生类的函数。

## 章节总结

- 继承通过从一个类派生出另一个类并通过为派生类添加功能，为代码复用提供了工具。
- 派生类继承基类的所有成员，并可以添加新的成员。
- 晚绑定意味着决定使用哪个版本的成员函数最合适是在运行时决定的。C++ 使用虚函数来实现晚绑定。多态、晚绑定和虚函数实际上都是同一个主题。
- 基类中的保护（protected）成员可以直接被公有（public））类的成员函数访问。

## 自测练习答案

1. 你可以将派生类的对象作为类类型参数的输入。`HourlyEmployee`（小时制员工）是一个 `Employee`（员工）。`SalariedEmployee`（月薪员工）也是一个 `Employee`。

```cpp
class SmartBut : public Smart
{
  public:
    SmartBut();
    SmartBut(int newA, int newB, bool newCrazy);
    bool isCrazy() const;
  private:
    bool crazy;
};
```

3. 这是合法的，因为 `a` 和 `b` 在基类 `Smart` 中被标记为 `protected`，因此它们可以在派生类中通过名称进行访问。如果 `a` 和 `b` 被标记为 `private`，那么这将是不合法的。

4. `SalariedEmployee` 的定义中没有给出 `getName` 函数的声明，因为该函数没有在 `SalariedEmployee` 类中被重定义。它继承自基类 `Employee`。

```cpp
5. #include <iostream>
#include "salariedemployee.h"
using namespace std;
namespace employeeessavitch
```

```cpp
class TitledEmployee : public SalariedEmployee {
    public:
        TitledEmployee();
        TitledEmployee(string name, string theTitle, string sSSN, double salary);
        string getTitle() const;
        void setTitle(string title);
        void setName(string name);
    private:
        string title;
}; // namespace employeeessavitch
```

```cpp
6. namespace employeeessavitch {
  TitledEmployee::TitledEmployee()
    : SalariedEmployee(), title("No title yet")
  {
    // 故意为空
  }
  TitledEmployee::TitledEmployee(string name, string theTitle, string sSSN, double salary)
    : SalariedEmployee(name, sSSN, salary), title(theTitle)
  {
    // 故意为空
  }
  void TitledEmployee::setName(string name) {
    Employee::setName(title + name);
  }
} // namespace employeeessavitch
```

- 7. 如果你没有为派生类定义重载的赋值运算符或拷贝构造函数，会为派生类定义一个默认赋值运算符和一个默认拷贝构造函数。然而，如果类涉及指针、动态数组或其他动态数据，默认赋值运算符和默认拷贝构造函数几乎不会按照你的预期工作。
- 8. 构造函数按以下顺序调用：首先是父类，然后是类，最后是孙类。析构函数按相反顺序调用：首先是孙类，然后是类，最后是父类。
- 9. 使用了 `iostream` 和 `cstdlib`：
  void PartFilledArray::addValue(double newEntry)
```cpp
{ 
  if (numberUsed == maxNumber) {
    cout << "Adding to a full array.\n";
    exit(1);
  } else {
    a[numberUsed] = newEntry;
    numberUsed++;
  }
}
```
```cpp
PartFilledArray::PartFilledArray(const PartFilledArray& object) : maxNumber(object.maxNumber), numberUsed(object.numberUsed)
{ 
  a = new double[maxNumber];
  for (int i = 0; i < numberUsed; i++) {
    a[i] = object.a[i];
  }
}
```
```cpp
void PartFilledArray::operator=(const PartFilledArray& rightSide) {
    if (rightSide.maxNumber > maxNumber) {
        delete[] a;
        maxNumber = new double[rightSide.maxNumber];
    }
    numberUsed = rightSide.numberUsed;
    for (int i = 0; i < numberUsed; i++) {
        a[i] = rightSide.a[i];
    }
}
PartFilledArray::~PartFilledArray() {
    delete[] a;
}
```
```cpp
10. class PartFilledArrayMax : public PartFilledArray {
    public:
    PartFilledArrayWMax(int arraySize);
    PartFilledArrayWMax(const PartFilledArrayMax& object);
    ~PartFilledArrayWMax();
```
