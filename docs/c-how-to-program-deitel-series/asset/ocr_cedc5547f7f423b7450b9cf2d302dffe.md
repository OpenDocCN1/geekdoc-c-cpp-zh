```
Player rolled 3 + 3 = 6
Point is 6
Player rolled 5 + 3 = 8
Player rolled 4 + 5 = 9
Player rolled 2 + 1 = 3
Player rolled 1 + 5 = 6
Player wins
```

Fig. 6.11 | Craps simulation. (Part 3 of 3.)

# enum Type Status

The player may win or lose on the first roll or on any subsequent roll. The program uses variable gameStatus to keep track of this. Variable gameStatus is declared to be of new type Status. Line 13 declares a user-defined type called an enumeration that’s introduced by the keyword enum and followed by a type name (in this case, Status) and a set of integer constants represented by identifiers. The values of these enumeration constants start at 0, unless specified otherwise, and increment by 1. In the preceding enumeration, the constant CONTINUE has the value 0, WON has the value 1 and LOST has the value 2. The identifiers in an enum must be unique, but separate enumeration constants can have the same integer value.

> **Good Programming Practice 6.2**
> 
> Capitalize the first letter of an identifier used as a user-defined type name.

> **Good Programming Practice 6.3**
> 
> Use only uppercase letters in enumeration constant names. This makes these constants stand out in a program and reminds you that enumeration constants are not variables.

Variables of user-defined type Status can be assigned only one of the three values declared in the enumeration. When the game is won, the program sets variable gameStatus to WON (lines 27 and 48). When the game is lost, the program sets variable gameStatus to LOST (lines 32 and 51). Otherwise, the program sets variable gameStatus to CONTINUE (line 35) to indicate that the dice must be rolled again.

> **Common Programming Error 6.5**
> 
> Assigning the integer equivalent of an enumeration constant (rather than the enumeration constant, itself) to a variable of the enumeration type is a compilation error.

Another popular enumeration is

```
enum Months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG,
    SEP, OCT, NOV, DEC };
```

which creates user-defined type Months with enumeration constants representing the months of the year. The first value in the preceding enumeration is explicitly set to 1, so the remaining values increment from 1, resulting in the values 1 through 12. Any enumeration constant can be assigned an integer value in the enumeration definition, and subsequent enumeration constants each have a value 1 higher than the preceding constant in the list until the next explicit setting.