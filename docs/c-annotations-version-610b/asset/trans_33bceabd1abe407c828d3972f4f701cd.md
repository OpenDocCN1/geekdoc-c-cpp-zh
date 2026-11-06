
```cpp
struct MultiBase<nr, PolicyT1, PolicyTypes...> :
    public UWrap<nr, PolicyT1>,
    public MultiBase<nr + 1, PolicyTypes...>
{
    typedef PolicyT1 Type;
    typedef MultiBase<nr + 1, PolicyTypes...> Base;

    MultiBase(PolicyT1 &&policyt1, PolicyTypes &&...policytpes)
    :
        UWrap<nr, PolicyT1>(std::forward<PolicyT1>(policyt1)),
        MultiBase<nr + 1, PolicyTypes...>(
            std::forward<PolicyTypes>(policytpes)...)
    {}
};
```

### 22.9.3 支持模板

Multi 类模板将 PlainTypes 定义为保存其参数包中所有类型的 TypeList。每个派生自 UWrap 类型的 MultiBase 还定义了一个类型 Type，表示用于定义该 UWrap 类型的策略类型，以及一个类型 Base，表示其嵌套 MultiBase 类的类型。

这三个类型定义使我们能够访问创建 Multi 对象时所用的类型，以及这些类型的值。

类模板 typeAt 是一个纯模板元编程类模板（它没有运行时执行代码）。它期望一个 size_t idx 模板实参，用于指定 Multi 类型对象中策略类型的索引，以及一个 Multi 类类型。它将类型 Type 定义为 Multi 的 MultiBase<idx, ...> 基类所定义的 Type。例如：

```cpp
typeAt<0, Multi<Vector, int, double>>::Type  // Type is vector<int>
```

类模板 typeAt 定义（并使用）一个完成所有工作的嵌套类模板 PolType。PolType 的泛型定义指定两个模板参数：一个用于指定所请求类型索引的索引，以及一个由 MultiBase 类型实参初始化的 typename。PolType 的递归定义递归地减小其索引非类型参数，并将 MultiBase 继承树中的下一个基类传递给递归调用。由于 PolType 最终将类型 Type 定义为所请求的策略类型，因此递归定义将其 Type 定义为递归调用所定义的类型。最后（非递归）的特化将 MultiBase 类型的初始策略类型定义为 Type。下面是 typeAt 的定义：

```cpp
template <size_t index, typename Multi>
class typeAt
{
    template <size_t idx, typename MultiBase>
    struct PolType;

    template <size_t idx,
              size_t nr, typename PolicyT1, typename ...PolicyTypes>
    struct PolType<idx, MultiBase<nr, PolicyT1, PolicyTypes...>>
    {
        typedef typename PolType<
            idx - 1, MultiBase<nr + 1, PolicyTypes...>>::Type Type;
    };

    template <size_t nr, typename PolicyT1, typename ...PolicyTypes>
    struct PolType<0, MultiBase<nr, PolicyT1, PolicyTypes...>>
    {
        typedef PolicyT1 Type;
    };

public:
    typeAt(typeAt const &) = delete;
    typedef typename PolType<index, typename Multi::Base>::Type Type;
};
```

Multi 的参数包所指定的类型也可以使用第二个辅助类模板来获取：plainTypeAt。例如：

```cpp
plainTypeAt<0, Multi<Vector, int, double>>::Type // Type is int
```

类模板 plainTypeAt 使用与 typeAt 类似（但更简单）的实现。它也是一个纯模板元编程类模板，定义了一个嵌套类模板 At。At 的实现类似 typeAt，但它访问的是传递给 Multi 的原始模板包中的类型，并由 Multi 以其 PlainTypes 类型提供。下面是 plainTypeAt 的定义：

```cpp
template <size_t index, typename Multi>
class plainTypeAt
{
    template <size_t idx, typename List>
    struct At;

    template <size_t idx, typename Head, typename ...Tail>
    struct At<idx, TypeList<Head, Tail...>>
    {
        typedef typename At<idx - 1, TypeList<Tail...>>::Type Type;
    };

    template <typename Head, typename ...Tail>
    struct At<0, TypeList<Head, Tail...>>
    {
        typedef Head Type;
    };

public:
    plainTypeAt(plainTypeAt const &) = delete;
    typedef typename At<index, typename Multi::PlainTypes>::Type Type;
};
```

