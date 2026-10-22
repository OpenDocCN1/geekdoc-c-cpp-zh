```
template<typename... Types>
template<typename... SourceTypes>
Variant<Types...>::Variant(Variant<SourceTypes...> const& source) {
if (!source.empty()) {
source.visit([&](auto const& value) {
*this = value;
});
}
}
```

Because this code visits the source, the assignment to *this will occur for each of the types of the source variant. Overload resolution for this assignment will find the most appropriate destination type for each source type, performing implicit conversions as necessary. The following example illustrates construction and assignment from different variant types: Click here to view code image

# variant/variantpromote.cpp

```
#include "variant.hpp"
#include <iostream>
#include <string>

int main()
{
Variant<short, float, char const*> v1((short)123);

Variant<int, std::string, double> v2(v1);
std::cout << "v2 contains the integer " << v2.get<int>() << '\n';

v1 = 3.14f;
Variant<double, int, std::string> v3(std::move(v1));
std::cout << "v3 contains the double " << v3.get<double>() << '\n';

v1 ="hello";
Variant<double, int, std::string> v4(std::move(v1));
std::cout << "v4 contains the string " << v4.get<std::string>() <<
'\n';
}
```

Constructing or assigning from v1 to either v2 or v3 involves integral promotions (short to int), floating-point promotions (float to double), and user-defined conversions (char const* to std::string). The output of this program is as follows: v2 contains the integer 123
v3 contains the double 3.14
v4 contains the string hello