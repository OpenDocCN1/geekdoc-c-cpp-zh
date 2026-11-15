```
//Call function to input data
input2DVec(fin,temps);

//Print the average value for each column
for(int j=0; j<cols; ++j)
{
    cout << "The average value of column " << j << " is "
         << columnAvgVec(temps,j) << endl;
}
return 0;
}
```

```
/*---------------------------------------------------------------*/
/* This function reads data from an input stream and             */
/* assigns the data to the 2D vector, arr.                       */
/* Pre-conditions:                                             */
/*     The istream has been defined.                            */
/*     istream source has sufficient data.                      */
/* Post-conditions:                                             */
/*     The vector arr is filled                                 */
/* void input2DVec(istream&in,vector<vector<double> >&arr)      */
```

```
{
//Declare and initialize local objects
double val;
int rows = arr.size();    // row size
int cols = arr[0].size(); // all rows have same col size

//Fill the array
for (int i=0; i<rows; ++i)
{
    for (int j=0; j<cols; ++j)
    {
        in >> arr[i][j];
    }
}
```

```
/*---------------------------------------------------------------*/
/* This function returns the average of column colNum           */
/* double columnAvgVec(vector<vector<double> >&arr, int colNum) */
```

```
{
//Declare and initialize local objects.
double avg = 0.0;
int r = arr.size();
//Sum all values in column colNum
for(int i=0; i<r; ++i)
```