
## Friend Functions

A friend function of a class is an ordinary function except that it has access to the private members of objects of that class. To make a function a friend of a class, you must list the function declaration for the friend function in the class definition. The function declaration is preceded by the keyword *friend*. The function declaration may be placed in either the private section or the public section, but it will be a public function in either case, so it is clearer to list it in the public section.

## SYNTAX (of a class definition with friend functions)

```
class ClassName
{
public:
    friend DeclarationForFriendFunction_1
    friend DeclarationForFriendFunction_2
             .
             .
             .
    MemberFunctionDeclarations
private:
    PrivateMemberDeclarations
};
```

> You need not list the friend functions first. You can intermix the order of these function declarations.

## EXAMPLE

```
class FuelTank
{
public:
    friend double needToFill(FuelTank tank);
    //Precondition: Member variables of tank have values.
    //Returns the number of liters needed to fill tank.
    FuelTank(double theCapacity, double theLevel);
    FuelTank();
    void input();
    void output();
private:
    double capacity;//in liters
    double level;
};
```

A friend function is not a member function. A friend function is defined and called the same way as an ordinary function. You do not use the dot operator in a call to a friend function and you do not use a type qualifier in the definition of a friend function.

member variable allCents, but with some compilers that would severely limit the amounts of money we could represent. In some implementations of C++, only 2 bytes are used to store the int type.¹ The result of the 2-byte implementation is that the largest value of type int is only slightly larger than 32000, but 32000 cents represents only $320, which is a fairly small amount of money. Since we may want to deal with amounts of money much larger than $320, we have used long for the type of the member variable allCents. C++ compilers that implement the int type in 2 bytes usually implement the type long in 4 bytes. Values of type long are integers just like the values of the type int, except that the 4-byte long implementation enables the largest allowable value of type long to be much larger than the largest allowable value of type int. On most systems the largest allowable value of type long is 2 billion or larger. (The type long is also called long int. The two names long and long int refer to the same type.)

The class Money has two operations that are friend functions: equal and add (which are defined in Display 11.3). The function add returns a Money object whose value is the sum of the values of its two arguments. A function call of the form equal(amount1, amount2) returns true if the two objects amount1 and amount2 have values that represent equal amounts of money.

Notice that the class Money reads and writes amounts of money as we normally write amounts of money, such as $9.95 or −$9.95. First, consider the member function input (also defined in Display 11.3). That function first reads a single character, which should be either the dollar sign (‘$’) or the minus sign (‘−’). If this first character is the minus sign, then the function remembers that the amount is negative by setting the value of the variable negative to true. It then reads an additional character, which should be the dollar sign. On the other hand, if the first symbol is not ‘−’, then negative is set equal to false. At this point the negative sign (if any) and the dollar sign have been read. The function input then reads the number of dollars as a value of type long and places the number of dollars in the local variable named dollars. After reading the dollars part of the input, the function input reads the remainder of the input as values of type char; it reads in three characters, which should be a decimal point and two digits.

(You might be tempted to define the member function input so that it reads the decimal point as a value of type char and then reads the number of cents as a value of type int. This is not done because of the way that some C++ compilers treat leading zeros. As explained in the Pitfall section entitled “Leading Zeros in Number Constants,” many compilers still in use do not read numbers with leading zeros as you would like them to, so an amount like $7.09 may be read incorrectly if your C++ code were to read the 09 as a value of type int.)

¹See Chapter 2 for details. Display 2.2 has a description of data types as most recent compilers implement them.

## DISPLAY 11.3 Money Class–Version 1 (part 1 of 4)

```
//Program to demonstrate the class Money.
#include <iostream>
#include <cstdlib>
#include <cctype>
using namespace std;

//Class for amounts of money in U.S. currency.
class Money
{
public:
    friend Money add(Money amount1, Money amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns the sum of the values of amount1 and amount2.
    
    friend bool equal(Money amount1, Money amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns true if the amount1 and amount2 have the same value;
    //otherwise, returns false.
    
    Money(long dollars, int cents);
    //Initializes the object so its value represents an amount with the
    //dollars and cents given by the arguments. If the amount is negative,
    //then both dollars and cents must be negative.
    
    Money(long dollars);
    //Initializes the object so its value represents $dollars.00.
    
    Money();
    //Initializes the object so its value represents $0.00.
    
    double getValue();
    //Precondition: The calling object has been given a value.
    //Returns the amount of money recorded in the data of the calling object.
    
    void input(istream& ins);
    //Precondition: If ins is a file input stream, then ins has already been
    //connected to a file. An amount of money, including a dollar sign, has been
    //entered in the input stream ins. Notation for negative amounts is -$100.00.
    //Postcondition: The value of the calling object has been set to
    //the amount of money read from the input stream ins.
    
    void output(ostream& outs);
    //Precondition: If outs is a file output stream, then outs has already been
    //connected to a file.
    //Postcondition: A dollar sign and the amount of money recorded
    //in the calling object have been sent to the output stream outs.
private:
    long allCents;
};
```

## DISPLAY 11.3 Money Class-Version 1 (part 2 of 4)

```
int digitToInt(char c);
//Function declaration for function used in the definition of Money::input:
//Precondition: c is one of the digits '0' through '9'.
//Returns the integer for the digit; for example, digitToInt ('3') returns 3.
int main()
{
    Money yourAmount, myAmount(10, 9), ourAmount;
    cout << "Enter an amount of money: ";
    yourAmount.input(cin);
    cout << "Your amount is ";
    yourAmount.output(cout);
    cout << endl;
    cout << "My amount is ";
    myAmount.output(cout);
    cout << endl;
    if (equal(yourAmount, myAmount))
        cout << "We have the same amounts.\n";
    else
        cout << "One of us is richer.\n";
    ourAmount = add(yourAmount, myAmount);
    yourAmount.output(cout);
    cout << " + ";
    myAmount.output(cout);
    cout << " equals ";
    ourAmount.output(cout);
    cout << endl;
    return 0;
}
Money add(Money amount1, Money amount2)
{
    Money temp;

    temp.allCents = amount1.allCents + amount2.allCents;
    return temp;
}
bool equal(Money amount1, Money amount2)
{
    return (amount1.allCents == amount2.allCents);
}
Money::Money(long dollars, int cents)
{
    if (dollars * cents < 0) //If one is negative and one is positive
```