可以说最简洁的辅助模板是 get。这是一个函数模板，将 size_t idx 定义为其第一个模板参数，将 typename Multi 定义为其第二个模板参数。函数模板 get 定义一个函数参数：一个到 Multi 的引用，因此它可以自行推导出 Multi 的类型。知道它是 Multi 后，我们推断它也是 UWrap<nr, PolicyType>，因而也是 PolicyType，因为后一个类被定义为 UWrap 的基类。

由于类类型对象可以初始化对其基类的引用，因此 PolicyType & 可以由适当的 UWrap 引用初始化，而该引用又可以由 Multi 对象初始化。由于我们可以使用 typeAt 确定 PolicyType（注意，求值 typename typeAt<idx, Multi>::Type 完全是编译期的事情），所以 get 函数完全可以通过单个 return 语句内联实现：

```cpp
template <size_t idx, typename Multi>
inline typename typeAt<idx, Multi>::Type &get(Multi &multi)
{
    return static_cast<
        UWrap<idx, typename typeAt<idx, Multi>::Type> &>(multi);
}
```

### 22.9.4 使用 Multi

既然 Multi 及其支持模板已经开发完成，那么如何使用 Multi 呢？

有必要先提醒一句。为了减小所开发类的体积，它们是以极简方式设计的。例如，get 函数模板不能用于 Multi const 对象，而且 Multi 类型没有可用的默认构造函数或移动构造函数。Multi 旨在说明模板元编程的一些可能性，希望 Multi 的实现很好地服务了这一目的。但它能使用吗？如果能，又该如何使用？

本节提供一些带注释的示例。它们可以串联起来定义一系列语句，这些语句可以放在 main 函数体中，从而构成一个可运行的程序。

- 可以定义一个简单的 Policy：

  ```cpp
  template <typename Type>
  struct Policy
  {
      Type d_type;
      Policy(Type &&type)
      :
          d_type(std::forward<Type>(type))
      {}
  };
  ```

  Policy 定义了一个数据成员，并且可用于定义 Multi 对象：

  ```cpp
  Multi<Policy, string> ms(Policy<string>("hello"));
  Multi<Policy, string, string> ms2s(Policy<string>("hello"),
                                     Policy<string>("world"));
  ```

  ```cpp
  typedef Multi<Policy, string, int> MPSI;
  MPSI mpsi(string("hello"), 4);
  ```

- 要获取 Multi 类或对象所定义的类型数量，可以使用 ::size 枚举值（使用 Multi 类），或使用 .size 成员（使用 Multi 对象）：

  ```cpp
  cout << "There are " << MPSI::size << " types in MPSI\n"
       << "There are " << mpsi.size << " types in mpsi\n";
  ```

- 可以使用 plainTypeAt 定义构成类型的变量：

  ```cpp
  plainTypeAt<0, MPSI>::Type sx = "String type";
  plainTypeAt<1, MPSI>::Type ix = 12;
  ```

- 可以使用原始 static_cast 来获取构成类型：

  ```cpp
  cout << static_cast<Policy<string> &>(mpsi).d_type << '\n'
       << static_cast<Policy<int> &>(mpsi).d_type << '\n';
  ```

- 然而，当模板参数包包含相同类型时，这种方法行不通，因为强制转换无法区分相同的 Policy<int> 类型。在这种情况下，get 仍然可以正常工作：

  ```cpp
  typedef Multi<Policy, int, int> MPII;
  MPII mpii(4, 18);

  cout << get<0>(mpii).d_type << ' ' << get<1>(mpii).d_type << '\n';
  ```

- 下面是一个将 `std::vector` 包装在 `Vector` 中的示例：

  ```cpp
  typedef Multi<Vector, int, double> MVID;
  MVID mi({1, 2, 3}, {1.2, 3.4, 5.6, 7.8});
  ```

- 这样的 vector 可以通过其 `Multi` 类型来定义：

  ```cpp
  typeAt<0, Multi<Vector, int>>::Type vi = {1, 2, 3};
  ```

- 已知 `Vector` 是 `std::vector`，`get` 返回的引用支持下标运算符，可用作左操作数或右操作数：

  ```cpp
  cout << get<0>(mi)[2] << '\n';
  get<1>(mi)[3] = get<0>(mi)[0];
  cout << get<1>(mi)[3] << '\n';
  ```
