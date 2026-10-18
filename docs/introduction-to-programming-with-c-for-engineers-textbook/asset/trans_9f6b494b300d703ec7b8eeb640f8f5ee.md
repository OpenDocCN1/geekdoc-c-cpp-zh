
# Listing 4.36 (continued)

```cpp
public:
    enum class ESex { kMan, kWoman };

public:

    PESEL( void ) {}
    PESEL( const string & s ) : BaseClass( s ) {}    // base class from the string

    virtual ~PESEL() {}              // this must be virtual, why?
    // also TLongNumberFor<> should have a virtual destructor
public:
    auto GetYearOfBirth( void )
    {
        return    GetNumberAt( kBirthYear_Dec ) * 10
                + GetNumberAt( kBirthYear_Sngl );
    }

    ESex GetSex( void )
    {
        return ( GetNumberAt( kSex ) & 0x01 ) == 0x01 ?
                ESex::kMan : ESex::kWoman;
    }
};
```

With the following code, we can measure the size of this version of the PESEL class and its base:

```cpp
#include "Derived_PESEL.h"
void Derived_PESEL_Test( void )
{
    std::cout << "Size with inherited object: " << sizeof( PESEL ) << std::endl;
    std::cout << "Size of PESEL::BaseClass: " <<
                sizeof( PESEL::BaseClass ) << std::endl;
}
```

Unfortunately, in this case, the output is much larger than it is for the aggregated version:

```text
Size with inherited object: 16
Size of PESEL::BaseClass: 16
```

The inherited version is larger by 10 bytes, which is necessary to maintain the VFT due to the presence of the virtual destructors.

Hence, in our example, the aggregated version, which wraps the TLongNumberFor object, is preferred.

## 4.15.4.3 LongNumber Project Organization

Since we have one definition of the TLongNumberFor class with preprocessor-defined symbols that guide compilation, we need to properly organize the project into separate translation units.

The source files that set the compilation flags include the headers and define their function, and are separately compiled into objects. The relations among the project files are shown in the UML artifact diagram shown in Figure 4.24.

[PAGE 350]

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_350_0.png)

To maintain the *LongNumberFor.h* header file, which is controlled by the ALLOW_INHERITANCE preprocessor flag, two different translation units are separately compiled. A third is created from the *main.cpp* source file shown in Listing 4.37.

Note that there are only function declarations, which are then invoked. No project headers are included, though.

**Listing 4.37** Definition of `main` with calls to the test functions (in *LongNumber/main.cpp*).

```cpp
#include <iostream>

void LongNumbers_Test( void );
void LongNumbersWithProxy_Test( void );

void Derived_PESEL_Test( void );
void Embedded_PESEL_Test( void );
```

## 4.15.5.1 Definition of the Proxy Class

Listing 4.38 contains the definition of the `RetObjProxy` class, which implements the proxy pattern added to the `TLongNumberFor` class to facilitate different versions of data transfer by the overloaded subscript operators.

**Listing 4.38** Definition of the RetObjProxy nested private class for the proxy pattern to implement full operation of the subscript operator in the TLongNumberFor class (in LongNumber, LongNumberFor.h).

```cpp
#define TURN_ON_PROXY
#ifdef TURN_ON_PROXY     // The following code is compiled if TURN_ON_PROXY is defined
    private:

        // The proxy pattern private area

        // ----------------------------------------------------------
        // This nested class realized the PROXY pattern
        class RetObjProxy
        {
            public:

            using MotherClass = typename TLongNumberFor< MAX_NUMBERS > ;

            private:

                // A const or reference type data member makes the compiler declare
                // a copy assignment operator as deleted.
                // This does not work for us - we need a copy assignment.

                MotherClass * fMyMother {}; // A pointer to the mother class

                int fPosition {};  // Local index storage for the operator []
```

The code associated with the proxy pattern is included in the conditional compilation section on lines [179–266]. This is compiled if the flag `TURN_ON_PROXY` is defined, as on line [178]. This is slightly different behavior than the conditional compilation shown on lines [66–68] of Listing 4.33. In that case, a preprocessor flag is not only defined but also assigned a value, so a condition like `ALLOW_INHERITANCE == 1` can be checked. Here, we only check if `#define TURN_ON_PROXY` is present. Preprocessors are discussed further in Section A.1.

The definition of the nested `RetObjProxy` starts on line [186], which is in the private section of `TLongNumberFor`. `TLongNumberFor` is aliased on line [190] as `MotherClass`. The `RetObjProxy` class has two private members. The first, defined on line [198], is `fMyMother`, a pointer to the `TLongNumberFor` class for which `RetObjProxy` will work. The second, on line [200], is an auxiliary value to hold the current digit position.

The whole idea of using the proxy pattern for subscript operations is shown in Figure 4.25b. Since we cannot simply code the double-side subscript operation, because we cannot address a nibble, we choose an indirect approach with the proxy: when operator [] is called, instead of a reference, a `RetObjProxy` object is returned, which holds a pointer to the main

[PAGE 353]

TLongNumberFor object and the current digit position, as shown on line [257]. This is created by the parametric constructor defined on line [207]. At the same time, we wish to disallow the default constructor, since RetObjProxy must always be attached to a TLongNumberFor object. This would be achieved automatically by defining only the parametric constructor. But to explicitly express our intention, we add =delete, as presented in Section 4.6.1. On line [216], the default constructor is marked as deleted, so it cannot be used.

```
public:
    // Constructor
    // myMother - a TLongNumberFor class we connect to
    // position - index position
    RetObjProxy( MotherClass * myMother, int position ) : fMyMother( myMother ), fPosition( position )
    {
    assert( fMyMother != nullptr );
    assert( fPosition < MotherClass::kMaxNumbers );
    }

    // Forbidden default constructor
    RetObjProxy( void ) = delete;
```

As alluded to previously, the new TLongNumberFor operator [], defined on line [257], returns a RetObjProxy object. But this can happen in two contexts: when a digit is read, or when a digit is written. Naturally, this complies with the right or left value being processed. In both cases, the RetObjProxy members get into the action. Namely, when a RetObjProxy object is on the left side of the assignment and an int object is on the right, then operator = ( int ), defined on line [230], is called. Line [233] delegates the write operation to the mother object by calling fMyMother->SetNumberAt. Then the proxy is returned on line [234] to allow assignment chaining.

If RetObjProxy object is on the right side of the assignment and an int object is expected, then a simple to-int conversion function is called, as defined on line [223], which returns a digit at a given position. Again, the action to read the digit is delegated on line [226] to the mother object.

Finally, as will be shown in the examples, there may be a RetObjProxy object on both the left and right sides of the assignment. In this case, RetObjProxy & operator = ( RetObjProxy & r ), defined on line [239], will be invoked. It copies one digit to the other digit, as shown on lines [242-243]. Then the proxy object is returned on line [244] to allow assignment chaining.

```
public:
    // Called when: int x = id[ 8 ]
    // Right side (read) operation
    // Conversion operator to int - for read operations
    operator int () const
    {
    assert( fMyMother != nullptr );
    return fMyMother->GetNumberAt( fPosition );
    }
```

[PAGE 354]

