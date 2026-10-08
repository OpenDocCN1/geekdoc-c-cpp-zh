# The KL Motors Program—Searching an Array

$35000: 5 " when the payroll manager enters 35000. The statements on Lines
39 through 41 then prompt the user to enter another salary amount and store
t user's response in the searchFor variable. The statement on Line 42
ets the numEarnOver counter variable. Next, the condition in the while
clause on Line 24 is evaluated. If the searchFor variable's value is
gr than equal to the number 0, the instructions in the while loop are
processed again. Otherwise, the loop ends, and the computer processes the
statements on Lines 44 and 45 before the program ends.

```
// //KL Motors.cpp - displays the number of employees
// //whose salary is greater than a specific amount
// //Created/revised by <name> on <current date>

#include <iostream>
using namespace std;

int main() {
    //declare array and variables
    int salaries[10] = {23000, 26000,
34000, 21000,
54000, 45000,
36000, 38000,
75000, 34000};
    int searchFor = 0;
    int numEarnOver = 0;           //counter

    //get salary to search for
    cout << "Salary to search for for "
    << "(negative number to end): ";
    cin >> searchFor;

    while (searchFor >= 0) {
        //search the array
        for (int sub = 0; sub < 10; sub += 1) {
            if (salaries[sub] > searchFor)
                numEarnOver += 1;
        }
    }
    //display the search results
    cout << "Number of employees earning"
    << " from $" << searchFor << " : ";
    << numEarnOver << endl;

    //get another salary to search for
    cout << "Salary to search for "
    << "(negative number to end): ";
    cin >> searchFor;
    numEarnOver = 0;
}
system("pause"); your C++ development tool may
require this statement
return 0;
} //end of main function
```