

# ISO/IEC 14882:2017(E)

```cpp
template<class T> complex<T> conj(const complex<T>&);
template<class T> complex<T> proj(const complex<T>&);
template<class T> complex<T> polar(const T&, const T& = 0);
```

```cpp
// 29.5.8. transcendent函数
template<class T> complex<T> acos(const complex<T>&);
template<class T> complex<T> asin(const complex<T>&);
template<class T> complex<T> atan(const complex<T>&);
```

```cpp
template<class T> complex<T> asosh(const complex<T>&);
template<class T> complex<T> asinh(const complex<T>&);
template<class T> complex<T> atanh(const complex<T>&);
```

```cpp
template<class T> complex<T> cos(const complex<T>&);
template<class T> complex<T> cosh(const complex<T>&);
template<class T> complex<T> exp(const complex<T>&);
template<class T> complex<T> log(const complex<T>&);
template<class T> complex<T> log(const complex<T>&);
```

```cpp
template<class T> complex<T> pow(const complex<T>&, const T&);
template<class T> complex<T> pow(const complex<T>&, complex<T>&);
template<class T> complex<T> pow(const T&, const complex<T>&);
```

```cpp
template<class T> complex<T> sin(const complex<T>&);
template<class T> complex<T> sinh(const complex<T>&);
template<class T> complex<T> sqrt(const complex<T>&);
template<class T> complex<T> tan(const complex<T>&);
template<class T> complex<T> tanh(const complex<T>&);
```

```cpp
// 29.5.10. 复数字字量
inline namespace complex_literals {
constexpr complex<long double> operator""il(long double);
constexpr complex<long double> operator""il(unsigned long long);
constexpr complex<double> operator""i(long double);
constexpr complex<double> operator""i(unsigned long long);
constexpr complex<float> operator""if(long double);
constexpr complex<float> operator""if(unsigned long long);
}
```

## 29.5.2 类模板 complex [complex]

```cpp
namespace std {
template<class T> class complex {
public:
  using value_type = T;
```

```cpp
constexpr complex(const T& re = T(), const T& im = T());
constexpr complex(const complex<T>&);
template<class U> constexpr complex(const complex<U>& constx);
```

```cpp
constexpr T real();
void real();
```

```cpp
constexpr T imag() const;
void imag(T);

complex<T>& operator+=(const T&);
complex<T>& operator+=(const T&);
complex<T>& operator-=(const T&);
complex<T>& operator*=(const T&);
complex<T>& operator/=(const T&);

complex<T> operator=(const complex<T>);
template<class X> complex<X>& operator=(const complex<X>&);
template<class X> complex<X>& operator++(const complex<X>&);
template<class X> complex<X>& operator-=(const complex<X>&);
template<class X> complex<X>& operator*=(const complex<X>&);
template<class X> complex<X>& operator/=(const complex<X>&);
}
```

- 1 该类描述了一个可以存储复数的笛卡尔分量（实部 real() 和虚部 imag()）的对象。

## 29.5.3 complex 特化版本

```cpp
namespace std {
template<class type> complex<float> {
public:
    using value_type = float;

    constexpr complex(float re = 0.0f, float im = 0.0f);
    constexpr explicit complex(const complex<double>& complex);
    constexpr explicit complex(const complex<long double>& complex);

    constexpr float real() const;
    void real(float);
    constexpr float imag() const;
    void imag(float);

    complex<float>& operator=(float);
    complex<float>& operator+=(float);
    complex<float>& operator-=(float);
    complex<float>& operator*=(float);
    complex<float>& operator/=(float);

    complex<float> operator=(const complex<float>&);
template<class X> complex<float>& operator=(const complex<X>&);
template<class X> complex<float>& operator++(const complex<X>&);
template<class X> complex<float>& operator-=(const complex<X>&);
template<class X> complex<float>& operator*=(const complex<X>&);
template<class X> complex<float>& operator/=(const complex<X>&);
}

template<class type> complex<double> {
public:
    using value_type = double;

    constexpr complex(double re = 0.0, double im = 0.0);
    constexpr complex(const complex<float>& complex);
[特化版本]

```cpp
constexpr explicit complex(const complex<long double>& complex);

constexpr double real() const;
void real(double);
constexpr double imag() const;
void imag(double);

complex<double>& operator=(double);
complex<double>& operator+=(double);
complex<double>& operator-=(double);
complex<double>& operator*=(double);
complex<double>& operator/=(double);

