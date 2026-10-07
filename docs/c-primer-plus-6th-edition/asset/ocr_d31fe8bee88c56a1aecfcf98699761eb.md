```
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
Employee veep;
Singer trala;
...
Employee * pe = &trala;
Singer * ps = (Singer *) &veep;
...
pe->show_name();
ps->range();
```

upcast—implicit type cast allowed

downcast—explicit type cast required

Upcasting leads to a safe operation because a Singer is an Employee (every Singer inherits name).

Downcasting can lead to an unsafe operation because an Employee isn’t a Singer (an Employee need not have a range() method).

Figure 13.4 Upcasting and downcasting.

# Assignment Operator Considerations

If the compiler detects that a program assigns one object to another of the same class, it automatically supplies that class with an assignment operator. The default, or implicit, version of this operator uses memberwise assignment, with each member of the target object being assigned the value of the corresponding member of the source object. However, if the object belongs to a derived class, the compiler uses the base-class assignment operator to handle assignment for the base-class portion of the derived-class object. If you’ve explicitly provided an assignment operator for the base class, that operator is used. Similarly, if a class contains a member that is an object of another class, the assignment operator for that class is used for that member.

As you’ve seen several times, you need to provide an explicit assignment operator if class constructors use new to initialize pointers. Because C++ uses the base-class assignment operator for the base part of derived objects, you don’t need to redefine the assignment operator for a derived class unless it adds data members that require special care. For example, the baseDMA class defines assignment explicitly, but the derived lacksDMA class uses the implicit assignment operator generated for that class.