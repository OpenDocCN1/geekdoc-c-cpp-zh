```
```cpp
33    << " hexadecimal digit\\n"
34    << ( isxdigit('8') ? "8 is a " : "8 is not a " )
35    << "hexadecimal digit\\n"
36    << ( isxdigit('7') ? "7 is a " : "7 is not a " )
37    << "hexadecimal digit" << endl;
38 } // end main
```
```

```
```
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
I is not a hexadecimal digit
7 is a hexadecimal digit
$ is not a hexadecimal digit
f is a hexadecimal digit
```
```

**Fig. 21.18** | Character-handling functions `isdigit`, `isalpha`, `isalnum` and `isxdigit`. (Part 2 of 2.)

Figure 21.18 uses the conditional operator (`?:`) with each function to determine whether the string "is a" or the string "is not a" should be printed in the output for each character tested. For example, line 10 indicates that '8' is a digit—i.e., if `isdigit` returns a true (nonzero) value—the string "8 is a" is printed. If '8' is not a digit (i.e., if `isdigit` returns 0), the string "8 is not a" is printed.

Figure 21.19 demonstrates functions `islower`, `isupper`, `tolower` and `toupper`. Function `islower` determines whether its argument is a *lowercase letter* (a–z). Function `isupper` determines whether its argument is an *uppercase letter* (A–Z). Function `tolower` converts an uppercase letter to lowercase and returns the lowercase letter—if the argument is not an uppercase letter, `tolower` returns the argument value unchanged. Function `toupper` converts a lowercase letter to uppercase and returns the uppercase letter—if the argument is not a lowercase letter, `toupper` returns the argument value unchanged.

```
```cpp
1  // Fig. 21.19: fig21_19.cpp
2  // Character-handling functions islower, isupper, tolower and toupper.
3  #include <iostream>
4  #include <cctype> // character-handling function prototypes
5  using namespace std;
```
```

**Fig. 21.19** | Character-handling functions `islower`, `isupper`, `tolower` and `toupper`. (Part 1 of 2.)