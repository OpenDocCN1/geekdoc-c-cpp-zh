```
/*-------------------------------- Program chapter7_3 --------------------------------*/
/* Program chapter7_3 */
/*
/* This program reads at most 100 values from a data
/* file and determines the number of values greater
/* than the average.
/*----------------------------------------------------------*/
#include<iostream> //Required for cin, cout, cerr.
#include<fstream> //Required for fstream.
#include<string> //Required for string.
using namespace std;

int main()
{
   // Define maximum array size constant
   const int N = 100;

   // Declare and initialize objects.
   string filename;
   int count=0, numberOfValues;
   double y[N], yAve, sum=0;
   ifstream lab;

   // Prompt user for name of input file
   cout << "Enter name of the input file";
   cin >> filename;

   // Open a data file and read data into an array.
   // Compute a sum of the values.
   lab.open(filename.c_str());
   if (lab.fail())
   {
      cerr << "Error opening input file\n";
      exit(1);
   }

   // File has been opened. */
   /* Read number of data values. */
   lab >>numberOfValues;
   /* Don't exceed the bound of the array.
   if(numberOfValues > N)
   {
      cerr << "Number of data values," << numberOfValues
      << " exceeds maximum array size of " << N << endl
      << N << " values will be read." << endl;
      numberOfValues = N;
   }

   int k;
   for (k=0; k<numberOfValues; ++k)
   {
      lab >> y[k];
      sum += y[k];
   }
```