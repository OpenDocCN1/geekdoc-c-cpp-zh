

显式调用基类构造函数，并向其传递 t。这个基类初始化表达式必须是初始化列表中的第一项，因为 C++ 要求对象从其基类继承的部分必须在任何新部分（由派生类添加）被初始化之前先进行初始化。初始化列表中的接下来三个表达式：

```
... left_bracket(left), right_bracket(right), connector(conn) ...
```

初始化正在构建的 FancyText 对象的 left_bracket、right_bracket 和 connector 字段。构造函数的函数体为空，因为不需要其他初始化工作。

FancyText 类改变了 get 的工作方式。我们说 FancyText 类重写了其继承的 get 方法。关键字 override 强调了 FancyText 中 get 方法的代码意图与 Text 的 get 方法中的代码执行不同的操作。在这种情况下，FancyText::get 方法通过连接三个字符串来构建一个字符串结果：第一个字符串是前括号字符串，第二个是包装字符串，第三个字符串是后括号字符串。请注意，第二个字符串是通过表达式获得的：

```
Text::get()
```

这调用了 get 方法的基类版本。我们说 FancyText::get 方法将部分工作委托给基类版本 Text::get。请注意，语句

```
return left_bracket + text + right_bracket; // Illegal
```

将是非法的，因为 text 是基类私有的。成员说明符 private 意味着类外不可访问，绝对不可访问。派生类在这方面没有特殊权限。为了执行委托，我们必须使用 Text::get() 而不是简单地使用 get()；非限定表达式 get() 等同于 this->get，它调用 FancyText::get。这意味着在 FancyText::get 的定义中调用非限定的 get 是一个递归调用，这不是我们想要的。

在基类中声明为 virtual 的方法在其派生类中自动为 virtual。你可以在派生类中重复 virtual 说明符，但使用 override 会使其变得多余。

![](img/e84ad11adb18201d71595b31ce6c9eff_513_0.png)

override 关键字是在 C++11 中添加到语言的。在 C++11 之前，当派生类中的方法与其基类中的虚拟方法具有相同的签名时，该方法会隐式重写其基类版本。问题是，程序员可能打算在派生类中重写一个方法，但签名写错了。结果方法重载了原始方法，而不是重写它。如果程序员使用 override 说明符并使用与基类版本不匹配的签名，编译器将报告错误。override 说明符为程序员提供了一种明确传达其意图的方式。

为了向后兼容性，override 关键字是可选的。它的存在使编译器能够验证该方法是否实际上正在重写基类中的虚拟方法。如果没有它，程序员必须小心忠实地复制要重写的方法的签名。

override 关键字是一个上下文敏感关键字，这意味着它只有在出现在方法头声明中时才是关键字。在其他上下文中，它的行为类似于标识符。

FancyText::append 方法通过在现有包装文本字符串和要追加的字符串之间插入一个特殊分隔符字符串来重写继承的 append 方法。与 FancyText::get 类似，FancyText::append 方法通过调用 Text::append 将实际的连接操作委托给其基类。同样，这是因为 FancyText 类中的代码无法直接影响其 text 字段。

FixedText 类在清单 17.6（fixedtext.h）和清单 17.7（fixedtext.cpp）中声明和定义，是另一个派生自 Text 的类。

```cpp
#ifndef FIXEDTEXT_H_INCLUDED
#define FIXEDTEXT_H_INCLUDED

// Compiler needs to know specifics of the Text class in order to
// derive a new class from it
#include "text.h"

// The text is always the word FIXED
class FixedText: public Text {
public:
    // Client does not provide a string argument; the
    // wrapped text is always "FIXED"
    FixedText();

    // Nothing may be appended to a FixedText object
    void append(const std::string&) override;
};

#endif
```

FixedText 类比 FancyText 类简单一些。它不添加字段，也不重写 get 方法。其构造函数不接受参数，因为客户端不得确定包装字符串的内容——text 字段始终是单词 FIXED。它从 Text 类继承 text 字段和 get 方法（原样继承）。

```cpp
#include "fixedtext.h"

// Client does not provide a string argument; the
// wrapped text is always "FIXED"
FixedText::FixedText(): Text("FIXED") {}

// Nothing may be appended to a FixedText object
void FixedText::append(const std::string&) {
    // Disallow concatenation
}
```

FixedText 构造函数实现调用基类构造函数，将字符串 "FIXED" 赋值给其继承的 text 字段。get 方法不需要自定义。自定义的 append 方法不执行任何操作，因为客户端不允许添加任何额外文本。

清单 17.8（testtext.cpp）测试了这些类。

## 清单 17.8: testtext.cpp

```cpp
#include <iostream>
#include "text.h"
#include "fancytext.h"
#include "FixedText.h"

int main() {
    Text t1("plain");
    FancyText t2("fancy", "<<", ">>", "***");
    FixedText t3;
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
    std::cout << "-----------------------------------\n";
    t1.append("A");
    t2.append("A");
    t3.append("A");
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
    std::cout << "-----------------------------------\n";
    t1.append("B");
    t2.append("B");
    t3.append("B");
    std::cout << t1.get() << " ' \n";
    std::cout << t2.get() << " ' \n";
    std::cout << t3.get() << " ' \n";
}
```

清单 17.8（testtext.cpp）的输出是

```
plain
<<fancy>>
FIXED
--------------------------------
plainA
<fancy***A>
FIXED
--------------------------------
plainAB
<fancy***A***+B>
FIXED
```

鉴于在清单 17.2（text.h）和清单 17.5（fancytext.cpp）中声明的 Text 和 FancyText 类，以下客户端代码是合法的：

```
Text t1("ABC");
FancyText t2("XYZ", "[", "]", ":=");
std::cout << t1.get() << " " << t2.get() << " \n";
t1 = t2;
std::cout << t1.get() << " " << t2.get() << " \n";
```

由于 t2 的声明类型是 FancyText，凭借继承，t2 也是一个 Text 对象。上述代码片段打印

## 图 17.1 将派生类实例赋值给基类变量时的对象切割

```
Text t1("plain");
FancyText t2("Fancy", "<<", ">>", "::");
```

![](img/e84ad11adb18201d71595b31ce6c9eff_516_0.png)

```
t1 = t2;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_516_1.png)

```
ABC <<XYZ>>
XYZ <<XYZ>>
```

请注意，赋值

```
t1 = t2;
```

仅将 FancyText 对象与 Text 对象共有的字段复制到对象 t1 中；即 text 字段。由于 t1 是一个普通 Text 对象，它不具有能够存储 FancyText 对象中包含的额外数据的 left_bracket、right_bracket 和 connector 字段。将派生类数据丢失时赋值给基类实例的过程称为对象切割。无法放入基类实例的部分将被“切割”掉。图 17.1 说明了对象切割。

请注意，反向赋值：

```
t2 = t1; // Illegal
```

是不可能的；尽管任何 FancyText 对象都是 Text 对象，但我们不能说任何 Text 对象都是 FancyText 对象（它可能是 FixedText 对象，或者只是没有任何特殊装饰的 Text 对象）。图 17.2 显示，这种尝试的赋值将是无意义的，因为基类实例缺少派生类实例所需的信息。未能正确分配所有

