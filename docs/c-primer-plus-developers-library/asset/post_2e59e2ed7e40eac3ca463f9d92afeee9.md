
## How C++ Decides What Type a Constant Is

A program's declarations tell the C++ compiler the type of a particular integer variable. But what about constants? That is, suppose you represent a number with a constant in a program:

```cpp
cout << "Year = " << 1492 << "\n";
```

Does the program store 1492 as an `int`, a `long`, or some other integer type? The answer is that C++ stores integer constants as type `int` unless there is a reason to do otherwise. Two such reasons are if you use a special suffix to indicate a particular type or if a value is too large to be an `int`.

First, look at the suffixes. These are letters placed at the end of a numeric constant to indicate the type. An `l` or `L` suffix on an integer means the type is a `long` constant, a `u` or `U` suffix indicates an `unsigned int` constant, and `ul` (in any combination of orders and uppercase and lowercase) indicates a type `unsigned long` constant. (Because a lowercase `l` can look much like the digit 1, you should use the uppercase `L` for suffixes.) For example, on a system using a 16-bit `int` and a 32-bit `long`, the number 22022 is stored in 16 bits as an `int`, and the number `22022L` is stored in 32 bits as a `long`. Similarly, `22022LU` and `22022UL` are `unsigned long`. C++11 provides the `ll` and `LL` suffixes for type `long long`, and `ull`, `uLL`, `Ull`, and `ULL` for `unsigned long long`.

Next, look at size. C++ has slightly different rules for decimal integers than it has for hexadecimal and octal integers. (Here decimal means base 10, just as hexadecimal means base 16; the term decimal does not necessarily imply a decimal point.) A decimal integer without a suffix is represented by the smallest of the following types that can hold it: `int`, `long`, or `long long`. On a computer system using a 16-bit `int` and a 32-bit `long`, 20000 is represented as type `int`, 40000 is represented as `long`, and 3000000000 is represented as `long long`. A hexadecimal or octal integer without a suffix is represented by the smallest of the following types that can hold it: `int`, `unsigned int`, `long`, `unsigned long`, `long long`, or `unsigned long long`. The same computer system that represents 40000 as `long` represents the hexadecimal equivalent `0x9C40` as an `unsigned int`. That's because hexadecimal is frequently used to express memory addresses, which intrinsically are unsigned. So `unsigned int` is more appropriate than `long` for a 16-bit address.

## The char Type: Characters and Small Integers

It's time to turn to the final integer type: `char`. As you probably suspect from its name, the `char` type is designed to store characters, such as letters and numeric digits. Now, whereas storing numbers is no big deal for computers, storing letters is another matter. Programming languages take the easy way out by using number codes for letters. Thus, the `char` type is another integer type. It's guaranteed to be large enough to represent the entire range of basic symbols—all the letters, digits, punctuation, and the like—for the target computer system. In practice, many systems support fewer than 128 kinds of characters, so a single byte can represent the whole range. Therefore, although `char` is most often used to handle characters, you can also use it as an integer type that is typically smaller than `short`.

The most common symbol set in the United States is the ASCII character set, described in Appendix C, “The ASCII Character Set.” A numeric code (the ASCII code) represents each character in the set. For example, 65 is the code for the character A, and 77 is the code for the character M. For convenience, this book assumes ASCII code in its examples. However, a C++ implementation uses whatever code is native to its host system—for example, EBCDIC (pronounced “eb-see-dik”) on an IBM mainframe. Neither ASCII nor EBCDIC serve international needs that well, and C++ supports a wide-character type that can hold a larger range of values, such as are used by the international Unicode character set. You’ll learn about this `wchar_t` type later in this chapter.

Try the `char` type in Listing 3.5.

### Listing 3.5 `chartype.cpp`

```cpp
// chartype.cpp -- the char type
#include <iostream>
int main( )
{
    using namespace std;
    char ch;             // declare a char variable

    cout << "Enter a character: " << endl;
    cin >> ch;
    cout << "Hola! ";
    cout << "Thank you for the " << ch << " character." << endl;
    return 0;
}
```

Here’s the output from the program in Listing 3.5:

```text
Enter a character:
M
Hola! Thank you for the M character.
```

The interesting thing is that you type an M, not the corresponding character code, 77. Also the program prints an M, not 77. Yet if you peer into memory, you find that 77 is the value stored in the `char` variable. The magic, such as it is, lies not in the `char` type but in `cin` and `cout`. These worthy facilities make conversions on your behalf. On input, `cin` converts the keystroke input M to the value 77. On output, `cout` converts the value 77 to the displayed character M; `cin` and `cout` are guided by the type of variable. If you place the same value 77 into an `int` variable, `cout` displays it as 77. (That is, `cout` displays two 7 characters.) Listing 3.6 illustrates this point. It also shows how to write a character literal in C++: Enclose the character within two single quotation marks, as in `'M'`. (Note that the example doesn’t use double quotation marks. C++ uses single quotation marks for a character and double quotation marks for a string. The `cout` object can handle either, but, as Chapter 4 discusses, the two are quite different from one another.) Finally, the program introduces a `cout` feature, the `cout.put( )` function, which displays a single character.

The fact that C++ represents characters as integers is a genuine convenience that makes it easy to manipulate character values. You don’t have to use awkward conversion functions to convert characters to ASCII and back.

Even digits entered via the keyboard are read as characters. Consider the following sequence:

```cpp
char ch;
cin >> ch;
```

If you type 5 and Enter, this code reads the 5 character and stores the character code for the 5 character (53 in ASCII) in `ch`. Now consider this code:

```cpp
int n;
cin >> n;
```

The same input results in the program reading the 5 character and running a routine converting the character to the corresponding numeric value of 5, which gets stored in `n`.

Finally, the program uses the `cout.put()` function to display both a `ch` and a character constant.

## A Member Function: `cout.put()`

Just what is `cout.put()`, and why does it have a period in its name? The `cout.put()` function is your first example of an important C++ OOP concept, the *member function*. Remember that a class defines how to represent data and how to manipulate it. A member function belongs to a class and describes a method for manipulating class data. The `ostream` class, for example, has a `put()` member function that is designed to output characters. You can use a member function only with a particular object of that class, such as the `cout` object, in this case. To use a class member function with an object such as `cout`, you use a period to combine the object name (`cout`) with the function name (`put()`). The period is called the *membership operator*. The notation `cout.put()` means to use the class member function `put()` with the class object `cout`. You’ll learn about this in greater detail when you reach classes in Chapter 10, “Objects and Classes.” Now the only classes you have are the `iostream` and `ostream` classes, and you can experiment with their member functions to get more comfortable with the concept.

The `cout.put()` member function provides an alternative to using the `<<` operator to display a character. At this point you might wonder why there is any need for `cout.put()`. Much of the answer is historical. Before Release 2.0 of C++, `cout` would display character *variables* as characters but display character *constants*, such as `'M'` and `'N'`, as numbers. The problem was that earlier versions of C++, like C, stored character constants as type `int`. That is, the code 77 for `'M'` would be stored in a 16-bit or 32-bit unit. Meanwhile, `char` variables typically occupied 8 bits. A statement like the following copied 8 bits (the important 8 bits) from the constant `'M'` to the variable `ch`:

```cpp
char ch = 'M';
```
