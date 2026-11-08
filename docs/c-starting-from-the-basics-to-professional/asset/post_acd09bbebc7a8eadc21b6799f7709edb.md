
Unlike standard arrays, you can also assign one `array<>` container to another, as long as they both store the same number of elements of the same type. Here's an example:

```cpp
them = those;        // Copy all elements of those to them
```

Moreover, `array<>` objects can be stored inside other containers. Regular arrays cannot. The following, for instance, uses a `vector<>` container that can hold `array<>` objects as elements, each in turn containing three `int` values:

```cpp
std::vector<std::array<int, 3>> triplets;
```

The `vector<>` container is discussed in the next section.

## Conclusion and Example

The takeaway should be clear by now: always choose `array<>` containers in your code over standard arrays. We've given you plenty of reasons already—at least seven by our count. And what's more, there's absolutely no disadvantage to using `array<>` either. Using an `array<>` container can outperform an array compared to a standard array. (That is, unless you use the `at()` function instead of the `[]` operator of `array<>`—bounds checking, of course, may come at a small runtime cost.)

> **Note**  Even if you use `std::array<>` containers in your code, it still remains perfectly possible to call legacy functions that expect plain arrays as input. You can always access the built-in array that is encapsulated within the `array<>` object using its `data()` member.

Here's an example that demonstrates `array<>` containers in action:

```cpp
// Ex5_14.cpp
// Using array<T,N> to create Body Mass Index (BMI) table
// BMI = weight/(height*height)
// weight in kilograms, height in meters

import <iostream>;
import <format>;
import <array>;        // For array<T,N>

int main()
{
    const unsigned min_wt {100};       // Minimum weight in table (in pounds)
    const unsigned max_wt {250};       // Maximum weight in table (in pounds)
    const unsigned wt_step {10};
    const size_t wt_count {1 + (max_wt - min_wt) / wt_step};

    const unsigned min_ht {48};        // Minimum height in table (inches)
    const unsigned max_ht {84};        // Maximum height in table (inches)
    const unsigned ht_step {2};
    const size_t ht_count {1 + (max_ht - min_ht) / ht_step };

    const double lbs_per_kg {2.2};   // Pounds per kilogram
    const double ins_per_m {39.37};  // Inches per meter
    std::array<unsigned, wt_count> weight_lbs {};
    std::array<unsigned, ht_count> height_ins {};

    // Create weights from 100lbs in steps of 10lbs
    for (unsigned i{0}, w{min_wt}; i < wt_count; w += wt_step, ++i)
    {
        weight_lbs[i] = w;
    }
    // Create heights from 48 inches in steps of 2 inches
    for (unsigned i{0}, h{min_ht}; h <= max_ht; h += ht_step)
    {
        height_ins.at(i++) = h;
    }
    // Output table headings
    std::cout << std::format("{:>8}", '|');
    for (auto & w : weight_lbs)
        std::cout << std::format("{:^6}|", w);
    std::cout << std::endl;

    // Output line below headings
    for (unsigned i{1}; i < wt_count; ++i)
        std::cout << "--------";
    std::cout << std::endl;

    const unsigned inches_per_foot {12};
    for (auto h : height_ins)
    {
        const unsigned feet = h / inches_per_foot;
        const unsigned inches = h % inches_per_foot;
        std::cout << std::format("{:>2}'{:>2}\" |", feet, inches);

        const double h_m = h / ins_per_m;      // Height in meter
        for (auto w : weight_lbs)
        {
            const double w_kg = w / lbs_per_kg; // Weight in kilogram
            const double bmi = w_kg / (h_m * h_m);
            std::cout << std::format("{:2.1f}|", bmi);
        }
        std::cout << std::endl;
    }
    // Output line below table
    for (size_t i {1}; i < wt_count; ++i)
        std::cout << "--------";
    std::cout << "\nBMI from 18.5 to 24.9 is normal" << std::endl;
}
```

We leave you to run the program to see the output because it takes quite a lot of space. There are two sets of four `const` variables defined that relate to the range of weights and heights for the BMI table. The weights and heights are stored in `array<>` containers with elements of type `unsigned` (short for `unsigned int`) because all the weights and heights are integral. The containers are initialized with the appropriate values in `for` loops. The second loop that initializes `height_ins` uses a different approach to setting the values just to demonstrate the `at()` function. This is appropriate in this loop because the loop is not controlled by the index limits for the container, so it is possible that a mistake could be made that would use an index outside the legal range for the container. The program would be terminated if this occurred, which would not be the case using square brackets to reference an element.

