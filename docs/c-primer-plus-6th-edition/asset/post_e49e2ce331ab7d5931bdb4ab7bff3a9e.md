
## Chapter 6 Branching Statements and Logical Operators

used precedence rules, and it reduces the chance of making errors because you don't quite remember the exact rule that applies.

C++ guarantees that when a program evaluates a logical expression, it evaluates it from left to right and stops evaluation as soon as it knows what the answer is. Suppose, for example, you have this condition:

```
x != 0 && 1.0 / x > 100.0
```

If the first condition is false, then the expression must be false. That's because for this expression to be true, each individual condition must be true. Knowing the first condition is false, the program doesn't bother evaluating the second condition. That's fortunate in this example because evaluating the second condition could result in dividing by zero, which is not in a computer's repertoire of possible actions.

## Alternative Representations

Not all keyboards provide all the symbols used for the logical operators, so the C++ Standard provides alternative representations, as shown in Table 6.3. The identifiers and, or and not are not C++ reserved words, meaning that you can not use them as names for variables or so. They are not considered keywords because they are alternative representations of existing language features. Incidentally, these are not reserved words in C, but a C program can use them as operators, provided that the program includes the iso646.h header file.

Table 6.3 Logical Operators: Alternative Representations
| Operator | Alternative Representation |
| --- | --- |
| && | and |
| || | or |
| ! | not |

## The cctype Library of Character Functions

C++ has inherited from C handy package of character-related functions, prototyped in the cctype header file (ctype.h, in the older style), that simplify such tasks as determining whether a character is an uppercase letter or a digit or punctuation. For example, isalpha (ch) function returns a nonzero value if ch is a letter and a zero value otherwise. Similarly, ispunct (ch) function returns a true value only if ch is a punctuation character, as a comma or period. (These functions return type int rather than bool, but the usual bool conversions allow you to treat them as bool.)

Using these functions is more convenient than using the AND OR operators. For example, here is how you might use AND and OR to test a character ch is an alphabetical character:

```
if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z'))
```

Compare to using isalpha():
```
if (isalpha(ch))
```

Not only is isalpha() easier to use, it is more general. The AND/OR form assumes that character codes for A through Z are in sequence, with no other characters having codes in range. This assumption is true for ASCII codes, but it't always true in general.

Listing 6.8 demonstrates some functions from the cctype family. In particular, it uses isalpha(), which tests for alphabetic characters; isdigit(), which tests for digit characters, as 3; isspace(), which tests for whitespace characters, as newlines, spaces, and tabs; and ispunct(), which tests for punctuation characters. The program also reviews the else if structure and using a while loop with cin.get(char).

## Listing 6.8 cctypes.cpp

```cpp
// cctypes.cpp -- using the ctype.h library
#include <iostream>
#include <cctype>                                     // prototypes for character functions
int main()
{
    using namespace std;
    cout << "Enter text for analysis, and type @"
         << "to terminate input.\n";
    char ch;
    int whitespace = 0;
    int digits = 0;
    int chars = 0;
    int punct = 0;
    int others = 0;

    cin.get(ch);                                     // get first character
    while (ch != '@')                                 // test for sentinel
    {
        if (isalpha(ch))                                 // it is an alphabetic character?
            chars++;
        else if (isspace(ch))                        // it is a whitespace character?
            whitespace++;
        else if (isdigit(ch))                          // it is a digit?
            digits++;
        else if (ispunct(ch))                         // it is a punctuation?
            punct++;
        else
            others++;
        cin.get(ch);                                 // get next character
    }

    cout << chars << " letters, "
    << whitespace << " whitespace, "
    << digits << " digits, "
    << punct << " punctuations, "
    << others << " others.\n";

    return 0;
}
```

Here is a sample run of the program in Listing 6.8 (note that the whitespace includes newlines):

Enter text for analysis, and type @ to terminate input.
Vision International producer Adrienne Vismonger announced production of their new 3-D film, a remake of
"My Dinner with Andre," scheduled for 2013. "Wait until
y see the the new scene with an enraged Colossipede!"
177 letters, 33 whitespace, 5 digits, 9 punctuations, 0 others.

Table 6.4 summarizes the functions available in the cctype package. Some systems may lack some of these functions or have additional ones.

| Function Name | Return Value |
| --- | --- |
| isalnum() | This function returns true if the argument is alphanumeric (that is, a letter or a digit). |
| alpha() | This function returns true if the argument is alphabetic. |
| isblank() | This function returns true if the argument is a space. |
| iscntrl() | This function returns true if the argument is control. |
| isdigit() | This function returns true if the argument is decimal digit (0–9). |
| isgraph() | This function returns true if the argument is any printing character other than space. |
| islower() | This function returns true if the argument is a lowercase letter. |
| isprint() | This function returns true if the argument is any printing character. |
| ispunct() | This function returns true if the argument is a punctuation character. |
| isspace() | This function returns true if the argument is standard-space character (that is, space, newline, horizontal tab, vertical tab). |
| isupper() | This function returns true if the argument is an uppercase letter. |

## The ? : Operator

C++ has an operator that often be used instead of if else statement. This operator is called the conditional operator, written ?, and for you trivia buffs, it is the only C++ operator that requires three operands. The general form looks like this:

expression1 ? expression2 : expression3

If expression1 is true, then the value of the conditional expression is the value of expression2. Otherwise, the value of the whole expression is the value of expression3. Here are two examples that show how the operator works:

5 > 3 ? 12 : 5 // // 5 > 3 is true, so expression value is 10
3 == 9 ? 25 : 18 // // 3 == 9 is false, so expression value is 18

We can paraphrase the first example this way: If 5 is greater than 3, the expression evaluates to 10; otherwise, it evaluates to 12. In real programming situations, of course, the expression would involve variables:

Listing 6.9 uses the conditional operator to determine the larger of two values.

Listing 6.9 condit.cpp

```cpp
// condit.cpp -- using the conditional operator
#include <iostream>
int main() {
    using namespace std;
    int a, b;
    cout << "Enter two integers: ";
    cin >> a >> b;
    cout << "The larger of " << a << " and " << b;
    int c = a > b ? a : b; // c = a > b, else c = b
    cout << " is " << c << endl;
    return 0;
}
```
