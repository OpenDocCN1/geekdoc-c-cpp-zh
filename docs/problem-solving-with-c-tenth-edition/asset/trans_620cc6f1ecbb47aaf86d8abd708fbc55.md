

效率。编译器和运行时环境需要为虚函数做更多的工作，因此，如果你标记的虚成员函数比实际需要的多，你的程序效率会更低。

## 重写

当虚函数的定义在派生类中被更改时，程序员通常说该函数定义被重写了。在 C++ 文献中，有时会在术语 redefined 和 overridden 之间做出区分。两个术语都指在派生类中更改函数的定义。如果该函数是虚函数，则称为 overriding。如果该函数不是虚函数，则称为 redefining。这对你程序员来说似乎是一个愚蠢的区别，因为在两种情况下你做的都是同样的事情，但编译器对这两种情况的处理是不同的。

## 多态

术语多态指的是通过晚绑定使一个函数名关联多个含义的能力。因此，多态、晚绑定和虚函数本质上都是同一个主题。

### 自测练习

11. 假设你修改了类 Sale（Display 15.9）的定义，删除了保留字 virtual。输出会如何改变程序在 Display 15.12 中的输出？

## 虚函数与扩展类型兼容性

我们将讨论将类成员函数声明为虚函数的一些进一步后果，并做一个使用这些特性的示例。

C++ 是一种相当强类型的语言。这意味着项的类型始终会被检查，如果类型不匹配，例如当参数与形式参数之间存在类型不匹配且无法自动调用转换时，就会发出错误消息。这也意味着通常分配给变量的值必须与变量的类型匹配，尽管在少数明确定义的情况下，C++ 会执行自动类型转换（称为 *coercion*），使其看起来你可以将一种类型的值分配给另一种类型的变量。例如，C++ 允许你将类型为 `char` 或 `int` 的值分配给类型为 `double` 的变量。然而，C++ 不允许你将类型为 `double` 或 `float` 的值分配给任何整数类型（`char`、`short`、`int`、`long`）的变量。

然而，强类型检查虽然重要，但它干扰了面向对象编程中继承的根本思想。假设你定义了类 A 和类 B，并定义了类型为类 A 和类 B 的对象。你不能总是在这些类型的对象之间进行赋值。例如，假设一个程序或单元包含以下类型声明：

```cpp
class Pet
{
public:
    virtual void print();
    string name;
};
class Dog : public Pet
{
public:
    virtual void print(); //Keyword virtual not needed, but is
                          //put here for clarity. (It is also good style!)
    string breed;
};
Dog vDog;
Pet vPet;
```

现在集中关注数据成员 name 和 breed。（为了使此示例简单，我们将成员变量设为 *public*。在实际应用中，它们应为 *private* 并具有操作它们的函数。）

任何 Dog 也是 Pet。似乎应该允许程序将类型为 Dog 的值也视为类型为 Pet 的值，因此以下操作应该是允许的：

```cpp
vDog.name = "Tiny";
vDog.breed = "Great Dane";
vPet = vDog;
```

C++ 确实允许这种赋值。你可以将一个值，例如 vDog 的值，分配给父类型变量，例如 vPet，但不允许执行反向赋值。虽然上面的赋值是允许的，但分配给变量 vPet 的值会丢失其 breed 字段。

### DISPLAY 15.13 使用虚函数的更多继承

```cpp
//Program to illustrate use of a virtual function
//to defeat the slicing problem.

#include <string>
#include <iostream>
using namespace std;

class Pet
{
public:
    virtual void print();
    string name;
};

class Dog : public Pet
{
public:
    virtual void print(); //Keyword virtual not needed, but put
                          //here for clarity. (It is also good style!)
    string breed;
};

int main()
{
    Dog vDog;
    Pet vPet;

    vDog.name = "Tiny";
    vDog.breed = "Great Dane";
    vPet = vDog;

    //vPet.breed; is illegal since class Pet has no member named breed

    Dog *pDog;
    pDog = new Dog;
    pDog->name = "Tiny";
    pDog->breed = "Great Dane";

    Pet *pPet;
    pPet = pDog;
    pPet->print(); // These two print the same output:
    pDog->print(); // name: Tiny breed: Great Dane

    //The following, which accesses member variables directly
    //rather than via virtual functions, would produce an error:
    //cout << "name: " << pPet->name << " breed: "
    // << pPet->breed << endl;
    //generates an error message: 'class Pet' has no member
    //named 'breed'.
    //See Pitfall section "Not Using Virtual Member Functions"
    //for more discussion on this.

    return 0;
}

void Dog::print()
{
    cout << "name: " << name << endl;
    cout << "breed: " << breed << endl;
}

void Pet::print()
{
    cout << "name: " << endl;//Note no breed mentioned
}
```

