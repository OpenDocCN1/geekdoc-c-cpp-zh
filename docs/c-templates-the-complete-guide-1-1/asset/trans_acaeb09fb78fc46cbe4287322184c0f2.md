
```cpp
throw NotEqualityComparable();
}

});
```

最后，通过在我们的 `SpecificFunctionProvider` 实现中使用 `TypeEqualityWithin`，我们可以在 `Function<>` 中为 `==` 提供支持，前提是存储的函数对象和该函数对象支持……

[点击此处查看代码图片](#)

```cpp
virtual bool equals(FunctionType& f, Arg... const& fb)
const override {
  if (auto spec = dynamic_cast<SpecificFunction<Foo...>&>(
      ...)) {
    return TypeEqualityFunction::equals(function,
      specificFunction);
  }
}

// Functions with different types are never equal:
return false;
```

### 22.6 性能考量

类型擦除提供了静态多态和动态多态的一些优点，但并非全部。特别是，使用类型擦除生成的代码的性能往往低于动态多态，因为两者都依赖通过虚函数进行的动态分发。因此，静态多态的一些传统优势——速度，例如编译器内联调用的能力——可能会丧失。这种性能损失是否可感知取决于具体应用，但通常很容易通过考虑被调用函数所执行的工作量与虚函数调用成本的相对关系来判断：如果两者相近（例如，使用 `Function<>` 简单地将两个整数相加），类型擦除的执行速度可能远比静态多态版本慢。另一方面，如果函数调用执行了大量工作——查询数据库、排序大型输入或更新用户界面——类型擦除的开销不太可能被测量到。

### 22.7 后记

Kevlin Henney 通过引入 `Any` 类型（`Boost.Any`/`boost::any`）在 C++ 中普及了类型擦除，该类型后来成为流行的 Boost 库（`Boost.Any`），并随 C++17 成为 C++ 标准库的一部分。这一技术在 Boost.Function 库中得到了些许改进，该库应用了虚函数和类型擦除操作，最终成为 `std::function`。然而，早期的每个库都只处理一组操作：`any` 是一个简单的值类型，只支持复制操作和一组仅限于调用的操作。

后来的努力，例如 Boost.TypeErasure 库（`Boost.TypeErasure`）和 Adobe 的 Poly 库（`AdobePoly`），应用模板元编程技术，允许用户形成具有指定能力列表的类型安全值。例如，以下使用 Boost.TypeErasure 库构造的类型处理任意构造、类似类型擦除的判据以及用于打印的输出流：

[点击此处查看代码图片](#)

```cpp
using AnyIterable = any<
  boost::type_erasure::copy_constructible<>,
  typeid_<>,
  ostreamable
>;
```

- 1. 将 `invoke()` 设为 `const` 是一种安全措施，防止通过 `const` 调用非 `const` 的 `operator()` 重载。
- 2. 尽管该类型可以通过从一个元素到另一个元素的动态转换进行复制，但 `Function<>` 类将 `bridge` 指针设为私有，因此 `Function<>` 的客户端无法访问该类型本身。
- 3. 在机制上，调用 `operator()` 的代码会因它是类模板（此处为 `SpecificFunction<>`）的虚函数而被实例化，因此通常实例化类模板本身就会导致该代码被实例化。

## 第23章

## 元编程

元编程包括“对程序进行编程”。换句话说，我们编写代码，由编程系统执行这些代码来生成实现我们真正想要的功能的新代码。通常，术语“元编程”暗示一种自反属性：元编程组件是程序的一部分，它为程序生成一小段代码（即程序的一个附加或不同的部分）。

为什么需要元编程？与大多数其他编程技术一样，其目标是以更少的努力实现更多的功能，其中努力可以量化为代码大小、维护成本等。元编程的特点是某些用户定义的计算发生在编译期。其根本动机通常是性能（在编译期计算的内容通常可以被优化掉）或接口简洁性（元编程通常比运行时方法更容易适应）。

元编程通常依赖于第19章中描述的 traits 和类型函数的概念。因此，我们建议在深入学习本章之前，先熟悉那一章。

### 23.1 现代 C++ 元编程的现状

C++ 元编程技术随着时间的推移而发展（本章末尾的后记详细介绍了这一演变过程）。让我们讨论并分类现代 C++ 中常用的各种元编程方法。

### 23.1.1 值元编程

在本书的第一版中，我们仅限于最初 C++ 标准（1998 年发布，2003 年有小幅修正）引入的特性。在那个时代，编写简单的编译期（“元”）计算就有点挑战性。因此，我们用本章的很大一部分来专门处理这件事；其中一个相当高级的示例使用递归模板实例化在编译期计算整数值的平方根。如第22页第1.2.4节所介绍，C++11，尤其是 C++14，通过引入 constexpr 函数消除了大部分这种挑战。例如，自 C++14 起，可以轻松地编写一个编译期函数来计算平方根，如下所示：

点击此处查看代码图片

```cpp
meta/sqrtconstexpr.hpp

template<typename T>
constexpr T sqrt(T x)
{
    // handle cases where x and its square root are equal as a special case to simplify
    // the iteration criterion for larger x:
    if (x <= 1) {
        return x;
    }

    // repeatedly determine in which half of a [lo, hi] interval the square root of x is located,
    // until the interval is reduced to just one value:
    T lo = 0, hi = x;
    for (;;) {
        auto mid = (hi+lo)/2, midSquared = mid*mid;
        if (midSquared <= x && (mid+1)*(mid+1) > x) {
            return mid;
        }
        // continue with the bigger half of the interval:
        if (midSquared < x) {
            lo = mid;
        } else {
            hi = mid;
        }
    }
}
```

该算法通过反复将包含 x 平方根的区间减半来搜索答案（将 0 和 1 的根作为特殊情况处理，以简化收敛判据）。这个 sqrt() 函数可以在编译期或运行期求值。

点击此处查看代码图片

```cpp
static_assert(sqrt(25) == 5, "");       // evaluated at compile time
static_assert(sqrt(4) == 2, "");        // evaluated at compile time

std::array<int, sqrt(40)> arr;           // declares array of 6 elements (compile time)
```

点击此处查看代码图片

```cpp
long long t = 53478;
std::cout << sqrt(t) << '\n';             // prints 231
```

这个函数的实现可能在编译期不是最高效的（在编译期利用机器的特性往往很有效），但因为它旨在执行编译期计算，绝对效率不如可移植性重要。注意，在平方根示例中，没有任何关于模板魔法的建议，只有函数模板通常的模板实参推导。这段代码是“纯 C++”，写起来并不特别具有挑战性。

正如我们上面所做的，值元编程（即对编译期值的计算进行编程）偶尔非常有用，但使用现代 C++（例如 C++14 和 C++17）还可以执行另外两种元编程：类型元编程和混合元编程。

### 23.1.2 类型元编程

在第19章讨论 traits 时，我们已经遇到了一种类型计算形式。在第5章中，这些 traits 接受一个类型并从中产生一个新类型。例如，上一章中的 RemoveReference trait 会移除引用类型。然而，我们在第5章中开发的示例仅包含相当基本的类型操作。通过依赖递归模板实例化——基于模板的元编程的支柱——我们可以执行更复杂得多的类型计算。

考虑以下小例子：

点击此处查看代码图片

```cpp
src/meta/removeallextents.hpp

// primary template: in general we yield the given type

template<typename T>
struct RemoveAllExtent {
    using Type = T;
};

// partial specializations for array types (with and without size)
template<typename T, std::size_t SZ>
struct RemoveAllExtent<T[SZ]> {
    using Type = typename RemoveAllExtent<T>::Type;
};

template<typename T>
struct RemoveAllExtent<T[]> {
    using Type = typename RemoveAllExtent<T>::Type;
};

template<typename T>
using RemoveAllExtents = typename RemoveAllExtent<T>::Type;
```

