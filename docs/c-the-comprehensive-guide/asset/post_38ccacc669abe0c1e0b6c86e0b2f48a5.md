
## Chapter 28 Standard Library: Extras

### Chapter Topics

- **pair and tuple**: Anonymous structures that can be easily created on the spot—for example, for returning multiple values.
- **Regular expression**: Formal description of a pattern for text search.
- **Random number generator**: A mechanism that generates random values.
- **Random distribution**: Defines the probabilities via which a random number generator produces values.
- **time_point and duration**: Type-safe data types for point in time and duration.
- **ratio**: A type-safe fraction—that is, a number represented by an integer numerator and an equally integer denominator.
- **system_error**: Tools for portable error handling with error codes and exceptions.
- **`<typeinfo>`**: Runtime type information.
- **`<functional>`**: The `function` type is found in this header along with many predefined functor classes like `hash`, `bind`, `plus`, and `logical_and`.

In this chapter, you will find more classes and functions of the standard library.

### 28.1 “pair” and “tuple”

A tuple is something similar to an anonymous struct. Neither the struct itself nor its elements have names. You address the elements by their position. `pair` is older than `tuple` and encapsulates exactly two elements. These have the names `first` and `second`. You will often find both in the standard library because they are so useful. It is possible to bundle multiple elements of different types together without much syntactic overhead.

#### 28.1.1 Returning Multiple Values

Using a structure or class, you can also pack multiple pieces of data together and thus return multiple values from a function. In C++, however, there are special tools like `tuple` and `pair` to directly return multiple values of different types from a function using the return statement.

The use of `pair` is extremely simple. Primarily, you use `make_pair` to create.

```cpp
// https://godbolt.org/z/4YM9d99xG
#include <iostream>
#include <string>
#include <vector>
#include <utility> // pair
using std::pair; using std::cout; using std::cin; using std::string;
std::vector<string> months { "Jan", "Feb", "Mar" };
std::vector temps { 8, 12, 11 };
std::pair<string, int> monthWithTemp(size_t m) {
    auto month = months.at(m);
    auto temperature = temps.at(m);
    return std::make_pair(month, temperature);
}
int main() {
    std::pair data = monthWithTemp(1);
    cout << "Month : " << data.first << std::endl; // Output: Month : Feb
    cout << "Temperature : " << data.second << std::endl;
    // Output: Temperature: 12
}
```

Listing 28.1 How to return two values simultaneously using “pair”.

When declaring the `monthWithTemp` function, you can already tell from the return value that this function returns a `string` and an `int`. That's basically all you need to do. You just need to enter the two types (separated by a comma) between the angle brackets that should be returned. In `monthWithTemp(1)`, I call the function and also assign the return value to a `pair<string,int>`. The return is constructed from the two specified data using the `make_pair()` function and made into a `pair<string,int>`.

You can now access the individual values of `pair` using `first` (for the first value) and `second` (for the second value), as you can see in the example.

With `pair`, you are limited to exactly two elements. It is older than `tuple`, which is the generalization for any number of elements. You use it similarly.

```cpp
// https://godbolt.org/z/5z4s6WMxG
#include <iostream>
#include <string>
#include <algorithm> // min, max
#include <tuple>
using std::tuple; using std::make_tuple; using std::get; using std::cout;
using std::string;
tuple<int,int,int> arrange(int a, int b, int c) {
    using std::min; using std::max;
    auto x = min(a,min(b,c));
    auto y = max(min(a,b), min(max(a,b),c));
    auto z = max(a,max(b,c));
    return make_tuple(x, y, z);
}
auto president(int year) {
    using namespace std::literals;
    if(year >= 2021)
        return std::make_tuple("Joseph", "Biden", "Democratic", 1942);
    if(year >= 2017)
        return std::make_tuple("Donald", "Trump", "Republican", 1946);
    if(year >= 2009)
        return std::make_tuple("Barack", "Obama", "Democratic", 1961);
    // Add more presidents as needed...
    return std::make_tuple("", "", "", 0); // Default case
}
int main() {
    tuple<int,int,int> zs = arrange(23, 42, 7);
    cout << get<0>(zs) << ' ' << get<1>(zs) << ' ' << get<2>(zs) << '\n';
    // Output: 7 23 42
    auto ps = president(2015);
    cout << get<1>(ps) << '\n'; // Output: Obama
}
```

