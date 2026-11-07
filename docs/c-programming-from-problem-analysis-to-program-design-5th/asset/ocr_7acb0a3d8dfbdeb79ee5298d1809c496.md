+   a. Data to the program is input from a file of an unspecified length; that is, the program does not know in advance how many numbers are in the file.

+   b. Save the output of the program in a file.

+   c. Modify the function `getNumber` so that it reads a number from the input file (opened in the function main), outputs the number to the output file (opened in the function main), and sends the number read to the function main. Print only 10 numbers per line.

+   d. Have the program find the sum and average of the numbers.

+   e. Modify the function `printResult` so that it outputs the final results to the output file (opened in the function main). Other than outputting the appropriate counts, this new definition of the function `printResult` should also output the sum and average of the numbers.

+   6. For research purposes and to better help students, the admissions office of your local university wants to know how well female and male students perform in certain courses. You receive a file that contains female and male student GPAs for certain courses. Due to confidentiality, the letter code of is used for female students and m for male students. Every file entry consists of a letter code followed by a GPA. Each line has one entry. The number of entries in the file is unknown. Write a program that computes and outputs the average GPA for both female and male students. Format your results to two decimal places. Your program should use the following functions:

+   a. Function `openFiles`: This function opens the input and output files, and sets the output of the floating-point numbers to two decimal places in a fixed decimal format with a decimal point and trailing zeros.

+   b. Function `initialize`: This function initializes variables such as `countFemale`, `countMale`, `sumFemaleGPA`, and `sumMaleGPA`.

+   c. Function `sumGrades`: This function finds the sum of the female and male students’ GPAs.

+   d. Function `averageGrade`: This function finds the average GPA for female and male students.

+   e. Function `printResults`: This function outputs the relevant results.

+   f. There can be no global variables. Use the appropriate parameters to pass information in and out of functions.

+   7. Write a program that prints the day number of the year, given the date in the form month-day-year. For example, if the input is 1-1-2006, the day number is 1; if the input is 12-25-2006, the day number is 359. The program should check for a leap year. A year is a leap year if it is divisible by 4, but not divisible by 100. For example, 1992 and 2008 are divisible by 4, but not by 100. A year that is divisible by 100 is a leap year if it is also divisible by 400. For example, 1600 and 2000 are divisible by 400. However, 1800 is not a leap year because 1800 is not divisible by 400.