lots of open source and commercial graphics and GUI libraries for C++, but in this book I restrict myself to ISO standard facilities.
To get a repeated or different sequence of values, we seed the engine; that is, we give its internal state a new value. For example:

Click here to view code image

```
Rand_int rnd(10,20);
for (int i = 0; i<10; ++i) cout << rnd() << '\\n'; // 16 13 20 19 14 17 10 16 15 14
rnd.seed(999);
for (int i = 0; i<10; ++i) cout << rnd() << '\\n'; // 11 17 14 19 20 13 20 14 16 19
nd.seed(999);
for (int i = 0; i<10; ++i) cout << rnd() << '\\n'; // 11 17 14 19 20 13 20 14 16 19
```

Repeated sequences are important for deterministic debugging. With different values is important when you don't want repetition. If you need random numbers, rather than a generated pseudo-random sequence, look to see how random_device is implemented on your machine.

# 17.6 Vector Arithmetic

The vector was designed in §12.2 to be a general mechanism for holding values, rather than flexible, and to fit the architecture of containers, iterators, and algorithms. However it does not support mathematical vector operations. Adding operations to vector would be easy, but its generality and flexibility preclude optimizations that are considered essential for numerical work. Consequently, the standard library provides a <valarray>-like template, called valarray, that is less general and more amenable to optimization for numerical computation:

```
template<typename T>
class valarray {
// ...
};
```

The usual arithmetic operations and the most common mathematical functions are supported by valarray. For example:

Click here to view code&lt;double&gt;&&1, valarray&lt;double&gt;&2

```
void f(valarray<double> a = a1*3.14+a2/a1);
{
nvalarray<double> a = a1*3.14+a2/a1; // numeric array operations *, +, /, and =
a2 += a*3.14;
a = abs(a);
double b = a2[7];
// ...
```

The operations are vector operations; that is, they are applied to each element of the vectors involved.

In addition to arithmetic operations, valarray offers stride access to help implement