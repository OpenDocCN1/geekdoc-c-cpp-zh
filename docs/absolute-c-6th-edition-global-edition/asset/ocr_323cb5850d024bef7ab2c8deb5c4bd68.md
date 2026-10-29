# Display 3.7 Use of return in a void Function

```
1 #include <iostream>
2 using namespace std;
3 void iceCreamDivision(int number, double totalWeight);
4 //Outputs instructions for dividing totalWeight ounces of ice cream
5 //among number customers. If number is 0, only an error
//message is output.
6 int main()
7 {
8     int number;
9     double totalWeight;
10     cout << "Enter the number of customers: ";
11     cin >> number;
12     cout << "Enter weight of ice cream to divide (in ounces): ";
13     cin >> totalWeight;
14     iceCreamDivision(number, totalWeight);
15     return 0;
16 }
17 void iceCreamDivision(int number, double totalWeight)
18 {
19     double portion;
20     if (number == 0)
21     {
22         cout << "Cannot divide among zero customers.\n";
23         return;
24     }
25     portion = totalWeight/number;
26     cout << "Each one receives "
27         << portion << " ounces of ice cream." << endl;
28 }
```

If number is 0, then the function execution ends here.

# Sample Dialogue

```
Enter the number of customers: 0
Enter weight of ice cream to divide (in ounces): 12
Cannot divide among zero customers.
```