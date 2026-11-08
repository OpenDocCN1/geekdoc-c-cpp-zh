Before we move on, though, there are two more numeric_limits<> functions we still want to introduce. We promised you earlier that we would. To obtain the special floating-point values for infinity and not-a-number (NaN), you should use expressions of the following form:

```
```cpp
float positive_infinity = std::numeric_limits<float>::infinity();
double negative_infinity = -std::numeric_limits<double>::infinity();
long double not_a_number = std::numeric_limits<long double>::quiet_NaN();
```
```

None of these expressions would compile for integer types, nor would they compile in the unlikely event that the floating-point types that your compiler uses do not support these special values. Besides quiet_NaN(), there's a function called signaling_NaN()—so not loud_NaN() or noisy_NaN(). The difference between the two is outside the scope of this brief introduction. If you're interested, you can always consult your Standard Library documentation.

# ## Working with Character Variables

Variables of type char are used primarily to store a code for a single character and occupy one byte. The C++ standard doesn't specify the character encoding to be used for the basic character set, so in principle this is down to the particular compiler, but it's usually ASCII.
You define variables of type char in the same way as variables of the other types that you've seen. Here's an example:

```
```cpp
char letter;            // Uninitialized - so junk value
char yes {'Y'}, no {'N'}; // Initialized with character literals
char ch {33};           // Integer initializer equivalent to '!'
```
```

You can initialize a variable of type char with a character literal between single quotes or by an integer. An integer initializer must be within the range of type char—remember, it depends on the compiler whether it is a signed or unsigned type. Of course, you can specify a character as one of the escape sequences you saw in Chapter 1.

There are also escape sequences that specify a character by its code expressed as either an octal or a hexadecimal value. The escape sequence for an octal character code is one to three octal digits preceded by a backslash. The escape sequence for a hexadecimal character code is one or more hexadecimal digits preceded by \x. You write either form between single quotes when you want to define a character literal. For example, the letter 'A' could be written as hexadecimal '\x41' in ASCII. Obviously, you could write codes that won't fit within a single byte, in which case the result is implementation defined.

Variables of type char are numeric; after all, they store integer codes that represent characters. They can therefore participate in arithmetic expressions, just like variables of type int or long. Here's an example:

```
```cpp
char ch {'A'};
char letter {ch + 2};     // letter is 'C'
++ch;                     // ch is now 'B'
ch += 3;                  // ch is now 'E'
```
```

When you write a char variable using cout or format(), it is by default output as a character, not as an integer. If you want to see it as a numerical value with cout, you have no choice but to cast it to another integer type first. With format(), you can instead format the character using binary (b), decimal (d), or hexadecimal (x) formatting. Here's an example:

```
```cpp
std::cout << std::format("ch is '{0}' which is code {0:#x}\n", ch);
```
```