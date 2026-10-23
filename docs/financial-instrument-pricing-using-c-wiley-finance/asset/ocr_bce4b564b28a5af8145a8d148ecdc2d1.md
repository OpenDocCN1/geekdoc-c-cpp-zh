```
// #include <boost/type_traits.hpp>      // Not needed anymore,
// now in C++

template <typename T> void IsArithmetic()
{ // First example of type_traits to check if T supports +,-,*,/

    if (std::is_arithmetic<T>::value)
    {
        std::cout << "This is an arithmetic type argument\n";
    }
    else
    {
        std::cout << "This is _not_ an arithmetic type argument\n";
    }
}

int main()
{
    IsArithmetic<int>();                        // true
    IsArithmetic<long double>();                // true
    IsArithmetic<std::complex<double>>();       // false
    IsArithmetic<std::string>();                // false

    // Compile-time fractional arithmetic
    const intmax_t numerator = 1;
    const intmax_t denominator = 2;
    using Half = std::ratio<numerator, denominator>;

    IsArithmetic<Half>();                      // false

    // Multiple precision types in Boost, chapter 8 of book
    using Multiprecision = boost::multiprecision::cpp_dec_float_100;
    IsArithmetic<Multiprecision>();            // false

    return 0;
}
```

Even in this simple example we can see the advantages because we can check whether a given type satisfies certain requirements and if not we can terminate the program by using a static assert (for example).

We also give an introduction to the concept of variadic templates. These are functions that accept a variable number of arguments. A template parameter pack is a template parameter that accepts zero or more template arguments. A function parameter pack is a function parameter that accepts zero or more function arguments. A template with at least one parameter pack is called a variadic template.

We take an example to show the use of variadic templates. To this end, we define two function types, both of which return a value. However, the first type expects one or more input arguments while the second type expects zero or more input arguments: