

# ISO/IEC 14882:2017(E)

16 备注：此提取是作为系列更简单的提取完成的。因此，每次提取对空白字符的跳过应该是相同的。

```cpp
template<class T, class char, class traits>
basic_ostream<char>& operator<<(basic_ostream<char>& traits& o, const complex<T>& x);
```
影响：将复数 x 插入流中，或者如果其实现为：
```cpp
basic_ostream<char>(traits& s);
s.flags(o.flags());
s.imbue(o.getloc());
s.precision(o.precision());
return r << '(' << x.real() << ", " << x.imag() << ')';
return s.str();
```

18 [注：在使用逗号作为小数点的区域设置中，字段的逗号可能是歧义的。在输出流中插入 showpoint 会强制所有输出显示显式的点字符；结果是所有插入的复数序列都可以被无歧义地提取——结束注释]

# 29.5.7 复数值操作 [complex.value.ops]

```cpp
1 template<class T> real(const complex<T>& x);
返回：x.real();
```

```cpp
2 template<class T> imag(const complex<T>& x);
返回：x.imag();
```

```cpp
3 template<class T> abs(const complex<T>& x);
返回：x 的模。
```

```cpp
4 template<class T> arg(const complex<T>& x);
返回：x 的相位，或 atan2(imag(x), real(x))
```

```cpp
5 template<class T> norm(const complex<T>& x);
返回：x 的模平方。
```

```cpp
6 template<class T> conj(const complex<T>& x);
返回：x 的复数共轭。
```

```cpp
7 template<class T> proj(const complex<T>& x);
返回：x 在黎球面上的投影。
```

8 备注：行为与 7.3.9.4 中定义的函数 cproj 相同。

```cpp
9 template<class T> polar(const complex<T>& x, const T& theta = 0);
返回：rho 必须是非负且非 NaN。theta 必须是有限的。
```

```cpp
10 返回：对应于模为 rho 相位为 theta 的复数。
```

# 29.5.8 复数超越函数 [complex.transcendental]

```cpp
1 template<class T> acos(const complex<T>& x);
返回：x 的反余弦。
2 备注：行为与 7.3.5.1 中定义的函数 cacos 相同。

```cpp
template<class T> asin(const complex<T>& x);
3 返回：x 的反正弦。
4 备注：行为与 7.3.5.2 中定义的函数 cacin 相同。

```cpp
template<class T> atan(const complex<T>& x);

5 返回：x 的反正正切。

6 备注：行为与 7.3.5.3 中定义的函数 catan 相同。

```cpp
template<class T> acosh(const complex<T>& x);
7 返回：x 的复数双余弦。

8 备注：行为与 7.3.6.1 中定义的函数 acosh 相同。

```cpp
template<class T> asinh(const complex<T>& x);
9 返回：x 的复数双正弦。

10 备注：行为与 7.3.6.2 中定义的函数 casinh 相同。

```cpp
template<class T> atanh(const complex<T>& x);
11 返回：x 的复数双正正切。

12 备注：行为与 7.3.6.3 中定义的函数 catanh 相同。

```cpp
template<class T> cos(const complex<T>& x);
13 返回：x 的复数余弦。

```cpp
template<class T> cosh(const complex<T>& x);
14 返回：x 的复数双正弦。

```cpp
template<class T> exp(const complex<T>& x);
15 返回：x 的复数底数指数。

```cpp
template<class T> log(const complex<T>& x);
16 返回：x 的复数自然对数（底数为e）。对于所有 x，imag(log(x)) 位于 [-π, π]，且当 x 为负数时，imag(log(x)) 为 π。
17 备注：分支沿负实轴。

```cpp
template<class T> log10(const complex<T>& x);
18 返回：x 的复数常用对数（底数为10），定义为 log(x)/log(10)。

```cpp
template<class T> pow(const complex<T>& x, const T& y);

```

cpp
template<class T> pow(const complex<T>& x, const complex<T>& y);
```

