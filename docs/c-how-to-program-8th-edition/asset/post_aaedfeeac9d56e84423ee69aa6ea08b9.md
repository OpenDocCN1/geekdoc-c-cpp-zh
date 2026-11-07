
| Card | Suit | Color | Card | Suit | Color |
|---:|---:|---:|---:|---:|---:|
| 12 | 0 | 0 | 12 | 2 | 1 |
| 0 | 0 | 0 | 0 | 3 | 1 |
| 1 | 1 | 0 | 1 | 3 | 1 |
| 2 | 1 | 0 | 2 | 3 | 1 |
| 3 | 1 | 0 | 3 | 3 | 1 |
| 4 | 1 | 0 | 4 | 3 | 1 |
| 5 | 1 | 0 | 5 | 3 | 1 |
| 6 | 1 | 0 | 6 | 3 | 1 |
| 7 | 1 | 0 | 7 | 3 | 1 |
| 8 | 1 | 0 | 8 | 3 | 1 |
| 9 | 1 | 0 | 9 | 3 | 1 |
| 10 | 1 | 0 | 10 | 3 | 1 |
| 11 | 1 | 0 | 11 | 3 | 1 |
| 12 | 1 | 0 | 12 | 3 | 1 |

**Fig. 21.16** | Bit fields used to store a deck of cards. (Part 2 of 2.)

It’s possible to specify an **unnamed bit field**, in which case the field is used as **padding** in the structure. For example, the structure definition uses an unnamed three-bit field as padding—nothing can be stored in those three bits. Member b is stored in another storage unit.

```cpp
struct Example
{
    unsigned a : 13;
    unsigned   : 4; // align to next storage-unit boundary
    unsigned b : 4;
}; // end struct Example
```

An **unnamed bit field with a zero width** is used to align the next bit field on a new storage-unit boundary. For example, the structure definition

```cpp
struct Example
{
    unsigned a : 13;
    unsigned   : 0; // align to next storage-unit boundary
    unsigned b : 4;
}; // end struct Example
```

uses an unnamed 0-bit field to **skip** the remaining bits (as many as there are) of the storage unit in which a is stored and align b on the *next storage-unit boundary*.

![](img/bfd978e7e9b192bab46ec2a89e481263_842_0.png)

> **Portability Tip 21.5**  
> *Bit-field manipulations are machine dependent. For example, some computers allow bit fields to cross word boundaries, whereas others do not.*

![](img/bfd978e7e9b192bab46ec2a89e481263_842_1.png)

> **Common Programming Error 21.5**  
> *Attempting to access individual bits of a bit field with subscripting as if they were elements of an array is a compilation error. Bit fields are not “arrays of bits.”*

![](img/bfd978e7e9b192bab46ec2a89e481263_842_2.png)

> **Common Programming Error 21.6**  
> *Attempting to take the address of a bit field (the & operator may not be used with bit fields because a pointer can designate only a particular byte in memory and bit fields can start in the middle of a byte) is a compilation error.*

![](img/bfd978e7e9b192bab46ec2a89e481263_843_0.png)

### Performance Tip 21.2

> Although bit fields save space, using them can cause the compiler to generate slower-executing machine-language code. This occurs because it takes extra machine-language operations to access only portions of an addressable storage unit. This is one of many examples of the space–time trade-off that occur in computer science.

## 21.17 Character-Handling Library

Most data is entered into computers as characters—including letters, digits and various special symbols. In this section, we discuss C++’s capabilities for examining and manipulating individual characters. In the remainder of the chapter, we continue the discussion of character-string manipulation that we began in Chapter 8.

The character-handling library includes several functions that perform useful tests and manipulations of character data. Each function receives a character—represented as an int—or EOF as an argument. Characters are often manipulated as integers. Remember that EOF normally has the value −1 and that some hardware architectures do not allow negative values to be stored in char variables. Therefore, the character-handling functions manipulate characters as integers. Figure 21.17 summarizes the functions of the character-handling library. When using functions from the character-handling library, include the `<cctype>` header.

| Prototype | Description |
|---|---|
| `int isdigit( int c )` | Returns 1 if c is a digit and 0 otherwise. |
| `int isalpha( int c )` | Returns 1 if c is a letter and 0 otherwise. |
| `int isalnum( int c )` | Returns 1 if c is a digit or a letter and 0 otherwise. |
| `int isxdigit( int c )` | Returns 1 if c is a hexadecimal digit character and 0 otherwise. (See Appendix D, Number Systems, for a detailed explanation of binary, octal, decimal and hexadecimal numbers.) |
| `int islower( int c )` | Returns 1 if c is a lowercase letter and 0 otherwise. |
| `int isupper( int c )` | Returns 1 if c is an uppercase letter; 0 otherwise. |
| `int tolower( int c )` | If c is an uppercase letter, tolower returns c as a lowercase letter. Otherwise, tolower returns the argument unchanged. |
| `int toupper( int c )` | If c is a lowercase letter, toupper returns c as an uppercase letter. Otherwise, toupper returns the argument unchanged. |
| `int isspace( int c )` | Returns 1 if c is a white-space character—newline ('\n'), space (' '), form feed ('\f'), carriage return ('\r'), horizontal tab ('\t') or vertical tab ('\v')—and 0 otherwise. |
| `int iscntrl( int c )` | Returns 1 if c is a control character, such as newline ('\n'), form feed ('\f'), carriage return ('\r'), horizontal tab ('\t'), vertical tab ('\v'), alert ('\a'), or backspace ('\b')—and 0 otherwise. |
| `int ispunct( int c )` | Returns 1 if c is a printing character other than a space, a digit, or a letter and 0 otherwise. |
| `int isprint( int c )` | Returns 1 if c is a printing character including space (`' '`) and 0 otherwise. |
| `int isgraph( int c )` | Returns 1 if c is a printing character other than space (`' '`) and 0 otherwise. |

