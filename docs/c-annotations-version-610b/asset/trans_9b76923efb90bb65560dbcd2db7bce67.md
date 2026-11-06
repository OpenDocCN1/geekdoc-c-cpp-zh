
对于不返回值的lambda函数（即void lambda函数），无需指定返回类型。

与lambda函数具有相同作用域的变量可以通过在lambda函数的方括号内声明引用来访问。这允许将局部上下文传递给lambda函数。这样的变量称为闭包。下面是一个示例：

```cpp
void showSum(vector<int> &vi)
{
    int total = 0;
    for_each(
        vi.begin(), vi.end(),
        [&total](int x)
        {
            total += x;
        }
    );
    std::cout << total;
}
```

变量int total以引用（[&total]）的形式传递给lambda函数，并且可以直接被该函数访问。其参数列表仅定义了一个int x，x按顺序由vi中存储的每个值初始化。一旦泛型算法完成，showSum的变量total将收到一个值，该值等于vector中所有值的总和。它的生命周期超过了lambda函数，其值被显示出来。

如果闭包变量在定义时没有引用符号（&），它将被解释为lambda函数的值参数，当lambda函数被传递给泛型算法时，该值参数由局部变量初始化。通常，闭包变量通过引用传递。如果所有局部变量都要按引用传递，只需使用`[&]`即可（要按值传递整个闭包，则应使用`[=]`）：

```cpp
void show(vector<int> &vi)
{
    int sum = 0;
    int prod = 1;
    for_each(
        vi.begin(), vi.end(),
        [&](int x)
        {
            sum += x;
            prod *= x;
        }
    );
    std::cout << sum << ' ' << prod;
}
```

也可以将某些变量按值传递给lambda函数，而将其余变量按引用传递。在这种情况下，默认方式使用&或=指定。该默认指定符号后跟一个以不同方式传递的变量列表。示例：

```cpp
[&, value](int x)
{
    total += x * value;
};
```

这里total按引用传递，value按值传递。

类成员也可以定义lambda函数。此类lambda函数可以完全访问该类的所有成员。换句话说，它们被自动定义为类的友元。示例：

尽管STL提供了各种统计分布，但其功能相当有限。这些分布允许我们从中获取随机数，但STL目前不提供概率密度函数或累积分布函数。然而，这些函数（分布以及密度和累积分布函数）可在其他库中获得，例如boost数学库^3（具体参见：http://www.boost.org/doc/libs/1_44_0/libs/math/doc/sf_and_dist/html/index.html）。

讨论C++11标准所支持的各种分布的数学特性超出了C++ Annotations的范围。感兴趣的读者可参阅相关的数学教科书（如Stuart和Ord的（2009）《Kendall's Advanced Theory of Statistics》，Wiley出版社）或访问诸如http://en.wikipedia.org/wiki/Bernoulli_distribution的网址。

## 18.8.1 随机数生成器（C++11）

以下生成器可用：

| 类模板 | 整型/浮点型 | 质量 | 速度 | 状态大小 |
| --- | --- | --- | --- | --- |
| linear_congruential_engine | 整型 | 中等 | 中等 | 1 |
| subtract_with_carry_engine | 两者 | 中等 | 快速 | 25 |
| mersenne_twister_engine | 整型 | 良好 | 快速 | 624 |

`linear_congruential_engine`随机数生成器计算

```
value_{i+1} = (a * value_i + c) % m
```

它分别期望以下模板参数：用于包含生成的随机值的数据类型；乘数`a`；加性常数`c`；以及模值`m`。示例：

```cpp
linear_congruential_engine<int, 10, 3, 13> lincong;
```

`linear_congruential`生成器可以通过向其构造函数提供种子参数来进行播种。例如，`lincong(time(0))`。

`subtract_with_carry_engine`随机数生成器计算

```
value_i = (value_{i-s} - value_{i-r} - carry_{i-1}) % m
```

它分别期望以下模板参数：用于包含生成的随机值的数据类型；模值`m`；以及减法常数`s`和`r`。示例：

```cpp
subtract_with_carry_engine<int, 13, 3, 13> subcar;
```

`subtract_with_carry_engine`生成器可以通过向其构造函数提供种子参数来进行播种。例如，`subcar(time(0))`。

预定义的`mersenne_twister_engine` `mt19937`（使用`<random>`头文件中的typedef预定义）将在下面的示例中使用。可以使用`mt19937 mt`构造它，也可以通过向其构造函数提供一个参数来播种（例如`mt19937 mt(time(0))`）。初始化`mersenne_twister_engine`的其他方式超出了C++ Annotations的范围（但参见Lewis等人^4（1969））。

随机数生成器也可以通过调用其接受`unsigned long`值或生成器函数的`seed`成员来播种（如`lc.seed(time(0))`、`lc.seed(mt)`）。

3 http://www.boost.org/

4 Lewis, P.A.W., Goodman, A.S., 和 Miller, J.M.（1969），用于System/360的伪随机数生成器，IBM Systems Journal, 8, 136-146.

## 18.8.2 统计分布（C++11）

在以下章节中，将介绍C++11标准支持的各种统计分布。记号`RNG`用于表示*随机数生成器*，`URNG`用于表示*均匀随机数生成器*。对于每个分布，都定义了一个包含该分布参数的结构体`param_type`。这些`param_type`结构体的组织方式取决于（并在实际分布处描述）。

所有分布都提供以下成员（*result_type*指分布返回值的类型名）：

- `result_type max() const`  
  返回分布的最小上界；
- `result_type min() const`  
  返回分布的最大下界；
- `param_type param() const`  
  返回对象的`param_type`结构体；
- `void param(const param_type &param)`  
  重新定义分布的参数；
- `void reset()`  
  清除其所有缓存值；

所有分布都支持以下运算符（*distribution-name*应替换为所需分布的名称，例如`normal_distribution`）：

- `template<typename URNG> result_type operator()(URNG &urng)`  
  从统计分布中返回下一个随机值，其中函数对象`urng`从均匀随机分布中返回下一个随机数；
- `template<typename URNG> result_type operator()(URNG &urng, param_type &param)`  
  从使用`param`结构体提供的参数初始化的统计分布中返回下一个随机值。函数对象`urng`从均匀随机分布中返回下一个随机数；
- `std::istream &operator>>(std::istream &in, distribution-name &object)`  
  从`std::istream`中提取分布的参数；
- `std::ostream &operator<<(std::ostream &out, distribution-name const &obd)`  
  将分布的参数插入到`std::ostream`中。

下面的示例展示了如何使用这些分布。只需将分布的名称（`normal_distribution`）替换为另一个分布的名称，即可切换分布。所有分布都有参数，如正态分布的均值和标准差，并且所有参数都有默认值。参数名称因分布而异，并在下文中各个分布处提及。分布提供返回或设置其参数的成员。

大多数分布被定义为类模板，需要指定用于函数返回类型的数据类型。如果是这样，空的模板参数类型规范（`<>`）将提供默认类型。默认类型是`double`（用于实值返回类型）或`int`（用于整数值返回类型）。对于未定义为类模板的分布，必须省略模板参数类型规范。
