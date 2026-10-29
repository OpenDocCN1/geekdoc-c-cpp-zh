
```
public:
    // again, notice the colon here
    Date(int = 7, int = 4, int = 2012); // a member method
    void setDate(int, int, int);      // a member method
    void showDate();                  // a member method
}; // this is a declaration - don't forget the semicolon

// class implementation section
// this is where methods are defined
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

void Date::setDate(int mm, int dd, int yyyy)
{
    month = mm; day = dd; year = yyyy;
    return;
}

void Date::showDate()
{
    cout << "The date is ";
    cout << setw(2) << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
    return;
}
```

Because this definition might look overwhelming, first notice that it does consist of two sections—a declaration section and an implementation section. The declaration section begins with the keyword class followed by a class name. Following the class name are the class's variable declarations and method prototypes, enclosed in a brace pair terminated with a semicolon. The general structure of this form is as follows:

```
//class declaration section
class Name
{
```

## Introduction to Classes

```
private:
    a list of variable declarations
public:
    a list of method prototypes
};
```

Notice that the Date class follows this format. For convenience, it’s listed again with no internal comments:

```
// class declaration section
class Date
{
    private:
        int month;
        int day;
        int year;
    public:
        Date(int = 7, int = 4, int = 2012);
        void setDate(int, int, int);
        void showDate();
};
```

The name of this class is Date. Although the initial uppercase letter isn’t required, it’s used by convention to designate a class. The body of the class declaration section, enclosed in braces, consists of variable and method declarations. In this case, the data members month, day, and year are declared as integers, and three methods named Date(), setDate(), and showDate() are declared via prototypes. The keywords private and public are access specifiers that define access rights.

The private keyword specifies that the class members following it—in this case, month, day, and year—can be accessed only by using the class methods (or friend functions, as discussed in Section 11.1).⁴ The private designation is meant to enforce data security by requiring that all access to private data members be made through the provided member methods. This type of access, which prevents a user from seeing how data is actually stored, is referred to as data hiding. After a class category such as private is designated, it remains in force until a new category is listed.

In this Date class, a date is stored by using three integers for the month, day, and year. In addition, the year will always be stored as a four-digit number. For example, the year 1998 is stored as 1998, not as 98. Making sure to store all years with their century designation eliminates a multitude of problems that can crop up if only the last two digits are stored. For example, the number of years between 2012 and 1999 can be calculated quickly as 2012 - 1999 = 13 years, but getting this same answer isn’t as easy with the year values 12 and 99. Additionally, with four digits, it’s clear what the year 2012 refers to, but the two-digit value 12 could refer to 1912 or 2012.

Following the private class data members, the method prototypes listed in the Date class have been declared as public. This means these class methods can be called by any objects and functions not in the class (from outside the class, in other words). In general, all class methods should be public so that they provide capabilities to manipulate class variables from outside the class.

The Date class provides three methods named Date(), setDate(), and showDate(). Notice that one of these member methods has the same name, Date, as the class name. It’s referred to as a constructor method, and it has a special purpose: It can be used to initialize class data members with values. The default values used for this method are the numbers 7, 4, and 2012, which, as you see shortly, are used as the default month, day, and year values. Note that the default year is represented as a four-digit integer to retain the century designation. Also, notice that the constructor method has no return type, which is a requirement for this special method. The two remaining methods declared in the Date class, setDate() and showDate(), have been declared as returning no value (void).

The class implementation section is where the member methods declared in the declaration section are written to permit the initialization, assignment, and display capabilities implied by their names. The following example shows the general form of methods written in the implementation section. This format is correct for all methods except the constructor, which, as stated previously, has no return type:

```
returnType className::methodName(parameter list)
{
    method body
}
```

As this example shows, member methods defined in the class implementation section have the same format as all user-written C++ functions, with the addition of the class name and scope resolution operator, ::, that identifies the method as a member of a particular class. Now take another look at the implementation section of the Date class, which is repeated for convenience:

```
// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

```
void Date::setDate(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    return;
}
```

```
void Date::showDate()
{
    cout << "The Date is ";
    cout << setfill('0')
         << setw(2) << month << '/'
         << setw(2) << day << '/'
         << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
    return;
}
```

Notice that the first method in this implementation section has the same name as the class, which makes it a constructor method. Therefore, it has no return type. The Date:: at the beginning of the header identifies this method as a member of the Date class. The rest of the header

```
Date(int mm, int dd, int yyyy)
```

defines the method as having three integer parameters. The body of this method simply assigns the data members month, day, and year with the values of the parameters mm, dd, and yyyy.

The next header

```
void Date::setDate(int mm, int dd, int yyyy)
```

defines setDate() as belonging to the Date class (Date::). This method returns no value (void) and expects three integer parameters: mm, dd, and yyyy. In a manner similar to the Date() method, the body of this method assigns the data members month, day, and year the values of its parameters.

Finally, the last header in the class implementation section

```
void Date::showDate()
```

defines a method named showDate(). This method has no parameters, returns no value, and is a member of the Date class. The body of this method, however, needs a little more explanation.

Although all years have been stored as four-digit values to retain century information, users are accustomed to seeing dates with the year represented as a two-digit value, such as 12/15/12. To display the last two digits of the year value, the expression year % 100 can be used. For example, if the year is 1999, the expression 1999 % 100 yields the value 99, and if the year is 2012, the expression 2012 % 100 yields the value 12.

If you had used an assignment statement such as year = year % 100;, however, you would actually be altering the stored value of year to correspond to the last two digits of the

year. Because you want to retain the year as a four-digit number, you must be careful to manipulate only the displayed value by using the expression year % 100 in the cout statement. The setfill and setw manipulators are used to make sure the displayed values correspond to conventionally accepted dates. For example, the date March 9, 2008, should appear as 3/09/08 or 03/09/08. The setw manipulator forces each value to be displayed in a field width of 2. Because this manipulator remains in effect only for the next insertion, it's used before the display of each date value. Because the setfill manipulator remains in effect until the fill character is changed, however, it must be included only once. The setfill manipulator has been used to change the fill character from the default of a blank space to the character 0. Doing this ensures that a date such as December 9, 2009 appears as 12/09/09, not as 12/ 9/ 9.

To see how the date class can be used in the context of a complete program, take a look at Program 10.1. To make the program easier to read, the shaded area contains the class declaration and implementation sections. The unshaded area contains the header and main() function. This shading is used in the remainder of the book for all programs using classes.

# Program 10.1

```
#include <iostream>
#include <iomanip>
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
    Date(int = 7, int = 4, int = 2012); // constructor
    void setDate(int, int, int);      // member method to copy a date
    void showDate();                  // member method to display a date
};
// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

> aThis shading isn't accidental. In practice, the shaded area containing the class definition is placed in a separate file. A single #include statement is then used to include this class declaration in the program. The final program would consist of the unshaded areas in Program 10.1, with the addition of another #include statement.
