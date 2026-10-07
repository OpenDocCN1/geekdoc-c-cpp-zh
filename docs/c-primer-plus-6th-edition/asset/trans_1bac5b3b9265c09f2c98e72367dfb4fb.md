

# 1244 附录 E 其他运算符

你需要用括号将整个 ob3.*pf 包围起来，以便清楚地识别该表达式表示一个函数名。

由于 show_feet() 与 show_inches() 具有相同的原型形式，你也可以使用 pf 来访问 show_feet() 方法：

```
pf = &Example::show_feet;
(ob3.*pf()); // apply show_feet() to the ob3 object
```

在附录 E.1 中的类定义中，use_ptr() 方法使用指针访问 Example 类的 both 数据成员和函数成员。

## 附录 E.1 memb_pt.cpp

```
// memb_pt.cpp -- dereferencing pointers to class members
#include <iostream>
using namespace std;

class Example {
private:
    int feet;
    int inches;
public:
    Example();
    Example(int ft);
    ~Example();
    void show_in() const;
    void show_ft() const;
    void use_ptr() const;
};

Example::Example() {
    feet = 0;
    inches = 0;
}

Example::Example(int ft) {
    feet = ft;
    inches = 12 * feet;
}

Example::~Example() {
}
```

## 成员解引用运算符 1245

```
void Example::show_in() const
{
    cout << inches << " inches\n";
}
```

```
void Example::show_ft() const
{
    cout << feet << " feet\n";
}
```

```
void Example::use_ptr() const
{
    Example yard(3);
    int Example::*ptr;
    ptr = &Example::inches;
    cout << "this->*ptr: " << this->*ptr << endl;
    cout << "yard.*ptr: " << yard.*ptr << endl;
    ptr = &Example::feet;
    cout << "Set ptr to &Example::feet\n";
    cout << "this->*ptr: " << this->*ptr << endl;
    cout << "yard.*ptr: " << yard.*ptr << endl;
    void (Example::*pf)() const;
    pf = &Example::show_in;
    cout << "Set pf to &Example::show_in\n";
    cout << "Using (this->*pf)(): ";
    (this->*pf)();
    cout << "Using (yard.*pf)(): ";
    (yard.*pf)();
}
```

```
int main()
{
    Example car(15);
    Example van(20);
    Example garage;

    cout << "car.use_ptr() output:\n";
    car.use_ptr();

    cout << "\nvan.use_ptr() output:\n";
    van.use_ptr();

    return 0;
}
```

# 1246 附录 E 其他运算符

以下是附录 E.1 中程序的一个示例运行结果：

```
car.use_ptr() output:
Set ptr to &Example::inches:
this->*ptr: 180
yard.*ptr: 36
Set ptr to &Example::feet:
this->*ptr: 15
yard.*ptr: 3
Set pf to &Example::show_in:
Using (this->*pf)(): 180 inches
Using (yard.*pf)(): 36 inches
```

```
van.use_ptr() output:
Set ptr to &Example::inches:
this->*ptr: 240
yard.*ptr: 36
Set ptr to &Example::feet:
this->*ptr: 20
yard.*ptr: 3
Set pf to &Example::show_in:
Using (this->*pf)(): 240 inches
Using (yard.*pf)(): 36 inches
```

此示例在编译时分配了指针值。在更复杂的类中，你可以使用指向数据成员和方法的成员指针，其中与指针关联的确切值在运行时确定。

## alignof (C++11)

计算机系统对内存中数据的存储方式有限制。例如，一个系统可能要求 double 值存储在偶数位置，而另一个系统可能要求存储从是 8 的倍数的地址开始。alignof 运算符以类型作为参数，并返回一个整数，表示所需的对齐类型。对齐要求例如决定了信息在结构内的排列方式，如附录 E.2 所示。

### 附录 E.2 align.cpp

```
// align.cpp -- checking alignment
#include <iostream>
using namespace std;
struct thing1
{
    char ch;
    int a;
    double x;
};
struct thing2
{
    int a;
    double x;
    char ch;
};
```

```
int main() {
    thing1 th1;
    thing2 th2;
    cout << "char alignment: " << alignof(char) << endl;
    cout << "int alignment: " << alignof(int) << endl;
    cout << "double alignment: " << alignof(double) << endl;
    cout << "thing1 alignment: " << alignof(thing1) << endl;
    cout << "thing2 alignment: " << alignof(thing2) << endl;
    cout << "thing2 size: " << sizeof(thing2) << endl;
    return 0;
}
```

