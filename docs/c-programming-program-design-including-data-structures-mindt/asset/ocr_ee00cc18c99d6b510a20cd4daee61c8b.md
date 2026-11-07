```
```cpp
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

    if (isAM == 'y' || isAM == 'Y')
        departureAM = true;
    else
        departureAM = false;

    cout << employeeName << endl;
    timeOnJob(arrivalHr, arrivalMin, arrivalAM,
        departureHr, departureMin, departureAM);

    cout << "Enter arrival hour: ";
    cin >> arrivalHr;
    cout << endl;
    cout << "Enter arrival minute: ";
    cin >> arrivalMin;
    cout << endl;
    cout << "Enter (y/Y) if arrival is before 12:00PM: ";
    cin >> isAM;
    cout << endl;

    int arrivalMin;
    bool arrivalAM;
    cout << "Run program again (y/Y): ";
    cin >> response;
    cout << endl;
    cin.get(discard);
}
}

return 0;
}

void timeOnJob(int arrHr, int arvMin, bool arvIsAM,
               int depHr, int depMin, bool depIsAM)
```
```