would just fine. This is a totally acceptable approach. But what if your program also needed to store several dates? It would be much better to somehow group these sets of three variables.

You can define a structure called date in the Objective-C language that consists of three components that represent the month, day, and year. The syntax for such a definition is rather straightforward:

```
struct date
{
    int month;
    int day;
    int year;
}
```

The date structure just contains three integer members, called month, day, and year. Essentially, the definition of date defines a new type in the language, in that variables can subsequently be declared to be of type struct date, as in the following definition:

struct date today;

You can also define a variable called purchaseDate to be of the same type with a separate definition:

struct date purchaseDate;

Or you can simply include the two on the same line:

struct date today, purchaseDate;

Unlike variables of type int, float, or char, a special syntax is needed when dealing with structure variables. A member of a structure is accessed by specifying the variable name, followed by a period and then the member name. For example, to set the value of day in the variable today to 21, you would write this:

```
today.day = 21;
```

Note that no spaces are permitted between the variable name, the period, and the member name.

Now, wait a second! Wasn't the same operator we used to access a property on an object? Recall that we could write the statement

```
myRect.width = 12;
```

to invoke the Rectangle object's setter method (called setColor:), passing the argument value of 12. No confusion arises here:the compiler determines whether it's a structure or to the left of the dot operator and handles the situation properly.

Returning to the struct date example, to set year in today to 2011, you can use this expression:

```
today.year = 2011;
```