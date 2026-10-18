
The opposite conversion, shown in Figure 4.22, is implemented as `operator double()`, as shown on lines [33–34]. Again, on line [37], the scaling Eq. (7.14) is used, but this time in the opposite direction. Hence, on line [38], the fractional part is divided by the value corresponding to the least significant bit of the integer part. In other words, this corresponds to a bit value of the integer 1, which happens to be the value of the `kIntegerLSB` bit in the `fValue` member.

Then, on line [40], the integer part is added to the result; and on line [41], the proper sign is set.

**Listing 7.3  Definition of the type-converting operator `double()` (in *CppBookCode, FxFor.h*).**

```cpp
// We repeat the same code as for the "double" conversion to
// avoid implicit conversion from "float" to "double" if additional
// function were used.
template<typename ST, int Prec, typename ACC_TYPE >
constexpr FxFor< ST, Prec, ACC_TYPE >::operator double() const
{
    // Start from the fraction
    double retVal = static_cast< double >( GetFractionalPart() )
                  / static_cast< double >( kIntegerLSB );

    retVal += GetMagnitudeOfIntegerPart();      // now add the integer part
    return IsNegative() ? - retVal : retVal;
}
```

We will now move on to some characteristic arithmetic operators. First is the prefix increment operator, whose definition starts on lines [44–45]. On line [47], it simply calls the increment operator `+=`, which we present later. Then, the same object needs to be returned. This is done on line [48], simply by returning `* this`.

The postfix version of the increment operator starts on lines [53–54]. To distinguish the two, the postfix version is equipped with the dummy formal parameter `int`. However, its implementation is slightly more complicated, since the "old" version needs to be returned, whereas the object needs to be incremented by 1. Hence, on line [56], a new object is created by calling the copy constructor provided with the `* this` object. Then, as in the previous function, the object is incremented by calling the `+=` operator with argument 1 on line [57]. Finally, the stored object is returned on line [58]. Knowing the precise operation of the prefix and postfix operators tells us why the postfix operators are much more expensive during computations. This happens mostly because an intermediate object needs to be created and returned. Here it is not a big deal, but imagine doing increments on a matrix.

**Listing 7.4  Definition of the prefix and postfix increment operators (in *CppBookCode, FxFor.h*).**

```cpp
// prefix
template<typename ST, int Prec, typename ACC_TYPE >
constexpr typename FxFor< ST, Prec, ACC_TYPE >::FxType & FxFor< ST, Prec, ACC_TYPE >::operator ++ ()
{
    * this += 1;
    return * this;
}

// postfix
template<typename ST, int Prec, typename ACC_TYPE >
constexpr typename FxFor< ST, Prec, ACC_TYPE >::FxType FxFor< ST, Prec, ACC_TYPE >::operator ++ ( int )
{
    FxType tmp( * this );    // this unfortunately requires a temporary copy
    * this += 1;
    return tmp;
}
```

Now it is time for the two most basic arithmetic operations. First is the add and assign operator `+=`, defined on lines [60–61] (see GROUP 15, Table 3.15). Summation is simple, except that the different combinations of the signs need to be properly considered. The signs are read in on lines [65–66]. Then, we select a proper summation algorithm in the double if statements. Let’s consider the case where the first argument (i.e. the one represented by `this`) is negative and the second is positive (i.e. the `f` object): for example, in the expression −13.5 + 10.0. On line [86], the first object is made positive. If `fValue` is less than `f.fValue`, then `fValue` is subtracted on line [92], and we are finished, since the result will be positive. Otherwise, as in the previous example, the subtraction 13.5 − 10.0 will take place on line [96], resulting in 3.5; its sign will be changed on line [99] to provide the final result, −3.5. But we need to avoid assigning a minus sign to a zero value, as checked on line [98]. This is one of the peculiarities of the SM representation.

**Listing 7.5  Definition of the add and assign operator `+=` (in *CppBookCode, FxFor.h*).**

