```
// multiply each element of an array by 2
public static void modifyArray( int[] array2 )
{
    for ( int counter = 0; counter < array2.length; counter++ )
        array2[ counter ] *= 2;
} // end method modifyArray
```

```
// multiply argument by 2
public static void modifyElement( int element )
{
    element *= 2;
    System.out.printf(
        "Value of element in modifyElement: %d\n", element );
} // end method modifyElement
```

} // end class PassArray

Effects of passing reference to entire array:
The values of the original array are:
  1  2  3  4  5

The values of the modified array are:
  2  4  6  8  10

Effects of passing array element value:
array[3] before modifyElement: 8
Value of element in modifyElement: 16
array[3] after modifyElement: 8

Fig. 7.13 | Passing arrays and individual array elements to methods. (Part 2 of 2.)

The enhanced for statement at lines 16–17 outputs the five int elements of array. Line 19 invokes method modifyArray, passing array as an argument. Method modifyArray (lines 36–40) receives a copy of array’s reference and uses the reference to multiply each of array’s elements by 2. To prove that array’s elements were modified, lines 23–24 output the five elements of array again. As the output shows, method modifyArray doubled the value of each element. We could not use the enhanced for statement in lines 38–39 because we’re modifying the array’s elements.

Figure 7.13 next demonstrates that when a copy of an individual primitive-type array element is passed to a method, modifying the copy in the called method does not affect the original value of that element in the calling method’s array. Lines 26–28 output the value of array[3] before invoking method modifyElement. Remember that the value of this element is now 8 after it was modified in the call to modifyArray. Line 30 calls method modifyElement and passes array[3] as an argument. Remember that array[3] is actually one int value (8) in array. Therefore, the program passes a copy of the value of array[3]. Method modifyElement (lines 43–48) multiplies the value received as an argument by 2, stores the result in its parameter element, then outputs the value of element (16). Since method parameters, like local variables, cease to exist when the method in which they’re declared completes execution, the method parameter element is destroyed when method modifyElement terminates. When the program returns control to main, lines 31–32 output the unmodified value of array[3] (i.e., 8).