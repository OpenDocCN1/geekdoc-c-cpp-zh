Temperature.h) and the nontrivial operations are usually defined in a separately compiled implementation file (e.g., Temperature.cpp). As described in Chapter 6, the documentation for the class and its operations are commonly put in a separate documentation file (e.g., Temperature.txt).

# 14.3.1 The Class Data Members

The first task is to implement the data items. For our Temperature class, we can store the number of degrees in a real variable and the scale in a character variable. Thus, in Temperature.h, we write:

```
/* Temperature.h is the header file for class Temperature.
...
------------------------------------------------------------*/

double myDegrees;
char myScale;        // 'F', 'C', or 'K'
```

These will become the data members—also known as instance variables—of our Temperature class. Note that their names begin with the prefix my to reflect our internal perspective. And as with all identifiers, the name of a data member should be self-documenting, describing what it stores.

We could have used string to define myScale if we wanted to store the entire name of the scale, but we chose char instead because temperatures are usually written using a single character for the scale (e.g., 98.6 F, 100 C, 273 K). The best choice in some situations may not be clear, but a decision must be made before we can proceed. Such implementation decisions can always be revised later if they prove unwise.

# 14.3.1.1 Encapsulation

Once we have declared variables for the data members of our class, we can actually create the class by wrapping a class declaration around these objects (again, in Temperature.h):

```
class Temperature
{
    public:
        // to be filled in later
    private:
        double myDegrees;
        char myScale;
};
```

Don't forget the semicolon after the closing curly brace. Like all declarations, a class declaration must be terminated by a semicolon.

Wrapping the data members in a class declaration and then using the class as a type to declare an object makes it possible for an object to store values of different types. We call this encapsulation. The Temperature class encapsulates the double data member myDegrees and the char data member myScale.