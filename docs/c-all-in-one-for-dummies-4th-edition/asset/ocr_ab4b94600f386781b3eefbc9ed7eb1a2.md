You would then have the three source code files used for the MultipleSource Files2 example, shown in Listings 7-3, 7-4, and 7-5:

+   - `main.cpp`: Calls the function
+   - `safestuff.h`: Contains the function prototype
+   - `safestuff.cpp`: Contains the actual code for the function whose prototype appears in the header file

Lots of files, but now the code is broken into manageable pieces. Also, make sure that you save all three of these files in the same directory.

# LISTING 7-3: Including the Header File in the main File

```
#include <iostream>
#include "safestuff.h"

using namespace std;

int main()
{
    cout << "Surprise, surprise!" << endl;
    cout << "The combination for Safe 12 is: " << endl;
    cout << SafeCracker(12) << endl;
    cout << "Let's check on Safe 11 too: " << endl;
    cout << SafeCracker(11) << endl;
    return 0;
}
```

# LISTING 7-4: Containing the Function Prototype in the Header File

```
#ifndef SAFESTUFF_H_INCLUDED
#define SAFESTUFF_H_INCLUDED

using namespace std;

string SafeCracker(int SafeID);

#endif // SAFESTUFF_H_INCLUDED
```