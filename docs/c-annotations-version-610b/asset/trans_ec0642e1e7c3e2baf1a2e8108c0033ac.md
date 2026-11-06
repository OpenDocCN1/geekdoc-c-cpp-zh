
```cpp
{
    public:
        std::string const &name()    const;
        std::string const &address()  const;
        std::string const &phone()    const;
        size_t mass()                 const;
};
```

3.1.3 节给出的经验法则在这里同样适用：出现在关键字 `const` 左侧的内容不会被修改。对于成员函数，这应解释为“不修改自身的数据”。

实现 const 成员函数时，必须重复 const 属性：

```cpp
string const &Person::name() const
{
    return d_name;
}
```

编译器阻止类的数据成员被其某个 const 成员函数修改。因此，像

```cpp
d_name[0] = toupper(static_cast<unsigned char>(d_name[0]));
```

这样的语句如果添加到上述函数的定义中，会导致编译错误。

const 成员函数用于防止无意的数据修改。除了构造函数和析构函数（参见第 9 章）之外，只有 const 成员函数才能用于（普通 const 对象、const 对象的引用或指针）。const 对象经常作为函数的 `const &` 参数出现。在此类函数内部，只能使用该对象的 const 成员。下面是一个例子：

```cpp
void displayMass(ostream &out, Person const &person)
{
    out << person.name() << " weighs " << person.mass() << " kg.\n";
}
```

由于 person 被定义为 Person const &，函数 displayMass 不能调用例如 `person.setMass(75)`。

const 成员函数属性可用于重载成员函数。当函数通过其 const 属性进行重载时，编译器会使用与该对象的 const 限定最匹配的成员函数：

- 当对象是 `const` 对象时，只能使用 const 成员函数。
- 当对象不是 `const` 对象时，将使用非 const 成员函数，除非只有 const 成员函数可用。在这种情况下，将使用 const 成员函数。

下一个例子说明了如何选择（非）const 成员函数：

```cpp
#include <iostream>
using namespace std;

class Members
{
    public:
        Members();
        void member();
        void member() const;
};
```

```cpp
Members::Members()
{}
void Members::member()
{
    cout << "non const member\n";
}
void Members::member() const
{
    cout << "const member\n";
}
```

```cpp
int main()
{
    Members const constObject;
    Members       nonConstObject;

    constObject.member();
    nonConstObject.member();
}
/*
        Generated output:

    const member
    non const member

*/
```

作为一般设计原则：应始终为成员函数赋予 `const` 属性，除非它们确实会修改对象的数据。

### 7.6.1 匿名对象

有时使用对象是因为它们提供某种功能。这些对象仅因其功能而存在，对象本身中的任何内容都不会改变。下面的类 `Print` 提供了一种打印字符串的工具，使用可配置的前缀和后缀。部分类接口可能如下：

```cpp
class Print
{
    public:
        Print(ostream &out);
        void print(std::string const &prefix, std::string const &text,
                   std::string const &suffix) const;
};
```

这样的接口将允许我们做类似这样的事情：

```cpp
Print print(cout);
for (int idx = 0; idx != argc; ++idx)
    print.print("arg: ", argv[idx], "\n");
```

这运行得很好，但如果我们能把 `print` 的不变参数传递给 `Print` 的构造函数，就可以大大改进。这将简化 `print` 的原型（只需传递一个参数，而不是三个），并且我们可以将上述代码包装在一个期望 `Print` 对象的函数中：

```cpp
void allArgs(Print const &print, int argc, char *argv[])
{
    for (int idx = 0; idx != argc; ++idx)
        print.print(argv[idx]);
}
```

以上代码相当通用，至少相对于 `Print` 来说是这样。由于 `prefix` 和 `suffix` 不会改变，它们可以传递给构造函数，该构造函数可被赋予如下原型：

```cpp
Print(ostream &out, string const &prefix = "", string const &suffix = "");
```

现在可以按如下方式使用 `allArgs`：

```cpp
Print p1(cout, "arg: ", "\n");        // prints to cout
Print p2(cerr, "err: --", "--\n");    // prints to cerr

allArgs(p1, argc, argv);              // prints to cout
allArgs(p2, argc, argv);              // prints to cerr
```

