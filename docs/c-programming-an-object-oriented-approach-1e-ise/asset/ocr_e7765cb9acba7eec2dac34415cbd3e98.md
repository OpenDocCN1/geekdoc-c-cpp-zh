In the second run, the number has three digits. Here the first iteration extracts the right most digit (1), but the second iteration discards this digit and replaces it with the new right most digit (3) because when we enter the second iteration, the value of num is 23. A number with three digits goes through three iterations. The problem shows that we definitely need at least one iteration because the number entered has at least one digit (even if the number is 0).

# ### Data Validation

Another common example that requires at least one iteration is **data validation**. Data validation should be included in a program whenever a user enters data that must match a set of criteria. For example, when we enter flight information in an airline reservation system, some of the data are required and some are optional. Data validation ensures that we have entered all of the required data in the proper format.

# ### EXAMPLE 5.17

Data entry often requires the data be in a predefined range. For example, when we change a numeric score to a grade, test scores are usually in the range of 0 and 100. If the user enters a number out of the range, the program needs to repeat the request until the user enters a number that is in the correct range. Program 5.13 demonstrates this data

# **Program 5.13** Using a do-while loop for validation

```
```cpp
/**************************************************************
 * Demonstrate the use of the do-while loop to validate data    *
 **************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration
    int score;
    char grade;
    // Input validation loop
    do
    {
        cout << "Enter a score between 0 and 100: ";
        cin >> score;
    } while (score < 0 || score > 100);
    // Decision
    switch (score / 10)
    {
        case 10: grade = 'A';
```
```