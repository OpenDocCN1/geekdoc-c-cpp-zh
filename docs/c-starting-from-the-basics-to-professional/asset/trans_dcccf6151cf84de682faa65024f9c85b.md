

**警告** 当通过右值引用传递像 `element` 这样的参数时，永远不要忘记在函数体内，表达式 `element` 又是一个左值。记住，任何命名变量都是左值，即使该变量本身具有右值引用类型！在我们的 `push_back()` 示例中，这意味着函数体中的 `std::move()` 非常有必要，它能迫使编译器选择 T 的移动赋值运算符而不是其复制赋值运算符。

## 按值传递的回归

移动语义的引入已经导致了你在某些函数的参数定义方式和应有方式上的重大转变。在 C++11 之前，生活很简单：为了避免复制，你只需始终通过引用传递对象，正如我们在第 8 章中教你的那样。然而，既然移动语义的支持已经很普遍，按引用传递就不再总是你的最佳选择。事实上，事实证明按值传递参数重新回到了考虑范围，至少在某些特定情况下如此。为了解释何时以及为什么，我们将继续基于刚才的同一个 `push_back()` 示例进行构建。

在上一小节中，我们创建了两个独立的 `push_back()` 重载，一个用于 `const T&` 引用，一个用于 `T&&` 引用。为了方便起见，你可以在 Ex18_05A 中找到此变体。虽然使用两个重载确实提供了一个可行的选项，但它确实意味着一些乏味的代码重复。解决这种重复的一种方法是根据 `T&&` 重载来重新定义 `const T&` 重载，如下所示：

```cpp
template <typename T>
void Array<T>::push_back(const T& element)
{
    push_back(T{ element });        // Create a temporary, transient copy and push that
}
```

但还有一种更好、更紧凑的方式，只需要一个函数定义。有点令人惊讶的是，这个单一的 `push_back()` 定义将使用按值传递。你可能永远也不会猜到可以用一个按值传递的单一定义来替换两个按引用传递的重载，但一旦你看到它的实际效果，你一定会欣赏这种方法纯粹的优雅。如果我们再次省略不相关的部分，你的新 `push_back()` 将如下所示：

```cpp
template <typename T>
void Array<T>::push_back(T element)    // Pass by value (copied lvalue, or moved rvalue!)
{
...
    newArray[m_size] = std::move(element); // Move the new element...
...
}
```

只要您只使用支持移动语义的类型（如标准库类型），此函数总是精确地执行您想要的操作。您传递什么类型的参数并不重要：左值参数会被复制一次，右值参数会被移动。因为函数参数是值类型 T，所以每当调用 `push_back()` 时都会创建一个类型为 T 的新对象。美妙之处在于，为了构造这个新的 T 对象，编译器将根据参数的类型使用不同的构造函数。如果函数的参数是左值，则使用 T 的复制构造函数构造 `element` 参数。然而，如果是右值，则将使用 T 的移动构造函数构造 `element`。

> **警告** 对于像 `Array<>` 这样的通用容器，你可能仍然需要考虑类型 `T` 不提供移动构造函数或赋值运算符的可能性。对于此类类型，按值接受 `T` 的变体实际上会将任何给定参数复制两次。请记住，除非 `T` 有移动赋值运算符，否则 `std::move()` 不会移动任何东西。如果没有，编译器将安静地回退到复制赋值运算符来求值 `newArray[m_size] = std::move(element)`。在现实世界中，像 `Array<>` 这样的容器因此很可能仍然会同时拥有 `push_back()` 的两个重载——一个用于左值，一个用于右值。
> 
> 在这里使用按值传递的唯一有趣之处在于，`push_back()` 总是且不可避免地要复制给定的左值。既然如此，复制无论如何都是不可避免的，你还不如在构造输入参数时就创建这个副本。当然，函数不需要复制的参数仍然应该通过 const 引用传递！

