The report printed by this program using the sensor2.txt file is exactly the same as the report printed using the sensor1.txt file.

End-of-file indicator

# End-of-file.

A special end-of-file indicator is inserted at the end of every data file; the feof function in the Standard C library can be used to detect when this indicator has been reached in a data file. The fscanf function can also be used to detect when the end of the data file has been read in a file. Recall that the fscanf function returns the number of values successfully read each time that it is executed. Thus, if the function returns a value that is different from the number of values that it was supposed to read, then the end of the data file has been reached, or there are errors in the information in the data file. If the information in the data file is valid, then the fscanf function can be used to determine when the end of the data file is reached. Consider the following statements:

```
while ((fscanf(data, "%lf", &x)) == 1)
{
    count++;
    sum += x;
}
ave = sum/count;
```

The fscanf function attempts to read a value for x from a data file. If a value is read, the function returns a value of 1, and the statements within the loop are executed. If the end of the data file is reached, there is no more data; thus, the function does not return a value of 1, and control passes to the statement following the while loop.

We now assume that the data file sensor3.txt contains the same information as the sensor2.txt file, except it does not include the trailer signal. In the following pseudocode and program, we read and accumulate information until we reach the end of the data file:

# Refinement in Pseudocode

```
main: set sum to zero
    set number of points to 0
    if file cannot be opened
        print error message
    else
        while not at the end of the file
            read time, motion
            add 1 to the number of points
            if k=1
                set max to motion
                set min to motion
            add motion to sum
            if motion > max
                set max to motion
            if motion < min
                set min to motion
        set average to sum/number of data points
        print average, max, min
```