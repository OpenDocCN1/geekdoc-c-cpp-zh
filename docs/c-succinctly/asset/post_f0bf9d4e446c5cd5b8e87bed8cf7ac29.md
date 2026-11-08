
There is an alternate way to define an inline member function. If you want to keep your class definitions nice and clean, with no member function definitions within them, but still want to have some inline member functions, you can do something like the following instead:

### Sample: SimpleClassSample\Vehicle.h (alternate code commented out at the bottom of the file)

```cpp
#pragma once
#include <string>

namespace Inventory
{
    enum class VehicleCondition;

    class Vehicle
    {
    public:
        Vehicle(
            VehicleCondition condition,
            double pricePaid
        );

        ~Vehicle(void);

        inline VehicleCondition GetVehicleCondition(void);

        void SetVehicleCondition(VehicleCondition condition);

        inline double GetBasis(void);

    private:
        VehicleCondition                 m_condition;
        double                           m_basis;
    };

    VehicleCondition Vehicle::GetVehicleCondition(void)
    {
        return m_condition;
    }

    double Vehicle::GetBasis(void)
    {
        return m_basis;
    }
}
```

As you can see, after the class declaration, we defined the member functions we wanted inline, just as we would if they were in a source file. The key difference is that the function declarations in the class are preceded by the `inline` keyword, and the function definitions are in the header file itself. If you leave that keyword off, you will get a linker error as in Figure 1.

![](img/e4d68f5a79326a8404dad75080806b64_36_0.png)

*Figure 1: The result of leaving the `inline` keyword off of the `Vehicle::GetVehicleCondition` member function.*

Linker errors are always horrible looking, by the way. The reason is that the linker no longer knows what your variables and functions were named in the source file. It only knows what the compiler transformed those names into in order to make all the names unique. This includes overloaded methods, which need a unique name at the linking stage so the linker can connect a call to an overloaded member function to the correct overloaded version of that function.

The errors in Figure 1 are simply telling us that we defined `Inventory::Vehicle::GetVehicleCondition(void)` more than once. Now, we know we only defined it once, just in the header file, but we have included the header file in both **Vehicle.cpp** and in **Main.cpp** in the **SimpleClassSample** project.

Since we intentionally forgot to add the `inline` keyword to the `Vehicle::GetVehicleCondition` function declaration, the compiler doesn’t make the code inline. Instead, it compiles it as a function in both **Main.cpp** and **Vehicle.cpp**.

This, of course, is something the compiler is fine with because it treats each source file as a unique compilation unit. The compiler doesn’t know any better, since, by the time the code reaches it, the code has already been inserted by the preprocessor stage. Only when the linker gets all the compiled code and tries to match everything up do we reach a phase where the build process says, “Hey, I already have another version of this function!” and then fails.

As you can see, there are two ways of making member functions inline. Both must be done within the header file since the compiler will evaluate the header-file code as many times as they are included, but it will only run through source files once. If you use the second method and forget an `inline` keyword, then you will have horrible linker errors. If you use the second method and remember the `inline` keyword, but define the functions within the source file, you will get horrible linker errors—this time saying there is no definition.

> **Tip:** Don’t try to make everything inline. You will just end up with slow compile times that kill your productivity. Do inline things that make sense, like simple getter and setter functions for member variables. Like anything else, profile first, and then optimize if needed.

## Protection Levels and Access Specifiers

Member functions and member data have three possible access specifiers:

- `public`
- `protected`
- `private`

These access specifiers denote the level of accessibility that the member has. In **SampleClass\Vehicle.h**, you can see two examples of how these are used. Note that unlike in C#, you do not restate the access specifier in front of each member. Instead, you state the access specifier, followed by a colon (e.g., `public:`), and then every declaration and definition that comes after is given that level of accessibility until you reach another access specifier.

By default, class members are private. This means if you have no access specifier at the beginning of the class declaration, then all members that are declared will be private until an access specifier is reached. If none is reached, you'd have an entirely private class, which would be very odd.

Structure members default to public, so on occasion you'll see a structure without any access specifiers. If you wish to use them in a structure, though, they work the same as in a class.

Lastly, you can use the same access specifier more than once; if you want to organize your class so you define the member functions first and then the member variables (or vice versa), you could easily do something like this:

*Note: This code is expository only; it is not included in any of the samples.*

```cpp
#include <string>

class SomeClass
{
public:
    SomeClass(void);
    virtual ~SomeClass(void);
    int AddTwoInts(int, int);
    void StoreAString(const wchar_t*);

private:
    bool CheckForIntAdditionOverflow(int, int);

public:
    int SomePublicInteger;

protected:
    std::wstring m_storedString;
};
```

The previous class definition doesn't define anything particularly useful. However, it does serve as an example of the use of all three access specifiers. It also demonstrates that you can use specifiers more than once, such as public in the previous example.

## Inheritance

When specifying classes that your class derives from in C++, you should also specify an access specifier. If not, you will get the default access levels: private for a class and public for a structure. Note that I said classes. C++ supports multiple-inheritance. This means a class or structure can have more than one direct base class or structure, unlike C# where a class can have only one parent.

C++ does not have a separate interface type. In general, multiple-inheritance should be avoided except as a workaround for lack of a separate interface. In other words, a class should have only zero or one real base class along with zero or more purely abstract classes (interfaces). This is just a personal style recommendation, though.

There are some good arguments for multiple-inheritance. For instance, say you have three groups of functionality. Each one consists of functions and data. Then say each group is unrelated to the other—there’s no connection between them, but they aren’t mutually exclusive. In this case, you may wish to put each functionality group into its own class. Then if you have a situation where you want to create a class needing two of these groups, or even all three, you can simply create a class that inherits from all three, and you’re done.

Or, you’re done as long as you didn’t have any naming conflicts in your public and protected members’ functions and variables. For example, what if all three of the functionality groups have a member function `void PrintDiagnostics(void);`? You’d be doomed, yes? Well, it turns out that no, you are not doomed (usually). You need to use some weird syntax to specify which base class `PrintDiagnostics` function you want. And even then you aren’t quite done.

C++ lets you specify whether you want a class to be a plain base class or a virtual base class. You do this by putting or not putting the keyword `virtual` before the class’ name in the base class specifier. We’ll look at a sample shortly that addresses all of this, but before we do, it’s important to understand that if you inherit a class at least twice, and two or more of the inheritances are not virtual, you will end up with multiple copies of that class’ data members.

This causes a whole bunch of problems when trying to specify which of those you wish to use. Seemingly, the solution is to derive from everything virtually, but that has a run-time performance hit associated with it due to how C++ implementations tend to resolve virtual members. Better still, try to avoid having this ever happen in the first place, but as that’s not always possible, do remember virtual inheritance.

And now a sample to help make this all make sense:

### Sample: InheritanceSample\InheritanceSample.cpp

```cpp
#include <iostream>
#include <ostream>
#include <string>
#include <typeinfo>
#include "../pchar.h"

using namespace std;

class A
{
public:
    A(void) : SomeInt(0) { }
    virtual ~A(void) { }

    const wchar_t* Id(void) const { return L"A"; }

    virtual const wchar_t* VirtId(void) const { return L"A"; }

    int GetSomeInt(void) const { return SomeInt; }
    int                 SomeInt;
};

class B1 : virtual public A
```
