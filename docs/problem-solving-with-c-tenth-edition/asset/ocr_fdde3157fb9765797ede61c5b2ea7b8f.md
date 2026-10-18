```
Coordinate::Coordinate() : Coordinate(99,99)
{ }
```

The object defined by Coordinate c1; will invoke the default constructor which will in turn invoke the constructor to set x to 99 and y to 99.

# SELF-TEST EXERCISES

22. Suppose your program contains the following class definition (along with definitions of the member functions):

```
class YourClass
{
public:
    YourClass(int newInfo, char moreNewInfo);
    YourClass();
    void doStuff();
private:
    int information;
    char moreInformation;
};
```

Which of the following are legal?

```
YourClass anObject(42, 'A');
YourClass anotherObject;
YourClass yetAnotherObject();
anObject = YourClass(99, 'B');
anObject = YourClass();
anObject = YourClass;
```

23. How would you change the definition of the class DayOfYear in Display 10.4 so that it has two versions of an (overloaded) constructor? One version should have two int formal parameters (one for the month and one for the day) and should set the private member variables to represent that month and day. The other should have no formal parameters and should set the date represented to January 1. Do this without using a constructor initialization section in either constructor.

24. Redo the previous exercise, but this time use a constructor initialization section to initialize all member functions in each constructor.

# 10.3 ABSTRACT DATA TYPES

> We all know — the Times knows — but we pretend we don’t.

VIRGINIA WOOLF, Monday or Tuesday