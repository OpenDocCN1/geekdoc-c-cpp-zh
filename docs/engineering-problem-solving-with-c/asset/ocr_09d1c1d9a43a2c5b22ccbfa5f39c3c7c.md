```
{
 cout << y[k] << endl;
}
```

Note that the values in an array must be printed one value at a time since C++ does not, in general, support aggregate output operations on arrays. When printing a large array such as this one, we probably would like to print several numbers on the same line. The following statements use the modulus operator to skip to a new line before each group of five values is printed:

```
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

Statements similar to the ones illustrated here can also be used to write array values to a data file. For example, the following statement will print the value of y[k] on a line in a data file using the file stream sensor:

```
sensor << y[k] << endl;
```

Since the endl manipulator is included, the next value written to the file will be on a new line.

# Modify 7.1

+   1. Rewrite program chapter7_4 without using an array. Hint: calculate the average, then close and reopen the input file and count the number of values greater than the average. Did you need to clear the eofbit before reading the file for a second time?

+   2. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
 char greeting[] = "HelloWorld";
 int numbers[] = {1,2,3,4,5};
 cout << greeting << endl;
 cout << numbers << endl;
 return 0;
}
```

Compile and run this program. Explain the output.