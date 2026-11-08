
The final parameter for `list_words()` is reference-to-const because it too is an input parameter. The function only accesses the argument; it doesn't change it.

> **Tip** Input parameters should usually be references-to-const. Only smaller values, most notably those of fundamental types, should be passed by value. Use references-to-non-const only for output parameters, and even then you should often consider returning a value instead. We’ll study how to return values from functions soon.

## Passing Arrays by Reference

At first sight, it might seem that for arrays there would be little benefit from passing them by reference. After all, if you pass an array by value, the array elements themselves are not copied. Instead, a copy is made of the pointer to the first element of the array. Passing an array also already allows you to modify the values of the original array—unless you add `const`, of course. So surely this already covers both advantages typically attributed to passing by reference: no copying and the possibility to modify the original value?

While this is most certainly true, you did already discover the main limitation with passing an array by value earlier, namely, that there is no way to specify the array’s first dimension in a function signature, at least not in such a way that the compiler enforces that only arrays of exactly that size are passed to the function. A lesser-known fact, though, is that you can accomplish this by passing arrays by reference.

To illustrate, we invite you to again replace the `average()` function in `Ex8_05.cpp` with an `average10()` function, but this time with the following variant:

```cpp
double average10(const double (&array)[10])  // Only arrays of length 10 can be passed
{
    double sum {};                            // Accumulate total in here
    for (size_t i {}; i < 10; ++i)
        sum += array[i];                       // Sum array elements
    return sum / 10;                           // Return average
}
```

As you can see, the syntax for passing an array by reference is somewhat more complex. The `const` could in principle be omitted from the parameter type, but it is preferred here because you do not want to modify the values of the array in the function’s body. The extra parentheses surrounding `array` are required, though. Without them, the compiler would no longer interpret the parameter type as a reference to an array of doubles but as an array of references to double. Because arrays of references are not allowed in C++, this would result in a compiler error.

```cpp
double average10(const double& array[10])  // Error: array of double& is not allowed
```

With our new and improved version of `average10()` in place, the compiler does live up to expectations. Attempting to pass an array of a different length now results, as desired, in a compiler error:

```cpp
double values[] { 1.0, 2.0, 3.0 };       // Only three values!!!
std::cout << "Average = " << average10(values) << std::endl;  // Error...
```

Note, moreover, that if you pass a fixed-size array by reference, it can be used as input to operations such as `sizeof()`, `std::size()`, and range-based for loops. This was not possible with arrays that are passed by value. You can use this to eliminate the two occurrences of 10 from the body of `average10()`:

```cpp
double average10(const double (&array)[10])
{
    double sum {};                    // Accumulate total in here
    for (double val : array)
        sum += val;                   // Sum array elements
    return sum / std::size(array);    // Return average
}
```

> **Tip** You have already seen a more modern alternative to working with arrays of fixed length in Chapter 5: `std::array<>`. Using values of this type, you can just as safely pass fixed-size arrays by reference and without having to remember the tricky syntax for passing plain fixed-size arrays by reference.
>
> ```cpp
> double average10(const std::array<double,10>& values)
> ```
>
> In Chapter 9, we explain a possibly even better alternative, namely `std::span<double, 10>`.

We made three variants of this program available to you: `Ex8_09A`, which uses pass-by-reference; `Ex8_09B`, which eliminates the magic numbers; and `Ex8_09C`, to show the use of `std::array<>`.

### References and Implicit Conversions

A program often uses many different types, and as you know, the compiler is usually quite happy to assist you by implicitly converting between them. Whether or not you should always be happy about such conversions is another matter, though. That aside, most of the time it is convenient that code such as the following snippet will compile just fine, even though it assigns an `int` value to a differently typed `double` variable:

```cpp
int i{};        // Declare some differently typed variables
double d{};
d = i;          // Implicit conversion from int to double
```

For function arguments that employ pass-by-value, it is only natural that such conversions occur as well. For instance, given the same two variables `i` and `d`, a function with signature `f(double)` can hence be called not only with `f(d)` or `f(1.23)` but also with differently typed arguments such as `f(1)`, `f(123)`, or `f(1.23f)`.

Implicit conversions thus remain quite straightforward for pass-by-value. Let's take a look at how they fare with reference arguments:

```cpp
// Ex8_10.cpp
// Implicit conversions of reference parameters
import <iostream>;

void double_it(double& it)       { it *= 2; }
void print_it(const double& it) { std::cout << it << std::endl; }

int main()
{
    double d(123);
    double_it(d);
    print_it(d);

    int i(456);
    // double_it(i);          /* error, does not compile! */
    print_it(i);
}
```

We first define two trivial functions: one that doubles doubles and one that streams them to std::cout. The first part of main() then shows that these, of course, work for a double variable—obviously, you should thus see the number 246 appear in the output. The interesting parts of this example are its final two statements, of which the first is commented out because it would not compile.

Let's consider the print_it() statement first and explain why it is in fact already a minor miracle that this even works at all. The function print_it() operates on a reference to a const double, a reference that as you know is supposed to act as an alias for a double that is defined elsewhere. On a typical system, print_it() will ultimately read the eight bytes found in the memory location behind this reference and print out the 64 bits it finds there in some human-readable format to std::cout. But the value that we passed to the function as an argument is no double; it is an int! This int is generally only four bytes big, and its 32 bits are laid out completely differently than those of a double. So, how can this function be reading from an alias for a double if there is no such double defined anywhere in the program? The answer is that the compiler, before it calls print_it(), implicitly creates a temporary double value somewhere in memory, assigns it the converted int value, and then passes a reference to this temporary memory location to print_it().

Such implicit conversions are only supported for reference-to-const parameters, not for reference-to-non-const parameters. Suppose for argument's sake that the double_it() statement on the second-to-last line will compile without error. Surely, the compiler will then similarly convert the int value 456 to a double value 456.0, store this temporary double somewhere in memory, and apply the function body of double_it() to it. Then you'd have a temporary double somewhere, now with value 912.0, and an int value i that is still equal to 456. Now, while in theory the compiler could convert the resulting temporary value back to an int, the designers of the C++ programming language decided that that would be a bridge too far. The reason is that generally such inverse conversions would inevitably mean loss of information. In our case, this would involve a conversion from double to int, which would result in the loss of at least the fractional part of the number. The creation of temporaries is therefore never allowed for reference-to-non-const parameters. This is also why the statement double_it(i) is invalid in standard C++ and should fail to compile.

### Default Argument Values

There are many situations in which it would be useful to have default argument values for one or more function parameters. This would allow you to specify an argument value only when you want something different from the default. A simple example is a function that outputs a standard error message. Most of the time, a default message will suffice, but occasionally an alternative is needed. You can do this by specifying a default parameter value in the function prototype. You could define a function to output a message like this:
