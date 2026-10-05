
# Friend Functions and Automatic Type Conversion 339

The most common kinds of friend functions are overloaded operators. However, any kind of function can be made a friend function.
A function (or overloaded operator) can be a friend of more than one class. To make it friend of multiple classes, just give the declaration of the friend function in each class for which you want it to be a friend.

Many experts consider friend functions (and operators) to be in some sense not "pure". They feel that the true spirit of object-oriented programming is that all operators and functions should be member functions. On the other hand, overloading operators as friends provides the pragmatic advantage of automatic type conversion in all arguments, and since the operator declaration is inside the class, it provides at least a bit more encapsulation than nonmember, nonfriend operators. We have shown you three ways to overload operators: as nonmember nonfriends, and as friends. You can decide for yourself which technique you prefer.

Figure 8.3 Overloading Operators as Friends (part 1 of 2)

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

// Class for amounts of money in U.S. currency
class Money {
public:
    Money();
    Money(double amount);
    Money(int dollars, int cents);
    Money(int dollars);
    double getAmount() const;
    int getDollars() const;
    int getCents() const;
    void input(); // Reads the dollar sign as well as the amount number
    void output() const;
    friend Money operator+(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount1, const Money& amount2);
    friend bool operator==(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount);
private:
    int dollars; // A negative amount is represented as negative dollars
    int cents; // negative cents. Negative $4.50 is represented as -4 and -50.
};

// (continued)
```

# 340 CHAPTER 8 Operator Overloading, Friends, and References

Display 8.3 Overloading Operators as Friends (part 2 of 2)

```cpp
25 int dollarsPart(double amount) const;
26 int centsPart(double amount) const;
27 int round(double number) const;
28 };
```

```cpp
29 int main ()
30 {
31 // <if the main function is the same as in Display 8.1, then the screen dialogue
32     // will be the same as in Display 8.1.>
33 }
34 
35 const Money operator +(const Money& amount1, const Money& amount2)
36 {
37 int allCents = amount1.cents + amount1.dollars*100;
38 int allC2 = amount2.cents + amount2.dollars*100;
39 int sumCents = allCents + allC2;
40 int absCents = abs(sumCents); // Money can be negative.
41 int finalDollars = absCents/100;
42 int finalCents = absCents%100;
```

> Note that friends have direct access to member variables.

```cpp
43 if (sumCents < 0)
44 {
45 finalDollars = -finalDollars;
46 finalCents = -finalCents;
47 }
```

```cpp
48 return Money(finalDollars, finalCents);
49 }
```

```cpp
50 const Money operator - (const Money& amount1, const Money& amount2)
51 // <The complete definition is Self-Test Exercise 7.>
```

```cpp
52 bool operator == (const Money& amount1, const Money& amount2)
53 {
54 return (amount1.dollars == amount2.dollars
55 && (amount1.cents == amount2.cents));
56 }
```

```cpp
57 const Money operator - (const Money& amount)
58 {
59 return Money (-amount.dollars, -amount.cents);
60 }
```

60 <Definitions of all other member functions are the same as in Display 8.1>

# Friend Functions and Automatic Type Conversion

## Friend Classes

friend class

A class can be a **friend** of another class in the same way that a function can be a friend of a class. If the class F is a friend of the class C, then every member function of the class F is a friend of the class C. To make one class a friend of another, you must declare the friend as a friend within the other class.

When one class is a friend of another, it is typical for the classes to reference each other in their class definitions. This requires that you include a **forward declaration** to the class defined second, as illustrated in the outline that follows this paragraph. Note that the forward declaration is just the heading of the class definition followed by a semicolon.

forward declaration

## Friend Functions

A friend of a class is an ordinary function except that it has access to the private members of objects of that class. To make a function a friend of a class, you must list the function declaration for the friend function in the class definition. The function declaration is preceded by the keyword friend. The function may be placed in either the private section or the public section, but it will be a public function in either case, so it is clearer to list it in the public section.

## SYNTAX OF A CLASS DEFINITION WITH FRIEND FUNCTIONS

```cpp
class Class_Name
{
public:
    friend void Function_1();
    friend int Function_2(int);
    friend double Function_3(double, double);
    // other members
};
```

## Example

```cpp
class FuelTank
{
public:
    friend void operator+(FuelTank& t1, FuelTank& t2);
    // <if the main function is the same as in Display 8.1, then the screen dialogue
    // will be the same as in Display 8.1.>
    FuelTank(double amount);
    // (continued)
```

71
```cpp
    void input();
    void output() const;
private:
    double;
```

```cpp
    void input(); // Reads the dollar sign as well as the amount number
    void output() const;
    friend Money operator+(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount1, const Money& amount2);
    friend bool operator==(const Money& amount1, const Money& amount2);
    friend Money operator-(const Money& amount);
private:
    int dollars; // A negative amount is represented as negative dollars
    int cents; // negative cents. Negative $4.50 is represented as -4 and -50.
};
```

> PITFALL: Compilers without Friends

On some compilers friend functions simply do not work as they are supposed to. Worst of all, they may work sometimes and not other times. On these compilers friend functions do not always have access to private members as are supposed to. Presumably, this will be fixed in later releases. In the meantime, you will use accessor functions to define nonmember.

## Rules on Overloading Operators

- When overloading an operator, at least one parameter (one operand) of the resulting operator must be of a class type.
- Most operators can be overloaded as a member of the class, a friend of the class, or nonmember, nonfriend.
- The following operators can only be overloaded (nonstatic) members of the class: ~, and ().
- You cannot create a new operator. All you can do is overloading operators such as +, -, *, /, and forth.
- You cannot change the number of arguments that an operator takes. For example, you cannot change * from a binary to a unary operator when you overload it; you cannot change ++ from a unary to a binary operator when you overload it.
- You cannot change the precedence of an operator. An overloaded operator has the same precedence as the ordinary version of the operator. For example, x*y + z always means x*y + z, unless x, y and z have been overloaded for the appropriate classes.
- The following operators cannot be overloaded: the dot operator (.), the scope resolution operator (::), sizeof ?, and the operator *, which is not discussed in this.
- An overloaded operator cannot have default arguments.

## Self-Test Exercises

- 6. What is the difference between a friend function for a class and a member function for a class?
- 7. Complete the definition of the friend subtraction operator - in Display 8.3.
- 8. Suppose you wish to overload the operator = so that it applies to the type Money. What do you need to add to the definition of Money given in Display 8.3?

# 8.3 References and More Overloaded Operators

Do not mistake the pointing finger for the moon.

> Zen saying

This section covers specialized, but important, overloading topics, including the assignment operator and the <<, [], ++, and -- operators. Because you need to understand returning a reference to correctly overload some of these operators, we also discuss this topic.
