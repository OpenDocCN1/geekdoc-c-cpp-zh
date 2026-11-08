
```cpp
bool hasLargerVolumeThan(Cube cube); // Compare volume of a cube with another
private:
    double m_side;
};
```

对于 Cube 的这种定义，Ex12_04.cpp 将无法编译。编译器绝不会使用声明为 explicit 的构造函数进行隐式转换，因此它只能在程序中显式使用。通过对具有单个参数的构造函数使用 explicit 关键字，可以防止从参数类型到类类型的隐式转换。hasLargerVolumeThan() 成员只接受 Cube 对象作为参数，因此使用 double 类型的参数调用它将无法编译。

> **提示**  隐式转换可能导致代码令人困惑；大多数时候，如果使用显式转换，代码为何能编译以及它的作用会变得更加明显。因此，默认情况下，您应该将单参数构造函数声明为 explicit（注意，这包括多参数构造函数中除第一个参数外其余参数都有默认值的情况）；只有在确实需要隐式类型转换时才省略 explicit。

> **注意**  虽然不太常见，但任何非单参数构造函数也可以标记为 explicit。假设 processBox() 是一个参数类型为 Box 或 const Box& 的函数，那么在现代 C++ 中，表达式 processBox({1.0, 2.0, 3.0}) 是 processBox(Box{1.0, 2.0, 3.0}) 的合法简写。要禁止这种简写形式，从而强制在每次构造时显式提及 Box 类型，可以将三参数构造函数 Box(double, double, double) 标记为 explicit。

## 委托构造函数

一个类可以有多个构造函数，提供创建对象的不同方式。一个构造函数的代码可以在初始化列表中调用同一个类的另一个构造函数。这可以避免在多个构造函数中重复相同的代码。下面用 Box 类简单说明这一点：

```cpp
class Box
{
public:
    Box(double length, double width, double height);
    explicit Box(double side);   // Constructor for a cube (explicit!)
    Box() = default;             // Defaulted default constructor

    double volume();             // Function to calculate the volume of a box

private:
    double m_length{1.0};
    double m_width {1.0};
    double m_height{1.0};
};
```

第一个构造函数的实现可以如下所示：

```cpp
Box::Box(double length, double width, double height)
    : m_length{length}, m_width{width}, m_height{height}
{
    std::cout << "Box constructor 1 called." << std::endl;
}
```

第二个构造函数创建一个所有边都相等的 Box 对象，我们可以这样实现它：

```cpp
Box::Box(double side) : Box{side, side, side}
{
    std::cout << "Box constructor 2 called." << std::endl;
}
```

该构造函数只是在初始化列表中调用前面的构造函数。side 参数被用作前面构造函数参数列表中的全部三个值。这称为委托构造函数，因为它将构造工作委托给另一个构造函数。委托构造函数有助于缩短和简化构造函数代码，并使类定义更易于理解。在线下载中的 Ex12_05.cpp 包含以下示例来说明这一点：

```cpp
int main()
{
    Box box1 {2.0, 3.0, 4.0};        // An arbitrary box
    Box box2 {5.0};                  // A box that is a cube
    std::cout << "box1 volume = " << box1.volume() << std::endl;
    std::cout << "box2 volume = " << box2.volume() << std::endl;
}
```

输出如下：

```text
Box constructor 1 called.
Box constructor 1 called.
Box constructor 2 called.
box1 volume = 24
box2 volume = 125
```

从输出可以看出，创建第一个对象只调用了构造函数 1。创建第二个对象先调用构造函数 1，再调用构造函数 2。这也表明构造函数的初始化列表的执行发生在构造函数体中的代码之前。体积与你预期的一样。

你只应在构造函数的初始化列表中调用同一类的构造函数。在委托构造函数的函数体中调用同一类的构造函数是不同的。此外，你不得在委托构造函数的初始化列表中初始化成员变量。如果这样做，代码将无法编译。你可以在委托构造函数的函数体中为成员变量设置值，但在这种情况下，你应该考虑该构造函数是否真的应该实现为委托构造函数。

## 复制构造函数

假设你在 Ex12_05.cpp 的 main() 中添加以下语句：

```cpp
Box box3 {box2};
std::cout << "box3 volume = " << box3.volume() << std::endl;  // Volume = 125
```

输出显示 box3 确实具有与 box2 相同的尺寸，但没有定义参数类型为 Box 的构造函数，那么 box3 是如何创建的呢？答案是编译器提供了一个默认复制构造函数，该构造函数通过复制现有对象来创建对象。默认复制构造函数将作为参数的对象成员变量的值复制到新对象。

默认行为对于 Box 对象来说没问题，但当一个或多个成员变量是指针时，它可能会引发问题。仅仅复制指针并不会复制它所指向的内容，这意味着当通过复制构造函数创建对象时，该对象与原对象相互关联。两个对象都会包含一个指向同一内容的成员。一个简单的例子是，如果一个对象包含一个指向字符串的指针，那么复制出来的对象也会有一个指向同一字符串的成员，因此如果该字符串对一个对象进行了修改，另一个对象也会随之改变。这通常不是你想要的。在这种情况下，你必须定义复制构造函数。我们将在第 13 章和第 18 章回到是否、何时以及为何应定义复制构造函数的问题。现在，我们只关注如何实现。

### 实现复制构造函数

复制构造函数必须接受相同类类型的参数，并以适当的方式创建副本。这带来了一个你必须立刻克服的问题；如果你尝试像下面这样为 Box 类定义复制构造函数，就能清楚地看到这个问题：

```cpp
Box::Box(Box box)   // Wrong!
    : m_length{box.m_length}, m_width{box.m_width}, m_height{box.m_height}
{}
```

新对象的每个成员变量都用作为参数的对象的成员变量值初始化。在这种情形下，复制构造函数的函数体不需要任何代码。这看起来没问题，但考虑一下调用构造函数时会发生什么。参数是按值传递的，但由于参数是 Box 对象，编译器会安排调用 Box 类的复制构造函数来复制该参数。当然，这次复制构造函数调用的参数也是按值传递的，因此需要再次调用复制构造函数，依此类推。简而言之，你制造了一种会无限递归调用复制构造函数的情况。你的编译器不会允许这段代码编译。

为了避免这个问题，复制构造函数的参数必须是引用。更具体地说，它应该是 const 引用参数。对于 Box 类，形式如下：

```cpp
Box::Box(const Box& box)
    : m_length{box.m_length}, m_width{box.m_width}, m_height{box.m_height}
{}
```

既然参数不再按值传递，就避免了复制构造函数的递归调用。编译器将传递给它的对象初始化给参数 box。参数应为 const 引用，因为复制构造函数只负责创建副本；它不应修改原对象。const 引用参数允许复制 const 和非 const 对象。如果参数是 non-const 引用，构造函数就不会接受 const 对象作为参数，从而不允许复制 const 对象。由此你可以得出结论：复制的参数类型为

