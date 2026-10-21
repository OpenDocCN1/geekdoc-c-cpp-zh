

- gName: global
- tName: tls
- lName: local
main() later:
- gName: thread1 name
- tName: thread1 name
- lName: thread1 name
foo() begin:
- gName: thread1 name
- tName: tls
- lName: local
foo() end:
- gName: thread2 name
- tName: thread2 name
- lName: thread2 name
main() end:
- gName: thread2 name
- tName: thread1 name
- lName: thread1 name

## 3.5 Afternotes

内联变量由 David Krauss 在 http://wg21.link/n4147 中提出动机，并首次由 Hal Finkel 和 Richard Smith 在 http://wg21.link/n4424 中提出。最终被接受的措辞由 Hal Finkel 和 Richard Smith 在 http://wg21.link/p0386r2 中制定。

此页 intentionally left blank

## Chapter 4

## Aggregate Extensions

C++ 有不同的方法和规则来初始化对象。其中一种方法称为 *aggregate initialization*，它描述了聚合体的初始化。¹ 如 C 中引入的那样，你必须使用大括号来传递多个初始化值：

```
struct Data {
    std::string name;
    double value;
};
```

```
Data x = {"test1", 6.778};
```

自 C++11 起，你不再需要等号：

```
Data x{"test1", 6.778};
```

自 C++17 起，聚合体可以有基类，这意味着对于派生自其他类/结构的结构，列表初始化是允许的：

```
struct MoreData : Data {
    bool done;
};
```

```
MoreData y{{"test1", 6.778}, false};
```

正如你所见，聚合初始化现在可用于向基类的成员传递初始值。基类成员被视为子聚合体，这意味着你可以使用嵌套大括号来初始化这些值。

然而，你也可以甚至跳过大括号：

```
MoreData y{"test1", 6.778, false};
```

这遵循初始化嵌套聚合体的通用规则，其中你根据基结构/类和成员的顺序使用初始值。

> ¹ 聚合体要么是数组，要么是简单的 C 风格类，该类没有用户提供的构造函数，没有私有或受保护的非静态数据成员，没有虚函数，并且在 C++17 之前，没有基类。

## 4.1 Motivation for Extended Aggregate Initialization

如果没有此功能，从另一种类型派生结构会禁用聚合初始化，这意味着你必须定义一个构造函数：

```
struct Cpp14Data : Data {
    bool done;
    Cpp14Data (const std::string& s, double d, bool b)
        : Data{s,d}, done{b} {
    }
};
```

```
Cpp14Data y{"test1", 6.778, false};
```

现在我们可以在不声明任何构造函数的情況下获得此能力。该功能使用嵌套大括号的语法，如果至少传递一个值，则可以省略：

```
MoreData x{{"test1", 6.778}, false};  // OK since C++17
MoreData y{"test1", 6.778, false};    // OK
```

请注意，因为现在这是一个聚合体，所以其他初始化也是可能的：

```
MoreData u;      // OOPS: value/done are uninitialized
MoreData z{};    // OK: value/done have values 0/false
```

如果这太危险，请在可能的情况下使用默认成员初始化器：

```
struct Data {
    std::string name;
    double value{0.0};
};
```

```
struct Cpp14Data : Data {
    bool done{false};
};
```

或者，继续提供构造函数。

## 4.2 Using Extended Aggregate Initialization

聚合初始化的一个典型应用是能够初始化由类派生的 C 风格结构的成员，以添加额外的成员或操作。例如：

```
struct Data {
    const char* name;
    double value;
};
```

```
struct CppData : Data {
    bool critical;
```

```
void print() const {
    std::cout << '[' << name << ',' << value << "]\n";
}
```

```
CppData y{{"test1", 6.778}, false};
y.print();
```

这里，内部大括号中的参数传递给基类型 Data。

请注意，你可以跳过初始值。在这种情况下，元素是从默认成员初始化器初始化的，或者它们是从 {} 复制初始化的（通常会得到元素类型的默认构造值，或者如果类型是基本数据类型，则为 0、false 或 nullptr）。例如：

