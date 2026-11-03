# 6.16 POINTERS AND STRUCTURES

however make explicit assignment between incompatible pointer types by using cast operator, as we do with the fundamental types. Example:

```
int x;
char *p;
p = (char *) x;
```

In such cases, we must ensure that all operations that use the pointer p must apply casting properly.

We have an exception. The exception is the void pointer (void *). The void pointer is a generic pointer that can represent any pointer type. All pointer types can be assigned to a void pointer and a void pointer can be assigned to any pointer without casting. A void pointer is created as follows:

```
void *vp;
```

Remember that since a void pointer has no object type, it cannot be de-referenced.

We know that the name of an array stands for the address of its zeroth element. The same thing is true of the names of arrays of structure variables. Suppose product is an array variable of struct type. The name product represents the address of its zeroth element. Consider the following declaration:

```
struct inventory
{
    char name[30];
    int number;
    float price;
} product[2], *ptr;
```

This statement declares product as an array of two elements, each of the type struct inventory and ptr as a pointer to data objects of the type struct inventory. The assignment

```
ptr = product;
```

would assign the address of the zeroth element of product to ptr. That is, the pointer ptr will now point to product[0]. Its members can be accessed using the following notation.

```
ptr -> name
ptr -> number
ptr -> price
```

The symbol -> is called the arrow operator (also known as member selection operator) and is made up of a minus sign and a greater than sign. Note that ptr-> is simply another way of writing product[0]. When the pointer ptr is incremented by one, it is made to point to the next record, i.e., product[1]. The following for statement will print the values of members of all the elements of product array.

```
for(ptr = product; ptr < product+2; ptr++)
    printf ("%s %d %f\n", ptr->name, ptr->number, ptr->price);
```

We could also use the notation

```
(*ptr).number
```

to access the member number. The parentheses around *ptr are necessary because the member operator '.' has a higher precedence than the operator *.