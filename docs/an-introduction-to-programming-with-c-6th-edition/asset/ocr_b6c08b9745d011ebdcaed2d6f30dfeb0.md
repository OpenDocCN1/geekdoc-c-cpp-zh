# The Random Addition Problems Program

```
1 //Hypotenuse.cpp - displays the length of the
2 //hypotenuse of a right triangle
3 //Created/revised by your <name> on current date
4
5 #include <iostream>
6 #include <cmath>
7 using namespace std;
8
9 int main() {
10 {
1
12 //declare variables
13 double sideA = 0.0;
14 double sideB = 0.0;
15 double sumSqr = 0.0;
16 double hypotenuse = 0.0;
17
18 //get length of two sides
19 cout << "Side a length: ";
20 cin >> sideA;
21 cout << "Side b length: ";
22 cin >> sideB;
23
24 //calculate the length of the hypotenuse
25 sumSqr = pow(sideA, 2) + pow(sideB, 2);
26 hypotenuse = sqrt(sumSqr);
27
28 //display the length of the hypotenuse
29 cout << "Hypotenuse length: ";
30 << hypotenuse << endl;
31
32 system("pause");
33 return 0;
34 } //end of main function
```

Figure 9-4 Hypotenuse program

![](bbox=[0.118, 0.676, 0.463, 0.768])

Figure 9-5 Sample run of the hypotenuse program

# The Random Addition Problems Program

Figure 9-6 shows the problem specification and IPO chart for the random addition problems program. (The flowchart for this program is contained in the Ch9flowcharts.pdf file, which is located in Cpp6Chap09 folder). The algorithm requires the computer to generate two random integers from 1 to 10, inclusive. You will learn how to generate random integers in the next section.