### 示例对话

```
name: Tiny
breed: Great Dane
name: Tiny
breed: Great Dane
```

### PITFALL 切片问题

虽然将派生类对象分配给基类变量是合法的，但将派生类对象分配给基类对象会切掉数据。派生类对象中存在于基类中的任何数据成员在赋值中都会丢失，并且基类对象中同样不可用的任何成员函数也会丢失。

如果我们做出以下声明和赋值：

```cpp
Dog vDog;
Pet vPet;
vDog.name = "Tiny";
vDog.breed = "Great Dane";
vPet = vDog;
```

那么 vPet 不能作为在 Dog 中引入的成员函数的调用对象，并且数据成员 Dog::breed 会丢失。

### PITFALL 未使用虚成员函数

为了获得我们之前讨论的扩展类型兼容性的好处，你必须使用虚成员函数。例如，假设我们在 Display 15.13 的示例中没有使用成员函数。假设我们用以下内容代替

```cpp
pPet->print();
```

我们使用了以下内容：

```cpp
cout << "name: " << pPet->name
    << " breed: " << pPet->breed << endl;
```

这段代码会引发错误消息。原因在于表达式

```cpp
*pPet
```

其类型由 pPet 的指针类型决定。它是类型 Pet 的指针类型，而类型 Pet 没有名为 breed 的字段。

但 print() 已由基类 Pet 声明为虚。因此，当编译器看到调用

```cpp
pPet->print();
```

时，它会检查类 Pet 和 Dog 的虚表，并看到 pPet 指向类型为 Dog 的对象。因此它使用为

```cpp
Dog::print(),
```

生成的代码，而不是为

```cpp
Pet::print().
```

生成的代码。

使用动态变量的面向对象编程是一种非常不同的编程视角。起初这可能令人困惑。如果你牢记以下两条简单规则会有所帮助：

1. 如果指针 pAncestor 的域类型是指针 pDescendant 的域类型的基类，则允许以下指针赋值：

   ```cpp
   pAncestor = pDescendant;
   ```

   而且，被 pDescendant 指向的动态变量的任何数据成员或成员函数都不会丢失。

2. 虽然动态变量的所有额外字段都在那里，但你需要虚成员函数来访问它们。

### PITFALL 尝试在没有为每个虚成员函数提供定义的情况下编译类定义

逐步开发是明智的。这意味着先编码一点，然后测试一点，再编码一点更多，然后测试更多，等等。然而，如果你尝试编译具有 *virtual* 成员函数的类，但没有实现每个成员，你可能会遇到一些非常难以理解的错误消息，即使你没有调用未定义的成员函数！

如果在编译之前任何虚成员函数未被实现，则编译失败，并出现类似以下的错误消息：“undefined reference to *Class_Name* virtual table。”即使 *没有派生类* 且 *只有一个虚* 成员，如果该函数没有定义，仍然会出现这种消息。

使错误消息难以解读的原因是，如果没有为声明为 *virtual* 的函数提供定义，可能会出现进一步的错误消息，抱怨默认构造函数的未定义引用，即使这些构造函数实际上已经定义。

### 编程技巧 使析构函数成为虚函数

始终使析构函数成为虚函数是一个好习惯，但在解释为什么这是个好习惯之前，我们需要说一两句话关于析构函数如何与指针交互，以及析构函数成为虚函数意味着什么。考虑以下代码，其中 `SomeClass` 是一个析构函数不是虚函数的类：

```cpp
SomeClass *p = new SomeClass;
    . . .
delete p;
```

当使用 p 调用 *delete* 时，SomeClass 类的析构函数会自动被调用。现在，让我们看看当析构函数被标记为 *virtual* 时会发生什么。

描述析构函数如何与虚函数机制交互的最简单方法是说析构函数被视为具有相同的名称（即使它们实际上没有相同的名称）。例如，假设 Derived 是类 Base 的派生类，并且假设类 Base 中的析构函数被标记为 *virtual*。现在考虑以下代码：

```cpp
Base *pBase = new Derived;
    . . .
delete pBase;
```

当使用 pBase 调用 *delete* 时，会调用一个析构函数。由于类 Base 中的析构函数被标记为 *virtual* 并且指向的对象是类型为

