difference is that each of the structure members is identified as belonging to structure variable part.

The following example shows the use of a member operator to assign values to the structure variable members.

```
strcpy(part.part,"bolt");
part.count = 20;
part.unitcost = 0.25;
part.totalcost = part.count * part.unitcost;
```

Notice that in each of these assignment statements the left-hand side consists of members of the structure variable part with a member operator (.). Since name is a character string array, a string cannot be assigned directly to it; instead the string copy function strcpy is used to copy the string "bolt" to the string member-name. The members count, unitcost, and totalcost are numeric; they are assigned numeric values using assignment statements.

The values are stored as follows:

| part.name | part.count | part.unitcost | part.totalcost |
| --- | --- | --- | --- |
| bolt | 20 | 0.25 | 5.00 |
| 10 bytes | 4 bytes | 4 bytes | 4 bytes |

A structure variable may also be initialized at the time it is declared as follows:
struct gadgetpart part1 = {"bolt", 20, .25, 5.0};

Variable Pointer A pointer to a structure variable contains the memory address of the storage allocated to it. The value of the pointer is the address of the first byte of the storage allocated to the structure variable. Structure variables and structure pointers may both be declared following the structure declaration. The following code shows the declaration of structure variables and a structure pointer.

Structure declaration:

```
struct gadgetpart {
    char partname[10];
    int count;
    float unitcost;
    float totalcost;
};
```