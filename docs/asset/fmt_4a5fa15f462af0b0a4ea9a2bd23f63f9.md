
`sizeof` 运算符也可以用于变长非类型参数，因为在第一个函数 `forwarder<1, 2, 3>` 中使用 `sizeof...(Ints)` 会返回 3。

变长非类型参数用于定义变长字面量运算符，该运算符在第 23.3 节中引入。

### 22.5.5 折叠表达式

接受可数量参数（类型可能不同）的函数通常使用变长模板处理。实现通常处理第一个参数，并将剩余参数传递给重载函数，该函数由编译器为这些参数类型定义。重载版本中的一个接受零或一个参数的版本结束了编译器的递归实现。

有时，必须使用二元运算符组合参数（`arg1 + arg2 + ...`）。在这些情况下，可以使用折叠表达式来代替使用传统的变长模板组合参数。

所有二元运算符（包括赋值、复合赋值和逗号运算符）都可以用于折叠表达式。

一元左折叠（unary left fold）形式如下的折叠表达式：

`(... op expr)`

其中 `op` 是折叠表达式使用的二元运算符，`expr` 是根据代表变长参数的函数参数公式表达式。这是一个示例：

```cpp
template <typename ReturnType, typename ...Params>
ReturnType sum(Params ...params)
{
  return (... + params);
}
```

如果使用了比仅变长参数标识符更复杂的表达式，则该表达式必须明确标记，例如用括号将其括起来：

```cpp
return (... + (2 * params));
```

在单元折叠中，所有匹配参数包类型的函数参数都将使用指定的运算符组合。例如：

`sum<int>(1, 2, 3);`

返回

（注：此处原文未提供具体返回值，故保留格式）

## 22.6. 元组 (TUPLES)

元组提供了以下静态元素（使用编译时初始化）：

- `std::tuple_size<Tuple>::value` 返回为为元组 `Tuple` 定义的类型数量。例如：
```cpp
c << tuple_size<tuple_ids>::value << '\n'; // 显示: 4
```
- `std::tuple_element<idx, Tuple>::type` 返回为元组 `Tuple` 中索引为 `idx` 的元素类型。例如：

解包运算符也可以用于将构造函数的参数转发到元组数据成员。考虑一个定义为变长模板的 `Wrapper` 类：

```cpp
template <typename ...Params>
class Wrapper {
  public:
    Wrapper(Params &&...params);
};
```

该类可以赋予一个元组数据成员，该成员应该使用用于完美转发的类型和值进行初始化。类似于类继承其模板类型的方式（参见第 22.5.3 节），它可以将其类型和构造函数参数转发给其元组数据成员：

```cpp
template <typename ...Params>
class Wrapper {
  std::tuple<Params...> d_tuple; // 与所使用的类型相同
  // Wrapper 本身
  public:
    Wrapper(Params &&...params) // 初始化 d_tuple
      d_tuple(std::forward<Params>(params)...); // Wrapper 的参数
};
```

### 22.6.1 元组与结构化绑定

结构化绑定是在 3.3.7.1 节引入的。该节专注于将结构化绑定声明与结构体的数据成员关联，并以 POD 值的形式返回。

然而，结构化绑定也可以通过与元组关联以更通用的方式使用。因此，结构化绑定不必与数据成员关联，它可以持有类成员返回的值。

结构化绑定声明与元组之间的关联非常紧密。事实上，这种关联紧密到标准明确允许用户定义元组特化，尽管元组特化位于标准命名空间，而该空间对程序员是非开放的（除非除非使用其功能时）。

为了允许结构化绑定与类成员关联，必须执行以下步骤：

- 类必须定义有重载的 `get` 成员模板，并带有 `int`（或其他整数类型）的特化，每个特化返回一个类元素（例如，成员函数）。
- `if constexpr` 的可用性使得将所有这些特化组合到单个成员模板变得简单。
- 另一种方法是在类外定义一个函数模板，这使得即使不是该类的作者，也可以将结构化绑定与类成员关联。在这种情况下，函数定义了一个 `ClassType [cv]` 对象参数。
- 提供 `std::tuple_size<Type>` 的特化，将 `static size_t const value` 定义为可以使用 `get<idx>` 函数指定的索引值数量。虽然标准命名空间中的实体对普通程序是不可访问的，但在这种特殊情况下，C++ 标准允许此类特化。
- 提供 `std::tuple_element<idx, Type>` 的特化，定义的 `type` 与 `get<idx>` 的返回类型匹配。

通过这种方式使用结构化绑定所实现的灵活性是巨大的。只要类允许返回值，成员就可以与结构化绑定变量关联。成员函数甚至不需要返回立即可用的值（例如，作为数据成员的访问器），但它们的返回值可以通过简单地引用相应的绑定变量即时计算。

为了说明上述将结构化绑定与类成员关联的步骤，我们使用以下代码：

