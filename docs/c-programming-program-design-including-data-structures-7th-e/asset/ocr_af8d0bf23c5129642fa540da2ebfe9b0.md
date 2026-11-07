+   c. After the program executes, what are the contents of the file `outFile.dat` if this file contained 100 numbers before the program executed?

+   d. What would happen if the file `outFile.dat` did not exist before the program executed?

24. Suppose that `infile` is an `ifstream` variable and it is associated with the file that contains the following data: `27306 Savings 7503.35`. Write the C++ statement(s) that reads and stores the first input in the `int` variable `acctNumber`, the second input in the `string` variable `accountType`, and the third input in the `double` variable `balance`. (10)

25. Suppose that you have the following statements: (10)

```
ofstream outfile;
double distance = 375;
double speed = 58;
double travelTime;
```

Write C++ statements to do the following:

+   a. Open the file `travel.dat` using the variable `outfile`.
+   
+   b. Write the statement to format your output to two decimal places in fixed form.
+   
+   c. Write the values of the variables `day`, `distance`, and `speed` in the file `travel.dat`.
+   
+   d. Calculate and write the `travelTime` in the file `travel.dat`.
+   
+   e. Which header files are needed to process the information in (a) to (d)?

# PROGRAMMING EXERCISES

1. Consider the following incomplete C++ program:

```
#include <iostream>

int main()
{
    ...
}
```

+   a. Write a statement that includes the header files `fstream`, `string`, and `iomanip` in this program.
+   
+   b. Write statements that declare `inFile` to be an `ifstream` variable and `outFile` to be an `ofstream` variable.
+   
+   c. The program will read data from the file `inData.txt` and write output to the file `outData.txt`. Write statements to open both of these files, associate `inFile` with `inData.txt`, and associate `outFile` with `outData.txt`.