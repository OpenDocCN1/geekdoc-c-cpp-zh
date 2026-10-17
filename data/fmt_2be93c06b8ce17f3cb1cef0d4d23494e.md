
```cpp
X<int,"BMW323Ci"> x1; char lx2[] = "BMW323Ci"; X<int,lx2> x2;
// error : string literal as template argument
// OK: lx2 has external linkage
```

这种限制，就像禁止浮点模板值参数一样，存在是为了简化单独编译的翻译单元的实现。最好将模板值参数视为传递整数和指针给函数的机制。抵制尝试做更巧妙事情的诱惑。不幸的是（没有根本原因），字面类型（§10.4.3）不能用作模板值参数。值模板参数是某些更高级的编译时计算技术（第 28 章）的机制。

整数模板参数必须是常量。例如：

```cpp
constexpr int max = 200;
```

```cpp
void f(int i) {
Buffer<int,i> bx; Buffer<int,max> bm; // ...
}
// error :constant expression expected // OK: constant expression
```

相反，模板中的值模板参数是常量，因此尝试更改参数的值是错误。例如：

```cpp
template<typename T, int max>
class Buffer {
T v[max];
public:
Buffer(int i) { max = i; } // error :attempt to assign to template value argument
// ...
};
```

类型模板参数可以在模板参数列表中稍后用作类型。例如：

```cpp
template<typename T, T default_value>
class Vec {
// ...
};
Vec<int,42> c1;
Vec<string,""> c2;
```

当与默认模板参数（§25.2.5）结合使用时，这变得特别有用；例如：

```cpp
template<typename T, T default_value = T{}>
class Vec {
// ...
};
```

```cpp
Vec<int,42> c1;
Vec<int> c11; // default_value is int{}, that is, 0
Vec<string,"forty two"> c2;
Vec<string> c22; // default_value is string{}, that is, ""
```

# 25.2.3 操作作为参数

考虑标准库 map（§31.4.3）的稍微简化版本：

```cpp
template<typename Key, class V>
class map {
// ...
```

我们如何为 Keys 提供比较标准？

- 我们不能将比较标准硬编码到容器中，因为容器通常不能对其元素类型施加需求。例如，默认情况下，map 使用 < 进行比较，但并非所有 Keys 都有我们想要使用的 <。

- 我们不能将排序标准硬编码到 Key 类型中，因为通常有多种基于键对元素进行排序的方式。例如，最常见的 Key 类型之一是 string，而字符串可以根据多种标准进行排序（例如，区分大小写和不区分大小写）。

因此，排序标准既不内置于容器类型，也不内置于元素类型。原则上，map 的排序标准的概念可以表示为：

[1] 一个模板值参数（例如，指向比较函数的指针）

[2] 一个模板类型参数，确定比较对象的类型

乍一看，第一种解决方案（传递特定类型的比较对象）似乎更简单。例如：

```cpp
template<typename Key, typename V, bool (*cmp)(const Key&, const Key&)>
class map {
public:
map();
// ...
};
```

此 map 要求用户以函数形式提供比较：

```cpp
bool insensitive(const string& x, const string& y)
{
    // compare case insensitive (e.g., "hello" equals "Hello")
}
```

```cpp
map<string,int,insensitive> m; // compare using insensitive()
```

然而，这并不灵活。特别是，map 的设计者必须决定是否使用指向函数的指针或某种特定类型的函数对象来比较（未知的）Key 类型。此外，由于比较运算符的参数类型必须依赖于 Key 类型，很难提供默认的比较标准。

因此，第二种替代方案（将比较的类型作为模板类型参数传递）更为常见，也是标准库中使用的方法。例如：

```cpp
template<typename Key, class V, typename Compare = std::less<Key>>
class map {
public:
    map() { /*...*/ } // use the default comparison
    map(Compare c) : cmp{c} { /*...*/ } // override default
    Compare cmp {}; // default comparison
};
```

最常见的情况，使用小于比较，是默认值。如果我们想要不同的比较标准，可以将其作为函数对象（§3.4.3）提供：

```cpp
map<string,int> m1; // use the default comparison (less<string>)
map<string,int,std::greater<string>> m2; // compare using greater<string>()
```

函数对象可以携带状态。例如：

