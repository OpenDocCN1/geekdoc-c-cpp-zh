# 616 Pointers and Dynamic Storage

| value1 | ptrvalue1 | 10000 |
| --- | --- | --- |
| | 10000 | 15000 |
| value2 | ptrvalue2 | 20000 |
| | 20000 | 25000 |
| value3 | ptrvalue3 | 30000 |
| | 30000 | 35000 |
| value4 | ptrvalue4 | 40000 |
| | 40000 | 45000 |

Figure 10.1 Variables and their pointers

of the right data type to the pointer. The following assignments define the pointer variables for the corresponding variables of value1, value2, value3, and value4.

ptrvalue1 = &value1;
ptrvalue2 = &value2;
ptrvalue3 = &value3;
ptrvalue4 = &value4;

The memory locations may be accessed by using the variables value1, value2, value3, and value4 or dereferencing the pointers ptrvalue1, ptrvalue2, ptrvalue3, and ptrvalue4. The following code shows the declaration of the variables and the pointers, the assignment of the memory addresses to the pointers. The assignment of values to variables can be either through variable names or through the pointers.

```
int value1;
int *ptrvalue1;
ptrvalue1 = &value1;
value1 = 458;
*ptrvalue1 = 458;
nor float value2;
float *ptrvalue2;
ptrvalue2 = &value1;
value2 = 645.89;
oror *ptrvalue2 = 645.89;
```