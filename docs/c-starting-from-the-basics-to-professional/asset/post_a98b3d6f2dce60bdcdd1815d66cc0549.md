
## Finding the Limits

You have seen typical examples of the upper and lower limits for various types. The `<limits>` Standard Library module makes this information available for all the fundamental data types so you can access this for your compiler. Let’s look at an example. To display the maximum value you can store in a variable of type `double`, you could write this:

```cpp
std::cout << "Maximum value of type double is " << std::numeric_limits<double>::max();
```

The expression `std::numeric_limits<double>::max()` produces the value you want. By putting different type names between the angled brackets, you can obtain the maximum values for other data types. You can also replace `max()` with `min()` to get the minimum value that can be stored, but the meaning of minimum is different for integer and floating-point types. For an integer type, `min()` results in the true minimum, which will be a negative number for a signed integer type. For a floating-point type, `min()` returns the minimum positive value that can be stored.

> **Caution** `std::numeric_limits<double>::min()` typically equals 2.225e-308, an extremely tiny *positive* number. So, for floating-point types, `min()` does not give you the complement of `max()`. To get the lowest negative value a type can represent, you should use `lowest()` instead. For instance, `std::numeric_limits<double>::lowest()` equals -1.798e+308, a hugely negative number. For integer types, `min()` and `lowest()` always evaluate to the same number.

The following program will display the maximums and minimums for some of the numerical data types:

```cpp
// Ex2_07.cpp
// Finding maximum and minimum values for data types
import <iostream>;
import <limits>;
import <format>;

int main()
{
  std::cout
    << std::format("The range for type short is from {} to {}\n",
                   std::numeric_limits<short>::min(), std::numeric_limits<short>::max())
    << std::format("The range for type unsigned int is from {} to {}\n",
                   std::numeric_limits<unsigned int>::min(),
                   std::numeric_limits<unsigned int>::max())
    << std::format("The range for type long is from {} to {}\n",
                   std::numeric_limits<long>::min(), std::numeric_limits<long>::max())
    << std::format("The positive range for type float is from {} to {}\n",
                   std::numeric_limits<float>::min(), std::numeric_limits<float>::max())
    << std::format("The full range for type float is from {} to {}\n",
                   std::numeric_limits<float>::lowest(), std::numeric_limits<float>::max())
    << std::format("The positive range for type double is from {} to {}\n",
                   std::numeric_limits<double>::min(),
                   std::numeric_limits<double>::max())
    << std::format("The positive range for type long double is from {} to {}\n",
                   std::numeric_limits<long double>::min(),
                   std::numeric_limits<long double>::max());
}
```

You can easily extend this to include additional numeric types. On our test system, the results of running the program are as follows:

```text
The range for type short is from -32768 to 32767
The range for type unsigned int is from 0 to 4294967295
The range for type long is from -9223372036854775808 to 9223372036854775807
The positive range for type float is from 1.17549e-38 to 3.40282e+38
The full range for type float is from -3.40282e+38 to 3.40282e+38
The positive range for type double is from 2.22507e-308 to 1.79769e+308
The positive range for type long double is from 3.3621e-4932 to 1.18973e+4932
```

**Note** In Ex2_07, we used `std::format()` even though we didn’t really need any of its powerful text formatting facilities (such as field width, precision, alignment, etc.). We did so to illustrate how `std::format()`, even then, offers advantages. Just count the `"` delimiters and `<<` operators you have to type when streaming the same output directly to `std::cout`:

```cpp
<< "The range for type short is from " << std::numeric_limits<short>::min()
<< " to " << std::numeric_limits<short>::max() << '\n';
```

More importantly, interleaving text and invocations of `<<` like this also makes your code harder to read. That is: constructing the output text becomes harder, as you have to scan the entire statement for snippets of text. With the `std::format()` version, on the other hand, you can instantly see that the output will be of the form “The range for type short is from ... to ...\n”.

## Finding Other Properties of Fundamental Types

You can retrieve many other items of information about various types. The number of binary digits, or bits, for example, is returned by this expression:

```cpp
std::numeric_limits<type_name>::digits
```

`type_name` is the type in which you’re interested. For floating-point types, you’ll get the number of bits in the mantissa. For signed integer types, you’ll get the number of bits in the value, that is, excluding the sign bit. You can also find out what the range of the exponent component of floating-point values is, whether a type is signed or not, and so on. You can consult a Standard Library reference for the complete list.

Before we move on, though, there are two more numeric_limits<> functions we still want to introduce. We promised you earlier that we would. To obtain the special floating-point values for infinity and not-a-number (NaN), you should use expressions of the following form:

```cpp
float positive_infinity = std::numeric_limits<float>::infinity();
double negative_infinity = -std::numeric_limits<double>::infinity();
long double not_a_number = std::numeric_limits<long double>::quiet_NaN();
```

None of these expressions would compile for integer types, nor would they compile in the unlikely event that the floating-point types that your compiler uses do not support these special values. Besides quiet_NaN(), there's a function called signaling_NaN()—so not loud_NaN() or noisy_NaN(). The difference between the two is outside the scope of this brief introduction. If you're interested, you can always consult your Standard Library documentation.

## Working with Character Variables

Variables of type char are used primarily to store a code for a single character and occupy one byte. The C++ standard doesn't specify the character encoding to be used for the basic character set, so in principle this is down to the particular compiler, but it's usually ASCII.

You define variables of type char in the same way as variables of the other types that you've seen. Here's an example:

```cpp
char letter;            // Uninitialized - so junk value
char yes {'Y'}, no {'N'}; // Initialized with character literals
char ch {33};           // Integer initializer equivalent to '!'
```

You can initialize a variable of type char with a character literal between single quotes or by an integer. An integer initializer must be within the range of type char—remember, it depends on the compiler whether it is a signed or unsigned type. Of course, you can specify a character as one of the escape sequences you saw in Chapter 1.

There are also escape sequences that specify a character by its code expressed as either an octal or a hexadecimal value. The escape sequence for an octal character code is one to three octal digits preceded by a backslash. The escape sequence for a hexadecimal character code is one or more hexadecimal digits preceded by \x. You write either form between single quotes when you want to define a character literal. For example, the letter 'A' could be written as hexadecimal '\x41' in ASCII. Obviously, you could write codes that won't fit within a single byte, in which case the result is implementation defined.

Variables of type char are numeric; after all, they store integer codes that represent characters. They can therefore participate in arithmetic expressions, just like variables of type int or long. Here's an example:

```cpp
char ch {'A'};
char letter {ch + 2};     // letter is 'C'
++ch;                     // ch is now 'B'
ch += 3;                  // ch is now 'E'
```

When you write a char variable using cout or format(), it is by default output as a character, not as an integer. If you want to see it as a numerical value with cout, you have no choice but to cast it to another integer type first. With format(), you can instead format the character using binary (b), decimal (d), or hexadecimal (x) formatting. Here's an example:

```cpp
std::cout << std::format("ch is '{0}' which is code {0:#x}\n", ch);
```
