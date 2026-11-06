
Bit-field manipulations are machine dependent. For example, some computers allow bit fields to cross word boundaries, whereas others do not.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2570_0.png)

### Common Programming Error 22.5

Attempting to access individual bits of a bit field with subscripting as if they were elements of an array is a compilation error. Bit fields are not "arrays of bits."

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2570_1.png)

### Common Programming Error 22.6

Attempting to take the address of a bit field (the & operator may not be used with bit fields because a pointer can designate only a particular byte in memory and bit fields can start in the middle of a byte) is a compilation error.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2571_0.png)

### Performance Tip 22.2

Although bit fields save space, using them can cause the compiler to generate slower-executing machine-language code. This occurs because it takes extra machine-language operations to access only portions of an addressable storage unit. This is one of many examples of the space–time trade-offs that occur in computer science.

## 22.7 Character-Handling Library

Most data is entered into computers as *characters*—including letters, digits and various special symbols. In this section, we discuss C++'s capabilities for examining and manipulating individual characters. In the remainder of the chapter, we continue the discussion of *character-string manipulation* that we began in Chapter 8.

The character-handling library includes several functions that perform useful tests and manipulations of character data. Each function receives a character—represented as an `int`—or `EOF` as an argument. *Characters are often manipulated as integers.* Remember that `EOF` normally has the value `−1` and that some hardware architectures do not allow negative values to be stored in `char` variables. Therefore, the character-handling functions manipulate characters as integers. Figure 22.17 summarizes the functions of the character-handling library. When using functions from the character-handling library, include the `<ctype>` header.

Fig. 22.17 Character-handling library functions.

| Prototype | Description |
|---|---|
| `int isdigit(int c)` | Returns `1` if `c` is a *digit* and `0` otherwise. |
| `int isalpha(int c)` | Returns `1` if `c` is a *letter* and `0` otherwise. |
| `int isalnum(int c)` | Returns `1` if `c` is a *digit* or a *letter* and `0` otherwise. |
| `int isxdigit(int c)` | Returns `1` if `c` is a *hexadecimal digit character* and `0` otherwise. (See **Appendix D** for a detailed explanation of binary, octal, decimal and hexadecimal numbers.) |
| `int islower(int c)` | Returns `1` if `c` is a *lowercase letter* and `0` otherwise. |
| `int isupper(int c)` | Returns `1` if `c` is an *uppercase letter*, `0` otherwise. |
| `int tolower(int c)` | If `c` is an *uppercase letter*, `tolower` returns `c` as a *lowercase letter*. Otherwise, `tolower` returns the argument *unchanged*. |
| `int toupper(int c)` | If `c` is a *lowercase letter*, `toupper` returns `c` as an *uppercase letter*. Otherwise, `toupper` returns the argument *unchanged*. |
| `int isspace(int c)` | Returns `1` if `c` is a *whitespace character*—newline (`'\n'`), space (`' '`), form feed (`'\f'`), carriage return (`'\r'`), horizontal tab (`'\t'`), or vertical tab (`'\v'`)—and `0` otherwise. |
| `int iscntrl(int c)` | Returns `1` if `c` is a *control character*, such as newline (`'\n'`), form feed (`'\f'`), carriage return (`'\r'`), horizontal tab (`'\t'`), vertical tab (`'\v'`), alert (`'\a'`), or backspace (`'\b'`)—and `0` otherwise. |
| `int ispunct(int c)` | Returns `1` if `c` is a *printing character other than a space, a digit, or a letter* and `0` otherwise. |
| `int isprint(int c)` | Returns `1` if `c` is a *printing character including space* (`' '`) and `0` otherwise. |
| `int isgraph(int c)` | Returns `1` if `c` is a *printing character other than space* (`' '`) and `0` otherwise. |

**Figure 22.18** demonstrates functions `isdigit`, `isalpha`, `isalnum` and `isxdigit`. Function `isdigit` determines whether its argument is a *digit* (`0–9`). Function `isalpha` determines whether its argument is an *uppercase letter* (`A–Z`) or a *lowercase letter* (`a–z`). Function `isalnum` determines whether its argument is an *uppercase letter*, a *lowercase letter* or a *digit*. Function `isxdigit` determines whether its argument is a *hexadecimal digit* (`A–F`, `a–f`, `0–9`).

