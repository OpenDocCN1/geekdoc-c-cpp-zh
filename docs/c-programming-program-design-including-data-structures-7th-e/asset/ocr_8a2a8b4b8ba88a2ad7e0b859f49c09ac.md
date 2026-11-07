**Sample Run:** In this sample run, the user input is shaded.

```
Line 10: Enter the radius: 2.5

Line 13: Radius = 2.50, area = 19.64

Line 14: Address of radiusPtr: 0012FF60
Line 15: Value stored in radiusPtr: 003450A8
Line 16: Value stored in the memory location to which
         radiusPtr is pointing: 2.50
Line 18: After using the delete operator, the value stored in the location
         to which radiusPtr is pointing: -14568159901474629000000000000000
0000000000000000000000000000000000000000000000000000000000000000000000000000
0000000000000000000000000000000000000000000000000000000000000000000000000000
Line 22: Address of radiusPtr: 0012FF60
Line 23: Value stored in radiusPtr: 00345550
Line 24: Value stored in the memory location to which radiusPtr is pointing:
5.38
Line 25: Value stored in lengthPtr: 003450A8
```

For the most part, the preceding program is the same as the program in Example 12-3. However, let us note the following: the statement in Line 9 allocates memory of type `double` and stores the address of the allocated memory in `radiusPtr`. The output of the statement in Line 15 shows that the address of the allocated memory is 003450A8. Next the statement in Line 17 deallocates the memory space to which `radiusPtr` is pointing. The statement in Line 18 outputs the value stored in the memory location to which `radiusPtr` is pointing. As shown by the output of this statement, the value stored is a strange number. This is because after the `delete` operation in Line 17, `radiusPtr` does not point to a valid memory location. Next, the statement in Line 19 declares the pointer variable `lengthPtr`, allocates memory space of type `double`, and stores the address of the allocated memory space in `lengthPtr`. The statement in Line 20 allocates (another) memory space of type `double` and stores the address of the allocated memory space in `radiusPtr`, and the statement in Line 21 stores 5.38 in the allocated memory space. The statements in Lines 22 to 25 output the addresses as shown by the output. (Note that the addresses and the value printed by the statement in Line 18 are machine dependent. When you run this program on your machine, you are likely to get different values.)

# Operations on Pointer Variables

The operations that are allowed on pointer variables are the assignment and relational operations and some limited arithmetic operations. The value of one pointer variable can be assigned to another pointer variable of the same type.

For example, suppose that we have the following statements:

```
int *p, *q;
```