但现在我们注意到，`p1` 和 `p2` 只在 `allArgs` 函数内部使用。此外，从 `print` 的原型可以看出，`print` 不会修改它所使用的 `Print` 对象的内部数据。

在这种情况下，实际上没有必要在使用对象之前定义对象。相反，可以使用*匿名对象*。匿名对象可用于：

- 初始化一个作为对象的 `const` 引用的函数参数；
- 如果该对象*仅*在函数调用内部使用。

这些匿名对象被视为常量，因为它们仅仅是为了将（类类型）对象的信息传递给函数而存在。它们不被视为“变量”。当然，可以使用 `const_cast` 去除 const 引用的常量性，但一旦函数返回，任何更改都会丢失。用于初始化 const 引用的这些匿名对象不应与右值引用（3.3.2 节）混淆，后者在生存期中的目的完全不同。右值引用主要存在是为了被接收它们的函数“吞下”。因此，右值引用所提供的信息比同样匿名的右值引用对象存活得更久。

当使用构造函数而未为所构造的对象提供名称时，就定义了匿名对象。下面是相应的例子：

```cpp
allArgs(Print(cout, "arg: ", "\n"), argc, argv);   // prints to cout
allArgs(Print(cerr, "err: --", "--\n"), argc, argv); // prints to cerr
```

在这种情况下，`Print` 对象被构造出来，并立即作为第一个参数传递给 `allArgs` 函数，在那里它们可以作为该函数的 `print` 参数访问。在 `allArgs` 函数执行期间，可以使用它们，但一旦函数完成，这些匿名 `Print` 对象就不再可访问。

### 7.6.2 匿名对象的微妙之处

匿名对象可用于初始化作为对象的 `const` 引用的函数参数。这些对象在调用此类函数之前创建，并在函数终止后销毁。C++ 的语法也允许我们在其他情况下使用匿名对象。考虑下面的代码片段：

```cpp
int main()
{
    // initial statements
    Print("hello", "world");
    // later statements
}
```

在这个例子中，构造了一个匿名 Print 对象，随后它立即被销毁。因此，在 'initial statements' 之后，我们的 Print 对象被构造出来。然后它再次被销毁，随后执行 'later statements'。

这个例子说明标准生存期规则不适用于匿名对象。它们的生存期限于*语句*，而不是定义它们的*块的末尾*。

普通的匿名对象至少在一个场景中有用。假设我们想在代码中放置*标记*，当程序执行到达某个点时产生一些输出。对象的构造函数可以实现为提供该标记功能，从而允许我们通过定义匿名对象而不是命名对象来在代码中放置标记。

C++ 的语法还包含另一个显著特征，如下一个例子所示：

```cpp
int main(int argc, char **argv)
{
    Print p(cout, "", "");        // 1
    allArgs(Print(p), argc, argv); // 2
}
```

在这个例子中，语句 1 中构造了一个非匿名对象 p，然后在语句 2 中用它来初始化一个匿名对象。接着，这个匿名对象又被用来初始化 allArgs 的 const 引用参数。这种使用现有对象初始化另一个对象的做法很常见，并且基于所谓*拷贝构造函数*的存在。拷贝构造函数（因为它是一个构造函数）使用现有对象的特征来初始化所创建对象的数据，从而创建一个对象。第 9 章将深入讨论拷贝构造函数，但目前只使用拷贝构造函数的概念。

在上面的例子中，使用拷贝构造函数初始化了一个匿名对象。然后这个匿名对象被用来初始化函数的一个参数。然而，当我们试图把同样的技巧（即使用现有对象初始化匿名对象）应用于普通语句时，编译器会产生错误：对象 p 不能被重定义（在下面的语句 3 中）：

```cpp
int main(int argc, char *argv[])
{
    Print p("", "");              // 1
    allArgs(Print(p), argc, argv); // 2
    Print(p);                     // 3 error!
}
```

这是否意味着，使用现有对象初始化一个用作函数参数的匿名对象是可以的，而在普通语句中不能使用现有对象初始化匿名对象？

编译器实际上为这个表面上的矛盾提供了答案。关于语句 3，编译器报告类似如下内容：

```text
error: redeclaration of 'Print p'
```
