Here is the output from the program in Listing 4.11:

Expand your guest list with Glorious Gloria and Audacious Arthur!
You can have both for $62.98!

# Program Notes

One important matter related to the program in Listing 4.11 is where to place the structure declaration. There are two choices for structure.cpp.You could place the declaration inside the main() function, just after the opening brace.The second choice, and the one made here, is to place it outside and preceding main().When a declaration occurs outside any function, it can be an external declaration. There is no practical difference between the two choices. But for programs consisting of two or more functions, the difference can be crucial.The external declaration can be used by all the functions following, whereas the internal declaration can be used only by the function in which it is found. Most often, you want an external structure declaration so that all the functions can use structures of that type (see Figure 4.7).

```
#include <iostream>
using namespace std;
struct parts
    unsigned long part_number;
    float part_cost;
};
void main();
int main()
{
    struct perks
        int key_number;
        char car[12];
    };
    parts chicken;
    perks mr_brug;
    ...
}
void mail()
{
    parts studebaker
    ...
}
```

external declaration—can be used in all functions in

local declaration—can be used only in this function

type parts variable
type perks variable

type parts variable
can’t declare a type
ks variable here

Figure 4.7 Local and external structure declarations.

Variables, too, can be defined internally or externally, with external variables shared among functions. (Chapter 9,”Memory Models and Namespaces,”looks further into this topic) C++ practices discourage the use of external variables but encourage the use of