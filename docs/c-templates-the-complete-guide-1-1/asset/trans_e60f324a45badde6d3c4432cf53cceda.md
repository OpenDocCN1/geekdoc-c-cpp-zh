
## 27.2.1 表达式模板的操作数

为了完整表示表达式，我们必须在每个 A_Add 和 A_Mult 对象中引用操作数，并获取 A_Add 或 A_Mult 对象中标量的值（或对它的引用）。以下是相应操作数的可能定义：

[点击此处查看代码图像](example/expression.cpp)

```cpp
#include <iostream>

#include <cassert>

// include helper class traits template to select whether
// expression template node either by value or by reference
#include "exprspecial.hpp"

// class for object that represent the addition of two operands
template<typename T, typename OP1, typename OP2>
class A_Add {
private:
    typename A_Traits<OP1>::ExprRef op1;    // first operand
    typename A_Traits<OP2>::ExprRef op2;    // second operand

public:
    // constructor initializes references to operands
    A_Add (OP1 const& a, OP2 const& b)
      : op1(a), op2(b) {
    }

    // compute sum when value requested
    T operator[] (std::size_t idx) const {
        return op1[idx] + op2[idx];
    }

    // compute size when requested
    std::size_t size() const {
        assert(op1.size()!=0 || op2.size()!=0
               || op1.size()==op2.size());
        return op1.size()!=0 ? op1.size() : op2.size();
    }
};

// class for object that represent the multiplication of two operands
template<typename T, typename OP1, typename OP2>
class A_Mult {
private:
    typename A_Traits<OP1>::ExprRef op1;    // first operand
    typename A_Traits<OP2>::ExprRef op2;    // second operand

public:
    // constructor initializes references to operands
    A_Mult (OP1 const& a, OP2 const& b)
      : op1(a), op2(b) {
    }

    // compute product when value requested
    constexpr auto operator[](std::size_t idx) const
    {
        return op1[idx] * op2[idx];
    }

    // size is maximum size
    std::size_t size() const
    {
        assert(op1.size() == 0 || op2.size() == 0
               || op1.size() >= op2.size());
        return op1.size() > op2.size() ? op1.size() : op2.size();
    }
};
```

如你所见，我们添加了下标操作和大小查询操作，使我们能够计算由以该对象为根的节点子树所表示的运算结果数组的大小和元素值。

对于仅涉及数组的运算，结果的大小是任一操作数的大小。然而，对于同时涉及数组和标量的运算，结果的大小是数组操作数的大小。为了区分数组操作数和标量操作数，我们将标量的大小定义为零。因此，A_Scalar 模板定义如下：

点击此处查看代码图像

`exprtmp/exprscalar.hpp`

```cpp
// class for objects that represent scalars
template<typename T>
class A_Scalar {
private:
    T const s;  // value of the scalar

public:
    // constructor initializes value
    constexpr A_Scalar(T const& v)
        : s(v) { }

    // for index operation, the scalar is the value
    constexpr T const& operator[](std::size_t) const
    {
        return s;
    }

    // scalars have zero as size
    constexpr std::size_t size() const
    {
        return 0;
    }
};
```

我们将构造函数和成员函数声明为 constexpr，以便该类可以在编译期使用。然而，就我们的目的而言，这并非严格必需。

注意，标量也提供下标运算符。在表达式内部，它们表示一个在每个索引处都具有相同标量值的数组。

你可能已经看到，运算符类使用了一个辅助类 A_Traits 来定义操作数的成员：

点击此处查看代码图像

`exprtmp/exprtraits.hpp`

```cpp
template <typename T>
struct A_Traits {
    using ExprRef = T const&;   // type to refer to
    using ExprT   = T const&;   // type to refer to
};
```

这是必要的，因为一般来说，我们可以将它们声明为引用，因为大多数临时节点绑定在顶层表达式中，因此会一直存活到该完整表达式的求值结束。唯一的例外是 A_Scalar 节点。它们绑定在……

换句话说，我们需要如下成员：

