
```cpp
int getNum() const;
//Function to return the number on the top face of the die.
//Returns the value of the instance variable num.

private:
    int num;
};

The definitions of the member functions are given next.

die::die()
{
    num = 1;
    srand(time(0));
}

int die::roll()
{
    num = rand() % 6 + 1;

    return num;
}

int die::getNum() const
{
    return num;
}
```

The following program shows how to use the class die in a program:

```cpp
//The user program that uses the class die
#include <iostream>
#include "die.h"

using namespace std;

int main()
{
    die die1;                                      //Line 1
    die die2;                                      //Line 2

    cout << "Line 4: die1: " << die1.getNum() << endl; //Line 4

    cout << "Line 5: die2: " << die2.getNum() << endl; //Line 5

    cout << "Line 6: After rolling die1:"
         << die1.roll() << endl;                   //Line 6

    cout << "Line 7: After rolling die2:"
         << die2.roll() << endl;                   //Line 7
    cout << "Line 8: The sum of the numbers rolled"
         << " by the dice is: "
         << die1.getNum() + die2.getNum() << endl;  //Line 8

    cout << "Line 9: After again rolling, the sum of "
         << "the numbers rolled is: "
         << die1.roll() + die2.roll() << endl;        //Line 9

    return 0;                                          //Line 10
} //end main                                      //Line 11
```

```text
Sample Run:

Line 4: die1: 1
Line 5: die2: 1
Line 6: After rolling die1: 3
Line 7: After rolling die2: 4
Line 8: The sum of the numbers rolled by the dice is: 7
Line 9: After again rolling, the sum of the numbers rolled is: 5
```

The preceding program works as follows. The statements in Lines 2 and 3 create the objects die1 and die2, and, using the default constructor, set both the dice to 1. The statements in Lines 4 and 5 output the number of both the dice. The statement in Line 6 rolls die1 and outputs the number rolled. Similarly, the statement in Line 7 rolls die2 and outputs the number rolled. The statement in Line 8 outputs the sum of the numbers rolled by die1 and die2. The statement in Line 9 again rolls both the dice and outputs the sum of the numbers rolled.

Example 10-10 further illustrates how classes are designed and implemented. The class personType that is designed in Example 10-10 is very useful; we will use this class in subsequent chapters.

## EXAMPLE 10-10

The most common attributes of a person are the person’s first and last name. The typical operations on a person’s name are to set the name and print the name. The following statements define a class with these properties.

```cpp
#include <string>

using namespace std;

class personType
{
public:
    void print() const;
        //function to output the first name and last name
        //in the format firstName lastName

    void setName(string first, string last);
        //Function to set firstName and lastName according
        //to the parameters.
        //Postcondition: firstName = first; lastName = last;

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
        //Postcondition: firstName = first; lastName = last;

private:
    string firstName;  //variable to store the first name
    string lastName;   //variable to store the last name
};
```

Figure 10-11 shows the UML class diagram of the class personType.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_715_0.png)

**FIGURE 10-11** UML class diagram of the class *personType*

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

## Static Members of a Class

> **NOTE:** This section may be skipped without any loss of continuity.

In Chapter 6, we described two types of variables: automatic and static. Recall that if a local variable of a function is static, it exists between function calls. Similar to static variables, a class can have static members, functions, or variables. Let us note the following about the static members of a class:

- If a function of a class is static, in the class definition it is declared using the keyword `static` in its heading.
- If a member variable of a class is static, it is declared using the keyword `static`, as discussed in Chapter 6 and also illustrated in Example 10-11.
- A public static member, function, or variable of a class can be accessed using the class name and the scope resolution operator.

Example 10-11 clarifies the effect of the keyword `static`.

## EXAMPLE 10-11

Consider the following definition of the class illustrate:

```cpp
class illustrate
{
public:
    static int count;    //public static variable

    void print() const;
        //Function to output x, y, and count.

    void setX(int a);
        //Function to set x.
        //Postcondition: x = a;

    static void incrementY();
        //static function
        //Function to increment y by 1.
        //Postcondition: y = y + 1

    illustrate(int a = 0);
        //constructor
        //Postcondition: x = a;
        //              If no value is specified for a, x = 0;

private:
    int x;
    static int y;  //private static variable
};
```

Suppose that the static member variables and the definitions of the member functions of the class illustrate are as follows. (These statements are all placed in the implementation file. Also, notice that all static member variables are initialized, as shown below.)

```cpp
int illustrate::count = 0;
int illustrate::y = 0;

void illustrate::print() const
{
    cout << "x = " << x << ", y = " << y
         << ", count = " << count << endl;
}

void illustrate::setX(int a)
{
    x = a;
}

void illustrate::incrementY()
{
    y++;
}

illustrate::illustrate(int a)
{
    x = a;
}
```

Because the function `incrementY` is static and public, the following statement is legal:

```cpp
illustrate::incrementY();
```

Similarly, because the member variable `count` is static and public, the following statement is legal:

```cpp
illustrate::count++;
```

Next, we elaborate on static member variables a bit more. Suppose that you have a class, say, myClass, with member variables (static as well as non-static). When you create objects of type myClass, only non-static member variables of the class myClass become the member variables of each object. For each static member variable of a class, C++ allocates only one memory space. All myClass objects refer to the same memory space. In fact, static member variables of a class exist even when no object of that class type exists. You can access the public static member variables outside of the class, as explained earlier in this section.

Next, we explain how memory space is allocated for static and non-static member variables of a class.

Suppose that you have the class illustrate, as given in Example 10-10. Memory space then exists for the static member variables y and count.

Consider the following statements:

```cpp
illustrate illusObject1(3);    //Line 1
illustrate illusObject2(5);    //Line 2
```

The statements in Lines 1 and 2 declare illusObject1 and illusObject2 to be illustrate type objects (see Figure 10-12).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_718_0.png)

**FIGURE 10-12** illusObject1 and illusObject2

Now, consider the following statements:

```cpp
illustrate::incrementY();
illustrate::count++;
```
