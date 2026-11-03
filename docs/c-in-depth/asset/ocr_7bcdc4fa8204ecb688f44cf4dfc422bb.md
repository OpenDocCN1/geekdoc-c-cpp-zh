After this statement owners will get all permissions, group will get read and execute permission, and others will get only read permission.

To grant execute permission to others we can write-

```
permission = permission | E_OTHERS;  /*Switch on 11th bit*/
```

To take away read permission from group we can write-

```
permission = permission & ~R_GROUP;  /*Switch off 4th bit*/
```

# 13.10 Bit Fields

We have seen how to access and manipulate individual bits or group of bits using bitwise operators. Bit fields provide an alternative method of accessing bits. A bit field is a collection of adjacent bits is defined inside a structure but is different from other members because its size is specified in terms of bits. The data type of a bit field can be int, signed int or unsigned int.

Let us take an example that shows the syntax of defining bit fields.

```
struct tag {
    unsigned a:2;
    unsigned b:5;
    unsigned c:1;
    unsigned d:3;
};
```

Here the structure has four bit fields a, b, c and d. The sizes of a, b, c and d are 2, 5, 1 and 3 respectively. The bit fields can be accessed like other members of the structure using the dot operator. Whenever they appear inside expressions, they are treated like integers(of smaller range). The following are some valid expressions using bit fields.

```
struct tag var;
var.a=2;
printf("%d",var.b);
x=var.a+var.b;
if(var.c==1)
    printf("Flag is on\n");
```

If the size of a bit field is n, then the range of values that the bit field can take is from 0

| Bit field | Size in bits | Range of values |
|---|---|---|
| a | 2 | 0 to 2^2-1 (0 to 3) |
| b | 5 | 0 to 2^5-1 (0 to 31) |
| c | 1 | 0 to 2^1-1 (0 and 1) |
| d | 3 | 0 to 2^3-1 (0 to 7) |

It would be invalid to assign any value to a bitfield outside its range, for example-

```
var.b = 54;  /*Invalid*/
```

We can't apply sizeof and address operators to bit fields. So we can't use scanf to input in a bit field.

```
scanf("%d", &var.a);  /*Invalid*/
```