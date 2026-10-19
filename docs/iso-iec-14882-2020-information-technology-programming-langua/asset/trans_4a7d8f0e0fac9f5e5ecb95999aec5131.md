

## 26.4.3 类模板 complex [complex]

```
namespace std {
  template<class T> class complex {
  public:
    using value_type = T;

    constexpr complex(const T& re = T(), const T& im = T());
    constexpr complex(const complex&);
    template<class X> constexpr complex(const complex<X>&);

    constexpr T real() const;
    constexpr void real(T);
    constexpr T imag() const;
    constexpr void imag(T);

    constexpr complex& operator= (const T&);
    constexpr complex& operator+=(const T&);
    constexpr complex& operator-=(const T&);
    constexpr complex& operator*=(const T&);
    constexpr complex& operator/=(const T&);

    constexpr complex& operator=(const complex&);
    template<class X> constexpr complex& operator= (const complex<X>&);
    template<class X> constexpr complex& operator+=(const complex<X>&);
    template<class X> constexpr complex& operator-=(const complex<X>&);
    template<class X> constexpr complex& operator*=(const complex<X>&);
    template<class X> constexpr complex& operator/=(const complex<X>&);
  };
}
```

类 complex 描述了一个可以存储复数的笛卡尔分量 real() 和 imag() 的对象。

## 26.4.4 特化 [complex.special]

```
namespace std {
  template<> class complex<float> {
  public:
    using value_type = float;
```

```
template<class T> complex<T> log  (const complex<T>&);
template<class T> complex<T> log10(const complex<T>&);

template<class T> complex<T> pow  (const complex<T>&, const T&);
template<class T> complex<T> pow  (const complex<T>&, const complex<T>&);
template<class T> complex<T> pow  (const T&, const complex<T>&);

template<class T> complex<T> sin  (const complex<T>&);
template<class T> complex<T> sinh (const complex<T>&);
template<class T> complex<T> sqrt (const complex<T>&);
template<class T> complex<T> tan  (const complex<T>&);
template<class T> complex<T> tanh (const complex<T>&);
```

```
// 26.4.11, complex literals
inline namespace literals {
inline namespace complex_literals {
    constexpr complex<long double> operator""i(long double);
    constexpr complex<long double> operator""i(unsigned long long);
    constexpr complex<double> operator""i(long double);
    constexpr complex<double> operator""i(unsigned long long);
    constexpr complex<float> operator""i(long double);
    constexpr complex<float> operator""i(unsigned long long);
}
}
```

```
constexpr complex(float re = 0.0f, float im = 0.0f);
constexpr complex(const complex<float>&) = default;
constexpr explicit complex(const complex<double>&);
constexpr explicit complex(const complex<long double>&);

constexpr float real() const;
constexpr void real(float);
constexpr float imag() const;
constexpr void imag(float);

constexpr complex& operator= (float);
constexpr complex& operator+=(float);
constexpr complex& operator-=(float);
constexpr complex& operator*=(float);
constexpr complex& operator/=(float);

constexpr complex& operator=(const complex&);
template<class X> constexpr complex& operator= (const complex<X>&);
template<class X> constexpr complex& operator+=(const complex<X>&);
template<class X> constexpr complex& operator-=(const complex<X>&);
template<class X> constexpr complex& operator*=(const complex<X>&);
template<class X> constexpr complex& operator/=(const complex<X>&);
};

template<> class complex<double> {
public:
    using value_type = double;

    constexpr complex(double re = 0.0, double im = 0.0);
    constexpr complex(const complex<float>&);
    constexpr complex(const complex<double>&) = default;
    constexpr explicit complex(const complex<long double>&);

    constexpr double real() const;
    constexpr void real(double);
    constexpr double imag() const;
    constexpr void imag(double);

    constexpr complex& operator= (double);
    constexpr complex& operator+=(double);
    constexpr complex& operator-=(double);
    constexpr complex& operator*=(double);
    constexpr complex& operator/=(double);

    constexpr complex& operator=(const complex&);
    template<class X> constexpr complex& operator= (const complex<X>&);
    template<class X> constexpr complex& operator+=(const complex<X>&);
    template<class X> constexpr complex& operator-=(const complex<X>&);
    template<class X> constexpr complex& operator*=(const complex<X>&);
    template<class X> constexpr complex& operator/=(const complex<X>&);
};

template<> class complex<long double> {
public:
    using value_type = long double;

    constexpr complex(long double re = 0.0L, long double im = 0.0L);
    constexpr complex(const complex<float>&);
    constexpr complex(const complex<double>&);
    constexpr complex(const complex<long double>&) = default;

    constexpr long double real() const;
    constexpr void real(long double);
    constexpr long double imag() const;
```

## 26.4.8 值操作

[complex.value.ops]

```
template<class T> constexpr T real(const complex<T>& x);
```

返回：x.real()。

