```
```cpp
// Compute average and count values that
// are greater than the average.
yAve = sum/numberOfValues;
for (int k=0; k<numberOfValues; ++k)
{
   if (y[k] > y_ave)
      count++;
}

// Print count.
cout << count << "values greater than the average \n";

// Close file and exit program.
lab.close();
return 0;
}
/*...........................................*/
```
```

If the purpose of this program had been to determine the average of the values in the data file, an array would not have been necessary. The loop to read values could read each value into the same object, adding its value to a sum before the next value is read. However, because we needed to compare each value to the average in order to count the number of values greater than the average, we chose to use an array to store the values so we could access them a second time.

Array values are printed using an offset to specify the individual value desired. For example, the following statement prints the first and last values of the array y used in the previous example:

```
```cpp
cout << "first and last array values: \n";
cout << y[0] << " " << y[numberOfValues-1] << endl;
```
```

The following loop prints all 100 values of y, one per line:

```
```cpp
cout << "y values: \n";
for (int k=0; k<N; ++k)
{
   cout << y[k] << endl;
}
```
```

Note that the values in an array must be printed one value at a time since C++ does not, in general, support aggregate output operations on arrays. When printing a large array such as this one, we probably would like to print several numbers on the same line. The following statements use the modulus operator to skip to a new line before each group of five values is printed:

```
```cpp
cout << "y values: \n";
for (int k=0; k<numberOfValues; ++k)
{
   if (k%5 == 0)
      cout << y[k] << endl;
   else
      cout << y[k] << " ";
}
cout << endl;
```
```