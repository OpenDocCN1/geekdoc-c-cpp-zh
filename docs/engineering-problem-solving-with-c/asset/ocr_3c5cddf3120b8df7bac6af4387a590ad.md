```
int main()
{
// Declare objects.
int numEngines, numTrials;
ifstream dataIn;

//Open input file.
dataIn.open("engine.dat");
if (dataIn.fail())
{
cerr << "could not open engine.dat";
exit(1);
}

//Input row and column size
dataIn >> numEngines >> numTrials;

//Declare constants for array declaration
const int NCOLS(numEngines);
const int NCOLS[numTrials];
double temps[NCOLS][NCOLS];

//Read temperature data and store in array.
for (int i=0; i<NCOLS; ++i)
{
for (int j=0; j<NCOLS; ++j)
dataIn >> temps[i][j];
}

dataIn.close();

//Echo input
cout << numEngines << ' ' << numTrials << endl;
for (int i=0; i<NCOLS; ++i)
{
for (int j=0; j<NCOLS; ++j)
{
cout << temps[i][j] << '\t';
} cout << endl; //end of ith row
}

return 0;
}
```

```
/*--------------------------------------
*--------------------------------------*/
```

A program trace and memory snapshot for the first iteration of program chapter8_1 is
provided below:

engine.dat.

```
3 3
335.6 339.4 421.7
299.6 332.4 340.5
320.1 329.8 339.3
```