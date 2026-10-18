
If a member function does not change the value of its calling object, then you can mark the function by adding the const modifier to the function declaration. If you make a mistake in your definition of the function so that it does change the calling object and the function is marked with const, then the computer will give an error message. The const is placed at the end of the function declaration, just before the final semicolon. The heading of the function definition should also have a const so that it matches the function declaration.

### EXAMPLE

```cpp
class Sample
{
public:
    Sample();
    friend int compare(const Sample& s1, const Sample& s2);
    void input();
    void output() const;
private:
    int stuff;
    double moreStuff;
};
```

Use of the const modifier is an all-or-nothing proposition. You should use the const modifier whenever it is appropriate for a class parameter and whenever it is appropriate for a member function of the class. If you do not use const every time that it is appropriate for a class, then you should never use it for that class.

### DISPLAY 11.4 The Class Money with Constant Parameters

```cpp
//Class for amounts of money in U.S. currency.
class Money
{
public:
    friend Money add(const Money& amount1, const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns the sum of the values of amount1 and amount2.

    friend bool equal(const Money& amount1, const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns true if amount1 and amount2 have the same value;
    //otherwise, returns false.

    Money(long dollars, int cents);
    //Initializes the object so its value represents an amount with the
    //dollars and cents given by the arguments. If the amount is negative,
    //then both dollars and cents must be negative.

    Money(long dollars);
    //Initializes the object so its value represents $dollars.00.

    Money();
    //Initializes the object so its value represents $0.00.

    double getValue() const;
    //Precondition: The calling object has been given a value.
    //Returns the amount of money recorded in the data of the calling object.

    void input(istream& ins);
    //Precondition: If ins is a file input stream, then ins has already been
    //connected to a file. An amount of money, including a dollar sign, has been
    //entered in the input stream ins. Notation for negative amounts is -$100.00.
    //Postcondition: The value of the calling object has been set to
    //the amount of money read from the input stream ins.

    void output(ostream& outs) const;
    //Precondition: If outs is a file output stream, then outs has already been
    //connected to a file.
    //Postcondition: A dollar sign and the amount of money recorded
    //in the calling object have been sent to the output stream outs.

private:
    long allCents;
};
```

### SELF-TEST EXERCISES

8. Give the complete definition of the member function getValue that you would use with the definition of Money given in Display 11.4.

9. Why would it be incorrect to add the modifier const, as shown here, to the function declaration for the member function input of the class Money given in Display 11.4?

```cpp
class Money
{
    ...
public:
    void input(istream& ins) const;
    ...
};
```

10. What are the differences and the similarities between a call-by-value parameter and a call-by-const-reference parameter? Function declarations that illustrate these are

```cpp
void callByValue(int x);
void callByConstReference(const int& x);
```

11. Given the following definitions:

```cpp
const int x = 17;
class A
{
public:
    A();
    A(int x);
    int f() const;
    int g(const A& x);
private:
    int i;
};
```

Each of the three const keywords is a promise to the compiler that the compiler will enforce. What is the promise in each case?

## 11.2 OVERLOADING OPERATORS

> Mathematics is the art of giving the same name to different things.
>
> HENRI POINCARÉ

Earlier in this chapter, we showed you how to make the function add a friend of the class Money and use it to add two objects of type Money (Display 11.3). The function add is adequate for adding objects, but it would be nicer if you could simply use the usual + operator to add values of type Money, as in the last line of the following code:

```cpp
Money total, cost, tax;
cout << "Enter cost and tax: ";
cost.input(cin);
tax.input(cin);
total = cost + tax;
```

instead of having to use the slightly more awkward

```cpp
total = add(cost, tax);
```

Recall that an operator, such as +, is really just a function except that the syntax for how it is used is slightly different from that of an ordinary function. In an ordinary function call, the arguments are placed in parentheses after the function name, as in the following:

A function can be overloaded to take arguments of different types. An operator is really a function, so an operator can be overloaded. The way you overload an operator, such as +, is basically the same as the way you overload a function name. In this section we show you how to overload operators in C++.

### Overloading Operators

You can overload the operator + (and many other operators) so that it will accept arguments of a class type. The difference between overloading the + operator and defining the function add (given in Display 11.3) involves only a slight change in syntax. The definition of the overloaded operator + is basically the same as the definition of the function add. The only differences are that you use the name + instead of the name add and you precede the + with the keyword operator. In Display 11.5 we have rewritten the type Money to include the overloaded operator + and we have embedded the definition in a small demonstration program.

The class Money, as defined in Display 11.5, also overloads the == operator so that == can be used to compare two objects of type Money. If amount1 and amount2 are two objects of type Money, we want the expression

```cpp
amount1 == amount2
```

to return the same value as the following Boolean expression:

```cpp
amount1.allCents == amount2.allCents
```

As shown in Display 11.5, this is the value returned by the overloaded operator ==.

You can overload most, but not all, operators. The operator need not be a friend of a class, but you will often want it to be a friend. Check the box entitled “Rules on Overloading Operators” for some technical details on when and how you can overload an operator.

### Operator Overloading

A (binary) operator, such as +, -, /, %, and so forth, is simply a function that is called using a different syntax for listing its arguments. With an operator, the arguments are listed before and after the operator; with a function, the arguments are listed in parentheses after the function name. An operator definition is written similarly to a function definition, except that the operator definition includes the reserved word operator before the operator name. The predefined operators, such as + and so forth, can be overloaded by giving them a new definition for a class type.

An operator may be a friend of a class although this is not required. An example of overloading the + operator as a friend is given in Display 11.5.

### DISPLAY 11.5 Overloading Operators (part 1 of 2)

```cpp
//Program to demonstrate the class Money. (This is an improved version of
//the class Money that we gave in Display 11.3 and rewrote in Display 11.4.)
#include <iostream>
#include <cstdlib>
#include <cctype>
using namespace std;

//Class for amounts of money in U.S. currency.
class Money
{
public:
    friend Money operator +(const Money& amount1, const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns the sum of the values of amount1 and amount2.

    friend bool operator ==(const Money& amount1, const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns true if amount1 and amount2 have the same value;
    //otherwise, returns false.

    Money(long dollars, int cents);
    Money(long dollars);
    Money();
    double getValue() const;
    void input(istream& ins);
    void output(ostream& outs) const;
private:
    long allCents;
};

<Any extra function declarations from Display 11.3 go here.>

int main()
{
    Money cost(1, 50), tax(0, 15), total;
    total = cost + tax;

    cout << "cost = ";
    cost.output(cout);
    cout << endl;
    cout << "tax = ";
    tax.output(cout);
    cout << endl;
    cout << "total bill = ";
    total.output(cout);
    cout << endl;
```

Some comments from Display 11.4 have been omitted to save space in this book, but they should be included in a real program.