```
template<class T> constexpr T imag(const complex<T>& x);
```

返回：x.imag()。

```
template<class T> T abs(const complex<T>& x);
```

返回：x 的幅值。

```
template<class T> T arg(const complex<T>& x);
```

返回：x 的相位角，或 atan2(imag(x), real(x))。

```
template<class T> constexpr T norm(const complex<T>& x);
```

返回：x 的幅值的平方。

```
template<class T> constexpr complex<T> conj(const complex<T>& x);
```

返回：x 的复共轭。

```
template<class T> complex<T> proj(const complex<T>& x);
```

返回：x 在黎曼球面上的投影。

说明：行为与 C 函数 cproj 相同。另请参阅：ISO C 7.3.9.5

```
template<class T> complex<T> polar(const T& rho, const T& theta = T());
```

前提条件：rho 为非负且非 NaN。theta 为有限值。

返回：对应于幅值为 rho 且相位角为 theta 的复数的复数值。

## 26.4.9 超越函数

[complex.transcendentals]

```
template<class T> complex<T> acos(const complex<T>& x);
```

返回：x 的复数反余弦。

说明：行为与 C 函数 cacos 相同。另请参阅：ISO C 7.3.5.1

```
template<class T> complex<T> asin(const complex<T>& x);
```

返回：x 的复数反正弦。

说明：行为与 C 函数 casin 相同。另请参阅：ISO C 7.3.5.2

```
template<class T> complex<T> atan(const complex<T>& x);
```

返回：x 的复数反正切。

说明：行为与 C 函数 catan 相同。另请参阅：ISO C 7.3.5.3

```
template<class T, class charT, class traits>
 basic_ostream<charT, traits>& operator<<(basic_ostream<charT, traits>& o, const complex<T>& x);
```

效果：将复数 x 插入到流 o 中，就好像实现如下：

```
basic_ostringstream<charT, traits> s;
s.flags(o.flags());
s.imbue(o.getloc());
s.precision(o.precision());
s << '(' << x.real() << "," << x.imag() << ')';
return o << s.str();
```

[注意 1：在使用逗号作为小数点字符的区域设置中，使用逗号作为字段分隔符可能会产生歧义。将 showpoint 插入到输出流中可强制所有输出显示显式的小数点字符；因此，所有插入的复数序列都可以无歧义地提取。——结束注意]

## 26.4.10 附加重载 [cmplx.over]

1 下列函数模板应具有附加重载：

- arg
- norm
- conj
- proj
- imag
- real

其中 norm、conj、imag 和 real 为 constexpr 重载。

2 附加重载应足以确保：
- （2.1）——如果参数类型为 long double，则 effectively 转换为 complex<long double>。
- （2.2）——否则，如果参数类型为 double 或整数类型，则 effectively 转换为 complex<double>。
- （2.3）——否则，如果参数类型为 float，则 effectively 转换为 complex<float>。

3 函数模板 pow 应具有足够的附加重载以确保，对于至少有一个参数类型为 complex<T> 的调用：
- （3.1）——如果任一参数类型为 complex<long double> 或 long double，则两个参数均 effectively 转换为 complex<long double>。
- （3.2）——否则，如果任一参数类型为 complex<double>、double 或整数类型，则两个参数均 effectively 转换为 complex<double>。
- （3.3）——否则，如果任一参数类型为 complex<float> 或 float，则两个参数均 effectively 转换为 complex<float>。

## 26.4.11 复数文字后缀 [complex.literals]

1 本小节描述用于构造复数字面量的文字后缀。后缀 i、il 和 if 分别创建类型为 complex<double>、complex<long double> 和 complex<float> 的复数，其虚部由给定的文字数字表示，实部为零。

```
constexpr complex<long double> operator""il(long double d);
constexpr complex<long double> operator""il(unsigned long long d);
```

2 返回：complex<long double>{0.0L, static_cast<long double>(d)}。

```
constexpr complex<double> operator""i(long double d);
constexpr complex<double> operator""i(unsigned long long d);
```

3 返回：complex<double>{0.0, static_cast<double>(d)}。

```
constexpr complex<float> operator""if(long double d);
constexpr complex<float> operator""if(unsigned long long d);
```

4 返回：complex<float>{0.0f, static_cast<float>(d)}。

## 26.5 位操作 [bit]

## 26.5.1 通用 [bit.general]

1 头文件 <bit> 提供了用于访问、操作和处理单个位和位序列的组件。

## 26.5.2 头文件 <bit> 概要 [bit.syn]

```
namespace std {
// 26.5.3, bit_cast
template<class To, class From>
constexpr To bit_cast(const From& from) noexcept;

// 26.5.4, 2 的积分幂
template<class T>
constexpr bool has_single_bit(T x) noexcept;
template<class T>
constexpr T bit_ceil(T x);
template<class T>
constexpr T bit_floor(T x) noexcept;
```

