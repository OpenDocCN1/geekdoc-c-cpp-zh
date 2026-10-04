
## Chapter 7 405
## Case Study: Statistical Analysis

To make sure you understand the required processing, do a hand calculation, assuming
average and standard deviation of the following 10 grades are to be determined: 98, 82,
67, 54, 78, 83, 95, 76, 68, 63. Here's the average of these grades:

Average = (98 + 82 + 67 + 54 + 78 + 83 + 95 + 76 + 68)/10) = 76.4

The standard deviation is calculated by first determining the sum of the squared
deviations, and then dividing the resulting sum by 10 and taking its square root, as shown:

```
Sum of squared deviations = (98-76.4)² + (82-76.4)² + (67-76.4)² + (54-76.4)² + (78-76.4)² + (83-76.4)² + (95-76.4)² + (76-76.4)² + (68-76.4)² + (63-76.4)² = 1730.40007
```

Standard deviation = √1730.40007/10 = √13.154407

Having specified the algorithm for both functions, you're in a position to code them.

## Step 3 Code the Solution

When writing functions, concentrating on the function header is helpful. You can then
write the function to process the input parameters correctly to produce the desired
Results. The averaging function findAvg() and selecting the parameter names
nums for the passed array and numel for the number of elements, the function header
comes the following:

```
double findAvg(int nums[], int numel)
```

This header defines the definition of the averaging function and allows
the function to accept an array of integer values and an integer number. As shown by the hand
calculation, the average of a set of integer numbers is a floating-point value; therefore,
the function is defined as returning a floating-point value. The function body calculates
an average as described by the algorithm developed earlier. The completed findAvg()
it is as follows:

```
double findAvg(int nums[], int numel)
{
    int i;
    double sums = 0.0;
    for (i = 0; i < numel; i++) // calculate the sum of the grades
        sums = sums + nums[i];

    return (sums / numel); // calculate and return the average
}
```

The function body contains a for loop to sum the numbers. Notice also that the
termination value of the loop counter for the for loop is numel, the number of integers in
the array passed to the function through the parameter list. Using this parameter gives the

## 406 Arrays

function its generality and allows it to be used for input arrays of any size. For example,
calling the function with the statement

```
findAvg(values,10)
```

tells the function that numel is 10 and the values array consists of 10 values, whereas the
statement

```
findAvg(values,1000)
```

tells findAvg() that numel is 1000 and the values array consists of 1000 numbers. In
both calls, the actual argument value corresponds to the parameter nums
in the findAvg() function.

Using similar reasoning as for the averaging function, the function header for the standard
deviation function, named stdDev(), is as follows:

```
double stdDev(int nums[], int numel, double av)
```

This header begins the definition of the stdDev() function. It defines the function as
returning a double-precision value and accepting an array of integers, an integer value, and
double-precision value as inputs to the function. The body of the stdDev() function must
calculate the standard deviation as described in the algorithm. This is the complete standard
deviation: function:

```
{
  int i;
  double sumdevs = 0.0;

  for (i = 0; i < numel; i++)
    sumdevs = sumdevs + pow(nums[i] - av,2.0);
}
```

## Step 4 Test and Correct the Program

Testing a program's function requires writing a main() function to call the function you're
testing and display the returned results. Program 7.10 uses a main() function to set up a
grade array with the data previously used in the hand calculation and to call the
findAvg() and stdDev() functions.

## Chapter 7 407
## Case Study: Statistical Analysis

## Program 7.10

```
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

double findAvg(int nums[], int numel);                    // function prototype
double stdDev(int nums[], int numel, double av);    // function prototype

int main()
{
    const int NUMELS = 10;

    int values[NUMELS] = {98, 82, 67, 54, 78, 83, 95, 76, 68, 63};
    double average, sDev;
    average = findAvg(values, NUMELS); // call the function
    sDev = stdDev(values, average); // call the function
    cout << "The average of the numbers is "
         << setw(5) << setiosflags(ios::showpoint)
         << setprecision(2) << average << endl;

    cout << "The standard deviation of the numbers is "
         << setw(5) << setiosflags(ios::showpoint)
         << setprecision(2) << sDev << endl;
    return 0;
}

double findAvg(int nums[], int numel)
{
    int i;
    double sums = 0.0;

    for (i = 0; i < numel; i++) // calculate the sum of the grades
        sums = sums + nums[i];

    return (sums / numel); // calculate and return the average
}
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_426_0.png)

## 408 Arrays

```
double stdDev(int nums[], int numel, double av)
{
    int i;
    double sumdevs = 0.0;
    for (i = 0; i < numel; i++)
        sumdevs = sumdevs + pow(nums[i] - av, 2.0);
    return(sqrt(sumdevs/numel));
}
```

A test run of Program 7.10 produced the following display:
The average of the numbers is 76.40
The standard deviation of the numbers is 13.15

Although this result agrees with the previous hand calculation, testing isn't complete without verifying the calculation at the boundary points. For this program, the test consists of checking the calculation with all the same values, as all 0s and all 100s. Another simple test is to use five 0s and five 100s. You can try these tests on your own as an exercise.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_427_0.png)

## EXERCISES 7.5

- 1. (Practice) Enter and run Program 7.10.
- 2. (Practice) Run Program 7.10 to determine the average and standard deviation of the following list: 68, 72, 78, 69, 85, 95, 75, 77, 82, 84, 91.
- 3. (List Maintenance) A common problem is maintaining a list in numerical order. For example, inventory numbers are typically kept in numerical order, but telephone lists are kept in alphabetical order. For this exercise, write a function that inserts a three-digit part into a list. The list is maintained in numerical order, and duplicate numbers aren't allowed. Allocate a maximum list size of 100, and use a sentinel value of 9999 to indicate the end of the list. For example, if the current list contains nine numbers, the 10th position in the list contains the sentinel value. Figure 7.12 shows the insertion process for an original list of nine numbers, using the following process-algorithm:

```
Determine where in the list the new part should be placed
This is done by comparing the new part number to each value in the current list until a match is found, a part number larger than the new part is located, or the end of the list is encountered
If the new part number matches an existing number,
display a message that the part exists
Else
To make room for the new element in the array, move each element down. This is done by starting from the sentinel value and copying each item down until the desired position is vacated
Insert the new part number in the vacated position
endif
```

| 109 | 122 | 136 | 144 | 157 | 162 | 178 | 185 | 192 | 9999 |
(a) Original list

| 109 | 122 | 136 | 142 | 144 | 157 | 162 | 178 | 185 | 192 | 9999 |
(b) Elements copied to make room for the new part

Figure 7.12 Updating an ordered list of part numbers

- 4. (List Maintenance) a. Write a complete C++ program that can be used to update an ordered list of numbers. Use the list of numbers shown in Figure 7.12 to test that your program is working correctly.
b. Test the program you wrote for Exercise 4a, using a new part number of 86 with the list of numbers shown in Figure 7.12. This test should place this new part number at the beginning of the existing list.
c. Test the program you wrote for Exercise 4a, using a part number of 200 with the list of numbers shown in Figure 7.12. This test should place this new part number at the end of the existing list.
- 5. (List Maintenance) a. Determine an algorithm for deleting an entry from an ordered list of numbers.
b. Write a function delete(), which uses the algorithm determined in Exercise 5a, to delete a part number from the list shown in Figure 7.12.
