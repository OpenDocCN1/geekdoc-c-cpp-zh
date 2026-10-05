# CHAPTER 7 Constructors and Other Tools

Display 7.1 Class with Constructors (part 1 of 2)

```
#include <iostream>
#include <cstdlib> // for exit
using namespace std;

class DayOfYear
{
public:
    DayYear(int monthValue, int dayValue);
    //Initializes the month and day to arguments.

    DayYear(int monthValue);
    //Initializes the date to the first of the given day.

    DayYear( ); // default constructor
    //Initializes the date to January 1.

    void input();
    void output();
    int getMonthNumber();
    //Returns 1 for January, 2 for February, etc.

private:
    int month;
    int day;
    void testDate();
};

int main()
{
    DayOfYear date1(2, 21), date2(5), date3;
    cout << "Initialized dates:\\n";
    date1.output(); cout << endl;
    date2.output(); cout << endl;
    date3.output(); cout << endl;

    DayOfYear dateel = DayOfYear(10, 31);
    cout << "date reset to the following:\\n";
    date1.output(); cout << endl;
    return 0;
}
```

> This definition of DayYear is an improved version of the class DayOfYear given in Display 6.4.

> This causes a call to the default constructor. Notice that there are no parentheses.

> an explicit call to the constructor
DayOfYear::DayOfYear