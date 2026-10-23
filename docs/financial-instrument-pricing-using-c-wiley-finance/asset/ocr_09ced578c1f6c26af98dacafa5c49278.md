```
std::cout << "Number of decimal digits representable without change:" << std::numeric_limits<T>::digits10 << "\n";
std::cout << "Smallest neg power of radix valid normalised number: " << std::numeric_limits<T>::min_exponent << "\n";
std::cout << "One more than largest power of radix that gives a valid floating point value: " << std::numeric_limits<T>::max_exponent << "\n";
}

template <typename T>
void NumericFunctions(const std::string& arithType)
{
std::cout << '\n' << "**Type: " << arithType << '\n';
std::cout << "Largest finite value: " << std::numeric_limits<T>::max();
std::cout << "Smallest finite value: " << std::numeric_limits<T>::min();
std::cout << "Lowest finite value: " << std::numeric_limits<T>::min();
std::cout << "Postive infinity value: " << std::numeric_limits<T>::infinity() << "\n";
std::cout << "Difference between 1.0 and next representable value: " << std::numeric_limits<T>::epsilon() << "\n";

std::cout << "F1 rounding: 0.5 to nearest digit, 1.0 to 0 or inf";
std::cout << "Maximum rounding rounding error: " << std::numeric_limits<T>::round_error() << "\n";

std::cout << "Return value for quiet NaN: " << std::boolalpha << std::numeric_limits<T>::quiet_NaN() << "\n";
std::cout << "Return value for signaling NaN: " << std::numeric_limits<T>::signaling_NaN() << "\n";

std::cout << "Smallest positive subnormal value: " << std::hex << std::numeric_limits<T>::denorm_min << "\n";
}

int main()
{
NumericConstants<float>("float");
NumericConstants<double>("double");

NumericFunctions<float>("float");
NumericFunctions<double>("double");

// 100-digit precision type from Boost multiprecision
// Discussed in Appendix C in more detail
namespace mp = boost::multiprecision;
NumericConstants<mp::cpp_dec_float_100>("100-digit type");
NumericFunctions<mp::cpp_dec_float_100>("100-digit type");
```