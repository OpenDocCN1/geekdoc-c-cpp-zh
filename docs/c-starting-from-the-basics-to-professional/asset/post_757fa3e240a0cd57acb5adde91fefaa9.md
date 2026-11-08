
## UCS and Unicode

UCS defines a mapping between characters and integer code values, called *code points*. It is important to realize that a *code point* is not the same as an *encoding*. A code point is an integer; an encoding specifies a way of representing a given code point as a series of bytes or words. Code values of less than 256 are popular and can be represented in one byte. It would be inefficient to use four bytes to store code values that require just one byte just because there are other codes that require several bytes. Encodings are ways of representing code points that allow them to be stored more efficiently.

Unicode is a standard that defines a set of characters and their code points identical to those in UCS. Unicode also defines several different encodings for these code points and includes additional mechanisms for dealing with such things as right-to-left languages such as Arabic. The range of code points is more than enough to accommodate the character sets for all the languages in the world, as well as many different sets of graphical characters such as mathematical symbols, or even emoticons and emojis. Regardless, the codes are arranged such that strings in the majority of languages can be represented as a sequence of single 16-bit codes.

One aspect of Unicode that can be confusing is that it provides more than one *character encoding method*. The most commonly used encodings are referred to as UTF-8, UTF-16, and UTF-32, any of which can represent all the characters in the Unicode set. The difference between them is in how a given character code point is represented; the numerical code value for any given character is the same in any of the representations. Here’s how these encodings represent characters:

- *UTF-8* represents a character as a variable-length sequence of between one and four bytes. The ASCII character set appears in UTF-8 as single-byte codes that have the same code values as ASCII. UTF-8 is by far the most popular encoding of Unicode. Most web pages, for example, use UTF-8 to encode text (95.2% according to a recent study).
- *UTF-16* represents characters as one or two 16-bit values. Until recently, Microsoft advocated the use of its native UTF-16-based APIs for Windows. Today the recommended encoding across most platforms, however, is UTF-8.
- *UTF-32*, you guessed it, simply represents all characters as 32-bit values. In practice, UTF-32 is rarely used by applications internally.

In C++20, you have four types designed to store Unicode characters: wchar_t, char8_t, char16_t, and char32_t—yet because char8_t was only introduced in C++20, many legacy applications and APIs will still use char to represent UTF-8-encoded strings as well. You’ll learn more about the different character types in Chapter 2.

## C++ Source Characters

You write C++ statements using a *basic source character set*. This is the set of characters that you’re allowed to use explicitly in a C++ source file. The character set that you can use to define a name is a subset of this. Of course, the basic source character set in no way constrains the character data that you work with in your code. Your program can create strings consisting of characters outside this set in various ways, as you’ll see. The basic source character set consists of the following characters:

- The letters a to z and A to Z
- The digits 0 to 9
- The whitespace characters space, horizontal tab, vertical tab, form feed, and newline
- The characters `{ } [ ] # ( ) < % : ; . ? * + - / ^ & | ~ ! = , \\ " '`

This is easy and straightforward. You have 96 characters that you can use, and it's likely that these will accommodate your needs most of the time. Most of the time the basic source character set will be adequate, but occasionally you'll need characters that aren't in it. You can, at least in theory, include Unicode characters in a C++ name as well. Which Unicode encoding to use, and which subset of Unicode is supported, depends on your compiler. Both character and string data can similarly include Unicode characters as well. If you want to include a Unicode character in a character or string literal (literals are discussed in Chapter 2), though, in a form that is accepted by any compiler, you should use the hexadecimal representation of its code point. That is: you should then enter it either as \udddd or as \Udddddddd, where d is a hexadecimal digit. Note the lowercase u in the first case and the uppercase U in the second; either is acceptable.

## Escape Sequences

