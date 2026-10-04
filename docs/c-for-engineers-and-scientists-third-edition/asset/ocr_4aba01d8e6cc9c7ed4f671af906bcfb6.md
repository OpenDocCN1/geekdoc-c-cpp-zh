# Modularity Using Functions

6. (Data Processing) Write a function named daycount() that accepts a month, day and year as its arguments; calculates an integer representing the total number of days from the turn of the century to the date that passed; and returns the calculated integer to the calling function. For this problem, assume each year has 365 days and each month has 30 days. Test your function by verifying that the date 1/100 returns a count of 1.

b. Include the daycount() function written for Exercise 6a in a working program. The main() function should correctly call daycount() and display the integer returned by the function.

7. (Data Processing) A clever and simple method of preparing to sort dates into ascending (increasing) or descending (decreasing) is to convert a date in the month/day/year into an integer using the formula date = year * 10000 + month + 100. For example, using this formula, the date 12/6/1988 converts to the integer 19881206, and the date 2/28/2010 converts to the integer 20100228. Sorting the resulting integers puts them in the correct order automatically. Using this formula, write a function named convertdays() that accepts a month, day, and year; converts the date into an integer and returns it to the caller.

b. Include the convertdays() function written for Exercise 7a in a working program. The main() function should call convertdays() correctly and display the integer returned

8. (Data Processing) Write a program that reads a key pressed on the keyboard and displays it on the screen. Use the program to determine the code for the Enter key. Write a function named ReadChar() that reads a character and ignores any succeeding characters until the Enter key is pressed. The entered character should be returned by ReadOne().

9. (Conversion) a. Write and test a C++ function named MakeMilesKmTable() to display a table of miles converted to kilometers. The arguments to the function should be the starting and stopping values of miles and the increment. The output should be a table of miles and their equivalent kilometer values. Use the relationship that 1 mile = 1.61 kilometers.

b. Modify the function written for Exercise 9a so that two columns are printed. For example, if the starting value is 1, the ending value is 20, and the increment is 1, the display should show like the following:

| Miles | Kilometers | Miles | Kilometers |
| --- | --- | --- | --- |
| 1 | 1.61 | 11 | 17.70 |
| 2 | 3.22 | 12 | 19.31 |
| .. | .. | .. | .. |
| 10 | 16.09 | 20 | 32.18 |

(Hint: Find split = {start + stop}/2. Let a loop execute from miles to split, and calculate and print one line the values of miles and kilometers for both miles and (miles - start + split + 1)).