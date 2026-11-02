One could allow the full range of Natural in this case by rewriting the
precondition as

```
```ada
Pre => Number'Length mod 2 = 0 and
       Number'Length / 2 = Result.Length
```
```

The first condition ensures that the length of the given string is even. Such rewritings are commonly possible, but they can be obscure. It is often easier and better to just constrain the types involved to “reasonable” ranges.

Before leaving Make_From_Hex_String, we point out that the flow dependency contract uses Result as input:

```
```ada
Depends => ((Result, Valid) => (Number, Result))
```
```

This might seem surprising given that Result is an **out** parameter. However, similar to the bounds on parameters of unconstrained array types, the actual parameter used in the call has a specific value of the discriminant set by the caller. The value written to, for example, Result depends on this discriminant. If Result's length is large, the value written to it will be different than if Result's length is small. Thus the dependency as shown is correct.

Returning now to the listing of Very_Long’s specification, lines 24–34 declare several relational operators. Private types can already be compared for equality, but it is natural to also have the other relational operators for a numeric type such as Very_Long. Notice that the preconditions require that both numbers being compared be the same size. Although it is mathematically logical to compare numbers with different sizes, the expected application domain (cryptography) does not normally require that. Furthermore, the restriction simplifies the implementation. Notice here that the precondition is being used to describe a relationship between the parameters; something Ada’s type system cannot do by itself.

Line 37 declares a convenience function Is_Zero to test if a Very_Long is zero. This function was originally motivated for use in later assertions, but it also has usefulness to clients of the package.

Line 40 declares another convenience function Number_Of_Digits that returns the number of significant digits in a Very_Long. This is different than the Very_Long’s length as leading zeros are not significant. In fact, if all the digits of the Very_Long are zero, then the Number_Of_Digits returns zero.

Lines 43–62 declare three arithmetic operators for Very_Long. Unlike the case with the relational operators, most of these functions are given names rather than overloaded operator symbols. This is because they do modular calculations in which the resulting carry is ignored without error. It is best to reserve the operator symbols for functions that follow the usual mathematical