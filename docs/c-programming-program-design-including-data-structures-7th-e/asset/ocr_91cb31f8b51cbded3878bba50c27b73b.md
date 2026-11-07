16. The statements in the following program are not in the correct order. Rearrange the statements so that the program outputs the total time an employee spent on the job each day. The program asks the user to enter the employee’s name, the arrival time (arrival hour, arrival minute, AM or PM), and departure time (departure hour, departure minute, AM or PM). The program also allows the user to run the program as long as the user wishes. After rearranging the statements, your program must be properly indented.

```
```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string employeeName;
    int arrivalHr;

    int departureHr;
    int departureMin;
    bool departureAM;

    char response;
    char discard;
    char isAM;

    cout << "This program calculates the total time spent by an "
         << "employee on the job." << endl;
    cout << "To run the program, enter (y/Y): ";
    cin >> response;
    cout << endl;
    cin.get(discard);

    while (response == 'y' || response == 'Y')
    {
        cout << "Enter employee's name: ";
        getline(cin, employeeName);
        cout << endl;

        if (isAM == 'y' || isAM == 'Y')
            arrivalAM = true;
        else
            arrivalAM = false;

        cout << "Enter departure hour: ";
        cin >> departureHr;
        cout << endl;
        cout << "Enter departure minute: ";
        cin >> departureMin;
        cout << endl;
        cout << "Enter (y/Y) if departure is before 12:00PM: ";
        cin >> isAM;
        cout << endl;
```
```