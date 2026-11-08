

## 4.3 相等比较与三路比较

![](img/c60a87adb7f61e2e82071d081bbb389a_156_0.png)

C++20 使您能够定义或自动生成相等运算符。相等运算符判断两个值 A 和 B 是否满足 A == B 或 A != B。此外，如果您的值 A 和 B 需要支持排序，请使用三路比较运算符 <=>。三路比较运算符通常被称为太空船运算符。太空船运算符判断两个值 A 和 B 是 A < B、A == B 还是 A > B。与相等运算符一样，您可以定义太空船运算符，也可以让编译器自动生成它。

为了理解三路比较运算符的优点，让我先从经典的做法开始。

### 4.3.1 C++20 之前的比较

我实现了一个简单的 int 包装器 MyInt。当然，我想比较 MyInt。下面是我使用函数模板 `isLessThan` 的解决方案。

#### MyInt 支持小于比较

```cpp
// comparisonOperator.cpp

#include <iostream>

struct MyInt {
    int value;
    explicit constexpr MyInt(int val): value{val} { }
    bool operator < (const MyInt& rhs) const {
        return value < rhs.value;
    }
};

template <typename T>
constexpr bool isLessThan(const T& lhs, const T& rhs) {
    return lhs < rhs;
}

int main() {

    std::cout << std::boolalpha << '\n';

    MyInt myInt2011(2011);
    MyInt myInt2014(2014);

    std::cout << "isLessThan(myInt2011, myInt2014): "
              << isLessThan(myInt2011, myInt2014) << '\n';

    std::cout << '\n';

}
```

程序按预期运行：

![](img/c60a87adb7f61e2e82071d081bbb389a_158_0.png)

使用小于运算符

说实话，MyInt 不是一个直观的类型。当你定义了六种比较关系中的一种时，你应该将它们全部定义。直观的类型至少应该是半正则的。现在，我必须编写大量样板代码。下面是缺失的五个运算符。

#### 缺失的五个比较运算符

```cpp
bool operator == (const MyInt& rhs) const {
    return value == rhs.value;
}

bool operator != (const MyInt& rhs) const {
    return !(*this == rhs);
}

bool operator <= (const MyInt& rhs) const {
    return !(rhs < *this);
}

bool operator > (const MyInt& rhs) const {
    return rhs < *this;
}

bool operator >= (const MyInt& rhs) const {
    return !(*this < rhs);
}
```

现在，让我们跳到 C++20，看看相等运算符和三路比较运算符。

### 4.3.2 C++20 以来的比较

您可以定义比较运算符或三路比较运算符，也可以使用 = default 请求编译器生成。让我从相等运算符开始。

#### 4.3.2.1 相等运算符

当您定义相等运算符或使用 = default 请求编译器生成相等运算符时，您会自动获得相等和不等运算符：== 和 !=。

##### 实现或请求生成相等运算符

```cpp
// equalityComparison.cpp

#include <iostream>

struct MyInt {
    int value;
    explicit constexpr MyInt(int val): value{val} { }
    bool operator==(const MyInt& rhs) const {
        return value == rhs.value;
    }
};

struct MyDouble {
    double value;

    explicit constexpr MyDouble(double val) : value{val} { }
    bool operator==(const MyDouble& rhs) const = default;
};

template <typename T>
constexpr bool areEqual(const T& lhs, const T& rhs) {
    return lhs == rhs;
}

int main() {

    std::cout << std::boolalpha << '\n';

    MyInt myInt1(2011);
    MyInt myInt2(2014);

    std::cout << "areEqual(myInt1, myInt2): "
              << areEqual(myInt1, myInt2) << '\n';

    MyDouble myDouble1(2011);
    MyDouble myDouble2(2014);

    std::cout << "areEqual(myDouble1, myDouble2): "
              << areEqual(myDouble1, myDouble2) << '\n';

    std::cout << '\n';

}
```

用户定义的（第 8 行）和编译器生成的（第 16 行）相等运算符都按预期工作。两者都返回布尔值。

![](img/c60a87adb7f61e2e82071d081bbb389a_160_0.png)

使用用户定义和编译器生成的相等运算符

#### 4.3.2.2 三路比较运算符

当您定义三路比较运算符或使用 = default 请求编译器生成它时，您会自动获得所有六个比较运算符：==、!=、<、<=、> 和 >=。该成员函数必须是 const，且参数必须是 const 左值引用。

##### 实现或请求生成三路比较运算符

