
Because an accessor function only accesses the values of the member variables, as a safeguard, we typically include the reserved word *const* at the end of the headings of these functions. Moreover, a constant member function of a class cannot modify the member variables of that class. For example, see the headings of the member functions getTime, printTime, and equalTime of the class clockType.

A member function of a class is called a **constant function** if its heading contains the reserved word const at the end. For example, the member functions getTime, printTime, and equalTime of the **class clockType** are constant functions. A constant member function of a class cannot modify the member variables of that class, so these are accessor functions. One thing that should be remembered about constant member functions is that a constant member function of a class can *only* call other constant member functions of that class. Therefore, you should be careful when you make a member function constant.

Example 10-2 shows how to use the **class clockType** in a program. Note that we have combined the definition of the class, the definition of the member functions, and the main function to create a complete program. Later in this chapter, you will learn how to separate the definition of the **class clockType**, the definitions of the member functions, and the main program, using three files.

## EXAMPLE 10-2

```cpp
//The program listing of the program that defines
//and uses the class clockType

#include <iostream>
using namespace std;

class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

private:
    int hr;
    int min;
    int sec;
};

int main()
{
    clockType myClock;
    clockType yourClock;
    int hours;
    int minutes;
    int seconds;

    //Set the time of myClock
    myClock.setTime(5, 4, 30);                              //Line 1

    cout << "Line 2: myClock: ";                         //Line 2
    myClock.printTime();  //print the time of myClock      //Line 3
    cout << endl;                                          //Line 4

    cout << "Line 5: yourClock: ";                        //Line 5
    yourClock.printTime(); //print the time of yourClock   //Line 6
    cout << endl;                                          //Line 7

    //Set the time of yourClock
    yourClock.setTime(5, 45, 16);                          //Line 8

    cout << "Line 9: After setting yourClock: ";           //Line 9
    yourClock.printTime(); //print the time of yourClock  //Line 10
    cout << endl;                                          //Line 11

    //Compare myClock and yourClock
    if (myClock.equalTime(yourClock))                       //Line 12
        cout << "Line 13: Both times are equal."
             << endl;                                      //Line 13
    else                                                    //Line 14
        cout << "Line 15: The two times are not equal."
             << endl;                                      //Line 15

    cout << "Line 16: Enter the hours, minutes, and "      //Line 16
         << "seconds: ";
    cin >> hours >> minutes >> seconds;                    //Line 17
    cout << endl;                                          //Line 18

    //Set the time of myClock using the value of the
    //variables hours, minutes, and seconds
    myClock.setTime(hours, minutes, seconds);               //Line 19

    cout << "Line 20: New myClock: ";                       //Line 20
    myClock.printTime();  //print the time of myClock      //Line 21
    cout << endl;                                          //Line 22

    //Increment the time of myClock by one second
    myClock.incrementSeconds();                             //Line 23

    cout << "Line 24: After incrementing myClock by "
         << "one second, myClock: ";                       //Line 24
    myClock.printTime();  //print the time of myClock      //Line 25
    cout << endl;                                          //Line 26

    //Retrieve the hours, minutes, and seconds of the
    //object myClock
    myClock.getTime(hours, minutes, seconds);              //Line 27

    //Output the value of hours, minutes, and seconds
    cout << "Line 28: hours = " << hours
         << ", minutes = " << minutes
         << ", seconds = " << seconds << endl;            //Line 28

    return 0;
}//end main

void clockType::setTime(int hours, int minutes, int seconds)
{
    if (0 <= hours && hours < 24)
        hr = hours;
    else
        hr = 0;

    if (0 <= minutes && minutes < 60)
        min = minutes;
    else
        min = 0;

    if (0 <= seconds && seconds < 60)
        sec = seconds;
    else
        sec = 0;
}

//Place the definitions of the remaining functions, getTime,
//incrementHours, incrementMinutes, incrementSeconds, printTime,
//and equalTime, of the class clockType, as described
//previously.
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 2: myClock: 05:04:30
Line 5: yourClock: -858993460:-858993460:-858993460
Line 9: After setting yourClock: 05:45:16
Line 15: The two times are not equal.
Line 16: Enter the hours, minutes, and seconds: 5 23 59

Line 20: New myClock: 05:23:59
Line 24: After incrementing myClock by one second, myClock: 05:24:00
Line 28: hours = 5, minutes = 24, seconds = 0
```

The value of yourClock, as printed in the second line of the output (Line 5), is machine dependent; you might get different values.

```cpp
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
};
```

## EXAMPLE 10-5

```cpp
class clockType
{
    int hr;
    int min;
    int sec;

public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
};
```

In Example 10-5, because the identifiers hr, min, and sec do not follow any member access specifier, they are by default *private*.

It is a common practice to list all of the *public* members first and then the *private* members. This way, you can focus your attention on the *public* members.

## Constructors

In the program in Example 10-2, when we printed the value of yourClock without calling the function setTime, the output was some strange numbers (see the output of Line 5 in the sample run). This is due to the fact that C++ does not automatically initialize the variables. Because the *private* members of a class cannot be accessed outside of the class (in our case, the member variables), if the user forgets to initialize these variables by calling the function setTime, the program will produce erroneous results.

To guarantee that the member variables of a class are initialized, you use constructors. There are two types of constructors: with parameters and without parameters. The constructor without parameters is called the **default constructor**.

Constructors have the following properties:

- The name of a constructor is the same as the name of the class.
- A constructor is a function and it has no type. That is, it is neither a value-returning function nor a void function.
- A class can have more than one constructor. However, all constructors of a class have the same name.
- If a class has more than one constructor, the constructors must have different formal parameter lists. That is, either they have a different number of formal parameters or, if the number of formal parameters is the same, then the data type of the formal parameters, in the order you list, must differ in at least one position. In other words, like function overloading, a constructor's name is overloaded.
- Constructors execute automatically when a class object is declared and enters its scope. Because they have no types, they cannot be called like other functions.
- Which constructor executes depends on the types of values passed to the class object when the class object is declared.

Let us extend the definition of the `class clockType` by including two constructors:

```cpp
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
    clockType(int, int, int);  //constructor with parameters
    clockType();               //default constructor

private:
    int hr;
    int min;
    int sec;
};
```

This definition of the `class clockType` includes two constructors: one with three parameters and one without any parameters. Let us now write the definitions of these constructors:
