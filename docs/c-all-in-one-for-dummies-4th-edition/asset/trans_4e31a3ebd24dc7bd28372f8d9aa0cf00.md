
```cpp
class Prince : public King {
public:
    string School;
};

void KingInfo(King *inst) {
    cout << "=========" << endl;
    cout << inst->MyName() << endl;
    Prince *asPrince = dynamic_cast<Prince *>(inst);
    if (asPrince != 0)
    {
        cout << asPrince->School << endl;
    }
}

int main() {
    Prince George;
    George.MyName() = "George I";
    George.School = "School of the Kings";
    KingInfo(&George);
    King Henry;
    Henry.MyName() = "Henry II";
    KingInfo(&Henry);
    return 0;
}
```

运行这段代码时，看到的输出如下：

```
=========
George I
School of the Kings
=========
Henry II
```

这段代码中有一些奇怪之处。从 `main()` 开始，代码调用 `KingInfo()`，先向它传递 George（一个 Prince 实例，派生自 King）的地址，然后传递 Henry（一个 King 实例）的地址。

`KingInfo()` 函数首先使用 `MyName()` 函数打印由于继承而两者共有的信息，并打印得到的名称。然后就是重要部分：动态转换。为了执行动态转换，代码调用 `dynamic_cast`，并将 `inst`（其类型可以是 `King` 或 `Prince`）保存到一个名为 `asPrince` 的指针变量中。注意 `dynamic_cast` 的语法。它看起来像模板，因为你在尖括号中包含一个类型。然后，把要转换的变量放在圆括号中（本例中是 inst）。

如果动态转换成功，它会返回一个指针，你可以将其保存为尖括号内的类型。否则，动态转换返回 0。调用 `dynamic_cast` 后，代码将结果与 0 进行比较。如果结果不为 0，说明动态转换成功，这意味着 inst 是 Prince 类型。然后，在 if 块中，代码获取并打印 School 成员，该成员属于 Prince，而不是 King。

注意清单 2-2 中 King 类的独特设计。为了让 dynamic_cast 正常工作，涉及的基类必须至少有一个虚函数。因此，基类——以及它的每个派生类——都有一个虚表（这也是 dynamic_cast 正常工作所需要的）。此外，当你没有提供虚析构函数时，Code::Blocks 编译器会给出警告消息：

```
warning: 'class King' has virtual functions but non-virtual
destructor
```

因此，示例中也包含了一个虚析构函数。还要注意，这个类采用了良好的设计：将 CrownName 保持为私有，并为它提供一个访问器函数 MyName()。

![](img/128ab511de4e7360e167e3b15cdd5dd0_545_0.png)

你不需要像这里展示的那样在类中使用引用，才能让 dynamic_cast 正常工作。但你确实需要至少一个虚函数。

老式直接转换和 dynamic_cast 的根本区别在于：编译器会在编译期生成自动执行老式转换的代码，而不管该转换是否有效。也就是说，这种转换是硬编码的。但 dynamic_cast 会在运行时测试类型。动态转换是否成功取决于对象的类型。

使用动态转换时，你可以转换指针或引用。前面清单 2-2 中展示的 KingInfo() 函数使用的是指针。下面是一个使用引用的修改版本：

```
void KingInfoAsReference(King &inst) {
    cout << "===========" << endl;
    cout << inst.MyName() << endl;
    try {
        Prince &asPrince = dynamic_cast<Prince &>(inst);
        cout << asPrince.School << endl;
    } catch (...) { }
}
```

要让这个版本正常工作，你必须使用异常处理程序（这是一种处理异常情况的方式；有关异常处理程序的更多信息，请参阅本迷你书第 3 章）。使用异常处理程序的原因是：对于指针，你可以简单地将结果与 0 比较。但对于引用，不存在空引用或 0 引用这样的东西。引用必须有效，否则会得到运行时错误。在 C++ 中，捕获失败情况的方法是输入单词 try，后面跟上放在花括号中、尝试完成工作的代码。接着是单词 catch 和一组包含三个句点的圆括号。再之后，放入花括号——以及可能想要运行的任何代码——以防前面的代码没有成功。

