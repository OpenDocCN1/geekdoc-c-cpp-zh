The ParamArray keyword indicates that there can be one or more arguments, but the number is not known ahead of time. The arguments of the Array function are separated by commas, with each argument becoming an element of the array:

```
Sub ArrayFunction()

    Dim vaRates As Variant
    Dim i As Long

    vaRates = Array(0.05, 0.055, 0.06, 0.065, 0.07)

    For i = LBound(vaRates) To UBound(vaRates)
        Debug.Print vaRates(i)
    Next i

End Sub
```

In the preceding example, the vaRates variable is a Variant containing an array with five elements (the five numbers from the Array function). Since the variable is a Variant, you don't specify the size of the array beforehand. The number of arguments in the Array function determines the size. Because of this, the lower and upper bounds are determined by VBA. The default lower bound is zero, and the default upper bound is one less than the number of arguments in the Array function. For vaRates in the preceding example, the bounds would be 0 to 4. The lower bound of an array returned by the Array function is determined by the Option Base directive, if one exists, at the top of the module.

# NOTE

The Array function returns a variant array—a Variant containing an array. You can also declare an array of Variants. An array of Variants is a fixed or dynamic array whose data type is Variant. A variant array and an array of Variants are two different types of arrays.

# The Split function

The Split function converts text into a Variant array. VBA can't know the size of the array the Split function will return, so the variable holding the array must be declared as a Variant. The Split syntax is as follows:

```
Split(string_expression, [delimiter], [limit], [compare])
```

The first argument is the string you want to split into an array. The delimiter argument tells the Split function on which characters to split the string. The limit argument determines how large the resulting array is. Once the array reaches the limit defined, Split stops splitting the string even if more delimiters are present:

```
Sub TheSplitFunction()

    Dim vaWords As Variant
    Dim i As Long
```