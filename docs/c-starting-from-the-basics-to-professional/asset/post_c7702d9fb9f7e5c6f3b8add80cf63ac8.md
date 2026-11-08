
Here's some typical output:

```
Enter a letter: H
You entered an uppercase letter.
```

After creating the `char` variable `letter` with an initial value of zero, the program prompts you to enter a letter. The `if` statement that follows checks whether the character entered is `'A'` or larger. If `letter` is greater than or equal to `'A'`, the nested `if` that checks for the input being `'Z'` or less executes. If it is `'Z'` or less, you conclude that it is an uppercase letter and display a message. You are done at this point, so you execute a `return` statement to end the program.

The next `if`, using essentially the same mechanism as the first, checks whether the character entered is lowercase, displays a message, and returns. You probably noticed that the test for a lowercase character contains only one pair of braces, whereas the uppercase test has two. The code block between the braces belongs to the inner `if` here. In fact, both sets of statements work as they should—remember that `if (condition) {...}` is effectively a single statement and does not need to be enclosed within more braces. However, the extra braces do make the code clearer, so it's a good idea to use them.

The output statement following the last `if` block executes only when the character entered is not a letter, and it displays a message to that effect. You can see that the relationship between the nested `if`s and the output statement is much easier to follow because of the indentation. Indentation is generally used to provide visual cues to the logic of a program.

This program illustrates how a nested `if` works, but it is not a good way to test for characters. Using the Standard Library, you can write the program so that it works independently of the character coding. We'll explore how that works in the next subsection.

## Character Classification and Conversion

The nested `if`s of Ex4_04 rely on these three built-in assumptions about the codes that are used to represent alphabetic characters:

- The letters A to Z are represented by a set of codes where the code for `'A'` is the minimum and the code for `'Z'` is the maximum.
- The codes for the uppercase letters are contiguous, so no nonalphabetic characters lie between the codes for `'A'` and `'Z'`.
- All uppercase letters in the alphabet fall within the range A to Z.

While the first two assumptions will hold for any character encoding used in practice today, the third is definitely not true for many languages. The Greek alphabet, for instance, knows uppercase letters such as Α, Θ, and Π; the Russian one contains Ж, Ф, and Ш; and even Latin-based languages such as French often use capital letters such as É and Ç whose encodings won't lie at all between `'A'` and `'Z'`. It is therefore not a good idea to build these kinds of assumptions into your code because it limits the portability of your program. Never assume that your program will be used only by fellow Anglophones!

To avoid making such assumptions in your code, the C and C++ Standard Libraries offer the concept of locales. A locale is a set of parameters that defines the user's language and regional preferences, including the national or cultural character set and the formatting rules for currency and dates. A complete coverage of this topic is beyond the scope of this book, though. We only cover the character classification functions provided by the `<cctype>` header, listed in Table 4-3.

### Table 4-3. Functions for Classifying Characters Provided by the `<cctype>` Header

| Function | Operation |
|---|---|
| `isupper(c)` | Tests whether `c` is an uppercase letter, by default `'A'` to `'Z'`. |
| `islower(c)` | Tests whether `c` is a lowercase letter, by default `'a'` to `'z'`. |
| `isalpha(c)` | Tests whether `c` is an uppercase or lowercase letter (or any alphabetic character that is neither uppercase nor lowercase, should the locale's alphabet contain such characters). |
| `isdigit(c)` | Tests whether `c` is a digit, `'0'` to `'9'`. |
| `isxdigit(c)` | Tests whether `c` is a hexadecimal digit, either `'0'` to `'9'`, `'a'` to `'f'`, or `'A'` to `'F'`. |
| `isalnum(c)` | Tests whether `c` is an alphanumeric character; same as `isalpha(c) \|\| isdigit(c)`. |
| `isspace(c)` | Tests whether `c` is whitespace, by default a space (`' '`), newline (`'\n'`), carriage return (`'\r'`), form feed (`'\f'`), or horizontal (`'\t'`) or vertical (`'\v'`) tab. |
| `isblank(c)` | Tests whether `c` is a space character used to separate words within a line of text. By default either a space (`' '`) or a horizontal tab (`'\t'`). |
| `ispunct(c)` | Tests whether `c` is a punctuation character. By default, this will be either a space or one of the following: `_ { } [ ] # ( ) < > % : ; . ? * + - / ^ & \| ~ ! = , \ " '`. |
| `isprint(c)` | Tests whether `c` is a printable character, which includes uppercase or lowercase letters, digits, punctuation characters, and spaces. |
| `iscntrl(c)` | Tests whether `c` is a control character, which is the opposite of a printable character. |
| `isgraph(c)` | Tests whether `c` has a graphical representation, which is true for any printable character other than a space. |

Table 4-3 lists the functions that the `<cctype>` header provides to classify characters. In each case, you pass the function a variable or literal that is the character to be tested.

Each of these functions returns a value of type `int`. The value will be nonzero (true) if the character is of the type being tested for, and 0 (false) if it isn't. You may be wondering why these functions don't return a `bool` value, which would make much more sense. The reason they don't return a `bool` value is that they originate from the C Standard Library and predate type `bool` in C++.

You could use `<cctype>`'s character classification functions to implement Ex4_04 without any hard-coded assumptions about either the character set or its encoding. The character codes in different environments are always taken care of by the Standard Library functions. An additional advantage is that these functions also make the code simpler and easier to read. You'll find the adjusted program under the name Ex4_04A.cpp.

```cpp
if (std::isupper(letter))
{
    std::cout << "You entered an uppercase letter." << std::endl;
    return 0;
}

if (std::islower(letter))
{
    std::cout << "You entered a lowercase letter." << std::endl;
    return 0;
}
```

As `<cctype>` is part of the C++ Standard Library, it defines all its functions inside the `std` namespace. You therefore normally should prefix their names with `std::`. However, because `<cctype>` is by origin a header from the C Standard Library—as indicated by the `c` prefix in its name—there is no guarantee you can use it as a C++ module. You encountered this before with the `<cmath>` C header in Chapter 2. To make `<cctype>`'s functions available to you, you should therefore use `#include <cctype>` rather than `import <cctype>`; (mind the lack of a semicolon after the `#include` directive).

To conclude, the `<cctype>` C header also provides the two functions shown in Table 4-4 for converting between uppercase and lowercase characters. The result will be returned as type `int`, so you need to explicitly cast it if you want to store it as type `char`, for instance.

### Table 4-4. Functions for Converting Characters Provided by the `<cctype>` Header

| Function | Operation |
|---|---|
| `tolower(c)` | If `c` is uppercase, the lowercase equivalent is returned; otherwise, `c` is returned. |
| `toupper(c)` | If `c` is lowercase, the uppercase equivalent is returned; otherwise, `c` is returned. |

> **Note** All standard character classification and conversion functions except for `isdigit()` and `isxdigit()` operate according to the rules of the current locale. All examples given in Table 4-3 are for the default, so-called "C" locale, which is a set of preferences similar to those used by English-speaking Americans. The C++ Standard Library offers an extensive library for working with other locales and character sets. You can use these to develop applications that work correctly irrespective of the user's language and regional conventions. This topic is a bit too advanced for this book, though. Consult a Standard Library reference for more details.

## The if-else Statement

The `if` statement that you have been using executes a statement or block of statements if the condition specified is true. Program execution then continues with the next statement in sequence. Of course, you may want to execute one block of statements when the condition is true and another set when the condition is false. An extension of the `if` statement called an `if-else` statement allows this.

The `if-else` combination provides a choice between two options. Figure 4-2 shows its general logic.