```cpp
Complex_compare f3 {"French",3}; map<string,int,Complex_compare> m3 {f3}; // make a comparison object (§25.2.5) // compare using f3()
```

我们也可以使用指向函数的指针，包括可以转换为指向函数的指针的 lambda（§11.4.5）。例如：

```cpp
using Cmp = bool(*)(const string&,const string&);
map<string,int,Cmp> m4 {insensitive}; // compare using a pointer to function
map<string,int,Cmp> m5 {[](const string& a, const string& b) { return a>b; } };
```

将比较操作作为函数对象传递与传递指向函数的指针相比有显著好处：

- 在类内定义的简单类成员函数很容易内联，而通过指向函数的指针调用的内联需要编译器的特别关注。

- 没有数据成员的函数对象可以零运行时成本传递。

- 多个操作可以作为单个对象传递而没有额外的运行时成本。

map 的比较标准只是一个例子。然而，用于传递它的技术是通用的，被广泛用于用“策略”参数化类和函数。示例包括算法的动作（§4.5.4，§32.4）、容器的分配器（§31.4，§34.4）以及 unique_ptr 的删除器（§34.3.1）。当我们需要为函数模板指定参数时，例如 sort()，我们也有相同的设计替代方案，标准库也为这些情况选择了替代方案 [2]（例如参见 §32.4）。

如果我们的程序中只有一个比较标准的用途，使用 lambda 来更简洁地表达函数对象版本可能有意义：

```cpp
map<string,int,Cmp> c3 {[](const string& x, const string& y) const { return x<y; }};
// error
```

不幸的是，这不起作用，因为 lambda 不能转换为函数对象类型。我们可以命名 lambda 然后使用该名称：

```cpp
auto cmp = [](const string& x, const string& y) const { return x<y; };
map<string,int,decltype(cmp)> c4 {cmp};
```

我发现从设计和维护的角度来看，命名操作是有用的。此外，任何被命名并在非局部声明的操作都可能找到其他用途。

# 25.2.4 模板作为参数

有时将模板——而不是类或值——作为模板参数传递是有用的。例如：

```cpp
template<typename T, template<typename> class C> class Xrefd {
C<T> mems;
C<T*> refs;
// ...
};
template<typename T>
using My_vec = vector<T>; // use default allocator
Xrefd<Entry,My_vec> x1; // store cross references for Entries in a vector
template<typename T> class My_container { // ...
};
Xrefd<Record,My_container> x2; // store cross references for Records in a My_container
```

要将模板声明为模板参数，我们必须指定其所需参数。例如，我们指定 Xrefd 的模板参数 C 是一个接受单个类型参数的模板类。如果我们不这样做，我们就无法使用 C 的特化。使用模板作为模板参数的目的是通常我们希望用多种参数类型（例如 T 和 T*）实例化它。也就是说，我们希望以另一个模板为参数来表达模板的成员声明，但我们希望该其他模板是参数，以便用户可以指定它。

只有类模板可以作为模板参数。模板只需要一个或两个容器的常见情况通常最好通过传递容器类型（§31.5.1）来处理。例如：

```cpp
template<typename C, typename C2>
```

```cpp
class Xrefd2 {
    C mems;
    C2 refs;
    // ...
};

Xrefd2<vector<Entry>, set<Entry*>> x;
```

这里，`C` 和 `C2` 的值类型可以通过一个简单的类型函数（§28.2）获得，该函数用于获取容器的元素类型，例如 `Value_type<C>`。这就是标准库容器适配器（如 `queue`（§31.5.2））所使用的技术。

# 25.2.5 默认模板参数

为每次 `map` 使用显式指定比较准则很繁琐——尤其是 `less<Key>` 通常是最好的选择。我们可以将 `less<Key>` 指定为 `Compare` 模板参数的默认类型，这样只有不常见的比较准则才需要显式指定：

```cpp
template<typename Key, class V, typename Compare = std::less<Key>>
class map {
public:
    explicit map(const Compare& comp = {});
    // ...
};

map<string, int> m1;
map<string, int, less<string>> m2;
```

```cpp
struct No_case {
    // define operator()() to do case-insensitive string comparison
};

// will use less<string> for comparisons
// same type as m1
map<string, int, No_case> m3; // m3 is of a different type from m1 and m2
```

