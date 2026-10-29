# 11. (Modify) Modify the function you wrote for Exercise 10 so that each test is stored in column order rather than row order.

# 12. (Program) A three-dimensional weather array for the months July and August 2011 has columns labeled by the month numbers 7 and 8. In each column, there are rows numbered 1 through 31, representing the days, and for each day, there are two ranks labeled H and L, representing the day's high and low temperatures. Use this information to write a C++ program that assigns the high and low temperatures for each element of the arrays. Then allow the user to request the following:

+   - Any day's high and low temperatures
+   - Average high and low temperatures for a given month
+   - Month and day with the highest temperature
+   - Month and day with the lowest temperature

# 7.5 Common Programming Errors

Four common errors are associated with using arrays:

+   1. Forgetting to declare the array. This error results in a compiler error message such as "invalid indirection" each time a subscripted variable is encountered in a program.
+   2. Using a subscript that references a nonexistent array element, such as declaring the array as size 20 and using a subscript value of 25. Most C++ compilers don't detect this error. However, it usually results in a runtime error that causes a program crash or results in a value with no relation to the intended element being accessed from memory. In either case, this error is usually troublesome to locate. The only solution is to make sure, by specific programming statements or by careful coding, that each subscript references a valid array element. Using symbolic constants for an array's size and the maximum subscript value helps eliminate this problem.
+   3. Not using a large enough counter value in a for loop to cycle through all the array elements. This error usually occurs when an array is initially specified as size n and there's a for loop in the program of the form for (i = 0; i < n; i++). The array size is then expanded, but the programmer forgets to change the interior for loop parameters. In practice, this error is eliminated by using the same symbolic constant for the array size declaration and loop parameter.
+   4. Forgetting to initialize the array. Although many compilers set all elements of integer and real value arrays to 0 automatically and all elements of character arrays to blanks, it's up to the programmer to make sure each array is initialized correctly before processing of array elements begins.