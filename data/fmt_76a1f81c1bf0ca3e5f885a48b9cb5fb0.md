
让我们回到我在讨论拷贝构造函数时用过的 `CMessage` 类。你可能记得它有一个成员 `message`，它是一个指向字符串的指针。现在考虑一下默认赋值运算符可能产生的影响。假设你有该类的两个实例，`motto` 和 `motto2`。你可以使用默认赋值运算符将 `motto2` 的成员设置为等于 `motto1` 的成员，如下所示：

```
motto2 = motto1; // 使用默认赋值运算符
```

对该类使用默认赋值运算符的效果与使用默认拷贝构造函数本质上相同：会导致灾难！由于每个对象都将指向字符串的指针，如果其中一个对象的字符串发生了变化，两个对象都会受到影响。还有一个问题是，当一个对象被销毁时，它的析构函数会释放字符串使用的内存，而另一个对象将留下一个可能永远不会用于其他用途的指针。你需要赋值运算符做的是将源对象的文本拷贝到目标对象拥有的内存区域。

## 修复问题

你可以通过编写自己的赋值运算符函数来修复这个问题，我假设该函数定义在类定义内部。这是一个初步的尝试，我警告你，现在这种写法对于正常运行是不够的：

```
// 针对 CMessage 对象的重载赋值运算符
CMessage& operator=(const CMessage& aMessage)
{
    // 释放第一个操作数的内存
    delete[] message;
    message = new char[strlen(aMessage.message) + 1];
    // 将第二个操作数拷贝到列表
    strncpy_s(this->message, strlen(aMessage.message) + 1, aMessage.message);
    // 返回第一个操作数的引用
    return this;
}
```

赋值看起来非常简单，但有几个细微之处需要进一步研究。注意的是，如果你从赋值运算符函数返回一个引用，可能无法立即看出为什么这样做——在赋值操作完全完成后，赋值语句右侧的对象将拷贝到左侧。具体来说，这暗示你不需要返回任何内容，但你需要更深入地考虑该运算符可能如何被使用。

你可能需要另一个赋值语句右侧的赋值操作的结果。考虑这样一条语句：

```
motto1 = motto2 = motto3;
```

赋值运算符是右结合的，因此将 `motto3` 赋值给 `motto2` 首先执行。该语句将翻译为：

```
motto1 = (motto2.operator=(motto3));
```

运算符函数调的结果位于等号右侧，因此该语句最终将变为：

```
motto1.operator=(motto2.operator=(motto3));
```

为了让这能够工作，你通常必须从 `operator=()` 函数返回某些内容。括号之间的函数调用必须返回一个可以作为另一个 `operator=()` 函数调用参数的对象。在这种情况下，返回类型为 `CMessage` 或 `CMessage&` 都可以，因此对于这来说并非强制要求引用，但你至少必须返回一个 `CMessage` 对象。

然而，考虑以下示例：

```
(motto1 = motto2) = motto3;
```

这是完全合法的代码——括号的作用是确保最左边的赋值首先执行。它翻译为语句：

```
motto1.operator=(motto2) = motto3;
```

当你将剩余的赋值操作表示为显重载函数调用时，它最终变成了：

```
motto1.operator=(motto2).operator=(motto3);
```

现在，你处于一种情况：从 `operator=()` 函数返回的对象被用于调用 `operator=()` 函数。如果返回类型只是 `CMessage`，那么这将是不合法的，因为实际返回的对象临时拷贝将是一个右值（rvalue），而编译器不允许使用右值调用成员函数。确保这能够编译并正确运行的唯一方法是返回一个引用，如果你希望允许你的类完全灵活地使用赋值运算符，类型应该是 `CMessage&`。

注意，C++ 没有对赋值运算符接受的参数或返回类型强制执行任何限制，但如果你希望你的赋值运算符函数支持正常的赋值用法，那么按照我描述的方式声明运算符是有意义的。

另一个细微之处是，每个对象已经分配了字符串内存，因此运算符函数要做的第一件事是删除分配给第一个对象的内存，并分配足够的内存来容纳第二个对象的字符串。一旦完成，就可以将第二个对象的字符串拷贝到现在由第一个对象的新内存中。

这个运算符函数仍然存在缺陷。如果你写了以下语句会怎样？

```
motto1 = motto1;
```

显然，你不会做这种愚蠢的操作，但它很容易隐藏在指针后面，如下语句所示：

```
motto1 = *pMessage;
```

如果指针 `pMessage` 指向 `motto1`，你本质上就执行了前面的赋值语句。在这种情况下，目前的运算符函数将删除 `motto1` 的内存，根据已删除的字符串长度分配一些内存。你可以通过在函数开始处检查相同的操作数来修复这个问题。

