```
constexpr complex(const complex<float>&);
explicit constexpr complex(const complex<long double>&);
```

```
constexpr double real(); void real(double);
constexpr double imag(); void imag(double);
```

```
// read the real part
// set the real part
// read the imaginarypar t // set the imaginarypar t
```

```
complex<double>& operator= (double);
complex<double>& operator+=(double);
//...
```

```
};
```

Obviously, operations, such as = and +=, that modify an object cannot be constexpr. Conversely, operations that simply read an object, such as real() and imag(), can be constexpr and be evaluated at compile time given a constant expression. The interesting member is the template constructor from another complex type. Consider:

```
constexpr complex< float> z1 {1,2}; constexpr double re = z1.real();
constexpr double im = z1.imag(); constexpr complex<double> z2 {re,im}; constexpr complex<double> z3 {z1};
```

```
// note: <float> not <double>
// z2 becomes a copyofz1 // z3 becomes a copyofz1
```

# Section 10.4.4 Reference Arguments 267

The copy constructor works because the compiler recognizes that the reference (the const complex<float>&) refers to a constant value and we just use that value (rather than trying anything advanced or silly with references or pointers).

Literal types allow for type-rich compile-time programming. Traditionally, C++ compile-time evaluation has been restricted to using integer values (and without functions). This has resulted in code that was unnecessarily complicated and error-prone, as people encoded every kind of information as integers. Some uses of template metaprogramming (Chapter 28) are examples of that. Other programmers have simply preferred run-time evaluation to avoid the difficulties of writing in an impoverished language.

# 10.4.5 Address Constant Expressions

The address of a statically allocated object (§6.4.2), such as a global variable, is a constant. However, its value is assigned by the linker, rather than the compiler, so the compiler cannot know the value of such an address constant. That limits the range of constant expressions of pointer and reference type. For example:

```
constexpr const char * p1 = “asdf”;
constexpr const char* p2 = p1; // OK
constexpr const char* p2 = p1+2; // error :the compiler does not knowthe value of p1
constexpr char c = p1[2]; // OK, c==‘d’; the compiler knows the value pointed to byp1
```