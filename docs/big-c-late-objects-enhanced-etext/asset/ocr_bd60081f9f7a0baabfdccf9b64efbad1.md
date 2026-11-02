The file rc.txt contains a list of values of time t and the corresponding capacitor voltage v(t). A time in µs and the corresponding voltage in volts are printed on the same line. For example, the line

110 7.02261

indicates that the capacitor voltage is 7.02261 volts when the time is 110 µs. The time is increasing in the data file.

Write a program that reads the file rc.txt and uses the data to calculate the rise time. Approximate B by the voltage in the last line of the file, and find the data points that are closest to 0.05 × B and 0.95 × B.

# Engineering P8.23 Suppose a file contains bond energies and bond lengths for covalent bonds in the following format:

![](bbox=[0.07, 0.36, 0.28, 0.66])

© Chris Dascher/Stockphoto.

| Single, double, or triple bond | Bond energy (kJ/mol) | Bond length (nm) |
|---|---|---|
| C|C | 370 | 0.154 |
| C||C | 680 | 0.13 |
| C|||C | 890 | 0.12 |
| C|H | 435 | 0.11 |
| C|N | 305 | 0.15 |
| C|O | 360 | 0.14 |
| C|F | 450 | 0.14 |
| C|Cl | 340 | 0.18 |
| O|H | 500 | 0.10 |
| O|O | 220 | 0.15 |
| O|Si | 375 | 0.16 |
| N|H | 430 | 0.10 |
| N|O | 250 | 0.12 |
| F|F | 160 | 0.14 |
| H|H | 435 | 0.074 |

Write a program that prompts the user to enter a data item in the format of any of the columns, and prints the corresponding data from the other columns in the stored file. The program should print "No matching entries" and exit when the user types an item that does not appear in the table. If input data matches different rows, then return all matching row data. For example, a bond length input of 0.12 should return triple bond C|||C and bond energy 890 kJ/mol and single bond N|O and bond energy 250 kJ/mol.