```cpp
cout << "motto2 contains - ";
motto2.ShowIt();
cout << endl;
```

```cpp
motto2 = motto1; // 使用新的赋值运算符
```

```cpp
cout << "motto2 contains - ";
motto2.ShowIt();
cout << endl;
```

```cpp
motto1.Reset(); // 将 motto1 设置为 * 不会影响 motto2
```

```cpp
cout << "motto1 now contains - ";
motto1.ShowIt();
cout << endl;
```

```cpp
cout << "motto2 still contains - ";
motto2.ShowIt();
cout << endl;
```

```cpp
return 0;
}
```

你从输出中看到一切工作得完全符合预期，两个对象的消息之间没有任何关联：

```
motto2 contains -
Default message
motto2 contains -
The devil takes care of his own
motto1 now contains -
************************************
motto2 still contains -
The devil takes care of his own
Destructor called.
Destructor called.
```

所以你又得到了另一条黄金法则：如果你为类的数据成员分配了动态内存，请务必实现赋值运算符函数。

在实现了赋值运算符后，像 `+=` 这样的操作会怎样呢？嗯，除非你实现了它们，否则它们无法工作。对于你想要与类对象使用的每种 `op=` 形式，你都需要编写另一个运算符函数。

## 重载加法运算符

让我们看看为我们的 `CBox` 类重载加法运算符。这很有趣，因为涉及创建并返回一个新对象。新对象将是作为操作数的两个 `CBox` 对象的和（取决于你对“和”的定义）。

那么我们希望两个盒子的和代表什么呢？嗯，有很多种合理的可能性，但我们在这里将保持简单。我们将两个 `CBox` 对象的和定义为一个 `CBox` 对象，其足够大，可以容纳另外两个堆叠在一起的盒子。理想情况下，你希望通过组合它们的最短维度来连接盒子。你可以通过确保箱子的长度始终大于等于宽度，且箱子的宽度大于等于高度来实现。然后你可以让新对象拥有一个 `m_Length` 成员，其值为相加对象中 `m_Length` 成员的较大者，`m_Width` 成员也以类似的方式得出。`m_Height` 成员将是操作对象 `m_Height` 成员之和，以便结果性 `CBox` 对象能够容纳另外两个 `CBox` 对象。这并不一定是其中两个 `CBox` 对象可以绕高度轴旋转以实现更高效组合的最优方案，但对于我们的目的来说足够了。通过修改构造函数，我们还将使 `CBox` 对象的长度、宽度和高度按降序排列。

我们版本的盒子加法在图示上更容易解释，因此在图 8-4 中所示。

![](img/382e3fc55bbc8265676aa869d85a0e73_401_0.png)

图 8-4

## 运算符重载 | 36

由于它需要访问 `CBox` 对象的私有成员，`operator+()` 函数将是类的成员。类内部的函数声明如下：

```cpp
CBox operator+(const CBox& aBox) const; // 相加两个 CBox 对象的函数
```

你将参数定义为引用，以避免在调用函数时对参数进行不必要的拷贝，并将其变为 `const` 引用，因为函数没有修改参数。如果你不将参数声明为 `const`，编译器将不允许将 `const` 对象传递给函数，`+` 的右操作数不能是 `const CBox` 对象。你还将函数声明为 `const`，因为它不会改变被调用的对象。如果不这样做，`+` 的左操作数不能是 `const` 对象。

你可以这样定义该函数：

```cpp
// 添加两个 CBox 对象
CBox::operator+(const CBox& aBox) const {
  // 新对象具有较大的长度、宽度和高度之和
  return CBox(m_Length > aBox.m_Length ? m_Length : aBox.m_Length,
              m_Width > aBox.m_Width ? m_Width : aBox.m_Width,
              m_Height + aBox.m_Height);
}
```

你从当前对象（`this`）和作为参数传递的 `aBox` 对象构造一个 `CBox` 对象。记住，这个过程会创建一个局部 `CBox` 对象的副本并将其传递给调用函数，而局部对象在从函数返回时被丢弃。

## 练习我们的加法运算符

你将在此示例中看到 `CBox` 类中重载的运算符是如何工作的：