注意默认的 `map` 构造函数会创建一个默认的比较对象，`Compare{}`。这是常见情况。如果我们想要更复杂的构造，就必须显式进行。例如：

```cpp
map<string, int, Complex_compare> m{Complex_compare{"French", 3}};
```

对模板参数的默认参数的语义检查只有在使用该默认参数时才会进行。特别是，只要我们避免使用默认模板参数 `less<Key>`，我们就可以比较类型为 `X` 的值，即使 `less<X>` 无法编译。这一点在标准容器的设计中至关重要（例如，`std::map`），它们依赖于模板参数来指定默认值（§31.4）。

与默认函数参数（§12.2.5）一样，默认模板参数只能为尾部参数指定和提供：

```cpp
void f1(int x = 0, int y); // error: default argument not trailing
void f2(int x = 0, int y = 1); // OK

f2(, 2); // syntax error
f2(2);   // call f(2, 1);

template<typename T1 = int, typename T2>
class X1 { // error: default argument not trailing
    // ...
};

template<typename T1 = int, typename T2 = double>
class X2 { // OK
    // ...
};

X2<, float> v1; // syntax error
X2<float> v2;   // v2 is an X2<float, double>
```

不允许使用“空”参数来表示“使用默认值”是在灵活性和避免晦涩错误机会之间做出的刻意权衡。

通过模板参数提供策略然后将该参数默认为最常见的策略的技术在标准库中几乎无处不在（例如，§32.4）。有趣的是，它并未用于 `basic_string`（§23.2，第36章）的比较。相反，标准库字符串依赖于 `char_traits`（§36.2.2）。同样，标准算法依赖于 `iterator_traits`（§33.1.3），而标准库容器依赖于分配器（§34.4）。特征的使用在 §28.2.4 中介绍。

## 25.2.5.1 默认函数模板参数

自然地，默认模板参数对于函数模板也很有用。例如：

```cpp
template<typename Target = string, typename Source = string>
Target to(Source arg) // convert Source to Target
{
    stringstream interpreter;
    Target result;

    if (!(interpreter << arg)       // write arg into stream
        || !(interpreter >> result) // read result from stream
        || !(interpreter >> std::ws).eof()) // stuff left in stream?
        throw runtime_error{"to<>() failed"};

    return result;
}
```

函数模板参数只有在无法推导或没有默认值时才需要显式提及，因此我们可以写：

```cpp
auto x1 = to<string, double>(1.2); // very explicit (and verbose)
auto x2 = to<string>(1.2);         // Source is deduced to double
auto x3 = to<>(1.2);               // Target is defaulted to string; Source is deduced to double
auto x4 = to(1.2);                 // the <> is redundant
```

如果所有函数模板参数都是默认的，可以省略 `<>`（与函数模板特化完全相同；§25.3.4.1）。

这种 `to()` 实现对于简单类型的组合（如 `to<double>(int)`）来说有点笨重，但可以提供特化作为改进实现（§25.3）。请注意 `to<char>(int)` 将无法工作，因为 `char` 和 `int` 没有共享的字符串表示。对于标量数值类型之间的转换，我更倾向于使用 `narrow_cast<>`（§11.5）。

# 25.3 特化

默认情况下，模板为用户可能想到的每个模板参数（或模板参数组合）提供单一定义。这对于编写模板的人来说并不总是合理。我可能想说，“如果模板参数是指针，就使用这个实现；如果不是，就使用那个实现”，或者“除非模板参数是从类 `My_base` 派生的指针，否则报错。” 许多此类设计问题可以通过提供模板的替代定义并让编译器根据使用时提供的模板参数在它们之间进行选择来解决。模板的此类替代定义称为 *用户定义特化*，或简称为 *用户特化*。考虑 `Vector` 的可能用途：

```cpp
template<typename T>
class Vector { // general vector type
    T* v;
    int sz;

public:
    Vector();
    explicit Vector(int);

    T& elem(int i) { return v[i]; }
    T& operator[](int i);
    void swap(Vector&);
    // ...
};

Vector<int> vi;
Vector<Shape*> vps;
Vector<string> vs;
Vector<char*> vpc;
Vector<Node*> vpn;
```
