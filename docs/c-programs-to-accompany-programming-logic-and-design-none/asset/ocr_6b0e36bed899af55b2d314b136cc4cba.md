and reads the user’s response. The loop control variable is tested with `response == "Y"`. If the user enters Y, which is the sentinel value, then the test expression is true and the four statements within the loop body execute.

The first statement displays the value of `bankBal`. Next, the value of `bankBal` is recalculated using the value of `intRate`, the third statement prompts the user for a new value for `response`, and the fourth statement retrieves the user’s input and stores it in `response`. This is the statement that may change the value of the loop control variable. The loop body ends when program control returns to the top of the loop, where the Boolean expression in the `while` statement is tested again. If the user entered Y at the last prompt, then the loop is entered again and the new value of `bankBal` is displayed. If the user enters any response other than Y, then the test expression is false, and the loop body doesn’t execute. When the loop is exited, the next statement to execute displays “Have a nice day?”

> > **NOTE**  
> > It is important for you to understand that lowercase “Y” and uppercase “Y” are different values.

# EXERCISE 5-4: USING A SENTINEL VALUE TO CONTROL A WHILE LOOP

In this exercise, you use what you have learned about sentinel values to answer questions about the following code:

```
cout << "How many pages do you want to print? ";
cin >> numToPrint;
counter = 1;
while(counter <= numToPrint);
{
    cout << "Page Number " << counter << endl;
    counter++;
}
cout << "Value of counter is " << counter << endl;
```

+   1. What is the output if the user enters a 5?
+   
+   2. What is the problem with this code and how can you fix it?
+   
+   3. Assuming you fix the problem, if the user enters 200 as the number of pages to print, what is the value of counter when the loop exits?
+   
+   4. Assuming you fix the problem, if the user enters 21 as the number of pages to print, how many pages will print?
+   
+   5. What is the output if the curly braces are deleted?