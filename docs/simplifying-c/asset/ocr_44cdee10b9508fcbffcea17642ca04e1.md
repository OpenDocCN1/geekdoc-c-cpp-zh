```
return;
}
/* End of function main */
```

**Output:**

+   Enter Values:
Element 1: 45
Element 2: 57
Element 3: 23
Element 4: 45
Element 5: 90
Element 6: 85
Element 7: 34
Element 8: 32
Element 9: 67
Element 10: 45

**Array Elements**

+   Value of element number 1 is 45
Value of element number 2 is 57
Value of element number 3 is 23
Value of element number 4 is 45
Value of element number 5 is 90
Value of element number 6 is 85
Value of element number 7 is 34
Value of element number 8 is 32
Value of element number 9 is 67
Value of element number 10 is 45

In Program 3, we have defined an array of size five. The loop used for reading data iterates 10 times, and so, instead of reading only 5 values, we are able to read 10 values. The compiler allows us to read 10 values due to the property of contiguous memory in the array. This property of the array may cause problems at times. Let us try to understand how it stores the value at the sixth position of the array.

As mentioned earlier, the name of the array refers to an address of the first element. The compiler calculates the rest of the addresses using the first address as base. The formula to calculate the address of any element is as follows:

> Address of element at index I = Base address of the array + (size of the data type × Index I)

For example, if a float array starts at address 655208 and we need to find the starting address of element in index 3, then the preceding formula can be written as follows:

```
Address of element at index 3 = 655208 + (4 × 3)
= 655208 + 12
= 655220
```

The address can be cross verified with the elements shown in Figure 3. This equation holds for any index. Thus, even when we have defined only five elements in the array, the compiler, using the aforementioned formula, calculates the address of any index and stores a value there.