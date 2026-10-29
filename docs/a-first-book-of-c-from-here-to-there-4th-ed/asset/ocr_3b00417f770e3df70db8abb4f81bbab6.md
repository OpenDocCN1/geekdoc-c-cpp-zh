All the program examples of the while statement use fixed-count loops because the tested condition is a counter that checks for a fixed number of repetitions. In a variation on the fixed-count loop, the counter isn’t incremented by 1 each time through the loop but by some other value. For example, suppose you have the task of producing a Celsius-to-Fahrenheit temperature conversion table. Fahrenheit temperatures corresponding to Celsius temperatures from 5 to 50 degrees are to be displayed in increments of 5 degrees, which can be done with this series of statements:

```
celsius = 5;      // starting Celsius value
while (celsius <= 50)
{
    fahren = (9.0/5.0) * celsius + 32.0;
    cout << setw(4) << celsius
         << setw(13) << fahren << endl;
    celsius = celsius + 5;
}
```

As before, the while statement consists of everything from the word while through the compound statement’s closing brace. Before the program enters the while loop, you must make sure a value is assigned to the counter being evaluated, and there’s a statement to alter the counter’s value in the loop (in increments of 5) to ensure an exit from the while loop. Program 5.4 illustrates using similar code in a complete program.

# Program 5.4

```
#include <iostream>
#include <iomanip>
using namespace std;

// a program to convert Celsius to Fahrenheit
int main()
{
    const int MAXCELSIUS = 50;
    const int STARTVAL = 5;
    const int STEPSIZE = 5;
    int celsius;
    double fahren;

    cout << "DEGREES    DEGREES\n"
         << "CELSIUS    FAHRENHEIT\n"
         << "-------    ---------\n";

    celsius = STARTVAL;
```