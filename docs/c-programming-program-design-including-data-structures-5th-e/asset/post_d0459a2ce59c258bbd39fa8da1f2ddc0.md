
received, and the percentage of the total votes received by the candidate. Your program should also output the winner of the election. A sample output is:

| Candidate | Votes Received | % of Total Votes |
|:---|---:|---:|
| Johnson | 5000 | 25.91 |
| Miller | 4000 | 20.73 |
| Duffy | 6000 | 31.09 |
| Robinson | 2500 | 12.95 |
| Ashtony | 1800 | 9.33 |
| Total | 19300 |  |

The Winner of the Election is Duffy.

- 8. Consider the following function `main`:

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

    - a. Write the definition of the function setZero that initializes any one-dimensional array of type `int` to 0.
    - b. Write the definition of the function inputArray that prompts the user to input 20 numbers and stores the numbers into alpha.
    - c. Write the definition of the function doubleArray that initializes the elements of beta to two times the corresponding elements in alpha. Make sure that you prevent the function from modifying the elements of alpha.
    - d. Write the definition of the function copyGamma that sets the elements of the first row of inStock to gamma and the remaining rows of inStock to three times the previous row of inStock. Make sure that you prevent the function from modifying the elements of gamma.
    - e. Write the definition of the function copyAlphaBeta that stores alpha into the first five rows of inStock and beta into the last five rows of inStock. Make sure that you prevent the function from modifying the elements of alpha and beta.
    - f. Write the definition of the function printArray that prints any one-dimensional array of type `int`. Print 15 elements per line.
    - g. Write the definition of the function `setInStock` that prompts the user to input the elements for the first column of `inStock`. The function should then set the elements in the remaining columns to two times the corresponding element in the previous column, minus the corresponding element in `delta`.
    - h. Write C++ statements that call each of the functions in parts a through g.
    - i. Write a C++ program that tests the function `main` and the functions discussed in parts a through g. (Add additional functions, such as printing a two-dimensional array, as needed.)

- 9. Write a program that uses a two-dimensional array to store the highest and lowest temperatures for each month of the year. The program should output the average high, average low, and the highest and lowest temperatures for the year. Your program must consist of the following functions:

    - a. Function `getData`: This function reads and stores data in the two-dimensional array.
    - b. Function `averageHigh`: This function calculates and returns the average high temperature for the year.
    - c. Function `averageLow`: This function calculates and returns the average low temperature for the year.
    - d. Function `indexHighTemp`: This function returns the index of the highest high temperature in the array.
    - e. Function `indexLowTemp`: This function returns the index of the lowest low temperature in the array.

    (These functions must all have the appropriate parameters.)

- 10. Programming Exercise 8 in Chapter 6 asks you to find the mean and standard deviation of five numbers. Extend this programming exercise to find the mean and standard deviation of up to 100 numbers. Suppose that the mean (average) of n numbers x₁, x₂, …, xₙ is x̄. Then, the standard deviation of these numbers is:

    $$s = \sqrt{\frac{(x_1-x̄)^2+(x_2-x̄)^2+\cdots+(x_i-x̄)^2+\cdots+(x_n-x̄)^2}{n}}$$

- 11. **(Adding Large Integers)** In C++, the largest `int` value is 2147483647. So, an integer larger than this cannot be stored and processed as an integer. Similarly, if the sum or product of two positive integers is greater than 2147483647, the result will be incorrect. One way to store and manipulate large integers is to store each individual digit of the number in an array. Write a program that inputs two positive integers of, at most, 20 digits and outputs the sum of the numbers. If the sum of the numbers has more than 20 digits, output the sum with an appropriate message. Your program must, at least, contain a function to read and store a number into an array and another function to output the sum of the numbers. *(Hint: Read numbers as strings and store the digits of the number in the reverse order.)*

