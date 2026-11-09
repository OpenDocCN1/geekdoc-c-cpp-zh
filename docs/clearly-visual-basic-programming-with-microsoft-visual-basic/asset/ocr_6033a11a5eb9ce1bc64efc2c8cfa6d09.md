The TryParse method converts the letter x to the number 0 and stores the result in the decSales variable. The variable’s value is then added to the accumulator variable, giving 0. Next, the counter variable is incremented by 1, giving 1. The InputBox function then prompts you to enter another sales amount. Because the TryParse method does not recognize the $, it converts your $5 entry to the number 0 and stores the result in the decSales variable. The variable’s value is added to the accumulator variable, giving 0. Next, the counter variable is incremented by 1, giving 2. The InputBox function then prompts you to enter another sales amount. When you click the Cancel button, the loop ends and the average sales amount is calculated by dividing the accumulator variable’s value (0) by the counter variable’s value (2); the result is 0. The formatted result appears in the lblAverage control. The $0.00 is an acceptable value to display when the user enters a letter or a special character along with a number.

+   12. Click the **Exit** button to end the application. Close the Code Editor window, then close the solution.

# ### MINI-QUIZ 3

+   1. Write an assignment statement to increment the intTotalNum accumulator variable by the contents of the intNum variable.
+   2. The empty string in Visual Basic is represented by the ________ named constant.
+   3. Write a statement that assigns the InputBox function’s return value to the strItem variable. The text “Item Name” should appear in the dialog box’s title bar. The “Enter the item:” message should appear inside the dialog box. The input area should be empty.

# ## SUMMARY

+   - You use a repetition structure, or loop, to repeatedly process one or more program instructions.
+   - A loop can be either a pretest loop or a posttest loop. Pretest loops are more commonly used. The condition in a pretest loop is evaluated *before* the loop instructions are processed. The condition in a posttest loop is evaluated *after* the loop instructions are processed.