complex<double>& operator=(const complex<double>);
template<class X> complex<double>& operator=(const complex<X>&);
template<class X> complex<double>& operator++(const complex<X>&);
template<class X> complex<double>& operator-=(const complex<X>&);
template<class X> complex<double>& operator*=(const complex<X>&);
template<class X> complex<double>& operator/=(const complex<X>&);
```

```cpp
template<> complex<long double> {
public:
    using value_type = double;

    constexpr double re = 0.0, long double im = 0.0;
    constexpr complex(const complex<float>& complex);
    constexpr complex(const complex<long double>& complex);

    constexpr double real() const;
    void real(double);
    constexpr double imag() const;
    void imag(double);

    complex<long double>& operator=(double);
    complex<long double>& operator+=(double);
    complex<long double>& operator-=(double);
    complex<long double>& operator*=(double);
    complex<long double>& operator/=(double);
}
```

## 29.5.4 complex 成员函数 [complex.members]

```cpp
template<class T> complex(const T& re = T(), const T& im = T());
```

- 构造一个复数对象。
- 前置条件：real() && imag()

```cpp
constexpr T real() const;
- 返回：实部的值。

void real(T val);
- 影响：将 val 赋值给实部。

constexpr T imag() const;
- 返回：虚部的值。

void imag(T val);
- 影响：将 val 赋值给虚部。

## 29.5.5 complex 成员运算符 [complex.member.ops]

```cpp
complex<T> operator=(const T& rhs);
- 影响：将 rhs 赋值给复数 *this 的实部，保持虚部不变。

complex<T> operator-(const T& rhs);
- 影响：从复数 *this 的实部中减去 rhs，并将结果存储在实部，保持虚部不变。

complex<T> operator*(const T& rhs);
- 影响：用 rhs 乘以复数 *this，并将结果存储在 *this。

complex<T> operator/(const T& rhs);
- 影响：用 rhs 除复数 *this，并将结果存储在 *this。

template<class X> complex<T>& operator+=(const complex<X>& rhs);
- 影响：将 rhs 加到复数 *this，并将和存储在 *this。
- 返回：*this。

template<class X> complex<T>& operator-=(const complex<X>& rhs);
- 影响：从复数 *this 中减去 rhs，并将差值存储在 *this。
- 返回：*this。

template<class X> complex<T>& operator*=(const complex<X>& rhs);
- 影响：用 rhs 乘以复数 *this，并将乘积存储在 *this。
- 返回：*this。

template<class X> complex<T>& operator/=(const complex<X>& rhs);
- 影响：用 rhs 除复数 *this，并将商存储在 *this。
- 返回：*this。

## 29.5.6 complex 非成员运算符 [complex.ops]

```cpp
template<class T> complex operator+(const complex<T>& lhs);
- 返回：complex<T>(lhs)。
- 备注：元运算符。

template<class T> complex operator+(const complex<T>& lhs, const complex<T>& rhs);
template<class T> complex operator+(const complex<T>& lhs, const T& rhs);
template<class T> complex operator+(const T& lhs, const complex<T>& rhs);
- 返回：complex<T>(lhs) += rhs;

template<class T> complex operator-(const complex<T>& lhs, -lhs.imag());
- 返回：complex<T>(-lhs.real(), lhs.imag());
- 备注：元运算符。

template<class T> complex operator-(const complex<T>& lhs, const complex<T>& rhs);
template<class T> complex operator-(const complex<T>& lhs, const T& rhs);
template<class T> complex operator-(const T& lhs, const complex<T>& rhs);
- 返回：complex<T>(lhs) - rhs;

template<class T> complex operator*(const complex<T>& lhs, const complex<T>& rhs);
template<class T> complex operator*(const complex<T>& lhs, const T& rhs);
template<class T> complex operator*(const T& lhs, const complex<T>& rhs);
- 返回：complex<T>(lhs) * rhs;

template<class T> bool operator==(const complex<T>& lhs, const complex<T>& rhs);
template<class T> bool operator==(const complex<T>& lhs, const T& rhs);
template<class T> bool operator==(const T& lhs, const complex<T>& rhs);
- 返回：lhs.real() == rhs.real() && lhs.imag() == rhs.imag();
- 备注：对于 T 参数，虚部假设为 T 或 0.0。

template<class T, charT, class classes>
basic_istream<charT, traits<T>> operator>>>(basic_istream<charT, traits<T>>&, complex<T> & x);
- 要求：输入值应可转换为 T。
- 影响：提取格式为 (u, v) 或 (u,v) 的复数 x，其中 u 是实部 v 是虚部 (30.7.4.2)。
- 如果遇到坏输入，调用 is.setstate(ios_base::failbit)（这可能触发 ios::failure (30.5.5.4)）。
- 返回：is;
```