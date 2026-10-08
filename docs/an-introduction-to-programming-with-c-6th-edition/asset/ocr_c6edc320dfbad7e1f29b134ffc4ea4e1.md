The third instruction in the algorithm is to calculate the tip by multiplying the total bill without liquor charge by the tip percentage. The desk-check table shows that the total bill without liquor charge is 35 and the tip percentage is .2. When you multiply 35 by 2, you get 7. You record the number 7 in the tip column, as shown in Figure 2-16.

| total bill | liquor charge | tip percentage | total bill without liquor charge | tip |
|---|---|---|---|--|
| 45 | 10 | 2 | 35 | 7 |

Figure 2-16 Output value entered in the desk-check table

The last instruction in the algorithm is to display the tip. In this case, the number 7 will be displayed as that appears in the tip column. Note that this amount agrees with the manual calculation shown in Figure 2-12; therefore, the algorithm appears to be correct. The only way to know for sure, is to test the algorithm a few times with different input values. For the second desk-check, you will test the algorithm using $30, $0, and .15 as the bill, liquor charge, and tip percentage, respectively. The tip should be $4.50, as shown in Figure 2-17.

| $30 (total bill) |
| 0 (liquor charge) |
| 30 (total bill without liquor charge) |
| .15 (tip percentage) |
| $4.50 (tip) |

Figure 2-17 Manual tip calculation for the second desk-check

Recall that the first instruction in the algorithm is to enter the total bill, liquor charge, and tip percentage. Therefore, you write 30, 0, and .15 in the appropriate columns of the desk-check table, as shown in Figure 2-18. Although it's not required, some programmers find it helpful to lightly cross out the previous value in a column before recording a new value. This does keep track of the column's current value.

| total bill | liquor charge | tip percentage | total bill without liquor charge | tip |
|---|---|---|---|--|
| 45 | 10 | 2 | 35 | 7 |
| 30 | 0 | .15 | 30 | 4.5 |

Figure 2-18 Second set of input values entered in the desk-check table

The second instruction in the algorithm is to calculate the total bill with liquor charge. You do this by subtracting the value in the liquor charge column (0) from the value in the total bill column (30). You record the result (30) in the total bill without liquor charge column. See Figure 2-19.