```cpp
template< typename ST, int Prec, typename ACC_TYPE >
constexpr typename FxFor< ST, Prec, ACC_TYPE >::FxType &
                    FxFor< ST, Prec, ACC_TYPE >::operator += ( FxType f )
{
    // We perform the sign-magnitude arithmetic
    bool first_is_negative  = IsNegative();
    bool second_is_negative = f.IsNegative();

    if( first_is_negative )
    {
        if( second_is_negative )
        {
            // Both are negative

            MakeAbs();          // Take the absolute value of the first operand
            f.MakeAbs();        // Take the absolute value of the second operand

            fValue += f.fValue; // Add the bare magnitudes;

            MakeNegative();     // And negate the result
        }
        else
        {
            // The first is negative, the second is positive

            MakeAbs(); // simply operate on magnitude (disregarding the sign bit)

            // Here we compare only the magnitudes,
            // The second is positive, so there is no need to get its abs
            if( fValue <= f.fValue ) // "soft" to make 0 positive
            {
                fValue = f.fValue - fValue; // and we do NOT change the sign
            }
            else
            {
                fValue -= f.fValue;
                assert( IsPositive() );
                if( fValue != 0 )
                    MakeNegative();        // and negate the result
            }
        }
    }
    else
    {
        if( second_is_negative )
        {
            // The first is positive, the second is negative

            f.MakeAbs();   // simply operate on magnitude (disregarding the sign bit)

            // Here we compare only the magnitudes;
            // The first is positive, so there is no need to get its abs
            if( fValue >= f.fValue )  // "soft" to make 0 positive
            {
                fValue -= f.fValue;  // and we do NOT change the sign
            }
            else
            {
                fValue = f.fValue - fValue;
                assert( IsPositive() );
                if( fValue != 0 )
                    MakeNegative();        // and negate the result
            }
        }
        else
        {
            // Both are positive

            fValue += f.fValue;
        }
    }

    return * this;
}
```

The implementation of multiplication in SM is much shorter, as shown in the definition of `operator *=` beginning on lines [135–137]. Again, the signs of the two operands are read and stored in temporary objects, as shown on lines [140–141]. Then, on line [144], the temporary object `theAccumulator` is created. Not surprisingly, it is the longest possible bit representation of `ACC_TYPE`, since its role is to store the result of the multiplication on line [150]. Then `theAccumulator` needs to be properly scaled by right-shifting the `kPrec` bits, as done on line [155]. At first, we may think that two such shifts are necessary. But one of them was done previously, since by the arrangement of `fValue`, the binary point is already `kPrec` bits to the left. On line [158], the adjusted accumulator is converted and copied to the `fValue` object. Hence, we have to be sure the result fits with no integer overflow. Finally, the sign is set on lines [161–162], and the current object is returned on line [164].

**Listing 7.7  Definition of the template `ComputeRoundingError` function for computing the difference between floating-point and fixed-point representations (in *CppBookCode, FxFor.h*).**

```cpp
//////////////////////////////
// This function returns the difference in representations
// between double and FxFor<>
//////////////////////////////
//
// INPUT:
//        d - an input double value
//        f - FxFor<> to be checked
//
// OUTPUT:
//        difference (as a double value) between double
//        and fixed representation of this number

template< typename D, int P, typename A >
constexpr auto ComputeRoundingError( const double d, const FxFor< D, P, A > f )
{
    auto diff( d - static_cast< double >( f ) );
    return diff < 0.0 ? -diff : diff;   // std::fabs failed to be constexpr friendly
}
```

Finally, on lines [188–191], a number of useful alias names are introduced with the `using` directive. Two special names for purely fractional types are created on lines [195–196].

**Listing 7.8  Definitions of useful alias names for some common types created from the `FxFor` class (in *CppBookCode, FxFor.h*).**

```cpp
// Here we define the specific data types. Be careful, however,
// to check the size of built-in types on your machine.

using FX_8_8      = FxFor< unsigned short, 8 >;
using FX_16_16    = FxFor< unsigned int, 16 >;
using FX_24_8     = FxFor< unsigned int, 8 >;
using FX_8_24     = FxFor< unsigned int, 24 >;

// The following types are for normalized numbers
// for which their magnitude is less than 1.0.
using FX_PURE_FRACT_15 = FxFor< unsigned short, 15 >;
using FX_PURE_FRACT_31 = FxFor< unsigned int, 31 >;
```

### 7.3.4  Applications of FxFor

Now that `FxFor` is ready, it is time to check its operation. However, we will start with some useful helpers, shown in Listing 7.9.

Lines [3–4] define a `template constexpr` for a constant value. It takes the value of a constant pi assigned to a type given during template instantiation. This way, we can define `gkPi< double >`, `gkPi< float >`, or `gkPi< FX_8_8 >`, as we will see soon.

**Listing 7.9  Helper utilities (in *CppBookCode, FixedPtArithm.cpp*).**

```cpp
// New way of defining constants
// with variable templates
template< typename T >
constexpr T gkPi = T( 3.1415926535897932385 );
```
