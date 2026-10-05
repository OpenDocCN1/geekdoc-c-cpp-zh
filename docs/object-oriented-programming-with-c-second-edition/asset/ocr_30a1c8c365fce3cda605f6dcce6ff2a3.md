# Object-Oriented Programming with C++

Statement: **int * iPtr**;

![](bbox=[0.342, 0.121, 0.657, 0.243])

Four bytes get allocated for **iPtr** containing junk value at
the with addresses from, say, 1265 to 1268.

**Figure 3.2(a)** Memory allocation for an array using iPtr

**Statement:** `iPtr = new int[SIZE]; //SIZE=10`

The new operator allocates memory in the heap to hold ten integer type values [see Figure 3.2(b)]. If the block from the byte with address 5972 to the byte with address 6012 gets allocated, the new operator returns the base address of the block 5972. The value gets stored in iPtr. After this, iPtr is simply dereferenced within the for loop by using the subscript operator. All the elements of the array at whose first element the pointing is accessed. The syntax for using the new operator to create an array is as follows:

![](bbox=[0.342, 0.497, 0.746, 0.823])

**Figure 3.2(b)** Dynamically allocating memory for an array using the new operator

```
<pointer> = new <data_type>[<number_of_elements>];
```

Now, let us make the program interactive to exploit the power of the new operator. The
value that we passed inside the subscript while allocating the memory using the new operatornbe that of a variable. In Listing 3.3, we will first ask the user to enter the size of the array