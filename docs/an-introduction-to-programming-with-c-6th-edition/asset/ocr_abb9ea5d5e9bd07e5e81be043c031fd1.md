# CHAPTER 4 Completing the Problem-Solving Process

9. See Figure 4-41.

```
//TryThis9.cpp - calculates and displays the total owed
//Created/revised by <your name> on <current date>
3
#include <iostream>
using namespace std;
6
int main() {
    //declare variables and named constant
    int cupsPurchased = 0;
    int platesPurchased = 0;
    double cupPrice = 0.0;
    double platePrice = 0.0;
    double totalCupCost = 0.0;
    double totalPlateCost = 0.0;
    double subtotal = 0.0;
    double totalCost = 0.0;
    const double TAX_RATE = .055;

    //input items
    cout << "Cup price: ";
    cin >> cupPrice;
    cout << "Plate price: ";
    cin >> platePrice;
    cout << "Cups purchased: ";
    cin >> cupsPurchased;
    cout << "Plates purchased: ";
    cin >> platesPurchased;

    //calculate total cost, subtotal, and the total cost
    totalCupCost = cupsPurchased * cupPrice;
    totalPlateCost = platesPurchased * platePrice;
    subtotal = totalCupCost + totalPlateCost;
    totalCost = subtotal * TAX_RATE + subtotal;

    //display total cost
    cout << "Total cost: $" << totalCost << endl;

    system("pause");
    return 0;
} //end of main function
```

> your C++ development tool may not require this statement

Figure 4-41