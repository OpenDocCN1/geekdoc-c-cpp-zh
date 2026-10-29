After this function has been defined, it can be called by using the relational expressions a == b or a.operator==(b), assuming both a and b are Date objects. More typically, it's used in a conditional expression, such as if (a == b). Program 11.1 includes this if statement and the operator function in the context of a complete program. The shaded lines indicate statements pertaining to the operator function.

# Program 11.1

```
#include <iostream>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2012); // constructor
    bool operator==(Date&); // prototype for the operator== function
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

bool Date::operator==(Date& date2)
{
    if(day == date2.day && month == date2.month && year == date2.year)
        return true;
    else
        return false;
}

int main()
{
    Date a(4,1,2012), b(12,18,2010), c(4,1,2012); // declare 3 objects
```