another in the computer’s memory. This ensures that there is minimal travel and retrieval time from one value to the next in the computer’s memory. It also enables us to perform operations that we wouldn’t normally, like working through the pieces of data in memory in a procedural way as we’ll talk about here in a bit.

Arrays essentially set up a contiguous or connected, areas of memory that is the size of n elements of the array times the s size of a data type. So, if a data type takes up 4 bytes of memory, and the array has four elements, it clears out and allocates 16 bytes worth of memory right next to each other.

These can then be assigned values individually according to the data type of the array. So, if you created an integer array, you could assign integers to the elements in that array.

You can declare an array like so:

```
    dataType arrayName[size];
```

You can also populate it (or partially populate it, at least) by including values in brackets after your declaration of the array.

```
    int myArray[3] = {0, 2, 7};
```

The indices of an array start counting at 0. You refer to a given element of an array by referring to its index. So, if you wanted to refer to the second element of an array, you’d do it like so:

```
    myArray[1];
```

```
    // this would be 2, since 2 is the element at index 1, which is position 2, within
    the array.
```

You can see that arrays are actually relatively easy to understand, but they’re nonetheless a fundamental concept for you to work with and try to ingrain as much as possible if you want to be a good Arduino programmer. You’re going to inevitably come upon this concept quite a bit in your time programming Arduino sketches, so you need to know it.

# # Truth and Logic