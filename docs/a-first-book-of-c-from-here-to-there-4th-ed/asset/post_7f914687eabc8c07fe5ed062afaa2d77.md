
void Date::setDate(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
    return;
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
    Date a, b, c(4,1,2000);  // declare 3 objects
    b.setDate(12,25,2009);  // assign values to b's data members
    a.showDate();           // display object a's values
    b.showDate();           // display object b's values
    c.showDate();           // display object c's values
    return 0;
}

The class declaration and implementation sections in the shaded area of Program 10.1 should look familiar to you. Notice, however, that this area only declares the class; it doesn't create any variables of this class type. This is true of all C++ types, including the built-in types, such as integers and doubles. Just as a variable of an integer type must be defined, variables of a user-declared class must also be defined. Variables defined to be of a user-declared class are referred to as objects.

Using this new terminology, the first statement in Program 10.1's main() function defines three objects—named a, b, and c—to be of the class type Date. In C++, when a new object is defined, memory is allocated for the object, and its data members are initialized automatically by a call to the class constructor method. For example, examine the definition Date a, b, c(4,1,2000); in main(). When the object named a is defined, the constructor

## Point of Information

## Interfaces, Implementations, and Data Hiding

The terms “interface” and “implementation” are used extensively in object-oriented programming literature and can be equated to specific parts of a class’s declaration and implementation sections.

An interface consists of a class’s public member method declarations and any supporting comments. The implementation consists of both the class implementation section (containing private and public member definitions) and the class’s private data members, which are defined in the class declaration section.

The implementation is the means of providing data hiding, which generally refers to the principle that how a class is constructed internally isn’t relevant to programmers who want to use the class. The implementation can and should be hidden from all class users to ensure that the class isn’t altered or compromised in any way. All that a programmer needs to know to use a class correctly should be provided by the interface.

The last three statements in main() call the showDate() method to operate on the a, b, and c objects. The first call results in the display of a’s data values, the second call in the display of b’s data values, and the third call in the display of c’s data values. Therefore, the output of Program 10.1 is the following:

```
The date is 07/04/12
The date is 12/25/09
The date is 04/01/00
```

Notice that a statement such as cout << a; is invalid inside main() because cout doesn’t know how to handle an object of class Date. Therefore, the Date class is supplied with a method that can be used to access and display an object’s internal values.

## Terminology

As there’s sometimes confusion about the terms classes, objects, and other object-oriented programming terminology, taking a moment to clarify and review the terminology is helpful.

A class is a programmer-defined data type from which objects can be created. Objects are created from classes; they have the same relationship to classes as variables do to C++’s built-in data types. For example, in the declaration

```
int a;
```

a is said to be a variable, and in the Program 10.1 declaration

```
Date a;
```

a is said to be an object. If it helps you to think of an object as a variable, do so.

Objects are also referred to as instances of a class, and the process of creating a new object is often referred to as an instantiation of the object. Each time a new object is instantiated (created), a new set of data members belonging to the object is created.¹ The values contained in these data members determine the object’s state.

Seen in this way, a class can be thought of as a blueprint for creating particular instances (objects). Each instance (object) of a class has its own set of values for the set of data members specified in the class declaration section.

In addition to the data types allowed for an object, a class also defines behavior—that is, the operations permitted to be performed on an object’s data members. Users of the object need to know what these methods can do and how to activate them through method calls but generally don’t need to know how the operation is done. The actual implementation details of an object’s operations are in the class implementation, which can (and should) be hidden from the user. Other names for the operations defined in a class implementation section are procedures, functions, services, and methods. These terms are used interchangeably throughout the remainder of the book.

## EXERCISES 10.2

- 1. (Review) Define the following terms:
  - a. Class
  - b. Object
  - c. Declaration section
  - d. Implementation section
  - e. Instance variable
  - f. Member method
  - g. Data member
  - h. Constructor
  - i. Class instance
  - j. Services
  - k. Methods
  - l. Interface

- 2. (Practice) Write a class declaration section for each of the following specifications. In each case, include a prototype for a constructor and a member method named showData() that can be used to display data member values.
  - a. A class named Time that has integer data members named secs, mins, and hours
  - b. A class named Complex that has double-precision data members named real and imaginary
  - c. A class named Circle that has integer data members named xcenter and ycenter and a double-precision data member named radius
  - d. A class named System that has character data members named computer, printer, and screen, each capable of holding 30 characters (including the end-of-string NULL), and double-precision data members named compPrice, printPrice, and scrnPrice

3. (Practice) a. Construct a class implementation section for the constructor and showData() member methods corresponding to the class declaration created for Exercise 2a.
b. Construct a class implementation section for the constructor and showData() methods corresponding to the class declaration created for Exercise 2b.
c. Construct a class implementation section for the constructor and showData() methods corresponding to the class declaration created for Exercise 2c.
d. Construct a class implementation section for the constructor and showData() methods corresponding to the class declaration created for Exercise 2d.

4. (Program) a. Include the class declaration and implementation sections prepared for Exercises 2a and 3a in a complete working program.
b. Include the class declaration and implementation sections prepared for Exercises 2b and 3b in a complete working program.
c. Include the class declaration and implementation sections prepared for Exercises 2c and 3c in a complete working program.
d. Include the class declaration and implementation sections prepared for Exercises 2d and 3d in a complete working program.

5. (Desk check) Determine the errors in the following class declaration section:

```
class Employee
{
public:
    int empnum;
    char code;
private:
    class(int = 0);
    void showemp(int, char);
};
```

6. (Modify) a. Add another member method named convert() to Program 10.1 that does the following: The method should access the month, year, and day data members and display and then return an integer calculated as year × 10000 + month × 100 + day. For example, if the date is 4/1/2014, the returned value is 20140401. (Dates in this form are useful when performing sorts because placing the numbers in numerical order automatically places the corresponding dates in chronological order.)
b. Include the modified Date class constructed for Exercise 6a in a complete C++ program.

7. (Modify) a. Add to Program 10.1's class definition an additional member method named leapyr() that returns a true if the year is a leap year and a false if it's not a leap year. A leap year is any year that's evenly divisible by 4 but not by 100, with the exception that all years evenly divisible by 400 are leap years. For example, the year 1996 is a leap year because it's evenly divisible by 4 and not evenly divisible by 100. The year 2000 is a leap year because it's evenly divisible by 400.
b. Include the class definition constructed for Exercise 7a in a complete C++ program. The main() function should display the message The year is a leap year or the message The year is not a leap year (depending on the Date object's year value).
