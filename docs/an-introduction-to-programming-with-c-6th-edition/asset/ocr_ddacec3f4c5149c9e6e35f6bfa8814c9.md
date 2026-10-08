# The Salary Program

(continued)

| Input | Processing | Output |
| --- | --- | --- |
| current reading | Processing items: none | units used |
| previous reading | | total charge |
| unit charge | | |
| address of variables to store: | | |
| units used | | |
| total charge | | |

+   Algorithm:
1. calculate the units used
   by subtracting the previous reading from the current reading
2. calculate the total charge
   by multiplying the units used by the unit charge

| Input | Processing | Output |
| --- | --- | --- |
| displayBill function | Processing items: none | units used |
| units used | | total charge |

+   Algorithm:
1. display the units used
2. display the total charge

Figure 10-28 IPO charts for the functions in the electric bill program

After completing the IPO charts, you move on to the third step in the problem-solving process, which is to desk-check the algorithm. You desk-check the algorithms in Figure 10-28 using 53512 and 51875 as the current and previous reading meters. Using these values, the number of units and total charge were 1637 and $147.33, respectively. Figure 10-29 shows the completed desk-check table.

| current reading (main) | previous reading (main) | unit charge (main) |
| --- | --- | --- |
| current reading (main) | previous reading (main) | unit charge (main) |
| 53512 | 51875 | .09 |
| units used (calcBill) | total charge (calcBill) | |
| units used (main) | total charge (main) | |
| 1637 | 147.33 | |
| current reading (calcBill) | previous reading (calcBill) | unit_charge (calcBill) |
| 53512 | 51775 | .09 |
| units used (displayBill) | total charge (displayBill) | |
| 1637 | 147.33 | |

Figure 10-29 Completed desk-check table for the electric bill algorithms