

```cpp
void setName(string first, string last);
    //Function to set firstName and lastName according
    //to the parameters.
    //Postcondition: firstName = first; lastName = last

string getFirstName() const;
    //Function to return the first name.
    //Postcondition: The value of firstName is returned.

string getLastName() const;
    //Function to return the last name.
    //Postcondition: The value of lastName is returned.

personType(string first = "", string last = "");
    //Constructor
    //Sets firstName and lastName according to the parameters.
    //The default values of the parameters are null strings.
    //Postcondition: firstName = first; lastName = last

private:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```

Figure 10-11 shows the UML class diagram of the class personType.

![](img/b217c421655b51e7494cf3b89bb5432d_745_0.png)

FIGURE 10-11  UML class diagram of the class personType

We now give the definitions of the member functions of the class personType.

```cpp
void personType::print() const
{
    cout << firstName << " " << lastName;
}

void personType::setName(string first, string last)
{
    firstName = first;
    lastName = last;
}
```

```cpp
string personType::getFirstName() const
{
    return firstName;
}

string personType::getLastName() const
{
    return lastName;
}

//constructor
personType::personType(string first, string last)
{
    firstName = first;
    lastName = last;
}
```

### EXAMPLE 10-11

In this example, we design and implement a class to manipulate an integer. Consider the integer 620385147907652638. Some of the operations that can be performed on this integer are: count the number of even digits, odd digits, and zeros; find the sum of the digits; reverse the digits; split the number into blocks of three-digit numbers; and find the sum of these numbers. The following class defines some of these operations.

```cpp
class integerManipulation
{
public:
    void setNum(long long n);
        //Function to set num.
        //Postcondition: num = n;

    long long getNum();
        //Function to return num.
        //Postcondition: The value of num is returned.

    void reverseNum();
        //Function to reverse the digits of num.
        //Postcondition: revNum is set to num with digits in
        //               the reverse order.

    void classifyDigits();
        //Function to count the even, odd, and zero digits of num.
        //Postcondition: evensCount = the number of even digits
        //                           in num.
        //               oddsCount = the number of odd digits in num.

    int getEvensCount();
        //Function to return the number of even digits in num.
        //Postcondition: The value of evensCount is returned.

    int getOddsCount();
        //Function to return the number of odd digits in num.
        //Postcondition: The value of oddsCount is returned.

    int getZerosCount();
        //Function to return the number of zeros in num.
        //Postcondition: The value of zerosCount is returned.

    int sumDigits();
        //Function to return the sum of the digits of num.
        //Postcondition: The sum of the digits is returned.

    integerManipulation(long long n = 0);
        //Constructor with a default parameter.
        //The instance variable num is set according to the
        //parameter, and other instance variables are
        //set to zero.
        //The default value of num is 0;
        //Postcondition: num = n; revNum = 0; evensCount = 0;
        //              oddsCount = 0; zerosCount = 0;

private:
    long long num;
    long long revNum;
    int evensCount;
    int oddsCount;
    int zerosCount;
};
```

The definition of some of the member functions are:

```cpp
void integerManipulation::setNum(long long n)
{
    num = n;
}

long long integerManipulation::getNum()
{
    return num;
}

void integerManipulation::reverseNum()
{
    cout << "See Programming Exercise 9 in Chapter 6." << endl;
}

void integerManipulation::classifyDigits()
{
    long long temp;

    temp = abs(num);

    int digit;

    while (temp != 0)
    {
        digit = temp - (temp / 10) * 10;
        temp = temp / 10;

        if (digit % 2 == 0)
        {
            evensCount++;
            if (digit == 0)
                zerosCount++;
        }
        else
            oddsCount++;
    }
}

int integerManipulation::getEvensCount()
{
    return evensCount;
}

int integerManipulation::getOddsCount()
{
    return oddsCount;
}

int integerManipulation::getZerosCount()
{
    return zerosCount;
}

int integerManipulation::sumDigits()
{
    cout << "See Programming Exercise 1 in Chapter 5." << endl;

    return 0;
}

integerManipulation::integerManipulation(long long n)
{
    num = n;
    revNum = 0;
    evensCount = 0;
    oddsCount = 0;
    zerosCount = 0;
}
```

The following program shows how to use this class in a program.

```cpp
//The user program that uses the class integerManipulation

#include <iostream>                         //Line 1
#include "integerManipulation.h"            //Line 2

using namespace std;                        //Line 3

int main()                                  //Line 4
{                                           //Line 5
    integerManipulation number;             //Line 6

    long long num;                          //Line 7

    cout << "Enter an integer: ";           //Line 8
    cin >> num;                             //Line 9
    cout << endl;                           //Line 10

    number.setNum(num);                     //Line 11

    number.classifyDigits();                //Line 12

    cout << number.getNum() << endl
         << "The number of even digits: "
         << number.getEvensCount() << endl
         << "The number of zeros: "
         << number.getZerosCount() << endl
         << "The number of odd digits: "
         << number.getOddsCount() << endl;  //Line 13

    return 0;                               //Line 14
} //end main                                //Line 15
```

**Sample Run:** In this sample run, the user input is shaded.

```
Enter an integer: 6203851479017652638

6203851479017652638
The number of even digits: 10
The number of zeros: 2
The number of odd digits: 9
```

Programming Exercise 24, at the end of this chapter, asks you to write the definition of the functions of the class `integerManipulation` that are not given.

## Inline Functions

The definition of the class `clockType` contains the declarations of the data members and the function prototypes of the member functions. The definitions of the member functions are placed in the implementations file. However, in the definition of the class you can give the complete definition of a member function. Such member functions definitions are called **inline function definitions**. Suppose that you want to include a function to return the hours of a clock. You can write the definition of the class `clockType` as follows:

```cpp
class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
    void getTime(int& hours, int& minutes, int& seconds) const;
    void printTime() const;

    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();

    bool equalTime(const clockType& otherClock) const;

    int getHours() const
    {
        return hr;
    }

    clockType(int hours = 0, int minutes = 0,
              int seconds = 0);

private:
    int hr;
    int min;
    int sec;
};
```

In this definition of the class, the function `getHours` is inline. Inline function definitions are typically used for very short function definitions. The compiler treats inline functions in a special way. It typically inserts the code of an inline function at every location the function is called. When a function is called, memory for its parameters and local variables is allocated and when the function exits the memory is deallocated. So there is an overhead when calling a function. In the case of an inline function the overhead of a function invocation is saved. In general, very short definitions should be defined as inline functions.

## Static Members of a Class

> **NOTE**  This section may be skipped without any loss of continuation.

In Chapter 6, we described two types of variables: automatic and static. Recall that if a local variable of a function is `static`, it exists between function calls. Similar to static variables, a class can have static members, functions, or variables. Let us note the following about the static members of a class:

- If a function of a class is `static`, in the class definition it is declared using the keyword `static` in its heading.

