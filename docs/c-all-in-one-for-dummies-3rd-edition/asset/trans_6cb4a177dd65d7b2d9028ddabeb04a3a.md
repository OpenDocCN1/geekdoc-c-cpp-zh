

但是，如果你改为让这些类具有关联关系（如 StaticCast 示例所示）

```cpp
class FinalType {};
class AnotherType : public FinalType {};
```

那么下面两行代码就能编译通过：

```cpp
AnotherType *orig = new AnotherType;
FinalType *f = static_cast<FinalType *>(orig);
```

不过，如果你使用的是 Code::Blocks 编译器，你会收到一条警告信息：

```text
warning: unused variable 'f' [-Wunused-variable]
```

![](img/6ba99460b0feb3585671a4612ff5fabb_483_0.png)

很多人认为 `static_cast` 没什么用，本质上和旧的 C 风格强制类型转换一模一样。事实并非如此。告诉他们错了！（不过态度要好一点。毕竟，朋友比软件重要。）这种错误的观念认为 `static_cast` 不做类型检查，而实际上它做了。`static_cast` 和 `dynamic_cast` 的区别在于，`static_cast` 在编译时进行类型检查；编译器会确保转换是合法的。而 `dynamic_cast` 在编译时也会做同样的类型检查，但在运行时，它还会做更多的检查，以确保实例确实是你正在转换的目标类型。旧的 C 风格强制类型转换则完全不做这些类型检查。

如果你只是想在浮点数和整数之间进行转换，你可以使用旧的 C 风格转换。（那是因为旧的 C 风格转换实际上是一种转换，而不是强制类型转换。）当然，你也可以使用 `static_cast` 来完成同样的工作：

```cpp
float f = static_cast<float>(x);
```

## 组织你的数据

在 C++ 诞生之前，C 语言已经有了一种类似于类的东西，叫做*结构体*。区别在于结构体只有成员变量——没有成员函数。下面是一个结构体的例子：

```cpp
struct Dimensions
{
    int height;
    int width;
    int depth;
    int weight;
    int price;
};
```

这段代码类似于一个类；如你所见，它有一些成员变量，但没有成员函数。它也没有任何访问控制（如 `public`、`private` 或 `protected`）。

但 C++ 的设计者不仅把类添加到了 C++ 中，还增强了 C++ 中的结构体。所以现在你可以在 C++ 中使用比 C 语言更强大的结构体。C++ 中结构体的主要变化是它们可以有成员函数和访问控制了。因此，我们可以像这样向 Dimensions 结构体添加内容：

```cpp
struct Dimensions
{
    private:
        int price;
    public:
        int height;
        int width;
        int depth;
        int weight;
        int GetPrice() { return price; }
};
```

然后我们可以像这样在代码中创建 Dimensions 的一个实例：

```cpp
Dimensions FlipItem;
Dimensions *SecondItem = new Dimensions;
```

嗯，这难道不有趣吗？这种 *struct* 的东西看起来可疑地像是一个类，你说呢？嗯。实际上，这个 *struct* 代码就是一个类。它们是*同一个*东西。

![](img/6ba99460b0feb3585671a4612ff5fabb_484_0.png)

当 C++ 语言的伟大创始人（比雅尼·斯特劳斯特鲁普）创造 C++ 时，他将结构体增强到了类和结构体*完全相同*的程度，只有一个例外。结构体的成员默认是 `public` 的。而类的成员默认是 `private` 的。

这很好。但为什么要使用结构体呢？实际上，这并不重要。如今大多数 C++ 程序员甚至从不碰结构体。

![](img/6ba99460b0feb3585671a4612ff5fabb_484_1.png)

不过，一些 C++ 程序员使用一种关于结构体的特殊约定。如果一个类只有公有成员变量而没有成员函数，那么就把它做成结构体。

换句话说，程序员将结构体用于那些本身就是较小数据类型集合的简单数据类型。（也就是说，他们按照 C 语言最初的方式使用结构体。）这实际上是一个相当不错的主意。在接下来的章节中，我们会告诉你一些关于这些数据结构问题的内容。（而且，无论如何，在 C++ 中保留结构体是一个好主意，因为很多人最初是把 C 应用程序用 C++ 编译器重新编译的。C++ 编译器能够处理结构体，这是件好事。）

![](img/6ba99460b0feb3585671a4612ff5fabb_485_0.png)

如果你熟悉 C 语言，正在学习 C++，你可能会想知道：在 C++ 中声明一个结构体类型的变量时，只需要给出结构体的名字。你不再需要在声明中写 `struct` 这个关键字。因此下面这行代码在 C++ 中仍然可以编译：

