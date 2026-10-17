
```
plain
<<fancy>>
FIXED
--------------------
plainA
<<fancy***A>>
FIXED
--------------------
plainB
<<fancy***B>>
FIXED
```

在列表 `17.2 (fancytext.cpp)` 中，`Text` 充了其他类的基类。`FancyText` 和 `FixedText`。一个 `Text` 对象封装了一个 `std::string` 对象，由于该字符串对象对于 `Text` 类是私有的，客户端无法直接获取该字符串对象。客户端可以通过 `get` 方法查看封装的字符串，并使用 `append` 方法以有限的方式对其进行修改。列表 `17.2 (fancytext.cpp)` 包含了两个新关键字：

- `virtual` 关键字出现在 `Text` 类中 `get` 和 `append` 方法定义的前面。`virtual` 指定符表明 `Text` 类的设计者意图让派生类能够自定义 `get` 和 `append` 方法的行为。

- `override` 关键字出现在 `Fancy` 类中 `get` 和 `append` 方法定义的末尾，以及 `FixedText` 类中 `append` 方法定义的末尾。这意味着这些方法的具体行为在某些方面与它们在 `Text` 类中的实现有所不同。`FixedText` 类仅重写了 `append` 方法；它在不作修改的情况下继承了 `get` 方法。

考虑 `FancyText::get` 方法：

```cpp
class FancyText : public Text {
public:
    //
    string get() const override {
        return left_bracket + Text::get() + right_bracket;
    }
}
```

`FancyText` 类更改了 `get` 方法。我们说 `Fancy` 类重写了它的 `get` 方法。`override` 关键字强调 `FancyText` 中 `get` 方法的类意图执行某些与 `Text` `get` 方法中的代码不同的操作。在这种情况下，`FancyText::get` 方法通过拼接三个字符串来构建一个字符串：第一个字符串是前缀括号字符串，第二个是封装的字符串，第三个是尾部括号字符串。注意第二个字符串是通过表达式获得的：

```
Text::get()
```

这调用了基类版本的 `get` 方法。我们说 `FancyText::get` 方法将其部分工作委托给了基类版本 `Text::get`。注意语句

```cpp
return left_bracket + text + right_bracket; // 非法
```

该语句是非合法的，因为 `text` 是基类的私有成员。类的 `private` 不可访问。派生类没有特殊特权。为了执行委托，我们使用 `Text::get()` 而不是简单的 `get()`；不带限定的表达式 `get()` 等同于 `this->get`，它会调用 `FancyText::get`。这意味着在 `FancyText::get` 的定义中调用 `get` 是递归调用，这并不是我们想要的。

在基类中声明的方法在派生类中自动是虚的，但 `override` 的使用使其与众不同。

`override` 是 C++11 引入语言的。在 C++11 之前，当派生类中的方法签名与其基类中的虚方法签名相同时，该方法会隐式地重写其基类版本。问题在于程序员可能意图重写派生类中的方法，但写错了签名。导致的方法重载了原始方法而不是重写它。如果程序员使用了 `override` 且签名与基类版本不匹配，编译器将报告错误。`override` 指定符为程序员显式地通信其意图提供了一种方法。

![](img/e326304bd50fbc4f7d5a64c1487eb635_471_0.png)

为了后兼容，`override` 关键字是可选的。它的存在允许编译器验证该方法确实在重写基类中的虚方法。如果没有它，程序员必须注意忠实地重现要重写的方法签名。

`override` 是一个上下文敏感的关键字，意味着它只在出现在方法头声明中时才是关键字。在其他上下文中，它的行为就像一个标识符。

`FixedText` 类没有改变 `FixedText` 对象的方法工作方式；因此，`FixedText::get` 方法没有添加任何装饰。

`FancyText::append` 方法通过在现有封装的字符串和要附加的字符串之间插入一个特殊的隔符字符串来重写 `append` 方法。类似于 `FancyText::get`，`FancyText::append` 方法将实际的拼接操作委托给其基类版本，`FancyText` 无法直接影响其文本字段。

`FixedText::append` 方法不允许封装的文本字符串被修改。`FancyText` 的构造函数需要四个参数：

```cpp
class FancyText : public Text {
public:
    //
    FancyText(const string t, const string& left,
              const string& right, const string& conn)
    : Text(t), left_bracket(left),
      right_bracket(right), connector(conn) {}
```

# 17.3 的的使用

继承是一种设计工具，它允许开发者利用现有类并产生新类，以提供增强的或不同的行为。这种增强或新的行为并不是以牺牲现有代码为代价的；也就是说，在使用继承时，程序员不需要接触基类中的任何源代码。此外，开发者可以利用代码（基类中的代码），而无需在派生类中重复它。

