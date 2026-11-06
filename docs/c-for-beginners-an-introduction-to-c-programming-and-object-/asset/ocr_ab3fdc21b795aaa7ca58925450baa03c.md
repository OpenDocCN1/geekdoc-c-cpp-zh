Output:

```
~~~text
C:\>Program Files\...>pointers.exe
C:\>Program Files\...>pointers.exe
At 10 -- Address of a (i.e. ptr1) : 0x28fe80
At 20 -- Address of b (i.e. ptr2) : 0x28fe8c
Value at ptr1 ( 0x28fe80 ) : 10
Value at ptr2 ( 0x28fe8c ) : 20

At 50.5 -- Address of x (i.e. fptr) : 0x28fe40
At 150.75 -- Address of y (i.e. fptr) : 0x28fe4c
Value at fptr ( 0x28fe40 ) : 50.5
Assigning address of y to fptr
At 150.75 -- Address of y (i.e. fptr) : 0x28fe4c
Value at fptr ( 0x28fe4c ) : 150.75
Changing the value of y using fptr
At 675.123 -- Address of y (i.e. fptr) : 0x28fe4c
Value at fptr ( 0x28fe4c ) : 675.123
Press any key to continue...
~~~
```

Addresses displayed here are hexadecimal values.

# Important points regarding pointers:

+   1. It is not possible to add, subtract, divide, multiply or perform any other arithmetic operation on two or more pointers.
+   2. It is possible to increment or decrement pointers but the value will be increased or decreased not by one but by the size of the given data type. For example, an integer occupies 4 bytes — incrementing or decrementing an integer pointer will have its value increased or decreased by 4. That is, the pointer will now point either to the next memory region (4 bytes forward in case of increment) or to the previous memory region (4 bytes backward in case of decrement).