```cpp
struct Dimensions another;
```

但你真正需要的只是：

```cpp
Dimensions another;
```

### 作为组件数据类型使用的结构体

结构体的一种常见用途是作为由底层数据类型组成的高级数据类型。例如，许多处理图形的操作系统都会包含一些需要 `Point` 结构体的库。通常，`Point` 结构体只是将 X 坐标和 Y 坐标组合在一个包中。

你可以像这样声明这样一个结构体：

```cpp
struct Point
{
    int x;
    int y;
};
```

然后，当你需要调用一个需要这种结构体的函数时——比如我们为这个示例编造的一个叫做 `DrawDot` 的函数——你只需声明一个 `Point` 并调用该函数，如下所示：

```cpp
Point onedot;
onedot.x = 10;
onedot.y = 15;
DrawDot(onedot);
```

`DrawDot` 函数的原型看起来像这样：

```cpp
void DrawDot(Point pt);
```

注意，该函数既不接受指向 `Point` 的指针，也不接受 `Point` 的引用。它直接获取 `Point` 本身。

如果你愿意，你可以像初始化数组一样初始化结构体的成员：

```cpp
Point seconddot = { 30, 50 };
DrawDot(seconddot);
```

### 结构体的赋值

将简单的结构体赋值给另一个结构体很容易。C++ 编译器会自动通过逐个复制成员来处理。清单 2-2 中的 Equatestruct 示例就是这一过程的实际演示。

### 清单 2-2：轻松复制结构体

```cpp
#include <iostream>

using namespace std;

struct Point3D
{
    double x;
    double y;
    double z;
};

int main()
{
    Point3D FirstPoint = { 10.5, 22.25, 30.8 };
    Point3D SecondPoint = FirstPoint;
    cout << SecondPoint.x << endl;
    cout << SecondPoint.y << endl;
    cout << SecondPoint.z << endl;
    return 0;
}
```

因为结构体几乎和类完全一样，你可以把清单 2-2 中的结构体定义改成下面的类定义，应用程序将继续以相同的方式运行：

```cpp
class Point3D
{
public:
    double x;
    double y;
    double z;
};
```

注意，在函数中，我们只是创建了一个 `Point3D` 类型的局部变量。这个变量不是指针，也不是引用。在函数结束时，我们直接返回了它。当我们调用它时，我们将返回的结构体的值复制到我们自己的变量中，先是 `MyPoint`，然后是 `OtherPoint`。

![](img/6ba99460b0feb3585671a4612ff5fabb_488_0.png)

当返回结构体（或类实例，因为它们是相同的东西）时，你可能会开始看到一些麻烦。返回结构体是否有效？是的，它确实有效，但发生的事情很复杂。当你在函数中创建一个结构体实例时，你只是创建了一个局部变量。这肯定*不是*你想要返回的东西；它会作为局部变量留在栈上。但请考虑这个调用：

```cpp
Point3D MyPoint = StartingPoint(5,2);
```

在汇编层面，`StartingPoint()` 函数接收 `MyPoint` 的地址。然后在函数结束时，同样在汇编层面，编译后的代码使用指向 `MyPoint` 的指针，将局部变量（此处称为 `start`）的内容复制到 `MyPoint` 结构体中。所以实际上并没有返回任何东西，而是复制了数据。因此，如果你的结构体包含一个指针变量（例如），你也会得到该指针变量的一个副本——也就是说，你的指针变量将指向与函数中的指针相同的东西。这可能是你想要的，也可能不是，具体取决于你的情况。所以请小心，并确保在从函数返回结构体时完全理解你在做什么！

### 命名你的空间

能够为一个变量或其他项目使用一个通用名称，而不必担心该名称会与已有的标识符冲突，这通常是一件很好的事情。例如，在某个头文件的某处，你可能会有一个名为 `Count` 的全局变量，而其他人可能想要在他或她的某个函数中创建一个名为 `Count` 的变量，该函数使用了你的全局头文件。或者你可能想要命名一个函数为 `GetData()`——但你如何确保使用你的函数的人不会包含其他人编写的、已经有一个 `GetData()` 函数的头文件呢？这会是一场 `GetData()` 函数的激烈大战，最后只有一个能幸存吗？这可不好！你能做什么来避免冲突呢？

你可以使用命名空间。*命名空间* 只是一种对标识符进行分组的方式，比如你所有的类。例如，如果你将这个组命名为 *Menagerie*，那么 *Menagerie* 就是你的命名空间。然后你可以把你的类放在里面，如 SimpleNamespace 示例所示：

```cpp
namespace Menagerie
{
    class Oxen {
    public:
```

