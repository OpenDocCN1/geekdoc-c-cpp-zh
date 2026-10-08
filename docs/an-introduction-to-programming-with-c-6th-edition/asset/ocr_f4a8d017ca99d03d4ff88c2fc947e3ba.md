# CHAPTER 7 The Repetition Structure

(continued)
The enter the sites instruction located above the loop is the priming read, and the one within the loop is the update read.

| total sales | sales; |
|---|---|
| enter the sales | cout << "Next sales amount (negative number to stop): "; cin << sales; // end while |
| end repeat | if (the number of sales entered is greater than 0) | if (numSales > 0) |
| | { average = totalSales / numSales; |
| | cout << "Average: $" average << endl; |
| | calculate the average sales by dividing the total sales by the number of sales entered | else |
| | cout << "No sales entered" << endl; |
| | display the average sales | // if |
| | display "No sales entered" message |

Figure 7-15 Problem specification, IPO chart information, and C++ instructions for the Sales Express program

You can observe the counters and accumulators are used in a program by desk-checking the code in Figure 7-15. You will do this using the following amounts: 30000, 40000, and -3. The average amount should be $35,000. After declaring and initializing the appropriate variables, the code prompts the user to enter the first sales amount and returns the user's response in the sales variable. See Figure 7-16.

| numSales | totalSales | average |
|---|---|---|
| sales = 30000 | 0.0 | 0.0 |

Figure 7-16 Desk-check table for first sales amount entered

The while (sales >= 0.0) clause begins a loop that repeats the loop body instructions as long as (or) the sales variable contains a value that is greater than or equal to 0.0. Note that the condition compares the variable's value with 0 rather than 0. This is because the value being compared has the same data type—in this case, double. The loop in Figure 7-15 stops when the sales variables contain a sentinel value. For this loop, sentinel is any value that is less than 0.0. The desk-check table in Figure 7-16 shows, the current value in the sales variable is greater than equal to 0.0; therefore, the computer will process the instructions in the loop body. The first instruction updates the counter's value by adding the 1 to it. The second instruction updates the accumulator's value by adding the current contents of the sales variable to it. You can also write the first two instructions in the loop

Unlike the loop in the Miller Incorporated program (earlier in Figure 7-13), the loop in the Sales Express program has more than one sentinel value.