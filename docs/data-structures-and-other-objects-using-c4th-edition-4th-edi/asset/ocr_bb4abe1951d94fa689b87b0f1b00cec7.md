```
double random_real(double low, double high)
// Library facilities used: cassert
//
assert(low <= high);
return low + random_fraction() * (high - low);
}
```

# Appendix J

# Fundamental Style Guide

# Specifications with Preconditions and Postconditions

This appendix outlines three of our fundamental style guidelines. Each of our function's behavior is specified with a precondition/postcondition contract.

For a function that is provided as part of a collection of functions, the contract appears in a comment at the top of the toolkit's header file.

For a member function of a class that is provided with a header file and implementation file, the contract appears in a comment at the top of the class's header file.

For a function that is implemented and used only in a ".cxx" file, the contract appears with the function's implementation in the ".cxx" file.

# Capitalization

Variable names and function names are written with all lowercase letters. If the name consists of several words, then these words are separated by an underscore (such as eat_white).

Declared constants and member constants of a class are written with all uppercase letters. If the name consists of several words, then these words are separated by an underscore (such as MANY_COLUMNS). However, constant function parameters are written with lowercase letters (just like any other parameter).

New class names are written in lowercase, preferably as a noun. This differs from our first edition of the text (where we used an initial capital letter). The reason for the change is to better match the Standard Template Library, where class names are lowercase letters and the name of a template parameter (such as Item) has an initial capital.

# Indentation

Any statements grouped between brackets ('{' and '}') are indented four spaces. The brackets themselves appear on separate lines with no extra indentation. The only exceptions are the keywords public, private, or protected (in a class definition), which appear on lines by themselves with the same indentation as the brackets.

In a loop or conditional statement with a one-line body (i.e., no brackets), the one line appears on a line by itself with four spaces of indentation beyond the loop or conditional statement.

The statements that follow a case label of a switch statement are written with at least four spaces of indentation beyond the case label.