```
```cpp
if(fin.fail())
{
    cerr << "error opening input file" << endl;
}
else
// Read data header and allocate memory.
fin >> npts >> time_incr;
sensor = new double[npts];

// Program continues if no exception is thrown.
cout << "Memory allocated." << endl;

// Read data into an array.
for (k=0; k<npts; ++k)
    fin >> sensor[k];

// Read window sizes from the keyboard.
cout << "Enter number of points for short-window: \n";
cin >> short_window;
cout << "Enter number of points for long-window: \n";
cin >> long_window;

// Compute power ratios and search for events.
for (k=long_window-1; k<npts; ++k)
(
    short_power = power_w(sensor, k, short_window);
    long_power = power_w(sensor, k, long_window);
    ratio = short_power/long_power;
    if (ratio > THRESHOLD)
    cout << "Possible event at " << time_incr*k
         << " seconds \n";
}

// Return memory to free-store, close file, and exit program.
delete [] sensor;
fin.close();

return 0;
}
```
```

```
```cpp
/**
*-------------------------------------------------------------*/
/*
* This function computes the average power in a
* specified window of a double array.
* double power_w(double arr[]), int length, int n)
{
    // Declare and initialize objects.
    double x[square[0];

    // Compute sum of values squared in the array x.
    for (int k=0; k<n; ++k)
```
```