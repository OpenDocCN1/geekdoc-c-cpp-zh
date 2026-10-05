# 9.4. FUNCTION EXAMPLES

In Listing 9.11 (betterinputfunc.cpp)

+   * The high and low values are specified by parameters. This makes the function more flexible since it could be used elsewhere in the program with a completely different range specified and still work correctly.

+   * The function is supposed to be called with the lower number as the first parameter and the higher number as the second parameter. The function will also accept the parameters out of order and automatically swap them to work as expected; thus,

```
num = get_int_range(20, 50);
```

will work exactly like

```
num = get_int_range(50, 20);
```

+   * The Boolean variable bad_entry is used to avoid evaluating the Boolean exception twice (once to see if the bad entry message should be printed and again to see if the loop should continue).

# 9.4.4 Better Die Rolling Simulator

```
Listing 9.12: betterdie cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

/*
* initialize_die
* Initializes the randomness of the die
*/
void initialize_die() {
    // Set the random seed value
    srand(static_cast<unsigned>(time(0)));
}

/*
* show_die(spots)
* Draws a picture of a die with number of spots
* indicated
* spots is the number of spots on the top face
*/
void show_die(int spots) {
    cout << "-----------" << endl;
    switch (spots) {
        case 1:
            cout << " | |" << endl;
            cout << " * |" << endl;
            cout << " | |" << endl;
            break;
        case 2:
            cout << " * |" << endl;
```