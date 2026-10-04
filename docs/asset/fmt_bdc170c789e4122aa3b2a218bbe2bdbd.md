
C++ 允许在类接口中初始化`static const`数据成员（见第 8 章）。C++11 标准增加了这一功能，允许在类接口中为普通数据成员定义默认初始化（这些数据成员可以是`const`类型或整型，当然，它们不能引用其他数据成员）。

这些默认初始化可以被构造函数覆盖。例如，如果`Stat`类使用一个默认值为`false`的数据成员`bool d_hasPath`，第三个构造函数（见上文）将其初始化为`true`，那么下面的方法是可能的：

```cpp
struct POD {
    int first = 4;
    double second = 13;
    std::string third("hello");
};
```

## 7.5 统一初始化 (Uniform INITIALIZATION)

在定义变量和对象时，可以立即赋予它们初始值。类对象始终通过其可用构造函数之一进行初始化。C 语言已经支持数组和结构体初始化列表，它由一对大括号括起来的常量表达式列表组成。

C++ 支持一种类似的初始化方式，称为**统一初始化**。它使用以下语法：

```
Type object(value list);
```

当使用对象列表定义对象时，每个单独的对象可以使用其自己的统一初始化。

与使用构造函数相比，统一初始化的优势在于：构造函数参数有时会导致歧义，因为构造对象可能与对象的重载函数调用运算符符发生混淆（参见第 11.11 节）。由于初始化列表只能用于简单旧数据 (POD) 类型和“感知初始化列表”的类（如`std::vector`），因此在使用初始化列表时不会出现这种歧义。

统一初始化可以用于初始化对象或变量，也可以用于在构造函数中初始化成员变量或在函数的返回语句中隐式初始化。为了简洁起见，以下是示例（类内实现）：

```cpp
class Person
{
    public:
        Person(std::string const &name, size_t mass)
        :
            d_name(name),
            d_mass(mass)
        Person copy()
        {
            return (d_name, d_mass);
        }
};
```

对象的定义可能会出现在意想不到的地方，很容易导致（人的）困惑。考虑一个函数`func`和一个非常简单的类`Fun`，这里使用了`struct`，因为在这里数据隐藏不是问题：

```cpp
void func();

struct Fun
{
    Fun(void (*f)())
    {
        std::cout << "Constructor\n";
    }
    void process()
    {
        std::cout << "process\n";
    }
};
```

假设在`main`中如下如下定义了一个`Fun`对象：

```cpp
Fun fun(func);
```

运行此程序会显示 Constructor，证实了对象`fun`被构造了。接下来我们修改这行代码，从一个匿名`Fun`对象中调用`process`：

```cpp
Fun(func).process();
```

如预期的那样，出现了 Constructor，随后是文本 process。
仅仅定义一个匿名`Fun`对象会怎样？我们这样做：

```cpp
Fun(func);
```

现在惊喜降临了。编译器报错说`Fun`缺少默认构造函数。为什么呢？在`Fun`之后立即插入一个代码块，你会得到`Fun(func)`。标识符周围的括号是可以的，并且在解析括号表达式时会被删除。在这种情况下：`(func)`等于`func`，因此我们有了`Fun(func)`：这是一个`Fun`对象的定义，它接收了这个构造函数（该构造函数没有在`Fun`的类接口中声明）。

那么为什么`Fun().process()`可以编译呢？在这种情况下我们有一个成员选择运算符，其左侧的操作数必须是类类型。对象必须存在，而`Fun(func)`代表了这一点。它不是已存在对象的名称，而是一个获取一个函数（如`func`）作为参数的构造函数。编译器创建一个匿名的`Fun`对象，该对象接收`fun`作为其参数。

显然，在`Fun(func)`中不能使用括号来创建匿名的`Fun`对象。但是，可以使用统一初始化。要定义匿名`Fun`对象，我们使用这种语法：

```cpp
Fun { func };
```

（这也可以用于立即调用它的一个成员。例如`Fun{func}.process()`）。

尽管统一初始化的语法与初始化列表的语法略有不同（后者使用赋值运算符），但如果存在支持初始化列表的构造函数，编译器仍然使用初始化列表。一个示例是：

```cpp
class Vector
{
public:
    Vector(size_t size);
    Vector(std::initializer_list<int> const &values);
};

Vector vi = {4};
```

在定义`vi`的构造函数时，调用的是初始化列表而不是期望`size_t`参数的构造函数。如果需要后者的构造函数，必须使用标准的构造函数语法。即`Vector vi(4)`。

## 7.6 默认和删除的类成员 (DEFAULTED AND DELETED CLASS MEMBERS)

