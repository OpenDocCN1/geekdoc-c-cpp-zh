
A program to update an item is shown in Fig. 12.6. The function **update** receives a copy of the structure variable **item** as one of its parameters. Note that both the function **update** and the formal parameter **product** are declared as type **struct stores**. It is done so because the function uses the parameter **product** to receive the structure variable **item** and also to return the updated values of **item**. The function **mul** is of type **float** because it returns the product of **price** and **quantity**. However, the parameter **stock**, which receives the structure variable **item** is declared as type **struct stores**. The entire structure returned by **update** can be copied into a structure of identical type. The statement

**item = update(item,p_increment,q_increment);**

replaces the old values of **item** by the new ones.

```
Program
/***************************************************************/
/*               STRUCTURE AS FUNCTION PARAMETERS              */
/*             Passing a copy of the entire structure          */
/***************************************************************/
struct stores
{
    char name[20];
    float price;
    int quantity;
};
main()
{
    struct stores update();
    float mul(), p_increment, value;
    int q_increment;
    static struct stores item = {"XYZ", 25.75, 12};
    printf("\nInput increment values:");
    printf("\nprice increment and quantity increment\n");
    scanf("%f%d", &p_increment, &q_increment);
    /*------------------------------------------------------------*/
    item = update(item,p_increment,q_increment);
    /*------------------------------------------------------------*/
    printf("\nUpdate values of item\n");
    printf("Name      :%s\n",item.name);
    printf("Price     :%f\n",item.price);
    printf("Quantity  :%d\n",item.quantity);
    /*------------------------------------------------------------*/
    value = mul(item);
    /*------------------------------------------------------------*/
    printf("\nValue of the item = %f\n", value);
}
struct stores update(product, p, q)
struct stores product;
float p;
int q;
{
    product.price += p;
    product.quantity += q;
    return(product);
}
```

```
float mul(stock)
struct stores stock;
{
return(stock.price * stock.quantity);
}

Output
Input increment values:  price increment and quantity increment
10 12
Update values of item
Name : XYZ
Price : 35.750000
Quantity : 24
Value of the item = 858.000000
```

Fig. 12.6 Using structure as a function parameter

You may notice that the template of stores is defined before main(). This has made the data type struct stores as global and has enabled the functions update and mul to make use of this definition.

## 12.10 UNIONS

Unions are a concept borrowed from structures and therefore follow the same syntax as structures. However, there is major distinction between them in terms of storage. In structures, each member has its own storage location, whereas all the members of a union use the same location. This implies that, although a union may contain many members of different types, it can handle only one member at a time. Like structures, a union can be declared using the keyword union as follows:

```
union item
{
    int m;
    float x;
    char c;
} code;
```

This declares a variable code of type union item. The union contains three members, each with a different data type. However, we can use only one of them at a time. This is due to the fact that only one location is allocated for a union variable, irrespective of its size.

![](img/65953ea584e494f3d396b2252cb5ea53_347_0.png)

Fig. 12.7 Sharing of a storage location by union members

The compiler allocates a piece of storage that is large enough to hold the largest variable type in the union. In the declaration above the member x requires 4 bytes which is the largest among the members.

Figure 12.7 shows how all the three variables share the same address. This assumes that a float variable requires 4 bytes of storage.

To access a union member, we can use the same syntax that we use for structure members. That is,

```
code.m
code.x
code.c
```

are all valid member variables. During accessing, we should make sure that we are accessing the member whose value is currently stored. For example, the statements such as

```
code.m = 379;
code.x = 7859.36;
printf("%d", code.m);
```

would produce erroneous output (which is machine dependent).

In effect, a union creates a storage location that can be used by any one of its members at a time. When a different member is assigned a new value, the new value supercedes the previous member's value.

Unions may be used in all places where a structure is allowed. The notation for accessing a union member which is nested inside a structure remains the same as for the nested structures.

## typedef

