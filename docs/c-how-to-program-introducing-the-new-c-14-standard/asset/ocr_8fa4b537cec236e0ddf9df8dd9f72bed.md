constant `CONTINUE` has the value 0, `WON` has the value 1 and `LOST` has the value 2. The identifiers in an `enum class` must be *unique*, but separate enumeration constants *can* have the same integer value. Variables of user-defined type `Status` can be assigned only one of the three values declared in the enumeration.

![](bbox=[0.119, 0.348, 0.193, 0.401])

# Good Programming Practice 6.2

*By convention, you should capitalize the first letter of an `enum class`’s name.*

![](bbox=[0.119, 0.575, 0.193, 0.629])

# Good Programming Practice 6.3

*Use only uppercase letters in enumeration constant names. This makes these constants stand out in a program and reminds you that enumeration constants are not variables.*

To reference a scoped `enum` constant, you *must* qualify the constant with the scoped `enum`’s type name (`Status`) and the scope-resolution operator (`::`), as in `Status::CONTINUE`. When the game is won, the program sets variable `gameStatus` to `Status::WON` (lines 25 and 45).