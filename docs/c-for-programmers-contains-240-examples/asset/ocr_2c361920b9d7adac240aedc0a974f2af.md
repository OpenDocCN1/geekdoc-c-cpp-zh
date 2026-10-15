PhoneNumber objects to be cascaded with input operations on other PhoneNumber objects or on objects of other data types. For example, a program can input two PhoneNumber objects in one statement as follows:

```
cin >> phone1 >> phone2;
```

First, the expression cin >> phone1 executes by making the global function call

```
operator>>( cin, phone1 );
```

This call then returns a reference to cin as the value of cin >> phone1, so the remaining portion of the expression is interpreted simply as cin >> phone2. This executes by making the global function call

```
operator>>( cin, phone2 );
```

The stream insertion operator function (Fig. 11.4, lines 12–17) takes an ostream reference (output) and a const PhoneNumber reference (number) as arguments and returns an ostream reference. Function operator<< displays objects of type PhoneNumber. When the compiler sees the expression

```
cout << phone
```

in line 25 of Fig. 11.5, the compiler generates the global function call

```
operator<<( cout, phone );
```

Function operator<< displays the parts of the telephone number as strings, because they are stored as string objects.

# Error-Prevention Tip 11.1

> Returning a reference from an overloaded << or >> operator function is typically successful because cout, cin and most stream objects are global, or at least long-lived. Returning a reference to an automatic variable or other temporary object is dangerous—this can create “dangling references” to nonexisting objects.

Note that the functions operator>> and operator<< are declared in PhoneNumber as global, friend functions (Fig. 11.3, lines 15–16). They are global functions because the object of class PhoneNumber appears in each case as the right operand of the operator. Remember, overloaded operator functions for binary operators can be member functions only when the left operand is an object of the class in which the function is a member. Overloaded input and output operators are declared as friends if they need to access non-public class members directly for performance reasons or because the class may not offer appropriate get functions. Also note that the PhoneNumber reference in function operator<<’s parameter list (Fig. 11.4, line 12) is const, because the PhoneNumber will simply be output, and the PhoneNumber reference in function operator>>’s parameter list (line 22) is non-const, because the PhoneNumber object must be modified to store the input telephone number in the object.

# Software Engineering Observation 11.3

> New input/output capabilities for user-defined types are added to C++ without modifying standard input/output library classes. This is another example of C++’s extensibility.