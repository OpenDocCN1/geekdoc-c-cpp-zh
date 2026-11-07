Notice that the statement in Line 17 initializes the LCV name. The expression `name != SENTINEL` in Line 18 checks whether the value of name is not equal to SENTINEL. The statement in Line 23 updates the LCV name.

Next, consider another example of a sentinel-controlled **while** loop. In this example, the user is prompted to enter the value to be processed. If the user wants to stop the program, he or she can enter the sentinel.

# EXAMPLE 5-5

# Telephone Digits

The following program reads the letter codes A to Z and prints the corresponding telephone digit. This program uses a sentinel-controlled **while** loop. To stop the program, the user is prompted for the sentinel, which is #. This is also an example of a nested control structure, where **if...else** and the **while** loop are nested.

```
```cpp
/************************************************************
// Program: Telephone Digits
// This is an example of a sentinel-controlled loop. This
// program converts uppercase letters to their corresponding
// telephone digits.
//************************************************************

#include <iostream>                                      //Line 1

using namespace std;                                    //Line 2

int main()                                               //Line 3
{
        char letter;                                     //Line 5
        int digit, num;                                  //Line 6

        cout << "Program to convert uppercase letters to "
             << "their corresponding telephone digits."
             << endl;                                    //Line 8

        cout << "To stop the program enter #." << endl; //Line 9

        cout << "Enter an uppercase  letter: ";         //Line 10
        cin >> letter;                                   //Line 11
        cout << endl;                                    //Line 12

        while (letter != '#')                            //Line 13
        {
                cout << "Letter: " << letter;           //Line 15
                cout << ", Corresponding telephone digit: "; //Line 16

                num = static_cast<int>(letter)
                    - static_cast<int>('A');             //Line 17
```
```