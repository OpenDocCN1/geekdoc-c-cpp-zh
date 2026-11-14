doesn't compile since no multiplication is defined for int and complex<double>. The problem is easily fixed by replacing 2 with 2.0. However, the issue is more annoying in generic functions, e.g.:

```
```cpp
template <typename T>
inline T twice(const T& z)
{
    return 2 * z;  // Error!
}

int main ()
{
    complex<double> z(3, 5), c;
    c = twice(z);
}
```
```

The function twice will not compile for the same reason as before. If we wrote 2.0 * z it would compile for complex<double> but not for complex<float> or complex<long double>. The function

```
```cpp
template <typename T>
complex<T> twice(const complex<T>& z)
{
    return T(2) * z;
}
```
```

works with all complex types—but only with complex types. In contrast, the following:

```
```cpp
template <typename T>
inline T twice(const T& z)
{
    return T(2) * z;
}
```
```

compiles with complex and non-complex types. However, when T is a complex type, 2 is unnecessarily converted into a complex and four multiplications plus two additions are performed where only half of them are needed. A possible solution is to overload the last two implementations. Alternatively, we can write type traits to deal with it.

The programming becomes more challenging when multiple arguments of different types are involved, some of them possibly complex numbers. The Matrix Template Library (MTL4, Section 4.7.3) provides mixed arithmetic for complex numbers. We are committed to incorporate this feature into future standards.

# ## 4.2.2 Random Number Generators

Many application domains—like computer simulation, game programming, or cryptography—use random numbers. Every serious programming language thus offers generators for them. Such generators produce sequences of numbers that appear random. A random generator may depend on physical processes like quantum phenomena. However, most generators are based on pseudo-random calculations. They have an internal state—called a Seed—that is transformed by deterministic computation each time a pseudo-random number is requested. Thus, a pseudo-random number generator (PRNG) always emits the same sequence when started with the same seed.

Before C++11, there were only the rand and srand functions from C with very limited functionality. More problematic is that there are no guarantees for the quality of generated numbers and it is indeed quite low on some platforms. Therefore, a high-quality <random>