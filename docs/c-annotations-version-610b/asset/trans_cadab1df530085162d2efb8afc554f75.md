
一个类模板。该类模板定义了一个由函数返回的枚举值 result，除非没有指定任何 int 值，此时返回 0。

```cpp
template <int ... Ints>
int forwarder()
{
    return computer<Ints ...>::result;  // forwarding the Ints
}

template <>    // specialization if no ints are provided
int forwarder<>()
{
    return 0;
}

// use as:
cout << forwarder<1, 2, 3>() << ' ' << ' ' << forwarder<>() << '\n';
```

sizeof 运算符也可用于可变参数非类型模板参数：在 forwarder<1, 2, 3>() 的第一个函数模板中使用 sizeof...(Ints) 将返回 3。

可变参数非类型模板参数用于定义可变参数字面量运算符，这将在第 22.3 节介绍。

## 21.6 元组（C++11）

C++11 标准提供了一种*广义 pair 容器*：*元组*，本节将介绍它。使用元组之前，必须包含头文件 `<tuple>`。

`std::pair` 容器的功能有限，并且只支持两个成员；相比之下，元组的功能稍多一些，并且可以包含数量不限的不同数据类型。在这方面，元组可以看作是*模板对 C 结构体的回应*。

元组的泛型声明（和定义）使用可变参数模板表示法：

```cpp
template <class ...Types>
class tuple;
```

下面是其用法示例：

```cpp
typedef std::tuple<int, double &, std::string, char const *> tuple_idsc;

double pi = 3.14;
tuple_idsc idsc(59, pi, "hello", "fixed");

// access a field:
std::get<2>(idsc) = "hello world";
```

`std::get<idx>(tupleObject)` 函数模板返回对元组 `tupleObject` 中第 idx<sup>th</sup> 个（从零开始）字段的引用。索引被指定为该函数模板的非类型模板参数。

元组可以在不指定初始值的情况下构造。基本类型被初始化为零；类类型字段由其默认构造函数初始化。请注意，在某些情况下，元组的构造可能成功，但其使用可能失败。考虑：

```cpp
tuple<int &> empty;
cout << get<0>(empty);
```

这里元组 `empty` 无法使用，因为其 `int &` 字段是未定义引用。然而，empty 的构造是成功的。

如果两个元组的类型列表相同，则它们可以相互赋值；如果其组成类型支持，拷贝构造函数也可用。如果右侧类型可以转换为匹配的左侧类型，或者左侧类型可以由匹配的右侧类型构造，则拷贝构造和赋值也可用。只要元组的组成类型支持比较，就可以使用关系运算符比较元组（类型数量和（可转换的）类型均匹配）。在这方面，元组类似于 pair。

元组提供以下静态元素（使用编译期初始化）：

- `std::tuple_size<Tuple>::value` 返回为元组类型 `Tuple` 定义的类型数量。示例：
  ```cpp
  cout << tuple_size<tuple_idsc>::value << '\n';  // displays: 4
  ```
- `std::tuple_element<idx, Tuple>::type` 返回 `Tuple` 中元素 `idx` 的类型。示例：
  ```cpp
  tuple_element<2, tuple_idsc>::type text;  // defines std::string text
  ```

解包运算符也可用于将构造函数的参数转发给元组数据成员。考虑一个定义为可变参数模板的类 `Wrapper`：

```cpp
template <typename ...Params>
class Wrapper
{
    ...
public:
    Wrapper(Params &&...params);
};
```

可以为该类提供一个元组数据成员，该成员应使用通过完美转发初始化 `Wrapper` 类对象时所用的类型和值来初始化。与类可以从其模板类型继承的方式类似（参见第 21.5.3 节），它可以将自己的类型和构造函数参数转发给其元组数据成员：

```cpp
template <typename ...Params>
class Wrapper
{
    std::tuple<Params...> d_tuple;    // same types as used for
                                      // Wrapper itself

public:
    Wrapper(Params &&...params)
        :                               // initialize d_tuple with
                                        // Wrapper’s arguments
        d_tuple(std::forward<Params>(params)...)
    {}
};
```

