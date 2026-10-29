
```cpp
int main()
{
    Date a;    // initialized by the default constructor
    Date b(20061225L);  // initialize with a long integer
    Date c(4,1,2007);   // initialize with the specified values

    cout << "Dates a, b, and c are ";
    a.showDate();
    cout << ", ";
    b.showDate();
    cout << ", and ";
    c.showDate();
    cout << ".\n";

    a = Date(20150103L);  // convert a long to a Date

    cout << "Date a is now ";
    a.showDate();
    cout << ".\n";

    return 0;
}
```

Program 11.7 produces the following output:

```
Dates a, b, and c are 07/04/12, 12/25/06, and 04/01/07.
Date a is now 01/03/15.
```

In reviewing Program 11.7, notice that the constructor function for converting changes b's long integer value to conform to the structure of a Date object. The conversion is made by the constructor function when b is declared. (For clarity, each object was declared separately.) Subsequently, a's date value is changed by calling the constructor function explicitly in the assignment statement `a = Date(20150103L);`

Formally, the constructor function defined in Program 11.7 is known as a type conversion constructor. This name is given to any constructor whose first argument is not a member of its class and whose remaining arguments, if any, have default values. If the first argument's data type is a built-in data type, as in Program 11.7, the constructor can be used to convert this built-in data type to a class object. In this case, because the first argument's data type is long, the constructor is used to convert a long to a Date object when the object is declared.

Additionally, because a constructor function can be called explicitly after all objects have been declared, it can be used as a cast independent of its initialization purpose. It's used in this manner in the following statement:

```cpp
a = Date(20150103L);  // convert a long to a Date
```

## Class to Class Conversion

Converting from a class data type to a class data type is done in the same manner as a conversion from a class to a built-in data type—by using a conversion operator function. In this case, however, the operator function uses the class name being converted to instead of a built-in data type name. For example, if you have two classes named Date and Intdate, the operator function `operator Intdate()` can be placed in the Date class to convert from a Date object to an Intdate object. Similarly, the operator function `Date()` can be placed in the Intdate class to convert from an Intdate to a Date. Notice that as before, in converting from a class data type to a built-in data type, the operator function’s name determines the result of the conversion; the class containing the operator function determines the data type being converted from.

Before seeing an example of a class to class conversion, you should note one additional point. Converting between classes clearly implies having two classes: one is always defined first, and one is defined second. Having a conversion operator function in the second class with the same name as the first class poses no problem because the compiler knows of the first class’s existence. However, including a conversion operator function with the second class’s name in the first class does pose a problem because the second class hasn’t been defined yet. To remedy this problem, a declaration for the second class must be made before the first class’s definition. This declaration, formally called a forward declaration, is shown in Program 11.8, which also includes conversion operators between the two defined classes. The relevant statements for this conversion have been shaded.

Program 11.8

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

// forward declaration of class Intdate
class Intdate;

// class declaration section for Date
class Date
{
private:
    int month, day, year;
public:
    Date(int = 7, int = 4, int = 2012); // constructor
    operator Intdate(); // conversion operator from Date to Intdate
    void showDate();
};

// class declaration section for Intdate
class Intdate
{
    private:
        long yyyymmdd;
    public:
        Intdate(long ym = 0);    // constructor
        operator Date();          // conversion operator from Intdate to Date
        void showint();
};

// class implementation section for Date
Date::Date(int mm, int dd, int yyyy)  // constructor
{
    month = mm;
    day = dd;
    year = yyyy;
}

// conversion operator function converting from Date to Intdate class
Date::operator Intdate()    // must return an Intdate object
{
    long temp;
    temp = year * 10000 + month * 100 + day;
    return(Intdate(temp));
}

// member function to display a Date
void Date::showDate()
{
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100;
    return;
}

// class implementation section for Intdate
Intdate::Intdate(long ymd)  // constructor
{
    yyyymmdd = ymd;
}

