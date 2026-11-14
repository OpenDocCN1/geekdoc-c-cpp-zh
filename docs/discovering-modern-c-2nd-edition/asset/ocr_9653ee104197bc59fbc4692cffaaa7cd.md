```
class complex {
public:
	explicit complex(double nr= 0.0, double i= 0.0) : r(nr),
i(i) {}
};
```

Then complex_abs would not be called with a double. To call this function with a double, we can write an overload for double or construct a complex explicitly in the function call:

Click here to view code image

```
cout << "|7| = " << complex_abs(complex(7.0)) << '\n';
```

The explicit attribute is really important for some classes, e.g., vector. There is typically a constructor taking the size of the vector as an argument:

Click here to view code image

```
class vector
{
public:
	vector(int n) : my_size(n), data(new double[n]) {}
};
```

A function computing a scalar product expects two vectors as arguments:

Click here to view code image

```
double dot(const vector& v, const vector& w) { ... }
```

This function can be called with integer arguments:

```
double d = dot(8, 8);
```

What happens? Two temporary vectors of size 8 are created with the implicit constructor and passed to the function dot. This nonsense can be easily avoided by declaring the constructor explicit. Which constructor shall be explicit is in the end the class designer's decision. It is pretty obvious in the vector example: no right-minded programmer wants the compiler converting integers automatically into vectors and the fact that the assignment-like notation:

```
vector v = 8;
```