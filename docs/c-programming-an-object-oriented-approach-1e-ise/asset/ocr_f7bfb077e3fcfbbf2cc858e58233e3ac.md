+   1. Input
+      a. Input an integer representing the duration in seconds.
+   2. Process
+      a. Extract the number of hours that can fit in the seconds.
+      b. Extract the number of minutes that can fit in the rest of the seconds.
+      c. Find the left-over seconds.
+   3. Output
+      a. Output the duration value given in seconds.
+      b. Output the number of extracted hours.
+      c. Output the number of extracted minutes.
+      d. Output the number of left-over seconds.

# Write the Code

Now we can create the program code based on the preceding algorithm (Program 3.30).

# **Program 3.30** Change a time duration to its components

```
```cpp
/*********************************************************
 * This program changes a duration of time in seconds to hours *
 * minutes, and seconds. *
 *********************************************************/
#include <iostream>
using namespace std;

int main ( )
{
// Variables Declaration
unsigned long duration, hours, minutes, seconds;
// Prompt and Input
cout << "Enter a positive integer for the number of seconds: ";
cin >> duration;
// Processing
hours = duration / 3600L;
minutes = (duration - (hours * 3600L)) / 60L;
seconds = duration - (hours * 3600L) - (minutes * 60);
// Output
cout << "Given Duration in seconds: " << duration << endl;
cout << "Result: ";
cout << hours << " hours, ";
cout << minutes << " minutes, and ";
cout << seconds << " seconds.";
return 0;
} // End main
```
```