# **Listing 7.1** Definition of the template `FxFor` class for representing the FX arithmetic format (in `CppBookCode, FxFor.h`).

```
```cpp
///////////////////////////////////////////////
// Class for fixed-point data types.
// No saturation, no overflow control.
// SupportType defines an UNSIGNED integer type for the whole number
// Prec - defines a number of fractional bits
// ACC_TYPE - Accumulator type (for intermediate results)
///////////////////////////////////////////////
template <typename ST, int Prec, typename ACC_TYPE = unsigned long long >
class FxFor
{
private:

    // Stores the whole number
    ST    fValue {};

public:

    // Returns an internal representation in Sign/Magnitude format
    constexpr ST GetInternalValue( void ) const { return fValue; }

    // Returns an internal representation in C2 format
    constexpr ST GetInternalValue_in_C2( void ) const
    { return IsPositive() ? fValue : (~fValue | kSignMask) + 1; }

    constexpr void SetInternalValue( ST new_val ) { fValue = new_val; }

public:

    // Local const for precision
    enum: ST      { kPrec = Prec };

private:

    // Let's define some useful flags
    enum: ST {
        kSignMask   = ST(1) << ( 8 * sizeof( ST ) - 1 ), // sign bit (integer MSB)
        kIntegerLSB = ST(1) << kPrec,                    // LSB of the integer part
        kFractMSB   = kPrec > 0 ? ST(1) << kPrec - ST(1) : 0 // MSB of the fract part
    };


    // A shortcut to this type
    using FxType = FxFor< ST, Prec, ACC_TYPE >;

public:

    // Some raw data manipulators
    constexpr ST DataValueAbs( void ) const
    { return fValue & ~kSignMask; } // Return the absolute value (always positive)

    constexpr ST GetMagnitudeOfIntegerPart( void ) const
    { return DataValueAbs() >> kPrec; }

    constexpr ST GetFractionalPart( void ) const
    { return fValue & ( kIntegerLSB - 1 ); }
    // ( kIntegerLSB - 1 ) sets all bits of the fractional part
```
```