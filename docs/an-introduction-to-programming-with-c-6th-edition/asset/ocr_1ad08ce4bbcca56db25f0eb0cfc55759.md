# CHAPTER 5 The Selection Structure

2. See Figure 5-39.

```
if (sold > 200) {
    bonus = 100;
    cout << "Great" << endl;
} else {
    bonus = 50;
    cout << "Good" << endl;
}//end if
```

Figure 5-39

![](bbox=[0.313, 0.323, 0.868, 0.355])

8. See Figures 5-40.

```
//TryThis.cpp - displays the total owed
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    //declare variables
    int quantity = 0;
    double price = 0.0;
    double discount = 0.0;
    double total = 0.0;
cout << "Price: ";
    cin >> price;
cout << "Quantity: ";
    cin >> quantity;
//calculate total owed
total = price * quantity;
//calculate discount, if necessary
    if (quantity > 5) {
        discount = total * .1;
        total = total - discount;
    }
//display total owed
out << fixed << setprecision(2);
cout << "Total owed: $" << total << endl;
sysystem("pause");
    return 0;
}//end of main function
```

Figure 5-40

> your C++ development tool may not require this statement