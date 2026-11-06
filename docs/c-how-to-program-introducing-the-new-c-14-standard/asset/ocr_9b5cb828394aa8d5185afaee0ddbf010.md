# Section 5.7.2 Class *DollarAmount*

+   - On most computers, an `int` is a value from −2,147,483,647 to 2,147,483,647—way too small for many monetary applications.
+   - C++11’s `long long` (p. **176**) type supports values in the range —9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 as a minimum.
+   - The range of `long long` (and C++’s other integer types) can vary across platforms. For portability, C++11 introduced new integer-type names so you can choose the appropriate range of values for your program. An `int64_t` (p. **177**) supports the exact range —9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.
+   - For a list of C++11’s integer-type names, see the header `<cstdint>` (p. **177**).
+   - A member function can access both the `private` data of the object on which that function is called and the `private` data of other objects of the same class that are passed to the function.
+   - In half-up rounding, values .5 and higher round up and everything else rounds down.
+   - C++ Standard Library function `to_string` (p. **178**; from header `<string>`) converts a numeric value to a `string` object.
+   - C++ Standard Library function `abs` (p. **178**; from header `<cmath>`) returns the absolute value of its argument.
+   - “Adding” string literals and `string` objects using the + operator is known as string concatenation (p. **178**).