# Program 2.4 Using unsigned integers

```
```
1 /************************************************
2  * Finding the total value of a set of coins
3  ************************************************/
4 #include <iostream>
5 using namespace std;
6
7 int main ()
8 {
9     // Defining constants
10     const unsigned int pennyValue = 1;
11     const unsigned int nickelValue = 5;
12     const unsigned int dimeValue = 10;
13     const unsigned int quarterValue = 25;
14     const unsigned int dollarValue = 100;
15     // Defining variables (number of each coin)
16     unsigned int pennies;
17     unsigned int nickels;
18     unsigned int dimes;
19     unsigned int quarters;
20     unsigned int dollars;
21     // Defining total value
22     unsigned long totalValue;
23     // Inputting number of different coins
24     cout << "Enter the number of pennies: ";
25     cin >> pennies;
26     cout << "Enter the number of nickels: ";
27     cin >> nickels;
28     cout << "Enter the number of dimes: ";
29     cin >> dimes;
30     cout << "Enter the number of quarters: ";
31     cin >> quarters;
32     cout << "Enter the number of dollars: ";
33     cin >> dollars;
34     // Calculating total value
35     totalValue = pennies * pennyValue + nickels * nickelValue +
36         dimes * dimeValue + quarters * quarterValue + dollars * dollarValue;
37     // Outputting result
38     cout << "The total value is: " << totalValue << " pennies.";
39     return 0;
40 }
```
```

```
```
Run:
Enter the number of pennies: 20
Enter the number of nickels: 5
Enter the number of dimes: 10
Enter the number of quarters: 4
Enter the number of dollars: 6
The total value is: 845 pennies.
```
```