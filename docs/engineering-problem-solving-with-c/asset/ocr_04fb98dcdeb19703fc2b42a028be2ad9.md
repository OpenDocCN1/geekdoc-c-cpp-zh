```
const int N = 100;
int npts=0;
double y[N], temp;
string filename;
ifstream lab;

// Prompt user for file name and open data file.
cout << "Enter the name of the data file:";
cin >> filename;
lab.open(filename);
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
while(npts < N && !lab.eof() )
{
    y[npts] = temp; // Assign data value to array.
    ++npts; // Increment npts.
    lab >> temp; // Input next value
}

// Find and print the maximum value.
cout << "Maximum value: " << maxval(y,npts) << endl;

// Close file and exit program.
lab.close();

return 0;
}
```

```
/*-------------------------------------------------
* This function returns the maximum
* value in the array x with n elements.
*/
```

```
double maxval(const double x[], int n)
{
    // Declare local objects.
    double maxVal;

    // Determine maximum value in the array.
    maxVal = x[0];
    for(int k=1; k<n; ++k)
    {
        if (x[k] > maxVal)
```