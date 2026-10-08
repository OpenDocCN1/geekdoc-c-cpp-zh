# CHAPTER 8 More on the Repetition Structure

(continued)

| Algorithm | |
| repeat while (number of lines is less than 4) | for (int line = 1; line < 4; line += 1) { |
| repeat while (number of asterisks is less than 6) | for (int numAsterisks = 1; numAsterisks < 6; numAsterisks += 1) cout << '*'; //end for |
| display an asterisk | cout << endl; |
| end repeat | //end for |
| position the cursor on the next line | |

![](bbox=[0.313, 0.318, 0.853, 0.574])

Figure 8-16 Problem specification, IPO chart, and C++ instructions for the modified asterisks program

You can observe how the computer shown in Figure 8-16. First, the initialization argument in the checking code shown in the outer loop's for clause (int line = 1) tells the computer to create the line variable and initialize it to 1. The condition argument (line < 4) then directs the computer to check whether the line variable's value is less than the number 4. It so, the instructions in the body of the outer loop are processed. The first instruction is the nested loop's for clause. The clause's initialization argument (int numAsterisks = 1) tells the computer to create the numAsterisks variable and initialize it to the number 1. Its condition argument (numAsterisks < 6) directs the computer to check whether the numAsterisks is less than 6. cout << '*'; in statement of the nested loop is processed. That statement then displays an asterisk on the current line on the computer screen. Figure 8-17 shows the desk-check table and output after the nested loop's statement is processed the first time.

Recall from Chapter 7 for the clause's condition argument must be processed as a looping condition, which means it must specify the requirement for processing the loop instructions.

278