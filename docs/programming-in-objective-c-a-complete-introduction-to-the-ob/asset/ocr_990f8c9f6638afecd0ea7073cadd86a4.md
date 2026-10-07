# Pointers 281

When you define a pointer that will be used to point to the elements of an array, you don't designate the pointer as type "pointer to array"; instead, you designate the pointer as pointing to the type of element contained in the array.

If you had an array of Fraction objects called fracts, you could similarly define a pointer to be used to points in fracts with the following statement:

```
Fraction **fractPtr;
```

Note that this is the same declaration used to define a Fraction object.
to set valuesPtr to point to the first element in the values array, you simply write this:

```
valuesPtr = values;
```

The address operator is not used in this case because the Objective-C compiler treats the occurrence of an array name without a subscript as a pointer to the first element of the array.Therefore, simply specifying values without a subscript produces a pointer to the first element of values.

An equivalent way of producing a pointer to the first element of values is to apply the address operator to the first element of the array.Thus, the statement

```
valuesPtr = &values[0];
```

serves the purpose of placing a pointer to the first element of values in the pointer variable valuesPtr.
to display the Fraction object in the array fracts fracts fractPtr points to, you would write this statement:

```
*fractPtr print;
```

The real power of using pointers to arrays comes into play when you want to sequence through the elements of an array.If valuesPtr is defined as mentioned previously and is setting to the first element of values, you can use the expression

```
*valuesPtr
```

to access the first integer of the values array—that is, values[0].To reference values[3] through the valuesPtr variable, you can add 3 to valuesPtr and then apply the redirection operator:

```
*(valuesPtr + 3)
```

In general, you can use the expression

```
\(valuesPtr + i)
```

to access the value contained in values[10].

To set values[10] to 27, you would write the following expression:

```
values[10] = 27;
```

Or, using valuesPtr, you would write this:

```
*(valuesPtr + 10) = 27;
```