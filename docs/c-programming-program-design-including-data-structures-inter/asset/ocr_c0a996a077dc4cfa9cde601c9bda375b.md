8. Consider the following function main:

```
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
```

+   a. Write the definition of the function `setZero` that initializes any one-dimensional array of type `int` to 0.

+   b. Write the definition of the function `inputArray` that prompts the user to input 20 numbers and stores the numbers into `alpha`.

+   c. Write the definition of the function `doubleArray` that initializes the elements of `beta` to two times the corresponding elements in `alpha`. Make sure that you prevent the function from modifying the elements of `alpha`.

+   d. Write the definition of the function `copyGamma` that sets the elements of the first row of `inStock` to `gamma` and the remaining rows of `inStock` to three times the previous row of `inStock`. Make sure that you prevent the function from modifying the elements of `gamma`.

+   e. Write the definition of the function `copyAlphaBeta` that stores `alpha` into the first five rows of `inStock` and `beta` into the last five rows of `inStock`. Make sure that you prevent the function from modifying the elements of `alpha` and `beta`.

+   f. Write the definition of the function `printArray` that prints any one-dimensional array of type `int`. Print 15 elements per line.

+   g. Write the definition of the function `setInStock` that prompts the user to input the elements for the first column of `inStock`. The function should then set the elements in the remaining columns to two times the corresponding element in the previous column, minus the corresponding element in `delta`.

+   h. Write C++ statements that call each of the functions in parts a through g.

+   i. Write a C++ program that tests the function `main` and the functions discussed in parts a through g. (Add additional functions, such as printing a two-dimensional array, as needed.)

9. Write a program that uses a two-dimensional array to store the highest and lowest temperatures for each month of the year. The program should output the average high, average low, and the highest and lowest temperatures for the year. Your program must consist of the following functions: