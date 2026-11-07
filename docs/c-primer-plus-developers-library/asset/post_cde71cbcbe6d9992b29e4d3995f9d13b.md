
is a friend to the baseDMA class. The next problem is that because friends are not member functions, you can’t use the scope-resolution operator to indicate which function to use. The solution to this problem is to use a type cast so that prototype matching will select the correct function. Thus, the code type casts the type `const hasDMA &` parameter to a type `const baseDMA &` argument:

```cpp
std::ostream & operator<<(std::ostream & os, const hasDMA & hs)
{
// use type cast to match operator<<(ostream & , const baseDMA &)
os << (const baseDMA &) hs;
os << "Style: " << hs.style << endl;
return os;
}
```

Listing 13.16 tests the baseDMA, lacksDMA, and hasDMA classes in a short program.

## Listing 13.16 `usedma.cpp`

```cpp
// usedma.cpp -- inheritance, friends, and DMA
// compile with dma.cpp
#include <iostream>
#include "dma.h"
int main()
{
    using std::cout;
    using std::endl;

    baseDMA shirt("Portabelly", 8);
    lacksDMA balloon("red", "Blimpo", 4);
    hasDMA map("Mercator", "Buffalo Keys", 5);
    cout << "Displaying baseDMA object:\n";
    cout << shirt << endl;
    cout << "Displaying lacksDMA object:\n";
    cout << balloon << endl;
    cout << "Displaying hasDMA object:\n";
    cout << map << endl;
    lacksDMA balloon2(balloon);
    cout << "Result of lacksDMA copy:\n";
    cout << balloon2 << endl;
    hasDMA map2;
    map2 = map;
    cout << "Result of hasDMA assignment:\n";
    cout << map2 << endl;
    return 0;
}
```

Here’s the output of the program in Listings 13.14, 13.15, and 13.16:

```
Displaying baseDMA object:
Label: Portabelly
Rating: 8

Displaying lacksDMA object:
Label: Blimpo
Rating: 4
Color: red

Displaying hasDMA object:
Label: Buffalo Keys
Rating: 5
Style: Mercator

Result of lacksDMA copy:
Label: Blimpo
Rating: 4
Color: red

Result of hasDMA assignment:
Label: Buffalo Keys
Rating: 5
Style: Mercator
```

## Class Design Review

C++ can be applied to a wide variety of programming problems, and you can’t reduce class design to some paint-by-numbers routine. However, there are some guidelines that often apply, and this is as good a time as any to go over them by reviewing and amplifying earlier discussions.

## Member Functions That the Compiler Generates for You

As first discussed in Chapter 12, the compiler automatically generates certain public member functions, termed *special member functions*. The fact that it does so suggests that these special member functions are particularly important. Let’s look again at some of them now.

## Default Constructors

A default constructor is one that has no arguments, or else one for which all the arguments have default arguments. If you don’t define any constructors, the compiler defines a default constructor for you. Its existence allows you to create objects. For example, suppose *Star* is a class. You need a default constructor to use the following:

```cpp
Star rigel;        // create an object without explicit initialization
Star pleiades[6];  // create an array of objects
```

One more thing an automatic default constructor does is call the default constructors for any base classes and for any members that are objects of another class.

Also if you write a derived-class constructor without explicitly invoking a base-class constructor in the member initializer list, the compiler uses the base class default constructor to construct the base class portion of the new object. If there is no base-class default constructor, you get a compile-time error in this situation.

If you define a constructor of any kind, the compiler does not define a default constructor for you. In that case, it’s up to you to provide a default constructor if one is needed.

Note that one of the motivations for having constructors is to ensure that objects are always properly initialized. Also if a class has any pointer members, they certainly should be initialized. Thus, it’s a good idea to supply an explicit default constructor that initializes all class data members to reasonable values.

## Copy Constructors

A copy constructor for a class is a constructor that takes an object of the class type as its argument. Typically, the declared parameter is a constant reference to the class type. For example, the copy constructor for a Star class would have this prototype:

```cpp
Star(const Star &);
```

A class copy constructor is used in the following situations:

- When a new object is initialized to an object of the same class
- When an object is passed to a function by value
- When a function returns an object by value
- When the compiler generates a temporary object

If a program doesn’t use a copy constructor (explicitly or implicitly), the compiler provides a prototype but not a function definition. Otherwise, the program defines a copy constructor that performs memberwise initialization. That is, each member of the new object is initialized to the value of the corresponding member of the original object. If a member is itself a class object, then memberwise initialization uses the copy constructor defined for that particular class.

In some cases, memberwise initialization is undesirable. For example, member pointers initialized with new generally require that you institute deep copying, as with the baseDMA class example. Or a class may have a static variable that needs to be modified. In such cases, you need to define your own copy constructor.

## Assignment Operators

A default assignment operator handles assigning one object to another object of the same class. Don’t confuse assignment with initialization. If a statement creates a new object, it’s using initialization, and if a statement alters the value of an existing object, it’s assignment.

```cpp
Star sirius;
Star alpha = sirius;    // initialization (one notation)
Star dogstar;
dogstar = sirius;        // assignment
```

Default assignment uses memberwise assignment. If a member is itself a class object, then default memberwise assignment uses the assignment operator defined for that particular class. If you need to define a copy constructor explicitly, you also need, for the same reasons, to define the assignment operator explicitly. The prototype for a Star class assignment operator is this:

```cpp
Star & Star::operator=(const Star &);
```

Note that the assignment operator function returns a reference to a Star object. The baseDMA class shows a typical example of an explicit assignment operator function. The compiler doesn’t generate assignment operators for assigning one type to another. Suppose you want to be able to assign a string to a Star object. One approach is to define such an operator explicitly:

```cpp
Star & Star::operator=(const char *) {...}
```

A second approach is to rely on a conversion function (see “Conversion Considerations” in the next section) to convert a string to a Star object and use the Star-to-Star assignment function. The first approach runs more quickly but requires more code. The conversion function approach can lead to compiler-befuddling situations.

Chapter 18, “Visiting with the New C++ Standard,” discusses two more special methods added by C++11: the move constructor and the move assignment operator.

## Other Class Method Considerations

There are several other points to keep in mind as you define a class. The following sections list some of them.

## Constructor Considerations

Constructors are different from other class methods in that they create new objects, whereas other methods are invoked by existing objects. This is one reason constructors aren’t inherited. Inheritance means a derived object can use a base-class method, but, in the case of constructors, the object doesn’t exist until after the constructor has done its work.

## Destructor Considerations

You need to remember to define an explicit destructor that deletes any memory allocated by new in the class constructors and takes care of any other special bookkeeping that destroying a class object requires. If the class is to be used as a base class, you should provide a virtual destructor even if the class doesn’t require a destructor.
