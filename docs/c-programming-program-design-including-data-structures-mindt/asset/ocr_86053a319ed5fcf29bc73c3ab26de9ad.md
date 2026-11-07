Chapter 4 discussed how decisions are incorporated in programs. This chapter discusses how repetitions are incorporated in programs.

# # Why Is Repetition Needed?

David needs to lower his cholesterol count to stay physically fit and reduce the risk of heart attack, and he wants to accomplish this by doing regular exercises. He decided to join a gym and, among other measures, keep track of the number of calories burned each time he uses the gym. At the end of each week he wants to determine the average number of calories burned each day. We need to write a program that David can use to enter the number of calories burned each day and get as output the average number of calories burned each day. Suppose that the numbers of calories burned each day in a particular week are: 375, 425, 270, 190, 350, 200, and 365. To find the average number of calories burned each day, we must add these numbers and divide the total by 7. From what we have learned so far, we can write the following program to find the average number of calories burned each day.

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    int calBurnedDay1, calBurnedDay2, calBurnedDay3,
        calBurnedDay4, calBurnedDay5, calBurnedDay6,
        calBurnedDay7;
    int calBurnedInAWeek;

    cout << "Enter calories burned day 1: ";
    cin >> calBurnedDay1;
    cout << endl;

    cout << "Enter calories burned day 2: ";
    cin >> calBurnedDay2;
    cout << endl;

    cout << "Enter calories burned day 3: ";
    cin >> calBurnedDay3;
    cout << endl;

    cout << "Enter calories burned day 4: ";
    cin >> calBurnedDay4;
    cout << endl;

    cout << "Enter calories burned day 5: ";
    cin >> calBurnedDay5;
    cout << endl;

    cout << "Enter calories burned day 6: ";
    cin >> calBurnedDay6;
    cout << endl;
```
```