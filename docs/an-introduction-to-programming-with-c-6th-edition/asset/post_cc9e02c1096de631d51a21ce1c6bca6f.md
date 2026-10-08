
# LAB 12-4 Desk-Check

Desk-check the Jenko Booksellers program, which is shown in Figure 12-12 in the chapter.

# LAB 12-5 Debug

Follow the instructions for starting C++ and opening the Lab12-5.cpp file. The file is contained in either the Cpp6\Chap12\Lab12-5 Project folder or the Cpp6\Chap12 folder. Debug the program.

# Summary

- A two-dimensional array resembles a table that the elements are in rows and columns. Each element has the same data type.
- You can determine the number of elements in a two-dimensional array by multiplying the number of rows by the number of its columns.
- Each element in a two-dimensional array is identified by a unique combination of subscripts. The first subscript represents the element's row location in the array, and the second subscript represents its location. You refer to each element in a two-dimensional array by the array's name and the element's subscripts, which are specified in two sets of square brackets immediately following.
- The first row subscript in a two-dimensional array is 0; the first column subscript is also 0. The last row subscript is always one less than the number of rows in the array. The last column subscript is always one less than the number of columns in the array.
- You must declare a two-dimensional array before you can use it. When declaring a two-dimensional array, you must provide the number of rows as well as the number of columns.
- After declaring a two-dimensional array, you can use an assignment statement or the extraction operator to enter data into the array.
- You need two loops to access every element in a two-dimensional array. One of the loops keeps track of row subscript. The other loop keeps track of column subscript.
- To pass a two-dimensional array to a function, you include the array's name in the statement that calls the function. The array's corresponding formal parameter in the function header must specify the formal parameter's data type and name, followed by two sets of square brackets. The first bracket contains the number of rows, and the second bracket contains the number of columns.

# Key Term

**Two-dimensional array**—an array made of rows and columns; each element has the same data type and is identified by a unique combination of two subscripts: a row subscript and a column subscript.

# Review Questions

- 1. The first element in a two-dimensional array has a row subscript of __ and a column subscript of __
  a. 0, 0
  b. 0, 1
  c. 1, 0
  d. 1, 1

- 2. Which of the following statements creates a two-dimensional array named rates that contains three rows and four columns?
  a. `int rates[3, 4] = {0};`
  b. `int rates[4, 3] = {0};`
  c. `int rates[3][4] = {0};`
  d. `int rates[4][3] = {0};`

Use the sales array to answer Review Questions 3 through 6. The array was declared using the `int sales[2][5] = {{10000, 12000, 900, 500, 20000}, {350, 600, 700, 800, 100}};`

- 3. The statement sales[1][3] = sales[1][3] + 10; will replace the number
  a. 900 with 910
  b. 500 with 510
  c. 700 with 710
  d. 800 with 810

- 4. The statement sales[0][4] = sales[0][4] - 2; will replace the number,
  a. 20000 with 900
  b. 20000 with 19998
  c. 20000 with 19100
  d. 500 with 12000

- 5. The statement cout << sales[0][3] + sales[1][3] << endl; will 
  a. display 1300
  b. display 1600
  c. display sales[0][3] + sales[1][3]
  d. result in an error

- 6. Which of the following if clauses verifies that the array subscripts stored in the row and col variables are valid for the sales array?
  a. if (sales[row][col] >= 0 && sales[row][col] < 5)
  b. if (sales[row][col] >= 0 && sales[row][col] <= 5)
  c. if (row >= 0 && row < 3 && col >= 0 && col < 6)
  d. if (row >= 0 && row <= 1 && col >= 0 && col <= 4)

# Exercises

## Pencil and Paper

1. Write the code to declare and initialize a two-dimensional double array named balances that has four rows and six columns. (The answers to TRY Exercises are located at the end of the chapter).
2. Write the code to display the contents of the balances array from Pencil Paper Exercise 1. Use two for statements to display the array, row by row. (The answers to TRY Exercises are located at the end of the chapter).
3. Rewrite the code from Pencil Paper Exercise 2 to display the array, column by column.
4. Write the code to store the number 100 in each element in the balances array from Pencil Paper Exercise 1. Use two for statements.
5. Rewrite the code from Pencil Paper Exercise 4 using two while statements.
6. Rewrite the code from Pencil Paper Exercise 4 using the while statement in the outer loop and the while statement in the nested loop.
7. Write the statement to assign the C++ keyword true to the variable located in the third row, first column of bool array.

