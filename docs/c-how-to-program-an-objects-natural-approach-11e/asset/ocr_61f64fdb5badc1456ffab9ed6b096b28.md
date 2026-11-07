```
```cpp
// fig19_22.cpp
// C++20 text formatting numeric formatting options.
#include <format>
#include <iostream>

int main() {
   std::cout << "Displaying signs and padding with leading 0s:\n"
             << std::format("{:+010d}\n{:+010d}\n", 27, -27);

   std::cout << "Displaying a space before a positive value:\n"
             << std::format("{:0d}\n{: d}\n", 27, -27);

   std::cout << "Displaying a base indicator before a number:\n"
             << std::format("{:#0b}\n{:#0x}\n", 100);
}
```
```

```
```text
Displaying signs and padding with leading 0s:
[+00000027]
[-00000027]

Displaying a space before a positive value:
27
 27
-27

Displaying a base indicator before a number:
100
0b1100100
0144
0x64
```
```

**Fig. 19.22**  |  C++20 text-formatting numeric formatting options.

# 19.9.4 C++20 `std::format` Field Width and Precision Placeholders

You can programmatically specify field widths and precisions using nested placeholders in a format specifier. Figure 19.23 displays the double value 123.456 in a field of 8 characters with precisions of 0–4. In line 13, the argument value is the number to format. In the format specifier `{:{}.{}f}`, the nested placeholders to the right of the colon (:) are replaced left-to-right by the values of the arguments width and precision, respectively.

```
```cpp
// fig19_23.cpp
// C++20 text formatting field width and precision placeholders.
#include <format>
#include <iostream>

int main() {
   std::cout << "Demonstrating field width and precision placeholders:\n";

   double value{123.456};
   int width{8};
```
```

**Fig. 19.23**  |  C++20 text-formatting field width and precision placeholders.