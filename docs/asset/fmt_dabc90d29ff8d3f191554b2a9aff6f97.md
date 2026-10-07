
为了验证构造函数是否在创建对象时被自动调用，请查看程序 11.2。注意在实现部分，构造函数使用了一个 `cout` 语句来显示“Created the new complex number object”。

# 第11章

## 基本类函数

因此，每当构造函数被调用时，就会显示这条消息。由于 `main()` 函数创建了两个对象，构造函数被调用两次，消息也显示了两次。此外，由于创建对象时（如对象的实例化所示）不需要任何参数，该构造函数被正确地称为默认构造函数。

![](img/d5a225ca53b347501e86d72212077531_654_0.png)

# 程序 11.2

```cpp
#include <iostream>
using namespace std;

// 声明部分
class Complex
{
private:
    double realPart; // 将realPart声明为double类型变量
    double imaginaryPart; // 将imaginaryPart声明为double类型变量

public:
    Complex(double = 0.0, double = 0.0); // 构造函数原型
    // 使用默认参数
};

// 实现部分
Complex::Complex(double real, double imag)
{
    realPart = real;
    imaginaryPart = imag;

    cout << "Created the new complex number object "
         << realPart << " + " << imaginaryPart << "i\n";
}

int main()
{
    Complex a; // 声明对象
    Complex b(6.8, 9.7); // 声明对象

    return 0;
}
```

Copyright 2012 KPMG Learning. 版权所有。不得以任何形式或媒介复制、扫描、分发或传输。未经授权的情况下，某些第三方内容可能从电子书和章节中删除。编辑审查认为，任何被删除的内容都不会在后续限制需要时，对移除额外内容的整体权利产生实质性影响。

# 类类类

### 信息点

**构造函数**

构造函数是任何与其类同相同的函数。它的主要目的是在创建对象时初始化对象的数据成员，因此当从类中创建对象时，构造函数会被调用。一个类可以有多个构造函数，只要每个构造函数都能通过其参数列表区分。

当无法识别构造函数时，会发生编译错误。如果没有提供构造函数，编译器将提供一个什么都不执行的默认构造函数。此外，每个构造函数的声明都不能有返回类型（即使是 `void` 也不行）。尽管它们是函数，但构造函数只能用于创建对象的语句。

“默认构造函数”一词在 C++ 中经常使用，指的是任何在调用时不需要参数的构造函数。之所以不需要参数是因为没有声明参数；例如，`Complex(double real = 0.0);` 是一个有效的默认构造函数原型。每个参数都已给出了默认值，可以在不提供任何参数的情况下声明类型为 `Complex` 的对象。使用此默认构造函数，声明 `Complex a;` 会将对象的实部和虚部都初始化为值 0.0。每个类只能有一个默认构造函数。

运行程序 11.2 时产生以下输出：

Created the new number object 0 + 0i

Created the new number object 6.8 + 9.7i

虽然构造函数中可以使用任何合法的 C++ 语句（例如程序 11.2 中的代码语句），但最好保持构造函数简单，并仅用于初始化目的。关于程序 11.2 中的构造函数还需要说明一点：根据 C++ 规则，数据成员是按照它们在声明部分的声明顺序进行初始化的，而不是它们在实现部分函数定义中出现的顺序。通常，这个顺序没有问题，除非一个数据成员是由另一个数据成员的值化的。

# 调用构造函数

正如你所看到的，每当创建对象时，就会调用构造函数。然而，创建对象可以通过多种方式。例如，程序 11.2 中使用的声明

`Complex b(6.8, 9.7);`

也可以写成

`Complex b = Complex(6.8, 9.7);`

第二种形式将 b 声明为 Complex 类型，并直接调用带有参数 6.8 和 9.7 的构造函数。当只向构造函数传递一个参数时，这种形式可以简化。例如，如果只需要将 c 对象的 `realPart` 数据成员初始化为值 6.8，而 `imaginaryPart` 数据成员可以使用默认值 0.0，可以使用此声明创建对象：

```cpp
Complex c = 6.8;
```

因为使用等号的形式代表了 C 语言中的声明，因此被称为 C 风格初始化。程序 11.2 中的声明形式没有等号，被称为 C++ 风格初始化，并将在本书的剩余部分中使用。

无论你使用哪种初始化方式，对象都不应该用空括号来声明。例如，声明 `Complex a();` 与声明 `Complex a;` 不同，后一个声明使用默认构造函数，而第一个声明将不会创建任何对象。

# 析构函数

构造函数的对应项是析构函数。与构造函数具有相同类的函数前面有一个波浪号 `~`。因此，对于 Complex 类，析构函数是 `~Complex()`。与构造函数一样，如果没有提供，C++ 编译器将提供一个默认的空析构函数。然而，与构造函数不同，每个类只能有一个析构函数，因为析构函数不接受参数也不返回值。

析构函数在对象消失时自动调用，旨在“清理”对象可能留下的任何不良影响。通常，这些只在对象具有指针成员时发生。

# 访问器函数

访问器函数的目的是提供一种报告对象状态的方法。它可以简单地提供存储在数据成员中的值或与一个或多个值相关的特征。例如，与其提供复数的实部和虚部，访问器函数可以报告该数所在的象限。返回数据成员中实际值的访问器函数传统上称为 `get()` 函数，尽管这通常也适用于任何返回有关对象数据成员信息的函数。

以下是用于返回 Complex 对象实部和虚部的简单内联访问器函数：

```cpp
double getReal() { return realPart; }
double getImaginary() { return imaginaryPart; } // 内联访问器
```

程序 11.3 在完整程序的上下文中显示了这些访问器函数。由于类的所有函数都已经在声明部分定义，因此不需要任何进一步的实现。

# 第 11 章

## 类函数

637

### 重点：访问器函数 (Accessor Functions)

访问器函数是一种类函数，通过访问对象的私有数据成员来返回有关对象的信息。以 "get" 命名的访问器函数通常用于返回单个数据成员的值。访问器函数极其重要，因为它们提供了一种检索和显示对象私有数据值的手段。

当你构造一个类时，要确保返回数据成员的精确值，但每个访问器函数并不需要返回该值的有用表示形式。例如，如果日期 12/25/2014 以整数 20142512 的形式存储，那么访问器函数可以直接显示这个值。然而，更有用的表示形式是 12/25/14 或 2014年12月25日。

## 修改器函数 (Mutator Functions)

修改器函数的目的是在对象创建后，提供一种更改对象数据成员的方法。你已经在第 11.1 节中看到过为 `Complex` 类定义的修改器函数。

```cpp
void Complex::assignNewValues(double real, double imag) // 一个修改器
{
  realPart = real;
  imaginaryPart = imag;
}
```

在实践中，这会在类的声明中被编码为内联函数，如下：

```cpp
void assignNewValues(double real, double imag) // 修改器
{realPart = real; imaginaryPart = imag;};
```

改变单个数据成员值的修改器函数专门称为 `set()` 函数，尽管该术语也常用于任何修改一个以上数据成员值的操作。以下是两个简单的内联修改器 `set` 函数，用于为 `Complex` 对象的实部和虚部赋值：

```cpp
void setReal(double rl) {realPart = rl};    // 内联修改器
void setImaginary(double im) {imaginaryPart = im}; // 内联修改器
```

程序 11.4 在一个完整程序的上下文中展示了这些修改器函数。

## 类类论

### 信息点

**修改器函数 (Mutator Functions)**

修改器是任何改变对象数据值的非构造函数成员函数。修改器函数用于在构造函数初始化对象数据成员后，更改对象的数据值。

一个类可以包含多个修改器，只要每个修改器都有唯一的名称或参数列表。例如，在 `Complex` 类中，你可以有一个用于更改对象实部的修改器，一个用于更改对象虚部的修改器，以及第三个同时改变这两个值的修改器。构造函数，其主要目的是在对象创建时初始化对象的数据成员，它们不被视为修改器。

## 程序 11.4

