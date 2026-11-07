
## Conversion Considerations

Any constructor that can be invoked with exactly one argument defines conversion from the argument type to the class type. For example, consider the following constructor prototypes for a Star class:

```cpp
Star(const char *);               // converts char * to Star
Star(const Spectral &, int members = 1); // converts Spectral to Star
```

Conversion constructors are used, for example, when a convertible type is passed to a function that is defined as taking a class argument. For instance, suppose you have the following:

```cpp
Star north;
north = "polaris";
```

The second statement would invoke the Star::operator=(const Star &) function, using Star::Star(const char *) to generate a Star object to be used as an argument for the assignment operator function. This assumes that you haven't defined a (char *)-to-Star assignment operator.

Using explicit in the prototype for a one-argument constructor disables implicit conversions but still allows explicit conversions:

```cpp
class Star
{
...
public:
    explicit Star(const char *);
...
};

Star north;
north = "polaris";          // not allowed
north = Star("polaris");    // allowed
```

To convert from a class object to some other type, you define a conversion function (see Chapter 11, "Working with Classes"). A conversion function is a class member function with no arguments or declared return type that has the name of the type to be converted to. Despite having no declared return type, the function should return the desired conversion value. Here are some examples:

```cpp
Star::operator double() {...}        // converts Star to double
Star::operator const char *() {...} // converts Star to const char *
```

You should be judicious with such functions, only using them if they make good sense. Also, with some class designs, having conversion functions increases the likelihood of writing ambiguous code. For example, suppose you define a double conversion for the Vector type of Chapter 11, and suppose you have the following code:

```cpp
Vector ius(6.0, 0.0);
Vector lux = ius + 20.2;        // ambiguous
```

The compiler could convert ius to double and use double addition, or else it could convert 20.2 to Vector (using one of the constructors) and use vector addition. Instead, it would do neither and inform you of an ambiguous construction.

C++11 provides the option of using the keyword explicit with conversion functions. As with constructors, explicit allows explicit conversions using type casts, but disallows implicit conversions.

### Passing an Object by Value Versus Passing a Reference

In general, if you write a function using an object argument, you should pass the object by reference rather than by value. One reason for this is efficiency. Passing an object by value involves generating a temporary copy, which means calling the copy constructor and then later calling the destructor. Calling these functions takes time, and copying a large object can be quite a bit slower than passing a reference. If the function doesn't modify the object, you should declare the argument as a const reference.

Another reason for passing objects by reference is that, in the case of inheritance using virtual functions, a function defined as accepting a base-class reference argument can also be used successfully with derived classes, as you saw earlier in this chapter. (Also see the section "Virtual Methods," later in this chapter.)

### Returning an Object Versus Returning a Reference

Some class methods return objects. You've probably noticed that some members return objects directly whereas others return references. Sometimes a method must return an object, but if it isn't necessary, you should use a reference instead. Let's look at this more closely.

First, the only coding difference between returning an object directly and returning a reference is in the function prototype and header:

```cpp
Star nova1(const Star &);      // returns a Star object
Star & nova2(const Star &);     // returns a reference to a Star
```

Next, the reason you should return a reference rather than an object is that returning an object involves generating a temporary copy of the returned object. It's the copy that is made available to the calling program. Thus, returning an object involves the time cost of calling a copy constructor to generate the copy and the time cost of calling the destructor to get rid of the copy. Returning a reference saves time and memory use. Returning an object directly is analogous to passing an object by value; both processes generate temporary copies. Similarly, returning a reference is analogous to passing an object by reference: both the calling and the called function operate on the same object.

However, it's not always possible to return a reference. A function shouldn't return a reference to a temporary object created in the function because the reference becomes invalid when the function terminates and the object disappears. In this case, the code should return an object in order to generate a copy that will be available to the calling program.

As a rule of thumb, if a function returns a temporary object created in the function, you shouldn't use a reference. For example, the following method uses a constructor to create a new object, and it then returns a copy of that object.

```cpp
Vector Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}
```

If a function returns an object that was passed to it via a reference or pointer, you should return the object by reference. For example, the following code returns, by reference, either the object that invokes the function or else the object passed as an argument:

```cpp
const Stock & Stock::topval(const Stock & s) const
{
    if (s.total_val > total_val)
        return s;               // argument object
    else
        return *this;           // invoking object
}
```

## Using const

You need to be alert to opportunities to use const. You can use it to guarantee that a method doesn't modify an argument:

```cpp
Star::Star(const char * s) {...} // won't change the string to which s points
```

You can use const to guarantee that a method won't modify the object that invokes it:

```cpp
void Star::show() const {...} // won't change invoking object
```

Here const means const Star *this, where this points to the invoking object. Normally, a function that returns a reference can be on the left side of an assignment statement, which really means you can assign a value to the object referred to. But you can use const to ensure that a reference or pointer return value can't be used to modify data in an object:

```cpp
const Stock & Stock::topval(const Stock & s) const
{
    if (s.total_val > total_val)
        return s;               // argument object
    else
        return *this;           // invoking object
}
```

Here the method returns a reference either to this or to s. Because this and s are both declared const, the function is not allowed to change them, which means the returned reference also must be declared const.

Note that if a function declares an argument as a reference or pointer to a const, it cannot pass along that argument to another function unless that function also guarantees not to change the argument.

## Public Inheritance Considerations

Naturally, adding inheritance to a program brings up a number of considerations. Let’s look at a few.

### Is-a Relationship Considerations

You should be guided by the *is-a* relationship. If your proposed derived class is not a particular kind of the base class, you shouldn’t use public derivation. For example, you shouldn’t derive a Programmer class from a Brain class. If you want to represent the belief that a programmer has a brain, you should use a Brain class object as a member of the Programmer class.

In some cases the best approach may be to create an abstract base class with pure virtual functions and to derive other classes from it.

Remember that one expression of the *is-a* relationship is that a base class pointer can point to a derived-class object and that a base-class reference can refer to a derived-class object without an explicit type cast. Also remember that the reverse is not true; thus, you cannot have a derived-class pointer or reference refer to a base-class object without an explicit type cast. Depending on the class declarations, such an explicit type cast (a down-cast) may or may not make sense. (You might want to review Figure 13.4.)

### What’s Not Inherited

Constructors are not inherited. That is, creating a derived object requires calling a derived-class constructor. However, derived-class constructors typically use the member-initializer list syntax to call base-class constructors to construct the base class portion of a derived object. If the derived-class constructor doesn’t explicitly call a base-class constructor by using the member-initializer list syntax, it uses the base class’s default constructor. In an inheritance chain, each class can use a member initializer list to pass back information to its immediate base class. C++11 adds a mechanism that enables the inheriting of constructors. However, the default behavior is still that constructors are not inherited.

Destructors are not inherited either. However, when an object is destroyed, the program first calls the derived destructor and then the base destructor. If there is a default base class destructor, the compiler generates a default derived class destructor. Generally speaking, if a class serves as a base class, its destructor should be virtual.

Assignment operators are not inherited. The reason is simple. An inherited method has the same function signature in a derived class as it does in the base class. However, an assignment operator has a function signature that changes from class to class because it has a formal parameter that is the class type. Assignment operators do have some interesting properties, which we’ll look at next.
