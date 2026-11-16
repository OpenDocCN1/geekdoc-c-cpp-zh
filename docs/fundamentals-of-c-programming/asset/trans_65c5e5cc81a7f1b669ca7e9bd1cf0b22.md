

作为李斯科夫替换原则，以计算机科学家芭芭拉·李斯科夫命名。

术语 *是一个* 在继承的上下文中有特殊含义。假设我们有类 B 和从 B 派生的类 D。B 是基类，D 是派生类。由于我们可以将派生类的实例视为其基类的实例，如果我们声明一个 D 对象为

```
D d; // d is a D object
```

我们可以说 d 是一个 D（如其声明所示），我们也可以说 d 是一个 B。

## 17.2 继承机制

`std::ofstream` 类的开发者并非从零开始。`ostream` 类首先存在，开发者指定 `std::ofstream` 类的方式使得任何 `std::ofstream` 对象都被视为一种特定的 `ostream`。在本节中，我们将考察一个非常简单的示例，以说明 C++ 中类继承的机制。

假设我们有如下定义的类 B：

```
class B {
}; // Details omitted
```

要从 B 派生一个新类 D，我们使用以下语法：

```
class D: public B {
}; // Details omitted
```

这里 B 是基类，D 是派生类。B 是预先存在的类，D 是基于 B 的新类。

要了解继承的工作原理，请考虑带有更多细节的类 B 和 D：

```
class B {
// Other details omitted
public:
void f();
};
```

```
void B::f() {
std::cout << "In function 'f'\n";
}
```

```
class D: public B {
// Other details omitted
public:
void g();
};
```

```
void D::g() {
std::cout << "In function 'g'\n";
}
```

客户端代码

```
B myB;
D myD;
myB.f();
myD.f();
myD.g();
```

输出

```
In function 'f'
In function 'f'
In function 'g'
```

尽管类 D 的源代码没有显式显示名为 f 的方法的定义，但它确实有一个从类 B 继承的此类方法。

请注意，继承只在一个方向上起作用。类 D 从类 B 继承方法 f，但类 B 不能继承 D 的 g 方法。鉴于上面类 B 和 D 的定义，以下代码是非法的：

```
B myB;
myB.g();    // Illegal, a B object is NOT a D object
```

![](img/e84ad11adb18201d71595b31ce6c9eff_509_0.png)

如果我们从类 D 的定义中省略 `public` 关键字，如下所示

```cpp
class D: B {
    // Details omitted
};
```

D 对象继承的 B 的所有公共成员默认将为 `private`；例如，如果基类 B 如下所示：

```cpp
class B {
public:
    void f();
};

void B::f() {
    std::cout << "In function 'f'\n";
}
```

以下代码不合法：

```cpp
D myD;
myD.f();    // Illegal, method f now is private!
```

这意味着客户端不能将 D 对象完全视为 B 对象。这违反了李斯科夫替换原则，且 `is a` 关系不存在。

虽然这种私有继承在罕见情况下很有用，但大多数面向对象的软件设计使用公有继承。C++ 是少数支持私有继承的面向对象语言之一。

开发者可以从单个基类派生的类的数量没有限制。在以下代码中：

```
class D1: public B { /* Details omitted */ };
class D2: public B { /* Details omitted */ };
class D3: public B { /* Details omitted */ };
```

类 D1、D2 和 D3 都派生自类 B。

开发者可以从多个基类派生一个类，这个过程称为 *多重继承*。在以下代码中：

```
class B1 { /* Details omitted */ };
class B2 { /* Details omitted */ };
class D: public B1, public B2 { /* Details omitted */ };
```

这里类 D 有两个基类，B1 和 B2。如果特定函数或方法期望 B1 对象作为参数，调用者可以传递 D 对象；同样，任何需要 B2 对象的上下文都会接受 D 对象。在面向对象设计中，多重继承不如单继承（一个基类）常见。

下一节提供了一个简单示例，展示继承的工作原理。

## 17.3 继承的用途

