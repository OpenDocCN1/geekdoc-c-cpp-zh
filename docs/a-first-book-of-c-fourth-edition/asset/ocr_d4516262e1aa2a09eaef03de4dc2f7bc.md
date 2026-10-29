# Program 15.7

```
#include <iostream>
#include <cstring>
#include <cstdlib>
#include <iomanip>
using namespace std;

int main()
{
    const int MAXELS = 20;
    char string[MAXELS] = "12345";
    int num;
    double dnum;

    num = atoi(string);

    cout << "The string \"" << string << "\" as an integer number is: " << num;
    cout << "\nThis number divided by 3 is: " << num / 3 << endl;

    strcat(string, ".96");

    dnum = atof(string);

    cout << "The string \"" << string << "\" as a double number is: " << fixed << setprecision(2) << dnum;
    cout << "\nThis number divided by 3 is: " << dnum / 3 << endl;

    return 0;
}
```

# EXERCISES 15.2

1. (Practice) Determine the value of *text, *(text + 3), and *(text + 10), assuming text is an array of characters and the following has been stored in the array:

+   a. Be of good purpose
+   b. Harry Houdini was a magician
+   c. What a great movie
+   d. Oops, my bad!