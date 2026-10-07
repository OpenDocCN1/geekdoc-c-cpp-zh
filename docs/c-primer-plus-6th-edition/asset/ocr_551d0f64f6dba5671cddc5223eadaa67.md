# Chapter 13 Class Inheritance

However, this approach has the effect of calling the default string constructor for firstname and invoking the string assignment operator to reset filename to fn. But the member initializer list syntax saves a step by using the string constructor to initialize filename to fn.
Listing 13.3 shows this modest class in action.

Listing 13.3 usett0.cpp

```
// usett0.cpp -- using a base class
#include <iostream>
#include "tabtenn0.h"

int main ( void )
{\n    using std::;
    TableTennisPlayer player1("Chuck", "Blizzard", true);
    TableTennisPlayer player2("Tara", "Boomdea", false);
    player1.Name();
    if (player1.HasTable())
        cout << ": has a table.\n";
    else
        cout << ": hasn't a table.\n";
    player2.Name();
    if (player2.HasTable())
        cout << ": has a table\n";
    else
        cout << ": hasn't a table.\n";

    return 0;
}
```

And here's the output of the program in Listings 13.1, 13.2, and 13.3:
Blizzard, Chuck: has a table.
Boomdea, Tara: has a table.

Note that the program uses constructors with C-style string arguments:
TableTennisPlayer player1("Chuck", "Blizzard", true);
TableTennisPlayer player2("Tara", "Boomdea", false);

But the formal parameters for the constructor were declared as type const string &. This is a type mismatch, the string class, like the string class of Chapter 12, has a constructor with a const char * parameter, and that is used automatically to create a string object initialized by the C-style string. In short, you can use either string object or a C-style string as an argument to the TableTennisPlayer constructor. The first invokes a string constructor with a const string & parameter, and the second invokes a string constructor with a const char * parameter.