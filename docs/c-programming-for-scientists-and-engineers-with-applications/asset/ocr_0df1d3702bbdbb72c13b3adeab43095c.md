The integer number 5234 stored in the variable value may be accessed using any
of the pointers ptrvalue1, ptrvalue2, or ptrvalue3. The following print state-
ments show the addresses and values of the variables.

```
printf("The address of the variable value: %u \n", &value);
printf("The contents of the variable value: %d \n", value);
printf("The contents of the pointer ptrvalue1: %u \n", &ptrvalue1);
printf("The contents of the pointer ptrvalue1: %u \n", ptrvalue1);
printf("The address of the pointer ptrvalue2: %u \n", &ptrvalue2);
printf("The contents of the pointer ptrvalue2: %u \n", ptrvalue2);
printf("The address of the pointer ptrvalue3: %u \n", &ptrvalue3);
printf("The contents of the pointer ptrvalue3: %u \n", ptrvalue3);
```

The output is as follows:

```
The address of the variable value: 10000
The contents of the variable value: 5234
The address of the pointer ptrvalue1: 20000
The contents of the pointer ptrvalue1: 10000
The address of the pointer ptrvalue2: 30000
The contents of the pointer ptrvalue2: 20000
The address of the pointer ptrvalue3: 40000
The contents of the pointer ptrvalue3: 30000
```

Notice "%u" used in the output control string is the control specification for
of output of unsigned integers.

The contents of the variable value may be accessed using pointers ptrvalue1,
ptrvalue2, and ptrvalue3 as follows:

```
printf("The contents of the variable value: %d \n", value);
printf("The contents of value by pointer ptrvalue1: %d \n", *ptrvalue1);
printf("The contents of value by pointer ptrvalue2: %d \n", **ptrvalue2);
printf("The contents of value by pointer ptrvalue3: %d \n", ***ptrvalue3);
```

The output is as follows:

```
The contents of the variable value: 5234
The contents of value by pointer ptrvalue1: 5234
The contents of value by pointer ptrvalue2: 5234
The contents of value by pointer ptrvalue3: 5234
```

The integer value 5234 printed by using the variable value is by direct access.
value 5234 printed using ptrvalue1 uses one-level indirection. The value 5234