继承是一种设计工具，允许开发者获取现有类并生成提供增强行为或不同行为的新类。增强或新的行为并非以现有代码为代价；也就是说，使用继承时，程序员不会触碰基类中的任何源代码。此外，开发者可以利用现有代码（在基类中），而无需在派生类中重复它。

我们可以演示使用继承来增强简单类的行为。清单 17.2 (text.h) 包含名为 Text 的类的声明。

### 清单 17.2: text.h

```
#ifndef TEXT_H_INCLUDED
#define TEXT_H_INCLUDED
#include <string>
// Base class for all Text derived classes
class Text {
std::string text;
public:
// Create a Text object from a client-supplied string
Text(const std::string& t);
// Allow clients to see the text field
virtual std::string get() const;
// Concatenate another string onto the
// back of the existing text
virtual void append(const std::string& extra);
};
#endif
```

Text 对象包装一个 std::string 对象，由于字符串对象对 Text 类是私有的，客户端无法直接访问字符串对象。客户端可以通过 get 方法查看字符串，并只能通过 append 方法以有限方式修改包装的字符串。请注意，两个方法 get 和 append 被标记为 virtual。virtual 关键字表明，这个 Text 类的设计者意图让从 Text 派生的类能够自定义其 get 和 append 方法的行为。

如清单 17.3 (text.cpp) 所示的 Text 方法实现没有什么特别之处。

### 清单 17.3: text.cpp

```
#include "text.h"

// Create a Text object from a client-supplied string
Text::Text(const std::string& t) : text(t) {}

// Allow clients to see the text field
std::string Text::get() const {
    return text;
}

// Concatenate another string onto the
// back of the existing text
void Text::append(const std::string& extra) {
    text += extra;
}
```

接下来我们介绍一个新类 FancyText，它派生自 Text 类。其接口出现在清单 17.4 (fancytext.h) 中。

### 清单 17.4: fancytext.h

```
#ifndef FANCYTEXT_H_INCLUDED
#define FANCYTEXT_H_INCLUDED

// Compiler needs to know specifics of the Text class in order to
// derive a new class from it
#include "text.h"

// Provides minimal decoration for the text
class FancyText: public Text {
    std::string left_bracket;
    std::string right_bracket;
    std::string connector;

public:
    // Client supplies the string to wrap plus some extra
    // decorations
    FancyText(const std::string& t, const std::string& left,
              const std::string& right, const std::string& conn);

    // Allow clients to see the decorated text field
    std::string get() const override;

// Concatenate another string onto the
// back of the existing text, inserting the connector
// string
void append(const std::string& extra) override;
};
#endif
```

请注意，get 和 append 方法的声明包含 override 说明符。这个关键字表明 FancyText 类覆盖了，或者为其基类中声明为 virtual 的方法提供了自定义行为。

清单 17.5 (fancytext.cpp) 提供了 FancyText 方法的实现。

### 清单 17.5: fancytext.cpp

```
#include "fancytext.h"

// Client supplies the string to wrap plus some extra
// decorations
FancyText::FancyText(const std::string& t, const std::string& left,
                     const std::string& right, const std::string& conn):
    Text(t), left_bracket(left),
    right_bracket(right), connector(conn) {}

// Allow clients to see the decorated text field
std::string FancyText::get() const {
    return left_bracket + Text::get() + right_bracket;
}

// Concatenate another string onto the
// back of the existing text, inserting the connector
// string
void FancyText::append(const std::string& extra) {
    Text::append(connector + extra);
}
```

虽然 Text 类的构造函数需要一个 std::string 参数，但 FancyText 的构造函数需要四个字符串参数：

```
FancyText::FancyText(const std::string& t, const std::string& left,
                     const std::string& right, const std::string& conn):
    Text(t), left_bracket(left),
    right_bracket(right), connector(conn) {}
```

构造函数体为空，因此所有初始化都在构造函数初始化列表中进行。我们想将构造函数的第一个参数 t 赋给继承的成员 text，但 text 在基类中是私有的。这意味着 FancyText 构造函数无法直接初始化它。由于其基类的构造函数知道如何处理这个参数，构造函数初始化列表（冒号和左花括号之间的部分）中的第一个表达式：

```
... Text(t) ...
```
