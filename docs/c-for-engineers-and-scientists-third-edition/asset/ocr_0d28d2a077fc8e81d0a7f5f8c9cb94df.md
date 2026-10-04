# Chapter 12

# 695

Passing Addresses

```
swap(&firstnum, &secnum);\      // call swap
cout << "The value stored in firstnum is now: "
<< firstnum << endl;
cout << "The value stored in secnum is now: "
<< secnum << endl;

return 0;

// this function swaps the values in its two arguments
void swap(double *nm1Addr, double *nm2Addr)
{
double temp;

temp = *nm1Addr; // save firstnum's value
*nm1Addr = *nm2Addr; // move secnum's value into firstnum
*nm2Addr = temp; // change secnum's value

return;
}
```

A sample run of Program 12.11 produced this output:

The value stored in firstnum is: 20.5
The value stored in secnum is: 6.25

The value stored in firstnum is: 6.25
The value stored in secnum is: 20.5

As this output shows, the values stored in main() variables have been modified in swap(), which was made possible using pointers. To make sure you understand, could compare this version of swap() with the version using references in Program 6.10. The advantage of using pointers rather than references is that the function specifies that addresses are being used, which is an alert that will likely affect other variables of the calling function. The advantage of using references is that the notation is much simpler. Generally, for functions such as swap(), case of notation winds out, and references are used. In passing arrays to functions, however, which is the next topic, the compiler passes an address automatically, which dictates using pointers to store the address.

# Passing Arrays

When an array is passed to a function, its address is the only item actually passed. “Address” means the address of the first location used to store the array, as shown in Figure 12.22. Because the first location reserved for an array corresponds to element 0 of the array, the “address of the array” is also the address of element 0.