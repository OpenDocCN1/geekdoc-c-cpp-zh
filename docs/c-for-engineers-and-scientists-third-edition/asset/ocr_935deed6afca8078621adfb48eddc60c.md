# Program 10.1

```
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2005); // constructor
    void setState(int, int, int); // member function to copy a date
    void showDate(); // member function to display a date
};

// class implementation section
Date::setDate(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

void Date::showDate()
{
    cout << "The date is ";
    cout << setfill('0')
        << setw(2) << month << '/\'
        << setw(2) << day << '/\'
        << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
}
```