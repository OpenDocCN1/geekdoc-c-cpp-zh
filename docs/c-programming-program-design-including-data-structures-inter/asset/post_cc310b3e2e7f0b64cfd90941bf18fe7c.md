
```cpp
cout << endl;
for (j = 0; j < 5; j++)
{
    two[j] = 2 * one[j] - 1;
    two[j + 5] = one[4 - j] + two[j];
}

cout << "Two contains: ";
for (j = 0; j < 10; j++)
    cout << two[j] << " ";
cout << endl;

return 0;
}
```

- **27.** What is the output of the following C++ code?

```cpp
const double PI = 3.14159;
double cylinderRadii[5] = {3.5, 7.2, 10.5, 9.8, 6.5};
double cylinderHeights[5] = {10.7, 6.5, 12.0, 10.5, 8.0};
double cylinderVolumes[5];

cout << fixed << showpoint << setprecision(2);

for (int i = 0; i < 5; i++)
    cylinderVolumes[i] = 2 * PI * cylinderRadii[i]
                         * cylinderHeights[i];

for (int i = 0; i < 5; i++)
    cout << (i + 1) << " " << cylinderRadii[i] << " "
         << cylinderHeights[i] << " " << cylinderVolumes[i] << endl;
```

- **28.** When an array is passed as an actual parameter to a function, what is actually being passed?

- **29.** In C++, as an actual parameter, can an array be passed by value?

- **30.** Sort the following list using the selection sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop.

  6, 45, 10, 25, 58, 2, 50, 30, 86

- **31.** Sort the following list using the selection sort algorithm as discussed in this chapter. Show the list after each iteration of the outer for loop.

  36, 55, 17, 35, 63, 85, 12, 48, 3, 66

- **32.** Given the declaration:

  ```cpp
  char string15[16];
  ```

  Mark the following statements as valid or invalid. If a statement is invalid, explain why.

  - a. `strcpy(string15, "Hello there");`
  - b. `strlen(string15);`
  - c. `string15 = "Jacksonville";`

- **36.** Assume the following declarations:

  ```cpp
  char name[21];
  char yourName[21];
  char studentName[31];
  ```

  Mark the following statements as valid or invalid. If a statement is invalid, explain why.

  - a. `cin >> name;`
  - b. `cout << studentName;`
  - c. `yourName[0] = '\0';`
  - d. `yourName = studentName;`
  - e.
    ```cpp
    if (yourName == name)
        studentName = name;
    ```
  - f. `int x = strcmp(yourName, studentName);`
  - g. `strcpy(studentName, name);`
  - h.
    ```cpp
    for (int j = 0; j < 21; j++)
        cout << name[j];
    ```

- **37.** Define a two-dimensional array named `temp` of three rows and four columns of type `int` such that the first row is initialized to 6, 8, 12, 9; the second row is initialized to 17, 5, 10, 6; and the third row is initialized to 14, 13, 16, 20.

- **38.** Suppose that array `temp` is as defined in Exercise 37. Write C++ statements to accomplish the following:

  - a. Output the contents of the first row and first column element of `temp`.
  - b. Output the contents of the first row and last column element of `temp`.
  - c. Output the contents of the last row and first column element of `temp`.
  - d. Output the contents of the last row and last column element of `temp`.

- **39.** Consider the following declarations:

  ```cpp
  const int CAR_TYPES = 5;
  const int COLOR_TYPES = 6;

  double sales[CAR_TYPES][COLOR_TYPES];
  ```

  - a. How many components does the array `sales` have?
  - b. What is the number of rows in the array `sales`?
  - c. What is the number of columns in the array `sales`?
  - d. To sum the sales by `CAR_TYPES`, what kind of processing is required?
  - e. To sum the sales by `COLOR_TYPES`, what kind of processing is required?

- **40.** Write C++ statements that do the following:

  - a. Declare an array `alpha` of 10 rows and 20 columns of type `int`.
  - b. Initialize the array `alpha` to 0.
  - c. Store 1 in the first row and 2 in the remaining rows.
  - d. Store 5 in the first column, and make sure that the value in each subsequent column is twice the value in the previous column.
  - e. Print the array `alpha` one row per line.
  - f. Print the array `alpha` one column per line.