初始化列表本身也是对象，可以使用另一个初始化列表来构造。然而，存储在初始化列表中的值是不可变的。一旦初始化列表被定义，其值将保持不变。

初始化列表支持一组基本的成员函数和构造函数：

- `initializer_list<Type> object;`将对象定义为空初始化列表。
- `initializer_list<Type> object { list of Type values };`将对象定义为包含`Type`值的初始化列表。
- `initializer_list<Type> object(other);`使用存储在`other`中的值初始化对象。
- `size_t size() const;`返回初始化列表中元素的数量。
- `Type const *begin() const;`返回指向初始化列表第一个元素的指针。
- `Type const *end() const;`返回指向初始化列表最后一个元素之后位置的指针。

在日常类设计中，经常会遇到两种情况：

- 提供构造函数的类必须显式定义一个默认构造函数；
- 类（例如实现流的类）不能通过拷贝该类已存在对象的值（称为*拷贝构造*，copy construction）来初始化对象，且不能将对象相互赋值。

一旦类定义了至少一个构造函数，编译器就不会自动定义它了。C++ 通过提供`= default`放宽了这一限制。指定`= default`的类会执行以下操作：

- 内置或原始类型的数据成员被初始化；
- 它的复合（类类型）成员被初始化。
- 如果该类派生自基类（参见第 13 章），则基类被初始化。

*拷贝构造函数*、重载赋值运算符和*析构函数*也可以提供平凡的实现。这些成员在第 9 章中介绍。

相反，某些情况下不应提供某些（自动提供的）成员。这通过指定`= delete`实现。使用`= default`和`= delete`的示例所示：

```cpp
class Strings
{
  public:
    Strings() = default;
    Strings(std::string const *sp, size_t size);
    Strings(Strings const &other) = delete;
};
```

## 7.7 成员函数和常量对象 (Const member functions and const objects)

`const`关键字通常用于成员函数的参数列表后面。该关键字表示成员函数不会修改对象的成员变量。这样的函数被称为常量成员函数。在`Person`类中，我们看到访问函数被声明为`const`：

```cpp
class Person {
  public:
    std::string const &name() const;
    std::string const &address() const;
    std::string const &phone() const;
    size_t mass() const;
};
```

在第 3.1.1 节给出的经验法则也适用于这里：位于`const`关键字左侧的内容不会被修改。对于成员函数，这应该被解释为“不修改自己的数据”。

在实现常量成员函数时，必须重复`const`属性：

```cpp
string const &Person::name() const {
  return d_name;
}
```

编译器防止常量成员函数修改类的数据成员。因此，像下面的语句

```cpp
d_name[0] = toupper(static_cast<unsigned char>(d_name[0]));
```

如果添加到上述函数的定义中，会导致编译错误。

**常量 (Const)**

常量成员函数用于防止意外修改数据。除了构造函数和析构函数之外（参见第 9 章），常量对象（普通、引用或指针指向）只能使用常量成员函数。

常量对象经常作为函数的常量参数出现。在这些函数内部，可以使用常量成员函数。这里有一个示例：

```cpp
void displayName(ostream &out, Person const &person) {
  out << person.name() << " " << weighs << " " << person.mass() << " " << kg.\n";
}
```

## 7.7. 常量成员函数与常量对象

由于`person`被定义为`Person const &`，因此无法调用`displayMass`函数，例如`person.setMass(75)`。
`const`成员函数属性可用于重载成员函数。当函数通过其`const`属性进行重载时，编译器会使用与对象的`const`属性匹配最紧密的成员函数：

- 当对象是常量对象时，只能使用`const`成员函数。
- 当对象不是常量对象时，将使用非`const`成员函数，除非只有`const`成员函数可用。在这种情况下，将使用`const`成员函数。

接下来的示例说明了如何选择（非）`const`成员函数：

```cpp
#include <iostream>
using namespace std;

class Members {
    public:
    Members();
    void member();
    void member() const;
};

Members::Members() {
}

void Members::member() {
    cout << "non const member\n";
}

void Members::member() const {
    cout << "const member\n";
}

int main() {
    Members const constObject;
    Members nonConstObject;
    constObject.member();
    nonConstObject.member();
}

/*
Generated output:
const member
non const member
*/
```

作为一项通的设计原则：成员函数应该始终赋予`const`属性，除非它们确实修改了对象的数据。

### 7.7.1 匿名对象

有时使用对象是因为它们提供了某些功能。这些对象仅因为其功能而存在，而对象本身没有任何内容被修改过。下面的`Print`类提供了一个打印字符串的功能，带有可配置的前缀和后缀。一个部分的类接口可以是：

