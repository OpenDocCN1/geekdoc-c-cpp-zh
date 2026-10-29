
# Pitfall

## RETURNING A REFERENCE TO CERTAIN MEMBER VARIABLES

When a member function returns a member variable and that member variable is of some class type, then it should normally not be returned by reference. For example, consider

```
class A
{
public:
    const SomeClass getMember() { return member; }
    ...
private:
    SomeClass member;
    ...
};
```

where SomeClass is, of course, some class type. The function getMember should not return a reference, but should instead return by const value as we have done in the example.

The problem with returning a reference to a class type member variable is the same as what we described for returning the member variable by non-const value in the programming tip section of this chapter entitled Returning Member Variables of a Class Type. When returning a member variable which is itself of some class type it should normally be returned by const value. (Every such rule has rare exceptions.)

## OVERLOADING >> AND <<

The operators >> and << can be overloaded so that you can use them to input and output objects of the classes you define. The details are not that different from what we have already seen for other operators, but there are some new subtleties.

The insertion operator << that we used with cout is a binary operator very much like + or -. For example, consider the following:

```
cout << "Hello out there.\n";
```

The operator is <<, the first operand is the predefined object cout (from the library iostream), and the second operand is the string value "Hello out there.\n". The predefined object cout is of type ostream, and so when you overload <<, the parameter that receives cout will be of type ostream. You can change either of the two operands to <<. When we cover file I/O in Chapter 12 you will see how to create an object of type ostream that sends output to a file. (These file I/O objects as well as the objects cin and cout are called streams, which is why the library name is ostream.) The overloading that we create, with cout in mind, will turn out to also work for file output without any changes in the definition of the overloaded <<.

In our previous definitions of the class Money (Display 8.1 through Display 8.3) we used the member function output to output values of type Money. This is adequate, but

it would be nicer if we could simply use the insertion operator << to output values of type Money, as in the following:

```
Money amount(100);
cout << "I have " << amount << " in my purse.\n";
```

instead of having to use the member function output as shown below:

```
Money amount(100);
cout << "I have ";
amount.output();
cout << " in my purse.\n";
```

One problem in overloading the operator << is deciding what value, if any, should be returned when << is used in an expression like the following:

```
cout << amount
```

The two operands in the above expression are cout and amount, and evaluating the expression should cause the value of amount to be written to the screen. But if << is an operator like + or -, then the above expression should also return some value. After all, expressions with other operands, such as n1 + n2, return values. But what does cout << amount return? To obtain the answer to that question, we need to look at a more complicated expression involving <<.

Let’s consider the following expression, which involves evaluating a chain of expressions using <<:

```
cout << "I have " << amount << " in my purse.\n";
```

If you think of the operator << as being analogous to other operators, such as +, then the above should be (and in fact is) equivalent to the following:

```
( (cout << "I have ") << amount ) << " in my purse.\n";
```

What value should << return to make sense of the above expression? The first thing evaluated is the subexpression:

```
(cout << "I have ")
```

If things are to work out, then the above subexpression had better return cout so that the computation can continue as follows:

```
( cout << amount ) << " in my purse.\n";
```

And if things are to continue to work out, (cout << amount) had better also return cout so that the computation can continue as follows:

```
cout << " in my purse.\n";
```

This is illustrated in Display 8.4. The operator << should return its first argument, which is of type ostream (the type of cout).

Thus, the declaration for the overloaded operator << (to use with the class Money) should be as follows:

```
class Money
{
public:
        . . .
    friend ostream& operator <<(ostream& outs, const Money& amount);
```

### Display 8.4    << as an Operator

```
cout << "I have " << amount << " in my purse.\n";
```

means the same as

```
((cout << "I have ") << amount) << " in my purse.\n";
```

and is evaluated as follows:

First evaluate (cout << "I have "), which returns cout:

```
(cout << "I have ")
```

The string "I have " is output.

```
(cout << amount) << " in my purse.\n";
```

Then evaluate (cout << amount), which returns cout:

```
(cout << amount) << " in my purse.\n";
```

The value of amount is output.

```
cout << " in my purse.\n";
```

Then evaluate cout << " in my purse.\n", which returns cout:

```
cout << " in my purse.\n"
```

The string "in my purse.\n" is output.

```
cout;
```

Since there are no more << operators, the process ends.

Once we have overloaded the insertion (output) operator <<, we will no longer need the member function output and will delete output from our definition of the class Money. The definition of the overloaded operator << is very similar to the member function output. In outline form, the definition for the overloaded operator is as follows:

```
ostream& operator <<(ostream& outputStream, const Money& amount)
{
    <This part is the same as the body of
    Money::output which is given in Display 8.1 (except that
    dollars is replaced with amount.dollars
    and cents is replaced by amount.cents).>

    return outputStream;
}
```

Note that the operator returns a reference.

The extraction operator >> is overloaded in a way that is analogous to what we described for the insertion operator <<. However, with the extraction (input) operator >>, the second argument will be the object that receives the input value, so the second parameter must be an ordinary call-by-reference parameter. In outline form the definition for the overloaded extraction operator >> is as follows:

```
istream& operator >>(istream& inputStream, Money& amount)
{
    <This part is the same as the body of
    Money::input, which is given in Display 8.1 (except that
    dollars is replaced with amount.dollars
    and cents is replaced by amount.cents).>

    return inputStream;
}
```

The complete definitions of the overloaded operators << and >> are given in Display 8.5, where we have rewritten the class Money yet again. This time we have rewritten the class so that the operators << and >> are overloaded to allow us to use these operators with values of type Money.

Note that you cannot realistically overload >> or << as member operators. If << and >> are to work as we want, then the first operand (first argument) must be cout or cin (or some file I/O stream). But if we want to overload the operators as members of, say, the class Money, then the first operand would have to be the calling object and so would have to be of type Money, and that will not allow you to define the operators so they behave in the normal way for >> and <<.

### Display 8.5 Overloading << and >> (part i of 3)

```
#include <iostream>
#include <stdlib.h>
#include <cmath>
using namespace std;

//Class for amounts of money in U.S. currency
class Money
{
public:
    Money();
    Money(double amount);
    Money(int theDollars, int theCents);
    Money(int theDollars) const;
    double getAmount() const;
    int getDollars() const;
    int getCents() const;
    friend const Money operator +(const Money& amount1, const Money& amount2);
    friend const Money operator -(const Money& amount1, const Money& amount2);
    friend bool operator ==(const Money& amount1, const Money& amount2);
    friend const Money operator -(const Money& amount);
    friend ostream& operator <<(ostream& outputStream, const Money& amount);
    friend istream& operator >>(istream& inputStream, Money& amount);
private:
    int dollars; //A negative amount is represented as negative dollars and
    int cents; //negative cents. Negative $4.50 is represented as -4 and -50.
    int dollarsPart(double amount) const;
    int centsPart(double amount) const;
    int round(double number) const;
};

int main()
{
    Money yourAmount, myAmount(10, 9);
    cout << "Enter an amount of money: ";
    cin >> yourAmount;
    cout << "Your amount is " << yourAmount << endl;
    cout << "My amount is " << myAmount << endl;
    if (yourAmount == myAmount)
        cout << "We have the same amounts.\n";
    else
        cout << "One of us is richer.\n";
    Money ourAmount = yourAmount + myAmount;
```
