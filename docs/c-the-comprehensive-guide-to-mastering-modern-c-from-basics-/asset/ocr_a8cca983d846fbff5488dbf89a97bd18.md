```
cout << "The week starts with " << wday[0] << ".\
"; // read values
out << "It ends with " << wday.at(6) << ".\
"; // read safely
/* notthern? */
wday[5] = "Satdee"; // change
}
```

# Listing 6.7 You store a fixed number of elements in square brackets with "array".

You access the elements with wday[] and wday[5] via a number index; you can both read and write values. The alternative method at(index) is somewhat safer: while [] there is no check for whether you have used an index that is too large or too small, and your program may crash or worse (it continues to run with incorrect values), at() includes a check with which you can catch an error—or at least receive an error message before the program ends Chapter 10.

The number of elements in the declaration of wday may be a constant. You cannot use a variable whose value you have previously determined. As a number literal, 7 is of course constant. However, it is good style to declare such a number as a constant beforehand.

```
// https://godbolt.org/zfe7dmM4ex
#include <array>
#include <iostream>
constexpr size_t MONTHS = 12; /* months in year */

int main() {
    std::array<unsigned, MONTHS> wday = {
        31,28,31,30,31,31,30,31,30,30,30,31};
    unsigned age = 0;
    std::cout << "How old are you? " << std::cin >> age;

std::array<int, years of life; // array size not by
```