- **41.** Consider the following declaration:

  ```cpp
  int beta[3][3];
  ```

  What is stored in `beta` after each of the following statements executes?

  - a.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 0;
    ```
  - b.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i + j;
    ```
  - c.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = i * j;
    ```
  - d.
    ```cpp
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            beta[i][j] = 2 * (i + j) % 4;
    ```

- **42.** Suppose that you have the following declarations:

  ```cpp
  int times[30][7];
  int speed[15][7];
  int trees[100][7];
  int students[50][7];
  ```

  - a. Write the definition of the function `print` that can be used to output the contents of these arrays.
  - b. Write the C++ statements that call the function `print` to output the contents of the arrays `times`, `speed`, `trees`, and `students`.

## PROGRAMMING EXERCISES

- **1.** Write a C++ program that declares an array `alpha` of 50 components of type `double`. Initialize the array so that the first 25 components are equal to the square of the index variable, and the last 25 components are equal to three times the index variable. Output the array so that 10 elements per line are printed.
- **2.** Write a C++ function, `smallestIndex`, that takes as parameters an `int` array and its size and returns the index of the first occurrence of the smallest element in the array. Also, write a program to test your function.
- **3.** Write a C++ function, `largestIndex`, that takes as parameters an `int` array and its size and returns the index of the last occurrence of the largest element in the array. Also, write a program to test your function.

- **8.** Consider the following function `main`:

  ```cpp
  int main()
  {
      int inStock[10][4];
      int alpha[20];
      int beta[20];
      int gamma[4] = {11, 13, 15, 17};
      int delta[10] = {3, 5, 2, 6, 10, 9, 7, 11, 1, 8};

      .
      .
      .
  }
  ```

  - a. Write the definition of the function `setZero` that initializes any one-dimensional array of type `int` to 0.
  - b. Write the definition of the function `inputArray` that prompts the user to input 20 numbers and stores the numbers into `alpha`.
  - c. Write the definition of the function `doubleArray` that initializes the elements of `beta` to two times the corresponding elements in `alpha`. Make sure that you prevent the function from modifying the elements of `alpha`.
  - d. Write the definition of the function `copyGamma` that sets the elements of the first row of `inStock` to `gamma` and the remaining rows of `inStock` to three times the previous row of `inStock`. Make sure that you prevent the function from modifying the elements of `gamma`.
  - e. Write the definition of the function `copyAlphaBeta` that stores `alpha` into the first five rows of `inStock` and `beta` into the last five rows of `inStock`. Make sure that you prevent the function from modifying the elements of `alpha` and `beta`.
  - f. Write the definition of the function `printArray` that prints any one-dimensional array of type `int`. Print 15 elements per line.
  - g. Write the definition of the function `setInStock` that prompts the user to input the elements for the first column of `inStock`. The function should then set the elements in the remaining columns to two times the corresponding element in the previous column, minus the corresponding element in `delta`.
  - h. Write C++ statements that call each of the functions in parts a through g.
  - i. Write a C++ program that tests the function `main` and the functions discussed in parts a through g. (Add additional functions, such as printing a two-dimensional array, as needed.)

- **9.** Write a program that uses a two-dimensional array to store the highest and lowest temperatures for each month of the year. The program should output the average high, average low, and the highest and lowest temperatures for the year. Your program must consist of the following functions:

  - a. **Function `getData`:** This function reads and stores data in the two-dimensional array.
  - b. **Function `averageHigh`:** This function calculates and returns the average high temperature for the year.
  - c. **Function `averageLow`:** This function calculates and returns the average low temperature for the year.
  - d. **Function `indexHighTemp`:** This function returns the index of the highest high temperature in the array.
  - e. **Function `indexLowTemp`:** This function returns the index of the lowest low temperature in the array.

  *(These functions must all have the appropriate parameters.)*

- **10.** Programming Exercise 10 in Chapter 6 asks you to find the mean and standard deviation of five numbers. Extend this programming exercise to find the mean and standard deviation of up to 100 numbers. Suppose that the mean (average) of *n* numbers *x₁, x₂, ..., xₙ* is *x̄*. Then, the standard deviation of these numbers is:

  $$s = \sqrt{\frac{(x_1 - \bar{x})^2 + (x_2 - \bar{x})^2 + \cdots + (x_i - \bar{x})^2 + \cdots + (x_n - \bar{x})^2}{n}}$$

- **11. (Adding Large Integers)** In C++, the largest `int` value is 2147483647. So, an integer larger than this cannot be stored and processed as an integer. Similarly, if the sum or product of two positive integers is greater than 2147483647, the result will be incorrect. One way to store and manipulate large integers is to store each individual digit of the number in an array. Write a program that inputs two positive integers of, at most, 20 digits and outputs the sum of the numbers. If the sum of the numbers has more than 20 digits, output the sum with an appropriate message. Your program must, at least, contain a function to read or store a number into an array and another function to output the sum of the numbers. *(Hint: Read numbers as strings and store the digits of the number in the reverse order.)*

- **12.** Jason, Samantha, Ravi, Sheila, and Ankit are preparing for an upcoming marathon. Each day of the week, they run a certain number of miles and write them into a notebook. At the end of the week, they would like to know the number of miles run each day, the total miles for the week, and average miles run each day. Write a program to help them analyze their data. Your program must contain parallel arrays: an array to store the names of the runners and a two-dimensional array of five rows and seven columns to store the number of miles run by each runner each day. Furthermore, your program must contain at least the following functions: a function to read and store the runners’ names and the numbers of miles run each day; a function to find the total miles run by each runner and the average number