```cpp
// Fig. 22.18: fig22_18.cpp
// Character-handling functions isdigit, isalpha, isalnum and isxdigit.
#include <iostream>
#include <cctype> // character-handling function prototypes
using namespace std;

int main() {
   cout << "\nAccording to isdigit:\n"
      << (isdigit('8') ? "8 is a " : "8 is not a ") << "digit\n"
      << (isdigit('$') ? "$ is a " : "$ is not a ") << "digit\n";

   cout << "\nAccording to isalpha:\n"
      << (isalpha('A') ? "A is a " : "A is not a ") << "letter\n"
      << (isalpha('b') ? "b is a " : "b is not a ") << "letter\n"
      << (isalpha('4') ? "4 is a " : "4 is not a ") << "letter\n";

   cout << "\nAccording to isalnum:\n"
      << (isalnum('A') ? "A is a " : "A is not a ")
      << " digit or letter\n"
      << (isalnum('8') ? "8 is a " : "8 is not a ")
      << " digit or letter\n"
      << (isalnum('#') ? "# is a " : "# is not a ")
      << " digit or letter\n";

   cout << "\nAccording to isxdigit:\n"
      << (isxdigit('F') ? "F is a " : "F is not a ")
      << " hexadecimal digit\n"
      << (isxdigit('J') ? "J is a " : "J is not a ")
      << " hexadecimal digit\n"
      << (isxdigit('7') ? "7 is a " : "7 is not a ")
      << " hexadecimal digit\n"
      << (isxdigit('S') ? "S is a " : "S is not a ")
      << " hexadecimal digit\n"
      << (isxdigit('f') ? "f is a " : "f is not a ")
      << " hexadecimal digit" << endl;
}
```

According to isdigit:
8 is a digit
$ is not a digit

According to isalpha:
A is a letter
b is a letter
& is not a letter
4 is not a letter

According to isalnum:
A is a digit or a letter
8 is a digit or a letter
# is not a digit or a letter

According to isxdigit:
F is a hexadecimal digit
J is not a hexadecimal digit
7 is a hexadecimal digit
S is not a hexadecimal digit
f is a hexadecimal digit

Fig. 22.18 Character-handling functions `isdigit`, `isalpha`, `isalnum` and `isxdigit`.

**Figure 22.18** uses the *conditional operator* `(?:)` with each function to determine whether the string `" is a "` or the string `" is not a "` should be printed in the output for each character tested. For example, line 9 indicates that if `'8'` is a digit—i.e., if `isdigit` returns a true (nonzero) value—the string `"8 is a "` is printed. If `'8'` is not a digit (i.e., if `isdigit` returns `0`), the string `"8 is not a "` is printed.

**Figure 22.19** demonstrates functions `islower`, `isupper`, `tolower` and `toupper`. Function `islower` determines whether its argument is a *lowercase letter* (`a-z`). Function `isupper` determines whether its argument is an *uppercase letter* (`A-Z`). Function `tolower` converts an uppercase letter to lowercase and returns the lowercase letter—if the argument is not an uppercase letter, `tolower` returns the argument value unchanged. Function `toupper` converts a lowercase letter to uppercase and returns the uppercase letter—if the argument is *not* a lowercase letter, `toupper` returns the argument value *unchanged*.

```cpp
// Fig. 22.19: fig22_19.cpp
// Character-handling functions islower, isupper, tolower and toupper.
#include <iostream>
#include <cctype> // character-handling function prototypes
using namespace std;

int main() {
   cout << "According to islower:\n"
      << (islower('p') ? "p is a" : "p is not a")
      << " lowercase letter\n"
      << (islower('P') ? "P is a" : "P is not a")
      << " lowercase letter\n"
      << (islower('5') ? "5 is a" : "5 is not a")
      << " lowercase letter\n"
      << (islower('$') ? "$ is a" : "$ is not a")
      << " lowercase letter\n";

   cout << "\nAccording to isupper:\n"
      << (isupper('D') ? "D is an" : "D is not an")
      << " uppercase letter\n"
      << (isupper('d') ? "d is an" : "d is not an")
      << " uppercase letter\n"
      << (isupper('8') ? "8 is an" : "8 is not an")
      << " uppercase letter\n"
      << (isupper('$') ? "$ is an" : "$ is not an")
      << " uppercase letter\n";
}
```
