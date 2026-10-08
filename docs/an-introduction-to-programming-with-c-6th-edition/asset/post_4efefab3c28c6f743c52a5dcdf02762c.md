
Robin is sitting at a table in a bookstore, attending her book signing. Customers are standing in line waiting for Robin to sign their copy of her bestselling book on Robotics. Robin needs to sign each customer's book. It's possible that some customers may not have a book, while others may have more than one book.

```
repeat (there are customers in line)
repeat (customer has a book that needs signing)
accept the book from the customer
open the front cover of the book
sign your name on the first page
close the book
return the book to the customer
end repeat
thank the customer
```

![](img/d64a28a68f49d61137bf2f3170ac40ad_295_0.png)

Figure 8-11 Modified problem specification and algorithm for signing zero or more books for each customer

A clock uses nested repetitions to keep track of the time. For simplicity, a clock's minute and second hands. The second hand moves one position, for every second that has elapsed. After the second hand moves 60 positions, the minute hand moves one position, also clockwise. The second hand then begins its journey around the clock face. Figure 8-12 shows the logic by a clock's minute and second hands. As the figure indicates, an outer loop controls the minute hand, while an inner (nested) loop controls the second hand. Again, notice that the entire loop is contained within the outer loop. Recall that this is a requirement for the loop to be nested and work correctly.

```
start minutes at 0
repeat (minutes are less than 60)
repeat (seconds are less than 60)
move second hand 1 position, clockwise
add 1 to seconds
end repeat
move minute hand 1 position, clockwise
add 1 to minutes
end repeat
```

![](img/d64a28a68f49d61137bf2f3170ac40ad_295_1.png)

The next iteration of the outer loop (which controls the minute hand) occurs only after the nested loop (which controls the second hand) has finished processing.

Figure 8-12 Logic by a clock's minute and second hands

# The Asterisks Program

Figure 8-13 shows the problem specification, IO chart information, and C++ instructions for a program that displays an asterisk on three separate lines on the computer screen. The algorithm, which is shown in both pseudocode and a flowchart, does not require a nested loop. This is because all of the instructions within the loop need to be repeated the same number of times: Figure 8-14 shows the completed desk-check table, and Figure 8-15 shows a sample run of the program.

| Problem specification | C++ instructions |
| :--- | :--- |
| Create a program that displays an asterisk on three separate lines on the computer screen, like this: <br>*<br>\* | |
| IPO chart information | |
| Input | |
| none | |
| Processing | this variable is created and initialized in the for clause |
| number of lines (counter: 1 to 3) | |
| Output | |
| asterisk (on each of 3 lines) | |
| Algorithm | |
| repeat (number of lines is less than 4) | for (int line = 1; line < 4; line += 1) { |
| display asterisk | cout << '*'; |
| position the cursor on the next line | cout << endl; |
| repeat | } // for end |

![](img/d64a28a68f49d61137bf2f3170ac40ad_296_0.png)

Figure 8-14 Completed desk-check table for the asterisks program

# The Asterisks Program

![](img/d64a28a68f49d61137bf2f3170ac40ad_297_0.png)

Figure 8-15 Sample run of the asterisks program

Figure 8-16 shows a modified version of the previous problem specification, along with the corresponding IPO chart information and C++ instructions. In the modified version, the program will display five asterisks on each of three separate lines on the computer screen. The modified algorithm will use two loops to accomplish this task: an outer loop to keep track of the number of lines and a nested loop to keep track of the number of asterisks. The changes made to the IPO chart information and C++ instructions are shown in Figure 8-16. In the code, the outer loop begins with the first for clause, which directs the computer to repeat the loop instructions. The outer loop ends with the //end for. Braces are required in the nested loop which begins with the second for clause, which directs the computer to repeat the cout << '* five times. The nested loop ends with //end for. Braces are not needed in the nested loop because its body contains only one statement. Here again, notice that the entire nested loop is contained within the outer loop. Both loops in Figure 8-16 are coded using the `for` statement, or both could be coded using the `while` statement. In addition, the algorithm could have been written using one or more posttest loops. Recall that you use the `do while` statement to create a posttest loop in C++.

![](img/d64a28a68f49d61137bf2f3170ac40ad_297_1.png)

Figure 8-16 Problem specification, IPO chart information, and C++ instructions for the modified asterisks program (continues)

# CHAPTER 8 More on the Repetition Structure (continued)

| Algorithm | C++ instructions |
| :--- | :--- |
| repeat while (number of lines is less than 4) | for (int line = 1; line < 4; line += 1) { |
| repeat while (number of asterisks is less than 6) | for (int numAsterisks = 1; numAsterisks < 6; numAsterisks += 1) cout << '*'; //end for |
| display an asterisk | cout << endl; |
| end repeat | //end for |
| position the cursor on the next line | |

![](img/d64a28a68f49d61137bf2f3170ac40ad_298_0.png)

Figure 8-16 Problem specification, IPO chart, and C++ instructions for the modified asterisks program

You can observe how the computer shown in Figure 8-16. First, the initialization argument in the checking code shown in the outer loop's for clause (int line = 1) tells the computer to create the line variable and initialize it to 1. The condition argument (line < 4) then directs the computer to check whether the line variable's value is less than the number 4. It so, the instructions in the body of the outer loop are processed. The first instruction is the nested loop's for clause. The clause's initialization argument (int numAsterisks = 1) tells the computer to create the numAsterisks variable and initialize it to the number 1. Its condition argument (numAsterisks < 6) directs the computer to check whether the numAsterisks is less than 6. cout << '*'; in statement of the nested loop is processed. That statement then displays an asterisk on the current line on the computer screen. Figure 8-17 shows the desk-check table and output after the nested loop's statement is processed the first time.

Recall from Chapter 7 for the clause's condition argument must be processed as a looping condition, which means it must specify the requirement for processing the loop instructions.

# The Asterisks Program

| line | numAsterisks |
| :--- | :--- |
| 1 | 1 |
| Output | * |

Figure 8-17 Desk-check table and output after the nested loop's `cout` statement processed the first time

Next, the `update` argument in the nested loop's `for` clause (`numAsterisks += 1`) tells the computer to add the number 1 to the value stored in the `numAsterisks` variable; the result is 2. Again, the `condition` argument in the nested loop's `cout` directs the computer to check whether the variable's value is less than 6. It is, the nested loop `cout << '*` statement displays another asterisk on the current line on the computer screen. Figure 8-18 shows the desk-check table and output after the `cout` statement processed the second time

| line | numAsterisks |
| :--- | :--- |
| 1 | 2 |
| Output | ** |

Figure 8-18 Desk-check table and output after the nested loop's `cout` statement processed the second time

The computer adds 1 to the value stored in the `numAsterisks` variable, giving 3. It then checks whether the variable's value is less than 6. It is, so the nested loop's `cout << '*` statement displays another asterisk on the current line on the computer screen. Figure 8-19 shows the desk-check table and output after the `cout` statement is processed the third time.

| line | numAsterisks |
| :--- | :--- |
| 1 | 3 |
| Output | *** |

Figure 8-19 Desk-check table and output after the nested loop's `cout` statement processed the third time
