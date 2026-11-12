# 2.4 Recursion with Arrays

When you are working with an array, recursion can be a practical and powerful tool. For our first example, we write the contents of an array backward. We then look at several problems that involve searching an array.

# 2.4.1 Writing an Array's Entries in Backward Order

The solution to this problem is much like our first solution in Section 2.3.1 when we wrote a string backward. We can write the following pseudocode:

```
writeArrayBackward(anArray: char [])
    if (the array is empty)
        Do nothing—this is the base case
    else
    {
        Write the last character in anArray
        writeArrayBackward(anArray minus its last character)
    }
```

How will we pass anArray minus its last character to writeArrayBackward? We could pass the number of characters left in the array. At each recursive call, we would decrease this number by 1. Alternatively, we could pass the index of the last character. That is, if last is this index, writeArrayBackward would act on the array anArray[0..last], that is, the portion anArray[0] through anArray[last]. The recursive call would then act on the subarray anArray[0..last - 1]. A more general variation of this idea also passes the index of the first array character. So instead of assuming that this index is 0, we would pass anArray[first..last] to writeArrayBackward.

We can write the function writeArrayBackward as follows:

```
/** Writes the characters in an array backward.
 * @pre  The array anArray contains size characters, where size >= 0.
 * @post None.
 * @param anArray  The array to write backward.
 * @param first    The index of the first character in the array.
 * @param last     The index of the last character in the array. */
void writeArrayBackward(const char anArray[], int first, int last)
{
    if (first <= last)
    {
        // Write the last character
        cout << anArray[last];
        // Write the rest of the array backward
        writeArrayBackward(anArray, first, last - 1);
    } // end if
    // first > last is the base case - do nothing
} // end writeArrayBackward
```