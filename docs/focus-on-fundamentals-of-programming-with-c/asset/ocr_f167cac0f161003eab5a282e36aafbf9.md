Although the 15! times 16 example just happens not to show this, provision has to be made for a node-to-node carry when adding the intermediate products in the "helping lists" to get the final result.

Because the program will have to support the multiplication of factorial multiplicands (e.g., 567!) times three-digit numbers (e.g., 568), or four-digit numbers, the idea embraced above will have to be enhanced to accommodate up to three or four intermediate products in three or four "helping lists".

# General Computational Strategy

Supposed the user wished to calculate 15!. 15! would be derived in the most straightforward of all possible ways, building it up from one factorial. One factorial, "hard wired" into the program as 1, would be used as the basis for computing 2!. Two factorial would be the basis for computing 3!. This would continue until 14! and this would be used as the basis for deriving 15!.

# Specification

The program will query the user for an integer, n, and return the exact value of that integer's factorial, n!. While there is no reason that there has to be a logical limit to the size of the n the program can handle, your program should be able to handle a number at least as high as 9,999!.

Since n! may be an integer hundreds or thousands of digits long, its display will spill across several lines. When this happens, print out n! with the most significant digit at the left end of the top line and the units digit on the right-hand end of the number's lowest line. You should print a comma after every third digit (i.e., between the hundred's digit and the thousand's digit, between the hundred thousand's digit and the million's digit, etc.). Break lines at points where commas belong, and put the comma to the right of the number on the line being broken. This signifies that the number continues on the next line. Specifically, print no more than 45 digits per line. Your program should also output statistics on the following:

+   - Number of digits in each factorial
+   - Time, in milliseconds, taken by program to calculate n! .