```cpp
class Print {
public:
    Print(ostream & &);
    void print(std::string const &prefix, std::string const &text,
               std::string const &suffix) const;
};
```

该接口允许我们执行如下操作：

```cpp
Print print{ cout };
for (int idx = 0; idx < argc; ++idx)
    print.print("", argv[idx], "\n");
```

这种写法运行良好，但如果我们将`print`的不变参数传递给`Print`的构造函数，就可以得到极大改进。这将简化`print`的原型（需要传递一个参数而不是三个），并且我们可以将代码封装在一个期望一个`Print`对象的函数内部：

```cpp
void allArgs(Print const &print, int argc, char **argv) {
    for (int idx = 0; idx < argc; ++idx)
        print.print(argv[idx]);
}
```

上述是一个相当通用的代码，至少在`Print`方面是如此。由于前缀和后缀不会改变，可以将它们传递给构造函数，从而获取原型：

```cpp
Print(ostream &out, string const &prefix = "", string const &suffix = "");
```

现在`allArgs`可以这样使用：

```cpp
Print p1(cout, "arg": "\n"); // 打印到 cout
Print p2(cerr, "err": "---", "--\n"); // 打印到 cerr
allArgs(p1, argc, argv); // 打印到 cout
allArgs(p2, argc, argv); // 打印到 cerr
```

但现在我们注意到`p1`和`p2`只在`allArgs`函数内部使用。此外，从`print`的原型可以看出，`print`并没有修改它正在使用的`Print`对象的内部数据。

在这些情况下，实际上没有必要在使用对象之前定义它们。相反，可以使用匿名对象：

- 用于初始化一个指向对象的常量引用的函数参数；
- 如果该对象仅在函数调用内部使用。

当匿名对象作为函数`const &`参数的参数时，它们被认为仅仅为了将（类类型）对象的信息传递给这些函数而存在。因此，它们不能被修改，它们的`const`成员函数也无法被使用。当然，可以使用`const_cast`去掉引用的常量属性，但对于接收匿名对象的函数来说，这被认为是不良实践。函数返回后对匿名对象的任何修改都会丢失，因为函数调用后匿名对象就不再存在。用于初始化引用的匿名对象不应与定义为右值引用（第 3.3.2 节）的匿名对象混淆，后者在生命周期是完全临时的。因此，右值引用提供的信息主要为了被同样匿名的右值引用对象“吞掉”。

当使用构造函数但未为构造的对象提供名称时，就会创建匿名对象。这里是相应的示例：

```cpp
allArgs(Print( cout, "arg", "\n"), arg, argv); // 打印到 cout
allArgs(Print(cerr, "error: \n", argc, argv)); // 打印到 cerr
```

在这种情况下，`Print`对象被构造并立即作为第一个参数传递给`allArgs`函数，在那里它们作为函数的`print`参数被访问。当`allArgs`函数执行时它们被使用，但在函数完成后，匿名对象不再可以被访问。

### 7.7.1 匿名对象的微妙之处

匿名对象可以用于初始化指向对象的常量引用函数参数。这些对象在调用此类函数之前创建，并在函数终止后销毁。C++ 语法允许我们在其他情况下使用匿名对象。考虑以下代码片段：

```cpp
int main() {
    // 初始语句
    Print("hello", "world"); // 假设有匹配的构造函数
    // 后续语句
}
```

在这个示例中，构造了一个非匿名对象`p`。下面的示例说明了它们的生命周期限于块的结束：

```cpp
int main(int argc, char *argv[]) {
  Print p { "", "" }; // 1
  allArgs(Print(p), argc, argv); // 2
  Print(p); // 3 错误！
}
```

这意味着使用现有对象来初始化作为函数参数的匿名对象是允许的，而现有对象不能在普通语句中初始化匿名对象？

编译器实际上为我们提供了这个看似矛盾的答案。关于语句 3，编译器会报告类似的内容：

```
error: redeclaration of 'Print p'
```

这在意识到复合语句内部可以定义对象和变量时解决了问题。在复合语句内部，类型名后跟变量名是变量定义的语法形式。括号可以用于打破优先级，但这里没有需要打破的优先级，它们没有影响，会被编译器忽略。在语句 3 中，括号允许我们省略类型名和变量名之间的空格，但对编译器来说我们写的是：

```cpp
Print (p);
```

由于括号是多余的，这等同于：

```cpp
Print p;
```

从而证明了`p`的重复定义。

进一步示例：当使用内置类型定义变量时，编译器会安静地为我们移除这些多余的括号：

```cpp
double (((a))); // 虽然很异，但允许。
```

```cpp
class Person
```

```cpp
{
```
