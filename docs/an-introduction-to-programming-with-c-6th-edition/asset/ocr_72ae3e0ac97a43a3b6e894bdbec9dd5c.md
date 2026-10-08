# Computer

8. See Figure 4-40.

```
// //TryThis8.cpp - calculates and displays the commission
2 //Created/revised by your <name> on <current date>
3
4 #include <iostream>
5 using namespace std;
6
7 int main()
8 {
9     //declare variables
10    double sale1 = 0.0;
11    double sale2 = 0.0;
12    double commissionRate = 0.0;
13    double totalSales = 0.0;
14    double commission = 0.0;
15
16    //enter input items
17    cout << "First sale? ";
18    cin >> sale1;
19    cout << "Second sale? ";
20    cin >> sale2;
21
22    cout << "Commission rate in decimal format? ";
23    cin >> commissionRate;
24
25    //calculate total sales and commission
26    totalSales = sale1+sale2;
27    commission = totalSales * commissionRate;
28
29    //display the commission
30    cout << "Commission: $" << commission << endl;
31
32    system("pause");
33    return: 0;
34 } //end of main function
```

Figure 4-40