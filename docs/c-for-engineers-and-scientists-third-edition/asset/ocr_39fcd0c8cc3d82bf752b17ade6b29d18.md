# 514 Completing the Basics

Table 9.4 The string Class Processing Functions (Require the Header File
(continued)

| Function/Operation | Description | Example |
|---|---|---||\| += | Concatenation and assignment | string2 += string1 |
| != | Relational operators string1 != string2 |
| < | Return true if the relation is satisfied; return return string1 < string2 |
| >= | | string1 > string2 |

The most used function in Table 9.4 length(). It returns the number of characters in the string, which is referred as the string's length. For example, the value returned by the function called "Hello World!"length() is 12. As always, the quotation marks surrounding a string aren't part of the string. Similarly, if the string referred by string1 contains the value "Have a good day.", the value returned by the call string.length() is.

Two strings can be compared for equality using the standard relational operators. Each character in a string is stored in binary with the ASCII or Unicode code. In both, although codes are different, they have some characteristics in common. In both, a blank (less than) all letters and numbers; letters of the alphabet are stored from A to Z, and digits are stored in order 0 to 9. In addition, digits come before (less than) uppercase characters, following lowercase characters. Therefore, uppercase characters are mathematically less than lowercase characters.

When two strings are compared, their characters are compared pair at a time (both first characters, and so on). If no differences are found, the strings are equal; if a difference is found, the string with the first lower character is considered the smaller string, as shown in these:

+   * "Hello" is greater than "Good Bye" because the first H in Hello is greater than the first G in Good Bye.
* "Hello" is less than "hello" because the first H in Hello is less than the first h in hello.
* "SMITH" is greater than "JONES" because the first S in SMITH is greater than the first J in JONES.
* "123" is greater than "1227" because the third character in 123, 3, is greater than the third character in 1227, the 2.
* "Behop" is greater than "Beehive" because the third character in Behop, the h, is greater than the third character in Beehive, the e.

Program 9.9 uses length() and several relational expressions in the context of a complete program.