列表 `17.2 (fancytext.cpp)` 提供了一个完整的程序，通过简单的类展示了我们如何使用继承来增强无序文本对象的行为。

```
Listing 17.2: fancytext.cpp
#include <string>
#include <iostream>

using namespace std;

// 所有 Text 派生类的基类
class Text {
    string text;
public:
    // 从客户端提供的字符串创建 Text 对象
    Text(const string& t) : text(t) {}

    // 允许客户端查看文本字段
    virtual string get() const {
        return text;
    }

    // 将另一个字符串附加到现有文本的后面
    void append(const string& extra) {
        text += extra;
    }
};

// 为文本提供最小的装饰
class FancyText : public Text {
    string left_bracket;
    string right_bracket;
    string connector;
public:
    // 客户端提供要包装的字符串以及一些装饰
    FancyText(const string t, const string& left,
              const string& right, const string& conn)
    : Text(t), left_bracket(left),
      right_bracket(right), connector(conn) {}

    // 允许客户端查看装饰后的文本字段
    string get() const override {
        return left_bracket + Text::get() + right_bracket;
    }
```

## 17.3 继承的使用

列表 `17.2 (fancytext.cpp)` 的输出如下：

```
plain
<<fancy>>
FIXED
--------------------
plainA
<<fancy***A>>
FIXED
--------------------
plainB
<<fancy***B>>
FIXED
```

在列表 `17.2 (fancytext.cpp)` 中，`Text` 充了其他类的基类。`FancyText` 和 `FixedText`。一个 `Text` 对象封装了一个 `std::string` 对象，由于该字符串对象对于 `Text` 类是私有的，客户端无法直接获取该字符串对象。客户端可以通过 `get` 方法查看封装的字符串，并使用 `append` 方法以有限的方式对其进行修改。列表 `17.2 (fancytext.cpp)` 包含了两个新关键字：

- `virtual` 关键字出现在 `Text` 类中 `get` 和 `append` 方法定义的前面。`virtual` 指定符表明 `Text` 类的设计者意图让派生类能够自定义 `get` 和 `append` 方法的行为。

- `override` 关键字出现在 `Fancy` 类中 `get` 和 `append` 方法定义的末尾，以及 `FixedText` 类中 `append` 方法定义的末尾。这意味着这些方法的具体行为在某些方面与它们在 `Text` 类中的实现有所不同。`FixedText` 类仅重写了 `append` 方法；它在不作修改的情况下继承了 `get` 方法。

考虑 `FancyText::get` 方法：

```cpp
class FancyText : public Text {
public:
    //
    string get() const override {
        return left_bracket + Text::get() + right_bracket;
    }
}
```

`FancyText` 类更改了 `get` 方法。我们说 `Fancy` 类重写了它的 `get` 方法。`override` 关键字强调 `FancyText` 中 `get` 方法的类意图执行某些与 `Text` `get` 方法中的代码不同的操作。在这种情况下，`FancyText::get` 方法通过拼接三个字符串来构建一个字符串：第一个字符串是前缀括号字符串，第二个是封装的字符串，第三个是尾部括号字符串。注意第二个字符串是通过表达式获得的：

```
Text::get()
```

这调用了基类版本的 `get` 方法。我们说 `FancyText::get` 方法将其部分工作委托给了基类版本 `Text::get`。注意语句

```cpp
return left_bracket + text + right_bracket; // 非法
```

该语句是非合法的，因为 `text` 是基类的私有成员。类的 `private` 不可访问。派生类没有特殊特权。为了执行委托，我们使用 `Text::get()` 而不是简单的 `get()`；不带限定的表达式 `get()` 等同于 `this->get`，它会调用 `FancyText::get`。这意味着在 `FancyText::get` 的定义中调用 `get` 是递归调用，这并不是我们想要的。

在基类中声明的方法在派生类中自动是虚的，但 `override` 的使用使其与众不同。

`override` 是 C++11 引入语言的。在 C++11 之前，当派生类中的方法签名与其基类中的虚方法签名相同时，该方法会隐式地重写其基类版本。问题在于程序员可能意图重写派生类中的方法，但写错了签名。导致的方法重载了原始方法而不是重写它。如果程序员使用了 `override` 且签名与基类版本不匹配，编译器将报告错误。`override` 指定符为程序员显式地通信其意图提供了一种方法。

![](img/e326304bd50fbc4f7d5a64c1487eb635_471_0.png)

为了后兼容，`override` 关键字是可选的。它的存在允许编译器验证该方法确实在重写基类中的虚方法。如果没有它，程序员必须注意忠实地重现要重写的方法签名。

`override` 是一个上下文敏感的关键字，意味着它只在出现在方法头声明中时才是关键字。在其他上下文中，它的行为就像一个标识符。

`FixedText` 类没有改变 `FixedText` 对象的方法工作方式；因此，`FixedText::get` 方法没有添加任何装饰。

