
# Step 2—Plan the Algorithm

connected with lines, called *flowlines*. The oval symbol is the **start/stop symbol**. The start oval indicates the beginning of the flowchart, the stop oval indicates the end of the flowchart. Between the start and stop ovals are parallelograms, called input/output symbols. You use the **input/output symbol** to represent input tasks (as getting information from the user) and output tasks (as displaying, printing, or storing information). The first parallelogram in Figure 2-10 represents an input task, while the last parallelogram represents an output task. The rectangle in a flowchart is called **process symbol** and is used to represent tasks such as calculations.

| Input | Processing | Output |
| --- | --- | --- |
| total bill | Processing items: none | tip |
| liquor charge | | |
| tip percentage | | |

![](img/d64a28a68f49d61137bf2f3170ac40ad_49_0.png)

Figure 2-10 Figure 2-9's algorithm in flowchart form

When planning an algorithm you do not need to create both pseudocode and a flowchart; you need to use one of these planning tools. The tool you use is really a matter of personal preference. For simple algorithms, pseudocode works just fine. However, when an algorithm becomes more complex, its logic may be easier to see in a flowchart. As the old adage goes, a picture is sometimes worth a thousand words.

Every very simple problem can have more than one solution. Figure 2-11 shows a different solution to the Treyson Mobility problem. In this solution, the difference between the total bill and liquor charge is calculated in a separate instruction rather than the instruction that calculates the tip. The total bill without liquor charge is neither an input task (because it's not provided by the user) nor an output task (because it won't be displayed, printed, or stored in a file). Instead, the total bill without liquor charge is a special item, commonly referred to as a **processing item**.

represents an intermediate value (neither input nor output) that the algorithm when processing the input into the output. In this case, the algorithm uses two of the input items (total bill and liquor charge) to calculate the total bill without liquor charge (an intermediate value). It then uses its intermediate value, along with the tip percentage, to compute the tip.

# Problem specification

Treyson Mobley wants a program that calculates and displays the amount he should tip a waiter at a restaurant. The program should subtract any liquor charge from the total bill and then calculate the tip (using a percentage) on the remainder.

| Input | Processing | Output |
| --- | --- | --- |
| total bill | Processing items: | tip |
| liquor charge | total bill without liquor charge | |
| tip percentage | | | |

- Algorithm (pseudocode):
1. enter the total bill, liquor charge, and tip percentage
2. calculate the total bill without liquor charge by subtracting the liquor charge from the total bill
3. calculate the tip by multiplying the total bill without liquor charge by the tip percentage
4. display the tip

Algorithm (flowchart):

![](img/d64a28a68f49d61137bf2f3170ac40ad_50_0.png)

Figure 2-11 A different solution to the Treyson Mobley problem

The algorithms shown in Figures 2-9 through 2-11 produce the same result and simply represent two different ways of solving the same problem.

# Mini-Quiz 2-2

- 1. The parallelogram in a flowchart is called the symbol.
- 2. In a flowchart, calculation tasks are placed in a processing symbol, which has a shape.
- 3. Kendra Chopra lives in a state that that charges a 5% sales tax. She wants a program that displays the amount of sales tax due on a purchase. The input is the purchase amount and the sales tax rate. Complete an IPO chart, using pseudocode in the Algorithm section.
- 4. Henry Denton belongs to a CD (compact disc) club. Last year, he bought all of his CDs from the club for $8 per CD. He wants to know how much he saved by buying the CDs through the club rather than buying a music store that charges $12 per CD. The output is the savings. The input is the number of CDs purchased, the CD price, and the store CD price. Complete an appropriate IPO chart, using a flowchart in the Algorithm section. The algorithm should use two processing items: one for the cost of buying the CDs through the club and the other for the cost of buying the CDs through the store.

> The answers to Mini-Quiz questions are located in Appendix A.

# Step 3—Desk-Check the Algorithm

After analyzing a problem and planning its algorithm, you then desk-check the algorithm. The term desk-checking refers to the fact that the programmer reviews the algorithm at his or her desk in front of the computer. Desk-checking is also called hand-tracing, because the programmer uses a pencil and paper to follow each of the algorithm's instructions by hand. You should desk-check to verify that it is not missing any instructions and that the existing instructions are correct and in the proper order. Before you begin the desk-check, you choose a set of sample data for the input values, which you then use to manually compute the expected output value. Using inputs of $45, $10, and $2 (the decimal equivalent of 20%) as the total bill, liquor charge, and tip percentage, respectively. A manual calculation of the tip results in $7, as shown in Figure 2-12.

| total bill | 45 |
| liquor charge | 10 |
| total bill without liquor charge | 35 |
| tip percentage | 2 |
| tip | 7 |

Figure 2-12 Manual calculation of the tip

Now you use the sample input to desk-check the algorithm, which should result in the expected output of $7. It is helpful to use a desk-check

# CHAPTER 2 Beginning the Problem-Solving Process

when desk-checking an algorithm. The table should contain one column for each input, as well as one column for output and one column for processing item (if any). You can perform the desk-check using either the algorithm's pseudocode or its flowchart. Figure 2-13 shows one solution for the Trey problem with a partially completed desk-check table. (The flowchart for this solution is shown earlier in Figure 11.) Note that the desk-check contains five columns.

| Input | Processing | Output |
| --- | --- | --- |
| total bill | Processing items: | tip |
| liquor charge | total bill without liquor charge | |
| tip percentage | | |

```
Algorithm:
1. enter the total bill, liquor charge, and tip percentage
2. calculate the total bill without liquor charge by subtracting the liquor charge from the total bill
3. calculate the tip by multiplying the total bill without liquor charge by the tip percentage
4. display the tip
```

| total bill liquor charge tip percentage total bill without liquor charge tip |
| --- | --- | --- | --- | --- | --- |
| 45 | 10 | .2 | | 35 |

Figure 2-13 Trey problem solution and partially completed desk-check table

The first instruction in the algorithm is to enter the input values. You record the results of this instruction by writing 45, 10, and .2 in the total bill, liquor charge, and tip columns, respectively, in the desk-check table. See Figure 2-14.

| total bill liquor charge tip percentage total bill without liquor charge tip |
| --- | --- | --- | --- | --- | --- |
| 45 | 10 | .2 | | |

Figure 2-14 Input values entered in the desk-check table

The second instruction in the algorithm is to calculate the total bill without subtracting the liquor charge from the total bill. The desk-check table shows that the total bill is 45 and the liquor charge is 10. When making the calculation, always use the table to determine the values of the total bill and liquor charge. This helps to verify the accuracy of the algorithm. If, for example, the table did not show any amount in the total bill, you would need to enter the total bill amount. When you subtract the liquor charge (10) from the total bill (45), you get 35. Record the number 35 in the total bill without liquor charge, as shown in Figure 2-15.

| total bill liquor charge tip percentage total bill without liquor charge tip |
| --- | --- | --- | --- | --- | --- |
| 45 | 10 | .2 | | 35 |

Figure 2-15 Processing item's value entered in the desk-check table
