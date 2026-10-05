# Friend Functions and Automatic Type Conversion 339

The most common kinds of friend functions are overloaded operators. However, any kind of function can be made a friend function.
A function (or overloaded operator) can be a friend of more than one class. To make it friend of multiple classes, just give the declaration of the friend function in each class for which you want it to be a friend.

Many experts consider friend functions (and operators) to be in some sense not "pure". They feel that the true spirit of object-oriented programming all operators and functions should be member functions. On the other hand, overloading operators as friends provides the pragmatic advantage of automatic type conversion in all arguments, and since the operator declaration is inside the class, it provides at least a bit more encapsulation than nonmember, nonfriend operators. We have shown you three ways to overload operators: as nonmember nonfriends, and as friends. You can decide for yourself which technique prefer.

Figure 8.3 Overloading Operators as Friends (part 1 of 2)

```
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

//Class for amounts of money in U.S. currency
class Money {
public:
    Money();
    Money(double amount);
    Money(int dollars, int cents);
    Money(int dollars);
    double getAmount() const;
    int getDollars() const;
    int getCents() const;
    void input(); //Reads the dollar sign as well as the amount number
    void output() const;
    friend Money operator+(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount1, const Money& amount2);
    friend bool operator===(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount);
private:
    int dollars; //A negative amount is represented as negative
        //dollars
    int cents; //negative cents. Negative $4.50 is represented
        //-4 and -50.

(continued)
```