```
constexpr explicit complex(const complex<long double>);

constexpr double real() const;
void real(double);
constexpr double imag() const;
void imag(double);
```

```
complex<double>& operator=(double);
complex<double>& operator+=(double);
complex<double>& operator-=(double);
complex<double>& operator*=(double);
complex<double>& operator/=(double);
```

```
complex<double>& operator=(const complex<double>);
template<class X> complex<double>& operator=(const complex<X>);
template<class X> complex<double>& operator+=(const complex<X>);
template<class X> complex<double>& operator-=(const complex<X>);
template<class X> complex<double>& operator*=(const complex<X>);
template<class X> complex<double>& operator/=(const complex<X>);
```

```
template<> class complex<long double> {
public:
    using_type = double;
```

```
constexpr double re = 0.0L, long double im = 0.0L;
constexpr complex(const complex<float>);
constexpr complex(const complex<long double>);
```

```
constexpr double real() const;
void real(long double);
constexpr double imag() const;
void imag(long double);
```

```
complex<double>& operator=(const complex<long double>);
complex<double>& operator+=(long double);
complex<double>& operator-=(long double);
complex<double>& operator*=(long double);
complex<double>& operator/=(long double);
```

```
template<class X> complex<long double>& operator=(const complex<X>);
template<class X> complex<long double>& operator+=(const complex<X>);
template<class X> complex<long double>& operator-=(const complex<X>);
template<class X> complex<long double>& operator*=(const complex<X>);
template<class X> complex<long double>& operator/=(const complex<X>);
```

# 29.5.4 complex member functions

[complex.members]

```
template<class T> constexpr complex(const T& T(), const T& im = T());
```

+   Effects: Constructs an object of complex number.

+   Postconditions: real() == re && imag() == im.