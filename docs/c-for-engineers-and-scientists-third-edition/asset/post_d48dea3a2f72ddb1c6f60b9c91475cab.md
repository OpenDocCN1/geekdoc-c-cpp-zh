
# Completing the Basics

## 9.4 Character Manipulation Functions

In addition to the string functions provided by the string class, the C++ language provides several useful character class functions, listed in Table 9.5. The function declaration (prototype) for each function is contained in the header file string or cctype, which must be included in any program using these functions.

Table 9.5 Character Library Functions (Require the Header File string or cctype)

| Function Prototype | Description | Example |
| --- | --- | --- |
| int isalpha(charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter, otherwise, it returns a false (zero integer) | isalpha('a') |
| int isnum(charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter or digit, otherwise, it returns a false (zero integer) | char key; cin >> key; isnum(key); |
| int isupper(charExp) | Returns a true (non-zero integer) if charExp evaluates to an uppercase letter, otherwise, it returns a false (zero integer) | isupper('a') |
| int islower(charExp) | Returns a true (non-zero integer) if charExp evaluates to a lowercase letter, otherwise, it returns a false (zero integer) | islower('a') |
| int isdigit(charExp) | Returns a true (non-zero integer) if charExp evaluates to a digit (0 through 9), otherwise, it returns a false (zero integer) | isdigit('a') |
| int isascii(charExp) | Returns a true (non-zero integer) if charExp evaluates to an ASCII character, otherwise, it returns a false (zero integer) | isascii('a') |
| int isspace(charExp) | Returns a true (non-zero integer) if charExp evaluates to a space, otherwise, it returns a false (zero integer) | isspace(' ') |
| int isprint(charExp) | Returns a true (non-zero integer) if charExp evaluates to a printable character, otherwise, it returns a false (zero integer) | isprint('a') |
| int isctrl(charExp) | Returns a true (non-zero integer) if charExp evaluates to a control character, otherwise, it returns a false (zero integer) | isctrl('a') |

**Table 9.5** Character Library Functions (Require the Header File string or cctype) (continued)

| Function Prototype | Description | Example |
| --- | --- | --- |
| int ispunct(charExp) | Returns a true (non-zero integer) if charExp evaluates to punctuation; otherwise, returns a false (zero integer) | ispunct('!') |
| int isgraph(charExp) | Returns a true (non-zero integer) if charExp evaluates to a printable character other than space; otherwise, returns a false (zero integer) | isgraph(' ') |
| int toupper(charExp) | Returns the uppercase equivalent if charExp evaluates to a lowercase character; otherwise, returns the character code without modification | toupper('a') |
| int tolower(charExp) | Returns the lowercase equivalent if charExp evaluates to an uppercase character; otherwise, returns the character code without modification | tolower('A') |

All the `istype()` functions in Table 9.5 return a non-zero integer (Boolean true value) when the character meets the condition and a zero integer (Boolean false value) when the condition is not met, these functions are typically used in `if` statement. For example, the following code assumes `ch` is a character:

```cpp
if (isdigit(ch))
    cout << "The character just entered is a digit" << endl;
else if (ispunct(ch))
    cout << "The character just entered is a punctuation mark" << endl;
```

In this example, if `ch` contains a digit, the first statement is executed; if the character is a letter, the second statement is executed. In both cases, the character to be checked is included as an argument to the function. Program 9.13 illustrates this type of code in a program that counts the number of letters, digits, and other characters in a string. The characters to checked are obtained using the `string` class's `at()` method. In Program 9.13, this function is used in a `for` loop that cycles through the string from the first character to the last. The output produced by Program 9.13 is as follows:

```
The original string is: Hello!
This string contains 6 characters, which consist of
5 letters
0 digits
1 characters.
```

As indicated by this output, each of the 6 characters in the string has been categorized correctly as a letter, a digit, or other character.

### Program 9.13

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main()
{
    string str = "Hello!";
    char nextChar;
    int i;
    int numLetters = 0;
```

### Program 9.14

Typically, as in Program 9.13, the functions in Table 9.5 are used in a character-by-character manner on each character in a string. You see this again in Program 9.14, where lowercase character is converted to its uppercase equivalent using the `toupper()` function. This function converts only lowercase letters, leaving all other characters unaffected.

In Program 9.14, pay particular attention to the statement `for (i = 0; i < (int)str.length()); i++)` to cycle through each character in the string. Typically, by cycling through the string, a character at a time, each element in a string is accessed, using the `length()` function to determine when the end of the string has been reached. Review Program 9.13 to see that it is used in the same way. The only real difference is that in Program 9.14, each element is accessed using the subscript notation `str[i]`; in Program 9.14 the `at()` function is used. Although these two notations are interchangeable—and which one you use is a matter of choice—the two notations should not be mixed in the same program.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int i;
    string str;

    cout << "Type in any sequence of characters: ";
    getline(cin, str);

    // cycle through all elements of the string
    for (i = 0; i < (int)str.length()); i++)
        str[i] = toupper(str[i]);

    cout << "The characters just entered, in uppercase, are: "
        << str << endl;

    cin.ignore();
    return 0;
}
```

A sample run of Program 9.14 produced the following output:

```
Type in any sequence of characters: this is a test of 12345.
The characters just entered, in uppercase, are: THIS IS A TEST OF 12345.
```

## Character I/O

Although you have used `cin` and `getline()` to accept data entered from the keyboard in a more or less "cookbook" manner, you need to understand what data is being sent to the program and how the program must react to process the data. At a fundamental level, all input (as well as output) is done on a character-by-character basis, as illustrated in Figure 9.12.

Figure 9.12 shows the entry of every piece of data, whether it's a string or a number, consists of typing characters. For example, the string Hello consists of pressing and releasing the five character keys H, e, l, o, and the Enter key. Similarly, output of the number 26 consists of displaying the five characters 2, 9, and 5. Although programmers typically do not think of data in this manner, programs are restricted to this character-by-character I/O, and all of C++s higher-level I/O functions and stream objects are based on lower-level I/O functions. These more elemental character functions, which can be used by a programmer, are listed in Table 9.6.

## Point of Information: Why the char Type Uses Integer Values

In C++, a character is stored as an integer value, the reason is that, in addition to sometimes being confusing to beginners, the need to represent English letters and characters, a program needs special characters that have no equivalents: One is the end-of-file character that all computer systems use to designate the end of a file. The EOF can be transmitted from the keyboard, for example, on UNIX-based systems, it is generated by holding down the key and pressing D; on Windows-based systems, it is generated by holding down Ctrl and Z. On both, the sentinel is stored as the number -1, which has no character value. (You can check this by displaying the integer value of each character (see Program 9.15) and pressing Ctrl+D or Ctrl+Z, depending on the system you're using.)

By using a 16-bit integer value, more than 64,000 different characters can be represented. This range of characters provides enough storage for multiple character sets, including Arabic, Chinese, Hebrew, Japanese, and Russian, and almost all known symbols. Therefore, storing a character as an integer value has a practical value.

An important consequence of using integer codes for strings is that characters can be compared easily for alphabetical ordering. For example, as long as subsequent letter in an alphabet has a higher value than its preceding letter, the comparison of character values is reduced to the comparison of numeric values. Storing characters in numerical order ensures that adding one to a letter produces the next letter in the alphabet.
