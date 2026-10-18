The code fragment starting on line [59] contains the public construction group. First is the default constructor. Obviously, fValue is set to 0 in the initializer on line [63]. Then, in the constructor body, some preconditions are set in the form of assertions. The first `static_assert` will be checked during compilation, so all of its arguments must be known at this time. But the second `static_assert`, which is commented out, does not fulfill this rule since fValue will not be known during compilation. So, this condition cannot be used in the static assertion. On the other hand, the `assert` on line [67] will not be checked until runtime. Its role is to verify the precondition on a relation between a total number of bits in the supporting type ST and the number of precision bits, both chosen as template parameters by the programmer. This assert is redundant since the previous `static_assert`, with the same condition, will always be checked before runtime.

The parametric constructor on line [71] accepts one int value to create the FxFor object. So, it serves as a type converter from int to FxFor, as presented in Section 4.15.3.1.

The transformation from integer types is simple – the argument needs to be shifted left by the number of bits in the fractional part, denoted by kPrec. The sign needs to be properly set in the SM format. All this is done on line [74]. We will explain the conversion from double (declared on line [77]) later, since its full definition is located outside the definition of the FxFor class.

```
```cpp
public:

    // ======================================================
    // Class default constructor
    constexpr FxFor( void ) : fValue( 0 )
    {
        static_assert( sizeof( ST ) * 8 > kPrec );
        //static_assert( fValue >= 0 ); will not compile since fValue is not known
        assert( sizeof( ST ) * 8 > kPrec );
    }

    // Type converting constructors
    constexpr FxFor( int x )
    {
        assert( sizeof( ST ) * 8 > kPrec );
        fValue = x < 0 ? -x << kPrec | kSignMask : x << kPrec;
    }

    constexpr FxFor( double x );
```
```

The FxFor class copy constructor, whose definition starts on line [80], is a template member function that lets us create one FxFor object from one with different parameters (Section 4.8.5). At the same time, it is also a type-converting constructor that helps transform one FxFor object into another version of FxFor with potentially different template parameters. Note that when analyzing this function, we have to consider not three but all six template parameters: three for this class and (potentially) a different three for the FxFor object passed as the argument f on line [81].

The conversion is not difficult and consists of copying and properly placing the integer and fractional parts of the provided argument, as done on lines [84, 86–87]. Finally, on lines [89–90], the sign is copied as well. But a problem arises if the source object has more bits than the object we copy to. In this case, depending on the value, important data may be lost.