```
// Fig. 9.27: fig09_27.cpp
// Cascading member-function calls with the this pointer.
#include <iostream>
#include "Time.h" // Time class definition
using namespace std;

int main() {
    Time t; // create Time object

    t.setHour(18).setMinute(30).setSecond(22); // cascaded function calls

    // output time in universal and standard formats
    cout << "Universal time: " << t.toUniversalString()
         << "\nStandard time: " << t.toStandardString();

    // cascaded function calls
    cout << "\n\nNew standard time: "
         << t.setTime(20, 20, 20).toStandardString() << endl;
}
```

```
Universal time: 18:30:22
Standard time: 6:30:22 PM

New standard time: 8:20:20 PM
```

# Fig. 9.27 Cascading member-function calls with the `this` pointer.

Line 18 (Fig. 9.27) also uses cascading. Note that we cannot chain another `Time` member-function call after `toStandardString` here, because it does *not* return a reference to `t`—we could, however, place a call to a `string` member function, because `toStandardString` returns a `string`. Placing the call to `toStandardString` before the call to `setTime` in line 18 results in a compilation error, because the `string` returned by `toStandardString` does not have a `setTime` function.

`Chapter 10` presents several practical examples of using cascaded function calls. One such example uses multiple `<<` operators with `cout` to output multiple values in a single statement.