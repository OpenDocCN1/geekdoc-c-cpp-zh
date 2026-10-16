The out-of-class definition of a member enumeration is only allowed for an enumeration for which we know the underlying type (§8.4). As usual, the enumerators of a nonclass enum are placed in the scope of the enumeration; that is, for a member enumeration, the enumerators are in the scope of its class.

# 23.4.6 Member Templates

A class or a class template can have members that are themselves templates. This allows us to represent related types with a pleasing degree of control and flexibility. For example, complex numbers are best represented as pairs of values of some scalar type:

```
template<typename Scalar>
class complex {
Scalar re, im;
public:
complex() :re{}, im{} {}
template<typename T>
complex(T rr, T ii =0) :re{rr}, im{ii} {}
// default constructor
complex(const complex&) = default; template<typename T>
// copyconstructor
complex(const complex<T>& c) : re{c.real()}, im{c.imag()} {}
//...
};
```

This allows mathematically meaningful conversions among complex types, while prohibiting the undesirable narrowing conversions (§10.5.2.6):

```
complex<float> cf;
complex<double> cd {cf}; complex<float> cf2 {cd};
complex<float> cf3 {2.0,3.0}; complex<double> cd2 {2.0F,3.0F}; // OK: uses float to double conversion
// default value
// OK: uses float to double conversion // error :no implicit double->float conversion
// error :no implicit double->float conversion
class Quad {
// no conversion to int
};
complex<Quad> cq;
complex<int> ci {cq}; // error :no Quad to int conversion
```

Given this definition of complex, we can construct a complex<T1> from a complex<T2> or from a pair of T2 values if and only if we can construct a T1 from a T2. That seems