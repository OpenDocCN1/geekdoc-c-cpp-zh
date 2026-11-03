
## UNIT II

## Chapter 8

### Arrays

### 8.1 INTRODUCTION

An array is a group of related data items that share a common name. For instance, we can define an array name `salary` to represent a set of salaries of a group of employees. A particular value is indicated by writing a number called index number or subscript in brackets after the array name. For example, `salary[10]` represents the salary of the 10th employee. While the complete set of values is referred to as an array, the individual values are called elements. Arrays can be of any variable type.

The ability to use a single name to represent a collection of items and to refer to an item by specifying the item number enables us to develop concise and efficient programs. For example, a loop with the subscript as the control variable can be used to read the entire array, perform calculations and print out the results. In this chapter, we shall discuss how arrays can be defined and used in C.

### 8.2 ONE-DIMENSIONAL ARRAYS

A list of items can be given one variable name using only one subscript and such a variable is called a single-subscripted variable or a one-dimensional array. In mathematics, we often deal with variables that are single-subscripted. For instance, we use the equation.

A = Σ_{i=1}^{n} x_i / n

to calculate the average of n values of x.

### Accessing and Storing Elements

The subscripted variable x_i refers to the i th element of x. In C, single-subscripted variable x_i can be expressed as

```
x[1], x[2], x[3] ........x[n]
```

The subscript can begin with number 0. That is

```
x[0]
```

is allowed. For example, if we want to represent a set of five numbers, say (35, 40, 20, 57, 19), by an array variable `number`, then we may declare the variable `number` as follows:

```
int number[5];
```

and the computer reserves five storage locations as shown below:

![](img/65953ea584e494f3d396b2252cb5ea53_200_0.png)

The values of the array elements can be assigned as follows:

```
number[0] = 35;
number[1] = 40;
number[2] = 20;
number[3] = 57;
number[4] = 19;
```

This would cause the array `number` to store the values as shown below:

| Array element | Value |
| --- | --- |
| number[0] | 35 |
| number[1] | 40 |
| number[2] | 20 |
| number[3] | 57 |
| number[4] | 19 |

These elements may be used in programs just like any other C variable. For example, the following are valid statements:

```
a = number[0] + 10;
number[4] = number[0] + number[2];
number[2] = x[5] + y[0];
value[6] = number[i] * 3;
```

The subscript of an array can be integer constants, integer variables like i, or expressions that yield integers. C performs no bounds checking and, therefore, care should be exercised to ensure that the array indices are within the declared limits.

### Declaration of Arrays

Like any other variable, arrays must be declared before they are used. The general form of array declaration is

```
type variable-name[size];
```

The type specifies the type of element that will be contained in the array, such as `int`, `float`, or `char`, and the size indicates the maximum number of elements that can be stored inside the array. For example,

```
float height[50];
```

declares the `height` to be an array containing 50 real elements. Any subscripts 0 to 49 are valid. Similarly,

```
int group[10];
```

declares the `group` as an array to contain a maximum of 10 integer constants. Remember, any reference to the arrays outside the declared limits would not necessarily cause an error. Rather, it might result in unpredictable program results.

The C language treats character strings simply as arrays of characters. The size in a character string represents the maximum number of characters that the string can hold. For instance,

```
char name[10];
```

declares the `name` as a character array (string) variable that can hold a maximum of 10 characters. Suppose we read the following string constant into the string variable `name`.

"WELL DONE"

Each character of the string is treated as an element of the array `name` and is stored in the memory as follows:

| Character stored |
| --- |
| 'W' |
| 'E' |
| 'L' |
| 'L' |
| ' ' |
| 'D' |
| 'O' |
| 'N' |
| 'E' |
| '\0' |

When the compiler sees a character string, it terminates it with an additional null character. Thus, the element `name[9]` holds the null character `'\0'` at the end. When declaring character arrays, we must always allow one extra element space for the null terminator.

### Example 8.1

Write a program using a single-subscripted variable to evaluate the following expressions:

Total = Σᵢ₌₁¹⁰ xᵢ²

The values of x₁, x₂, .... are read from the terminal.

Program in Fig. 8.1 uses a one-dimensional array x to read the values and compute the sum of their squares.