```cpp
// 06.cpp
#include <iostream>
#include <utility>
using std::cout;
using std::endl;

namespace rel_ops;

class CBox {
public:
    // 构造函数定义
    explicit CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0) : m_Height(hv) {
        m_Length = max(lv, wv);
        m_Width = min(lv, wv);
    }

    // 长度大于等于宽度
    // 计算盒子体积的函数
    double Volume() const {
      return m_Length * m_Width * m_Height;
    }

    // 比较 CBox 对象的“小于”运算符
    bool operator<(const CBox& aBox) const {
      return this->Volume() < aBox.Volume();
    }

    // 与常量比较 CBox 体积的“小于”运算符
    bool operator<(double value) const {
      return this->Volume() < value;
    }

    // 与常量比较 CBox 对象的“大于”函数
    bool operator>(double value) const {
      return this->Volume() > value;
    }

    // 等等运算符
    bool operator==(const CBox& aBox) const {
      return this->Volume() == aBox.Volume();
    }

    // 添加两个 CBox 对象的函数
    CBox operator+(const CBox& aBox) const {
      // 新对象具有较大的长度、宽度和高度之和
      return CBox(m_Length > aBox.m_Length ? m_Length : aBox.m_Length,
                  m_Width > aBox.m_Width ? m_Width : aBox.m_Width,
                  m_Height + aBox.m_Height);
    }

    // 显示盒子尺寸的函数
    void ShowBox() const {
      cout << m_Length << " * " << m_Width << " * " << m_Height << endl;
    }

private:
    double m_Length; // 英制盒子长度
    double m_Width;  // 英制盒子宽度
    double m_Height; // 英制盒子高度
};

// 与常量比较 CBox 对象的
inline bool operator>(double value, const CBox& aBox) {
    return value > aBox.Volume();
}

int main() {
    CBox smallBox(4.0, 2.0, 1.0);
    CBox mediumBox(10.0, 4.0, 2.0);
    CBox aBox;
    CBox bBox;

    cout << "*smallBox dimensions are: ";
    smallBox.ShowBox();

    cout << "*mediumBox dimensions are: ";
    mediumBox.ShowBox();

    aBox = smallBox + mediumBox;
    cout << "*aBox = smallBox + mediumBox. Dimensions are: ";
    aBox.ShowBox();

    bBox = aBox + smallBox + mediumBox;
    cout << "*bBox = aBox + smallBox + mediumBox. Dimensions are: ";
    bBox.ShowBox();

    return 0;
}
```

在本章接下来的几页中你会遇到 `CBox` 类的定义，请注意你将回到书中的此处。

## 工作原理

在这个示例中，我稍微修改了 `CBox` 类的成员。我删除了析构函数，因为这个类不需要它，并且修改了构造函数以确保 `m_Length`、`m_Width` 和 `m_Height` 按数值降序排列。这使用了 C++ 库中的 `max()` 和 `min()` 函数。我还添加了 `ShowBox()` 函数来输出对象的尺寸。我们可以用此验证我们的重载加法操作是否正常工作。

该程序的输出为：

```
smallBox dimensions are 4 2 1
mediumBox dimensions are 10 4 2
aBox = smallBox + mediumBox. Dimensions are 10 4 3
bBox = aBox + smallBox + mediumBox. Dimensions are 10 6 4
```

这似乎与我们定义的 `CBox` 对象概念一致，正如你所见，该函数也适用于表达式中的多次加法。对于 `bBox` 的计算，重载的加法运算符被调用了两次。结果显示这并非最优方案。

你可以将加法操作实现为友函数。其原型如下：

```cpp
friend CBox operator+(const CBox aBox, const CBox bBox);
```

产生结果的过程相同，只需使用直接成员选择运算符获取两个参数的成员即可。

## 重载自增减运算符

我将简要介绍在类中重载自增自减运算符的机制，因为它们具有一些与其他运算符不同的特殊性质。你需要处理 `++` 和 `--` 运算符以前置和后置形式运行，其影响取决于应用于前置还是后置形式。增减运算符的前置和后置形式重载运算符是不同的。以下是它们在名为 `Length` 的类中的定义方式：

```cpp
class Length {
  private:
    double len; // 类的长度值
  public:
    Length& operator++(); // 前置增运算符
    const Length operator++(int); // 后置增运算符
    Length& operator--(); // 前置减运算符
    const Length operator--(int); // 后置减运算符

    // 类其余部分...
}
```

这个简单的类假设长度仅存储为 `double` 类型的值。你可能会比这更复杂的类，但它足以说明你如何重载这些运算符。

运算符函数的前缀和后置形式通过参数列表进行区分；对于前缀形式，没有参数；而后置形式则有一个 `int` 类型的参数。后置运算符函数中的参数仅用于将其与前缀形式区分开，并在函数实现中使用。

递增和递减运算符在操作数的值用于表达式之前进行增加或递减，因此在对象增加或递减后，你返回当前对象的引用。以下是 `Length` 类中前缀运算符 `++()` 函数的实现：

```
inline Length& Length::operator++()
{
    +(this)->len;
    return *this;
}
```

对于后置形式，操作数在其当前值用于表达式之后才进行增加。你可以通过在增加当前对象之前创建一个当前对象的拷贝，并在修改当前对象后返回该拷贝来实现。以下是为 `Length` 类实现后置 `++` 的方式：
