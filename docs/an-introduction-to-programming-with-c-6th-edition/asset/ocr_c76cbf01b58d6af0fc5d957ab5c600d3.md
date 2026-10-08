# CHAPTER 8

# More on the Repetition Structure

You can also write the for clause's update argument, which appears on Line 19 in Figure 8-40, as multiplier = multiplier + 1.

```
1 //Lab8-2.cpp - displays a multiplication table
2 //Created/revised by <name> on <current date>
3
4 #include <iostream>
5 using namespace std;
6
7 int main() {
8
9 //declare variables
10 int multiplicand = 0;
11 int product = 0;
12
13 cout << "Multiplicand (negative number to end): ";
14 cin >> multiplicand;
15
16 while (multiplicand >= 0) {
17
18 for (int multiplier = 1; multiplier < 10;
19 multiplier += 1)
20 {
21
22 product = multiplicand * multiplier;
23 cout << multiplicand << " = ";
24 << multiplier << " = ";
25 << product << endl;
26 }
27 //end for
28 //end while
29
30 cout << endl;
31 cout << "Multiplicand (negative number to end): ";
32 cin >> multiplicand;
33 }
34 //end of main function
```

Figure 8-40 Multiplication table program

# LAB 8-3 Modify

If necessary, create a new project named Lab8-3 Project. Enter (or copy) the Lab8-2.cpp instructions into a new source file named Lab8-3.cpp. Change Lab8-2.cpp in the first comment to Lab8-3.cpp. Change both loops to posttest loops. Save and then run the program. Use the program to display multiplication tables for the following multiplicands: 6, 9, and 2.