C provides the typedef keyword that allows you to specify a new name for a data type already provided in the C programming language. In other words, you can use the typedef keyword to specify an identifier for an existing data type. The declaration for the typedef keyword is: typedef data type newname In the above example, data type represents the existing data type for which you want to specify an identifier and newname refers to that identifier. As an example, consider the following declaration: typedef int num; Here, int is the data type available in C and a new identifier num has been specified for this data type. The following code shows an example for using the typedef keyword:

```
#include <stdio.h>
#include <conio.h>
int main(void)
{
typedef int num;
num a, b, add;
a=10;
b=20;
add=0;
add = a+b;
clrscr();
printf("The sum of %d and %d is: %d",a,b,add);
getch();
return 0;
}
```

In the above code, the typedef keyword is used to specify a new name for the int data type. The output of the above code is:

The sum of 10 and 20 is: 30

## 12.11 SIZE OF STRUCTURES

We normally use structures, unions, and arrays to create variables of large sizes. The actual size of these variables in terms of bytes may change from machine to machine. We may use the unary operator sizeof to tell us the size of a structure (or any variable). The expression `sizeof(struct x)` will evaluate the number of bytes required to hold all the members of the structure x. If y is a simple structure variable of type struct x, then the expression `sizeof(y)` would also give the same answer. However, if y is an array variable of type struct x, then `sizeof(y)` would give the total number of bytes the array y requires.

This kind of information would be useful to determine the number of records in a database. For example, the expression `sizeof(y)/sizeof(x)` would give the number of elements in the array y.

## 12.12 BIT FIELDS

So far, we have been using integer fields of size 16 bits to store data. There are occasions where data items require much less than 16 bits space. In such cases, we waste memory space. Fortunately, C permits us to use small bit fields to hold data items and thereby to pack several data items in a word of memory. Bit fields allow direct manipulation of string of a string of preselected bits as if it represented an integral quantity.

A bit field is a set of adjacent bits whose size can be from 1 to 16 bits in length. A word can therefore be divided into a number of bit fields. The name and size of bit fields are defined using a structure. The general form of bit field definition is:

```
struct tag-name
{
    data-type name1: bit-length;
    data-type name2: bit-length;
    .....
    .....
    data-type nameN: bit-length;
}
```

The data-type is either int or unsigned int or signed int and the bit-length is the number of bits used for the specified name. Remember that a signed bit field should have at least 2 bits (one bit for sign).

## 12.20 C Programming and Data Structures

Note that the field name follows a colon. The bit-length is decided by the range of value to be stored. The largest value that can be stored is 2^{n-1}, where n is bit-length. The internal representation of bit fields is machine dependent. That is, it depends on the size of int and the ordering of bits. Some machines store bits from left to right and others from right to left. The sketch below illustrates the layout of bit fields, assuming a 16-bit word that is ordered right to left.

![](img/65953ea584e494f3d396b2252cb5ea53_350_0.png)

- 1. The first field always starts with the first bit of the word.
- 2. A bit field cannot overlap integer boundaries. That is, the sum of lengths of all the fields in a structure should not be more than the size of a word. In case, it is more, the overlapping field is automatically forced to the beginning of the next word.
- 3. There can be unnamed fields declared with size. Example:
- Unsigned : bit-length
- Such fields provide padding within the word.
- 4. There can be unused bits in a word.
- 5. We cannot take the address of a bit field variable. This means we cannot use scanf to read values into bit fields. We can neither use pointer to access the bit fields.
- 6. Bit fields cannot be arrayed.
- 7. Bit fields should be assigned values that are within the range of their size. If we try to assign larger values, behaviour would be unpredictable.

Suppose, we want to store and use personal information of employees in compressed form, this can be done as follows:

```
struct personal {
    unsigned sex : 1;
    unsigned age : 7;
    unsigned m_status : 1;
    unsigned children : 3;
} emp;
```

This defines a variable name emp with four fields. The range of values each field could have is as follows:

| Bit field | Bit length | Range of value |
|----------|------------|----------------|
| sex | 1 | 0 or 1 |
| age | 7 | 0 or 127 (2^7 - 1) |
| m_status | 1 | 0 or 1 |
| children | 3 | 0 to 7 (2^3 - 1) |
