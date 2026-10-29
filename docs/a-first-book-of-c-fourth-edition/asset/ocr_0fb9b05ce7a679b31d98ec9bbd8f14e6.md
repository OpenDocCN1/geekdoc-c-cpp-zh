The initialization of the seasons array can also be incorporated into the definition of the array, as follows:

```
char *seasons[4] = {"Winter",
    "Spring",
    "Summer",
    "Fall"};
```

This declaration both creates an array of pointers and initializes the pointers with appropriate addresses. After addresses have been assigned to the pointers, each pointer can be used to access its corresponding string. Program 15.8 uses the seasons array to display each season by using a for loop.

# Program 15.8

```
#include <iostream>
using namespace std;
int main()
{
    const int NUMSEASONS = 4;
    int n;
    char *seasons[] = {"Winter",
        "Spring",
        "Summer",
        "Fall"};

    for( n = 0; n < NUMSEASONS; n++)
        cout << "\n\tThe season is " << seasons[n];

    return 0;
}
```

The output of Program 15.8 is as follows:

```
The season is Winter
The season is Spring
The season is Summer
The season is Fall
```

The advantage of using a list of pointers is that logical groups of data headings can be collected and accessed with one array name. For example, the months in a year can be grouped in one array called months, and the days in a week can be grouped in an array called days. The grouping of like headings enables the programmer to access and print a corresponding heading simply by specifying the heading's correct position in the array. Program 15.9 uses the seasons array to identify and display the season corresponding to a user-entered month.