**Listing 28.2** With “tuple”, you can return any number of elements.

You combine multiple values of different types into a tuple using `make_tuple`. You can, as with `arrange` and `zs`, feel free to write out the tuple type. However, I recommend working with `auto`, as shown with `president` and `ps`. Here it is actually a `tuple<string, string, string, int>`, but you can save yourself the typing with `auto`.

Instead of accessing the elements with `first` and `second`, you now use `get<0>` and `get<1>`. For further elements, logically use larger numbers. Note that you can only specify fixed values (`constexpr`) as an index here. This does not work with variables.

You can even pass a type instead of a number, the type that you want.

```cpp
// https://godbolt.org/z/TETIECYPv
// ... as before ...
int main() {
    tuple ps = president(2015);
    cout << get<int>(ps) << '\n';   // Output: 1961
    cout << get<string>(ps) << '\n'; // not unique
}
```

Listing 28.3 "get" works with a type as an index.

Because `int` appears only once in `tuple<string, string, string, int>`, you can use `get<int>` to access the corresponding element. `get<string>` does not work because that would not be unique.

> **“array” as “tuple”**
>
> The real array container (see Chapter 24, Section 24.6.4) for a fixed number of elements of the same type also offers the possibility to access its elements with `get<>`.
> You can almost use an `array<int,3>` like a `tuple<int,int,int>`.

If accessing elements in this way is too cumbersome for you, then bind the return value of a function to variables with `tie`.

```cpp
// https://godbolt.org/z/GZgZYGfK
// ... as before ...
int main() {
    using std::tie; using std::ignore;
    string lastName {};
    int birthYear {};
    tie(ignore, lastName, ignore, birthYear) = president(2015);
    cout << lastName << ' ' << birthYear << '\n'; // Output: Obama 1961
}
```

Listing 28.4 Decomposing tuples with "tie" and "ignore".

When you use `tie` on the left side of an assignment as shown here, you can directly assign the individual parts of `tuple` and `pair` returns to previously declared variables. If you are only interested in parts of the return, then use `ignore` at the positions you are not interested in.

#### Structured Binding with “auto”

With C++17, it has become even easier to directly assign the returns of `tuple` or `array` to variables. This feature is called *structured binding*. This makes it possible to declare variables simultaneously.

```cpp
auto [a, lastname, c, birthyear] = president(2015);
```

Here, four variables are automatically declared with the correct types and initialized with the corresponding parts of the returned tuple. For this, the expression on the right side needs a "tuple-like interface"; that is, it must support `get<>` and `tuple_size<>`, which is the case for `array`, `tuple`, and `pair`.

A C-array or a struct can also be on the right side.

`tuple` has overloaded operators for comparisons, particularly `<` and `==`, which are necessary for algorithms like `sort` and the standard containers. If the first elements of a tuple are equal, then the second elements are compared, and so on. This is called *lexicographical order*, because it works like sorting words in a dictionary.

```cpp
// https://godbolt.org/z/sG4E66YhW
#include <iostream>
#include <string>
#include <tuple>
#include <vector>
#include <algorithm> // ranges::sort

using std::tuple; using std::get; using std::cout; using std::string;

int main() {
    std::vector<tuple<string,string,int>> armstrongs =
        { {"Armstrong", "Louis", 1901} // Initialize using initializer list
        , {"Armstrong", "Lance", 1971}
        , {"Armstrong", "Neil", 1930} };
    std::ranges::sort(armstrongs);    // Lance < Louis < Neil
    for(const auto& a : armstrongs) {
        cout << get<0>(a) << ", " << get<1>(a) << ", " << get<2>(a) << '\n';
    }
}
```

**Listing 28.5 Tuples implement lexicographical order.**

First, you can see that it is easy to initialize a tuple when the type is given. This is the case here with `vector<tuple<string,string,int>>`. Therefore, it is sufficient to initialize each individual element with an initializer list of two `const char[]`s and an `int`.

When `sort` is performed, the tuples are compared with each other. The first `"Armstrong"` elements are always the same, and the comparison is not yet conclusive. Therefore, the second element is considered—for example, `"Lance"` and `"Louis"`.
