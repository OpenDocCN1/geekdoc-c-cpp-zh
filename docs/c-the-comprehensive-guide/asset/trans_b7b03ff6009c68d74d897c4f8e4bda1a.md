
具体来说，在 C++ 中，表达式 `if(-4 < 2u)` 的值被编译器判定为 false，因为有符号字面量 -4 与无符号字面量 2u 进行比较。

> **避免混用**
>
> 如果你处理的是在此类转换中存在风险的数字范围——负数或大数——那么你就不应该依赖隐式转换。在这种情况下，请预先自行转换操作数。如果两个类型符号不同，不要写 `if(mySize > theLimit)...`，而要自己转换。这样你才会意识到这里正在发生某些需要留意的事情：
>
> `if(mySize > (long)theLimit) ...`
>
> 更好的做法是，从一开始就让两个数值具有相同的类型。
>
> 从 C++20 开始，可以使用更安全的辅助函数，如 `std::cmp_less()`、`std::cmp_equal()` 等，但这些函数比直接写 `<` 或 `==` 更复杂。要检查某个值能否安全地存入特定类型，请使用 `in_range<T>()`。在泛型模板代码中，这通常是唯一安全的方法。

## 数字类型别名

有些数字类型在不同的系统上有不同的定义。一个显著的例子是 `size_t`：有时该类型等同于 `unsigned int`，有时等同于 `unsigned long`，甚至等同于 `unsigned long long`。但如果你只是将这些类型的变量用于其设计目的，你就不会关心底层的具体类型。例如，如果你想了解数据结构的大小，请使用 `sizeof(data)`。返回的是一个 `size_t`——你应该将结果存储在其中。当然，它实际上是其他 int 类型之一，但你无需确切知道是哪一个。它是（未知）真实类型的别名。

使用别名有几个理由。其中最重要的有：

- 你可以省去输入工作。别名更短，尤其是在模板中。
- 它们能说明用途：也就是说，它们将别名用作语义标签。`ptrdiff_t` 和 `size_t` 可能完全相同，但它们的名称已经说明了它们的用途。
- 它们对以后的修改更加灵活，因为在不同的系统中，针对特定用途可能需要不同的类型。在这种情况下，你只需要在某个地方修改别名即可。

诸如 `size_t` 这样的别名是通过 `using` 创建的，如果你已经在使用相应的 `#include`，那么它们通常就是可用的。例如，`size_t` 可以这样定义：

```cpp
using size_t = unsigned long long;
```

> **“typedef”对比“using”**
>
> 如果你现在去看，也许根本不会在头文件里找到任何 `using`，因为 C++11 之前的做法如下：
>
> ```cpp
> typedef unsigned long long size_t;
> ```
>
> 我建议你使用新风格。这可能是品味（或习惯）问题，但我个人喜欢新名称位于等号 `=` 左侧的风格。不过我向你展示 `typedef` 风格，是因为我们可能很长一段时间内仍然会看到它。

正如你将在第四部分看到的，`vector` 可以容纳大量元素。你可以使用方括号 `[ ]` 通过索引来访问各个元素。该索引必须是一个数字——更准确地说，是一个 `size_t`。因此，如果你为 `vector` 索引定义一个计数变量，你完全可以将其设为 `size_t`。

```cpp
// https://godbolt.org/z/zGso3xGqj
#include <vector>
#include <cstddef> // size_t
int main()
{
        std::vector<int> data = { 100, -4, 6'699, 88, 0, };

        int sum = 0;

        for(size_t idx = 0; idx < data.size(); ++idx)
        { // A specific int
                sum += data[idx];
        }
}
```

**清单 4.31** 索引变量可以是“size_t”类型。

然而，不应向你隐瞒的是，前面例子中的求和当然可以用 `for(auto d: data) sum += d;` 实现得更好。或者你也可以直接使用 `<algorithm>` 中的算法：`auto sum = std::accumulate(data.begin(), data.end(), 0);`。在两种情况下，你都能看到，借助 C++11，你现在常常可以省去了解确切类型的麻烦。

其他经常使用的别名，以及针对某些整数类型的典型定义，见表 4.8。