When you want to use character constants such as a single character or a character string in a program, certain characters are problematic. Obviously, you can't enter characters such as newline directly as character constants, as they'll just do what they're supposed to do: go to a new line in your source code file (the only exception to this rule is raw string literals, which are covered in Chapter 7). You can enter these problem characters in character constants by means of an escape sequence. An escape sequence is an indirect way of specifying a character, and it always begins with a backslash. Table 1-3 shows the most commonly used escape sequences.

Table 1-3. The Most Commonly Used Escape Sequences

| Escape Sequence | Character |
| --- | --- |
| `\n` | Newline |
| `\r` | Carriage return (part of the `\r\n` newline sequence for Windows) |
| `\t` | Horizontal tab |
| `\\` | Backslash (`\`) |
| `\"` | Double quote (`"`) in string literals |
| `\'` | Single quote (`'`) in character literals |

The first three escape sequences in Table 1-3 represent various line break or whitespace characters. The last three characters, however, are more regular characters, yet at times problematic to represent directly in code. Clearly, the backslash character itself is difficult because it signals the start of an escape sequence, and the single and double quote characters because they are used as delimiters for literals, as in the constant 'A' or the string "text". This program that uses escape sequences outputs a message to the screen. To see it, you'll need to enter, compile, link, and execute the code:

```cpp
// Ex1_02.cpp
// Using escape sequences
import <iostream>;

int main()
{
    std::cout << "\"Least \'said\' \\\n\t\tsoonest \'mended\'.\"" << std::endl;
}
```

When you manage to compile, link, and run this program, you should see the following output displayed:

```text
"Least 'said' \
        soonest 'mended.'"
```

The output is determined by what's between the outermost double quotes in the following statement:

```cpp
std::cout << "\"Least \'said\' \\\n\t\tsoonest \'mended.\'\"" << std::endl;
```

In principle, *everything* between the outer double quotes in the preceding statement gets sent to cout. A string of characters between a pair of double quotes is called a *string literal*. The double quote characters are *delimiters* that identify the beginning and end of the string literal; they aren't part of the string. Each escape sequence in the string literal will be converted to the character it represents by the compiler, so the character will be sent to cout, not the escape sequence itself. A backslash in a string literal always indicates the start of an escape sequence, so the first character that's sent to cout is a double quote character.

Least followed by a space is output next. This is followed by a single quote character, then said, followed by another single quote. Next is a space, followed by the backslash specified by `\\`. Then a newline character corresponding to `\n` is written to the stream so the cursor moves to the beginning of the next line. You then send two tab characters to cout with `\t\t`, so the cursor will be moved two tab positions to the right. The word soonest is output next followed by a space and then mended between single quotes. Finally, a period is output followed by a double quote.

> **Note** If you're no fan of escape sequences, Chapter 7 introduces an interesting alternative to them called *raw string literals*.

The truth is, in our enthusiasm for showcasing character escaping, we may have gone a bit overboard in Ex1_02.cpp. You actually do not have to escape the single quote character, `'`, inside string literals; there's already no possibility for confusion. So, the following statement will have the same output:

```cpp
std::cout << "\"Least 'said' \\\n\t\tsoonest 'mended.'\"" << std::endl;
```

It's only when within a character literal of the form `'\''` that a single quote really needs escaping. Conversely, double quotes, of course, won't need a backslash then; your compiler will happily accept both `'\''` and `'"'`. But we're getting ahead of ourselves: character literals are more a topic of the next chapter.

> **Note** The `\t` escape sequences in Ex1_02 are, strictly speaking, not required either—you could in principle type tabs in a string literal as well (as in `"\"Least 'said' \\n    soonest 'mended.'\""`). Using `\t` is nevertheless recommended; the problem with tabs is that one generally cannot tell the difference between a tab, `"    "`, and a number of spaces, `"  "`, let alone properly count the number of tabs. Also, some text editors tend to convert tabs into spaces upon saving. It's therefore not uncommon for style guides to require the use of the `\t` escape sequence in string literals.
