There are advantages and disadvantages to each of the three file structures discussed. A file with a trailer signal is simple to use, but choosing a value for the trailer signal must be done carefully so that it does not contain values that could occur in the valid data. If the first record in the data file will contain the number of lines of actual data, we must know how many lines of data will be in the file before we begin to generate the file. It may not always be easy to determine the number of lines before executing the program that generates the file. The simplest file to generate is the one that contains only the valid information, with no special information at the beginning or end of the file. If the information in the file is going to be used with a plotting package, it is usually best to use this third file structure which includes only valid information.

We now present a program that is a modification of the program presented in Chapter 4 that printed a table of time, height, and velocity values for a weather balloon. In addition to generating a table of information that is displayed on the screen, we also write the time, height, and velocity information to a data file. Compare this program to program chapter4-8:

```
/**--------------------------------*/
/* Program chapter5_5 */
/* */
/* This program generates a file of height and */
/* velocity values for a weather balloon. The */
/* information is also printed in a report. */
/* */

#include <iostream> //Required for cin, cout.
#include <fstream> //Required for ofstream.
#include <iomanip> //Required for setw().
#include <cmath> //Required for pow().
#include <string> //Required for string.
using namespace std;

int main()
{
    // Declare and initialize objects.
    double initial, increment, final, time, height,
    velocity, max_time(0), max_height(0);
    int loops, itime;
    string filename;
    ofstream balloon;

    // Prompt user for name of output file.
    cout << "Enter the name of the output file";
    cin >> filename;

    // Open output file
    balloon.open(filename);

    // Get user input.
    cout << "Enter initial value for table (in hours) \\n";
    cin >> initial;
```