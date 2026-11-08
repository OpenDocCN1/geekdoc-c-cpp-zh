But of course you can override the default formatting. You do so by adding a *format specifier* between the curly braces of a replacement field. We discuss this in the next subsection. After that, we'll explain you how to override the default left-to-right order, and how to output the same value more than once.

# Format Specifiers

A format specifier is a seemingly cryptic sequence of numbers and characters, introduced by a colon, telling `std::format()` how you would like the corresponding data to be formatted. To tune floating-point precision, for instance, you add, after the mandatory colon, a dot followed by an integer number:

```
```cpp
std::cout << std::format("Pond diameter required for {} fish is {:.2} feet.\n",
                         fish_count, pond_diameter);
```
```

By default, this integer specifies the *total number of significant digits* (2 in our example), counting digits both before and after the decimal point. The result thus becomes (see Ex2_03C.cpp):

```
```text
Pond diameter required for 20 fish is 8.7 feet.
```
```

You can instead make the precision specify the number of digits after the decimal point—the *number of decimal places* in other words—by enabling so-called "fixed-point" formatting of floating-point numbers. You do so by appending the letter `f` to the format specifier. If you replace `{:.2}` with `{:.2f}` in our running example, it produces the following output:

```
```text
Pond diameter required for 20 fish is 8.74 feet.
```
```

> **Note**  You obtain the equivalent with stream manipulators by inserting `<< std::precision(2) << std::fixed` into an output stream. See how much more compact `{:.2f}` is?

Here is the (slightly simplified) general form of the format specifiers for fields of fundamental and string types:

```
```text
[[fill]align][sign][#][0][width][.precision][type]
```
```

The square brackets are for illustration purposes only and mark optional *formatting options*. Not all options are applicable to all field types. `precision`, for instance, is only applicable to floating-point numbers (as you already know) and strings (where it defines how many characters will be used from the string).

> **Caution**  If you specify an unsupported formatting option, or if you make any syntactical mistake in one of the format specifiers, `std::format()` will fail. To report this failure, `std::format()` raises what is known as an *exception*. If such an exception occurs, and there is no error handling code in place, your entire program instantly terminates with an error. You can give this a try by replacing the format string in `Ex2_03C.cpp` with the following (we added a precision to the first format specifier):

```
```cpp
std::cout << std::format("Pond diameter required for {:.2} fish is {:.2} feet.\n",
                         fish_count, pond_diameter);
```
```