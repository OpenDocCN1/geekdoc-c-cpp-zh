In scientific notation, the number before the multiplication operator, called the mantissa, is expressed as having a single digit to the left of the decimal point, and as many digits as necessary to the right side of the decimal point to express the number. The number after the multiplication operator is a power of 10, which may be positive for large numbers or negative for very small fractions. The value of the expression is the mantissa multiplied by the power of 10.

E notation is very similar to scientific notation. The only difference is the multiplication operator, followed by 10 and an exponent, is replaced by an E followed by the exponent.

# Storage of Floating-Point Numbers

Since only ones and zeros can be stored in memory, complex numbers, well beyond the scope of this book, are required to store floating-point numbers. Even with complex codes, a computer can only approximately represent floating-point values. Indeed, in certain programs the programmer has to take care to ensure that such discrepancies in each of a approximations do not accumulate to the point where the final result is wrong.

+   Note Because mathematics with floating-point numbers requires a great deal of computing power, many CPUs use a chip specialized for performing floating-point arithmetic. These chips are often referred to as math coprocessors.

# Text Data Types

There are two data types. The first is char, which stands for character. It is usually 1 byte, and can represent any single character, including a letter, a digit, a punctuation mark, or a space.

The second data type is string. The string data type may store a number of characters, including this sentence, or paragraph, or page. The number of bytes required depends on the number of characters involved.

+   Note Unlike char and the other data types we have discussed, the string type is not a data type built into C++. Instead, it is defined in the standard library file string, which must be included with an include directive (#include <string>) to use the string type. Chapter 1 covers the include directive, which in the "Hello World! program was include <iostream>.

# Storage of Character Values

There is a reason the size of character data type is usually 1.

ANSI (American National Standards Institute) and ASCII (American Standards Committee for Information Interchange) adopted for the English language a set of 256 characters, which includes alphabetical characters (upper- lowercase), digits and punctuation marks, and even characters used in graphics and line drawing. Each of 256 characters is represented by a number between 0 and 255 and that corresponds to Table 2-5 lists the ASCII values of commonly used characters.

Table 2-5: ASCII Values of Commonly Used Characters

| Characters | Values | Comments |
|---|---|---|