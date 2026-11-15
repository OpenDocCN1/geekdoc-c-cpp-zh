We now present a program that is a modification of the program presented in Chapter 4 that printed a table of time, height, and velocity values for a weather balloon. In addition to generating a table of information that is displayed on the screen, we also write the time, height, and velocity information to a data file. Compare this program to program chapter4-8:

```
/*
.................................................. */
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
 balloon.open(filename.c_str());

 // Get user input.
 cout << "Enter initial value for table (in hours) \n";
 cin >> initial;
 cout << "Enter increment between lines (in hours) \n";
 cin >> increment;
 cout << "Enter final value for table (in hours) \n";
 cin >> final;

 // Set format flags for standard output.
 cout.setf(ios::fixed);
 cout.precision(2);

 // Set format flags for file output.
 balloon.setf(ios::fixed);
 balloon.precision(2);
```