of elements to be stored in the array. The square brackets indicate that the variable is an array. Similarly in the second example, book is a character array with a size of 102 elements. In the third example, extern is used before the data type float to indicate that the array amount is a global array variable.

# Properties of an array

+   - The type of an array is the data type of its elements.
+   - The location of an array is the location of its first element.
+   - The length of an array is the number of data elements in the array.
+   - The size of the array is the length of the array times the size of the elements, but the size of the array is usually referred as the product of subscripts used.

# Important points to be noted while using arrays

+   - An array name should be a valid C identifier.
+   - The name of the array should be unique, similar to other variables.
+   - The values of the elements stored in the array should be of the same type (i.e., if an array is declared as int, it can store elements that are only int).

# 1.12.2 Accessing Array Elements

Once an array is declared, let us see how individual elements in the array are accessed. This is done with the help of subscripts (i.e., the number specified in the brackets following the array name). The subscript specifies the element's position in the array. All the array elements are numbered, starting from zero. The first item is stored at the address pointed by the array name itself. This can also be referred as position 0. Thus, the first element of the array days is referred as days[0]. The fourth element of the array is referred as days[3]. The ability to use variables as subscripts makes arrays so useful in writing programs. Program 1.15 helps you to understand arrays better.

# Program 1.15 :

```
/* Program to find the biggest of 10 numbers using arrays. */
/* big_10.c */
#include<stdio.h>
void main()
{
    int value[10], i, big = 0;
    printf("Enter any 10 numbers : ");
    for(i = 0 ; i < 10 ; i++)
        scanf("%d", &value[i]);
    big = value[0];
    for(i = 0 ; i < 10 ; i++)
```