```cpp
1  // threeWayComparison.cpp
2
3  #include <compare>
4  #include <iostream>
5
6  struct MyInt {
7    int value;
8    explicit MyInt(int val): value{val} { }
9    auto operator<=>(const MyInt& rhs) const {
10     return value <=> rhs.value;
11   }
12 };
13
14 struct MyDouble {
15   double value;
16   explicit constexpr MyDouble(double val): value{val} { }
17   auto operator<=>(const MyDouble&) const = default;
18 };
19
20 template <typename T>
21 constexpr bool isLessThan(const T& lhs, const T& rhs) {
```

![](img/c60a87adb7f61e2e82071d081bbb389a_162_0.png)

##### 指针的自动比较

编译器生成的比较运算符比较的是指针，而不是引用的对象。

```cpp
// spaceshipPointer.cpp

#include <iostream>
#include <compare>
#include <vector>

struct A {
    std::vector<int>* pointerToVector;
    auto operator <=> (const A&) const = default;
};

int main() {

    std::cout << '\n';

    std::cout << std::boolalpha;

    A a1{new std::vector<int>()};
    A a2{new std::vector<int>()};

    std::cout << "(a1 == a2): " << (a1 == a2) << "\n\n";

}
```

令人惊讶的是，a1 == a2（第 21 行）的结果是 false 而不是 true，因为比较的是 `std::vector<int>` 的地址。

![](img/c60a87adb7f61e2e82071d081bbb389a_162_1.png)

有三种比较类别。

### 4.3.3 比较类别

三种比较类别的名称分别是：强排序（std::strong_ordering），也称为全序，弱排序（std::weak_ordering）和偏排序（std::partial_ordering）。

强排序也称为全序。

对于类型 T，以下三个属性区分了三种比较类别：

- 1. T 支持所有六个关系运算符：==、!=、<、<=、> 和 >=（简称：关系运算符）
- 2. 所有等价的值都是不可区分的（简称：等价）
- 3. T 的所有值都是可比较的：对于 T 的任意值 a 和 b，三个关系 a < b、a == b 和 a > b 中必有一个为真（简称：可比较）

整型或字符串是强排序的典型示例。当比较有符号整型的绝对值或不区分大小写地比较字符串时，这种排序被称为弱排序。强排序决定了值的同一性，而弱排序决定了值的等价性。此外，两个任意的浮点值不一定是可比较的：对于 a = 5.5 和 b = NaN（非数值），以下表达式都不返回 true：a < NaN、a == NaN 或 a > NaN。这意味着浮点值支持偏排序。

基于这三个属性，区分三种比较类别就很简单了：

强、弱和偏排序

| 比较类别 | 关系运算符 | 等价 | 可比较 |
| --- | --- | --- | --- |
| 强排序 | 是 | 是 | 是 |
| 弱排序 | 是 |  | 是 |
| 偏排序 | 是 |  |  |

支持强排序的类型隐式地支持弱排序和偏排序。弱排序也是如此。支持弱排序的类型也支持偏排序。其他方向则不适用。

```cpp
// FINE
// std::partial_ordering operator <=> (const StrongWeakPartial&) const = default;

// ERROR
// std::strong_ordering operator <=> (const StrongWeakPartial&) const = default;
// std::weak_ordering operator <=> (const StrongWeakPartial&) const = default;

};

int main() {
    StrongWeakPartial a1, a2;

    a1 < a2;
}
```

类型 `StrongWeakPartial` 具有支持强排序（第 6 行）、弱排序（第 10 行）和偏排序（第 14 行）的子类型。因此，类型 `StrongWeakPartial`（第 17 行）的共同比较类别是 `std::partial_ordering`。使用更强大的比较类别，如强排序（第 29 行）或弱排序（第 30 行），会导致编译时错误。

#### 4.3.3.1 比较类别的值

三个比较类别 `std::strong_ordering`、`std::weak_ordering` 和 `std::partial_ordering` 各有三个值，用于表示小于、等于或大于。

##### 4.3.3.1.1 `std::strong_ordering`

```cpp
std::strong_ordering::less
std::strong_ordering::equal, or std::strong_ordering::equivalent
std::strong_ordering::greater
```

##### 4.3.3.1.2 `std::weak_ordering`

```cpp
std::weak_ordering::less
std::weak_ordering::equivalent
std::weak_ordering::greater
```

##### 4.3.3.1.3 `std::partial_ordering`

