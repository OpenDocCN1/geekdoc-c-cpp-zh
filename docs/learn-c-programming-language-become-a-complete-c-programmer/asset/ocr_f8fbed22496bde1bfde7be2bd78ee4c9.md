and access them through the part stored in the class object itself. That’s the way **vector** and **string** are implemented; they can be considered resource handles with carefully crafted interfaces.

# 3.2.1.1 An Arithmetic Type

The “classical user-defined arithmetic type” is **complex**:

```
class complex {
double re, im; // representation: two doubles
public:
complex(double r, double i) :re{r}, im{i} {} complex(double r) :re{r}, im{0} {}
complex() :re{0}, im{0} {}

// construct complex from two scalars // construct complex from one scalar // default
complex: {0,0}

double real() const { return re; } void real(double d) { re=d; } double imag() const {
return im; } void imag(double d) { im=d; }

complex& operator+=(complex z) { re+=z.re, im+=z.im; return *this; } // add to re
and im // and return the result
complex& operator-=(complex z) { re-=z.re, im-=z.im; return *this; }
complex& operator*=(complex); // defined out-of-class somewhere
complex& operator/=(complex); // defined out-of-class somewhere
};
```

This is a slightly simplified version of the standard-library **complex** (§40.4). The class definition itself contains only the operations requiring access to the representation. The representation is simple and conventional. For practical reasons, it has to be compatible with what Fortran provided 50 years ago, and we need a conventional set of operators. In addition to the logical demands, **complex** must be efficient or it will remain unused. This implies that simple operations must be inlined. That is, simple operations (such as constructors, **+=**, and **imag()**) must be implemented without function calls in the generated machine code. Functions defined in a class are inlined by default. An industrial-strength **complex** (like the standard-library one) is carefully implemented to do appropriate inlining.

A constructor that can be invoked without an argument is called a *default constructor*. Thus, **complex()** is **complex**’s default constructor. By defining a default constructor you eliminate the possibility of uninitialized variables of that type.

The **const** specifiers on the functions returning the real and imaginary parts indicate that these functions do not modify the object for which they are called. Many useful operations do not require direct access to the representation of **complex**, so they can be defined separately from the class definition:

```
complex operator+(complex a, complex b) { return a+=b; }
complex operator-(complex a, complex b) { return a-=b; }
complex operator-(complex a) { return {-a.real(), -a.imag()}; } // unary y minus
complex operator*(complex a, complex b) { return a*=b; }
complex operator/(complex a, complex b) { return a/=b; }
```