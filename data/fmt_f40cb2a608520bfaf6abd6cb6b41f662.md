
```cpp
template<class InputIterator, class InputIterator>
bool lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator>
bool lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2);
template<class InputIterator, class InputIterator, class Compare>
bool lexicographical_compare(InputIterator first1, InputIterator last1, InputIterator first2, InputIterator last2, Compare comp);
template<class ExecutionPolicy, class ForwardIterator, class ForwardIterator, class Compare>
bool lexicographical_compare(ExecutionPolicy&& exec, ForwardIterator first1, ForwardIterator last1, ForwardIterator first2, ForwardIterator last2, Compare comp);
```

返回：如果范围 `[first1, last1)` 定义的序列字典序小于范围 `[first2, last2)` 定义的序列，则返回 `true`；否则返回 `false`。

复杂度：如果两个序列元素数量相同且对应的元素（如果有）等效，则两者都不小于另一个。如果一个序列是另一个的前缀，则较短的序列字典小于较长的序列。否则，字典序的结果与第一对不相等元素的比较相同。

示例：以下实现满足这些要求：

```cpp
for (; first1 != last1 && first2 != last2; ++first1, ++first2) {
    if (*first1 < *first2) return false;
    if (*first2 < *first1) return true;
}
return first1 == last1 && first2 == last2;
```

备注：空序列字典序小于任何非空序列，但不小于任何。

## 28.7.11 排生成器 [alg.permutation.generators]

```cpp
template<class BidirectionalIterator>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last);
```

## ISO/IEC 14882:2017(E)

```cpp
template<class BidirectionalIterator, class Compare>
bool next_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 1 要求：`BidirectionalIterator` 必须满足可交换（`ValueSwapable`）（20.5.3.2）。

- 2 影响：取范围 `[first, last]` 定义的序列并转换为下一个排列。下一个排列通过假设所有排列相对于 `operator<` 或 `comp` 是字典序排序。

- 3 返回：如果存在这样的排列，则返回 `true`。否则，将序列转换为降序排序的最大排列并返回 `false`。

- 4 复杂度：最多 `(last - first) / 2` 次交换。

```cpp
template<class BidirectionalIterator>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);
template<class BidirectionalIterator, class Compare>
bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last, Compare comp);
```

- 5 要求：`BidirectionalIterator` 必须满足可交换（`ValueSwapable`）（20.5.3.2）。

- 6 影响：取范围 `[first, last]` 定义的序列并转换为上一个排列。上一个排列通过假设所有排列相对于 `operator<` 或 `comp` 是字典序排序。

- 7 返回：如果存在这样的排列，则返回 `true`。否则，将序列转换为降序排序的最小排列并返回 `false`。

- 8 复杂度：最多 `(last - first) / 2` 次交换。

## 28.8 C 算法

备注：头文件 `<cstdlib>` (21.2.2) 声明了本子句描述的函数。结束

```c
void* search(const void* key, const void* base, size_t nemb, size_t size,
               int (*compare_pred)(const void*, const void*));
