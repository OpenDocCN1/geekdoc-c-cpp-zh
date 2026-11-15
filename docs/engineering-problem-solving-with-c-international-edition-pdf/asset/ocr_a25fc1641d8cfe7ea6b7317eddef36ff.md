# Specified Number of Records

Assume that the first record in the sensor data file contains an integer that specifies the number of records of sensor information that follow. Each of the following lines contains a time and sensor reading:

```
sensor1.dat
10
0.0 132.5
0.1 147.2
0.2 148.3
0.3 157.3
0.4 163.2
0.5 158.2
0.6 169.3
0.7 148.2
0.8 137.6
0.9 135.9
```

The process of first reading the number of data points and then using that to specify the number of times to read data and accumulate information is easily described using a variable-controlled loop. In the program shown next, the first actual data value is used to initialize the max and min values. If we set the min value initially to zero and all the sensor values were greater than zero, the program would print the erroneous value of zero for the minimum sensor reading. The program for this solution is as follows:

![](bbox=[0.14, 0.44, 0.2, 0.5])

```
/*....................................................................*/
/* Program chapter5_2 ..... */
/* ..... */
/* This program generates a summary report from */
/* a data file that has the number of data points */
/* in the first record. ..... */
/*....................................................................*/
#include <iostream> //Required for cerr, cin, cout.
#include <fstream> //Required for ifstream, ofstream.
#include <string> //Required for string.
using namespace std;
int main()
{
// Declare and initialize objects.
int num_data_pts, k;
double time, motion, sum=0, max, min;
string filename;
ifstream sensor1;
ofstream report;
// Prompt user for name of input file.
cout << "Enter the name of the input file";
cin >> filename;
// Open file and read the number of data points.
```