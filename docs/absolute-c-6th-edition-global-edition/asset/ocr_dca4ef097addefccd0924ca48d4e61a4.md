# Display 6.4  Class with Private Members (part 3 of 3)

```
```cpp
//Uses iostream and cstdlib;
void DayOfYear::set(int newMonth)
{
    if ((newMonth >= 1) && (newMonth <= 12))
        month = newMonth;
    else
    {
        cout << "Illegal month value! Program aborted.\n";
        exit(1);
    }
    day = 1;
}

int DayOfYear::getMonthNumber()
{
    return month;
}

int DayOfYear::getDay()
{
    return day;
}

//Uses iostream and cstdlib;
void DayOfYear::input()
{
    cout << "Enter the month as a number: ";
    cin >> month;
    cout << "Enter the day of the month: ";
    cin >> day;
    if ((month < 1) || (month > 12) || (day < 1) || (day > 31))
    {
        cout << "Illegal date! Program aborted.\n";
        exit(1);
    }
}

void DayOfYear::output()
    <The rest of the definition of DayOfYear::output is given in Display 6.3.>
```
```

Sample Dialogue

> ```text
> Enter today's date:
> Enter the month as a number: 3
> Enter the day of the month: 21
> Today's date is March 21
> J. S. Bach's birthday is March 21
> Happy Birthday Johann Sebastian!
> ```