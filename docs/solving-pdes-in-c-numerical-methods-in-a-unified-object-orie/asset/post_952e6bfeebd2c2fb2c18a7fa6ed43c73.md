
## Figure 2.1. Schematic representation of inheritance.

![](img/1f293b0ceb2de964310ea7f941a1b580_110_0.png)

## Figure 2.2. Schematic representation of inheritance from the base class "point" to the derived class "complex".

![](img/1f293b0ceb2de964310ea7f941a1b580_110_1.png)

The "is a" concept in C++ is implemented by inheritance or derivation. The new class is derived from the "base" class and inherits its properties (see Figure 2.1). In the present example, the "complex" class is derived from the "point" class and inherits its properties as a point in the two-dimensional Cartesian plane (see Figure 2.2). On top of these properties, more arithmetic operations that are special to complex numbers can be defined in the derived "complex" class. These algebraic operations (multiplication and division of two complex numbers) complete the Cartesian plane from a mere vector space into a complete mathematical field.

```cpp
class complex : public point{
```

The word "public" before the name of the base class is optional. However, without it the derivation is private in the sense that the nonpublic functions in the base class are unavailable from objects or functions of the derived class. In other words, the derived class has the same access rights as ordinary classes. This way, the users are completely "unaware" of the derivation in the sense that they are unable to use objects from the derived class in functions written in terms of the base class. This is definitely what we want here: in fact, we definitely want users of the "complex" class to be able to add and subtract complex numbers as if they were mere "point" objects. Therefore, we use here public derivation by writing the word "public" before the name of the base class as in the above code line.

```cpp
public:
complex(const point& p) {
set(0,p[0]);
set(1,p[1]);
} // constructor with "point" argument

complex(double re=0., double im=0.){
set(0,re);
set(1,im);
} // constructor with "double" arguments
```

When a "complex" object is constructed, the underlying "point" object is first constructed by its own default constructor, which sets the values of its fields to 0. These values are then reset to their correct values obtained from the argument. This resetting must use the public "set" function in the "vector" template class in Section 2.18. It is impossible to change the components of a vector object directly because they are declared as private in the "vector" class and are thus inaccessible not only by users but also by deriv ers.

```cpp
friend complex operator+(const complex&){
return complex(c[0], -c[1]);
} // complex conjugate
```

Next, we define a friend function that calls the constructor to return the complex conjugate:

```cpp
const complex&operator+=(double);
const complex&operator-=(double);
const complex&operator*=(const complex&);
const complex&operator/=(const complex&);
};
```

This completes the block of the derived "complex" class.

The derived class has no access to the private fields of the base class. However, it has access to "half private" fields: fields that are declared as "protected" in the block of the base class by simply writing the reserved word "protected:" before their names. These fields are accessible by deriv ers only, not by other users. In fact, if the "component" field is declared "protected" in the base "vector" class, then it can be accessed from the derived "complex" class and set in its constructors directly. With the present implementation of the "vector" class in Section 2.18, however, the constructors of "complex" objects must access it indirectly through the public "set" function as above.

In summary, the members of a class are of three possible kinds:
- (a) public members that can be used by everyone;
- (b) private members that are accessible only to members and friends; and
- (c) protected members that are accessible to members and friends of derived classes (or when called in conjunction with current objects that have been derived by public derivation), but not to ordinary functions, even if they take arguments from the class or any other class derived from it (see Figure 2.3).

## Figure 2.3. The three kinds of members of a class (public, protected, and private) and their access pattern.

![](img/1f293b0ceb2de964310ea7f941a1b580_112_0.png)

When the derived object is constructed, the base class constructor is called first. Thus, the constructors in the derived class cannot use an initialization list for these fields, as they are already initialized to their default values. If these data fields are declared protected in the base class, then they can be reset in the body of the constructors of the derived class. If, on the other hand, they are private members of the base class, then they can be reset only indirectly through public member functions like "set" in the above example. In this example, the "set" function is applied to the "complex" object that is currently constructed. Since no such function is available in the derived "complex" class, the "complex" object is interpreted as a "point" object, and the "set" function of Section 2.18 is invoked to reset the data fields that represent the real and imaginary parts of the complex number to their correct values.

