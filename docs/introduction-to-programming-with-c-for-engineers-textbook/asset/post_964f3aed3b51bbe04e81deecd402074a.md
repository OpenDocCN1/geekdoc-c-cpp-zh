
During the same iteration, the corresponding Roman digit, represented by the str string, is added to the final outStr object.

## Listing 3.28 Function to convert decimal numbers to Roman numerals (in CppBookCode, Dec2Roman.cpp).

```cpp
#include <iostream>
#include <vector>
#include <string>
using std::cout, std::cin, std::endl;
using std::vector, std::string, std::tuple;

// Converts decimal number in_dec_num into a Roman numeral string
auto ConvertDecimal_2_Roman( int in_dec_num )
{
    // The values need to be sorted from the largest one
    const vector< tuple< int, string > > RomanValueTranslator =
    {
        { 1000, "M" }, { 900, "CM" },
        { 500, "D" }, { 400, "CD" },
        { 100, "C" }, { 90, "XC" },
        { 50, "L" }, { 40, "XL" },
        { 10, "X" }, { 9, "IX" },
        { 5, "V" }, { 4, "IV" },
        { 1, "I" }
    };

    string outStr { " " };
    // Traverse all tuples [ val, str ], starting from the largest val
    for( const auto & [ val, str ] : RomanValueTranslator ) // structured binding
    while( in_dec_num >= val )
        outStr += str, in_dec_num -= val; // the largest possible value

    return outStr;
}
```

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_181_0.png)

## Listing 3.29 (continued)

```cpp
// Print the elements -- do not confuse the order
cout << "My/:" << get<0>(t_date) << " / " << get<1>(t_date) << " / " << get<2>(t_date) << endl;

// Retrieve the elements to separate objects
// with the structured binding
const auto [d, m, y] = t_date;

// Print the elements
cout << "My/:" << d << " / " << m << " / " << y << endl;

// Use the with ignore to retrieve a few elements
int d{};
string m{};

// Retrieve only day and month, ignore the year
tie(d, m, ignore) = t_date;

// Print
cout << "My/:" << d << " / " << m << endl;
```

```
// Print the elements
cout << "My/:" << get<0>(t_date) << " / " << get<1>(t_date) << " / " << get<2>(t_date) << endl;

// Retrieve the elements to separate objects
// with the structured binding
const auto [d, m, y] = t_date;

// Print the elements
cout << "My/:" << d << " / " << m << " / " << y << endl;
```

If a tuple has more objects, then accessing them by index can lead to confusion. In our case, the first and last elements are of the same type: `int`. So, writing `t_date(2019, "June", 27)` on line [3] could confuse the day with the year, since field semantics are assumed.

A similar data structure, this time obtained with `struct`, is shown in the right pane of Listing 3.29. The definition of the unnamed struct starts at line [2]. Then, on lines [5–7], the structure’s data members, `fDay`, `fMonth`, and `fYear` are defined. Unlike in the tuple, these can be accessed only² by providing the name of the object followed by a dot operator (GROUP 2, Table 3.15), followed by the member name. Then, on line [8], the `s_date` object is created. Its members are already initialized with the default values provided in their definitions. The data members of `s_date` are accessed and printed to the screen, as shown on lines [14–15]. Interestingly, structural binding also works with `struct`, as shown on lines [19–22].

So, when should we use `std::tuple`, and when should we use `struct`? Here are some hints.

Use `std::tuple` when:

- A collection of a few data objects of potentially different types is necessary. Storing too many objects can lead to confusion, since their meaning (semantics) is based on their position in a series
- No stress is laid on naming the data members
- It is fine that all elements are equally accessible to all objects that have access to the tuple
- We want to return multiple objects from a function (see Section 7.4.8)

Use `struct` (class) when:

- A collection of data objects with potentially different types is necessary
- Data member objects need to be easily identified by their names (strong semantics)
- Access rights need to be assigned to the members (i.e. `private`, `public`; see Section 4.3)
- Member functions are expected
- Inheritance is expected

But as always, there are cases when the two are equally good choices. And if the objects are of the same type, then `std::vector` or `std::array` can also be considered.

## 3.17.2 How to Write a Software Unit Test

Even more important than writing code is ensuring that the code executes the way we expect. This can be a tedious task even for short functions, not to mention huge software systems composed of dozens of libraries written over many years, etc. How can we get closer to certainty that our software is working properly? One way is to use unit tests – test functions that are embedded in a software testing framework and that run and verify the correctness of the corresponding software components. Some teams even start writing their code from unit tests, before they write any operational code. More information on software testing is provided in Appendix A.7. In this section, we will write a simple test function for our Roman numeral converter; see Listing 3.30.

`ConvertDecimal_2_Roman_UnitTest` checks the number of decimal values and, using `assert`, compares the output of the `ConvertDecimal_2_Roman` function with the corresponding Roman numerals. All must pass to return true. Otherwise, assert fires and stops execution. In practice, a more subtle behavior can be more useful, such as an entry to the log file, etc.

> ² This is a normal, natural, and recommended path, although there are some other tricky techniques with pointers.

## Listing 3.30 Unit test function for the decimal to Roman converter (in *CppBookCode, Dec2Roman.cpp*).

```cpp
// Unit test for ConvertDecimal_2_Roman
bool ConvertDecimal_2_Roman_UnitTest( void )
{
    assert( ConvertDecimal_2_Roman( 2000 ) == "MM" );
    assert( ConvertDecimal_2_Roman( 137 ) == "CXXXVII" );
    assert( ConvertDecimal_2_Roman( 1999 ) == "MCMXCVIV" );
    assert( ConvertDecimal_2_Roman( 2018 ) == "MMVIII" ); // a mistake to catch
    return true;
}
```

## 3.17.3 Automating Unit Tests – Using the Standard Random Number Library

In the previous section, we showed a simple unit test. The question remains, how many tests are enough? More often than not, we are not able to check all possible settings. In practice, randomly selected values or border conditions can be an option. In this section, we will learn:

- How to generate a vector of uniformly distributed random integers in a given range
- How to run automated tests on Roman-to-decimal and decimal-to-Roman conversions

For years, the function pair `rand` and `seed` was used to generate random integers. This was fine in simple applications, but in many cases the generated values were not truly “random” as expected. Since C++11, an advanced library is available to generate random numbers in various distributions (Stroustrup 2013). With the help of this facility, Listing 3.31 shows how to create a vector of uniformly distributed random integers.

To create a series of random numbers, three things are necessary: an initialization object, a random generation engine, and a random distribution, as shown in Figure 3.25.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_186_0.png)

**Figure 3.25** C++ chain for generating random numbers in a given distribution.

This example uses the Mersenne twister random engine `mt19937`. To do its job, it needs to be properly initialized. For this purpose, on line [17], a `random_device` object is created, which is then called in the constructor of `mtRandomEngine`.

On line [21], a `uniform_int_distribution` object is created. It will be responsible for generating a series of uniformly (but not yet randomly) distributed numbers in the range from `kFrom` to `kTo`. This series will be driven by the random engine created on line [19]. To generate random numbers of a given distribution and range, the following scheme has to be followed.

On line [23], an empty vector of `ints` is created. This is filled with random values on line [27] using the `generate_n` function from the SL library. Since `random_decimals` was created
