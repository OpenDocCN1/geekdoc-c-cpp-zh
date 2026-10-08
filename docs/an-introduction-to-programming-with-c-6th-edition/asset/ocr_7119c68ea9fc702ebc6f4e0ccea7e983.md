# Passing a Two-Dimensional Array to a Function

```
//Lab12-2.cpp - displays the shipping charge
//Created/revised by your name on <current date>

#include <iostream>
using namespace std;

int main()
{
    //declare array and variables
    int shipCharges[3][2] = {{50, 20},
                               {100, 10},
                               {99999, 0}};

    int numOrdered = 0;
    int rowSub = 0;

    //enter the number ordered
    cout << "Number ordered ";
    cout << "(negative number or 0 to end): ";
    cin >> numOrdered;

    while (numOrdered > 0 && numOrdered <= 99999)
    {
        //search array
        rowSub = 0;
        while (rowSub < 3 && shipCharges[rowSub][0])
        {
            rowSub += 1; // you can use rowSub++;
        }
        } while;

        //display shipping charge
        cout << "Shipping charge for a quantity of ";
        cout << numOrdered << " is $$";
        cout << shipCharges[rowSub][1] << endl;

        //enter the number ordered
        cout << "Number ordered ";
        cout << "(negative number or 0 to end): ";
        cin >> numOrdered;
    }

    system("pause"); // your C++ development
    tool may not require this statement
    return 0;
} //end of main function
```

Figure 12-25 Falcon Incorporated program

![](bbox=[0.915, 0.182, 0.975, 0.215])