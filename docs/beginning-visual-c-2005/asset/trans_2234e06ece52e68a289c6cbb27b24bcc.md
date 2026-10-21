

## 定义引用类类型

```
// Records the height in feet and inches
int feet;
int inches;
literal int inchesPerFoot = 12;

public:
    // Create a height from inches value
    Height(int ins)
    {
        feet = ins / inchesPerFoot;
        inches = ins % inchesPerFoot;
    }

    // Create a height from feet and inches
    Height(int ft, int ins) : feet(ft), inches(ins) {}

    // Create a string representation of the object
    virtual String^ ToString() override
    {
        return feet + L" feet " + inches + L" inches";
    }
```

现在构造函数使用名称 inchesPerFoot 而不是 12，因此不会对正在发生的事情产生任何疑问。

只要用于指定值的字段的名称先于定义，就可以将文字字段的值定义为其他文字字段的函数。例如：

```
value class Height
{
    // Other code...
    literal int inchesPerFoot = 12;
    literal double millimetersPerInch = 25.4;
    literal double millimetersPerFoot = inchesPerFoot * millimetersPerInch;
    // Other code...
};
```

在这里，您将文字字段 millimetersPerFoot 的值定义为其他两个文字字段的乘积。如果将 millimetersPerFoot 字段的定义移动到其中一个或两个其他字段之前，代码将无法编译。

引用类在功能上与原生 C++ 类相当，并且没有值类所具有的限制。但是，与原生 C++ 类不同，引用类没有默认的复制构造函数或默认的赋值运算符。如果您的类需要支持其中任何一个运算符，您必须显式添加该功能的函数——您将在下一章中看到如何操作。

您使用 ref class 关键字定义引用类——这两个词一起用一个或多个空格分隔代表一个关键字。以下是 Ex7_07 示例中的 CBox 类重新定义为引用类。

```
ref class Box
{
public:
    // No-arg constructor supplying default field values
    Box() : Length(1.0), Width(1.0), Height(1.0)
    {
        Console::WriteLine(L"No-arg constructor called.");
    }

    // Constructor definition using an initialisation list
    Box(double lv, double bv, double hv) :
        Length(lv), Width(bv), Height(hv)
    {
        Console::WriteLine(L"Constructor called.");
    }

    // Function to calculate the volume of a box
    double Volume()
    {
        return Length * Width * Height;
    }

private:
    double Length;    // Length of a box in inches
    double Width;     // Width of a box in inches
    double Height;    // Height of a box in inches
};
```

首先请注意，我已删除类名的 C 前缀和成员名的 m_ 前缀，因为这种记法不推荐用于 C++/CLI 类。您不能在 C++/CLI 类中为函数和构造函数参数指定默认值，因此您必须向 Box 类添加无参构造函数以实现此功能。无参构造函数只是将三个私有字段初始化为 1.0。

## 试用引用类类型

下面是一个使用您在上一节中看到的 Box 类的示例。

```
// Ex7_15.cpp : main project file.
// Using the Box reference class type

#include "stdafx.h"

using namespace System;

ref class Box
{
public:
    // No-arg constructor supplying default field values
    Box() : Length(1.0), Width(1.0), Height(1.0)
    {
        Console::WriteLine(L"No-arg constructor called.");
    }

    // Constructor definition using an initialisation list
    Box(double lv, double bv, double hv) :
        Length(lv), Width(bv), Height(hv)
    {
        Console::WriteLine(L"Constructor called.");
    }

    // Function to calculate the volume of a box
    double Volume()
    {
        return Length * Width * Height;
    }

private:
    double Length;    // Length of a box in inches
    double Width;     // Width of a box in inches
    double Height;    // Height of a box in inches
};

int main(array<System::String ^> ^args)
{
    Box^ aBox;                 // Handle of type Box^
    Box^ newBox = gcnew Box(10, 15, 20);
    aBox = gcnew Box;          // Initialize with default Box
    Console::WriteLine(L"Default box volume is {0}", aBox->Volume());
    Console::WriteLine(L"New box volume is {0}", newBox->Volume());

    return 0;
}
```

此示例的输出为：

```
Constructor called.
No-arg constructor called.
Default box volume is 1
New box volume is 3000
Press any key to continue . . .
```

### 如何工作

main() 中的第一条语句创建一个指向 Box 对象的句柄。

```
Box^ aBox;                 // Handle of type Box^
```

此语句不会创建对象，只是跟踪句柄 aBox。aBox 变量默认初始化为 nullptr，因此它尚未指向任何内容。相比之下，值类类型的变量始终包含一个对象。

下一条语句创建一个指向新 Box 对象的句柄。

```
Box^ newBox = gcnew Box(10, 15, 20);
```

接受三个参数的构造函数被调用以在堆上创建 Box 对象，并将地址存储在句柄 newBox 中。正如您所知，ref 类类型的对象始终在 CLR 堆上创建，并且始终使用句柄引用。

您通过调用无参构造函数创建 Box 对象并将其地址存储在 aBox 中。

```
aBox = gcnew Box;    // Initialize with default Box
```

此对象的 Length、Width 和 Height 字段设置为 1.0。

最后，您输出创建的两个 Box 对象的体积。

```
Console::WriteLine(L"Default box volume is {0}", aBox->Volume());
Console::WriteLine(L"New box volume is {0}", newBox->Volume());
```

由于 aBox 和 newBox 是句柄，因此您使用 -> 运算符调用它们所引用对象的 Volume() 函数。

## 类属性

属性是值类或引用类的成员，您可以像访问字段一样访问它，但它实际上不是字段。属性与字段的主要区别在于，字段的名称引用一个存储位置，而属性的名称则不是——它调用一个函数。属性具有 get() 和 set() 访问器函数，分别用于检索和设置其值，因此当您使用属性名获取其值时，幕后您正在调用该属性的 get() 函数，而当您在赋值语句的右侧使用属性名时，您正在调用其 set() 函数。如果属性仅提供 get() 函数的定义，则称为只读属性，因为 set() 函数不可用于设置属性值。属性可能仅定义 set() 函数，在这种情况下，它被描述为只写属性。

一个类可以包含两种不同的属性：标量属性和索引属性。标量属性是使用属性名访问的单个值，而索引属性是一组值，您使用属性名后跟方括号中的索引来访问它们。String 类具有标量属性 Length，它提供字符串中的字符数，对于 String 对象 str，您使用表达式 str->Length 访问 Length 属性，因为 str 是一个句柄。当然，要访问存储在变量 val 中的值类对象的名为 MyProp 的属性，您将使用表达式 val.MyProp，就像访问字段一样。字符串的 Length 属性是只读属性的示例，因为没有为其定义 set() 函数——您无法设置字符串的长度，因为 String 对象是不可变的。String 类还允许您将字符串中的单个字符作为索引属性访问。对于字符串句柄 str，您可以使用表达式 str[2] 访问第三个索引属性，这对应于字符串中的第三个字符。

属性可以与特定对象关联并且特定于该对象，在这种情况下，属性被描述为实例属性。String 对象的 Length 属性是实例属性的示例。您还可以将属性指定为 static，在这种情况下，属性与类关联，并且属性值对该类类型的所有对象都相同。让我们更深入地探讨属性。
