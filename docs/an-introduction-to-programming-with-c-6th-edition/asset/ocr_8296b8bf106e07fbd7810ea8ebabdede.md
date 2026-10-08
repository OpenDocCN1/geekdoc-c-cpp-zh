# The for Statement

(continued)

| 2. repeat for (rate from 10% to 25% in increment of 5%) | for (double rate = .1; rate <= .25; rate = rate + .05) |
|---|---|n| calculate the commission by multiplying the sales amount by the rate | commission = sales * rate; |
| display the commission | cout << rate * 100 << "% commission: $" << commission << endl;
 } // for repeat |

Figure 7-36 Problem specification, IPO chart information, and C++ instructions for the Colfax sales program

Figure 7-37 lists the steps the computer follows when processing the code shown in Figure 7-36, using a sales amount of $25,000. Note that the for loop ends when the value stored in the variable is .3. Figure 7-38 shows a sample run of the Colfax program.

# Processing steps

+   1. The computer creates the sales and computer variables and initializes them to 0.0.
2. The computer prompts the user to enter a sales amount and stores the user's response (in this case, 25000) in the sales variable.
3. The computer processes the for's initialization argument (double rate = .1), creates the variable and initializes it to .1.
4. The computer processes the for's condition argument (rate <= .25), which checks whether the variable value is less or equal to .25. If it is, the computer processes the statements in the loop body. Those statements calculate a 10% commission and display the result (2500) on the screen.
5. The computer processes the for's update argument (rate += .05), which adds the value stored in the rate variable; the result is 15.
6. The computer processes the for's condition argument, which checks whether the variable's value is less than or equal to .25. If it is, the computer processes the statements in the loop body. Those statements calculate a 15% commission and display the result (3750) on the screen.
7. The computer processes the for's update argument, which adds the .05 to the value stored in the rate variable; the result is .2.
8. The computer processes the for's condition argument, which checks whether the variable value is less or equal to .25. If it is, the computer processes the statements in the loop body. Those statements calculate a 20% commission and display the result (5000) on the screen.
9. The computer processes the for's update argument, which adds the .05 to the value stored in the rate variable; the result is .25.\n10. The computer processes the for's condition argument, which checks whether the variable's value is less or equal to .25. If it is, the computer processes the statements in the loop body. Those statements calculate a 25% commission and display the result (6250) on the screen.
11. The computer processes the for's update argument, which adds the .05 to the value stored in the rate variable; the result is .3.

Figure 7-37 Processing steps for the code shown in Figure 7-36 (continues)