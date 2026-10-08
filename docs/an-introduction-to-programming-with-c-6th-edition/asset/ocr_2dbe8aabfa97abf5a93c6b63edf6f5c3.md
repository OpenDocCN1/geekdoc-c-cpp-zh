# CHAPTER 12 Two-Dimensional Arrays

(continued)

| Output | displayed from the array |
| --- | --- |
| shipping charge | |
| Algorithm | |
| 1. enter the number ordered | cout << "Number ordered ";
cout << "negative number or 0 to end":
cin >> numOrdered;
| 2. repeat while (the number ordered is greater than 0, and less or equal to 99999) | while (numOrdered > 0 &&
numOrdered <= 999999)
assign = 0 to the row subscript counter to ensure the search begins in the first row | rowSub = 0;
| repeat (the row subscript counter is less than 3 and the number ordered is greater than the value located in the first column of the current row) | while (rowSub < 3 &&
numOrdered >
shipCharges[rowSub][0]);
| add 1 to the row subscript counter to continue the search in the next row | rowSub += 1;
| end repeat | //end while
| display the shipping charge | cout << "Shipping charge for a quantity of " << is $\$
<< shipCharges[rowSub][1]
<< endl;
| enter the number ordered | cout << "Number ordered ";
cout << "negative number or 0 to end":
cin >> numOrdered;
//end while
| end repeat |

Figure 12-24 Problem specification, IPO chart information, and C++ instructions for Lab 2-2

Figure 12-25 shows the code for the entire Falcon Incorporated program, and Figure 12-26 shows the completed desk-check table for the program, assuming the user enters the numbers 75, 200, and -1 as the number of items ordered.