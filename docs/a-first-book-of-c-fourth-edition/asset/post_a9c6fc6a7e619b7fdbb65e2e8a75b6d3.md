
```
while (temp.day > 30)    // now adjust the months
{
    temp.month++;
    temp.day -= 30;
}
while (temp.month > 12) // adjust the years
{
    temp.year++;
    temp.month -= 12;
}
return temp;    // the values in temp are returned
}
```

Again, except for the function header, it's similar in construction to the operator function definitions covered in Section 11.1. After the function is created, however, it can be called only by passing the required argument through the subscript brackets. For example, if oldDate is a Date object, the function call oldDate[284] calls the subscript operator function and causes the function to operate on the a object with the integer value 284. This function's prototype, definition, and call are shaded in Program 11.9.

## Program 11.9

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
    Date(int = 7, int = 4, int = 2012);    // constructor
    Date operator[](int);    // function prototype
    void showDate();    // member function to display a Date
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

## Chapter 11

### Two Useful Alternatives: `operator()` and `operator[]`

```
Date Date::operator[](int days)
{
    Date temp;      // a temporary Date to store the result

    temp.day = day + days;    // add the days
    temp.month = month;
    temp.year = year;
    while (temp.day > 30)     // now adjust the months
    {
        temp.month++;
        temp.day -= 30;
    }
    while (temp.month > 12)   // adjust the years
    {
        temp.year++;
        temp.month -= 12;
    }
    return temp;     // the values in temp are returned
}
```

```
void Date::showDate()
{
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100;
    return;
}
```

```
int main()
{
    Date oldDate(7,4,2011), newDate; // declare two objects

    cout << "The initial Date is ";
    oldDate.showDate();

    newDate = oldDate[284]; // add in 284 days = 9 months and 14 days

    cout << "\nThe New Date is ";
    newDate.showDate();
    cout << endl;

    return 0;
}
```

Program 11.9 is almost identical to Program 11.2, except that a subscript operator function is used in place of an overloaded addition operator function. Both programs produce the same output. In general, the overloaded operator used in Program 11.2 is preferable because the operator's name documents what operation is being performed. Although Program 11.9 shows how a subscript operator is created, in practice these operators are used for more complicated operations that other operator functions don't handle suitably. Therefore, subscript operators must be commented carefully to indicate their intended purpose.

Although the expression oldDate[284] used in Program 11.9 appears to indicate that oldDate is an array, it's not. It's simply the notation required to call an overloaded subscript function.

The parentheses operator function, operator(), is almost identical in construction to calling to the subscript function, operator[], with the substitution of parentheses, (), for brackets, []. The difference between these two operator functions is in the number of allowable arguments. The subscript operator function permits passing zero or one argument, but the parentheses operator function has no limit on the number of its arguments. For example, a suitable parentheses operator function prototype to add an integer number of months, days, or years to a Date object is as follows:

```
Date operator()(int, int, int);
```

After this function is implemented (which you do in Exercises 11.4), a call such as a(2,3,4) can be used to add 2 months, 4 days, and 3 years to the Date object named a.

These two extra functions offer a lot of programming flexibility. When only one argument is needed, they permit writing two different functions, both with the same argument type. For example, you could use operator[] to add an integer number of days to a Date object and operator() to add an integer number of months. Because both functions have the same argument type, one function name can't be overloaded for both cases. These two functions also give you the flexibility to restrict all other operator functions to class member arguments and then use these two functions for operations using nonclass arguments.

## EXERCISES 11.4

- 1. (Modify) a. Replace the operator[] function in Program 11.9 with the operator() function.
    b. Include the operator() function written for Exercise 1a in a working C++ program and verify its operation.

- 2. (Modify) a. Replace the operator[] function in Program 11.9 with a member operator() function that accepts an integer month, day, and year count. Have the function add the input months, days, and years to the object's date and return the resulting date. For example, if the input is 3, 2, 1 and the object's date is 7/16/2011, the function should return the date 10/18/2012. Make sure your function correctly handles an input such as 37 days and 15 months and adjusts the calculated day to be within the range 1 to 30 and the month to be within the range 1 to 12. Therefore, if the input is 37, 15, 1 and the object's date is 7/16/2011, the function should return the date 9/1/2015.
    b. Include the operator() function written for Exercise 2a in a working C++ program and verify its operation.

- 3. (Program) a. Construct a class named Student consisting of these private data members: an integer ID number, an integer count, and an array of four double-precision grades. The constructor for this class should set all data member values to 0. The class should also include a member function that displays all valid member grades, as determined by the grade count, and calculates and displays the average of the grades. Include the class in a working C++ program that declares three class objects named a, b, and c.

    b. Modify the class constructed for Exercise 3a to include a member operator[] function that has a double-precision grade count argument. The function should check the grade count data member and, if fewer than four grades have been entered, store its argument in the grade array, using the count as an index value. If four grades have already been entered, the function should return an error message indicating that the new grade can't be accepted. Additionally, a new grade should force an increment to the count data member.

    c. Modify the class constructed for Exercise 3a to include a member operator() function that has a grade index and grade value as arguments. The function should force a change to the grade corresponding to the index value and update the count, if necessary. For example, an argument list of 4, 98.5 should change the fourth test grade value to 98.5.

- 4. (Modify) a. Modify Program 10.9 to include a member operator[] function that multiplies an object's complex number (both the real and the imaginary parts) by a real number and returns a complex number. For example, if the real number is 2 and the complex number is 3 + 4i, the result is 6 + 8i.

    b. Verify the operation of the operator[] function written for Exercise 4a by including it in a working C++ program.

## 11.5 Common Programming Errors

- 1. Attempting to redefine an operator's meaning as it applies to C++'s built-in data types.
- 2. Redefining an overloaded operator to perform a function not indicated by its conventional meaning. Although this method works, it's an example of bad programming practices.
- 3. Using a user-defined assignment operator in a multiple assignment expression when the operator hasn't been defined to return an object.
- 4. Attempting to make a conversion operator function a friend rather than a member function.
- 5. Attempting to specify a return type for a conversion operator function.
- 6. Forgetting that this is a pointer that must be dereferenced by using *this or this->.

## 11.6 Chapter Summary

- 1. User-defined operators can be constructed for classes by using operator functions. An operator function has the form operator<symbol>, where <symbol> is one of the following:
- ( ) [ ] -> new delete ++ -- ! ~ * / % + -
- << >> < <= > >= ++ += -- -= && || & ^ | = +=
- -= *= /= %= &= ^= |= <<= >>= ,
