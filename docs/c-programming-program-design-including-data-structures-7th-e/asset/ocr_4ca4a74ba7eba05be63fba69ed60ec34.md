```
cout << "Time spent of job: "
     << timeOnJobIn / 60 << " hour(s) and "
     << timeOnJobIn % 60 << " minute(s." << endl;
}
else
    cout << "Invalid input." << endl;
if ((arvISAM == true && depISAM == true)
    || (arvISAM == false && depISAM == false))
{
    cout << "Invalid input." << endl;
}

void timeOnJob(int arvHr, int arvMin, bool arvISAM,
               int depHr, int depMin, bool depISAM);
}
```

+   17. The function `printGrade` in Example 6-13 is written as a void function to compute and output the course grade. The course score is passed as a parameter to the function `printGrade`. Rewrite the function `printGrade` as a value-returning function so that it computes and returns the course grade. (The course grade must be output in the function `main`.) Also, change the name of the function to `calculateGrade`.

+   18. In this exercise, you are to modify the Classify Numbers programming example in this chapter. As written, the program inputs the data from the standard input device (keyboard) and outputs the results on the standard output device (screen). The program can process only 20 numbers. Rewrite the program to incorporate the following requirements:
+   
+      a. Data to the program is input from a file of an unspecified length; that is, the program does not know in advance how many numbers are in the file.
+   
+      b. Save the output of the program in a file.
+   
+      c. Modify the function `getNumber` so that it reads a number from the input file (opened in the function `main`), outputs the number to the output file (opened in the function `main`), and sends the number read to the function `main`. Print only 10 numbers per line.
+   
+      d. Have the program find the sum and average of the numbers.
+   
+      e. Modify the function `printResult` so that it outputs the final results to the output file (opened in the function `main`). Other than outputting the appropriate counts, this new definition of the function `printResult` should also output the sum and average of the numbers.

+   19. Write a program that prints the day number of the year, given the date in the form month-day-year. For example, if the input is 1-1-2006, the day number is 1; if the input is 12-25-2006, the day number is 359. The program should check for a leap year. A year is a leap year if it is divisible by 4, but not divisible by 100. For example, 1992 and 2008 are divisible by