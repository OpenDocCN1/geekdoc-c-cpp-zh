```
/*-------------------------------------------------------------*/
/* Program chapter7_4                                          */
/*                                                             */
/* This program reads values from a data file and              */
/* calls a function to determine the maximum value             */
/* with a function.                                            */
/*-------------------------------------------------------------*/
#include<iostream> //Required for cin, cerr.
#include<fstream> //Required for ifstream.
#include<string> //Required for string.
using namespace std;

// Define function prototypes.
double maxval (const double x[], int n);

int main()
{
   // Declare objects.
   const int N = 100;
   int npts=0;
   double y[N], temp;
   string filename;
   ifstream lab;

   // Prompt user for file name and open data file.
   cout << " Enter the name of the data file:";
   cin >> filename;
   lab.open(filename.c_str());
   if(lab.fail())
   {
      cerr << "Error opening input file\n";
      exit(1);
   }

   // Read a data value from the file.
   lab >> temp;

   // While there is room in the array and
   // and end of file was not encountered,
   // assign the value to the array and
   // input the next value.
   while (npts < N && !lab.eof() )
   {
      y[npts] = temp; // Assign data value to array.
      ++npts; // Increment npts.
      lab >> temp; // Input next value.
   }

   // Find and print the maximum value.
   cout << "Maximum value: " << maxval(y,npts) << endl;
```