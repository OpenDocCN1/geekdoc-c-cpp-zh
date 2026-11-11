```
```cpp
printf("%u",*q);
```
```

This statement applies an indirection operator (*) to a pointer q. The operator (*) directs the CPU to access the memory location using the address contained in the pointer and fetch the value stored in that location. Because pointer q contains the address 2000, the CPU will access the contents of memory location 2000, which is obviously the value of pointer p as shown in Figure 8.38. As the value of pointer p is the address of variable a, the statement `printf("%u",*q);` prints 1000 on the computer screen.

```
```cpp
printf("%d",**q);
```
```

This statement applies a ‘double indirection’ on pointer q. Hence the statement prints the value of the memory location whose address is contained in a ‘target pointer’ which is ‘pointed’ by the pointer q. The pointer q points to pointer p and pointer p points to variable a, hence **q will give the value of variable a which is 10. Therefore the statement prints the value 10 on the computer screen.

# 8.11  Pointers and 2D Arrays

We understand from Chapter 7 that a 2-D array is organized as a matrix of r-rows and c-columns. This section explains the procedure adopted by C/C++ in order to represent a 2-D matrix in computer memory.

Compiler internally creates a 1-D ‘array of pointers’ with a size same as that of number of rows specified while creating a 2-D array. Every pointer present in this array points to one row of the 2-D matrix in memory.

There also exists a pointer that points to the ‘array of pointers’. This will naturally be a ‘pointer to a pointer’ because it points to the ‘array of pointers’. The ‘pointer to pointer’ will have a same name as that of the name of a 2-D array.

As an example, let us understand the creation of an integer type 2-D array with 3 rows and 4 columns as shown below:

```
```cpp
int a[3][4]={10,20,30,40,
             50,60,70,80,
             90,100,110,120
             };
```
```

We understand from Chapter 7 that this array is organized as a matrix shown in the Figure 8.39.

To create such a matrix in the computer memory compiler internally creates a 1-D array of pointers with a size three (because the array has a three rows in it). The array of pointers created by the compiler is as shown in the Figure 8.40, where each element of the array points to one of the rows of the matrix. Also there is a ‘pointer to pointer’ that points to this array of pointers as shown. The name ‘pointer to pointer’ is a (same as the name given to the 2-D array). Figure 8.40 assumes that the starting address of an ‘array of pointers’ is 1000 (which is contained in 2-D pointer a). Considering that every pointer in the array is of 2 bytes the addresses of subsequent elements in the array can be derived as shown in Figure 8.40.