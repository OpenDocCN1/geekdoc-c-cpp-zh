# Section 5.6.3 Random Numbers 131

There is no standard graphics library for C++, so I use “ASCII graphics.” Obviously, there are lots of open source and commercial graphics and GUI libraries for C++, but in this book I’ll restrict myself to ISO standard facilities.

For more information about random numbers, see §40.7.

# 5.6.4 Vector Arithmetic

The vector described in §4.4.1 was designed to be a general mechanism for holding values, to be flexible, and to fit into the architecture of containers, iterators, and algorithms. However, it does not support mathematical vector operations. Adding such operations to vector would be easy, but its generality and flexibility precludes optimizations that are often considered essential for serious numerical work. Consequently, the standard library provides (in <valarray>) a vector-like template, called valarray, that is less general and more amenable to optimization for numerical computation:

```
template<typename T>
class valarray {
//...
};
```

The usual arithmetic operations and the most common mathematical functions are supported for valarrays. For example:

```
void f(valarray<double>& a1, valarray<double>& a2)
{
valarray<double> a = a1*3.14+a2/a1; // numeric array operators *, +, /, and = a2 += a1*3.14;
a = abs(a);
double d = a2[7];
//...
}
```

For more details, see §40.5. In particular, valarray offers stride access to help implement multidimensional computations.

# 5.6.5 Numeric Limits

In <limits>, the standard library provides classes that describe the properties of built-in types – such as the maximum exponent of a float or the number of bytes in an int; see §40.2. For example, we can assert that a char is signed:

```
static_assert(numeric_limits<char>::is_signed,"unsigned characters!");
```