这段代码在 catch 块中不做任何事情，因为即使调用失败，应用程序也会继续工作——只是输出中缺少学校名称。C++ 要求所有 try 块都与 catch 块匹配，因此即使 catch 块不做任何事情，也必须包含它。

### 使用 static_cast 进行静态转换

ANSI C++ 标准包含一种不进行类型检查的特殊转换。如果你必须在没有 dynamic_cast 帮助的情况下直接转换，应选择 static_cast，而不是老式 C 风格转换。

当你想进行静态转换时，调用 static_cast，后面跟上包含目标类型的尖括号。然后，将要转换的项放在圆括号中，如下所示：

```
FinalType *f = static_cast<FinalType *>(orig);
```

使用 static_cast 的优点是它会在编译期进行一些类型检查，而老式 C 风格转换不会。编译器只允许你在相关对象之间进行 static_cast。你可以从一个类的实例 static_cast 到派生类或基类的实例。但如果两个类不相关，就会得到编译器错误。例如，假设你有下面两行代码：

```
class FinalType {};
class AnotherType {};
```

它们是不相关的类。然后，如果你有下面这些代码行：

```
AnotherType *orig = new AnotherType;
FinalType *f = static_cast<FinalType *>(orig);
```

```cpp
#include <iostream>

using namespace std;

void PrintIt(int *out) {
    cout << "The value is: " << *out << endl;
}

int main() {
    volatile int X = 20;
    const int Y = 30;

    PrintIt(const_cast<int*>(&X));
    PrintIt(const_cast<int*>(&Y));
    return 0;
}
```

在第一种情况下，如果你尝试 PrintIt(&X)，编译时会看到错误：invalid conversion from 'volatile int*' to 'int*'。同样，在第二种情况下，PrintIt(&Y) 会产生错误消息：invalid conversion from 'const int*' to 'int*'。当然，X 和 Y 的属性都没有被移除；你只是去掉了 volatile 或 const 属性，以便将值发送给 PrintIt()。

## 组织你的数据

在 C++ 诞生之前，C 有一种类似于类的东西，称为结构体。区别在于结构体只有属性——没有方法。下面是一个结构体的示例：

```cpp
struct Dimensions {
    int height;
    int width;
    int depth;
    int weight;
    int price;
};
```

这段代码类似于一个类；如你所见，它有一些属性，但没有方法。它也没有任何访问控制（例如 public、private 或 protected）。

但 C++ 的设计者不仅为 C++ 添加了类，还增强了 C++ 中的结构体。因此，现在你在 C++ 中可以比在 C 中更强大地使用结构体。C++ 中结构体的主要变化是它们可以有方法和访问控制。因此，你可以像下面这样扩展 `Dimensions` 结构体（使 `struct` 和 `class` 等价）：

```cpp
struct Dimensions {
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

然后在代码中像这样创建 `Dimensions` 的实例：

```cpp
Dimensions FirstItem;
Dimensions *SecondItem = new Dimensions;
```

> **记住**
> 
> 当 C++ 语言的伟大创始人（Bjarne Stroustrup）创建 C++ 时，他对结构体进行了增强，以至于类和结构体变得*完全相同*，只有一个例外。结构体的成员默认是 public。然而，类的成员默认是 private。由于差异如此之小，如今大多数 C++ 程序员甚至从不接触结构体，除非是为了创建一个只包含公有属性的对象。

换句话说，程序员使用 `struct` 来表示简单数据类型，这些类型是较小数据类型的集合。（也就是说，他们使用 `struct` 的方式与 C 最初使用它们的方式相同。）接下来的小节将介绍其中一些数据结构问题。

> **技术细节**
> 
> 如果你熟悉 C 并且刚开始学习 C++，你可能有兴趣知道：当声明一个结构体类型的变量时，在 C++ 中只需要给出结构体的名称。声明中不再需要单词 `struct`。因此，下面这一行在 C++ 中仍然可以编译：

```cpp
struct Dimensions another;
```

但你真正需要的只是：

```cpp
Dimensions another;
```

