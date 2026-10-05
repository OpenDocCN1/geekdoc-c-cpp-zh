# CHAPTER 7 Constructors and Other Tools

> TIP: (continued)

You should recognize the following as a legal way to declare an object of type
SampleClass and call the constructor for that class:

SampleClass myVariable(7, 7.77);

However, the following is illegal:

SampleClass yourVariable;

The compiler interprets the previous declaration including a call to a constructor
with no arguments, but there is no definition for a constructor with zero arguments.
You must either add two arguments to the declaration of yourVariable or else add a
constructor definition for a constructor with no arguments.

If you refine the class SampleClass as follows, the previous declaration of
yourVariable would be:

```
class SampleClass
{
public:
    SampleClass(int parameter1, double parameter2);
    SampleClass( ); // Default constructor
    void doStuff();
private:
    int data;
    double data2;
}
```

To avoid this sort of confusion, you should always include a default constructor in any
class you define. If you do not want the default constructor to initialize any member
variables, you can simply give it an empty body when you implement it. The following
constructor definition is perfectly legal. It does nothing but create an uninitialized object:

```
SampleClass::SampleClass() 
/*/Do nothing.*/ */
```

# Constructors with No Arguments

A constructor that takes no arguments is called a default constructor. When you declare an
object and want the constructor with zero arguments to be called, you do not include any
parenheses. For example, to declare an object and pass two arguments to the constructor,
might you do the following:

```
DayYear date(12, 31);
```

However, if you want the constructor with zero arguments to be used, you declare the
object as follows:

```
DayYear date;
```