void qsort(void* base, size_t nemb, size_t size, int (*compare_pred)(const void*, const void*));
```

- 2 影响：这些函数具有 C 标准库指定的语义。

- 3 备注：除非由 `base` 指向的数组对象是平凡类型，否则行为是未定义的。

- 4 抛出：任何由 `compare()` (20.5.12) 抛出的异常。

另另：ISO C 7.22.5.

# ISO/IEC 14882:2017(E)

# 29 数值库 [numerics]

## 29.1 通用 [numerics.general]

1 本节描述了 C++ 程序可能用于执行半数值操作的组件。

2 下列子句描述了用于复数类型、随机数生成、数值（n-at-a-）数组、广义数值算法以及针对浮点数类型的数学函数的组件，如表 101 所示。

| 子句 | 头文件(s) |
| --- | --- |
| 29.2 定义 | |
| 29.3 要求 | |
| 29.4 浮点数环境 | `<cfenv>` |
| 29.5 复数 | `<complex>` |
| 29.6 随机数生成 | `<random>` |
| 29.7 数值数组 | `<valarray>` |
| 29.8 广义数值操作 | `<numeric>` |
| 29.9 针对浮点数类型的数学函数 | `<cmath>` `<cstdlib>` |

## 29.2 定义 [numerics.defns]

+ 定义 `GENERALIZED_NONCOMMUTATIVE_SUM(op, a1, ..., aN)` 如下：

+ (1.1) 当 `N` 不为 1 时，为所有；否则

(1.2) 对于任何满足 `1 < K+1 = M ≤ N` 的 `K`，`op(GENERALIZED_NONCOMMUTATIVE_SUM(op, a1, ..., aN), aK)`, `GENERALIZED_NONCOMMUTATIVE_SUM(op, a1, ..., aK)` 。

2 定义 `GENERALIZED_SUM(op, a1, ..., aN)` 为 `GENERALIZED_COMMUTATIVE_SUM(op, b1, ..., bN)`，其中 `b1, ..., bN` 是 `a1, ..., aN` 的任意排列。

## 29.3 数值类型要求 [numerics.requirements]

1 复数和数组组件由它们所包含的信息类型进行参数化，一个 C++ 程序应使用仅满足以下要求的类型 `T` 来实例化这些组件，²267

+ (1.1) `T` 不是抽象类（它没有虚成员函数）；

(1.2) `T` 不是引用类型；

(1.3) `T` 未经过 cv 修饰；

(1.4) 如果 `T` 是类，它有一个默认构造函数；

(1.5) 如果 `T` 是类，它有一个签名为 `T::(const Tk)` 的公共拷贝构造函数；

(1.6) 6) 如果 `T` 是类，它有一个公共的析构函数；

> ²267 换句话说，即值类型。这些包括算术类型、指针、库类 `complex` 以及值类型的 `vararray` 实例化。

(1.7) 如果 `T` 是类，它有一个公共的赋值运算符，其签名为 `T& T::operator=(const T&)` 或 `T& T::operator=(T)`

(1.8) 如果 `T` 是类，它的赋值运算符、拷贝构造函数、默认构造函数以及析构函数应对应下行中的每一项：

+ (1.8.1) 使用如何获得的 `T()` 值通过拷贝构造函数初始化原始存储，在语义上等同于原始存储的值初始化。

+ (1.8.2) 使用默认构造函数初始化原始存储，随后进行赋值，在语义上等同于使用拷贝构造函数初始化原始存储。

+ (1.8.3) 析构对象后使用拷贝构造函数初始化原始存储，在语义上等同于原始对象。

> [注：此规则在某些地方规定初始化与赋值的语义不应有任何差异。这为实现如何初始化数组提供了相当的清晰度。
> [示例：允许实现通过使用 `new` 运算符分配存储来初始化 `varray`（这暗示对每个元素调用默认构造函数），然后为每个元素赋值其值。或者实现也可以分配原始存储并使用拷贝构造函数初始化每个。——示例结束]

如果初始化和赋值之间的差异对某个类很重要，或者它未能满足上述列出的任何其他条件，程序员应使用 `vector` (26.3)。

(1.9) 如果是对 `T` 的操作，则不重载异常。

2 此外，`varray<T>` 的许多成员和相关函数只有在 `T` 满足每个成员或相关函数的额外要求时才能成功实例化并表现出定义良好的行为。

> [示例：实例化 `varray<complex>` 是有效的，但 `operator()` 不会为 `varray<complex>` 成功实例化，因为 `complex` 没有具有任何运算符。——示例结束]

## 29.4 浮点数环境 [cfenv]

### 29.4.1 头文件 <cfenv> 概要 [cfenv.syn]

```cpp
#define FE_ALLEXCEPT
#define FE_DIVZERO
#define FE_INVALID
#define FE_OVERFLOW
#define FE_UNDERFLOW
#define FE_DOWNWARD
#define FE_TONAREST
#define FE_TOWARDZERO
#define FE_UPWARD
#define FE_DFLEENV
```

```cpp
namespace std {
// types
using fenv_t = object type;
using fxecept_t = integer type;
```

```
// functions
int fetestexcept(int except);
int getexceptflag(fenv_t*, int except);
int fiserecept(int except);
int setexceptflag(fenv_t*, int except);
int fetetexcept(int except);
int getround();
int fetetround(int mode);
int getfenv(fenv_t*);
int feholdexcept(fenv_t*);
int setfenv(const fenv_t*);
int fesetenv(const fenv_t*);
```

+ 1 头文件 `<fenv>` 的内容与标准库头文件 `<fenv.h>` 相同。[注：文档并不要求实现支持 `FENV_ACCESS` pragma；该 pragma 是否支持由实现定义。因此，这些函数可以用于测试浮点标志、设置浮点控制模式，或在默认模式下运行。]

+ 2 浮点环境具有存储持续时间 (6.7.2)。浮点环境的初始状态是构造该对象的线程 (33.3.2) 在构造对象时的浮点环境状态。[注：这意味着，子线程获取其创建时父线程的浮点状态。——结束]

+ 3 每个线程都应维护一个独立的浮点环境。每个函数通过其调用访问环境。

另另参见：ISO/C 7

## 29.5 复数 [complex-numbers]

+ 1 头文件 `<complex>` 定义了用于表示复数的模板以及许多函数。

+ 2 除 `float`、`double` 以外的复数模板实例化是未指定的。`complex<float>` 和 `complex<double>`

+ 3 对于复数类型，其结果是未定义的。

+ 4 如果是类型 `T` 的表达式，则：

+ (4.1) `reinterpret_cast<cu>(z)` 应指定实部

+ (4.2) `reinterpret_cast<cv>(z)` 应指定实部

+ (4.3) `reinterpret_cast<cv>(a)` 应指定虚部

+ (4.4) `reinterpret_cast<cu>(a)` 应指定实部

### 29.5.1 头文件 <complex> 概要

```cpp
namespace std {
    template<class T> complex;
    template<class T> complex<float>;
    template<class T> complex<double>;
    template<class T> complex<long double>;
    // 29.5.6 运算符
    template<class T>
        complex<T> operator+(const complex<T>&, const complex<T>&);
        template<class T> operator+(const complex<T>&, const T&);
        template<class T> operator+(const T&, const complex<T>&);
    template<class T>
        operator-(const complex<T>&, const complex<T>&);
        template<class T> operator-(const complex<T>&, const T&);
        template<class T> operator-(const T&, const complex<T>&);
    template<class T>
        operator*(const complex<T>&, const complex<T>&);
        template<class T> operator*(const complex<T>&, const T&);
        template<class T> operator*(const T&, const complex<T>&);
    template<class T>
        operator/(const complex<T>&, const complex<T>&);
        template<class T> operator/(const complex<T>&, const T&);
        template<class T> operator/(const T&, const complex<T>&);
    template<class T>
        operator+(const complex<T>&, const complex<T>&);
        template<class T>
        operator-(const complex<T>&, const complex<T>&);
    template<class T>
        operator==(const complex<T>&, const complex<T>&);
        template<class T> operator===(const complex<T>&, const T&);
        template<class T> operator===(const T&, const complex<T>&);
    template<class T>
        operator!(const complex<T>&, const complex<T>&);
        template<class T> operator!==(const complex<T>&, const T&);
        template<class T> operator!==(const T&, const complex<T>&);
    template<class T, charT> traits {
        basic_istream<charT, traits<T>>
            operator>>(basic_istream<charT, traits<T>&, const complex<T>&);
    template<class T, charT> traits {
        basic_ostream<charT, traits<T>>
```
