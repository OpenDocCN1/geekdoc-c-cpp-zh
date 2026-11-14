

> "灰色，亲爱的朋友，是一切理论，而绿色是生命之树的金色。"¹⁷
> 
> —约翰·沃尔夫冈·冯·歌德

17. 作者译本。“Grau, teurer Freund, ist alle Theorie und grün des Lebens goldner Baum.”

在前面的章节中，你可能会产生这样的印象：模板参数可以被任何类型替代。但实际上并非完全如此。模板类和函数的程序员会对可在模板参数上执行的操作做出假设。

因此，了解哪些参数类型是可接受的非常重要。例如，我们已经看到，清单 3-4 中的 accumulate 可用于 int 或 double 的向量或列表。但是，像文件流这样不支持加法的值类型不能与 accumulate 一起使用。那么，应该从一组文件中累积什么呢？

因此，我们必须找出潜在参数类型所需的要求集合。这样的集合称为概念。一个包含概念 c 的所有要求以及可能的额外要求的概念 CR，称为 c 的细化。在标准中，这称为子含：CR 子含 c。然而，子含的定义更为一般：概念 c2 子含 c1，并不一定意味着 c2 的定义包含 c1 以及可能的更多要求。它的意思是，c2 中的要求集合是 c1 要求集合的超集（在进行适当重命名和其他等价转换后）。概念子含的正式规范见标准 [39, §13.5.4] 和在线参考资料。满足概念 c 的所有要求的类型 t，称为 c 的模型。关于子含：如果 c2 子含 c1，则 c2 的模型是 c1 模型的子集。

概念可以包含纯粹的语法要求，例如某个类型参数必须具有拷贝构造函数或 operator+。语义要求指定一个强制属性，例如加法的交换律：x + y = y + x ∀ x, y。

在 C++20 之前，概念仅存在于文档中（如果有的话），泛型函数和类的用户有责任满足模板参数的所有要求。如果违反了语法要求，用户例如会看到编译器关于缺少函数的报错。不幸的是，这种情况常常发生在实例化某些与程序员无关的技术细节的内部实现时，位于巨大的函数调用栈深处。因此，除了无法实例化的内部代码的作者之外，这些错误信息对任何人都不太有意义。编译器在冗长的消息中提供调用栈和包含栈，这更多是让程序员感到畏惧而非启发。然而，语法错误始终会被编译器捕获——尽管不一定以有帮助的方式报告。另一方面，语义错误对编译器来说是不可检测的。

现在，通过 C++20，我们可以将概念作为程序的一部分来表达。使用概念有以下几个优势：

- 未满足的要求已在被调用的函数中检测到。
  - 而非深入实现内部。
  - 这会显著缩短错误信息。
- 错误信息通常更有意义。
- 可以检测语义错误。
- 可以根据类型属性对函数进行分发。

到目前为止，只有语法要求可以直接表达，但我们可以模拟语义概念，如我们稍后将演示的那样（第 5.5 节）。在以前，基于类型属性的分发已经可以通过元编程技巧实现，但概念使实现变得简单得多且更易读。

### 3.10.1 定义概念

```
=> c++20/concept_accumulate_syntactic.cpp
```

在清单 3-4 中，我们实现了一个适用于可加值类型的数组和列表的泛型求和。此外，它可以用于任何一对迭代器，只要它们的值可读且可以加到初始值的类型上。这些类型要求将在概念 Summable 中实现，因为这是我们函数所需要的：

点击此处查看代码图像

```cpp
template <typename Iter, typename Value>
Value accumulate(Iter first, Iter last, Value init)
requires Summable<Iter, Value>
{
    for (; first != last; ++first)
        init += *first;
    return init;
}
```

The `requires` 子句可以像我们这样插入在函数头之后，也可以插入在模板参数列表之后：

点击此处查看代码图像

```cpp
template <typename Iter, typename Value>
requires Summable<Iter, Value>
Value accumulate(Iter first, Iter last, Value init);
```

现在，我们的函数受 *受约束的* 于我们概念 `Summable` 的模型，我们最终应该实现它。它应该包含什么？

- 类型 `Iter` 应该是：
  - 可比较的；
  - 可递增的；以及
  - 间接可读的，即 `operator*` 的结果应当可读。
- 类型 `Value` 应该是可拷贝的，以便返回结果。
- `Iter` 上 `operator*` 的结果应当可以加到 `Value`。

这些要求在以下概念中实现：

点击此处查看代码图像

```cpp
template <typename Iter, typename Value>
concept Summable=
    requires (Iter it, Value init)
{
    requires std::input_iterator<Iter>;
    requires std::is_copy_constructible_v<Value>;
    Value{init}; // Attempt a copy
    init += *it;
};
```

我们的 `concept` 以熟悉的模板参数及其名称开头。接下来的 `requires` 子句是可选的，这里用于引入概念中使用的变量名称。或者，我们可以使用 `declval` 即时创建它们，但这会显著冗长且可读性较低。

对 `Iter` 的要求已由标准概念 `input_iterator` 实现，我们在概念的第一行中请求它。`Value` 的拷贝能力可以通过类型特征 `is_copy_constructible` 进行测试，或者更简洁地使用变量 `is_copy_constructible_v`。在编译时已知的 `bool` 类型模板变量——即声明为 `constexpr` 的变量——可以直接在 `requires` 子句中像概念一样使用。反之，概念可以像类型依赖的 `bool` 常量一样使用。

最后两个要求是包含占位符对象的表达式。自然，当该表达式可以编译时，此类要求即被满足。倒数第二个要求是表达对拷贝构造函数需求的另一种形式，即请求从 `init` 创建副本的可编译性。最后一行要求 `operator+=` 可以应用于 `init` 和解引用的 `it`。我们受约束的函数会接受一个仅可移动而不可拷贝的 `Value` 类型吗：

点击此处查看代码图像

```cpp
struct uncopyable
{
    uncopyable(int v) : v(v) {}
    uncopyable(const uncopyable&) = delete;
    uncopyable(uncopyable&&) = default;

    uncopyable& operator+=(const uncopyable& rhs) &
    {
        v += rhs.v;
        return *this;
    }
    operator int() const { return v; }
    int v;
};
```

不会。与无约束的模板函数相反。因此，也许我们不应该请求拷贝构造函数，而应该请求移动构造函数：

点击此处查看代码图像

```cpp
template <typename Iter, typename Value>
concept Summable=
    requires (Iter it, Value init)
    {
        requires std::input_iterator<Iter>;
        requires std::is_move_constructible_v<Value>;
        Value(std::move(init));
        init += *it;
    };
```

同样，第二和第三个要求是等价的，用以说明实现选项。现在我们可以累积不可拷贝值的范围。那么，一个不可移动但可拷贝的类型呢：

点击此处查看代码图像

```cpp
struct unmovable
{
    unmovable(const unmovable&) = default;
    unmovable(unmovable&&) = delete;
    // ... remainder like uncopyable
};
```

它适用于我们的第一个概念版本，但不适用于第二个。我们希望有一个适用于可拷贝或可移动类型的概念。为简洁起见，我们称其为 Returnable：

点击此处查看代码图像

```cpp
template <typename T>
concept Returnable=
    std::is_move_constructible_v<T>
    || std::is_copy_constructible_v<T>;

template <typename Iter, typename Value>
concept Summable=
    requires (Iter it, Value init)
    {
        requires std::input_iterator<Iter>;
        requires Returnable<Value>;
        init += *it;
    };
```

使用我们最后一个版本的 Summable，受约束的 accumulate 函数与其无约束的对应物一样通用。然而：