```
CppData x1{};            // zero-initialize all elements
CppData x2{{"msg"}};    // same as {{"msg",0.0},false}
CppData x3{{}, true};    // same as {{nullptr,0.0},true}
CppData x4;              // values of fundamental types are unspecified
```

注意使用空大括号和完全不使用大括号之间的区别：

- x1 的定义初始化了所有成员，因此字符指针 name 由 nullptr 初始化，双精度值 value 由 0.0 初始化，而布尔标志由 false 初始化。
- x4 的定义没有初始化任何成员。所有成员都有未指定的值。

你也可以从非聚合类派生聚合体。例如：

```
struct MyString : std::string {
    void print() const {
        if (empty()) {
            std::cout << "<undefined>\n";
        }
        else {
            std::cout << c_str() << '\n';
        }
    }
};
```

```
MyString x{"hello"};
MyString y{"world"};
```

请注意，这不是通常用于多态的公共继承。因为 std::string 没有虚成员函数，你应该非常小心并避免混合这两种类型。

你甚至可以从多个基类和/或聚合体派生聚合体：

```
template<typename T>
struct D : std::string, std::complex<T>
{
    std::string data;
};
```

然后你就可以像下面这样使用和初始化它：

```
D<float> s{"hello"}, {4.5,6.7}, "world"};      // OK since C++17
D<float> t{"hello", {4.5, 6.7}, "world"};            // OK since C++17
std::cout << s.data;                                   // outputs: "world"
std::cout << static_cast<std::string>(s);              // outputs: "hello"
std::cout << static_cast<std::complex<float>>(s);      // outputs: (4.5,6.7)
```

内部初始化列表按基类声明的顺序传递给基类。

新功能还有助于用很少的代码定义 lambda 的重载。

## 4.3 Definition of Aggregates

总之，自 C++17 起，聚合体定义为

- 要么是数组
- 要么是类类型（class、struct 或 union），具有：
  - 没有用户声明或显式构造函数
  - 没有通过 using 声明继承的构造函数
  - 没有私有或受保护的非静态数据成员
  - 没有虚函数
  - 没有虚、私有或受保护的基类

然而，聚合体要能够初始化它们，还存在额外的约束：

- 没有私有或受保护的基类成员
- 没有私有或受保护的构造函数

请参阅下一节，了解由于这些额外约束而导致编译失败的示例。

C++17 还引入了新的类型特征 is_aggregate<> 来测试一个类型是否为聚合体：

```
template<typename T>
struct D : std::string, std::complex<T> {
    std::string data;
};
D<float> s{"hello"}, {4.5,6.7}, "world"};          // OK since C++17
std::cout << std::is_aggregate<decltype(s)>::value; // outputs: 1 (true)
```

## 4.4 Backward Incompatibilities

请注意，以下示例不再编译：

```
lang/aggr14.cpp

struct Derived;

struct Base {
    friend struct Derived;
    private:
        Base() {
        }
};

struct Derived : Base {
};

int main()
{
    Derived d1{};    // ERROR since C++17
    Derived d2;      // still OK (but might not initialize)
}
```

在 C++17 之前，Derived 不是一个聚合体。因此，

    Derived d1{};

调用了 Derived 的隐式定义的默认构造函数，该构造函数默认调用基类 Base 的默认构造函数。尽管基类的默认构造函数是私有的，但通过派生类的默认构造函数调用它是有效的，因为派生类被定义为友元类。

自 C++17 起，此示例中的 Derived 是一个聚合体，完全没有隐式默认构造函数（构造函数没有通过 using 声明继承）。因此，初始化是聚合初始化，这意味着表达式

    std::is_aggregate<Derived>::value

产生 true。

然而，你不能使用大括号初始化，因为基类具有私有构造函数（参见上一节）。基类是否为友元无关紧要。

## 4.5 Afternotes

扩展聚合初始化首次由 Oleg Smolsky 在 http://wg21.link/n4404 中提出。最终被接受的措辞也由 Oleg Smolsky 在 http://wg21.link/p0017r1 中制定。

类型特征 std::is_aggregate<> 是作为美国国家机构评论引入的，用于 C++17 的标准化（参见 http://wg21.link/lwg2911）。

