# Chapter 9

```
cout << endl << "CCandyBox constructor1 called";
    m_Contents = new char[ strlen(str) + 1 ];
    strcpy_s(m_Contents, strlen(str) + 1, str);
}
```

```
~CCandyBox()
    // Destructor
{ delete[] m_Contents; }
};
```

The #include directive for the <iostream> header and the two using declarations are not strictly necessary here because Box.h contains the same code, but it does no harm to put them in. On the contrary, putting these statements in here also means that if you were to remove this code from Box.h because it was no longer required there, CandyBox.h still compiles.

The contents of Ex9_03.cpp is:

```
// Ex9_03.cpp
// Calling a base constructor from a derived class constructor
#include <iostream>                // For stream I/O
#include <cstring>                 // For strlen() and strcpy()
#include "CandyBox.h"              // For CBox and CCandyBox
using std::cout;
using std::endl;

int main()
{
    CBox myBox(4.0, 3.0, 2.0);
    CCandyBox myCandyBox;
    CCandyBox myMintBox(1.0, 2.0, 3.0, "Wafer Thin Mints");

    cout << endl
        << "myBox occupies " << sizeof myBox      // Show how much memory
        << " bytes" << endl                     // the objects require
        << "myCandyBox occupies " << sizeof myCandyBox
        << " bytes" << endl
        << "myMintBox occupies " << sizeof myMintBox
        << " bytes";
    cout << endl
        << "myMintBox volume is "               // Get volume of a
        << myMintBox.Volume();                 // CCandyBox object
    cout << endl;
    return 0;
}
```

# How It Works

As well as adding the additional constructor in the derived class, you have added an output statement in each constructor so you know when either gets called. The explicit call of the constructor for the CBox class appears after a colon in the function header of the derived class constructor. You have perhaps noticed that the notation is exactly the same as what you have been using for initializing members in a constructor anyway: