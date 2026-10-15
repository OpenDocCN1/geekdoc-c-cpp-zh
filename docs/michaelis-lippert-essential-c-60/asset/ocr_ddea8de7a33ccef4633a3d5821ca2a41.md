# OUTPUT 3.6

```
4.2 != 4.200000047683716
4.2 != 4.200000047683716
(float)4.2M != 4.2F
4.200000047683716 != 4.20000028610229
4.200000047683716 != 4.2
4.2F != 4.2D
4.19999980926514 != 4.2
4.2F != 4.2D
```

The Assert() methods alert the developer whenever arguments evaluate to false. However, of all the comparisons in this code listing, none of them are in fact equal. In spite of the apparent equality of the values in the code listing, they are not actually equivalent due to the inaccuracies associated with float values.

# Guidelines

AVOID using equality conditionals with binary floating-point types. Either subtract the two values and see if their difference is less than a tolerance, or use the decimal type.

You should be aware of some additional unique floating-point characteristics as well. For instance, you would expect that dividing an integer by zero would result in an error—and it does with data types such as int and decimal. The float and double types, however, allow for certain special values. Consider Listing 3.8, and its resultant output, Output 3.7.

# LISTING 3.8: Dividing a Float by Zero, Displaying NaN

```
float n=0f;
// Displays: NaN
System.Console.WriteLine(n / 0);
```

# OUTPUT 3.7

```
NaN
```