Here is the complete program, ch02/vending.cpp:

```
```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
   const int PENNIES_PER_DOLLAR = 100;
   const int PENNIES_PER_QUARTER = 25;

   cout << "Enter bill value (1 = $1 bill, 5 = $5 bill, etc.): ";
   int bill_value;
   cin >> bill_value;
   cout << "Enter item price in pennies: ";
   int item_price;
   cin >> item_price;

   int amount_due = PENNIES_PER_DOLLAR * bill_value - item_price;
   int dollar_coins = amount_due / PENNIES_PER_DOLLAR;
   amount_due = amount_due % PENNIES_PER_DOLLAR;
   int quarters = amount_due / PENNIES_PER_QUARTER;

   cout << "Dollar coins: " << setw(6) << dollar_coins << endl
        << "Quarters:     " << setw(6) << quarters << endl;
}
```
```

# Program Run

```
```
Enter bill value (1 = $1 bill, 5 = $5 bill, etc.): 5
Enter item price in pennies: 225
Dollar coins:       2
Quarters:           3
```
```

# **WORKED EXAMPLE 2.2** Computing the Cost of Stamps

![](bbox=[0.08, 0.617, 0.185, 0.675])

This Worked Example uses arithmetic functions to simulate a stamp vending machine.

# 2.5 Strings

Strings are sequences of characters.

Many programs process text, not numbers. Text consists of characters: letters, numbers, punctuation, spaces, and so on. A string is a sequence of characters. For example, the string "Harry" is a sequence of five characters.

![](bbox=[0.642, 0.781, 0.893, 0.874])