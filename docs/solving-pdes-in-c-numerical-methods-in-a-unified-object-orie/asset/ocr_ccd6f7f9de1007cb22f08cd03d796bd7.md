```
complex(double re=0., double im=0.){
set(0,re);
set(1,im);
} // constructor with "double" arguments
```

When a "complex" object is constructed, the underlying "point" object is first constructed by its own default constructor, which sets the values of its fields to 0. These values are then reset to their correct values obtained from the argument. This resetting must use the public "set" function in the "vector" template class in Section 2.18. It is impossible to change the components of a vector object directly because they are declared as private in the "vector" class and are thus inaccessible not only by users but also by deriv ers.

```
friend complex operator+(const complex&){
return complex(c[0], -c[1]);
} // complex conjugate
```

Next, we define a friend function that calls the constructor to return the complex conjugate:

```
const complex&operator+=(double);
const complex&operator-=(double);
const complex&operator*=(const complex&);
const complex&operator/=(const complex&);
};
```

This completes the block of the derived "complex" class.

The derived class has no access to the private fields of the base class. However, it has access to "half private" fields: fields that are declared as "protected" in the block of the base class by simply writing the reserved word "protected:" before their names. These fields are accessible by deriv ers only, not by other users. In fact, if the "component" field is declared "protected" in the base "vector" class, then it can be accessed from the derived "complex" class and set in its constructors directly. With the present implementation of the "vector" class in Section 2.18, however, the constructors of "complex" objects must access it indirectly through the public "set" function as above.

In summary, the members of a class are of three possible kinds: (a) public members that can be used by everyone; (b) private members that are accessible only to members and friends; and (c) protected members that are accessible to members and friends of derived classes (or when called in conjunction with current objects that have been derived by public derivation), but not to ordinary functions, even if they take arguments from the class or any other class derived from it (see Figure 2.3).

When the derived object is constructed first by the default constructor of the base class. Thus, the constructors in the derived class cannot use an initialization list for these fields, as they are already initialized to their default values. If these data fields are declared protected in the base class, then they can be reset in the body of the constructors of the derived class. If, on the other hand, they are private members of the base class, then they can be reset only