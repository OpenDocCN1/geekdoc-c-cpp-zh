```
```cpp
{
    int quarter;
    int maxIndex = 0;

    for (quarter = 0; quarter < 4; quarter++)
        if (saleByQuarter[maxIndex] < saleByQuarter[quarter])
            maxIndex = quarter;

    outData << "Max Sale by Quarter: Quarter = "
            << maxIndex + 1
            << ", Amount = $" << saleByQuarter[maxIndex]
            << endl;
} //end maxSaleByQuarter
```
```

To make the program more flexible, we will prompt the user to specify the input and output files during its execution.

We are now ready to write the algorithm for the function main.

# Main Algorithm

+   1. Declare the variables.
+   2. Prompt the user to enter the name of the file containing the salesperson’s ID data.
+   3. Read the name of the input file.
+   4. Open the input file.
+   5. If the input file does not exist, exit the program.
+   6. Initialize the array `salesPersonList`. Call the function `initialize`.
+   7. Close the input file containing the salesperson’s ID data and clear the input stream.
+   8. Prompt the user to enter the name of the file containing the sales data.
+   9. Read the name of the input file.
+   10. Open the input file.
+   11. If the input file does not exist, exit the program.
+   12. Prompt the user to enter the name of the output file.
+   13. Read the name of the output file.
+   14. Open the output file.
+   15. To output floating-point numbers in a fixed decimal format with the decimal point and trailing zeroes, set the manipulators `fixed` and `showpoint`. Also, to output floating-point numbers to two decimal places, set the precision to two decimal places.