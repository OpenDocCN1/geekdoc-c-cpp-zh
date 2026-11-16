| Arity | Operators | Associativity |
| :--- | :--- | :--- |
| unary | (post) ++ (post) -- static_cast | |
| unary | (pre) ++ (pre) -- - + ! ~ | |
| binary | * / % | left |
| binary | + - | left |
| binary | << >> | left |
| binary | < > <= >= | left |
| binary | == != | left |
| binary | & | left |
| binary | ^ | left |
| binary | | | left |
| binary | && | left |
| binary | || | left |
| binary | =, +=, -=, *=, /=, %= | right |

Suppose you wish to print the word “OK” if a variable x is 1, 2, or 3. An informal translation from English might yield:

```
if (x == 1 || 2 || 3)
    std::cout << "OK\n";
```

Unfortunately, x’s value is irrelevant; the code always prints the word “OK”. Since the == operator has higher precedence than ||, the expression

```
x == 1 || 2 || 3
```

![](bbox=[0.22, 0.48, 0.26, 0.515])

```
(x == 1) || 2 || 3
```

The expression x == 1 is either true or false, but integer 2 is always interpreted as true, and integer 3 is interpreted as true as well.

The correct statement would be

```
if (x == 1 || x == 2 || x == 3)
    std::cout << "OK\n";
```

The revised Boolean expression is more verbose and less similar to the English rendition, but it is the correct formulation for C+.

Our current list of C++ operators is shown in Table 5.4.

# 5.7 Nested Conditionals

The statements in the body of the if or the else may be any C++ statements, including other if/else statements. We can use nested if statements to build arbitrarily complex control flow logic. Consider Listing 5.7 (checkrange.cpp) that determines if a number is between 0 and 10, inclusive.

```
Listing 5.7: checkrange.cpp

#include <iostream>
```