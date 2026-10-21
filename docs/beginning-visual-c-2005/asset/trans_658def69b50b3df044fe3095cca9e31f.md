

使用此函数定义，程序将与原始程序完全相同。这使你能够在需要时将成员函数定义放在类定义之外，同时仍保留内联带来的执行性能优势。

你也可以将关键字 `inline` 应用于与类无关的普通函数，并获得相同的效果。然而，最好将其用于简短、简单的函数。

你现在需要了解更多关于声明类对象时会发生什么的内容。

## 类构造函数

在之前的程序示例中，你声明了 CBox 对象 box1 和 box2，然后费力地遍历每个对象的每个数据成员以便为其分配初始值。从几个角度来看，这是不令人满意的。首先，很容易遗漏对数据成员的初始化，特别是对于数据成员比我们的 CBox 类更多的类。对复杂类的多个对象的数据成员进行初始化可能涉及数页的赋值语句。对这种方法施加的最终限制是，当你定义类的私有数据成员时——你无论如何都无法从类外部访问它们。必须有更好的方法，当然有——它被称为类构造函数。

## 什么是构造函数？

类构造函数是类中的一个特殊函数，在创建类的新对象时被调用。因此，它提供了在对象创建时初始化对象的机会，并确保数据成员只包含有效值。一个类可以有多个构造函数，使你能够以各种方式创建对象。

你在类中命名构造函数时没有余地——它们始终与定义它们的类同名。例如，函数 CBox() 是我们类 CBox 的构造函数。它也没有返回类型。为构造函数指定返回类型是错误的；你甚至不能将其写为 void。类构造函数的主要目的是为类的<|message|> 数据元素分配初始值，并且构造函数不需要也不允许有返回类型。

## 试一试 为 CBox 类添加构造函数

让我们扩展我们的 CBox 类以加入构造函数。

```
// Ex7_04.cpp
// Using a constructor
#include <iostream>
using std::cout;
using std::endl;

class CBox        // Class definition at global scope
{
    public:
        double m_Length;        // Length of a box in inches
        double m_Width;         // Width of a box in inches
        double m_Height;        // Height of a box in inches
```

### Chapter 7

```cpp
// Constructor definition
CBox(double lv, double bv, double hv)
{
    cout << endl << "Constructor called.";
    m_Length = lv;                  // Set values of
    m_Width = bv;                   // data members
    m_Height = hv;
}
```

```cpp
// Function to calculate the volume of a box
double Volume()
{
    return m_Length* m_Width* m_Height;
}
};

int main()
{
    CBox box1(78.0,24.0,18.0);             // Declare and initialize box1
    CBox cigarBox(8.0,5.0,1.0);             // Declare and initialize cigarBox

    double boxVolume = 0.0;                 // Stores the volume of a box

    boxVolume = box1.Volume();              // Calculate volume of box1
    cout << endl
         << "Volume of box1 = " << boxVolume;

    cout << endl
         << "Volume of cigarBox = "
         << cigarBox.Volume();

    cout << endl;
    return 0;
}
```

## 它是如何工作的

构造函数 `CBox()` 使用三个类型为 double 的参数编写，对应于 CBox 对象的 `m_Length`、`m_Width` 和 `m_Height` 成员的初始值。构造函数中的第一条语句输出一条消息，以便你知道何时被调用。你不会在生产程序中这样做，但因为它在显示何时调用构造函数时非常有帮助，所以在测试程序时经常使用。我会定期为说明目的使用它。构造函数体内的代码非常简单。它只是将你在调用时传递给构造函数的参数分配给相应的数据成员。如果需要，你也可以包含检查是否提供了有效且非负的参数的检查，并且在实际环境中，你可能希望这样做，但我们在这里主要关注的是了解机制的工作方式。

在 `main()` 中，你使用初始化值声明对象 `box1`，用于数据成员 `m_Length`、`m_Width` 和 `m_Height`，按顺序排列。这些值在对象名称后面用括号括起来。这使用了函数式初始化记法，如你在第 2 章所见，也可以应用于初始化基本类型的普通变量。你还声明了第二个类型为 CBox 的对象，名为 `cigarBox`，它也有初始化值。

box1 的体积使用成员函数 Volume() 按与前一个示例相同的方式计算，然后显示在屏幕上。你还显示了 cigarBox 的体积值。示例的输出为：

```
Constructor called.
Constructor called.
Volume of box1 = 33696
Volume of cigarBox = 40
```

前两行是两次调用构造函数 CBox() 的输出，每声明一个对象一次。你在类定义中提供的构造函数在声明 CBox 对象时会自动调用，因此两个 CBox 对象都使用声明中出现的初始化值进行初始化。这些值按在声明中书写的顺序作为参数传递给构造函数。如你所见，box1 的体积与之前相同，而 cigarBox 的体积看起来可疑地像是其尺寸的乘积，这令人相当欣慰。

## 默认构造函数

尝试通过添加我们之前声明的 box2 来修改最后一个示例：

```
CBox box2;    // Declare box2 of type CBox
```

在这里，我们没有为 box2 提供初始化值。当你重建此版本的程序时，你会收到错误消息：

```
error C2512: 'CBox': no appropriate default constructor available
```

这意味着编译器正在寻找 box2 的默认构造函数（也称为无参构造函数，因为调用时不需要参数），因为你没有为数据成员提供任何初始化值。默认构造函数是不需要提供任何参数的构造函数，可以是构造函数定义中未指定参数的构造函数，也可以是所有参数都是可选的构造函数。好吧，这个语句在 Ex7_02.cpp 中是完全可以接受的，为什么现在不起作用呢？

答案是之前的示例使用了编译器提供的默认无参数构造函数，并且编译器提供了此构造函数，因为你没有提供一个。因为在这个示例中你确实提供了一个构造函数，编译器假设你已经处理好了一切，因此没有提供默认构造函数。因此，如果你仍然想使用未初始化的 CBox 对象声明，你必须自己包含默认构造函数。默认构造函数到底是什么样的？在最简单的情况下，它只是一个不接受任何参数的构造函数；它甚至不需要做任何事情：

```
CBox()    // Default constructor
{}        // Totally devoid of statements
```

你可以看到这样的构造函数在运行。

## 试一试 提供默认构造函数

让我们将默认构造函数的版本添加到最后一个示例中，同时加上 box2 的声明，以及 box2 数据成员的原始赋值。你必须将默认构造函数扩展到足以显示它被调用的程度。以下是程序的下一个版本：

```
// Ex7_05.cpp
// Supplying and using a default constructor
#include <iostream>
using std::cout;
using std::endl;

class CBox                 // Class definition at global scope
{
public:
double m_Length;          // Length of a box in inches
double m_Width;           // Width of a box in inches
double m_Height;          // Height of a box in inches

// Constructor definition
CBox(double lv, double bv, double hv)
{
    cout << endl << "Constructor called.";
    m_Length = lv;        // Set values of
    m_Width = bv;         // data members
    m_Height = hv;
}

// Default constructor definition
CBox()
{
    cout << endl << "Default constructor called.";
}

// Function to calculate the volume of a box
double Volume()
{
    return m_Length*m_Width*m_Height;
};

int main()
{
    CBox box1(78.0,24.0,18.0);        // Declare and initialize box1
    CBox box2;                        // Declare box2 - no initial values
    CBox cigarBox(8.0, 5.0, 1.0);      // Declare and initialize cigarBox

    double boxVolume = 0.0;           // Stores the volume of a box

    boxVolume = box1.Volume();        // Calculate volume of box1
    cout << endl
