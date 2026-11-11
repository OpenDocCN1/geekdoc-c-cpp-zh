![](bbox=[0.249, 0.119, 0.743, 0.362])

**Figure 8.20:** Memory allocation of array a

![](bbox=[0.179, 0.417, 0.744, 0.659])

**Figure 8.21:** Pointer p points to the first location in the array

The statement p=&a[0]; stores the address of the first element of the array inside the pointer, hence the pointer p now contains 1000. This is as shown in the Figure 8.21.

Figure 8.22, describes the results of some expressions based on the Figure 8.21. Let us take an example of an expression *(p+1). In this case, p+1 is surrounded in parenthesis, hence the expression first adds a constant 1 to the address contained in p and then applies indirection operator on the resultant address. The address contained in p is 1000 and because the pointer is of type integer 1000+ 1 is evaluated as 1002. Now we apply indirection operation and fetch the value at memory location 1002 which gives 20 as seen in the Figure 8.21. (Applying indirection operator on memory address 1002 will read 2 consecutive bytes in memory stored at addresses 1002 and 1003, this is because every integer is 2 bytes). Hence, the expression returns a value 20 which is the value of a[1].