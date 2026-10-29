
# Program 11.2

```
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2012);    // constructor
    Date operator+(int); // prototype for the + operator function
    void showDate();    // member function to display a date
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}
```

```
Date Date::operator+(int days)
{
    Date temp;  // a temporary date to store the result

    temp.day = day + days;    // add the days
    temp.month = month;
    temp.year = year;

    while (temp.day > 30)    // adjust the months
    {
        temp.month++;
        temp.day -= 30;
    }
    while (temp.month > 12)  // adjust the years
```

```
{ temp.year++;
    temp.month -= 12;
}
return temp;    // the values in temp are returned
}
```

```
void Date::showDate()
{
    cout << setfill('0')
        << setw(2) << month << '/'
        << setw(2) << day << '/'
        << setw(2) << year % 100;
    return;
}
```

```
int main()
{
    Date oldDate(4,1,2011), newDate; // declare two objects

    cout << "The initial date is ";
    oldDate.showDate();
    cout << endl;
    newDate = oldDate + 284;  // add in 284 days = 9 months and 14 days
    cout << "The new date is ";
    newDate.showDate();
    cout << endl;

    return 0;
}
```

Program 11.2 produces the following output:

The initial date is 04/01/11
The new date is 01/15/12

In constructing your own operator functions, the only restrictions on selecting and using the operator symbols in Table 11.1 are the following:

+   - An operator's syntax can't be changed, so a binary operator must remain binary, and a unary operator must remain unary.
+   - Symbols not in Table 11.1 can't be used. For example, the ., ::, and ?: symbols can't be used as operator functions.

Note that an operator symbol can be used to produce any operation, whether or not the operation is consistent with the symbol's accepted use. For example, you could redefine the addition symbol to provide multiplication. Clearly, this redefinition violates the intent of making these symbols available, so care must be taken to redefine each symbol in a manner consistent with its accepted use.

+   - New operator symbols can’t be created. For example, because `%` is not an operator in C++, it can’t be defined as a class operator.
+   - Neither the precedence nor the associativity of C++’s operators can be modified. Therefore, you can’t give the addition operator a higher precedence than the multiplication operator.
+   - Operators can’t be redefined for C++’s built-in types.
+   - The operator must be a class member or friend function and must be defined to take at least one class member as an operand.

## Assignment Operator

The **assignment operator**, `=`, is the one operator that works with all classes without requiring an operator function. For example, if a and b are objects constructed from the Date class, the statement `a = b;` sets a’s data members equal to their equivalent b members. Therefore, if b’s month, day and year members are 12, 25, 2014, the expression `a = b` sets a’s month variable to 12, its day variable to 25, and its year variable to 2014. This type of assignment is referred to as **memberwise assignment**.

In the absence of a user-written assignment operator, the C++ compiler builds a memberwise assignment operator as the default assignment operator for each class, which is generally adequate for most classes. However, if the class contains any pointer data members, this default assignment operator usually has to be created explicitly (see Section 12.4). Creating an assignment function is the same as creating any other operator function, such as `==` and `+`: declaring it in the class declaration section and then defining it in the class implementation section. A simple assignment operator declaration has this form:

```
void operator=(const ClassName&);
```

As in all functions, the keyword void indicates that the assignment operator returns no value. The class name and ampersand in parentheses indicate that the argument passed to the operator is a class reference, and the const keyword ensures that the function can’t change the reference.

The following definition in the class implementation section creates an explicit assignment that corresponds to this operator’s prototype. It mimics the operation of the default assignment operator:

```
void Date::operator=(Date& olddate)
{
    day = olddate.day;      // assign the day
    month = olddate.month;  // assign the month
    year = olddate.year;    // assign the year
}
```

In this definition, olddate is defined as a reference to a Date class and refers to the object passed to the function when it’s called. The call can be made by using an expression such as `a.operator=(b)` or `a = b`, with a and b replaced by the names of the Date objects you’re using. In the called function, the day, month, and year data members referenced internally by olddate (which correspond to b’s data members) are assigned to the equivalent data members

in a. (You can see that b is the reference argument passed to olddate in the function call a.operator=(b), where b is the argument inside the function's parentheses.)

One useful modification concerns the operation's return value. As constructed, your simple assignment operator returns no value, which precludes you from using it in multiple assignments, such as a = b = c. The reason is that operator functions retain the same precedence and associativity as their built-in counterparts. Therefore, an expression such as a = b = c is evaluated in the order a = (b = c). Because of the way assignment has been defined by the operator function, unfortunately, the expression b = c returns no value, making subsequent assignment to a an error because it results in the invalid expression a = void. To allow multiple assignments, a more complete assignment operation would return a Date type. Returning the correct date requires a special class pointer, which is discussed in Section 11.2.

## Copy Constructors⁴

Although assignment looks similar to initialization, they're entirely different operations. In C++, an initialization occurs every time a new object is created. In an assignment, no new object is created—the value of an existing object is simply changed. Figure 11.1 shows this difference.

![](img/202cface8244f523c2641baa2e00d7dd_519_0.png)

One type of initialization that closely resembles assignment occurs in C++ when one object is initialized by using another object of the same class. For example, in the declaration

```
Date b = a;
```

or its equivalent form

```
Date b(a);
```

the b object is initialized to the previously declared a object. The constructor performing this type of initialization is called a copy constructor, and if you don't declare one, the compiler creates it for you. The compiler's default copy constructor performs similarly to the default assignment operator by doing a memberwise assignment between objects. Therefore, for the declaration Date b = a;, the default copy constructor sets b's month, day, and year values to their counterparts in a.

As with default assignment operators, default copy constructors work just fine unless the class contains pointer data members. Before considering the possible complications with pointer data members and how to handle them, seeing how to construct your own copy constructor is helpful.

Copy constructors, like all operator functions, are declared in the class declaration section and defined in the class implementation section. The declaration of a copy constructor has this syntax:

```
ClassName(const ClassName&);
```

As with all constructors, the function name must be the class name. Also, the argument is a reference to the class, which is a characteristic of all copy constructors. To ensure that the argument isn't altered inadvertently, it's always specified as a constant. Applying this general form to the Date class, a copy constructor can be declared as follows:

```
Date(const Date&);
```

The actual implementation of this constructor, if it were to perform the same memberwise assignment as the default copy constructor, would take this form:

```
Date:: Date(const Date& olddate)
{
    month = olddate.month;
    day = olddate.day;
    year = olddate.year;
}
```

A comparison of this copy constructor with the assignment operator defined previously shows them to be the same function. The difference is that the copy constructor, like all constructors, creates an object's data members before using assignment to specify member values. Therefore, the copy constructor doesn't perform a true initialization, but a creation followed by assignment. Program 11.3 contains this copy constructor in the context of a complete program.

## Program 11.3

```
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
```
