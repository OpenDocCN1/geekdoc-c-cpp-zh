to be cascaded with input operations on other PhoneNumber objects or other data types. For example, a program can input two PhoneNumber objects in one statement as follows:

```
cin >> phone1 >> phone2;
```

First, the expression `cin >> phone1` executes by making the non-member function call

```
operator>>( cin, phone1 );
```

This call then returns a reference to cin as the value of `cin >> phone1`, so the remaining portion of the expression is interpreted simply as `cin >> phone2`. This executes by making the non-member function call

```
operator>>( cin, phone2 );
```

> **Good Programming Practice 11.1**
> 
> *Overloaded operator should mimic the functionality of their built-in counterparts—for example, the + operator should be overloaded to perform addition, not subtraction. Avoid excessive or inconsistent use of operator overloading, as this can make a program cryptic and difficult to read.*

# Overloading the Stream Insertion (<<) Operator

The stream insertion operator function (Fig. 11.4, lines 11–16) takes an ostream reference (output) and a const PhoneNumber reference (number) as arguments and returns an ostream reference. Function operator<< displays objects of type PhoneNumber. When the compiler sees the expression

```
cout << phone
```

in line 22 of Fig. 11.5, the compiler generates the non-member function call

```
operator<<( cout, phone );
```

Function operator<< displays the parts of the telephone number as strings, because they’re stored as string objects.

> **Error-Prevention Tip 11.1**
> 
> *Returning a reference from an overloaded << or >> operator function is typically successful because cout and most stream objects are global, or at least long-lived. Returning a reference to an automatic variable or other temporary object is dangerous—this can create “dangling reference” to nonexistent objects.*

# Overloaded Operators as Non-Member Friend Functions

The functions operator>> and operator<< are declared in PhoneNumber as non-member, friend functions (Fig. 11.3, lines 12–13). They’re non-member functions because the object of class PhoneNumber must be the operator’s right operand. If these were to be PhoneNumber member functions, the following awkward statements would have to be used to output and input an Array:

```
phone << cout;
phone >> cin;
```

Such statements would be confusing to most C++ programmers, who are familiar with cout and cin appearing as the left operands of << and >>, respectively.