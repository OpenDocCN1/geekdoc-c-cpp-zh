Notice that 5000 is the memory location (address) of the variable var1 and 6000 is the memory location (address) of the pointer variable ptrvar1. Executing the assignment places places the address of var1 in the storage of ptrvar1.

Now the value for the variable var1 may be accessed by the variable name var1 or through the pointer variable ptrvar1. To access the value of var1 through the pointer ptrvar1 a dereference operator (*) must be used. The following code shows the use of the dereference operator.

Before

address

| var1 | address |
| 5000 | 460.58 |

*ptrvar1 = 723.14;

After

address

| var1 | address |
| 5000 | 723.14 |

```
ptrvar1 = &var1;
*ptrvar1 = 723.14;
is is equivalent to
var1 = 723.14;
```

Similarly the assignment statement *ptrvar1 = *ptrvar1 + 200; *ptrvar1 on the right of the assignment accesses the value of 723.14 from the storage of the variable var1 and then adds 200 and stores the altered value 923.14 in var1 using the pointer dereference.

Before

address

| var1 | address |
| 5000 | 723.14 |

*ptrvar1 = 200 + *ptrvar1;