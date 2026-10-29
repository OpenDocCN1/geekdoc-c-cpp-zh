
## Introduction to Classes

### Program 10.2

```cpp
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
        Date(int = 7, int = 4, int = 2012);    // constructor
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    cout << "Created a new date object with data values"
         << month << ", " << day << ", " << year << endl;
}

int main()
{
    Date a;             // declare an object
    Date b;             // declare an object
    Date c(4,1,2009);   // declare an object
    return 0;
}
```

### Calling Constructors

As you have seen, constructors are called whenever an object is created. The actual declaration, however, can be made in a variety of ways. For example, the declaration

```cpp
Date c(4,1,2009);
```

used in Program 10.2 could also have been written as

```cpp
Date c = Date(4,1,2009);
```

This second form declares c as being of type Date and then makes a direct call to the constructor with the arguments 4, 1, and 2009. This second form can be simplified when only one argument is passed to the constructor. For example, if only the month data member of the `c` object needs to be initialized with the value 8 and the day and year members can use the default values, the object can be created by using this declaration:

```cpp
Date c = 8;
```

Because the form using an equal sign resembles declarations in C, it’s referred to as the **C style of initialization**. The declaration form in Program 10.2, referred to as the **C++ style of initialization**, is the form used predominantly in the remainder of this book.

Regardless of which initialization form you use, an object should never be declared with empty parentheses. For example, the declaration `Date a();` is not the same as the declaration `Date a;`. The second declaration uses the default constructor values, and the first declaration results in no object being created.

### Overloaded and Inline Constructors

The main difference between a constructor and other user-written methods is how the constructor is called: Constructors are called automatically each time an object is created, and other methods must be called explicitly by name.⁸ As a method, however, a constructor must still follow all the rules for user-written functions discussed in Chapter 6. Therefore, constructors can have default arguments (as in Program 10.1), can be overloaded, and can be written as inline functions.

Recall from Section 6.1 that function overloading permits using the same function name with different argument lists. Based on the supplied argument types, the compiler determines which function to use when the call is encountered. To see how overloading can be applied to the Date class, take another look at the class declaration repeated here:

```cpp
 // class declaration section
class Date
{
    private:
        int month;
        int day;
        int year;
    public:
        Date(int = 7, int = 4, int = 2012);      // constructor
};
```

The constructor prototype specifies three integer parameters, which are used to initialize the month, day, and year data members.

Another method of specifying a date is using a long integer in the form `year * 10000 + month * 100 + day`. With this form, the date 12/24/1998 is 19981224, and the date 2/5/2009 is 20090205.⁹ A suitable prototype for a constructor that uses dates in this form is shown here:

```cpp
Date(long);    // an overloaded constructor
```

8. This rule is true for all methods except destructors, described later in this section. A destructor method is called automatically each time an object is destroyed.
9. The reason for specifying dates in this manner is that only one number needs to be used per date, and sorting the numbers puts the corresponding dates into chronological order automatically.

The constructor is declared as receiving one long integer argument. The code for this new `Date()` method must, of course, convert its single argument into a month, day, and year and is included in the class implementation section. The actual code for this constructor is as follows:

```cpp
Date::Date(long yyyymmdd)  // a second constructor
{
    // extract the year
    year = int(yyyymmdd/10000.0);
    // extract the month
    month = int( (yyyymmdd - year * 10000.0) / 100.00 );
    // extract the day
    day = int(yyyymmdd - year * 10000.0 - month * 100.0);
}
```

Don't be overly concerned with the conversion code used in the method body. The important point is the concept of overloading the `Date()` method to provide two constructors. Program 10.3 contains the complete class definition in the context of a working program.

### Program 10.3

```cpp
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
    Date(int = 7, int = 4, int = 2012);  // constructor
    Date(long);           // another constructor
    void showDate();      // member method to display a date
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

Date::Date(long yyyymmdd)
{
    year = int(yyyymmdd/10000.0);  // extract the year
    month = int((yyyymmdd - year * 10000.0)/100.00 ); // extract the month
    day = int(yyyymmdd - year * 10000.0 - month * 100.0); // extract the day
}
void Date::showDate()
{
    cout << "The date is ";
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
    return;
}

int main()
{
    Date a, b(4,1,1998), c(20090515L);  // declare three objects
    a.showDate();                    // display object a's values
    b.showDate();                    // display object b's values
    c.showDate();                    // display object c's values

    return 0;
}
```

The output of Program 10.3 is as follows:

```text
The date is 07/04/12
The date is 04/01/98
The date is 05/15/09
```

Three objects are created in Program 10.3's `main()` function. The first object, a, is initialized with the default constructor, using its default arguments. Object b is also initialized with the default constructor but uses the arguments 4, 1, and 1998. Finally, object c, which is initialized with a long integer, uses the second constructor in the class implementation section. The compiler knows to use this second constructor because the specified argument, 20090515L, is designated as a long integer by the uppercase L. It's worth pointing out that a compiler error would occur if both Date constructors had default values. For example, a declaration such as `Date d;` would be ambiguous to the compiler because it couldn't determine which constructor to use. Therefore, in each implementation section, only one constructor can be written as the default.

As mentioned, constructors can also be written as inline functions. Doing so simply means defining the function in the class declaration section. For example, the following declaration section makes both constructors in Program 10.3 inline:

```cpp
// class declaration section
class Date
{
    private:
        int month;
        int day;
        int year;
    public:
        Date(int mm = 7, int dd = 4, int yyyy = 2012)
        {
            month = mm;
            day = dd;
            year = yyyy;
        }
        Date(long yyyymmdd)   // here is the overloaded constructor
        {
            year = int(yyyymmdd/10000.0);    // extract the year
            // extract the month
            month = int((yyyymmdd - year * 10000.0)/100.00);
            // extract the day
            day = int(yyyymmdd - year * 10000.0 - month * 100.0);
        }
};
```

The keyword `inline` isn’t required in this declaration because member methods defined in the class declaration are inline by default.

Generally, only methods that can be coded on a single line are good candidates for inline functions. This guideline reinforces the convention that inline functions should be small. Therefore, the first constructor is more conventionally written as follows:

```cpp
Date(int mm = 7, int dd = 4, int yyyy = 2012)
{
    month = mm; day = dd; year = yyyy;
}
```

The second constructor, which extends over three lines, should not be written as an inline function.

### Destructors

The counterpart to constructor methods are **destructor methods**. Destructors are methods with the same class name as constructors but are preceded with a tilde (~). Therefore, for the `Date` class, the destructor name is `~Date()`. Like constructors, the C++ compiler provides a default do-nothing destructor in the absence of an explicit destructor. Unlike constructors, however, there can be only one destructor method per class because destructors take no parameters and return no values.
