# The while Statement

sales variable. The looping condition in the while !(sales != -1) compares the value stored in the sales variable with the sentinel value. If the sales variable does not contain the sentinel value, the loop condition evaluates to true and the loop body instructions are processed. These instructions calculate and display the bonus, then prompt the user to enter new sales amount, and store the user's in the sales variable. Each time the user enters sales amount, the looping condition in the while clause compares the sales to the sentinel value. When the user enters the sentinel value—in this case,—1 as the amount, the loop condition evaluates to false. As a result, the loop body is skipped and processing continues with the instructions located immediately after the end of the loop. Keep in mind that if you forget to enter the read (cin >> sales); in the loop body, it will process the loop instructions indefinitely. This is because without the cin >> sales; statement there is no way to change the value stored in the sales variable once the loop body instructions are processed. A loop is either an endless or infinite loop. You can stop a program by pressing Ctrl+C (and hold the Ctrl key as you tap the c, and you also use the Command Prompt Window's closure). A sample run of the program is shown in Figure 7-14. (The program uses the fixed and precision stream managers to display fixed-point notation with two decimal places).

![](bbox=[0.735, 0.373, 0.882, 0.465])

# IPO chart information

# C++ instructions

Input
sales ($%)

```
const double RATE = .05;
int sales = 0;
```

Processing
none

Output
bonus
double bonus = 0.0.

+   Algorithm
1. repeat while the sales are equal to -1
cout << "First sales amount
(-1 to stop): ";
cin >> sales;
while (sales != -1)
{
bonus = sales * RATE;
cout << "Bonus: $" << bonus;
cout << endl;
cout << "Next sales amount
(-1 to stop): ";
cin >> sales;
}// end while
2. calculate the bonus by multiplying the sales by the bonus rate
display the bonus
enter the sales
} repeat

Figure 7-13 IPO chart information and C++ instructions for the Miller Incorporated program

![](bbox=[0.923, 0.173, 0.982, 0.211])