```cpp
class Euclid
{
    size_t d_x;
    size_t d_y;
public:
    Euclid(size_t x = 0, size_t y = 0);
    double distance() const; // sqrt(dx * d_x + d_y * d_y)
};

class Data
{
    std::string d_text("hello from Data");
    Euclid d_euclid;
public:
    void setXY(size_t x, size_t y);
    Euclid factory() const;
    double distance() const;
    std::string const &text() const;
};
```

允许 `Data` 使用结构化绑定的第一步是定义（成员）模板 `get`。如果 `Data` 是我们自己的类，我们可以添加一个成员模板 `get`。或者，如果我们只对访问 `Data` 的公共成员，可以从 `Data` 派生一个类 `DataGet` 并为该类提供 `get` 成员模板。另一种可能性是定义一个自由的 `get` 模板。函数必须返回我们感兴趣的内容。为了做出适当的选择，我们使用整数类型（int, size_t, ...）作为选择器值，并且函数模板有一个默认参数。建议使用 `constexpr` 子句定义多个特化，因为这极大简化了函数的定义。

我们的 `get` 函数为 `factory` 定义选择器 0，为 `distance` 定义选择器 1，为 `text` 定义选择器 2。`distance` 成员简单返回 `d_euclid.distance()`，而 `Euclid::distance` 使用 `d_x` 和 `d_y` 值在运行时求值。那么，`distance` 就是在后续引用结构化绑定变量时运行时求值的函数示例。

以下是成员模板的定义：

```cpp
template <size_t Nr>
auto get() {
    if constexpr (Nr == 0)
        return factory();
    if constexpr (Nr == 1)
        return distance();
    if constexpr (Nr == 2)
        return text();
}
```