- **一般情况下是常量引用：**

    [点击此处查看代码图像](#)

    ```cpp
    OP1 const& op1;    // refer to first operand by reference
    OP2 const& op2;    // refer to second operand by reference
    ```

- **对标量使用普通值：**

    [点击此处查看代码图像](#)

    ```cpp
    OP1 op1;            // refer to first operand by value
    OP2 op2;            // refer to second operand by value
    ```

这是特性类的完美应用。该特性类定义了一个类型，在一般情况下是常量引用，但对于标量则是普通值：

[点击此处查看代码图像](#)

```cpp
template<typename T>
class A_Traits {
public:
    using ExprRef = T const&;    // type to refer to
};

// partial specialization for scalars
template<typename T>
class A_Traits<A_Scalar<T>> {
public:
    using ExprRef = A_Scalar<T>;   // type to refer to
};
```

注意，由于 A_Scalar 对象引用顶层表达式中的标量，这些标量可以使用引用类型。也就是说，A_Scalar<T> 是一个引用成员。

## 27.2.2 数组类型

借助使用轻量级表达式模板来编码表达式的能力，我们现在必须创建一个 Array 类型，它控制实际存储并了解表达式模板。然而，从工程角度来看，尽可能保持真实带存储数组的接口与表示生成数组的表达式的接口相似，也是有用的。为此，我们如下声明 Array 模板：

[点击此处查看代码图像](#)

```cpp
template<typename T, typename Rep = ArrayTraits<T>::Rep>
class Array;
```

类型 Rep 可以是 SArray 或存储数组。当然，它也可以是对表达式进行编码的嵌套模板，例如 A_Add 或……。无论哪种方式，我们处理的都是惰性实例化，这大大简化了我们后续的处理。事实上，甚至 Array 模板的定义也不需要特化来区分这两种情况，尽管某些成员不能为像 A_Mult（替换 Rep）这样的类型实例化。

下面是定义。其功能大致限于我们的 Array 模板所提供的功能，不过一旦理解了代码，就不难在该功能基础上进行添加：

[点击此处查看代码图像](#)

```cpp
#include <iostream>
#include <cassert>
#include "traits.hpp"

template<typename T, typename Rep = ArrayTraits<T>::Rep>
class Array {
private:
    Rep expr_rep; // (access to) the data of the array

public:
    // create array with initial size
    explicit Array (std::size_t n)
        : expr_rep(n) {
    }

    // create array from possible representation
    Array (Rep const& b)
        : expr_rep(b) {
    }

    // assignment operator for same type
    Array& operator= (Array const& b) {
        assert(size() == b.size());

        for (std::size_t i = 0; i < b.size(); ++i)
            expr_rep[i] = b[i];

        return *this;
    }

    // assignment operator for arrays of different types
    template<typename T2, typename Rep2>
    Array& operator= (Array<T2, Rep2> const& b) {
        assert(size() == b.size());

        for (std::size_t i = 0; i < b.size(); ++i)
            expr_rep[i] = b[i];

        return *this;
    }

    // size is size of represented data
    std::size_t size() const {
        return expr_rep.size();
    }

    // index operator for constants and variables
    decltype(auto) operator[] (std::size_t idx) const {
        assert(idx < size());
        return expr_rep[idx];
    }

    T& operator[] (std::size_t idx) {
        assert(idx < size());
        return expr_rep[idx];
    }

    // return what the array currently represents
    Rep const& rep() const {
        return expr_rep;
    }
};
```

同样，许多操作只是转发给底层的 Rep 对象。然而，当复制另一个数组时，我们必须考虑到另一个数组实际上可能构建在表达式模板之上的可能性。因此，我们根据底层的 Rep 表示来参数化这些复制操作。

因此，下标运算符值得稍作讨论。请注意，该运算符的核心版本使用推导返回类型，而不是更传统的类型特性语法。我们这样做是因为，如果 Rep 表示 A_Mult，其下标运算符会返回一个临时子表达式，而该子表达式不能通过引用返回（因而不能成为对它的引用）。如果我们决定不为右值结果使用引用类型，那么该运算符会产生一个 const 左值，而推导出的返回类型在这种情况下将是对应的 const 引用。

## 27.2.3 运算符

对于一元 Array 模板的高效数值运算符，我们大部分机制已经就绪，只差运算符本身。如前所述，这些运算符只组装表达式模板对象——它们并不实际求值结果数组。

对于每个相邻的二元运算符，我们必须实现三个版本：数组-数组、数组-标量和标量-数组。为了能够计算初始值，例如，我们需要以下运算符：

[点击此处查看代码图像](#)

```cpp
// addition of two Arrays

template<typename T, typename R1, typename R2>
Array<T, A_Add<T,R1,R2>>
operator+ (Array<T,R1> const& a, Array<T,R2> const& b)
{
    return Array<T, A_Add<T,R1,R2>>
        (A_Add<T,R1,R2>(a.rep(),b.rep()));
}

// multiplication of two Arrays

template<typename T, typename R1, typename R2>
Array<T, A_Mult<T,R1,R2>>
operator* (Array<T,R1> const& a, Array<T,R2> const& b)
{
    return Array<T, A_Mult<T,R1,R2>>
        (A_Mult<T,R1,R2>(a.rep(),b.rep()));
}

// multiplication of scalar and Array

template<typename T, typename R2>
Array<T, A_Mult<T,R2,A_Scalar<T>>>
operator* (Array<T,R2> const& a, A_Scalar<T> const& b)
{
    return Array<T, A_Mult<T,R2,A_Scalar<T>>>
        (A_Mult<T,R2,A_Scalar<T>>(a.rep(),A_Scalar<T>(b)));
}

// multiplication of Array and scalar, addition of ...

// addition of Array and scalar
```

这些运算符的声明有些繁琐（从这些示例中可以看出），但这些函数实际上做的事情并不多。例如，用于两个数组的运算符首先创建一个 A_Add 对象，该对象表示运算符和操作数。

[点击此处查看代码图像](#)

```cpp
A_Add<T,R1,R2> op(a.rep(), b.rep());
```
