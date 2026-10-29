Program 11.3 produces the following output:

```
The date stored in a is 04/01/11
The date stored in b is 12/18/12
The date stored in c is 04/01/11
The date stored in d is 12/18/12
```

As this output shows, the copy constructor has initialized c’s and d’s data members to a’s and b’s values. Although the copy constructor in Program 11.3 adds nothing to the functionality of the compiler’s default copy constructor, it does give you the fundamentals of defining your own copy constructors.

# Base/Member Initialization⁶

A true initialization has no reliance on assignment and is possible in C++ by using a base/member initialization list. This list can be applied only to constructor functions and can be written in two ways. The first way is inside a class’s declaration section in this form:

```
ClassName(argument list):list of data members(initializing values) {}
```

Here’s an example of a default constructor performing true initialization in this form:

```
// class declaration section
public:
  Date(int mo=4, int da=1, int yr=2012):month(mo), day(da), year(yr) {}
```

The second way is to declare a function prototype with defaults in the class declaration section followed by the initialization list in the class implementation section. For the Date constructor, it takes this form:

```
// class declaration section
public:
  Date(int = 4, int = 1, int = 2012);  // prototype with defaults

// class implementation section
Date::Date(int mo, int da, int yr) : month(mo), day(da), year(yr) {}
```

Notice that in both forms, the body of the constructor function is empty. This isn’t a requirement, and the body can include any subsequent operations you want the constructor to perform. The interesting feature of this type of constructor is that it clearly differentiates between the initialization tasks performed in the member initialization list (between the colon and the braces) and any subsequent assignments in the function’s body. Although you won’t be using this type of initialization in this book, it’s required whenever a const class instance variable is used.