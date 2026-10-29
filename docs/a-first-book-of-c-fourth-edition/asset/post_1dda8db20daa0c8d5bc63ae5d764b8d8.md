
If the statement str.replace(12, 6, "to"); is executed next, the existing characters in index positions 12 through 17 are deleted, and the two characters contained in to are inserted starting at index position 12. Figure 14.8 shows the net effect of this replacement. The number of replacement characters (in this case, two) can be fewer than, equal to, or greater than the number of characters being replaced, which in this case is six.

## Character position:

![](img/202cface8244f523c2641baa2e00d7dd_638_0.png)

## Figure 14.8 The string after the replacement

Finally, if you append the string "correct" to the string shown in Figure 14.8 by using the concatenation operator, +, you get the string shown in Figure 14.9.

## Character position:

![](img/202cface8244f523c2641baa2e00d7dd_638_1.png)

## Figure 14.9 The string after the append

Program 14.6 uses these statements in a complete program.

## Program 14.6

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string str = "This cannot be";

    cout << "The original string is: " << str << endl
         << " and has " << int(str.length()) << " characters." << endl;

    // insert characters
    str.insert(4," I know");
    cout << "The string, after insertion, is: " << str << endl
         << " and has " << int(str.length()) << " characters." << endl;
```

## The string Class and Exception Handling

```
// replace characters
str.replace(12, 6, "to");
cout << "The string, after replacement, is: " << str << endl
     << "  and has " << int(str.length()) << " characters." << endl;

// append characters
str = str + " correct";
cout << "The string, after appending, is: " << str << endl
     << "  and has " << int(str.length()) << " characters." << endl;

return 0;
}
```

The following output produced by Program 14.6 matches the strings shown in Figures 14.6 to 14.9:

```
The original string is: This cannot be
  and has 14 characters.
The string, after insertion, is: This I know cannot be
  and has 21 characters.
The string, after replacement, is: This I know to be
  and has 17 characters.
The string, after appending, is: This I know to be correct
  and has 25 characters.
```

Of the remaining string methods in Table 14.3, the most commonly used are those that locate specific characters in a string and create substrings. A **substring** is any sequence of characters contained in the original string. Program 14.7 shows how some of these other methods are used.

## Program 14.7

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string string1 = "LINEAR PROGRAMMING THEORY";
    string s1, s2, s3;
    int j, k;

    cout << "The original string is " << string1 << endl;
```

```
j = int(string1.find('I'));
cout << " The first position of an 'I' is " << j << endl;

k = int(string1.find('I', (j+1)));
cout << " The next position of an 'I' is " << k << endl;

j = int(string1.find("THEORY"));
cout << " The first location of \"THEORY\" is " << j << endl;

k = int(string1.find("ING"));
cout << " The first index of \"ING\" is " << k << endl;

// now extract three substrings
s1 = string1.substr(2,5);
s2 = string1.substr(19,3);
s3 = string1.substr(6,8);

cout << "The substrings extracted are:" << endl
     << " " << s1 + s2 + s3 << endl;

return 0;
}
```

Here's the output produced by Program 14.7:

```
The original string is LINEAR PROGRAMMING THEORY
The first position of an 'I' is 1
The next position of an 'I' is 15
The first location of "THEORY" is 19
The first index of "ING" is 15
The substrings extracted are:
NEAR THE PROGRAM
```

The main point shown in Program 14.7 is that characters and sequences of characters can be located and extracted from a string with string class methods.

## EXERCISES 14.1

- 1. (Practice) Enter and run Program 14.2.
- 2. (Practice) Determine the value of text.at(0), text.at(3), and text.at(10), assuming for each one that text is each of the following strings:
- a. Now is the time
- b. Rocky raccoon welcomes you
- c. Happy Holidays
- d. The good ship
- 3. (Practice) Enter and run Program 14.5.
- 4. (Modify) Modify Program 14.5 to count and display the numbers of each vowel contained in the string.
- 5. (Modify) Modify Program 14.5 to display the number of vowels in a user-entered string.
- 6. (Program) Using the at() method, write a C++ program that reads in a string by using getline(), stores the string in a string object named message, and then displays the string in reverse order. (Hint: After the string has been entered and saved, retrieve and display characters, starting from the end of the string. The last character is located at the position message.length() - 1.)
- 7. (Program) Write a C++ program that accepts both a string and a single character from the user. The program should determine how many times the character is contained in the string. (Hint: Search the string by using the find(str, ind) method. This method should be used in a loop that starts the index value at 0 and then changes the index value to 1 past the index of where the char was last found.)
- 8. (Practice) Enter and run Program 14.6.
- 9. (Practice) Enter and run Program 14.7.

## 14.2 Character Manipulation Methods

In addition to the string methods from the string class, C++ provides several useful character class methods, listed in Table 14.4. The header files string and cctype must be included in any program using these methods.

## Table 14.4 Character Library Methods (Require the Header Files string and cctype)

| Method Prototype | Description | Example |
|---|---|---|
| int isalpha (charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter; otherwise, it returns a false (zero integer) | isalpha('a') |
| int isalnum (charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter or a digit; otherwise, it returns a false (zero integer) | isalnum(key) |
| int isupper (charExp) | Returns a true (non-zero integer) if charExp evaluates to an uppercase letter; otherwise, it returns a false (zero integer) | isupper('a') |
| int islower (charExp) | Returns a true (non-zero integer) if charExp evaluates to a lowercase letter; otherwise, it returns a false (zero integer) | islower('a') |
| int isdigit (charExp) | Returns a true (non-zero integer) if charExp evaluates to a digit (0 through 9); otherwise, it returns a false (zero integer) | isdigit('a') |

## Table 14.4 Character Library Methods (Require the Header Files `string` and `cctype`) *(continued)*

| Method | Description | Example |
|---|---|---|
| `int isascii (charExp)` | Returns a true (non-zero integer) if charExp evaluates to an ASCII character; otherwise, returns a false (zero integer) | `isascii('a')` |
| `int isspace (charExp)` | Returns a true (non-zero integer) if charExp evaluates to a space; otherwise, returns a false (zero integer) | `isspace(' ')` |
| `int isprint (charExp)` | Returns a true (non-zero integer) if charExp evaluates to a printable character; otherwise, returns a false (zero integer) | `isprint('a')` |
| `int isctrl (charExp)` | Returns a true (non-zero integer) if charExp evaluates to a control character; otherwise, it returns a false (zero integer) | `isctrl('a')` |
| `int ispunct (charExp)` | Returns a true (non-zero integer) if charExp evaluates to a punctuation character; otherwise, returns a false (zero integer) | `ispunct('!')` |
| `int isgraph (charExp)` | Returns a true (non-zero integer) if charExp evaluates to a printable character other than white space; otherwise, returns a false (zero integer) | `isgraph(' ')` |
| `int toupper (charExp)` | Returns the uppercase equivalent if charExp evaluates to a lowercase character; otherwise, returns the character code without modification | `toupper('a')` |
| `int tolower (charExp)` | Returns the lowercase equivalent if charExp evaluates to an uppercase character; otherwise, returns the character code without modification | `tolower('A')` |

Because all the `istype()` methods listed in Table 14.4 return a non-zero integer (interpreted as a Boolean true value) when the character meets the condition and a zero integer (interpreted as a Boolean false value) when the condition isn't met, these methods are typically used in an `if` statement. For example, the following code segment assumes `ch` is a character variable:

```
if(isdigit(ch))
    cout << "The character just entered is a digit" << endl;
else if(ispunct(ch))
    cout << "The character just entered is a punctuation mark" << endl;
```
