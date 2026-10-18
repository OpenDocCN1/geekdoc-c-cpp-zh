The opposite conversion, shown in Figure 4.22, is implemented as `operator double()`, as shown on lines [33–34]. Again, on line [37], the scaling Eq. (7.14) is used, but this time in the opposite direction. Hence, on line [38], the fractional part is divided by the value corresponding to the least significant bit of the integer part. In other words, this corresponds to a bit value of the integer 1, which happens to be the value of the `kIntegerLSB` bit in the `fValue` member.

Then, on line [40], the integer part is added to the result; and on line [41], the proper sign is set.

```
Listing 7.3  Definition of the type-converting operator double() (in CppBookCode, FxFor.h).

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
```

We will now move on to some characteristic arithmetic operators. First is the prefix increment operator, whose definition starts on lines [44–45]. On line [47], it simply calls the increment operator `+=`, which we present later. Then, the same object needs to be returned. This is done on line [48], simply by returning `* this`.

The postfix version of the increment operator starts on lines [53–54]. To distinguish the two, the postfix version is equipped with the dummy formal parameter `int`. However, its implementation is slightly more complicated, since the “old” version needs to be returned, whereas the object needs to be incremented by 1. Hence, on line [56], a new object is created by calling the copy constructor provided with the `* this` object. Then, as in the previous function, the object is incremented by calling the `+=` operator with argument 1 on line [57]. Finally, the stored object is returned on line [58]. Knowing the precise operation of the prefix and postfix operators tells us why the postfix operators are much more expensive during computations. This happens mostly because an intermediate object needs to be created and returned. Here it is not a big deal, but imagine doing increments on a matrix.

```
Listing 7.4  Definition of the prefix and postfix increment operators (in CppBookCode, FxFor.h).

```cpp
// prefix
template<typename ST, int Prec, typename ACC_TYPE >
typename constexpr FxFor< ST, Prec, ACC_TYPE >::FxType & FxFor< ST, Prec, ACC_TYPE >::operator ++ ()
{
    * this += 1;
    return * this;
}

// postfix
template<typename ST, int Prec, typename ACC_TYPE >
```
```