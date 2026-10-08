The fourth step in the problem-solving process is to code the algorithm into a program. The IPO chart information and C++ instructions for the electric bill program are shown in Figure 10-30.

| main function IPO chart information | C++ instructions |
| :--- | :--- |
| Input | |
| current reading previous reading unit charge (.09) | int current = 0; int previous = 0; const double UNIT_CHG = .09; |
| Processing | |
| none | |
| Output | |
| units used total charge | int units = 0; double total = 0.0; |
| Algorithm | |
| 1. call the calcBill to get the current reading and previous reading, pass the function the addresses of variables in which to store the current reading and previous reading | getInput(current, previous); |
| 2. call the calcBill to calculate the units used and total charge, pass the function the current reading, and unit charge, as well as the addresses of variables in to store the units used and total charge | calcBill(current, previous, UNIT_CHG, total); |
| 3. call the displayBill to display the units used and total charge, pass the function the units used and total charge | displayBill(units, total); |
| getInput IPO chart information | C++ instructions |
| Input | |
| addresses of variables to store: current reading (formal parameter) previous reading (formal parameter) | int &newReading int &oldReading |
| Processing | |
| none | |
| Output | |
| current reading | stored in the newReading formal parameter |
| previous reading | stored in the oldReading parameter |

10-30 IPO chart information and C++ instructions for the electric bill program (continues)