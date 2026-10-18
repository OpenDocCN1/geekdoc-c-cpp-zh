constructor on lines [3–4]. It converts from floating-point, represented by the built-in double type, to the FX format, represented by our class. Basically, it follows the scaling property described in Section 7.1.6. But at its beginning on lines [6–10], the sign is stored, and the input floating-point value is made positive. Then, on line [13], the standard value cast is applied. It simply cuts off the fractional part using the standard built-in rounding procedure. This way, the integer part is copied on line [16] to the internal representation fValue, which is immediately shifted to its proper position on line [17].

Now it is time to obtain and convert the fractional part of the input floating-point value x. A fraction is simply the difference of x and the previously computed integer part, as computed on line [19]. This is then scaled on line [21], as guided by Eq. (7.14). This way, the obtained fraction is converted on line [22] to the internal type ST and, on line [24], joined with the fValue by the simple logical OR operation. Finally, on line [26–27], we take care of the minus sign.

Interestingly enough, if, for example, minus_sign was initialized not on line [6] but instead in the following lines, then, although the code would compile under normal conditions, the compiler would abort when working on the constexpr.¹ Hence, working with constexpr requires additional care.

```
```cpp
// ============================================================
// The type-converting constructor: float to fixed
template< typename ST, int Prec, typename ACC_TYPE >
constexpr FxFor< ST, Prec, ACC_TYPE >::FxFor( double x ) : fValue( 0 )
{
    bool minus_sign { false };
    if( x < 0.0 )
    {
        minus_sign = true;      // remember the sign
        x = -x;                 // then take the absolute value
    }

    ST int_part = static_cast< ST >( x );   // here we use the standard conversion
                                           // from the double which cuts off the fraction

    fValue = int_part;
    fValue <<= kPrec;          // put integer part into its place

    double fract_part = x - int_part;

    double scaled_fraction = fract_part * static_cast< double >( kIntegerLSB );
    ST fraction = static_cast< ST >( scaled_fraction );

    fValue |= fraction;        // join the two together

    if( minus_sign == true && fValue != 0 )
        MakeNegative();        // finally consider the sign
}
```
```

¹ Checked with the Microsoft Visual 2019 compiler.