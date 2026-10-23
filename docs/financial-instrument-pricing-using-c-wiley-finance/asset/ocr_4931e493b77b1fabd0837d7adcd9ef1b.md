```
```cpp
std::string s("1.3");
//std::cout << ArithmeticCompute(s) << '\n';    // Error

//std::cout << NonArithmeticCompute(d) << '\n'; // Error

std::cout << NonArithmeticCompute(s) << '\n';   // OK
```
```

A final example: many numerical processes need to support both floating-point and complex numbers. Let us suppose that we develop an algorithm and that we wish to restrict the data types to double and std::complex<double>. Then the following code satisfies this requirement:

```
```cpp
template <typename T> typename boost::enable_if_c
  <std::is_same<T, double>::value
   || std::is_same<T, std::complex<double>>::value, T>::type
Exponential(T t)
{ // Only for double or complex<double>

    return std::exp(t);
}
```
```

An example of use is:

```
```cpp
// Exponential for double or complex<double>
double x = 3.2;
std::complex<double> c(1.0, 2.0);
float f = 3.0F;
std::cout << Exponential<double>(x) << '\n';                         // OK
std::cout << Exponential<std::complex<double>>(c) << '\n';          // OK
//std::cout << Exponential<float>(f) << '\n';                        // Error
```
```

Here we also see that float is not allowed and a compiler error will result if we try to use it. More generally, the function Exponential only accepts doubles and complex numbers.

As a concluding remark, we note that many of the language features in C++ started life as one or more Boost libraries. In general, Boost tends to offer more extensive functionality, examples and documentation than C++ at the moment of writing. For this reason we recommend keeping up to date with developments in Boost and its online documentation.

# 4.8  `std::decay()` TRAIT

This is another piece of exotic syntax in C++. It can best be understood as a function that transforms a given type into a simpler type. In general terms, it removes *extraneous* or other secondary information from a type. The transformed type (called the *decay type*) is aliased as `std::decay::type`. The conversion resembles implicit conversions that take place when an argument is passed by value to a function.