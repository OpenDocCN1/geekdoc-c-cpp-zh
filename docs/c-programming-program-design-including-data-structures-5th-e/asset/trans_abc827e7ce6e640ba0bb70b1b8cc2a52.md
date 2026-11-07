
- 4. 派生类可以重定义基类的 `public` 成员函数。也就是说，在派生类中，可以有一个与基类中某个函数同名、参数个数和类型均相同的成员函数。然而，这种重定义仅适用于派生类的对象，而不适用于基类的对象。
- 5. 基类的所有成员变量也是派生类的成员变量。类似地，基类的成员函数（除非被重定义）也是派生类的成员函数。（在派生类中访问基类的成员时，请记住规则 1。）

接下来的几节描述与继承相关的两个重要问题。第一个问题是在派生类中重定义基类的成员函数。在讨论这个问题时，我们还将说明如何在派生类中访问基类的 `private`（数据）成员。第二个关键的继承问题与构造函数有关。派生类的构造函数不能直接访问基类的 `private` 成员变量。因此，我们需要确保在派生类的构造函数执行时，从基类继承的 `private` 成员变量被初始化。

## 重定义（覆盖）基类的成员函数

假设有一个 `class` derivedClass 派生自 `class` baseClass。进一步假设 derivedClass 和 baseClass 都有一些成员变量。由此可知，`class` derivedClass 的成员变量是它自己的成员变量，再加上 baseClass 的成员变量。假设 baseClass 包含一个函数 print，用于输出 baseClass 的成员变量的值。现在 derivedClass 除了从 baseClass 继承的成员变量之外，还包含其他成员变量。假设你想加入一个函数，用于输出 derivedClass 的成员变量的值。你可以给这个函数取任意名字。然而，在 `class` derivedClass 中，你也可以将这个函数命名为 print（与 baseClass 使用的名称相同）。这称为重定义（或覆盖）基类的成员函数。接下来，我们借助一个示例说明如何重定义基类的成员函数。

> **注意**
>
> 要在派生类中重定义基类的 `public` 成员函数，派生类中对应的函数必须具有相同的名称、参数个数和参数类型。换句话说，在派生类中被重定义的函数必须具有相同的名称和相同的参数集合。如果基类和派生类中的对应函数名称相同但参数集合不同，那么这是派生类中的函数重载，这也是允许的。

![](img/f97f778697507bb6fdd80c5991210cba_722_0.png)

**图 12-2** 类 `rectangleType` 的 UML 类图

类 `rectangleType` 有 10 个成员。

假设类 `rectangleType` 的成员函数定义如下：

```cpp
void rectangleType::setDimension(double l, double w)
{
    if (l >= 0)
        length = l;
    else
        length = 0;

    if (w >= 0)
        width = w;
    else
        width = 0;
}

double rectangleType::getLength() const
{
    return length;
}

double rectangleType::getWidth() const
{
    return width;
}

double rectangleType::area() const
{
    return length * width;
}

double rectangleType::perimeter() const
{
    return 2 * (length + width);
}

void rectangleType::print() const
{
    cout << "Length = " << length
         << "; Width = " << width;
}

rectangleType::rectangleType(double l, double w)
{
    setDimension(l, w);
}

rectangleType::rectangleType()
{
    length = 0;
    width = 0;
}
```

现在考虑以下类 boxType 的定义，它派生自类 rectangleType：

```cpp
class boxType: public rectangleType
{
public:
    void setDimension(double l, double w, double h);
    //Function to set the length, width, and height
    //of the box.
    //Postcondition: length = l; width = w; height = h;

    double getHeight() const;
    //Function to return the height of the box.
    //Postcondition: The value of height is returned.

    double area() const;
    //Function to return the surface area of the box.
    //Postcondition: The surface area of the box is
    //              calculated and returned.

    double volume() const;
    //Function to return the volume of the box.
    //Postcondition: The volume of the box is
    //              calculated and returned.

    void print() const;
    //Function to output the length, width, and height of a box.

    boxType();
    //Default constructor
    //Postcondition: length = 0; width = 0; height = 0;

    boxType(double l, double w, double h);
    //Constructor with parameters
    //Postcondition: length = l; width = w; height = h;

private:
    double height;
};
```

图 12-3 展示了类 `boxType` 的 UML 类图以及继承层次结构。

![](img/f97f778697507bb6fdd80c5991210cba_724_0.png)

**图 12-3** 类 `boxType` 的 UML 类图以及继承层次结构

从类 `boxType` 的定义可以清楚地看出，类 `boxType` 派生自类 `rectangleType`，并且是公有继承。因此，类 `rectangleType` 的所有公有成员都是类 `boxType` 的公有成员。类 `boxType` 还覆盖（重定义）了函数 `print` 和 `area`。

一般来说，在编写派生类的成员函数定义以指定对基类的公有成员函数的调用时，我们这样做：

- 如果派生类覆盖了基类的某个公有成员函数，那么要指定对该基类公有成员函数的调用，需使用基类的名称，后跟作用域解析运算符 `::`，再后跟带有适当参数列表的函数名。
- 如果派生类没有覆盖基类的某个公有成员函数，则可以通过使用函数名和适当的参数列表来指定对该公有成员函数的调用。（对于在派生类中被重载的基类成员函数，请参见下面的注释。）

![](img/f97f778697507bb6fdd80c5991210cba_724_1.png)

> **注意**
>
> 如果派生类*重载*了基类的某个 **public** 成员函数，那么在编写派生类的成员函数定义时，要指定对该（被重载的）基类成员函数的调用，你可能需要（取决于编译器）使用基类的名称，后跟作用域解析运算符 `::`，再后跟带有适当参数列表的函数名。例如，类 `boxType` 重载了类 `rectangleType` 的成员函数 `setDimension`。（参见本节后面给出的类 `boxType` 的函数 `setDimension` 的定义。）

接下来，让我们编写类 `boxType` 的成员函数 `print` 的定义。

类 `boxType` 有三个成员变量：length、width 和 height。类 `boxType` 的成员函数 `print` 输出这些成员变量的值。要编写类 `boxType` 的函数 `print` 的定义，请记住以下几点：

- 成员变量 length 和 width 是类 `rectangleType` 的私有成员，因此不能在类 `boxType` 中直接访问它们。所以，在编写类 `boxType` 的函数 `print` 的定义时，我们不能直接访问 length 和 width。
- 类 `rectangleType` 的成员变量 length 和 width 可以通过类 `rectangleType` 的公有成员函数在类 `boxType` 中访问。因此，在编写类 `boxType` 的成员函数 `print` 的定义时，我们首先调用类 `rectangleType` 的成员函数 `print` 来输出 length 和 width 的值。输出 length 和 width 的值之后，我们再输出 height 的值。

要在类 `boxType` 的成员函数 `print` 的定义中调用 `rectangleType` 的成员函数 `print`，我们必须使用以下语句：

`rectangleType::print();`

这条语句确保我们调用的是基类 `rectangleType` 的成员函数 `print`，而不是类 `boxType` 的成员函数 `print`。

类 `boxType` 的成员函数 `print` 的定义为：

```cpp
void boxType::print() const
{
    rectangleType::print();
    cout << "; Height = " << height;
}
```

让我们编写类 `boxType` 其余成员函数的定义。