**Fig. 21.17** | Character-handling library functions. (Parts 1–2 of 2.)

Figure 21.18 demonstrates functions **isdigit**, **isalpha**, **isalnum** and **isxdigit**. Function **isdigit** determines whether its argument is a digit (0–9). Function **isalpha** determines whether its argument is an uppercase letter (A–Z) or a lowercase letter (a–z). Function **isalnum** determines whether its argument is an uppercase letter, a lowercase letter or a digit. Function **isxdigit** determines whether its argument is a hexadecimal digit (A–F, a–f, 0–9).

```cpp
1  // Fig. 21.18: fig21_18.cpp
2  // Character-handling functions isdigit, isalpha, isalnum and isxdigit.
3  #include <iostream>
4  #include <cctype> // character-handling function prototypes
5  using namespace std;
6
7  int main()
8  {
9     cout << "\nAccording to isdigit:\n"
10       << ( isdigit( '8' ) ? "8 is a " : "8 is not a" ) << " digit\n"
11       << ( isdigit( '#' ) ? "# is a " : "# is not a" ) << " digit\n";
12
13    cout << "\nAccording to isalpha:\n"
14       << ( isalpha( 'A' ) ? "A is a " : "A is not a" ) << " letter\n"
15       << ( isalpha( 'b' ) ? "b is a " : "b is not a" ) << " letter\n"
16       << ( isalpha( '&' ) ? "& is a " : "& is not a" ) << " letter\n"
17       << ( isalpha( '4' ) ? "4 is a " : "4 is not a" ) << " letter\n";
18
19    cout << "\nAccording to isalnum:\n"
20       << ( isalnum( 'A' ) ? "A is a " : "A is not a" )
21       << " digit or a letter\n"
22       << ( isalnum( '8' ) ? "8 is a " : "8 is not a" )
23       << " digit or a letter\n"
24       << ( isalnum( '#' ) ? "# is a " : "# is not a" )
25       << " digit or a letter\n";
26
27    cout << "\nAccording to isxdigit:\n"
28       << ( isxdigit( 'F' ) ? "F is a " : "F is not a" )
29       << " hexadecimal digit\n"
30       << ( isxdigit( 'J' ) ? "J is a " : "J is not a" )
31       << " hexadecimal digit\n"
32       << ( isxdigit( '7' ) ? "7 is a " : "7 is not a" )
33       << " hexadecimal digit\n"
34       << ( isxdigit( '$' ) ? "$ is a " : "$ is not a" )
35       << " hexadecimal digit\n"
36       << ( isxdigit( 'f' ) ? "f is a " : "f is not a" )
37       << " hexadecimal digit" << endl;
38 } // end main
```

```text
According to isdigit:
8 is a digit
# is not a digit

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
$ is not a hexadecimal digit
f is a hexadecimal digit
```

**Fig. 21.18** | Character-handling functions `isdigit`, `isalpha`, `isalnum` and `isxdigit`. (Parts 1–2 of 2.)

Figure 21.18 uses the conditional operator (`?:`) with each function to determine whether the string "is a" or the string "is not a" should be printed in the output for each character tested. For example, line 10 indicates that '8' is a digit—i.e., if `isdigit` returns a true (nonzero) value—the string "8 is a" is printed. If '8' is not a digit (i.e., if `isdigit` returns 0), the string "8 is not a" is printed.

Figure 21.19 demonstrates functions `islower`, `isupper`, `tolower` and `toupper`. Function `islower` determines whether its argument is a *lowercase letter* (a–z). Function `isupper` determines whether its argument is an *uppercase letter* (A–Z). Function `tolower` converts an uppercase letter to lowercase and returns the lowercase letter—if the argument is not an uppercase letter, `tolower` returns the argument value unchanged. Function `toupper` converts a lowercase letter to uppercase and returns the uppercase letter—if the argument is not a lowercase letter, `toupper` returns the argument value unchanged.

```cpp
1  // Fig. 21.19: fig21_19.cpp
2  // Character-handling functions islower, isupper, tolower and toupper.
3  #include <iostream>
4  #include <cctype> // character-handling function prototypes
5  using namespace std;
```

**Fig. 21.19** | Character-handling functions `islower`, `isupper`, `tolower` and `toupper`. (Part 1 of 2.)
