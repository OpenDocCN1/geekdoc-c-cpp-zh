
```cpp
// function notation
cout << "morefixing.operator+(total) = \";
total.Show();
cout << endl;
```

```cpp
return 0;
}
```

Here is the output of the program in Listings 11.4, 11.5, and 11.6:

planning time = 0 hours, 0 minutes
coding time = 2 hours, 40 minutes
fixing time = 5 hours, 55 minutes
coding + fixing = 8 hours, 35 minutes
more fixing time = 3 hours, 28 minutes
morefixing.operator+(total) = 12 hours, 3 minutes

In short, the name of the operator+() function allows it to be invoked by either function notation or operator notation. The compiler uses the operand types to figure out what to do:

```cpp
int a, b, c;
Time A, B, C;
c = a + b; // use int addition
C = A + B; // use addition as defined for Time objects
```

Can you add more than two objects? For example, if t1, t2, t3, and t4 are all Time objects, can you do the following?

```cpp
t4 = t1 + t2 + t3; // valid?
```

The way to answer this is to consider how the statement gets translated into function calls. Because addition is a left-to-right operator, the statement is translated to this:

```cpp
t4 = t1.operator+(t2 + t3); // valid?
```

Then the argument is itself translated to a function call, giving the following:

```cpp
t4 = t1.operator+(t2.operator+(t3)); // valid YES
```

Is this valid? Yes, the function call t2.operator+(t3) returns a Time object that represents the sum of t2 and t3. This object then becomes the object of the t1.operator+() function call, and that returns the sum of t1 and the Time object that represents the sum of t2 and t3. In short, the final return value is the sum of t1, t2, and t3, just as desired.

# Time on Our Hands: Developing an Operator Overloading Example

## Overloading C++ Restrictions

Most C++ operators (see Table 11.1) can be overloaded in the manner described in the preceding section. Overloaded operators (with some exceptions) don't necessarily have to be member functions. However, at least one of the operands must be a user-defined type. Let's take a closer look at the limits C++ imposes on user-defined operator overloading:

- The overloaded operator must have at least one operand that is a user-defined type. This prevents you from overloading operators for the standard types. Thus, you can't redefine the minus operator (-) so that it yields the sum of two values instead of their difference. This restriction preserves program safety, although it may hinder creative accounting.

- You can't use an operator in a manner that violates the syntax rules for the original operator. For example, you can't overload the modulus operator (%) so that it can be used with a single operand:

```cpp
int x;
Time shiva;
% x; // invalid for modulus operator
% shiva; // invalid for overloaded operator
```

Similarly, you can't alter any operator precedence. If you overload the addition operator to let two classes, the new operator has the same precedence as ordinary addition.

- You can create new operator symbols. For example, you can define an operator**() function to denote exponentiation.

- You cannot overload the following operators:

| Operator | Description |
| :--- | :--- |
| sizeof | The sizeof operator |
| . | The membership operator |
| * | The pointer-to-member operator |
| :: | The scope-resolution operator |
| ? | The conditional operator |
| typeid | An RTTI operator |
| const_cast | A type cast operator |
| dynamic_cast | A type cast operator |
| reinterpret_cast | A type cast operator |
| static_cast | A type cast operator |

This still leaves all the operators in Table 11.1 available for overloading.

Most of the operators in Table 11.1 can be overloaded by using either member or nonmember functions. However, you can use only member functions to overload the following operators:

| Operator | Description |
| :--- | :--- |
| = | Assignment operator |
| () | Function call operator |
| [] | Subscribing operator |
| -> | Class member access by pointer operator |

**Note**: This chapter does not cover every operator mentioned in the list of restrictions or in Table 11.1. However, Appendix E, "Other Operators," summarizes the operators that are not covered in the main body of this text.

# Table 11.1 Operators That Can Be Overloaded

| + | * | ^ |
| :--- | :--- | :--- |
| & | | ! | < |
| > | += | -= | *= | /= | = |
| &= | *= | << | >> | >= |
| <= | == | != | <= | && |
| || | ++ | -- | | |
| () | [] | new delete new [] | delete [] |

In addition to these formal restrictions, you should use restraint when overloading operators. For example, you shouldn't overload the * operator that swaps the data members of two Time objects. Nothing in the notation would suggest what the operator did, so it would be better to define a class method with an explanatory name such as Swap().

## More Overloaded Operators

