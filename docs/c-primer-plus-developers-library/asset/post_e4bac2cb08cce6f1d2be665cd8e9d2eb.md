
```cpp
class Employee
{
private:
    char name[40];
    ...
public:
    void show_name();
    ...
};
class Singer : public Employee
{
    ...
public:
    void range();
    ...
};
...
Employee veep;
Singer trala;
...
Employee * pe = &trala;      // upcast—implicit type cast allowed
Singer * ps = (Singer *) &veep; // downcast—explicit type cast required
pe->show_name();              // Upcasting leads to a safe operation because
                              // a Singer is an Employee (every Singer
                              // inherits name).
ps->range();                  // Downcasting can lead to an unsafe operation
                              // because an Employee isn’t a Singer (an
                              // Employee need not have a range() method).
```

![](img/9afc44517b591d64e2e19f623c9308ef_787_0.png)

Figure 13.4   Upcasting and downcasting.

## Assignment Operator Considerations

If the compiler detects that a program assigns one object to another of the same class, it automatically supplies that class with an assignment operator. The default, or implicit, version of this operator uses memberwise assignment, with each member of the target object being assigned the value of the corresponding member of the source object. However, if the object belongs to a derived class, the compiler uses the base-class assignment operator to handle assignment for the base-class portion of the derived-class object. If you’ve explicitly provided an assignment operator for the base class, that operator is used. Similarly, if a class contains a member that is an object of another class, the assignment operator for that class is used for that member.

As you’ve seen several times, you need to provide an explicit assignment operator if class constructors use new to initialize pointers. Because C++ uses the base-class assignment operator for the base part of derived objects, you don’t need to redefine the assignment operator for a derived class unless it adds data members that require special care. For example, the baseDMA class defines assignment explicitly, but the derived lacksDMA class uses the implicit assignment operator generated for that class.

Suppose, however, that a derived class does use `new`, and you have to provide an explicit assignment operator. The operator must provide for every member of the class, not just the new members. The `hasDMA` class illustrates how this can be done:

```cpp
hasDMA & hasDMA::operator=(const hasDMA & hs)
{
    if (this == &hs)
        return *this;
    baseDMA::operator=(hs);  // copy base portion
    delete [] style;         // prepare for new style
    style = new char[std::strlen(hs.style) + 1];
    std::strcpy(style, hs.style);
    return *this;
}
```

What about assigning a derived-class object to a base-class object? (Note that this is not the same as initializing a base-class reference to a derived-class object.) Take a look at this example:

```cpp
Brass blips;                                      // base class
BrassPlus snips("Rafe Plosh", 91191, 3993.19, 600.0, 0.12); // derived class
blips = snips;                                    // assign derived object to base object
```

Which assignment operator is used? Remember that the assignment statement is translated into a method that is invoked by the left-hand object:

```cpp
blips.operator=(snips);
```

Here the left-hand object is a `Brass` object, so it invokes the `Brass::operator=(const Brass &)` function. The *is-a* relationship allows the `Brass` reference to refer to a derived-class object, such as `snips`. The assignment operator only deals with base-class members, so the `maxLoan` member and other `BrassPlus` members of `snips` are ignored in the assignment. In short, you can assign a derived object to a base object, and only the base-class members are involved.

What about the reverse? Can you assign a base-class object to a derived object? Take a look at this example:

```cpp
Brass gp("Griff Hexbait", 21234, 1200);   // base class
BrassPlus temp;                          // derived class
temp = gp;   // possible?
```

Here the assignment statement would be translated as follows:

```cpp
temp.operator=(gp);
```

The left-hand object is a `BrassPlus` object, so it invokes the `BrassPlus::operator=(const BrassPlus &)` function. However, a derived-class reference cannot automatically refer to a base-class object, so this code *won't* run unless there is also a conversion constructor:

```cpp
BrassPlus(const Brass &);
```

It could be, as is the case for the BrassPlus class, that the conversion constructor is a constructor with a base-class argument plus additional arguments, provided that the additional arguments have default values:

```cpp
BrassPlus(const Brass & ba, double ml = 500, double r = 0.1);
```

If there is a conversion constructor, the program uses this constructor to create a temporary BrassPlus object from gp, which is then used as an argument to the assignment operator.

Alternatively, you could define an assignment operator for assigning a base class to a derived class:

```cpp
BrassPlus & BrassPlus::operator=(const Brass &) {...}
```

Here the types match the assignment statement exactly, and no type conversions are needed.

In short, the answer to the question “Can you assign a base-class object to a derived object?” is “Maybe.” You can if the derived class has a constructor that defines the conversion of a base-class object to a derived-class object. And you can if the derived class defines an assignment operator for assigning a base-class object to a derived object. If neither of these two conditions holds, then you can’t make the assignment unless you use an explicit type cast.

## Private Versus Protected Members

Remember that protected members act like public members as far as a derived class is concerned, but they act like private members for the world at large. A derived class can access protected members of a base class directly, but it can access private members only via base-class member functions. Thus, making base-class members private offers more security, whereas making them protected simplifies coding and speeds up access. Stroustrup, in his book *The Design and Evolution of C++*, indicates that it’s better to use private data members than protected data members but that protected methods are useful.

## Virtual Method Considerations

When you design a base class, you have to decide whether to make class methods virtual. If you want a derived class to be able to redefine a method, you define the method as virtual in the base class. This enables late, or dynamic, binding. If you don’t want the method to be redefined, you don’t make it virtual. This doesn’t prevent someone from redefining the method, but it should be interpreted as meaning that you don’t want it redefined.

Note that inappropriate code can circumvent dynamic binding. Consider, for example, the following two functions:

```cpp
void show(const Brass & rba)
{
    rba.ViewAcct();
    cout << endl;
}
```

```cpp
void inadequate(Brass ba)
{
    ba.ViewAcct();
    cout << endl;
}
```

The first function passes an object by reference, and the second passes an object by value. Now suppose you use each with a derived class argument:

```cpp
BrassPlus buzz("Buzz Parsec", 00001111, 4300);
show(buzz);
inadequate(buzz);
```

The show() function call results in the rba argument being a reference to the BrassPlus object buzz, so rba.ViewAcct() is interpreted as the BrassPlus version, as it should be. But in the inadequate() function, which passes an object by value, ba is a Brass object constructed by the Brass (const Brass &) constructor. (Automatic upcasting allows the constructor argument to refer to a BrassPlus object.) Thus, in inadequate(), ba.ViewAcct() is the Brass version, so only the Brass component of buzz is displayed.

## Destructor Considerations

As mentioned earlier, a base class destructor should be virtual. That way, when you delete a derived object via a base-class pointer or reference to the object, the program uses the derived-class destructor followed by the base-class destructor rather than using only the base-class destructor.

## Friend Considerations

Because a friend function is not actually a class member, it’s not inherited. However, you might still want a friend function to a derived class to use a friend to the base class. The way to accomplish this is to type cast a derived-class reference or pointer to the base-class equivalent and to then use the type cast reference or pointer to invoke the base-class friend:

```cpp
ostream & operator<<(ostream & os, const hasDMA & hs)
{
    // type cast to match operator<<(ostream & , const baseDMA &)
    os << (const baseDMA &) hs;
    os << "Style: " << hs.style << endl;
    return os;
}
```

You can also use the dynamic_cast<> operator, discussed in Chapter 15, “Friends, Exceptions, and More,” for the type cast:

```cpp
os << dynamic_cast<const baseDMA &> (hs);
```

For reasons discussed in Chapter 15, this would be the preferred form of type cast.
