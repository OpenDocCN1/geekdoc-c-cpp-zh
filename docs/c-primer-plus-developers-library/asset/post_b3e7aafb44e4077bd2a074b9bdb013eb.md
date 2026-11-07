
- a. What's wrong with this default constructor?

```cpp
String::String() {}
```

- b. What's wrong with this constructor?

```cpp
String::String(const char * s)
{
    str = s;
    len = strlen(s);
}
```

- c. What's wrong with this constructor?

```cpp
String::String(const char * s)
{
    strcpy(str, s);
    len = strlen(s);
}
```

- 2. Name three problems that may arise if you define a class in which a pointer member is initialized by using `new`. Indicate how they can be remedied.

- 3. What class methods does the compiler generate automatically if you don't provide them explicitly? Describe how these implicitly generated functions behave.

- 4. Identify and correct the errors in the following class declaration:

```cpp
class nifty
{
// data
    char personality[];
    int talents;
// methods
    nifty();
    nifty(char * s);
    ostream & operator<<(ostream & os, nifty & n);
}
```

```cpp
nifty::nifty()
{
    personality = NULL;
    talents = 0;
}
```

```cpp
nifty::nifty(char * s)
{
    personality = new char [strlen(s)];
    personality = s;
    talents = 0;
}
```

```cpp
ostream & nifty::operator<<(ostream & os, nifty & n)
{
    os << n;
}
```

- 5. Consider the following class declaration:

```cpp
class Golfer
{
private:
    char * fullname;        // points to string containing golfer's name
    int games;              // holds number of golf games played
    int * scores;           // points to first element of array of golf scores
public:
    Golfer();
    Golfer(const char * name, int g = 0);
    // creates empty dynamic array of g elements if g > 0
    Golfer(const Golfer & g);
    ~Golfer();
};
```

    - a. What class methods would be invoked by each of the following statements?

```cpp
Golfer nancy;                     // #1
Golfer lulu("Little Lulu");       // #2
Golfer roy("Boy Hobbs", 12);      // #3
Golfer * par = new Golfer;        // #4
Golfer next = lulu;               // #5
Golfer hazard = "Weed Thwacker";  // #6
*par = nancy;                     // #7
nancy = "Nancy Putter";           // #8
```

    - b. Clearly, the class requires several more methods to make it useful. What additional method does it require to protect against data corruption?

### Programming Exercises

- 1. Consider the following class declaration:

```cpp
class Cow {
    char name[20];
    char * hobby;
    double weight;
public:
    Cow();
    Cow(const char * nm, const char * ho, double wt);
    Cow(const Cow & c);
    ~Cow();
    Cow & operator=(const Cow & c);
    void ShowCow() const;  // display all cow data
};
```

Provide the implementation for this class and write a short program that uses all the member functions.

