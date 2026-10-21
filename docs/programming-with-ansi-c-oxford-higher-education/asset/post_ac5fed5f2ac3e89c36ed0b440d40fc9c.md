
This example also illustrates how a class can become a friend of another and how useful it is. Another possibility is that of having a friend class that provides useful though general utilities such as GUI input/output using message boxes as discussed earlier.

## 4.12 const AND volatile FUNCTIONS

Like C, the const and volatile variables are available in C++. However, it is also possible to have const and volatile functions in C++ additionally, unlike in C. A brief introduction is provided in the following sections.

### 4.12.1 const Functions

Constant objects have already been discussed in Chapter 3 and the definition of a const function was shown in Program 3.12. They are defined by placing the keyword const between the argument list and the body of the function.

> Note A const function can operate on either constant or non-constant objects; however, it cannot modify the objects of the class.

```
<return type><function name>(argument1, argument2, ...) const
{
    <The body of the function>
}
```

Program 3.12 in Chapter 3 contains the following function:

```
void PrintDetails()const
/* This function is now constant; it cannot modify
an object of the class student */
{
    cout << "Roll number is " << RollNumber << "\n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";
}
```

If this function is modified as follows, we get errors while compiling the program.

```
void PrintDetails()const
{
    cout << "Roll number is" << RollNumber << " \n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";
    RollNumber = 4;    // This is erroneous
}
```

> Note It is a good programming practice to define member functions as constant when they should not modify the invoking objects. So, later on, if the functions are accidentally modified to change the values of data members, the error can be caught during compilation.

### 4.12.2 Mutable Data Members

Ordinary data members, as we have seen, cannot be modified by const functions. What if we want a special data member to be modified by a function? If we do not declare the member

A mutable member can be modified even by the const functions.

function as const, it cannot access constant objects. Declaration of a special data member as mutable is the solution here. When a data member is declared mutable, it can be modified even by the const functions.

A volatile function is a function that can only act on volatile objects.

In the example given, if RollNumber definition is changed to

```
mutable int RollNumber;
```

in the student class, then the statement

```
void PrintDetails() const
{
    ...
    RollNumber = 4;
}
```

will no longer result in an error. There is no difference between a normal data member and a mutable data member for a normal member function.

### 4.12.3 volatile Functions

A member function can also be declared as volatile if it is invoked by a volatile object. A volatile object’s value can be changed by external parameters, which are not under the control of the program. For example, an object taking an input from a network interface card does not take input from our program. As and when the hardware interrupts, the values related to it change without our program’s knowledge.

A sample definition of a volatile function and a volatile object are shown in the following code:

Static functions deal with static variables alone. It is always possible to replace a static function with a normal function; however using a static function makes the program more readable and also reduces the chances of accidental changes.

```
class NICClass
{
public:
    void CheckValuesForNIC volatile
    // A volatile function definition
    {
        // Function body
    }
    ...
};
volatile NICClass NICObject;
// A volatile object definition
```

## 4.13 STATIC FUNCTIONS

Some utilities are generic to a set of objects. We have seen the case of dealing with a collection of objects. The utility or the operation does not address a singleton object but works on multiple objects. At times, we need to provide operations that refer to all the objects, such as finding out how many objects are created at the moment. Such cases need static variables, discussed in Chapter 3. We can see that a static variable is an ideal choice for the variable that represents a number of objects alive at the moment. Program 4.11 shows how a static function can be used instead of a member or non-member function.

> Note Non-member functions are similar to normal C functions. If we define them as static, they become local to the file in which they are defined. In other words, the scope of that function is the body of the file within which the function is defined.

Program 4.11 is the modified version of the progam in Chapter 3 that counts the number of students defined at the moment. A static function is used here for displaying the total number of students.

### PROGRAM 4.11 Static functions for counting the number of students

```
// StaticFunction.cpp
#include <iostream>
#include <string>
using namespace std;

class student
{
public:
    static int TotalStudents;
    static void DispTotal();
    // Declaration of a static member function

private:
    int RollNumber;
    string Name;
    string Address;

public:
    void SetDetails(int Roll, string StudentName, string StudentAddress)
    {
        RollNumber = Roll;
        Name = StudentName;
        Address = StudentAddress;
        TotalStudents++;
    }

    void PrintDetails()
    {
        cout << "Roll number is " << RollNumber << "\n";
        cout << "Name is " << Name << "\n";
        cout << "Address is " << Address << "\n";
    }
};

int student::TotalStudents;
void student::DispTotal()
/* See how the function name is preceded with the class name similar to a member function */
{
    cout << "Total students at the moment" << student::TotalStudents << "\n";
}

void main()
{
    student::DispTotal();
    student Robin;

    Robin.SetDetails(1, "Robin Singh", "New Delhi");
    Robin.PrintDetails();
    student::DispTotal();

student Sonia;
Sonia.SetDetails(2, "Mathur", "Mumbai");
Sonia.PrintDetails();
student::DispTotal();

if(true)
{
    student Anita;
    Anita.SetDetails(3, "Sharma", "Indore");
    Anita.PrintDetails();
    student::DispTotal();
}
cout << "Anita departs! \n";
/* The following will not work as expected. Total students are still three */
student::DispTotal();
}
```

### How the Program Works

DispTotal() is a new function defined as static. A static function is very similar to a non-member function, with the only difference that it is now bound and known only to the class in which it is defined. It should be remembered that non-member functions are known to all the classes of the program. The static functions, similar to member functions, can be invoked only by the objects of the class in which they are declared as static. They can be invoked directly by their name with the class name and scope resolution operator preceding it.

> Note In C, if a function is declared as static, it will be treated local to the file in which it is defined. The same concept is applied in the case of a non-member. A static non-member function is local to the file and is not accessible outside that physical file.

The manner in which a static function is defined and used should be noted. Like a non-member function, a static function is defined outside the class. At the same time, it is preceded by the class name and the scope resolution operator, just like a member function defined outside the class.

```
void student::DispTotal()
```

DispTotal() is a static function that is used to display the total number of students and TotalStudents is also a static variable. This did not happen by accident; a static function can act upon only the static variables of the class and cannot have access to other data members of the class. It can also have access to global functions and data.

The most important advantage of static functions is that they increase the readability of the program. Instead of calling Shyam.DispTotal, where Shyam is just a dummy object for counting the total students, we can call student::DispTotal, that is, it should be preceded by the class name, which is far more readable.

### 4.13.1 Restrictions on Static Function

Static functions have some restrictions as well. Some of the important ones are as follows:

- 1. They do not have the this pointer because they are not member functions in the true sense. This is why they cannot access the member variables.
- 2. They cannot access other data members of the class because doing so will implicitly call the this pointer. (Remember: RollNumber is the same as this -> RollNumber.)