## CHAPTER 12 Two-Dimensional Arrays

8. Write the code to display the sum of the numbers stored in the following elements in a two-dimensional double array named sales: the first row, first column; the second row, third column; and the third row, fourth column.
9. Write the code to subtract 1 from each element in a two-dimensional int array named quantities. The array has 10 rows and 25 columns. Use two for statements.
10. Rewrite the code from Pencil Paper Exercise 9 using two while statements.
11. Write the code to find the square root of the number stored in the first row, third column in a two-dimensional double array named mathNumbers. Display the result on the screen.
12. Write the code to display the largest number in the first column of a two-dimensional int array named orders. The array has five rows and two columns. Use the for statement.
13. Rewrite the code from Pencil Paper Exercise 12 using the while statement.
14. The numbers array is a two-dimensional int array that contains three rows and five columns. The following statement should call the void calTotal function passing the numbers array: `calTotal(numbers[5])`. Correct the statement.

## Computer

15. If necessary, create a new project named Try15 Project. Enter the C++ instructions from Figure 12-9 to a source file named Try15.cpp. Change the filename in the first comment to Try15.cpp. Save and run the program using the data shown in Figure 12-10. Change the for loops that enter the data into the array to while loops. Change the loops that display the array's contents to while loops and then run the program. (The answers to TRY Exercises are located at the end of the chapter).
16. If necessary, create a new project named Try16 Project. Enter the C++ instructions from Figure 12-22 into a source file named Try16.cpp. Change the filename in the first comment to Try16.cpp. Save and then run the program. As mentioned in the chapter, when you pass a two-dimensional array to a function, the first set of square brackets in its corresponding formal parameter can be empty. Remove the number 4 from the first formal parameter in the function prototype and function header. The main function will need to pass two actual arguments to the displayArray function: the array and the number of rows in the array. Make the appropriate modifications to the displayArray function prototype, function header, and function call. Also modify the outer loop for the displayArray function so it uses the number of rows passed to the function rather than the literal 4. (The answers to TRY Exercises are located at the end of the chapter).

- 17. If necessary, create a new project named ModifyThis17 Project. Enter the C++ instructions from Figure 12-12 to a source file named ModifyThis17.cpp. Change the filename in the first comment. Save and run the program. Jenko Booksellers and hardcover bookstores are $60.85 and $246.85, respectively. Add the new sales information to the array, and then modify the program. Save and run the program.
- 18. If necessary, create a new project named ModifyThis18 Project. Enter the C++ instructions from Figure 12-17 to a source file named ModifyThis18.cpp. Change the filename in the first comment. Save and run the program. Test the program using the two pay codes: 6 and 5. Enter -1 to stop the program. Add a new pay code and rate to the array. The new pay code is 11, and its corresponding rate is $23. Make the appropriate modifications to the code. Save and run the program. Test the program using the three pay codes: 6, 5, and 11. Enter -1 to stop the program.
- 19. Follow the instructions for starting C++ and opening the Introductory19.cpp file. The file is contained in either the Cpp6Chap12:Introductory19 Project folder or the Cpp6Chap12 folder. The program should calculate the average of the values stored in the rates array. It should then display the average on the screen with two decimal places. Complete the program using the for statement. Save and run the program.
- 20. Follow the instructions for starting C++ and opening the Introductory20.cpp file. The file is contained in either the Cpp6Chap12:Introductory20 Project folder or the Cpp6Chap12 folder. The program should display the contents of the two-dimensional array, column by column and row by row. Complete the program using a while statement and a for statement in the nested loops. Save and run the program.
- 21. If necessary, create a new project named Intermediate21 Project. Also create a new source file, two-column int array named temperatures. The program should prompt the user to enter the highest and lowest temperatures for seven days. Store the highest temperatures in the first column of the array. Store the lowest temperatures in the second column. The program should display the average high temperature and the average low temperature. Display the average temperatures with one decimal place. Save and run the program. Test the program using the data shown in Figure 12-27.
