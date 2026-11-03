# Pointers 11.23

During the execution of table, the statement
value = (*f)(a);
calls the function y, which is pointed to by f, passing it the parameter a. Thus the function y is evaluated over the range 0.0 to 2.0 at the intervals of 0.5.

Similarly, the call

table (cos, 0.0, PI, 0.5);

passes a pointer to cos as first parameter and therefore, the function table evaluates the value of cos over the range 0.0 to PI at the intervals of 0.5.

# 11.11 POINTERS AND STRUCTURES

We know that the name of an array stands for the address of its zeroth element. The same thing is true of the names of arrays of structure variables. Suppose product is an array variable of struct type. The name product represents the address of its zeroth element. Consider the following declaration:

```
struct inventory {
 char name[30];
 int number;
 float price;
} product[2], *ptr;
```

This statement declares product as an array of two elements, each of the type struct inventory and ptr as a pointer to data objects of the type struct inventory.

The assignment ptr = product; would assign the address of the zeroth element of product to ptr. That is, the pointer ptr will now point to product[0]. Its members can be accessed using the following notation.

```
ptr → name
ptr → number
ptr → price
```

The symbol → is called the arrow operator and is made up of a minus sign and a greater than sign. Note that ptr → is simply another way of writing product[0]. When the pointer ptr is incremented by one, it is made to point to the next record, i.e., product[1]. The following for statement will print the values of members of all the elements of product array.

```
for(ptr = product; ptr < product+2; ptr++)
printf("%s %d %f\n",ptr→ name,ptr→ number,ptr→ price);
```

We could also use the notation (*ptr).number to access the member number. The parentheses around *ptr are necessary because the member operator "." has a higher precedence than the operator "*".