- 12. Jason, Samantha, Ravi, Sheila, and Ankit are preparing for an upcoming marathon. Each day of the week, they run a certain number of miles and write them into a notebook. At the end of the week, they would like to know the number of miles run each day, the total miles for the week, and average miles run each day. Write a program to help them analyze their data. Your program must contain parallel arrays: an array to store the names of the runners and a two-dimensional array of five rows and seven columns to store the number of miles run by each runner each day. Furthermore, your program must contain at least the following functions: a function to read and store the runners’ names and the numbers of miles run each day; a function to find the total miles run by each runner and the average number of miles run each day; and a function to output the results. (You may assume that the input data is stored in a file and each line of data is in the following form: `runnerName milesDay1 milesDay2 milesDay3 milesDay4 milesDay5 milesDay6 milesDay7`.)

- 13. Write a program to calculate students’ average test scores and their grades. You may assume the following input data:

    ```text
    Johnson 85 83 77 91 76
    Aniston 80 90 95 93 48
    Cooper 78 81 11 90 73
    Gupta 92 83 30 69 87
    Blair 23 45 96 38 59
    Clark 60 85 45 32 67
    Kennedy 77 31 52 74 83
    Bronson 93 94 89 77 97
    Sunny 79 85 28 93 82
    Smith 85 72 49 75 63
    ```

    Use three arrays: a one-dimensional array to store the students’ names, a (parallel) two-dimensional array to store the test scores, and a parallel one-dimensional array to store grades. Your program must contain at least the following functions: a function to read and store data into two arrays, a function to calculate the average test score and grade, and a function to output the results. Have your program also output the class average.

- 14. **(Airplane Seating Assignment)** Write a program that can be used to assign seats for a commercial airplane. The airplane has 13 rows, with six seats in each row. Rows 1 and 2 are first class, rows 3 through 7 are business class, and rows 8 through 13 are economy class. Your program must prompt the user to enter the following information:

    - a. Ticket type (first class, business class, or economy class)
    - b. Desired seat

    Output the seating plan in the following form:

    |  | A | B | C | D | E | F |
    |---|---|---|---|---|---|---|
    | Row 1 | * | * | X | * | X | X |
    | Row 2 | * | * | X | X | X | X |
    | Row 3 | * | * | X | X | * | X |
    | Row 4 | X | * | X | * | X | X |
    | Row 5 | * | X | * | X | * | * |
    | Row 6 | * | X | * | * | * | X |
    | Row 7 | X | X | * | * | X | X |
    | Row 8 | * | X | * | X | X | * |
    | Row 9 | X | * | X | X | * | X |
    | Row 10 | * | X | * | X | X | X |
    | Row 11 | * | * | X | * | X | * |
    | Row 12 | * | * | X | X | * | X |
    | Row 13 | * | * | * | * | X | * |

    Here, * indicates that the seat is available; X indicates that the seat is occupied. Make this a menu-driven program; show the user’s choices and allow the user to make the appropriate choices.

In Chapter 9, you learned how to group values of the same type by using arrays. You also learned how to process data stored in an array and how to perform list operations, such as searching and sorting data.

> **NOTE** This chapter may be skipped without experiencing any discontinuity.

In this chapter, you will learn how to group related values that are of different types. C++ provides another structured data type, called a struct (some languages use the term “record”), to group related items of different types. An array is a homogeneous data structure; a struct is typically a heterogeneous data structure. The treatment of a struct in this chapter is similar to the treatment of a struct in C. A struct in this chapter, therefore, is a C-like struct. Chapter 11 introduces and discusses another structured data type, called a class.

## Records (structs)

Suppose that you want to write a program to process student data. A student record consists of, among other things, the student’s name, student ID, GPA, courses taken, and course grades. Thus, various components are associated with a student. However, these components are all of different types. For example, the student’s name is a string, and the GPA is a floating-point number. Because these components are of different types, you cannot use an array to group all of the items associated with a student. C++ provides a structured data type called struct to group items of different types. Grouping components that are related but of different types offers several advantages. For example, a single variable can pass all the components as parameters to a function.

**struct:** A collection of a fixed number of components in which the components are accessed by name. The components may be of different types.

The components of a struct are called the members of the struct. The general syntax of a struct in C++ is:

```cpp
struct structName
{
    dataType1 identifier1;
    dataType2 identifier2;
    .
    .
    .
    dataTypen identifiern;
};
```
