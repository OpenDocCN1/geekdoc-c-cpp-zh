```
int nested = 1;
for (int outer = 1; outer <= 2; outer += 1)
{
    do //begin loop
        cout << nested;
        cout << " ";
        nested += 1;
    } while (nested < 4);
    cout << endl;
    nested = 1;
} //end for
```

Figure 8-42

+   1. Write a C++ while clause that stops a posttest loop when the value in the quantity variable is less than the number 0. (The answers to TRY THIS Exercises are located at the end of the chapter.)

+   2. Rewrite the code shown in Figure 8-42 so it uses the while statement for the outer loop and the for statement for the nested loop.

+   3. Rewrite the code shown in Figure 8-42 to use the while statement for the outer loop.

+   4. Write a C++ while clause that processes a posttest loop's instructions as long as the value in the inStock variable is greater than the order variable.

+   5. Write a C++ while clause that stops a posttest loop when the value in a char named letter is anything other than the letter Y (in either uppercase or lowercase).

+   6. Write an assignment statement that raises the number 2 to the 25th power and assigns the result to a double variable named answer.

+   7. A program that declares an int variable named oddNum and initializes it to 1. Write the C++ code to display the odd integers 1, 3, 5, 7, and 9 separate lines on the computer screen. Use the while statement.

+   8. Write the code to display a table of four rows and six columns. The first column should contain the numbers 1 through 4 raised to the first power. The second column should contain the result of raising the number in the first column to the second power. The third column should contain the result of raising the number in the first column to the third power, and so on. The table will look like the one shown in Figure 8-43. Use two for statements: one to keep track of the numbers 1 through 4, and the other to keep track of the powers (1 through 6).