
```cpp
25     cout << "\\nstrncmp(s1, s3, 6) = " << setw( 2 )
26          << strncmp( s1, s3, 6 ) << "\\nstrncmp(s1, s3, 7) = " << setw( 2 )
27          << strncmp( s1, s3, 7 ) << "\\nstrncmp(s3, s1, 7) = " << setw( 2 )
28          << strncmp( s3, s1, 7 ) << endl;
29     return 0; // indicates successful termination
30 } // end main
```

```
s1 = Happy New Year
s2 = Happy New Year
s3 = Happy Holidays

strcmp(s1, s2) =  0
strcmp(s1, s3) =  1
strcmp(s3, s1) = -1

strncmp(s1, s3, 6) =  0
strncmp(s1, s3, 7) =  1
strncmp(s3, s1, 7) = -1
```

**Fig. 8.32** | `strcmp` and `strncmp`. (Part 2 of 2.)

## Common Programming Error 8.21

> Assuming that strcmp and strncmp return one (a true value) when their arguments are equal is a logic error. Both functions return zero (C++'s false value) for equality. Therefore, when testing two strings for equality, the result of the strcmp or strncmp function should be compared with zero to determine whether the strings are equal.

To understand just what it means for one string to be “greater than” or “less than” another string, consider the process of alphabetizing a series of last names. You would, no doubt, place “Jones” before “Smith,” because the first letter of “Jones” comes before the first letter of “Smith” in the alphabet. But the alphabet is more than just a list of 26 letters—it is an *ordered* list of characters. Each letter occurs in a specific position within the list. “Z” is more than just a letter of the alphabet; “Z” is specifically the 26th letter of the alphabet.

How does the computer know that one letter comes before another? All characters are represented inside the computer as numeric codes; when the computer compares two strings, it actually compares the numeric codes of the characters in the strings.

In an effort to standardize character representations, most computer manufacturers have designed their machines to utilize one of two popular coding schemes—ASCII or *EBCDIC*. Recall that ASCII stands for “American Standard Code for Information Interchange.” EBCDIC stands for “Extended Binary Coded Decimal Interchange Code.” There are other coding schemes as well.

ASCII and EBCDIC are called *character codes*, or character sets. Most readers of this book will be using desktop or notebook computers that use the ASCII character set. IBM mainframe computers use the EBCDIC character set. As Internet and World Wide Web usage becomes pervasive, the newer Unicode® character set is growing in popularity (www.unicode.org). String and character manipulations actually involve the manipulation of the appropriate numeric codes and not the characters themselves. This explains the interchangeability of characters and small integers in C++. Since it is meaningful to say

that one numeric code is greater than, less than or equal to another numeric code, it becomes possible to relate various characters or strings to one another by referring to the character codes. Appendix B contains the ASCII character codes.

## Portability Tip 8.4

The internal numeric codes used to represent characters may be different on different computers that use different character sets.

## Portability Tip 8.5

Do not explicitly test for ASCII codes, as in if ( rating == 65 ); rather, use the corresponding character constant, as in if ( rating == 'A' ).

> [Note: With some compilers, functions strcmp and strncmp always return -1, 0 or 1, as in the sample output of Fig. 8.32. With other compilers, these functions return 0 or the difference between the numeric codes of the first characters that differ in the strings being compared. For example, when s1 and s3 are compared, the first characters that differ between them are the first character of the second word in each string—N (numeric code 78) in s1 and H (numeric code 72) in s3, respectively. In this case, the return value will be 6 (or -6 if s3 is compared to s1).]

## Tokenizing a String with strtok

Function strtok breaks a string into a series of tokens. A token is a sequence of characters separated by delimiting characters (usually spaces or punctuation marks). For example, in a line of text, each word can be considered a token, and the spaces separating the words can be considered delimiters.

Multiple calls to strtok are required to break a string into tokens (assuming that the string contains more than one token). The first call to strtok contains two arguments, a string to be tokenized and a string containing characters that separate the tokens (i.e., delimiters). Line 19 in Fig. 8.33 assigns to tokenPtr a pointer to the first token in sentence. The second argument, " ", indicates that tokens in sentence are separated by spaces. Function strtok searches for the first character in sentence that is not a delimiting character (space). This begins the first token. The function then finds the next delimiting character in the string and replaces it with a null ('\0') character. This terminates the current token. Function strtok saves (in a static variable) a pointer to the next character following the token in sentence and returns a pointer to the current token.

```
1  // Fig. 8.33: fig08_33.cpp
2  // Using strtok to tokenize a string.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <cstring> // prototype for strtok
8  using std::strtok;
9
10 int main()
11 {
12  char sentence[] = "This is a sentence with 7 tokens";
13  char *tokenPtr;
14
15  cout << "The string to be tokenized is:\n" << sentence
16      << "\n\nThe tokens are:\n\n";
17
18  // begin tokenization of sentence
19  tokenPtr = strtok( sentence, " " );
20
21  // continue tokenizing sentence until tokenPtr becomes NULL
22  while ( tokenPtr != NULL )
23  {
24      cout << tokenPtr << '\n';
25      tokenPtr = strtok( NULL, " " ); // get next token
26  } // end while
27
28  cout << "\nAfter strtok, sentence = " << sentence << endl;
29  return 0; // indicates successful termination
30  } // end main
```

The string to be tokenized is:
This is a sentence with 7 tokens

The tokens are:

This
is
a
sentence
with
7
tokens

After strtok, sentence = This

Fig. 8.33 | Using strtok to tokenize a string. (Part 2 of 2.)

Subsequent calls to strtok to continue tokenizing sentence contain NULL as the first argument (line 25). The NULL argument indicates that the call to strtok should continue tokenizing from the location in sentence saved by the last call to strtok. Note that strtok maintains this saved information in a manner that is not visible to you. If no tokens remain when strtok is called, strtok returns NULL. The program of Fig. 8.33 uses strtok to tokenize the string "This is a sentence with 7 tokens". The program prints each token on a separate line. Line 28 outputs sentence after tokenization. Note that strtok modifies the input string; therefore, a copy of the string should be made if the program requires the original after the calls to strtok. When sentence is output after tokenization, note that only the word "This" prints, because strtok replaced each blank in sentence with a null character ('\0') during the tokenization process.

> Common Programming Error 8.22
> 
> Not realizing that strtok modifies the string being tokenized, then attempting to use that string as if it were the original unmodified string is a logic error.

## Determining String Lengths

Function strlen takes a string as an argument and returns the number of characters in the string—the terminating null character is not included in the length. The length is also the index of the null character. The program of Fig. 8.34 demonstrates function strlen.

```
// Fig. 8.34: fig08_34.cpp
// Using strlen.
#include <iostream>
using std::cout;
using std::endl;

#include <cstring> // prototype for strlen
using std::strlen;

int main()
{
    char *string1 = "abcdefghijklmnopqrstuvwxyz";
    char *string2 = "four";
    char *string3 = "Boston";

    cout << "The length of \"" << string1 << "\" is " << strlen( string1 )
        << "\nThe length of \"" << string2 << "\" is " << strlen( string2 )
        << "\nThe length of \"" << string3 << "\" is " << strlen( string3 )
        << endl;
    return 0; // indicates successful termination
} // end main
```

The length of "abcdefghijklmnopqrstuvwxyz" is 26
The length of "four" is 4
The length of "Boston" is 6

Fig. 8.34 | strlen returns the length of a char * string.

## 8.14 Wrap-Up

In this chapter we provided a detailed introduction to pointers, or variables that contain memory addresses as their values. We began by demonstrating how to declare and initialize pointers. You saw how to use the address operator (&) to assign the address of a variable to a pointer and the indirection operator (*) to access the data stored in the variable indirectly referenced by a pointer. We discussed passing arguments by reference using both pointer arguments and reference arguments.

You learned how to use const with pointers to enforce the principle of least privilege. We demonstrated using nonconstant pointers to nonconstant data, nonconstant pointers to constant data, constant pointers to nonconstant data, and constant pointers to constant data. We then used selection sort to demonstrate passing arrays and individual array elements by reference. We discussed the sizeof operator, which can be used to determine the sizes of data types and variables in bytes during program compilation.

We demonstrated how to use pointers in arithmetic and comparison expressions. You saw that pointer arithmetic can be used to jump from one element of an array to another. You learned how to use arrays of pointers, and more specifically string arrays (arrays of
