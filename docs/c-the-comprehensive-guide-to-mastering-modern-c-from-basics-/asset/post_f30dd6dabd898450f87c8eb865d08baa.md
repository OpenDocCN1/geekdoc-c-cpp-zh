
must already be determined at compile time. This is particularly noticeable with array. You might be tempted to do one of the following things:

```cpp
void calculateImArray(int n) {
    array<int,n> data();      // n must be constant
    // ...
}
```

```cpp
long sumArray(array<int,n> data) { // where does this n come from?
    int sum = 0;
    for(int e : data) {
        sum += e;
    }
    return sum;
}
```

Neither is possible, as n is a variable that is only determined at runtime. At most, you can use simple calculations such as 3+4 or a constexpr.

But enough of the preview of array as a vehicle for the language feature of parameterized types. I'd better get specific now.

## Omission of the Element Type

With C++17, you can often omit the type parameters between the angle brackets. The compiler can determine the element type of the container using the constructor arguments:

```cpp
std::vector vec { 1, 2, 3 };
```

This is still a vector<int>, except that you can save yourself some typing. However, this is not always sensible (or possible):

```cpp
std::vector<std::string> elves { "Elrond", "Galadriel" };
using namespace std::literals;
std::vector dwarves { "Oin"s, "Glin"s };
```

With the suffix "s", you force string constructor arguments and get a vector<string> also for dwarfs.

## 6.4 The Simple Sequence Containers

- std::array
You specify the number of elements this container should hold at creation. It neither grows nor shrinks; you access its elements with an index or iterate over ranges.

- std::vector
This all-rounder stores its elements consecutively. You access its elements via a numeric index or iterate over ranges. In addition, it grows automatically when you add elements.

I strive not to use the ambiguous term arrays, but always write either `array` or `std::array` or `C-array`. In other sources, the latter is usually called `array`—or, or in some texts, `field[13]`.

> You use the array when you know how many elements you need. As you can see in the first line of main(), you specify the number of elements in the declaration. It cannot be changed later.

```cpp
// https://godbolt.org/z/cd1dW7T1
#include <array>
#include <iostream>

using std::cout; using std::array; using std::string;

int main() {
    array<string,7> wday = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" };
```

### 6.4.1 "array"

```cpp
    cout << "The week starts with " << wday[0] << "."; // read values
    cout << "It ends with " << wday.at(6) << "."; // read safely
    /* not another? */
    wday[5] = "Saturday"; // change
}
```

### Listing 6.7 You store a fixed number of elements in square brackets with "array".

You access the elements with wday[] and wday[5] via a number index; you can both read and write values. The alternative method at(index) is somewhat safer: while [] there is no check for whether you have used an index that is too large or too small, and your program may crash or worse (it continues to run with incorrect values), at() includes a check with which you can catch an error—or at least receive an error message before the program ends.

The number of elements in the declaration of wday may be a constant. You cannot use a variable whose value you have previously determined. As a number literal, 7 is of course constant. However, it is good style to declare such a number as a constant beforehand.

```cpp
// https://godbolt.org/z/fe7dmM4ex
#include <array>
#include <iostream>
constexpr size_t MONTHS = 12; /* months in year */

int main() {
    std::array<unsigned, MONTHS> wday = {
        31,28,31,30,31,31,30,31,30,30,30,31};
    unsigned age = 0;
    std::cout << "How old are you? " << std::cin >> age;

    std::array<int, 10> jan; // array size not by variable
} 
```

### Listing 6.8 The array size must be constant.

Figure 6.1 An "array" can neither grow nor shrink. Its elements are arranged compactly.

If you want to pass an array as a parameter to a function, its type must exactly match the array definition. Because array<int,4> is a different type than array<int,5> and array<short,4>, it would not match such a parameter type. constantly, to avoid repeating yourself you should give the array type its own name using a (or typedef) statement beforehand.

```cpp
// https://gdbbolt.org/z/a4xzbd99z
#include <array>
#include <algorithm>
#include <numeric>
using January = std::array<int, 10>; // alias

void init(January& jan) { // array parameter
    std::iota(jan.begin(), jan.end(), 1); // fills with 1
}

int main() {
    January jan; // declares
    init(jan);
}
```

| value | value | value | value | value |
|---|---|---|---|---|