在一个系统上的输出如下：
char alignment: 1
int alignment: 4
double alignment: 8
thing1 alignment: 8
thing2 alignment: 8
thing1 size: 16
thing2 size: 24

两个结构都具有 8 的对齐要求。其中的一个含义是结构大小应为 8 的倍数，这样就可以创建结构数组，每个元素彼此相邻，并且也从是 8 的倍数的对齐边界开始。附录 E.2 中每个结构的各个成员总共只使用 13 个字节，但 8 个字节的倍数的要求意味着每个结构都需要一些填充。接下来，在每个结构内部，double 成员需要在 8 的倍数上对齐。thing1 和 thing2 中成员的不同排列导致 thing2 需要更多的内部填充以使边界正确。

# noexcept (C++11)

`noexcept` 关键字用于表示函数不抛出异常。它也可以用作运算符，确定其操作数（一个表达式）是否可能抛出异常。它如果操作数可能抛出异常则返回 `false`，否则返回 `true`。例如，考虑以下声明：

```
int hilt(int);
halt(int) noexcept;
```

表达式 `noexcept(hilt)` 将被求值为 `false`，因为 `hilt()` 的声明并不保证不会抛出异常。但 `noexcept(halt)` 将被求值为 `true`。

# string 模板类

本附录的大部分内容有点技术性。然而，如果你只想了解 string 模板类的功能，你可以集中在各种 string 方法的描述上。
string 类基于一个模板定义：

```
template<class charT, class traits = char_traits<charT>,
class Allocator = allocator<charT> > class basic_string {...};
```

这里 charT 表示存储在字符串中的类型。traits 表示一个类，该类定义了该类型必须作为字符串表示所需的操作。例如，它应具有一个 length() 方法，返回字符串的长度，表示为 charT 的数组。这样的数组的结尾由值 charT(0) 表示，即空字符。 （表达式 charT(0) 是将 0 转换为类型 charT 的类型转换。对于类型 char，它可以只是 0，更一般地，它可以是由 charT 构造函数创建的对象。）该类还包括比较值等方法。Allocator 参数表示一个类来处理内存分配。默认模板以标准方式使用 new 和 delete。

有四个预定义的特化：

```
typedef basic_string<char> string;
typedef basic_string<char16_t> u16string;
typedef basic_string<char32_t> u32string;
typedef basic_string<wchar_t> wstring;
```

这些特化依次使用以下特化：

```
char_traits<char>
allocator<char>
char_traits<char16_t>
allocator<char16_t>
char_traits<char32_t>
allocator<char32_t>
char_traits<wchar_t>
allocator<wchar_t>
```

你可以通过定义一个 traits 类并使用 basic_string 模板，为 char 或 wchar_t 以外的某些类型创建一个 string 类。

# 十三种类型和一个常量

basic_string 模板定义了几种稍后在定义方法时使用的类型：

```
typedef typename traits::char_type    traits_type;
typedef typename traits::value_type   value_type;
typedef Allocator                     allocator_type;
typedef typename Allocator::size_type      size_type;
typedef typename Allocator::difference_type difference_type;
typedef typename Allocator::reference reference;
typedef typename Allocator::const_reference const_reference;
typedef typename Allocator::pointer     pointer;
typedef typename Allocator::const_pointer const_pointer;
```

请注意 traits 是一个模板参数，对应于某个特定类型，例如 char_traits<char>；traits_type 成为该特定类型的 typedef。以下表示法意味着 char_type 是在类表示中定义的：

```
typedef typename Allocator::char_type    value_type;
```

关键字 typename 用于告诉编译器表达式 ::char_type 是一个类型。对于 string 特化，例如，value_type 是 char。

size_type 的用法类似于 sizeof，只是它返回字符串的大小，以存储的类型为单位。对于 string 特化，这将以 char 为单位，其中 size_type 与 size_t 相同。它是一个无符号类型。difference_type 用于衡量字符串中两个元素之间的距离，以单个元素大小为单位。通常，它是底层 size_type 的有符号版本。

对于 char 特化，pointer 类型是 char *，reference 类型是 char &。然而，如果你为自己设计的类型创建一个特化，这些类型（pointer 和 reference）指的是具有与更基本指针和引用相同属性的类。

为了允许标准模板库（STL）算法与字符串一起使用，模板定义了一些迭代器：

```
typedef (models random access iterator)     iterator;
typedef (models random access iterator)     const_iterator;
typedef std::reverse_iterator<iterator>      reverse_iterator;
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```
