# CHAPTER 7 Constructors and Other Tools

# Class Type Member Variables

A class member may have a member variable whose type is that of another class. By large there is nothing special that you need to have a class member variable, but there is a special notation to allow for the invocation of the member variable's constructor within the constructor of the outer class. An example is given in Display 7.3.

Display 7.3 A Class Member Variable (part 1 of 3)

```
#include <iostream>
#include <cstdlib>
using namespace std;

class DayOfYear {
public:
    DayOfYear(int month, int dayValue);
    DayOfYear(int month);
    DayOfYear();
    void output(); // The DayOfYear is the same as in
Display 7.1, but we have repeated all the
details you need for this discussion.
    int getMonth();
    int getDay();
private:
    int month;
    int day;
    void testDate();
};

class Holiday {
public:
    Holiday(int month, int day, bool theEnforcement);
    void output();
private:
    DayOfYear date; // member variable of a
    class type
    bool parkingEnforcement; //true enforced
};

int main() {
    Holiday h(2, 1, true);
    cout << "Testing the class Holiday.\n";
    h.output(); // Invocations of constructors
from the class
    return 0;
}
Hol::Holiday() : date(1, 1), parkingEnforcement(false)
/*/Intentionally empty */

Hol::Holiday(int month, int day, bool theEnforcement)
    : date(month, day), parkingEnforcement(theEnforcement);
```