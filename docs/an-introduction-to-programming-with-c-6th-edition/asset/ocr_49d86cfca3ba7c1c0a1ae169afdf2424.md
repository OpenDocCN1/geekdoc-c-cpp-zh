# CHAPTER 5 The Selection Structure

```
1 //TryThis9.cpp - displays the new pay
2 //Created/revised by <your name> on current date>
3
4 #include <iostream>
5 #include <iomanip>
6 using namespace std;
7
8 int main()
9 {
10 //declare named constants and variables
11 const double RATE1 = .03;
12 const double RATE2 = .05;
13 char code = ' ';
14 double currentPay = 0.0;
15 double raise = 0.0;
16 double newPay = 0.0;
17
18 //enter input items
19 cout << "Pay code: ";
20 cin >> code;
21 cout << "Current pay: ";
22 cin >> currentPay;
23
24 //calculate raise and new pay
25 if (code == '4' || code == '9')
26 raise = currentPay * RATE2;
27 else
28 raise = currentPay * RATE1;
29 //end-if
30 newPay = currentPay + raise;
31
32 //display new pay
33 cout << fixed << setprecision(0);
34 cout << "New pay: $" << newPay << endl;
35
36 system("pause");
37 return 0;
38 } //end of main function
```

![](bbox=[0.62, 0.635, 0.735, 0.685])

Figure 5-42

162