The next two `for` loops output the table column headings and a line to separate the headings from the rest of the table. The table is created using nested range-based `for` loops. The outer loop iterates over the heights and outputs the height in the leftmost column in feet and inches. The inner loop iterates over the weights and outputs a row of BMI values for the current height.

## Using std::vector<T> Containers

The `vector<T>` container is a sequence container that may seem much like the `array<T,N>` container, but that is in fact far more powerful. There's no need to know the number of elements a `vector<>` will store in advance at compile time. In fact, there is even no need to know the number of elements it will store in advance at runtime. That is, the size of a `vector<>` can grow automatically to accommodate any number of elements. You can add some now and then some more later. You can remove some in the middle and then insert some more. It's all very easy with a `vector<>` container. A `vector<>` will grow as you add more and more elements; additional space is allocated automatically whenever required. There is no real maximum number of elements either—other than the one imposed by the amount of memory available to your process, of course—which is the reason you need only the type parameter `T`. There's no need for the `N` with a `vector<>`. Using the `vector<>` container needs the `<vector>` module to be imported in your source file.

Here's an example of creating a `vector<>` container to store values of type `double`:

```cpp
std::vector<double> values;
```

This typically has no space for elements allocated yet, so memory will need to be allocated dynamically when you add the first data item. You can add an element using the `push_back()` function for the container object. Here's an example:

```cpp
values.push_back(3.1415);    // Add an element to the end of the vector
```

The `push_back()` function adds the value you pass as the argument—3.1415 in this case—as a new element at the end of the existing elements. Since there are no existing elements here, this will be the first, which probably will cause memory to be allocated for the first time.

You can initialize a `vector<>` with a predefined number of elements, like this:

```cpp
std::vector<double> values(20);    // Vector contains 20 double values - all zero
```

Unlike a built-in array or an `array<>` object, a `vector<>` container always initializes its elements. In this case, our container starts out with 20 elements that are initialized with zero. If you don't like zero as the default value for your elements, you can specify another value explicitly:

```cpp
std::vector<long> numbers(20, 99L);    // Vector contains 20 long values - all 99
```

The second argument between the parentheses specifies the initial value for all elements, so all 20 elements will be `99L`. Unlike most other array types you've seen so far, the first argument that specifies the number of elements—20 in our example—does not need to be a constant expression. It could be the result of an expression executed at runtime or read in from the keyboard. Of course, you can add new elements to the end of this or any other vector using the `push_back()` function.

A further option for creating a `vector<>` is to use a braced list to specify initial values:

```cpp
std::vector<int> primes { 2, 3, 5, 7, 11, 13, 17, 19 };
```

The `primes` vector container will be created with eight elements with the given initial values. If you initialize a `vector<>` with at least one given value, a C++17 compiler can again deduce the template type argument, which may seem somewhat surprising. Here are two examples where this works:

```cpp
std::vector primes { 2, 3, 5, 7, 11, 13, 17, 19 };  // Deduced type: std::vector<int>
std::vector numbers(20, 99L);                         // Deduced type: std::vector<long>
```

**Caution**  You may have noticed that we didn't initialize the `values` and `numbers` `vector<>` objects using the usual braced initializer syntax but instead using round parentheses:

```cpp
std::vector<double> values(20);     // Vector contains 20 double values - all zero
std::vector<long> numbers(20, 99L);  // Vector contains 20 long values - all 99
```

This is because using braced initializers here has a significantly different effect, as the comments next to the statement explain:

```cpp
std::vector<double> values{20};     // Vector contains 1 double value: 20
std::vector<long> numbers{20, 99L};  // Vector contains 2 long values: 20 and 99
```

When you use curly braces to initialize a `vector<>`, the compiler always interprets it as a sequence of initial values. This is one of the few occasions where the so-called uniform initialization syntax is not quite so uniform. To initialize a `vector<>` with a given number of identical values—without repeating that same value over and over, that is—you cannot use curly braces. If you do, it is interpreted by the compiler as a list of one or two initial values.

You can use an index between square brackets to set a value for an existing element or just to use its current value in an expression. Here’s an example:

```cpp
values[0] = std::numbers::pi;       // Pi
values[1] = 5.0;                     // Radius of a circle
values[2] = 2.0*values[0]*values[1];  // Circumference of a circle
```

Index values for a `vector<>` start from 0, just like a standard array. You can always reference existing elements using an index between square brackets, but you cannot create new elements this way. For that, you need to use, for instance, the `push_back()` function. The index values are not checked when you index a vector like this, so you can accidentally access memory outside the extent of the vector and store values in such locations using an index between square brackets. The `vector<>` object again provides the `at()` function as well, just like an `array<>` container object, so you could consider using the `at()` function to refer to elements whenever there is the potential for the index to be outside the legal range.