Similarly, when a "complex" object is passed as a concrete argument to a function, the compiler first looks for this function among the functions that take a "complex" argument. Only if no such function exists does it interpret the passed "complex" object as a "point" object and look for a function that takes a "point" argument.

When a derived object is destroyed, the data members inherited from the base class are destroyed last. This is done by the default destructor of the base class, which is invoked automatically at the end of the destruction and destroys the members inherited from the base class in reverse order to the order in which they are declared in it. For this reason, the destructor in the "complex" class needs to do nothing: the destructor in the base "point" class does the actual destruction implicitly. To invoke it, the default destructor available automatically in the "complex" class is sufficient, and no explicit destructor needs to be written.

The above discussion indicates that the process of inheritance suffers from slight overhead in terms of both time and storage due to the base object hidden behind every derived object. Still, it may be well worth it for the sake of elegant and transparent programming and for using objects that are already implemented properly to derive various kinds of more advanced objects. Furthermore, inheritance gives us the opportunity to follow the true concept of mathematical objects and the relation between them. It is particularly useful in high-level programming, where the programmer can concentrate on the special properties of the new object derived from more technical elementary objects.

The members of the base class also function as members of the derived class and can thus be used in the definition of its own members. Furthermore, since the derivation is public, the public members of the base class remain public in the derived class and can thus be used by its users.

Members of the base class can also be rewritten in the derived class. In this case, the version in the derived class overrides the version in the base class. For example, the `*=` and `/=` operators in the "complex" class override the corresponding operators in the base "point" class and are therefore used for "complex" objects. One can still call the version in the base class by adding a prefix of the form "base::" (where "base" stands for the name of the base class) before the function name to indicate that the old version is called. For example, `point::operator*=` invokes the `*=` operator in the base "point" class.

The unary `+` operator defined above also overrides the corresponding operator in the "point" class and returns the complex conjugate of a complex number. The `+` symbol is chosen for this purpose because it represents the only operator that leaves real numbers unchanged, as indeed does the complex-conjugate operator when applied to complex numbers with zero imaginary part. This operator is used in the division of complex numbers:

```cpp
const complex&
complex::operator*=(const complex& c) {
    double keep0 = (*this)[0];
    set(0,(*this)[0]*c[0]-(*this)[1]*c[1]);
    set(1,keep0*c[1]+(*this)[1]*c[0]);
    return *this;
}   // multiplying by complex

const complex&
complex::operator/=(const complex& c) {
    return *this *= (complex)((point)(+c)/=squaredNorm(c));
}   // dividing by complex
```

The above "/=" operator works as follows. Dividing by the complex number c̄ is the same as multiplying by c̄/|c|². First, |c|² is calculated by the "squaredNorm" function. Since the derived "complex" class has no such function, the argument c̄ is interpreted as a "point" object, and the "squaredNorm" function of the base "vector" class in Section 2.18 is invoked. The unary `+` operator, on the other hand, is available in both base and derived classes, so the version in the derived "complex" class overrides the version in the base "vector" class. As a result, `+c̄` is interpreted as the required complex conjugate c. Now, the compiler needs to invoke a "/=" operator to divide the "complex" object c̄ by the "double" number |c|². However, if one attempts to do this naively, then, since no division by "double" is available in the "complex" class, the compiler will implicitly convert the number |c|² from "double" to "complex" and invoke the "/=" operator recursively. Of course, this will lead to infinitely many recursive calls, with no result.

The cure to the above problem is to convert c̄ explicitly from "complex" to "point" by adding the prefix `(point)`, which converts a derived object to the underlying base object, while preserving its value. The "point" object c̄ is then divided by the scalar |c|² unambiguously by the "/=" operator of the "vector" class in Section 2.18, as required.

The resulting "point" object c̄/|c|² is then converted back to a "complex" object by the prefix `(complex)`, which invokes the constructor that takes a "point" argument and constructs a "complex" object with the same value. Since c̄/|c|² is now interpreted as a complex number, it can multiply the current "complex" object stored in "this", which completes the required division by the complex number c.