```
template<class T> pow(const T& x, const complex<T>& y);
20 返回：底数的 y 次方，定义为 exp(y * log(x))。pow(0, 0) 返回的值由实现定义。
21 备注：分支沿负实轴。

```cpp
template<class T> sin(const complex<T>& x);
返回：x 的复数正弦。

```cpp
template<class T> sinh(const complex<T>& x);
返回：x 的复数双正弦。

```cpp
template<class T> sqrt(const complex<T>& x);
返回：x 的复数平方根，位于右半平面范围内。如果参数为负数，则该值位于正虚轴上。

```cpp
template<class T> tan(const complex<T>& x);
返回：x 的复数正切。

```cpp
template<class T> tanh(const complex<T>& x);
返回：x 的复数双正切。
```

# 29.5.9 额外重载 [complex.overloads]

1 下列函数模板应具有额外的重载：
```
arg          norm
conj         proj
imag         real
```

2 额外的重载应足以确保：
1. 如果参数类型为 double，则它被有效转换为 complex<double>。
2. 否则，如果参数类型为 double 或整型类型，则它被有效转换为 complex<double>。
3. 否则，如果参数类型为 float，则它被有效转换为 complex<float>。

3 函数 pow 应具有额外的重载，以确保对于至少一个类型为 complex<T> 的调用：
1. 如果任意一个参数为 complex<double> 或 long double，则两个参数都被有效转换为 complex<double>。
2. 否则，如果任意一个参数类型为 complex<double>、double 或整数，则两个参数都被有效转换为 complex<double>。
3. 否则，如果任意一个参数类型为 complex<float> 或 float，则两个参数都被有效转换为 complex<float>。

# 29.5.10 复数字面量的后缀 [complex.literals]

1 本节描述了复数的构造。后缀 i、il 和 if 分别创建 complex<double>、complex<long double> 和 complex<float> 类型的数字，其虚部由字面量数字表示，实部为零。

```cpp
constexpr complex<double> operator ""(long double d);
```
3 返回：complex<double>{0.0, static_cast<double>(d)}

```cpp
constexpr complex<float> operator ""(float d);
constexpr complex<float> operator ""(unsigned long d);
```
4 返回：complex<float>{0.0f, static_cast<float>(d)}

# 29.6 随机数生成

1 小节定义了生成（伪）随机数的设施。
2 除了工具外，定义了四类实体：均匀随机位生成器、随机数引擎、随机数适配器和随机分布。[注：这些分类适用于相应的类型、此类类型的对象以及模板，允许将随机位生成器对象作为零参数参数，如 bind(d)。]
3 通过本节指定的每个实体具有算术类型（6.9.1），作为 result_type 的 T：
    a) 布尔或等布尔，如果 T 为 bool；
    b) 整数或等整数值，如果 numeric_limits<T>::is_integer 为真；
    c) 浮点或等实值。
如果是整数，还可以根据 numeric_limits<T>::is_signed 进一步分类为符号或无符号。
4 另有规定，本节中所有计算描述使用数学规则。
5 在本节中，运算符 bitand、bitor 和 xnor 表示传统的位运算。此外
    a) 运算符 shiftleft 表示高位填充零的位移，以及
    b) 运算符 shiftright 表示低位填充零的位移，且其结果始终取 2^m。

# 29.6.1 要求

1 在本节 29.6 中，实例化模板的影响如下：
    a) 具有模板类型参数 Sseq 的是未定义的，除非相应的模板参数未限定且满足种子序列（29.6.1.2）的要求。
    b) 具有模板参数 URBG 的是未定义的，除非相应的模板参数未限定且满足均匀随机位生成器（29.6.1.3）的要求。
    c) 具有模板参数 Engine 的是未定义的，除非相应的模板参数未限定且满足随机数引擎（29.6.1.4）的要求。
    d) 具有模板类型参数 RealType 的是未定义的，除非相应的模板参数未限定且是 float、double 或 long double 之一。
    e) 具有模板类型参数 IntType 的是未定义的，除非相应的模板参数未限定且是 short、int、long、long long、unsigned short、unsigned int、unsigned long 或 unsigned long 之一。