*(注：OCR 文本包含一些乱码和重复。我根据提供的技术内容重构了逻辑流。）*

## 22.7. 计算函数对象的返回类型

### 22.7 计算函数对象的返回类型

如第 19 节所示，函数对象在泛型算法中起着重要作用。与泛型算法一样，函数对象可以泛泛地定义为类模板的成员。如果此类类的函数调用运算符 `operator()` 定义了参数，那么这些参数的类型也可以通过将函数调用运算符本身定义为成员模板来抽象化。例如：

```cpp
template <typename Class>
class Filter
{
    Class obj;
    public:
        template <typename Param>
        Param operator() (Param const &param) const
        {
            return obj(param);
        }
};
```

`Filter` 类是 `Class` 的包装器，它通过自己的函数调用运算符来过滤 `Class` 的函数调用运算符。在上面的示例中，`Class` 函数调用运算符的返回值被简单地传递了，但也可以对其进行任何操作。

作为 `Filter` 模板参数的类型可能有多个函数调用运算符：

```cpp
struct Math
{
    int operator() (int x);
    double operator() (double x);
};
```

现在可以使用 `Filter<Math>` 使用 `Math` 的第一个或第二个调用运算符来过滤 `Math` 对象，取决于实际类型。通过 `fm(5)` 使用 `int` 版本，通过 `fm(12.5)` 使用 `double` 版本。

然而，如果函数调用运算符具有不同的返回类型和参数类型，这种方案就不起作用。因此，下面的类 `Convert` 无法与 `Filter` 使用：

```cpp
struct Convert
{
    double operator() (int x); // int转double
    std::string operator() (double x); // double转string
};
```

这个问题可以通过类模板 `std::result_of<Functor(TypeList)>` 成功地解决。在使用 `std::result_of` 之前，必须包含头文件 `<functional>`。

类模板 `result_of` 提供了一个声明 `(type)`，表示 `Functor<TypeList>` 返回的类型。可以如下所示使用它，以改进 `Filter` 的实现：

```cpp
template <typename Class>
class Filter
{
    Class obj;
  public:
    template <typename Arg>
        typename std::result_of<Class(Arg)>::type
        operator()(Arg const &arg) const
        {
            return obj(arg);
        }
};
```

使用此定义，可以构造 `Filter<Convert> fc`。现在 `fc(5)` 返回一个 double，而 `fc(4.5)` 返回一个 double。

`Convert` 类必须定义其函数调用运算符与它们返回类型之间的关系。预定义的函数对象（如标准模板库中的）已经这样做了，因此自定义的函数对象必须显式地这样做。

如果一个函数对象只定义了一个函数调用运算符，它可以通过 `using` 声明来指定其返回类型。如果上面的 `Convert` 类只定义其两个函数运算符中的第一个，那么声明（在类的公共部分）应当是：

```cpp
using type = double;
```

如果定义了多个调用运算符，每个运算符都有自己的签名和返回类型，那么签名与返回类型之间的关联建立如下（全部在类的公共部分）：

- 定义一个如下的泛型结构体 `result`：

```cpp
template <typename Signature>
struct result;
```

- 对于每个函数调用签名，定义 `struct result` 的特化。`Convert` 的第一个函数调用运算符产生了：

```cpp
template <typename Class>
struct result<Class(int)>
{
    using type = double;
};
```

- 以及 `Convert` 的第二个函数调用运算符产生了：

```cpp
template <typename Class>
struct result<Class(double)>
{
    using type = std::string;
};
```

- 在函数调用运算符有多个参数的情况下，规范应再次提供正确的签名。一个使用 `int` 和 `double` 运行并返回 `size_t` 的函数调用运算符得到：

```cpp
template <typename Class>
struct result<Class(int, double)>
  using type = size_t;
);
```

## 22.8 实例化类模板

### 22.8 实例化类模板

类模板在定义类模板对象的实例时被实例化。当定义或声明一个类对象时，必须显式地指定其模板参数。

当指定默认模板参数值时，模板参数*也会*被指定，尽管在这种情况下编译器提供了 `DataType` 参数的默认值（参见 22.4 节，其中使用 `double` 作为默认类型）。模板参数的实际值是从参数中*推导*出来的，就像函数模板参数一样。因此，要定义一个包含复数元素的 `Matrix`，使用以下语法：

```cpp
Matrix<3, 5, std::complex> complexMatrix;
```

由于类模板 `Matrix` 使用 `double` 值的数据类型矩阵，可以像这样定义矩阵：

```cpp
Matrix<3, 5> doubleMatrix;
```

类对象可以使用 `extern` 关键字*声明*。例如，要*声明*矩阵 `complexMatrix`，使用：

```cpp
extern Matrix<3, 5, std::complex> complexMatrix;
```

类模板声明就足够编译属于类类型的返回值或参数：以下源文件可以编译，尽管编译器尚未见过 `Matrix` 的定义：以下源文件可以编译，尽管编译器尚未见过 `Matrix` 的定义：以下源文件可以编译，尽管编译器尚未见过 `Matrix` 的定义：以下源文件可以编译，尽管编译器尚未见过 `Matrix` 的定义：

## 22.9. 处理类模板和实例化

### 22.9 处理类模板和实例化

在 22.4 节中，引入了依赖模板参数的代码与不依赖模板参数的代码的区别。在定义类模板时，这种区别同样适用。

## 22.10 声明友元

# 866 第 22 章 类模板

class. 尽管在使用类模板时，任何类型的类（普通类或模板）都可以使用 `friend` 关键字，但应区分以下情况：

- 类模板可以将一个普通函数或类声明为它的友元（friend）。这是常见的友元声明，例如用于 `ostream` 对象的插入运算符。
- 类模板可以将另一个函数模板或类模板声明为它的友元。在这种情况下，必须指定该友元模板的模板参数。
- 如果友元模板参数的实际值必须与绑定的友元类或函数模板相等。在这种情况下，声明该友元的模板类模板参数被称为指定友元的**绑定（bound）友元类或函数模板**，它指定了绑定（bind）友元类模板参数的值。绑定友元会导致模板参数与友元的模板参数之间建立一对一的对应关系。
- 在一般情况下，类模板可以将另一个函数模板或类模板声明为它的友元，而无论该友元的实际模板参数如何。
- 在这种情况下，声明了一个未绑定的（unbound）友元类或函数模板。必须指定友元类或函数模板的模板参数，且它们与声明该友元的类的模板参数无关。如果一个类具有由其模板参数指定的各种类型的数据成员，并且允许另一个类访问这些成员，我们希望在指定友元时指定当前的模板参数。与其指定多个绑定友元，不如声明一个单一的泛型（未绑定）友元，仅在需要时指定该友元的实际模板参数。

- 上述将模板声明为友元的情况，在使用普通类时也可能遇到：
    - 声明友元的普通类已经涵盖过（第 15 章）。
    - 如果普通类在声明其友元时指定了特定的模板参数，则等同于绑定友元。
    - 如果普通类将一个泛型模板声明为其友元，则等同于未绑定友元。

## 22.10.1 在模板中作为友元使用的非模板

类模板可以将一个普通函数、普通成员函数或普通类声明为它的友元。此类友元可以访问类模板的私有成员。

具体类和普通函数可以被声明为友元，但在将类的某个成员函数声明为友元之前，编译器必须看到声明该成员的类接口。让我们考虑各种可能性：

- 类模板可以将一个普通函数声明为它的友元。目前还不完全清楚我们为什么要将一个普通函数声明为友元。通常，我们将声明该友元的类对象传递给此类函数。对于类模板，这要求我们在不指定其类型的情况下，为模板参数提供（友元）函数。由于语言不支持如下构造：

```
void function(std::vector<Type> &vector)
```

除非函数本身是一个模板，否则并不立刻清楚应该如何以及为什么要构造这样的友元。一个可能的原因是允许该函数访问该类的私有静态成员。此外，此类友元可以实例化声明它们为友元的类对象。这将允许友元函数直接访问此类对象的私有成员。例如：

```cpp
template <typename Type>
class Storage
{
    friend void basic();
    static size_t s_time;
    std::vector<Type> d_data;
public:
    Storage();
};

template <typename Type>
```
