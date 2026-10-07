# The if Statement

# Listing 6.2 ifelse.cpp

```
// ifelse.cpp -- using the if else statement
#include <iostream>
int main()
{
    char ch;

    std::cout << "Type, and I shall repeat.\\n";
    std::cin.get(ch);
    while (ch != ' ')
{
        if (ch == '\n')
            std::cout << ch;    // done if newline
        else
            std::cout << ++ch;  // done otherwise
        std::cin.get(ch);
    }
    // try ch + 1 instead of ++ch for interesting effect
std::cout << "\nPlease cause the slight confusion.\\n";
    std::cin.get();
    std::cin.get();
    return 0;
}
```

Here's some sample output from the program in Listing 6.2:

Type, and I shall repeat.
An ineffable joy suffused me as I beheld
Bo!jofgbcmf!lkpvtvvgfe!inf!J|lcifme
The wonders of modern computing.
uixpoefst!pg!npefsujoh
nPlease cause the slight confusion.

Note that one of the Comments in Listing 6.2 suggests changing ++ch to ch+1 an interesting effect. Can you deduce what it will be? If not, try it out and see if you can explain what's happening. (Hint:Think about how count handles different types).

# Formatting if else Statements

Keep in mind the two alternatives in an if else statement must be single-statements. If you need more than one statement, you must use braces to collect them into a single block statement. Unlike some languages, such as BASIC and FORTRAN, C++ does not automatically consider everything between if and else a block, so you have to use braces to make the statements a block. The following code, for example, produces a compiler error: