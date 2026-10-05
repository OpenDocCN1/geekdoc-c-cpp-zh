# 5.7. NESTED CONDITIONALS

corresponding value is one. Listing 5.12 (timeconvcond1.cpp) uses if/else statements to express time units with the correct number.

# Listing 5.12: timeconvcond1.cpp

```
// File timeconvcond1.cpp
#include <iostream>
using namespace std;
int main() {
    // Some useful conversion constants
    const int SECONDS_PER_MINUTE = 60;
    const int SECONDS_PER_HOUR = 60*SECONDS_PER_MINUTE; // 3600
    int hours, seconds;
    cout << "Please enter the number of hours in seconds:";
    cin >> seconds;
    // First, compute the number of hours in the given number
    hours = seconds / SECONDS_PER_HOUR; // 3600 seconds = 1 hours
    // Compute the remaining seconds after hours are accounted
    seconds = seconds % SECONDS_PER_HOUR;
    // Compute the number of minutes in the remaining
    minutes = seconds / SECONDS_PER_MINUTE; // 60 seconds = 1 minute
    // Compute the remaining seconds after the minutes are accounted
    seconds = seconds % SECONDS_PER_MINUTE;
    // Report the results
    cout << hours:";
    // Decide between singular and plural form of hours
    if (hours == 1)
        cout << " hour";
    else
        cout << " hours";
    // Decide between singular and plural form of minutes
    if (minutes == 1)
        cout << " minute";
    else
        cout << " minutes";
    // Decide between singular and plural form of seconds
    if (seconds == 1)
        cout << " second";
    else
        cout << " seconds";
}
```

The if/else statements within Listing 5.12 (timeconvcond1.cpp) are responsible for printing the correct version—singular or plural—for each unit. One run of Listing 5.12 (timeconvcond1.cpp) produces