- 2. Enhance the `String` class declaration (that is, upgrade `string1.h` to `string2.h`) by doing the following:
    - a. Overload the `+` operator to allow you to join two strings into one.
    - b. Provide a `stringlow()` member function that converts all alphabetic characters in a string to lowercase. (Don't forget the `cctype` family of character functions.)
    - c. Provide a `stringup()` member function that converts all alphabetic characters in a string to uppercase.
    - d. Provide a member function that takes a `char` argument and returns the number of times the character appears in the string.

Test your work in the following program:

```cpp
// pe12_2.cpp
#include <iostream>
using namespace std;
#include "string2.h"
int main()
{
    String s1(" and I am a C++ student.");
    String s2 = "Please enter your name: ";
    String s3;
    cout << s2;                    // overloaded << operator
    cin >> s3;                     // overloaded >> operator
    s2 = "My name is " + s3;       // overloaded =, + operators
    cout << s2 << ".\n";
    s2 = s2 + s1;
    s2.stringup();                 // converts string to uppercase
    cout << "The string\n" << s2 << "\ncontains " << s2.has('A')
         << " 'A' characters in it.\n";
    s1 = "red";                    // String(const char *),
                                   // then String & operator=(const String&)
    String rgb[3] = { String(s1), String("green"), String("blue")};
    cout << "Enter the name of a primary color for mixing light: ";
    String ans;
    bool success = false;
    while (cin >> ans)
    {
        ans.stringlow();        // converts string to lowercase
        for (int i = 0; i < 3; i++)
        {
            if (ans == rgb[i])  // overloaded == operator
            {
                cout << "That's right!\n";
                success = true;
                break;
            }
        }
        if (success)
            break;
        else
            cout << "Try again!\n";
    }
    cout << "Bye\n";
    return 0;
}
```

Your output should look like this sample run:

```text
Please enter your name: Fretta Farbo
My name is Fretta Farbo.
The string
MY NAME IS FRETTA FARBO AND I AM A C++ STUDENT.
contains 6 'A' characters in it.
Enter the name of a primary color for mixing light: yellow
Try again!
BLUE
That's right!
Bye
```

- 3. Rewrite the Stock class, as described in Listings 10.7 and 10.8 in Chapter 10 so that it uses dynamically allocated memory directly instead of using string class objects to hold the stock names. Also replace the show() member function with an overloaded operator<<() definition. Test the new definition program in Listing 10.9.

- 4. Consider the following variation of the Stack class defined in Listing 10.10:

```cpp
// stack.h -- class declaration for the stack ADT
typedef unsigned long Item;

class Stack
{
private:
    enum {MAX = 10};        // constant specific to class
    Item * pitems;         // holds stack items
    int size;              // number of elements in stack
    int top;               // index for top stack item
public:
    Stack(int n = MAX);    // creates stack with n elements
    Stack(const Stack & st);
    ~Stack();
    bool isempty() const;
    bool isfull() const;
    // push() returns false if stack already is full, true otherwise
    bool push(const Item & item); // add item to stack
    // pop() returns false if stack already is empty, true otherwise
    bool pop(Item & item);         // pop top item
    Stack & operator=(const Stack & st);
};
```

As the private members suggest, this class uses a dynamically allocated array to hold the stack items. Rewrite the methods to fit this new representation and write a program that demonstrates all the methods, including the copy constructor and assignment operator.

- 5. The Bank of Heather has performed a study showing that ATM customers won’t wait more than one minute in line. Using the simulation from Listing 12.10, find a value for number of customers per hour that leads to an average wait time of one minute. (Use at least a 100-hour trial period.)

- 6. The Bank of Heather would like to know what would happen if it added a second ATM. Modify the simulation in this chapter so that it has two queues. Assume that a customer will join the first queue if it has fewer people in it than the second queue and that the customer will join the second queue otherwise. Again, find a value for number of customers per hour that leads to an average wait time of one minute. (Note: This is a nonlinear problem in that doubling the number of ATMs doesn’t double the number of customers who can be handled per hour with a one-minute wait maximum.)

This page intentionally left blank

## Class Inheritance

In this chapter you’ll learn about the following:

- Inheritance as an *is-a* relationship
- How to publicly derive one class from another
- Protected access
- Constructor member initializer lists
- Upcasting and downcasting
- Virtual member functions
- Early (static) binding and late (dynamic) binding
- Abstract base classes
- Pure virtual functions
- When and how to use public inheritance

One of the main goals of object-oriented programming is to provide reusable code. When you develop a new project, particularly if the project is large, it’s nice to be able to reuse proven code rather than to reinvent it. Employing old code saves time and because it has already been used and tested, can help suppress the introduction of bugs into a program. Also the less you have to concern yourself with details, the better you can concentrate on overall program strategy.

Traditional C function libraries provide reusability through predefined, precompiled functions, such as `strlen()` and `rand()`, that you can use in your programs. Many vendors furnish specialized C libraries that provide functions beyond those of the standard C library. For example, you can purchase libraries of database management functions and of screen control functions. However, function libraries have a limitation: Unless the vendor supplies the source code for its library functions (and often it doesn’t), you can’t extend or modify the functions to meet your particular needs. Instead, you have to shape your program to meet the workings of the library. Even if the vendor does supply the source code, you run the risk of unintentionally modifying how part of a function works or altering the relationships among library functions as you add your changes.
