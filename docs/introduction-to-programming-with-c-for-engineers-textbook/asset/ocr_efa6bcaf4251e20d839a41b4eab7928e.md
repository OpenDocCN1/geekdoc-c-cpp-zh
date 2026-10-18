# Listing 7.7 Definition of the template `ComputeRoundingError` function for computing the difference between floating-point and fixed-point representations (in *CppBookCode, FxFor.h*).

```
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
    return diff < 0.0 ? -diff: diff;   // std::fabs failed to be constexpr friendly
}
```
```

Finally, on lines [188–191], a number of useful alias names are introduced with the using directive. Two special names for purely fractional types are created on lines [195–196].

# Listing 7.8 Definitions of useful alias names for some common types created from the FxFor class (in *CppBookCode, FxFor.h*).

```
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
```

# 7.3.4  Applications of FxFor

Now that FxFor is ready, it is time to check its operation. However, we will start with some useful helpers, shown in Listing 7.9.

Lines [3–4] define a `template constexpr` for a constant value. It takes the value of a constant pi assigned to a type given during template instantiation. This way, we can define `gkPi< double >`, `gkPi< float >`, or `gkPi< FX_8_8 >`, as we will see soon.

# Listing 7.9 Helper utilities (in *CppBookCode, FixedPtArithm.cpp*).

```
```cpp
// New way of defining constants
// with variable templates
template< typename T >
constexpr T gkPi = T( 3.1415926535897932385 );
```
```