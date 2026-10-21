# Chapter 7

Take an example of a simple value class definition:

```
// Class representing a height
value class Height
{
private:
    // Records the height in feet and inches
    int feet;
    int inches;

public:
    // Create a height from inches value
    Height(int ins)
    {
        feet = ins/12;
        inches = ins%12;
    }

    // Create a height from feet and inches
    Height(int ft, int ins) : feet(ft), inches(ins) {}
};
```

This defines a value class type with the name Height. It has two private fields that are both of type int that record a height in feet and inches. The class has two constructors—one to create a Height object from a number of inches supplied as the argument, and the other to create a Height object from both a feet and inches specification. The latter should really check that the number of inches supplied as an argument is less than 12, but I’ll leave you to add that as a fine point. To create a variable of type Height you could write:

```
Height tall = Height(7, 8);        // Height is 7 feet 8 inches
```

This creates the variable, tall, containing a Height object representing 7 feet 8 inches; this object is created by calling the constructor with two parameters.

```
Height baseHeight;
```

This statement creates a variable, baseHeight, that will be automatically initialized to a height of zero. The Height class does not have a no-arg constructor specified and because it is a value class, you are not permitted to supply one in the class definition. There will be a no-arg constructor included automatically in a value class that will initialize all value type fields to the equivalent of zero and all fields that are handles to nullptr and you cannot override the implicit constructor with your own version. It’s this default constructor that will be used to create the value of baseHeight.

There are a couple of other restrictions on what a value class can contain:

+   - You must not include a copy constructor in a value class definition.
+   - You cannot override the assignment operator in a value class (I’ll discuss how you override operators in a class in Chapter 8).

Value class objects are always copied by just copying fields and the assignment of one value class object to another is done in the same way. Value classes are intended to be used to represent simple objects