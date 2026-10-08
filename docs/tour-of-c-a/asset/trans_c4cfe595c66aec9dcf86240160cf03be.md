

```cpp
void user(vector<int>::iterator vip, list<string>::iterator lsp)
{
    advance(vip,10);    // 使用快速的 advance())
    advance(lsp,10);    // 使用缓慢的 advance())
}
```

```cpp
template<forward_iterator Iter>
    requires requires(Iter p, int i) { p[i]; p+i; } // Iter 具有下标运算和整数加法
void advance(Iter p, int n) // // 将 p 向移动 n 个元素
{
    p+=n;
}
```

```cpp
requires(Iter p, int i) { p[i]; p+i; }
```

```cpp
template<random_access_iterator Iter>
void advance(Iter p, int n)    // 将 p 向移动 n 个元素
{
    p+=n;                       // 随机访问迭代器具有 +===
}
```

```cpp
template<typename T>
concept Equality_comparable =
requires (T a, T b) {
    { a == b } -> boolean; // 用 == 比较 T
    { a != b } -> boolean; // 用 != 比较 T
};
```

```cpp
static_assert(Equality_comparable<int>); // 成功
```

```cpp
struct S { int a; };
static_assert(Equality_comparable<S>); // 失败，因为结构体不会自动获得 == 和 !=
```

```cpp
template<typename T, typename T2 =T>
concept Equality_comparable = =
requires (T a, T2 b) {
    { a == b } -> boolean; // 用 == 比较一个 T 和 T2
    { a != b } -> boolean; // 用 != 比较一个 T 和 T2
    { b == a } -> boolean; // 用 == 比较一个 T2 和 T
    { b != a } -> boolean; // 用 != 比较一个 T2 和 T
};
```

```cpp
static_assert(Equality_comparable<int,double>);  // 成功
static_assert(Equality_comparable<int>);      // 成功 (T2 默认为 int)
static_assert(Equality_comparable<int,string>); // 失败
```

```cpp
template<typename T, typename U = T>
concept Number =
    requires(T x, U y) { // 包含算术运算和零
    x+y; x-y; x*y; x/y;
    x+=y; x-=y; x*=y; x/=y;
    x=x; // 拷贝
    x=0;
};
```

```cpp
template<typename T, typename U = T>
concept Arithmetic = Number<T,U> && Number<U,T>;
```

```cpp
template<typename S>
concept Sequence = requires (S a) {
    typename range_value_t<S>;
    typename iterator_t<S>;

    { a.begin() } -> same_as<iterator_t<S>>;
    { a.end() } -> same_as<iterator_t<S>>;

    requires input_iterator<iterator_t<S>>;
    requires same_as<range_value_t<S>, iter_value_t<S>>;
};

// S 必须有一个值类型
// S 必须有一个迭代器类型

// S 必须有一个返回迭代器的 begin()

// S 的迭代器必须是一个 input_iterator

```cpp
template<typename S>
concept Sequence = input_range<S>; // 编写起来简单且通用
```

```cpp
template<class S>
using Value_type = typename S::value_type;
```

```cpp
template<equality_comparable T>
bool cmp(T a, T b)
{
    return a<b;
}
```

```cpp
bool b0 = cmp(cout,cerr);           // 错误：ostream 不支持 ==
bool b1 = cmp(2,3);               // OK：返回 true
bool b2 = cmp(2+3i,3+4i);      // 错误：complex<double> 不支持 <
```

```cpp
auto x = 1;             // x 是一个 int
auto z = complex<double>{1,2}; // z 是一个 complex<double>
```

```cpp
auto g() { return 99; }
int f(auto x) { /* ... */ }

int x = f(1);
int z = f(complex<double>{1,2});
```

> // g() 返回一个 int
// 接收任何类型的参数
// 这个 f() 接收一个 int
// 这个 f() 接收一个 complex<double>

```cpp
auto twice(Arithmetic auto x) { return x+x; } // 针对数字
auto thrice(auto x) { return x+x+x; } // 针对任何支持 + 的类型

auto x1 = twice(7); // OK：x1==14
string s "Hello";
auto x2 = twice(s); // 错误：字符串不是 Arithmetic
auto x3 = thrice(s); // OK x3="Hello"
```

```cpp
auto ch1 = cmp("foo");
Arithmetic auto ch2 = cmp("foo");
auto ch3 = cmp("foo");
```

> // 无论 cmp() 返回什么都能正常工作
// 错误：a 不是 Arithmetic
// OK：假设有一个合适的 concept
// 并且 cmp() 返回了该 concept

```cpp
Number auto some_function(int x)
{
    // ...
    return cmp(x); // 除非 cmp(x) 返回一个 Number，否则错误
}
```

```cpp
auto some_function(int x)
{
    // ...
    Number y = cmp(x); // 除非 cmp(x) 返回一个 Number，否则错误
    return y;
}
```

```cpp
void sort(auto&); // 错误：需要 'auto'
void sort(auto&);    // 错误：名称后需要 'auto' 
```

```cpp
double sum(const vector<int>& v)
{
    double res = 0;
    for (auto x : v)
        res += x;
    return res;
}
```

```cpp
template<forward_iterator Iter, Arithmetic<iter_value_t<Iter>>>
auto accumulate(Iter first, Iter last, auto res)
{
    for (auto p = first; p!=last; ++p)
        res += *p;
    return res;
}
```

```cpp
void use(const vector<int>& vec, const list<double>& lst)
{
    auto sum = accumulate(begin(vec),end(vec),0.0); // 在 double 中累加
    auto sum = accumulate(begin(vec),end(vec),0.0); // accumulate in a double
}
```