// conversion operator function converting from Intdate to Date class
Intdate::operator Date()    // must return a Date object
```

results. Notice, too, the forward declaration of the Intdate class before the Date class's declaration. It's required so that the Date class can reference Intdate in its conversion operator function.

### EXERCISES 11.3

- 1. (For review)
  - a. Define the three new data type conversions introduced in this section and the method of performing each conversion.
  - b. Define the terms "type conversion constructor" and "conversion operator function" and describe how they're used in user-defined conversions.

- 2. (Program) Write a C++ program that declares a class named Time having integer data members hours, minutes, and seconds. Include a type conversion constructor that converts a long integer, representing the elapsed seconds from midnight, into an equivalent representation as hours:minutes:seconds. For example, the long integer 30336 should convert to the time 8:25:36. Use military time—for example, 2:30 p.m. is represented as 14:30:00. The relationship between time representations is as follows:

    ```
    elapsed seconds = hours × 3600 + minutes × 60 + seconds
    ```

- 3. (Program) A Julian date is represented as the number of days from a known base date. The following pseudocode shows one algorithm for converting from a Gregorian date, in the form month/day/year, to a Julian date with a base date of 00/00/0000. All calculations in this algorithm use integer arithmetic, which means the fractional part of all divisions must be discarded. In this algorithm, M = month, D = day, and Y = year.

    ```
    If M is less than or equal to 2
    Set the variable MP = 0 and YP = Y - 1
    Else
    Set MP = int(0.4 × M + 2.3) and YP = Y
    EndIf
    T = int(YP / 4) - int(YP / 100) + int(YP / 400)
    Julian date = 365 × Y + 31 × (M - 1) + D + T - MP
    ```

    Using this algorithm, modify Program 11.7 to cast from a Gregorian Date object to its corresponding Julian representation as a long integer. Test your program by using the Gregorian dates 1/31/2011 and 3/16/2012, which correspond to the Julian dates 734533 and 734943.

- 4. (Modify) Modify the program written for Exercise 2 to include a conversion operator function that converts an object of type Time into a long integer representing the number of seconds from midnight.

- 5. (Program) Write a C++ program that has a Date class and a Julian class. The Date class should be the same Date class used in Program 11.6, and the Julian class should represent a date as a long integer. For this program, include a conversion operator function in the Date class that converts a Date object to a Julian object, using the algorithm shown in Exercise 3.

    Test your program by converting 1/31/2011 and 3/16/2012, which correspond to the Julian dates 734533 and 734943.

- 6. (Program) Write a C++ program that has a Time class and an Ltime class. The Time class should have integer data members named hours, minutes, and seconds, and the Ltime class should have a long integer data member named elsecs, which represents the number of elapsed seconds since midnight. For the Time class, include a conversion operator function named `Ltime()` that converts a Time object to an Ltime object. For the Ltime class, include a conversion operator function named `Time()` that converts an Ltime object to a Time object.

## 11.4 Two Useful Alternatives: operator() and operator[]

At times, it’s convenient to define an operation having more than two arguments, which is the limit imposed on all binary operator functions. For example, each Date object contains three integer data members: month, day, and year. For this object, you might want to add an integer value to one of the other members instead of just the day member, as was done in Program 11.2. C++ makes this possible by supplying the parentheses operator function, `operator()`, which has no limits on the number of arguments that can be passed to it.

Additionally, the case used in Program 11.2—in which only a single non-object argument is required—occurs so frequently that C++ provides an alternative means of achieving it: For this case, C++ supplies the subscript operator function, `operator[]`, which permits a maximum of one argument. The only restriction C++ imposes on the `operator()` and `operator[]` functions is that they must be defined as member (not friend) functions.

For simplicity, the `operator[]` function is discussed first. It’s declared and defined in the same manner as any other operator function, but it’s called differently from the normal function and operator call. For example, if you want to use the `operator[]` function to accept an integer argument and return a Date object, the following prototype is valid:

```cpp
Date operator[](int); // declare the subscript operator
```

Except for the operator function’s name, it’s similar in construction to any other operator function prototype. Assuming you want this function to add its integer argument to a Date object, a suitable function implementation is as follows:

```cpp
Date Date::operator[](int days)
{
    Date temp;    // a temporary Date to store the result

    temp.day = day + days;    // add the days
    temp.month = month;
    temp.year = year;
```
