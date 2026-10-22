# Module 4

# Structures and file management

# The type definition

The typedef is a keyword that allows the programmer to create a new datatype name for an already existing data type. i.e it redefines the name of an existing data type.

Syntax:

```
typedef datatype new_name1,new_name2,.................,new_name n;
```

```
ex: typedef int MARKS,ID_NUMBER;
```

here MARKS & ID_NUMBER are called user defined data types.

Using these types we can decalre variables..

```
MARKS sub1,sub2,sub3;
```

The typedef definitions can be placed :

+   - Prior to the prototype of any function
+   - At the beginning of the program before declaring other variables.

Advantage:

+   - Provides a meaningful way of declaring the variables
+   - Increases the readability of the program
+   - Complex and lengthy declaration can be reduced to short and meaningful declaration
+   - Helps us to understand the source code

Note: The user-defined data type will be in upper case

Example program:

To compute Simple interest

```
#include<stdio.h>
typedef float
AMOUNT; typedef
float TIME; typedef
float RATE; void main()
{
    AMOUNT p,si;
    TIME t;
    RATE r;
    printf("Enter p,t,r\n");
    scanf("%%f%%f%%f",&p,&t,&r);
```