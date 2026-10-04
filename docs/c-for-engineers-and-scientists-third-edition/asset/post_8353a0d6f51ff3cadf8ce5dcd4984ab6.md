
```cpp
for (i = 0; i < MAXTEMPS; i++)    // Enter the temperatures
{
    cout << "Enter a temperature: ";
    cin >> temp[i];
}

for (i = 0; i < MAXTEMPS; i++)    // Print the temperatures
    cout << "temperature " << i << " is " << temp[i] << endl;

return 0;
```

A sample run of Program 7.1 follows:

```
Enter a temperature: 85
Enter a temperature: 90
Enter a temperature: 78
Enter a temperature: 75
Enter a temperature: 92

temperature 0 is 85
temperature 1 is 90
temperature 2 is 78
temperature 3 is 75
temperature 4 is 92
```

In reviewing the output of Program 7.1, pay attention to the difference between the index value displayed and the numerical value stored in the corresponding array element. The index value refers to the element's location in the array, and the subscript variable refers to the value stored in the designated location.

In addition to simply displaying the values in each array element, the elements can also be processed by referencing the desired element. For example, in Program 7.2, the value of each element is accumulated in a total, which is displayed after all array elements have been displayed.

## Program 7.2

```cpp
#include <iostream>
using namespace std;

int main() {
    const int MAXTEMPS = 5;
    int i, temp[MAXTEMPS], total = 0;

    for (i = 0; i < MAXTEMPS; i++) // Enter the temperatures
    {
        cout << "Enter a temperature: ";
        cin >> temp[i];
    }

    cout << "\nThe total of the temperatures";

    for (i = 0; i < MAXTEMPS; i++) // Display and total the temperatures
    {
        cout << " * " << temp[i];
        total = total + temp[i];
    }

    cout << " is " << total << endl;

    return 0;
}
```

A sample run of Program 7.2 follows:
Enter a temperature: 85
Enter a temperature: 90
Enter a temperature: 78
Enter a temperature: 75
Enter a temperature: 92
The total of the temperatures 85 90 78 75 92 is 420

Notice that in Program 7.2, unlike Program 7.1, only the values stored in each array element, not the index numbers, are displayed. Although the second for loop is used to accumulate the total of each element, the accumulation could also have been accomplished in the first loop for placing the statement total = total + temp[i]; after the cin statement used to enter a value. Also, the cout statement used to display the total is placed outside the second loop so that the total is displayed only once, after all values have been added to the total. If this cout statement were placed inside the for loop, five totals would be displayed, with only the last displayed containing the sum of all values.

## EXERCISES 7.1

1. (Practice) Write array declarations for the following:
- a. A list of 100 double-precision voltages
- b. A list of 50 double-precision temperatures
- c. A list of 30 characters, each representing a code
- d. A list of 100 integers
- e. A list of 32 double-precision velocities
- f. A list of 1000 double-precision distances
- g. A list of 6 integer numbers

2. (Practice) Write correct notation for the first, third, and seventh elements of the following arrays:
- a. int grades[20]
- b. double volts[10]
- c. double amps[16]
- d. int dist[15]
- e. double velocity[25]
- f. double time[100]

3. (Practice) Write input statements using cin that can be used to enter values in the first, third, and seventh elements of each array declared in Exercise 2.
- b. Write a for loop that can be used to enter values for each array declared in Exercise 2.

4. (Practice) Write output statements that can be used to display values from the first, third, and seventh elements of each array declared in Exercise 2.
- b. Write a for loop that can be used to display values for the complete array declared in Exercise 2.

5. (Check) List the elements displayed by the following following code:
- a. for (m = 1; m <= 5; m++) cout << a[m] << " ";
- b. for (k = 1; k <= 5; k++) cout << a[k] << " ";
- c. for (j = 3; j <= 10; j++) cout << b[j] << " ";
- d. for (k = 3; k <= 12; k++) cout << b[k] << " ";
- e. for (i = 2; i <= 11; i++) cout << c[i] << " ";

