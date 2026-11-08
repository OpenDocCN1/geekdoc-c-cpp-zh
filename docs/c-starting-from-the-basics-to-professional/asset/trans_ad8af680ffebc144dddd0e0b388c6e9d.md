
然而，为成员函数的 const 和非 const 重载引入重复定义被视为不良实践。这是通常所谓的代码重复的一个具体实例。由于避免代码重复是确保代码保持可维护性的关键，因此在继续讨论最后一个类成员模板——赋值运算符的模板——之前，我们会再稍微思考一下这个问题。

### 代码重复

多次编写相同或相似的代码很少是好主意。这不仅浪费时间，而且这种所谓的重复代码由于多种原因而不可取——最值得注意的是，它会削弱代码库的可维护性。需求会演变，会获得新的认识，也会发现缺陷。因此，代码在编写完成之后往往需要多次调整。此时，存在重复的代码片段就意味着你必须始终记得调整同一代码的所有副本。请相信我们，这简直是维护噩梦！避免代码重复的原则也称为“不要重复自己”（Don't Repeat Yourself，DRY）原则。

即使重复的代码只有几行，通常也值得重新考虑。例如，考虑我们刚刚为 `Array<>` 模板提出的重复 `operator[]()` 模板。现在想象你想更改抛出的异常类型，或者更改传递给异常的消息。那么你就必须在两个地方进行更改。这不仅繁琐，而且非常容易忘记其中一个重复项——尤其当这是别人编写的代码，或者你已经不记得其细节时。不幸的是，这种情况在实践中经常发生；对重复代码的更改或缺陷修复只在一个或部分重复项中进行，而其他重复项仍然保留着最初现已不正确的版本。如果每一段逻辑在代码库中只出现一次，这种情况就不会发生！

好消息是，你已掌握对抗代码重复所需的大多数工具。函数是可复用的计算块，模板会针对任意数量的类型实例化为函数或类，基类封装其派生类的所有共同之处，等等。所有这些机制正是为了确保你不必重复自己而创建的！

消除成员函数 const 和非 const 重载之间代码重复的传统方法是，用其 const 对应版本来实现非 const 版本。虽然这在原则上听起来足够简单，但生成的代码一开始可能——不，一定会——显得令人生畏。所以请做好准备。例如，对于我们的 `operator[]()` 模板，该习语的经典实现如下所示：

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    return const_cast<T&>(static_cast<const Array<T>&>(*this)[index]);
}
```

哎哟！我们警告过你会变得吓人，不是吗？好消息是，C++17 引入了一个小助手模板 `std::as_const()`，可以让这段代码更容易接受：

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    return const_cast<T&>(std::as_const(*this)[index]);
}
```

不过，既然这是你第一次遇到这个习语，让我们把这个仍然不明显的 return 语句重写成几个更小的步骤。这将有助于我们解释发生了什么：

```cpp
template <typename T>
T& Array<T>::operator[](size_t index)
{
    Array<T>& nonConstRef = *this;                    // Start from a non-const ref
    const Array<T>& constRef = std::as_const(nonConstRef); // Convert to const ref
    const T& constResult = constRef[index];           // Obtain the const result
    return const_cast<T&>(constResult);               // Convert to non-const result
}
```

因为这个模板生成非 const 成员函数，所以 `this` 指针具有指向非 const 类型的指针类型。因此在我们的例子中，解引用这个指针会得到 `Array<T>&` 类型的引用。我们需要做的第一件事是给这个类型加上 const。从 C++17 起，可以使用标准库 `<utility>` 模块中定义的 `std::as_const()` 函数模板来完成。给定 `T&` 类型的值，该模板的实例会生成 `const T&` 类型的值。

一旦我们有了指向 const 的引用，我们只需用同一组参数再次调用重载函数。在我们的例子中，我们再次用相同的 `size_t` 参数 `index` 调用 `[]` 运算符函数。唯一的区别是，这次我们通过指向 const 的引用变量来调用重载函数，这意味着会调用该函数的 const 重载——`operator[](size_t) const`。如果我们没有先给 `*this` 的类型加上 const，我们就只是再次调用同一个函数，这会触发无限递归。

因为我们现在在一个 const 对象上调用该函数，所以它通常也会返回对 const 元素的引用。如果不是这样，就会破坏 const 正确性。但我们需要的是对非 const 元素的引用。因此在最后一步，我们必须在从函数返回结果之前去掉结果的 const 属性。而在 C++ 中移除 const 的唯一（干净）方式是使用 `const_cast<>`（见第 12 章）。

套用 J. R. R. 托尔金的话，我们建议将这个习语称为“const 去而复返”。你先从非 const 转到 const（使用 `std::as_const`），然后再回到非 const（使用 `const_cast<>`）。请注意，这个习语是少数实际推荐使用 `const_cast<>` 的情形之一。一般来说，去掉 const 属性被视为不良实践。但使用“const 去而复返”习语消除代码重复，是这条规则被广泛接受的例外。

> **提示**  使用“const 去而复返”习语来避免成员函数 const 和非 const 重载之间的代码重复。一般来说，它的工作方式是使用以下模式，用成员的 const 对应版本实现其非 const 重载：
>
> ```cpp
> ReturnType MyClass::myFunction(Arguments)
> {
>     return const_cast<ReturnType>(std::as_const(*this).myFunction(Arguments));
> }
> ```

## 赋值运算符模板

赋值运算符可以如何工作，存在不止一种可能性。操作数必须是具有相同 `T` 的同一 `Array<T>` 类型，但这并不妨碍它们具有不同的值。你可以这样实现赋值运算符：只要可能，就让左操作数的 `m_elements` 成员保留相同的值。也就是说，如果右操作数的元素比左操作数少，你可以只从右操作数复制足够的元素来填充左操作数数组的部分内容。然后，你可以让多余的元素保留其原始值，或者将它们设置为由默认 `T` 构造函数生成的值。

不过，为保持简单，我们只会让左操作数始终分配一个新的 `m_elements` 数组，即使先前的数组已经足够长，足以容纳右操作数元素的副本。为实现这一点，赋值运算符函数必须释放目标对象中分配的任何内存，然后执行复制构造函数所做的工作。为了确保赋值运算符不会 `delete[]` 自己的内存，它们必须首先检查对象是否不相同（见第 13 章）。以下是定义：

```cpp
template <typename T>
Array<T>& Array<T>::operator=(const Array& rhs)
{
    if (&rhs != this)             // If lhs != rhs
    {
        delete[] m_elements;     // ... do the assignment...
                                  // Release any free store memory

        m_size = rhs.m_size;      // Copy the members of rhs into lhs
        m_elements = new T[m_size];
        for (size_t i = 0; i < m_size; ++i)
            m_elements[i] = rhs.m_elements[i];
    }
    return *this;                  // ... return lhs
}
```

请记住，在这里检查以确保左操作数与右操作数不相同至关重要；否则，你会释放 `this` 所指向对象的 `m_elements` 成员的内存，然后在它不再存在时尝试将其复制给自身！这种形式的每个赋值运算符都必须以这样的安全检查开始。当操作数不同时，在创建右操作数的副本之前，要释放左操作数拥有的任何自由存储区内存。

> **注意**  你注意到我们在这里如何重复自己了吗？如果你错过了，也许可以再看一眼赋值运算符模板。该模板首先重复析构函数模板的逻辑，接着重复复制构造函数模板的逻辑。因此，我们在这里明显违反了 DRY 原则。但这并不是这个模板唯一有问题的地方，我们将在接下来的边栏中解释。不过好消息是，你可以使用所谓的*复制并交换习语*一次性解决这两个问题。
