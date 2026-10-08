# CHAPTER 7

# The Repetition Structure

setprecision stream manipulators to display the average sales amount in fixed-point notation with no decimal places.

| sales | numSales | totalSales | average |
| --- | --- | --- | --- |
| 6.0 | 6.0 | 6.0 | 6.0 |
| 30000.0 | + | 30000.0 | 35000.0 |
| 40000.0 | 2 | 70000.0 | |
| -3.0 | | | |

**Figure 7-19** Completed desk-table for the Sales Express program

![](bbox=[0.312, 0.283, 0.785, 0.372])

**Figure 7-20** First sample run of the Sales Express program

![](bbox=[0.312, 0.429, 0.785, 0.508])

**Figure 7-21** Second sample run of the Sales Express program

The answers to the Mini-Quiz questions are located in Appendix A.

# Mini-Quiz 7-2

+   1. Which of the following usually is updated by an amount that varies?
   a. accumulators
   b. counters
2. Write a C++ assignment statement that updates the quantity variable by 2.
3. Write a C++ assignment statement that updates the total counter variable by -3.
4. Write a C++ assignment statement that updates the totalPurchases accumulator variable by the value stored in the purchases variable.

# Counter-Controlled Pretest Loops

In both Miller Incorporated and Sales Express programs, the termination of the loop is determined by a sentinel value that is entered by the user at the keyboard. Other loops are controlled using a counter rather than a sentinel value; such loops are referred to as **counter-controlled loops**. The