- `b |= a, b &= a, b ^= a` 将运算结果保存回 `b`。
- `~b` 返回一个新的字节，其中所有位都取反。

一个典型用途是 `vector<byte>`，例如，你可以用它来读取文件的内容。

## 4.4.4 浮点数

除了整数类型之外，还有用于浮点数的 `float`、`double` 和 `long double` 类型。在进行 `5/2` 这样的除法时，余数不会被丢弃，而是可以存储在 `double` 中；例如，`double x = 5.0 / 2.0;` 会将 2.5 存储在 `x` 中。但请注意，浮点数也有其局限性：它们同样只有固定数量的位可用，但使用方式与整数类型不同。它们会使用一部分位来“缩放”数值。这意味着你可以用它们存储极大和极小的数，但精度是有上限的。你需要记住以下几点：

- **溢出**
  尽管数字范围比 `int` 大得多，`double` 也可能溢出。它无法存储大于 `10^300` 或小于 `-10^300` 的数字。
- **精度**
  精度更为关键。你越远离作为中心的零，`double` 能存储的值就变得越粗糙。两个“相邻” `double` 数之间的距离会增大。大约从 `10^15` 开始，这个距离就大于 1。如果将它们存储在 `double` 中，数字 `10^16+1` 和 `10^16+2` 对计算机来说是相同的；参见清单 4.33。
- **舍入**
  但 `double` 在处理接近零的数字时也有问题。例如，`int` 可以精确存储 7，而 `double` 却无法精确存储 `0.1`——更不用说 `1/3` 和 `0.3` 了，正如图 4.4 所示。

标准数据类型是 `double`。这些类型的位宽并非固定，但通常 `double` 为 64 位，`float` 为 32 位，`long double` 为 80 或 128 位。从 C++23 开始，还有固定宽度的类型（见表 4.10）。

```cpp
// https://godbolt.org/z/8ae83nPYs
#include <iostream>       // cout
#include <iomanip>        // setprecision, etc.
#include <cmath>          // fabs
using std::cout;          // cout as abbreviation for std::cout
int main() {
    cout << std::fixed << std::setprecision(25);    // for better readable output
    // 0.1 and 0.01 cannot store double exactly
    double x = 0.1 * 0.1;
    cout << "0.1*0.1: " << x << "\n";
    // Output: 0.01000000000000000019428903
    if(x == 0.01) {        // never compare double with ==
        cout << "Yes! x == 0.01" << "\n";
    } else {
        cout << "Uh-oh! x != 0.01" << "\n";        // you see this output
    }
    // Attention especially when comparing with 0.0
    double null = x - 0.01;
    cout << "null: " << null << "\n";
    // Output: null: 0.0000000000000017347235
    if(std::fabs(null) < 0.00000001) {                  // compare with an "epsilon"
        cout << "Yes! null is close to 0.0" << "\n";  // you see this output
    } else {
        cout << "Uh-oh! null not close to 0.0" << "\n";
    }
    // fractions of powers of 2 are less critical
    double y = 0.5 * 0.5;
    cout << "0.5*0.5: " << y << "\n";
    // Output: 0.5*0.5: 0.250000000000000000000000000
    if(y == 0.25) {       // here the dangerous comparison works exceptionally
        cout << "Yes! y == 0.25" << "\n";              // you see this output
    } else {
        cout << "Oh-oh! y != 0.25" << "\n";
    }
    //
    return 0;
}
```

**清单 4.32** “double”并非总能精确存储数字。用“==”进行计算和比较是错误的。

> **不要使用 == 比较浮点数**
>
> 由于 `float`、`double` 和 `long double` 这些浮点类型都无法精确存储所有数字，你绝不应该使用 `==` 来测试相等性。相反，应计算差值并检查结果是否接近零。例如，如果你想了解两个 `double` 值 `a` 和 `b` 是否“几乎相等”，可以用这种方式检查：
>
> ```cpp
> if( fabs(b-a)<0.0001 )...
> ```
>
> `fabs()` 函数用于计算绝对值（使其为正数），位于 `<cmath>` 头文件中。对于 `0.0001`，请使用适合你的应用的 epsilon 值。