然而，对于本质上会复制任何左值输入的非模板函数来说，使用一个具有按值传递参数的单一函数几乎总是一种非常简洁的替代方案。具体的例子可以是具有如 `setNumbers(std::vector<double> values)` 或 `add(BigObject bigboy)` 签名的函数。传统的本能反应是使用 const 引用传递，但通过改为按值传递参数，你实际上可以一石二鸟。如果这样定义，同一个单一函数就可以以接近最优的性能同时处理左值和右值！

为了演示这确实有效，只需将我们在这里设计的 `push_back(T)` 函数添加到 Ex18_04 的 `Array<>` 模板中。既然 `Array<>` 支持 `push_back()`，那么将其构造函数的大小参数赋予默认值零也是有意义的：

```cpp
export template <typename T>
class Array
{
public:
  explicit Array(size_t size = 0);  // Constructor
  ...
  void push_back(T element);         // Add a new element (either copied or moved)
  // ...
};
```

所有其他成员都可以保持与 Ex18_04 中一样。有了这个，你可以编写以下示例程序（`buildStringArray()` 的定义也可以取自 Ex18_04）：

```cpp
// Ex18_05.cpp - Use of a pass-by-value parameter to pass by either lvalue or rvalue
import array;
import string;

// Construct an Array<> of a given size, filled with some arbitrary string data
Array<std::string> buildStringArray(const size_t size);

int main()
{
  Array<Array<std::string>> array_of_arrays;

  Array<std::string> array{ buildStringArray(1'000) };
  array_of_arrays.push_back(array);             // Push an lvalue

    array.push_back("One more for good measure");
    std::cout << std::endl;

    array_of_arrays.push_back(std::move(array));    // Push an rvalue
}
```

在 `main()` 中，我们创建了一个字符串的 `ArrayOfArrays`，恰当地命名为 `array_of_arrays`。我们首先将一个包含 1,000 个字符串的 `Array<>` 插入到这个容器中。这个 `Array<>` 元素，恰当地命名为 `array`，显然是作为左值被压入的，所以我们期望它被复制。这是一件好事：我们在程序的剩余部分仍然需要它的内容。在程序的最后，我们第二次添加 `array`，但这次我们首先通过对变量名应用 `std::move()` 将其转换为右值。我们这样做是希望 `Array<>` 及其 `string` 数组现在将被移动而不是复制。运行 `Ex18_05B` 证实了这确实是事实；总的来说，`array` 只被复制了一次。

```
Array of 1000 elements copied
Array of 1000 elements moved (assignment)
Array of 1001 elements moved (assignment)
```

各种移动赋值发生在 `push_back()` 函数体内。在将 `array` 作为左值添加和再次作为右值添加之间，我们向其中注入了一个额外的 `string`，以便能够在输出中区分两个 `Array<>` 元素。请注意，在推送这个额外的 `string` 的过程中，`array` 内部已有的 1,000 个 `string` 元素也不会被复制。它们都会通过 `std::string` 的移动赋值运算符被移动到一个更大的 `string` `Array<>` 中！

> **提示** 对于基本类型和指针，你可以直接使用按值传递。对于复制成本更高的对象，你通常应该使用 `const T&` 参数。这可以避免任何左值参数被复制，而且右值参数也能很好地与 `const T&` 参数绑定。然而，如果你的函数本质上要复制其 `T` 参数，那么你应该改为按值传递。这样，左值参数在传递给函数时会被复制，而右值参数会被移动。后一条准则假定参数类型支持移动语义——如今所有类型都应当如此。在不太可能的情况下，如果参数类型缺乏适当的移动成员，你应该坚持使用按引用传递。不过，如今越来越多的类型支持移动语义——尤其是所有标准库类型——所以按值传递无疑重新回到了考虑范围！

如果你使用调试构建或优化程度较低的编译器运行此示例，你可能会看到一些由 `Array<>` 的移动成员打印的额外输出。然而，即使如此，也应该只有一个数组被复制，这才是关键。

