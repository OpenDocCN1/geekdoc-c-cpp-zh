```
complex<T>& operator+=(const complex<X>&);
// ...
};
```

Note that the scalar assignment operators take reference arguments. That’s not efficient for floats, so complex<float> passes those by value:

```
template<>
class complex<float> {
public:

// ...
complex<float>& operator= (float);
complex<float>& operator+=(float);
// ...
complex<float>& operator=(const complex<float>&);
```

For complex<double>, that same optimization applies. In addition, conversions from complex<float> and complex<long double> are provided (as described in §23.4.6):

```
template<>
class complex<double> {
public:

constexpr complex(double re = 0.0, double im = 0.0);
constexpr complex(const complex<float>&);
explicit constexpr complex(const complex<long double>&);
// ...
};
```

Note that these specialized constructors are constexpr, making complex<double> a literal type. We could not do that for the general complex<T>. Also, this definition takes advantage of the knowledge that conversion from complex<float> to complex<double> is safe (it never narrows), so that we can have an implicit constructor from complex<float>. However, the constructor from complex<long double> is explicit to make narrowing less likely.

# 25.3.1.1 Implementation Specialization

Specialization can be used to provide alternative implementations of a class template for a specific set of template parameters. In that case, a specialization can even provide a representation that differs from that of the general template. For example:

```
template<typename T, int N>
class Matrix; // N-dimensional Matrix of Ts
```

```
template<typename T,0>
class Matrix { // specialization for N==1 Tval;
// ...
};
```

```
template<typename T,1>
class Matrix { // specialization for N=1 T* elem;
```