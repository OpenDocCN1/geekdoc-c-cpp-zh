```
```cpp
int crossings(double x[], int n);
int main()
{
    // Declare objects.
    const int MAXIMUM = 2500;
    int npts(0);
    double speech[MAXIMUM];
    string filename;
    ifstream file_1;

    // Prompt user for file name and
    // open file.
    cout << "Enter filename ";
    cin >> filename;
    file_1.open(filename);
    if (file_1.fail() )
{
        cout << "error opening file " << filename
             << endl;
        return 0;
    }

    // Read information from a data file.  *
    while (npts <= MAXIMUM-1 && file_1 >> speech[npts])
{
        npts++;
    } // end while

    // Compute and print statistics.
    cout << "Digit Statistics \n";
    cout << "Mean:       " << mean(speech,npts) << endl;
    cout << "Standard deviation: " <<
         << std_dev(speech,npts) << endl;
    cout << "Variance:   " << variance(speech,npts)
         << endl;
    cout << "Average power: " << ave_power(speech,
         << endl;
    cout << "Average magnitude: " <<
         << ave_magn(speech,npts) << endl;
    cout << "Zero crossings: " << crossings(speech,npts)
         << endl;

    // Close file and exit program.
    file_1.close();
    return 0;
}
```
```