```
Program
/***************************************************************/
/*              PROGRAM SHOWING ONE-DIMENSIONAL ARRAY          */
/**************************************************************/
main()
{
    int i;
    float x[10], value, total;
    /* .................... READING VALUES INTO ARRAY .................... */
    printf("ENTER 10 REAL NUMBERS\n");
    for(i = 0; i < 10; i++)
    {
        scanf("%f", &value);
        x[i] = value;
    }
    /* .................... COMPUTATION OF TOTAL .................... */
    total = 0.0;
    for(i = 0; i < 10; i++)
        total = total + x[i] * x[i];
    /* .................... PRINTING OF x[i] VALUES AND TOTAL .......... */
    printf("\n");
    for(i = 0; i < 10; i++)
        printf("x[%2d] = %5.2f\n",i+1, x[i]);
    printf("\nTotal = %.2f\n", total);
}
Output
ENTER 10 REAL NUMBERS
1.1 2.2 3.3 4.4 5.5 6.6 7.7 8.8 9.9 10.10
x[1]  = 1.10
x[2]  = 2.20
x[3]  = 3.30
x[4]  = 4.40
x[5]  = 5.50
x[6]  = 6.60
x[7]  = 7.70
x[8]  = 8.80
x[9]  = 9.90
x[10] = 10.10
Total = 446.86
```

Fig. 8.1 Program to illustrate one-dimensional array

### Initialization of Arrays

We can initialize the elements of arrays in the same way as the ordinary variables when they are declared. The general form of initialization of arrays is:

```
static type array-name[size] = { list of values };
```

The values in the list are separated by commas. For example, the statement

```
static int number[3] = { 0,0,0 };
```

will declare the variable `number` as an array of size 3 and will assign zero to each element. If the number of values in the list is less than the number of elements, then only that many elements will be initialized. The remaining elements will be set to zero automatically. For instance,

```
static float total[5] = {0.0,15.75, -10};
```

will initialize the first three elements to 0.0, 15.75, and -10.0 and the remaining two elements to zero.

Note that we have used the word `static` before type declaration. This declares the variable as a static variable. More about static and other class of variables are discussed in Chapter 10.

Note: Under the old version (the K & R standard), automatic arrays cannot be initialized. Only external and static arrays may be initialized. However, the ANSI standard permits arrays with auto storage class to be initialized. That is, the keyword `static` could be omitted, when an ANSI compiler is used. Since ANSI compilers accept both the versions, we use the storage class `static` in our programs so that they can run under both the K & R and ANSI compilers.

The size may be omitted. In such cases, the compiler allocates enough space for all initialized elements. For example, the statement

```
static int counter[] = {1,1,1,1};
```

will declare the `counter` array to contain four elements with initial values 1. This approach works fine as long as we initialize every element in the array.

Character arrays may be initialized in a similar manner. Thus, the statement

```
static char name[] = {'J','o','h','n'};
```

declares the `name` to be an array of four characters, initialized with the string "John".

Initialization of arrays in C suffers two drawbacks.

- 1. There is no convenient way to initialize only selected elements.
- 2. There is no shortcut method for initializing a large number of array elements like the one available in FORTRAN.

Consider an array of size, say 100. All the 100 elements have to be explicitly initialized. There is no way to specify a repeat count. In such situations, it would be better to use a for loop to initialize the elements. Consider the following segment of a C program:

```
for (i = 0; i < 100; i = i+1)
{
if (i < 50)
    sum[i] = 0.0;
else
```

7.12 Write a program to read the age of 100 persons and count the number of persons in the age group 50 to 60. Use `for` and `continue` statements.

7.13 Rewrite the program of case study 7.4 (plotting of two curves) using `else ... if` constructs instead of `continue` statements.

7.14 Write a program to print a table of values of the function

y = exp (−x)

for x varying from 0.0 to 10.0 in steps of 0.10. The table should appear as follows:

**Table for Y = EXP(−X)**

| x | 0.1 | 0.2 | 0.3 | ............ | 0.9 |
|---|---|---|---|---|---|
| 0.0 |  |  |  |  |  |
| 1.0 |  |  |  |  |  |
| 2.0 |  |  |  |  |  |
| 3.0 |  |  |  |  |  |
| . |  |  |  |  |  |
| 9.0 |  |  |  |  |  |

7.15 Write a program that will read a positive integer and determine and print its binary equivalent. (Hint: The bits of the binary representation of an integer can be generated by repeatedly dividing the number and the successive quotients by 2 and saving the remainder, which is either 0 or 1, after each division.)