6. (Practice) Write a program to input the following values in an array volts: 11.95, 16.32, 12.15, 8.22, 15.98, 26.22, 13.54, 6.45, and 17.59. After the data has been entered, have your program display.
- b. Repeat Exercise 6a, after the data has been entered, have your program display in the following format:

| 11.95 | 16.32 | 12.15 |
| 8.22 | 15.98 | 26.22 |
| 13.54 | 6.45 | 17.59 |

7. (Practice) Write a program to input eight integer numbers in an array temp. As each number is input, add the numbers to a total. After all numbers are input, display the numbers and their average.

8. (Data Processing) Write a program to input 10 integers in an array max and determine the maximum value. Your program should contain only one loop, and show the maximum equal to the first element, array being input before the loop used (Hint: Set the array to input the remaining values). Repeat Exercise 8a, keeping track of both the maximum in the array and the index number for the maximum. After displaying the numbers, print these two messages (the underlines with the correct values):
> The maximum value is:
> This is element number in the list of numbers

- c. Repeat Exercise 8b, write a program to input the following integers in an array named grades: 89, 95, 72, 83, 99, 54, 86, 75, 92, 79, 82, and 73. As each number is input, add the numbers to a total. After all numbers are input, calculate the average of the numbers, and use the average to determine the deviation of each value from the average. Store each deviation in an array deviation. Each deviation is obtained as the element value less the average of all the data. Your program display each deviation with its corresponding element from the grades array.
- b. Calculate the variance of the data used in Exercise 9a. The variance is obtained by squaring each deviation and dividing the sum of the squared deviations by the number of deviations.

10. (Electrical Eng.) Write a program that specifies three one-dimensional arrays named current, resistance, and volts. Each array should be capable of holding 10 elements. Using a for loop, input values for the current and resistance arrays. The entries in the volts array are the product of the corresponding values in the current and resistance arrays (so volts[i] = current[i] * resistance[i]). After all the data has been entered, display the following output, with the appropriate value under each column heading:

Current | Resistance | Volts

## 7.2 Array Initialization

Array elements can be initialized in their declaration statements in the same manner as scalar variables, except the initializing elements must be included in braces, as shown in the following examples:

```
int temp[5] = {98, 87, 92, 75, 85};
char codes[6] = {'s', 'a', 'm', 'p', '1', 'e'};
double slopes[7] = {7.8, 6.4, 4.9, 11.2, 6.3, 5.86, 8.22};
```

Initializers are applied in the order they are written, with the first value used to initialize element 0, the second value used to initialize element 1, and so on, until all values have been used. For example, in the declaration

```cpp
int temp[5] = {98, 87, 92, 75, 85};
```

temp[0] is initialized to 98, temp[1] is initialized to 87, temp[2] is initialized to 92, temp[3] is initialized to 75, and temp[4] is initialized to 85.

Because white space is ignored in C++, initializations can be continued across multiple lines. For example, the declaration uses four lines to initialize all the array elements:

```cpp
int gallons[20] = {19, 16, 14, 19, 20, 18,
                  12, 22, 15, 18, 17,
                  16, 24, 19, 15, 18,
                      21};
```

If the number of initializes is less than the number of elements listed in square brackets, the initializers are applied starting element 0. Therefore, in the declaration

```cpp
double length[7] = {7.8, 6.4, 4.9, 11.2};
```

onlyLength[0], length[1], length[2], and length[3] are initialized with the listed values.
The other array elements are initialized to 0.

Unfortunately, there's no method of indicating repetition of an initialization value or initializing later array elements without specifying values for earlier elements.

A feature of initializers is that the array size can be omitted when initializing values are included in the declaration statement. For example, the following declaration reserves enough storage room for five elements:

```cpp
int gallons[] = {16, 12, 10, 14, 11};
```