```cpp
#include <iostream>
using namespace std;
// 声明部分
class Complex
private:
    double realPart;
    double imaginaryPart;
public:
    Complex(double real = 0.0, double imag = 0.0) // 内联构造函数
        realPart = real; imaginaryPart = imag;
    double getReal() { return realPart; } // 内联访问器
    double getImaginary() { return imaginaryPart; } // 内联访问器
    void setReal(double rl) { realPart = rl; } // 内联修改器
    void setImaginary(double im) { imaginaryPart = im; } // 内联修改器
}; // 类声明结束

int main()
{
    Complex num1(16.4, 18.9); // 声明一个 Complex 对象
    cout << "The real part of num1 is " << num1.getReal() << endl;
    cout << "The imaginary part of num1 is " << num1.getImaginary() << endl;
    num1.setReal(25.2);
    num1.setImaginary(27.8);
    cout << "The real part of num1 is " << num1.getReal() << endl;
    cout << "The imaginary part of num1 is " << num1.getImaginary() << endl;
    return 0;
}
```

由于程序 11.4，这些修改器函数的输出如下：

num1 的实部是 16.4

num1 的虚部是 18.9

num1 的实部是 25.2

num1 的虚部是 27.8

## 642 类类论

图 11.3 中 `this` 周围的括号对于初始访问“对象地址在 this 指针中”是必要的。接着是点运算符 `.`，后面跟着数据成员的名称。需要括号是为了重写点运算符的优先级。如果没有括号，表达式将变为 `this.imaginaryPart`，这等同于 `*(this.imaginaryPart)`。在表达式中，点运算符在 `*` 运算符之前应用，并指的是“地址位于此对象 imaginaryPart 数据中的数据成员”。这种引用显然没有意义，因为不存在一个名为 `this` 的对象，而且 `imaginaryPart` 并不包含一个地址。

在 `(*pointer).dataMember` 中使用指针是一种非常特殊的符号，它是专门为之而存在的。通用表达式 `(*)` 可以替换为符号 `pointer->dataMember`。`->` 运算符是一个连字符后跟大于号。这两种方式都可用于定位数据成员。因此，这些表达式是等价的：

- `(*pointer).realPart` 可以替换为 `this->realPart`。
- `(*pointer)->imaginaryPart` 可以替换为 `this->imaginaryPart`。

例如，使用此指针时，Complex 类的 `assignValues()` 函数为了方便起见在此处重复：

```cpp
void assignValues(double real, double imag) {
  realPart = real; imaginaryPart = imag;
}
```

可以写为：

```cpp
void assignValues(double real, double imag) {
  this->realPart = real; this->imaginaryPart = imag;
}
```

显然，以这种方式使用 `this` 指针是没有必要的，并且会干扰函数的代码。在许多时候，被访问的对象必须从函数返回。在这种情况下，必须使用指针来访问成员。

## 基类/成员初始化

除了像程序 11.2 中 Complex 类那样通过赋值初始化对象的数据成员外，还可以使用第二种方法，称为基类/成员初始化。这种初始化只能应用于构造函数，并且可以用两种方式编写。第一种方法是在类的声明部分通过定义构造函数来包含初始化，使用如下格式：

`ClassName(参数列表):数据成员列表(初始化器) {`

这是一个使用这种基类/成员初始化的 Complex 类默认构造函数的示例：

```cpp
// 在声明部分
public:
  Complex(double rl = 0.0, double im = 0.0):realPart(rl),imaginaryPart(im);
  // 实现部分没有构造函数
```

10 这一主题在源代码较少时可以省略。

## 第 11 章

### 基础类函数

第二种方法是在类的声明部分声明一个带有默认值的函数原型，然后在类的实现部分定义构造函数时跟上初始化列表。对于 Complex 构造函数，它采用这种形式：

```cpp
// 在声明部分
public:
  Complex(double d = 0.0, double im = 0.0); // 带有默认值的原型
```

```cpp
// 在实现部分
Complex::Complex(double rl, double im):realPart(rl),imaginaryPart(im) {};
```
