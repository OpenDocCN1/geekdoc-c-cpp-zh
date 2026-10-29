# Program 10.2

```
#include <iostream>
using namespace std;
```

```
// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2012);    // constructor
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    cout << "Created a new date object with data values "
         << month << ", " << day << ", " << year << endl;
}
```

```
int main()
{
    Date a;        // declare an object
    Date b;        // declare an object
    Date c(4,1,2009); // declare an object
    return 0;
}
```

# Calling Constructors

As you have seen, constructors are called whenever an object is created. The actual declaration, however, can be made in a variety of ways. For example, the declaration

```
Date c(4,1,2009);
```

used in Program 10.2 could also have been written as

```
Date c = Date(4,1,2009);
```

This second form declares c as being of type Date and then makes a direct call to the constructor with the arguments 4, 1, and 2009. This second form can be simplified when only