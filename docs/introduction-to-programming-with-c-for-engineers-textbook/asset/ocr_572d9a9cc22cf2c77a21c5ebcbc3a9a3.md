```
```cpp
typename constexpr FxFor< ST, Prec, ACC_TYPE >::FxType FxFor< ST, Prec, ACC_TYPE >::operator += ( int )
{
    FxType tmp( * this );    // this unfortunately requires a temporary copy
    * this += 1;
    return tmp;
}
```
```

Now it is time for the two most basic arithmetic operations. First is the add and assign operator +=, defined on lines [60–61] (see GROUP 15, Table 3.15). Summation is simple, except that the different combinations of the signs need to be properly considered. The signs are read in on lines [65–66]. Then, we select a proper summation algorithm in the double if statements. Let’s consider the case where the first argument (i.e. the one represented by this) is negative and the second is positive (i.e. the f object): for example, in the expression −13.5 + 10.0. On line [86], the first object is made positive. If fValue is less than f.fValue, then fValue is subtracted on line [92], and we are finished, since the result will be positive. Otherwise, as in the previous example, the subtraction 13.5 − 10.0 will take place on line [96], resulting in 3.5; its sign will be changed on line [99] to provide the final result, −3.5. But we need to avoid assigning a minus sign to a zero value, as checked on line [98]. This is one of the peculiarities of the SM representation.

# Listing 7.5  Definition of the add and assign operator += (in *CppBookCode, FxFor.h*).

```
```cpp
template< typename ST, int Prec, typename ACC_TYPE >
typename constexpr FxFor< ST, Prec, ACC_TYPE >::FxType &
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
```
```