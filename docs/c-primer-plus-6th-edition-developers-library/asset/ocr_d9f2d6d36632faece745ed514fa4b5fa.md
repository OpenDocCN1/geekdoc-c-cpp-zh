you can use them as sizes in array declarations, and you can use them as labels in a switch statement.

# Default Values

By default, the constants in the enumeration list are assigned the integer values 0, 1, 2, and so on. Therefore, the declaration

```
enum kids {nippy, slats, skippy, nina, liz};
```

results in nina having the value 3.

# Assigned Values

You can choose the integer values that you want the constants to have. Just include the desired values in the declaration:

```
enum levels {low = 100, medium = 500, high = 2000};
```

If you assign a value to one constant but not to the following constants, the following constants will be numbered sequentially. For example, suppose you have this declaration:

```
enum feline {cat, lynx = 10, puma, tiger};
```

Then cat is 0, by default, and lynx, puma, and tiger are 10, 11, and 12, respectively.

# enum Usage

Recall that the purpose of enumerated types is to enhance a program’s readability and make it easier to maintain. If you are dealing with colors, using red and blue is much more obvious than using 0 and 1. Note that the enumerated types are for internal use. If you want to enter a value of orange for color, you have to enter a 1, not the word orange, or you can read in the string "orange" and have the program convert it to the value orange.

Because the enumerated type is an integer type, enum variables can be used in expressions in the same manner as integer variables. They make convenient labels for a case statement.

Listing 14.15 shows a short example using enum. The example relies on the default value-assignment scheme. This gives red the value 0, which makes it the index for the pointer to the string "red".

# Listing 14.15 The enum.c Program

```
/* enum.c -- uses enumerated values */
#include <stdio.h>
#include <string.h>   // for strcmp(), strchr()
#include <stdbool.h>  // C99 feature
char * s_gets(char * st, int n);
```