
```cpp
std::cout << "The two boxes that sum to the smallest volume are "
          << boxes[first] << " and " << boxes[second] << '\n';
std::cout << std::format("The volume of the first box is {:.1f}\n",
                         boxes[first].volume());
std::cout << std::format("The volume of the second box is {:.1f}\n",
                         boxes[second].volume());
std::cout << "The sum of these boxes is " << boxes[first] + boxes[second] << '\n';
std::cout << std::format("The volume of the sum is {:.1f}", minVolume.volume()) << std::endl;
}
```

我们得到以下输出：

```text
The two boxes that sum to the smallest volume are Box(39.8, 4.9, 17.0) and
Box(24.7, 8.8, 25.6)
The volume of the first box is 3341.7
The volume of the second box is 5586.6
The sum of these boxes is Box(39.8, 8.8, 42.6)
The volume of the sum is 14964.9
```

每次运行程序时，你应该会得到不同的结果。有关`createUniformPseudoRandomNumberGenerator()`函数的说明，请参阅第12章。

`main()`函数生成一个包含20个`Box`对象的向量，这些对象的尺寸为1到99之间的任意值。然后，嵌套的`for`循环测试所有可能的`Box`对象对，以找到组合后体积最小的那一对。内层循环中的`if`语句使用`operator+()`成员生成一个`Box`对象，该对象是当前对象对的和。然后（隐式地）使用`operator<=>()`成员将得到的`Box`对象与`minVolume`的值进行比较（请记住：编译器本质上会将`boxes[i] + boxes[j] <= minVolume`重写为`std::is_lteq(boxes[i] + boxes[j] <=> minVolume)`）。输出显示它有两个盒子，这是应该的。我们建议你对运算符函数和`Box`构造函数进行插桩，以查看它们何时以及被调用多少次。

当然，你可以在更复杂的表达式中使用重载的加法运算符来对`Box`对象求和。例如，你可以这样写：

```cpp
Box box4 {box1 + box2 + box3};
```

这会调用`operator+()`成员两次，创建一个表示三者之和的`Box`对象，并将其传递给`Box`类的复制构造函数以创建`box4`。结果是一个`Box`对象`box4`，它可以包含堆叠在一起的其他三个`Box`对象。

## 用另一个运算符实现一个运算符

一件事总是引向另一件事。如果你为一个类实现了加法运算符，就不可避免地会让人期望`+=`运算符也能工作。如果你要同时实现两者，值得注意的是，你可以非常经济地基于`+=`来实现`+`。

首先，我们为`Box`类定义`+=`。由于涉及赋值，惯例规定该运算符函数返回引用：

```cpp
// Overloaded += operator
Box& Box::operator+=(const Box& aBox)
{
    // New object has larger length and width, and sum of heights
    m_length = std::max(m_length, aBox.m_length);
    m_width  = std::max(m_width, aBox.m_width);
    m_height += aBox.m_height;
    return *this;
}
```

这很直接。你只需根据`Box`对象的加法定义，通过加上右操作数来修改左操作数（即`*this`）。现在你可以使用`operator+=()`来实现`operator+()`，因此`operator+()`的定义简化为以下内容：

```cpp
// Function to add two Box objects
Box Box::operator+(const Box& aBox) const
{
    Box copy(*this);
    copy += aBox;
    return copy;
}
```

函数体的第一行调用复制构造函数创建左操作数的副本，用于加法。然后调用`operator+=()`函数将右操作数对象`aBox`加到新的`Box`对象上。随后返回该对象。

复合赋值运算符返回指向自身的引用的惯例，其动机是它支持这样的语句，即在更大的表达式中使用赋值表达式的结果。为便于做到这一点，大多数通过惯例修改其左操作数的运算符会返回指向自身的引用，或者如果实现为非成员函数，则返回对第一个参数的引用。你已经在`<<`流运算符中看到了这一点，我们讨论递增和递减运算符的重载时还会再次遇到。

`Ex13_06`包含一个box模块，它从`Ex13_05`的模块开始，但按本节所述实现了加法运算符。使用这个新的`Box`定义，你可以轻松修改`Ex13_05`的`main()`函数，并尝试新的`+=`运算符。例如，在`Ex13_06.cpp`中，我们是这样做的：

```cpp
int main()
{
    // Generate boxCount random Box objects as before in Ex13_05...

    Box sum{0, 0, 0};          // Start from an empty Box
    for (const auto& box : boxes)  // And then add all randomly generated Box objects
        sum += box;

    std::cout << std::format("The sum of {} random boxes is {:.1f}ft", boxCount, sum.volume()) << std::endl;
}
```

> **提示** 始终根据对应的算术赋值运算符`op=()`来实现二元算术运算符`op()`。

## 成员函数与非成员函数

`Ex13_05`和`Ex13_06`都将`operator+()`定义为`Box`类的成员函数。然而，你也可以同样轻松地将这个加法实现为非成员函数。下面是这样一个函数的原型：

```cpp
Box operator+(const Box& aBox, const Box& bBox);
```

由于`Box`对象的尺寸可以通过公有成员函数访问，因此不需要友元声明。但即使成员变量的值不可访问，你仍然可以将该运算符定义为友元函数，这就引出了一个问题：这些选项中哪个最好？成员函数？非成员函数？还是友元函数？

在所有选项中，友元函数通常被认为是最不受欢迎的。虽然并不总是有可行的替代方案，但友元声明会破坏数据隐藏，因此应尽可能避免。

然而，在成员函数和非友元非成员函数之间做选择并不总是那么明确。运算符函数对类能力至关重要，因此我们大多倾向于将它们实现为类成员。这使这些函数成为该类型不可或缺的一部分，从而将其置于封装的核心。因此，你的默认选择可能应该是将运算符重载定义为成员函数。但至少有两种情况你应该改为将它们实现为非成员函数。

首先，有些情况下你别无选择，只能将它们实现为非成员函数，即使这意味着你必须求助于友元函数。这些情况包括二元运算符的重载，其中第一个参数要么是基础类型，要么是不同于你当前正在编写的类的类型。我们已经看到了这两类情况的示例：

```cpp
Box operator+(double value, const Box& box);    // double cannot have members
std::ostream& operator<<(std::ostream& stream, const Box& box); // cannot add ostream members
```

> **注意** 一旦某个运算符的某个重载需要是非成员函数，你可能会决定为了保持一致，也将所有其他重载变成非成员函数。例如，假设你为`Box`类定义了一个乘法运算符（留作练习）：
>
> ```cpp
> Box operator*(double, const Box&); // Must be nonmember function
> Box operator*(const Box&, double);   // Symmetrical case often done for consistency
> ```

这两个重载中只有第一个真正需要是非成员函数。C++20编译器只会尝试交换`<`、`>`、`<=`、`>=`、`==`、`!=`和`<=>`这些运算符的操作数顺序（见前文）。因此，为了获得对其他任何二元运算符（如`+`、`-`、`*`、`/`、`%`、`^`和`&`）的混合类型支持，你仍然至少需要一个非成员函数。不过，将另一种操作数顺序的函数也变成非成员函数，可以让你在源代码中很好地将这些声明分组在一起。

但还有一个原因可能让你有时更倾向于非成员函数而不是成员函数，那就是当希望二元运算符的左操作数进行隐式转换时。我们将在下一小节讨论这种情况。
