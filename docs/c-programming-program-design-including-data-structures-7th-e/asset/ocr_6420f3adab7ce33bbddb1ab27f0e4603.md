The following program illustrates how to use the modified definition of the class clockType:

```
#include <iostream>
#include "clockType.h"

using namespace std;

int main()
{
        clockType myClock(8, 23, 50);
        clockType yourClock(8, 23, 50);
        clockType tempClock(9, 16, 25);

        cout << "Line 6: myClock: ";
        myClock.printTime();
        cout << endl;

        cout << "Line 9: yourClock: ";
        yourClock.printTime();
        cout << endl;

        cout << "Line 12: tempClock: ";
        tempClock.printTime();
        cout << endl;

                //Compare myClock and yourClock
        if (myClock == yourClock) {
                cout << "Line 16: The time of myClock and "
                     << "yourClock are equal." << endl;
        }
        else
                cout << "Line 18: The time of myClock and "
                     << "yourClock are not equal." << endl;

                //Compare myClock and tempClock
        if (myClock == tempClock)
                cout << "Line 20: The time of myClock and "
                     << "tempClock are equal." << endl;
        else
                cout << "Line 22: The time of myClock and "
                     << "tempClock are not equal." << endl;

        return 0;
}//end main
```

# Sample Run:

```
Line 6: myClock: 08:23:50
Line 9: yourClock: 08:23:50
Line 12: tempClock: 09:16:25
Line 16: The time of myClock and yourClock are equal.
Line 22: The time of myClock and tempClock are not equal.
```