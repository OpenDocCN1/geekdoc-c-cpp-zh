

# 图 7-6

## 试一试
私有数据成员

你可以重写 CBox 类，使其数据成员变为私有。

// Ex7_07.cpp
// A class with private members
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // Class definition at global scope
{
public:

    // Constructor definition using an initialisation list
    CBox(double lv = 1.0, double bv = 1.0, double hv = 1.0):
                        m_Length(lv), m_Width(bv), m_Height(hv)
    {
        cout << endl << "Constructor called.";
    }

    // Function to calculate the volume of a box
    double Volume()

![](img/2359b0c604600c58fba3539c738a356e_392_0.png)

{
    return m_Length*m_Width*m_Height;
}

private:
    double m_Length;            // Length of a box in inches
    double m_Width;             // Width of a box in inches
    double m_Height;            // Height of a box in inches
};

int main()
{
    CBox match(2.2, 1.1, 0.5);    // Declare match box
    CBox box2;                   // Declare box2 - no initial values

    cout << endl
         << "Volume of match = "
         << match.Volume();

    // Uncomment the following line to get an error
    // box2.m_Length = 4.0;

    cout << endl
         << "Volume of box2 = "
         << box2.Volume();

    cout << endl;
    return 0;
}

## 工作原理

现在，CBox 类的定义分为两个部分。第一部分是 public 部分，包含构造函数和成员函数 Volume()。第二部分被指定为 private，包含数据成员。现在，数据成员只能由类的成员函数访问。你不必修改任何成员函数——它们本来就可以访问类的所有数据成员。但是，如果你取消函数 main() 中给对象 box2 的 m_Length 成员赋值的语句的注释，就会得到一条编译器错误消息，确认该数据成员不可访问。如果你还没有这样做，可以在“类视图”中查看 CBox 类的成员；你会看到每个成员旁边的图标指示其可访问性；图标中的小挂锁表示该成员是 private 的。

> 有一点需要记住：现在，使用构造函数或成员函数是将值传入对象私有数据成员的唯一途径。你必须确保所有可能想要设置或修改类私有数据成员的方式都通过成员函数来提供。

你也可以将函数放入类的 private 部分。在这种情况下，它们只能由同一个类的其他函数成员调用。如果你将函数 Volume() 放在 private 部分，那么 main() 函数中试图使用它的语句将产生编译器错误。如果你将构造函数放在 private 部分，则无法声明该类的任何对象。

前面的示例生成如下输出：

```
Constructor called.
Constructor called.
Volume of match = 1.21
Volume of box2 = 1
```

输出表明，在将数据成员定义为具有 `private` 访问属性的情况下，类仍然工作正常。主要区别在于，它们现在完全受到保护，不会被未经授权地访问和修改。

> 如果没有特别指明，类成员的默认访问属性是 private。因此，你可以将所有私有成员放在类定义的开头，省略关键字，让它们默认为 private。不过，最好还是费点心思在每种情况下都明确写出访问属性，这样就不会对你的意图产生任何疑问。

当然，你不必让所有数据成员都是 `private`。如果你的类应用需要，你可以将一些数据成员定义为 `private`，另一些定义为 `public`。这完全取决于你要做什么。如果没有理由将类的成员设为 `public`，那么最好将它们设为 `private`，因为这会让类更安全。普通函数将无法访问类的任何 `private` 成员。

## 访问私有类成员

仔细想来，将类的数据成员声明为 `private` 有些过于极端。保护它们免受未经授权的修改固然很好，但没有理由将它们的值保密。你需要的是针对 `private` 成员的“信息自由法案”。

你不必为此给州参议员写信——它已经唾手可得。你只需编写一个成员函数来返回数据成员的值。请看 CBox 类的这个成员函数：

```
inline double CBox::GetLength()
{
    return m_Length;
}
```

为了展示它的写法，这里将它写成类外部的成员函数定义。我将其指定为 `inline`，因为这样既能获得速度提升，又不会让代码体积增加太多。假设你在类的 `public` 部分声明了该函数，就可以通过编写如下语句来使用它：

```
int len = box2.GetLength();    // Obtain data member length
```

你只需为每个希望对外界可用的数据成员编写一个类似的函数，就可以在不妨碍类安全性的前提下访问它们的值。当然，如果你将这些函数的定义放在类定义内部，它们默认就是 `inline` 的。

## 类的友元函数

在某些情况下，出于这样或那样的原因，你可能希望某些并非类成员的选定函数仍然能够访问类的所有成员——就像一个享有特殊特权的精英群体。这类函数称为类的友元函数，使用关键字 friend 定义。你可以在类定义中包含友元函数的原型，也可以包含完整的函数定义。在类定义中定义的友元函数默认也是 inline 的。

> 友元函数不是类的成员，因此访问属性不适用于它们。它们只是拥有特殊特权的普通全局函数。

设想你想在 CBox 类中实现一个友元函数来计算 CBox 对象的表面积。

## 试一试：使用友元计算表面积

在下面的示例中，你可以看到友元函数是如何工作的：

```
// Ex7_08.cpp
// Creating a friend function of a class
#include <iostream>
using std::cout;
using std::endl;

class CBox                         // Class definition at global scope
{
public:

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

private:
    double m_Length;                 // Length of a box in inches
    double m_Width;                  // Width of a box in inches
    double m_Height;                 // Height of a box in inches

// Friend function
friend double BoxSurface(CBox aBox);
}

// friend function to calculate the surface area of a Box object
double BoxSurface(CBox aBox)
{
    return 2.0*(aBox.m_Length*aBox.m_Width +
                aBox.m_Length*aBox.m_Height +
                aBox.m_Height*aBox.m_Width);
}

int main()
{
    CBox match(2.2, 1.1, 0.5);        // Declare match box
    CBox box2;                        // Declare box2 - no initial values

    cout << endl
         << "Volume of match = "
         << match.Volume();

    cout << endl
         << "Surface area of match = "
         << BoxSurface(match);

    cout << endl
         << "Volume of box2 = "
         << box2.Volume();

    cout << endl
         << "Surface area of box2 = "
         << BoxSurface(box2);

    cout << endl;
    return 0;
}
```

## 工作原理

你通过在函数原型前面加上关键字 friend，将 BoxSurface() 函数声明为 CBox 类的友元。由于 BoxSurface() 函数本身是一个全局函数，因此 friend 声明放在类定义中的哪个位置并不重要，但最好在放置此类声明时保持一致性。你可以看到，我选择将它放在类的所有 public 和 private 成员之后。请记住，友元函数不是类的成员，因此访问属性不适用于它。

函数的定义位于类定义之后。注意，在 BoxSurface() 的定义中，需要使用传递给函数的 CBox 对象作为参数来访问对象的数据成员。由于友元函数不是类成员，数据成员不能仅通过名称引用。它们都必须像在普通函数中那样用对象名称限定，当然，普通函数无法访问类的私有成员。友元函数与普通函数相同，只是它可以不受限制地访问其作为友元的那个类（或那些类）的所有成员。

