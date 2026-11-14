# EXAMPLE 7.10

Let's repeat the previous example; only now we will use a negative integer. Once again, let myPointer1 be of type pointer to integer and placed at memory location 0x3000. We write:

```
int* myPointer0 = myPointer1 - 4;
```

the code fragment is interpreted as:

```
int* myPointer0 = myPointer1 - 4 * ( sizeof ( int ) );
= 0x3000 - 4*2
= 0x2FF8
```

The variable myPointer1 will now refer to the address 0x2FF8.

Returning to the problem of subtracting pointers, we should now see that the difference between two pointers is computed by the compiler as:

```
pointer_1 - pointer_2 / sizeof (type)
```

Remember that when we write the name of a variable – in this case, a pointer – it is synonymous with writing its value and that value is an address.

The meaning and result of any of the following code fragments should now start to become clear.

```
int* myPtr = anAddress;
myPtr*1;
myPtr++;
myPtr*3;
myPtr -= 1;
--myPtr;
```

Each of the operations algebraically adds a scalar value to a pointer. However, one must be careful when using the auto increment (decrement) operator and know when the pointers are dereferenced. For the auto increment (decrement) operator, prefix placement says to do the arithmetic and then evaluate the pointer variable, while postfix placement says to evaluate the pointer variable and then do the arithmetic.

The code fragments in Figure 7.13 do not all accomplish the same thing, nor do they leave the value of the pointer in the same state. Let’s assume that the value of the pointer starts out at 0x3000, that the value 0x3 is stored at location 0x3000, and that we are working with 16-bit integers.

![](bbox=[0.273, 0.658, 0.867, 0.858])

# Figure 7.13 Precedence with Pointers and Pointer Operations