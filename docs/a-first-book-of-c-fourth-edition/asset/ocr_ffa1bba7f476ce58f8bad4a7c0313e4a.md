+   - New operator symbols can’t be created. For example, because `%` is not an operator in C++, it can’t be defined as a class operator.
+   - Neither the precedence nor the associativity of C++’s operators can be modified. Therefore, you can’t give the addition operator a higher precedence than the multiplication operator.
+   - Operators can’t be redefined for C++’s built-in types.
+   - The operator must be a class member or friend function and must be defined to take at least one class member as an operand.

# Assignment Operator

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