`FancyText::append` 方法通过在现有封装的字符串和要附加的字符串之间插入一个特殊的隔符字符串来重写 `append` 方法。类似于 `FancyText::get`，`FancyText::append` 方法将实际的拼接操作委托给其基类版本，`FancyText` 无法直接影响其文本字段。

`FixedText::append` 方法不允许封装的文本字符串被修改。`FancyText` 的构造函数需要四个参数：

```cpp
class FancyText : public Text {
public:
    //
    FancyText(const string t, const string& left,
              const string& right, const string& conn)
    : Text(t), left_bracket(left),
      right_bracket(right), connector(conn) {}
```

| t1 | t2 |

|---|---|

| 文本: 普通 | 文本: fancy |

| | 左括号: << |

| | 右括号: >> |

| | 连接符: : |

> 赋值前

# t1 = t2;

| t1 | t2 |

|---|---|

| 文本: fancy | 文本: fancy |

| | 左括号: << |

| | 右括号: >> |

| | 连接符: : |

> 赋值后

图 17.1：将派生类赋值给基类时的对象切片

这是可能的；尽管 `FancyText` 对象是一个 `Text` 对象，我们不能说任何 `Text` 对象都是 `FancyText` 对象（它可能是一个 `FixedText` 对象，或者仅仅是一个没有任何特殊装饰的 `Text` 对象）。图 17.2 显示了尝试赋值是没有意义的，因为基类实例缺少派生类所需的信息。未能正确分配派生类实例中的所有字段会导致产生一个定义定义的对象，因为 C++ 不允许这种赋值。

`FixedText` 实例不包含任何普通 `Text` 实例所没有的额外数据，但赋值规则保持不变：

```
Text t1("ABC");
FixedText t3;
cout << t1.get() << " " << t3.get() << endl;
t1 = t3;
cout << t1.get() << " " << t3.get() << endl;
```

是合法的并产生：

```
ABC FIXED
FIXED FIXED
```

## 17.3. 继承的用法

# Text t1("plain");

FancyText t2("Fancy", "<<", ">", "::");

| t1 | | t2 |

|---|---|---|---|

| 文本 | plain | 文本 | fancy |

| | | 左括号 | << |

| | | 右括号 | >> |

| | | 连接符 | : |

赋值前

# t2 = t1;

![](img/e326304bd50fbc4f7d5a64c1487eb635_474_0.png)

赋值后

图 17.2：在 C++ 中，将基类实例赋值给派生类变量是不可能的且非法的

但语句

t3 = t1; // 非法

是非法的且将无法编译。

> 将派生类实例赋值给基类类型的变量是合法的。这是因为派生类实例是基类实例的一种特定。相比之下，将基类实例赋值给派生类型的变量是不合法的。这是因为这种继承关系是单向的，从派生类到其基类。

`FancyText` 和 `FixedText` 类形成了一个小的类层次结构。该类层次结构中的关系可以使用统一建模语言（UML）以图形形式表示。图 17.3 显示了我们特定类层次结构的 UML 图。矩形表示一个类。`Text` 作为基类，出现在图 17.3 的顶部。派生类出现在 `Text` 之下。继承箭头从派生类指向基类。箭头代表了一种向上的流动的关系。UML 图提供的这种布局和详细程度比 C++ 源代码更简洁地传了类与类之间的关系。

©2014 Richard L. Halterman 草稿日期：2014年1月26日

## 17.4. 多态

![](img/e326304bd50fbc4f7d5a64c1487eb635_475_0.png)

图 17.3：文本类家族的统一建模语言类层次结构图

UML 是一种大型、复杂的图形语言，可用于建模软件开发过程许多方面。关于 UML 的更多信息可以访问 http://www.uml.org。

## 17.4 多态

回想图 17.3 所示列表 `17.2 (fancytext.cpp)` 中的 `Text` 类层次结构。考虑以下代码片段：

执行 `t1.get()` 生成的机器码本质是什么？编译器将此高级表达式翻译成机器语言指令，导致执行跳转到代码的其他部分。程序的执行跳转到哪里？变量 `t1` 的声明类型是 `Text`，程序的执行跳转到编译后的 `Text::get` 方法（同时 `t1` 的地址作为隐含参数传递给方法，以便编译后的代码访问 `t1` 的 `text` 字段）。

对于表达式 `t2.get()`，程序的执行跳转到 `FancyText` 编译后的 `get` 方法，并将 `t2` 的地址作为隐含参数传递。

当编译器根据对象的声明类型确定要执行哪个方法时，该过程被称为静态绑定或早期绑定。静态绑定用于所有非虚方法，以及我们目前看到的虚方法的情况。

如果我们使用指针来访问对象本身，情况就会不同。考虑以下代码：
