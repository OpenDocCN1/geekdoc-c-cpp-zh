that might lead compilers into an infinite loop. Fortunately, compilers do not stall on this and even give us a meaningful error message in this case (from the experience in the sense of Oscar Wilde that many programmers made this mistake before and some will in the future).

# 2.3.1.3 Conversion and Explicit Constructors

In C++, we distinguish between implicit and explicit constructors. Implicit constructors enable implicit conversion and assignment-like notation for construction. Instead of

```
complex c1(3.0); // <c++11 and higher
complex c1(3.0); // all standards
```

we can also write:

```
complex c1= 3.0;
```

or

```
complex c1= pi * pi / 6.0;
```

This notation is more readable for many scientifically educated people, while current compilers generate the same code for both notations.

The implicit conversion kicks in when one type is needed and another one is given, e.g., a double instead of a complex. Assume we have a function.²

```
double inline complex_abs(complex c)
{
    return std::sqrt(real(c) * real(c) + imag(c) * imag(c));
}
```

and call this with a double, e.g.:

```
cout << "|7| = " << complex_abs(7.0) << '\n';
```

The literal 7.0 is a double but there is no function overload for complex_abs accepting a double. We have, however, an overload for a complex argument and complex has a constructor accepting double. So, the complex value is implicitly built from the double literal.

The implicit conversion can be disabled by declaring the constructor as explicit:

```
class complex { public:
    explicit complex(double nr= 0.0, double i= 0.0) : r(nr), i(i) {}
};
```

Then complex_abs would not be called with a double. To call this function with a double, we can write an overload for double or construct a complex explicitly in the function call:

```
cout << "|7| = " << complex_abs(complex(7.0)) << '\n';
```

The explicit attribute is really important for some classes, e.g., vector. There is typically a constructor taking the size of the vector as an argument:

```
class vector
{
    public:
    vector(int n) : my_size(n), data(new double[my_size]) {}
};
```

2. The definitions of real and imag will be given soon.