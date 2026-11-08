
当然，体积将为 1，因为三个维度的初始值都是 1.0。Box 类的成员变量是私有的，这意味着我们无法设置这些成员。你可以将成员变量指定为公有，在这种情况下，你就可以从类外部显式地设置它们，如下所示：

```
    myBox.m_length = 1.5;
    myBox.m_width = 2.0;
    myBox.m_height = 4.0;
    std::cout << "Volume of myBox is " << myBox.volume() << std::endl;  // Volume is 12
```

但当然，将成员变量设为公有是不好的做法。这样做违背了数据隐藏原则。因此，我们需要一种不同的机制，用一组给定的值来初始化对象的私有成员变量。负责这一工作的特殊成员函数称为构造函数。

## 构造函数

类构造函数提供了在创建新对象时初始化该对象的机会，并确保成员变量包含有效值。它是类中一种特殊的函数，在几个重要方面与普通成员函数不同。类构造函数始终与类同名。构造函数也不返回值，因此没有返回类型。为构造函数指定返回类型是错误的。每当定义类的新实例时，都会调用构造函数。总是如此，没有例外。类类型的对象只能使用构造函数创建。

### 默认构造函数

等等，稍等一下！我们在上一节中创建了一个 Box 对象并计算了它的体积。这是怎么发生的？我们从未定义构造函数？好吧，如果你没有为类定义构造函数，编译器会提供一个默认构造函数。而且没错，这两个“默认”并不是笔误。多亏了这个默认的默认构造函数，Box 类的实际行为就好像定义如下：

```
    class Box
    {
    public:
      // The default constructor that was supplied by the compiler...
      Box()
      {
        // Empty body so it does nothing...
      }

      // Function to calculate the volume of a box
      double volume()
      {
        return m_length * m_width * m_height;
      }

    private:
      double m_length {1.0};
      double m_width {1.0};
      double m_height {1.0};
    };
```

*默认构造函数*是无需参数即可调用的构造函数。如果你没有显式调用带给定参数的构造函数，则默认调用此构造函数。

```
Box myBox;    // Invokes the default constructor
```

如果你没有为类定义*任何*构造函数——既没有默认构造函数，也没有任何其他构造函数——那么编译器会为你生成一个：默认构造函数。这就是它被称为默认的默认构造函数的原因；它是由默认情况下生成的默认构造函数。默认的默认构造函数没有参数，其唯一目的是允许创建对象。它不做其他事情，因此所有成员变量都将具有其默认值。如果没有为基本类型（double、int、bool、...）或指针类型（int*、const Box* ...）的成员变量指定初始值，它将包含任意垃圾值。在 Box 类中，我们将所有成员变量初始化为 1.0，因此默认的默认构造函数总是让 Box 对象处于定义良好的初始状态。

一旦你定义了任何构造函数，即使是带参数的非默认构造函数，也不再提供默认的默认构造函数。在某些情况下，除了你定义的带参数的构造函数之外，你还需要一个无参数的构造函数。在这种情况下，你必须确保类中有一个默认构造函数的定义。

### 定义类构造函数

让我们扩展上一示例中的 Box 类，加入一个构造函数，然后检查它是否能正常工作：

```cpp
// Ex12_01.cpp
// Defining a class constructor
import <iostream>;

// Class to represent a box
class Box
{
public:
  // Constructor
  Box(double length, double width, double height)
  {
    std::cout << "Box constructor called." << std::endl;
    m_length = length;
    m_width = width;
    m_height = height;
  }

  // Function to calculate the volume of a box
  double volume()
  {
    return m_length * m_width * m_height;
  }

private:
  double m_length {1.0};
  double m_width {1.0};
  double m_height {1.0};
};

int main()
{
    Box firstBox {80.0, 50.0, 40.0};      // Create a box
    double firstBoxVolume {firstBox.volume()};  // Calculate the box volume
    std::cout << "Volume of Box object is " << firstBoxVolume << std::endl;

    // Box secondBox;          // Causes a compiler error message
}
```

这会生成以下输出：

```text
Box constructor called.
Volume of Box object is 160000
```

Box 类的构造函数有三个 double 类型的参数，分别对应对象的 m_length、m_width 和 m_height 成员变量的初始值。不允许有返回类型，并且构造函数的名称必须与类名 Box 相同。构造函数体中的第一条语句输出一条消息，以显示它何时被调用。你不会在生产程序中这样做，但在测试程序以及理解正在发生什么和何时发生时，这很有帮助。我们会经常使用它来跟踪示例中正在发生的事情。构造函数体中的其余代码将参数赋给相应的成员变量。

> **注意**  请注意 m_ 命名约定在构造函数定义中是多么有效。如果我们改用 length、width 和 height 作为成员变量的名称，我们就必须为 Box 构造函数的三个参数发明不同的名称。

第一个 Box 对象通过以下语句创建：

```cpp
Box firstBox {80.0, 50.0, 40.0};
```

成员变量 m_length、m_width 和 m_height 的初始值出现在花括号初始化器中，并作为参数传递给构造函数。因为列表中有三个值，编译器会查找具有三个参数的 Box 构造函数。当构造函数被调用时，它会显示输出第一行中出现的消息，因此你知道你添加到类中的构造函数被调用了。

我们之前说过，一旦你定义了构造函数，编译器就不再提供默认构造函数，至少默认情况下不会。这意味着以下语句将不再编译：

```cpp
Box secondBox;        // Causes a compiler error message
```

如果你希望允许像这样定义 Box 对象，就必须添加一个无参数构造函数的定义。我们将在下一节中这样做。 ³

³ 有些人还会使用 this->length = length; 这样的语句来规避这种名称冲突（本章后面会讨论 this 指针），但我们更喜欢更简洁的 m_ 命名约定。

### 使用 default 关键字

一旦你添加了构造函数——任何构造函数——编译器就不再隐式定义默认的默认构造函数。如果此后你仍然希望对象可默认构造，那么就需要你确保该类有一个默认构造函数。当然，你的第一个选择是自己定义一个。例如，对于 Ex12_01.cpp 中的 Box 类，你只需在类的公有部分的某个位置添加以下构造函数定义：

```
Box()  {}		// Default constructor
```

因为 Box 的成员变量在初始化期间已经被赋予有效值 1.0，所以你在默认构造函数体中无事可做。

除了定义函数体为空的默认构造函数之外，你还可以使用 default 关键字。该关键字可用于指示编译器生成默认构造函数，即使存在其他用户定义的构造函数。对于 Box，如下所示：

```
Box() = default;	// Defaulted default constructor
```

等号和分号都是必需的。带有默认化构造函数的 Ex12_01 修改版可在网上 Ex12_01A.cpp 中获取。

虽然显式的空函数体定义和默认化的构造函数声明几乎等价，但在现代 C++ 代码中更推荐使用 default 关键字：

> **提示**  如果默认构造函数体（或初始化列表，我们稍后会遇到）中无事可做，那么你应该使用 `= default;` 而不是 `{}`。这不仅更清楚地表明它涉及默认的默认构造函数，还有一些技术原因使编译器生成的版本成为更好的选择。

### 在类外定义函数

我们之前说过，成员函数的定义可以放在类定义之外。类构造函数也是如此。此时类定义本身只包含构造函数的签名，而不包含其函数体。例如，对于 Box 类，可以如下定义：

```cpp
// Class to represent a box
class Box
{
public:
  Box() = default;
  Box(double length, double width, double height);

  double volume();  // Function to calculate the volume of a box

private:
  double m_length {1.0};
  double m_width {1.0};
  double m_height {1.0};
};
```