Some operators make sense for the Time class. For example, you might want to subtract one from another or multiply by a factor. This suggests the subtraction and multiplication operators. The technique is the same as the addition operator: you create operator- and operator* methods. That is, you add the following prototypes to the class declaration:

```cpp
Time operator-(const Time & t) const;
Time operator*(double n) const;
```

```cpp
// mytime2.cpp -- implementing Time methods
#include <iostream>
#include "mytime2.h"

Time::Time()
{
    hours = 0;
}

Time::Time(int h, int m)
{
    hours = h;
    minutes = m;
}

void Time::AddMin(int m)
{
    minutes += m;
    hours += 60;
    minutes %= 60;
}

void Time::AddHr(int h)
{
    hours += h;
}

void Time::Reset(int h, int m)
{
    hours = h;
    minutes = m;
}

Time::operator+(const Time & t) const
{
    Time sum;
    sum.minutes = minutes + t.minutes;
    sum.hours = hours + t.hours + sum.minutes / 60;
    sum.minutes %= 60;
    return sum;
}

Time::operator-(const Time & t) const
{
    Time diff;
    int tot1, tot2;
    tot1 = t.minutes + 60;
    tot2 = minutes + 60;
    diff.minutes = (tot2 - tot1) % 60;
    diff.hours = (tot2 - tot1) / 60;
    return diff;
}

Time::operator*(double mult) const
{
    Time result;
    long totalminutes = hours * mult * 60 + minutes * mult;
    result.hours = totalminutes / 60;
    result.minutes = totalminutes % 60;
    return result;
}

void Time::Show()
{
    std::cout << hours << " hours, " << minutes << " minutes";
}
```

# Time on Our Hands: Developing an Operator Overloading Example

With these changes made, you can test the new definitions with the code shown in Listing 11.9.

```cpp
// ustime2.cpp - using the third draft of the Time class
// compile ustime2.cpp and mytime2.cpp together
#include <iostream>
#include "mytime2.h"

int main()
{
    using std::cout;
    using std::endl;
    Time weeding(4, 35);
    Time waxing(2, 47);
    Time total;
    Time diff;
    Time adjusted;

    cout << "weeding time = ";
    weeding.Show();
    cout << endl;

    cout << "waxing time = ";
    waxing.Show();
    cout << endl;

    cout << "total work time = ";
    total = weeding + waxing; // use operator+
    total.Show();
    cout << endl;

    diff = weeding - waxing; // use operator-
    cout << "weeding time - waxing time = ";
    diff.Show();
    cout << endl;

    adjusted = total * 1.5; // use operator*
    cout << "adjusted work time = ";
    adjusted.Show();
    cout << endl;

    return 0;
}
```

Here is the output of the program in Listings 11.7, 11.8, and 11.9:

```text
weeding time = 4 hours, 35 minutes
waxing time = 2 hours, 47 minutes
total work time = 7 hours, 22 minutes
weeding time - waxing time = 1 hours, 48 minutes
adjusted work time = 11 hours, 3 minutes
```

## Introducing Friends

As you've seen, C++ controls the private portions of a class object. Usually, public class methods serve as the only access, but sometimes this restriction is too rigid to fit particular programming problems. In such cases, C++ provides another form of access: the *friend*. Friends come in three varieties:

- Friend functions
- Friend classes
- Friend member functions

By making a function friend to a class, you allow the function the same privileges that a member function of the class has. We'll look into friend functions now, leaving the other two varieties to Chapter 15, "Friends, Exceptions, and More"

Before seeing how to make friends, let's look into why they might be needed. Often, overloading a binary operator (that is, an operator with two arguments) for a class generator needs a friend function. Multiplying a Time object by a real number provides such a situation, so let's that case.

In the previous Time class example, the overloaded multiplication operator is different from the other two overloaded operators that it combines different types. The addition and subtraction operators each combine two Time values, but the multiplication operator combines a Time value with a double value. This restricts how the operator can be used. Remember, the left operand is the invoking object. That is,

```cpp
A = B * 2.75;
```

translates to the following member function:

```cpp
A = B.operator*(2.75);
```

But about the following statement:

```cpp
A = 2.75 * B; // cannot correspond to a member function
```

Conceptually, 2.75 * B should be the same as B * 2.75, but the first expression cannot not correspond to a member function because 2.75 is not a type Time object.