## 21.7 计算函数对象的返回类型（C++11）

正如第 19 章充分说明的那样，函数对象在泛型算法中扮演着重要角色。与泛型算法本身一样，函数对象也可以泛型地定义为类模板的成员。如果这些类的函数调用运算符（`operator()`）定义了参数，那么也可以通过将函数调用运算符本身定义为成员模板来抽象这些参数的类型。示例：

```cpp
template <typename Class>
class Filter
{
    Class obj;
public:
    template <typename Param>
    Param operator()(Param const &param) const
    {
        return obj(param);
    }
};
```

模板类 Filter 是 Class 的包装器，它通过自己的函数调用运算符过滤 Class 的函数调用运算符。在上面的示例中，Class 的函数调用运算符的返回值只是被直接传递，当然也可以进行任何其他处理。

被指定为 Filter 模板类型参数的类型当然可以有多个函数调用运算符：

```cpp
struct Math
{
    int operator()(int x);
    double operator()(double x);
};
```

现在可以使用 Filter<Math> fm 来过滤 Math 对象，具体使用 Math 的第一个还是第二个函数调用运算符取决于实际参数类型。使用 fm(5) 时会调用 int 版本，使用 fm(12.5) 时会调用 double 版本。

遗憾的是，如果函数调用运算符具有不同的返回类型和参数类型，这种方案就不起作用。因此，下面的类 Convert 不能与 Filter 一起使用：

```cpp
struct Convert
{
    double operator()(int x);        // int-to-double
    std::string operator()(double x); // double-to-string
};
```

这个问题可以通过 C++11 标准定义的类模板 std::result_of<Functor (Typelist)> 成功解决。使用 std::result_of 之前，必须包含头文件 <functional>。

result_of 类模板提供了一个 typedef（type），表示 Functor<TypeList> 返回的类型。可以如下使用它来改进 Filter 的实现：

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

使用这个定义，可以构造 `Filter<Convert> fc`。现在 `fc(5)` 返回 `double`，而 `fc(4.5)` 返回 `std::string`。

类 `Convert` 必须定义其函数调用运算符与返回类型之间的关系。预定义的函数对象（例如标准模板库中的那些）已经这样做了，但自定义的函数对象必须显式地这样做。

如果一个函数对象类只定义一个函数调用运算符，它可以通过 `typedef` 定义其返回类型。如果上面的类 `Convert` 只定义其两个函数调用运算符中的第一个，那么该 `typedef`（在类的 `public` 部分中）应为：

```cpp
typedef double type;
```

如果定义了多个函数调用运算符，每个都有自己的签名和返回类型，那么签名与返回类型之间的关联按如下方式建立（均在类的 `public` 部分中）：

- 像这样定义一个泛型结构体 `result`：
  ```cpp
  template <typename Signature>
  struct result;
  ```
- 为每个函数调用签名定义 `struct result` 的一个*特化*。`Convert` 的第一个函数调用运算符产生：
  ```cpp
  template <typename Class>
  struct result<Class(int)>
  {
      typedef double type;
  };
  ```
  而 `Convert` 的第二个函数调用运算符产生：
  ```cpp
  template <typename Class>
  struct result<Class(double)>
  {
      typedef std::string type;
  };
  ```
- 在函数调用运算符有多个参数的情况下，这些声明规范应再次提供正确的签名。一个以 `int` 和 `double` 调用、返回 `size_t` 的函数调用运算符得到：
  ```cpp
  template <typename Class>
  struct result<Class(int, double)>
  {
      typedef size_t type;
  };
  ```

## 21.8 实例化类模板

当定义类模板的对象时，类模板会被实例化。当定义或声明类模板对象时，必须显式指定其模板参数。

当指定默认模板参数值时，也*会*指定模板参数，尽管在这种情况下编译器会提供默认值（参见第 21.4 节，其中 `double` 被用作
