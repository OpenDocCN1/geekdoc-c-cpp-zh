

```
<< "Volume of box1 = " << boxVolume;
```

```
box2.m_Height = box1.m_Height - 10;  // Define box2
box2.m_Length = box1.m_Length / 2.0;  // members in
box2.m_Width = 0.25*box1.m_Length;    // terms of box1

cout << endl
    << "Volume of box2 = "
    << box2.Volume();
```

```
cout << endl
    << "Volume of cigarBox = "
    << cigarBox.Volume();

cout << endl;
return 0;
}
```

## 工作原理

既然你已经加入了自己版本的默认构造函数，编译器就不会再产生错误消息了，一切都正常工作。程序产生如下输出：

```
Constructor called.
Default constructor called.
Constructor called.
Volume of box1 = 33696
Volume of box2 = 6084
Volume of cigarBox = 40
```

默认构造函数所做的只是显示一条消息。显然，当你声明对象 box2 时，它被调用了。同时，三个 CBox 对象体积的值也都是正确的，因此程序的其余部分工作正常。

你可能已经注意到这个示例的一个方面：现在我们知道，构造函数可以像第 6 章中重载函数一样进行重载。你刚刚运行了一个包含两个构造函数的示例，它们的区别仅在于参数列表。一个构造函数有三个 double 类型的参数，另一个则完全没有参数。

## 在类中为参数指定默认值

在讨论函数时，你已经了解了如何在函数原型中为函数的参数指定默认值。对于类成员函数（包括构造函数），你也可以这样做。如果将成员函数的定义放在类定义的内部，就可以在函数头中放置参数的默认值。如果在类定义中只包含函数的原型，那么默认参数值应放在原型中。

如果你认为 CBox 对象的默认尺寸是一个所有边长均为 1 的单位盒子，可以将上一示例中的类定义修改为如下形式：

```
class CBox                 // Class definition at global scope
{
    public:
```

```
double m_Length;                         // Length of a box in inches
 double m_Width;                          // Width of a box in inches
 double m_Height;                         // Height of a box in inches

 // Constructor definition
 CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
 {
     cout << endl << "Constructor called.";
     m_Length = lv;                       // Set values of
     m_Width = bv;                        // data members
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
 }
};
```

如果对上一示例做了这一修改，会发生什么情况？当然，你又会从编译器那里得到一条错误消息。除了大量其他内容之外，编译器还会给出这些有用的提示：

```
warning C4520: 'CBox': multiple default constructors specified
error C2668: 'CBox::CBox': ambiguous call to overloaded function
```

这意味着编译器无法确定要调用两个构造函数中的哪一个——是那个你为参数设置了默认值的构造函数，还是那个不接受任何参数的构造函数。这是因为声明 box2 时需要调用一个不带参数的构造函数，而现在两个构造函数都可以在无参数的情况下被调用。一个显而易见的解决方案是去掉那个不接受参数的构造函数。这实际上是有益的。没有这个构造函数后，任何未显式初始化而声明的 CBox 对象，其成员都将被自动初始化为 1。

## 试一试    为构造函数参数提供默认值

你可以用下面这个简化的示例来演示这一点：

```
// Ex7_06.cpp
// Supplying default values for constructor arguments
#include <iostream>
using std::cout;
using std::endl;

class CBox                              // Class definition at global scope
{
public:
    double m_Length;                     // Length of a box in inches
```

```
double m_Width;                  // Width of a box in inches
double m_Height;                 // Height of a box in inches

// Constructor definition
CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0)
{
    cout << endl << "Constructor called.";
    m_Length = lv;                 // Set values of
    m_Width = bv;                  // data members
    m_Height = hv;
}

// Function to calculate the volume of a box
double Volume()
{
    return m_Length*m_Width*m_Height;
}
};

int main()
{
    CBox box2;                      // Declare box2 - no initial values

    cout << endl
         << "Volume of box2 = "
         << box2.Volume();

    cout << endl;
    return 0;
}
```

## 工作原理

你只声明了一个未初始化的 CBox 变量——box2——因为这是演示所需的全部内容。这个版本的程序产生如下输出：

```
Constructor called.
Volume of box2 = 1
```

这表明带默认参数值的构造函数正在履行其职责，即为那些没有指定初始值的对象设置成员值。

你不应该由此认为这是实现默认构造函数的唯一方式，甚至不是推荐的方式。在很多情况下，你不会希望以这种方式分配默认值，此时你就需要编写一个单独的默认构造函数。甚至会有一些时候，即使你已经定义了另一个构造函数，你也完全不希望有默认构造函数在起作用。这样可以确保类的所有已声明对象在声明时都必须显式指定初始值。

## 在构造函数中使用初始化列表

此前，你是在类的构造函数中使用显式赋值来初始化对象的成员。你还可以使用另一种不同的技术，即使用所谓的初始化列表。我可以用类 CBox 的构造函数的另一个版本来演示这一点：

```
// Constructor definition using an initialization list
CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0):
    m_Length(lv), m_Width(bv), m_Height(hv)
{
    cout << endl << "Constructor called.";
}
```

这个构造函数定义假定它位于类定义的内部。现在，数据成员的值不是在构造函数体内的赋值语句中设置的。与声明中一样，它们使用函数表示法指定为初始值，并作为函数头的一部分出现在初始化列表中。例如，成员 m_Length 由 lv 的值初始化。这比你在上一版本中使用的赋值方式更高效。如果将这一版本的构造函数替换到上一示例中，你会看到它同样运行良好。

请注意，构造函数的初始化列表与参数列表之间用冒号分隔，每个初始化项之间用逗号分隔。在构造函数中初始化参数的技术很重要，因为正如你稍后将看到的，它是为对象的某些类型的数据成员设置值的唯一方式。MFC 也严重依赖初始化列表技术。

## 类的私有成员

如果一个构造函数能设置类对象的数据成员的值，但仍然允许程序的任何部分去摆弄那些本质上属于对象核心的内容，这几乎就是自相矛盾的。打个比方，在你安排了一位技艺精湛、经过多年训练磨练的外科医生（如基尔代尔医生）来处理你的内部问题之后，再让当地的水管工或泥瓦匠来试上一手，这显然不太合适。你需要为类的数据成员提供一些保护。

在定义类成员时使用关键字 private，就可以获得所需的安全性。一般来说，私有的类成员只能被类的成员函数访问。有一个例外情况，但我们留到以后再讨论。普通函数无法直接访问类的私有成员。如图 7-6 所示。

能够将类成员指定为私有，也使得你可以将类的接口与其内部实现分离开来。类的接口由公共成员构成，尤其是公共成员函数，因为它们可以提供对类所有成员（包括私有成员）的间接访问。通过保持类的内部成员为私有，你可以在之后对它们进行修改，例如为了提升性能，而无需修改那些通过公共接口使用该类的代码。为了让类的数据成员和函数成员免受不必要的干涉，一个好的实践是：将那些不需要暴露出来的成员声明为私有。只将那些对你的类的使用至关重要的成员设为公共。

