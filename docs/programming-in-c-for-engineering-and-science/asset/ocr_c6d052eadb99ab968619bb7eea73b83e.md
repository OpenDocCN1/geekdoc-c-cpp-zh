```
Output: the mileage between city1 and city2
------------------------------------------------------------*/

#include <iostream>      // cin, cout, >>, <<
#include <cassert>       // assert()
using namespace std;

int main()
{
const int NUMBER_OF_CITIES = 6;
int mileageChart[NUMBER_OF_CITIES][NUMBER_OF_CITIES]
    = { {  0,  97,  90, 268, 262, 130 },    // Astroburg
        { 97,   0,  74, 337, 144, 128 },    // Bedrock
        { 90,  74,   0, 354, 174, 201 },    // Dogpatch
        { 268, 337, 354,   0, 475, 269 },    // Gotham City
        { 262, 144, 174, 475,   0, 238 },    // Metropolis
        { 130, 128, 201, 269, 238,   0 } };  // Mudville

cout << "To determine the mileage between two cities,\n"
     " enter the numbers of 2 cities from this menu:\n\n"
     "0 for Astroburg, 1 for Bedrock\n"
     "2 for Dogpatch, 3 for Gotham City\n"
     "4 for Metropolis, 5 for Mudville\n\n"
     "--> ";

int city1, city2;
cin >> city1 >> city2;

int mileage = mileageChart[city1][city2];

cout << "\nThe mileage between those 2 cities is "
     << mileage << " miles.\n";
}
```

# SAMPLE RUN:

To determine the mileage between two cities,
please enter the numbers of 2 cities from this menu:

0 for Astroburg,  1 for Bedrock
2 for Dogpatch,  3 for Gotham City
4 for Metropolis, 5 for Mudville

-->2 5

The mileage between those 2 cities is 201 miles.