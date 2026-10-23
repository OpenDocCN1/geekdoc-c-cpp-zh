```
template <typename T>
void classify(const T& t)
{
    std::cout << "*Value: " << t << '\n';
    std::cout << "\tFinite: " << std::isfinite(t) << '\n';
    std::cout << "\tInfinite: " << std::isinf(t) << '\n';
    std::cout << "\tIs NaN: " << std::isnan(t) << '\n';
    std::cout << "\tIs Normal: "<< std::isnormal(t) << '\n';
    std::cout << "\tIs Negative: " << std::signbit(t) << '\n';
}
```

# 8.3 A TOUR OF std::numeric_limits<T>

This class template provides a standardised way to query various properties of arithmetic types. It offers a number of member constants and member functions that can be used in applications. A specialisation exists for each cv (const volatile) qualified version of each arithmetic type in addition to each unqualified specialisation. We note that non-arithmetic standard types (for example, std::complex<T>) do not have specialisations.

```
template <typename T>
void NumericConstants(const std::string& arithType)
{
    std::cout << '\n' << "**Type: " << arithType
              << "\n, #representable digits: "
              << std::numeric_limits<T>::digits << "\n";

    // Infinity, NaN and detection of denormalisation/subnormal numbers
    std::cout << "Has a special value for infinity: " << std::boolalpha
              << std::numeric_limits<T>::has_infinity << "\n";
    std::cout << "Has a special value for quiet NaN: " << std::boolalpha
              << std::numeric_limits<T>::has_quiet_NaN << "\n";
    std::cout << "Has a special value for signaling NaN: "<< std::boolalpha
              << std::numeric_limits<T>::has_signaling_NaN << "\n";

    std::cout << "Float subnormal styles: -1 == indeterminate, 0 == absent, 1 == present: " << "\n";
    std::cout << "Supports subnormal values: "
              << std::numeric_limits<T>::has_denorm << "\n";
    std::cout << "Detects subnormal loss of precision: " << std::boolalpha
              << std::numeric_limits<T>::has_denorm_loss << "\n";

    std::cout << "Float rounding style (see std::float_round_style): "
              << std::numeric_limits<T>::round_style << "\n";

    // Digits etc.
    std::cout << "For int/floats, number of essential bits or digits in significand: " << std::numeric_limits<T>::digits << "\n";
```