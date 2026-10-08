
## Program 3

```c
/* Program to illustrate the use of real arithmetic */

#include <stdio.h>

/* Beginning of main function */
main()
{
    /* Declare variables */
    float f_base, f_height, f_area;

    /* Accept the value of base and height */
    printf("\n Enter the value of base of triangle: ");
    scanf(" %f", &f_base);

    printf("\n Enter the value of height of triangle: ");
    scanf(" %f", &f_height);

    /* Calculate area of triangle */
    f_area = (f_base * f_height) / 2;

    /* Print Area */
    printf("\nArea of triangle with base %f and height %f is %f \n",
           f_base, f_height, f_area);

    return;
}
/* End of function main */
```

**Output 1:**

```
Enter the value of base of triangle: 10
Enter the value of height of triangle: 15
Area of triangle with base 10.000000 and height 15.000000 is 75.000000
```

**Output 2:**

```
Enter the value of base of triangle: 5
Enter the value of height of triangle: 15
Area of triangle with base 5.000000 and height 15.000000 is 37.500000
```

Program 3 is similar to Program 1, except for the change in the data type of variables. In Program 3, all the variables are declared as *float* type. In both the outputs, we observed that the integer values for base and height have been entered. The compiler has then automatically converted these integer values into float. This can be identified from the line *Area of triangle with base 5.000000 and height 15.000000 is 37.500000* in Output 2, where the value of base is 5.000000 instead of 5 and the value of height is 15.000000 instead of 15. Also observe that the value of area is now 37.500000 instead of 37 as shown in output 2 of Program 1.

The C expressions in most cases consist of operands having different data types, thus giving rise to another type of arithmetic known as mixed mode arithmetic. The next section discusses about mixed mode arithmetic.

## Mixed Mode Arithmetic

As mentioned earlier, due to the possibilities of the operands being of different but compatible type in C language, another type of arithmetic known as the mixed mode arithmetic is available in C language. In this mode of arithmetic, we can use integer as well as float operands within an expression. The output of such an expression will then depend on the data type of the resultant variable. Although an expression such as `f_area = (7.5 * 6)/2` is allowed in C language, it is not directly possible to evaluate it. An expression in C can only be evaluated if all the operands used in it are of the same data type. To make sure that all operands in an expression are of the same type, C language allows automatic conversion of lower range data type to higher range data type. Program 4 gives an example of the mixed mode arithmetic:

### Program 4

```c
/* Program to illustrate the use of mix mode arithmetic */
#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variables */
    int i_base, i_height;
    float f_area;

    /* Accept the value of base and height */
    printf("\n Enter the value of base of triangle: ");
    scanf("%d", &i_base);
    printf("\n Enter the value of height of triangle: ");
    scanf("%d", &i_height);

    /* Calculate area of triangle */
    f_area = (i_base * i_height) / 2.0;

    /* Print Area */
    printf("\nArea of triangle with base %d and height %d is %f\n",
           i_base, i_height, f_area);
    return;
}
/* End of function main */
```

**Output:**

```
Enter the value of base of triangle: 5
Enter the value of height of triangle: 15
Area of triangle with base 5 and height 15 is 37.500000
```

In Program 4, even though the variables `i_base` and `i_height` are integers, the output is still a float value. This happens as C language automatically converts the int data type into a float data type. In the expression `f_area = (i_base * i_height) / 2.0`, we observed that 2.0 has been used as divisor instead of 2. This also affects the output, as using 2 in this expression will convert the right-hand side (RHS) to an integer calculation and we would get the area as 37.000000.

Try Program 4 using value 2 in the expression `f_area = (i_base * i_height) / 2.0`, instead of 2.0, and note the difference. The next section discusses the concept of type conversion used in C language.

## Type Conversion

As mentioned earlier, an expression in C language can be evaluated only if all the operands in the expression are of the same data type. This property for evaluating an expression at times requires the compiler to convert an operand of one data type into another and this is known as internal conversion of data types. This conversion can be performed automatically by the C compiler, or a programmer can ask the compiler to temporarily convert it to the desired data type. The automatic conversion done by the C compiler is known as type conversion, while the conversion in which a programmer asks the compiler to temporarily convert the datatype of an operand is known as type casting. Program 4 uses automatic type conversion. The evaluation of expression `f_area = (i_base * i_height) / 2.0` is shown in Figure 3:

![Figure 3](img/5d422ba7108ffdf64376be51eaf0c459_96_0.png)

▲ Figure 3: Automatic Type Conversion

The expression evaluation in C also follows the Brackets Order Division Multiply Add Subtract (BODMAS) rule. It can be seen in Figure 3 that first the subexpression `i_base * i_height` is evaluated; it will result to an integer value. The next operation is division by 2.0; however, before performing this operation, the compiler converts the result of multiplication into a float value, as shown in Figure 3. Finally, the result is then assigned to the variable `f_area`. The internal conversion (implicit conversion) of data types is performed in the order as shown in Figure 4:

![Figure 4](img/5d422ba7108ffdf64376be51eaf0c459_96_1.png)

▲ Figure 4: Conversion Order of Data Types

Figure 4 shows that C language converts the data type in order of lower space requirement to higher space requirements. The bytes shown in the figure may vary from compiler to compiler, but the order will remain the same.

A programmer can explicitly convert the data type of any variable used in the expression by using a process called type casting. When type casting is applied to an operand, it overrides the internal conversion performed by the compiler. To type cast a variable used in the expression, we prefix the variable with the data type that we want it to be converted to. The syntax of the type cast is as follows:

`(data type) identifier` or `(data type) constant`

Program 5 illustrates the use of type casting:

### Program 5

```c
/* Program to illustrate the use of type cast */
#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variables */
    int i_base, i_height;
    float f_area;

    /* Accept the value of base and height */
    printf("\n Enter the value of base of triangle: ");
    scanf("%d", &i_base);
    printf("\n Enter the value of height of triangle: ");
    scanf("%d", &i_height);

    /* Calculate area of triangle */
    f_area = ((float) i_base * (float) i_height) / 2.0;

    /* Print Area */
    printf("\nArea of triangle with base %d and height %d is %f\n",
           i_base, i_height, f_area);
    return;
}
/* End of function main */
```

**Output:**

```
Enter the value of base of triangle: 5
Enter the value of height of triangle: 15
Area of triangle with base 5 and height 15 is 37.500000
```

Program 5 is similar to Program 4, with only the change in the expression `f_area = ((float) i_base * (float) i_height)/2.0;` where the variables `i_base` and `i_height` are prefixed with data type float. Thus, the variables `i_base` and `i_height` are converted to float data type temporarily. Here, the actual values stored in both the variables are integers; however, for the purpose of evaluating the expression, it is considered as float.

The programmers need to take caution when writing expressions in C language. The expression at times may not give desired results due to different type of arithmetic operations supported by C language. After looking at the arithmetic operators available with C language, let us now discuss about assignment operator.

## Assignment Operators

The special symbol `=` is known as an assignment operator in C language. In normal mathematics, it is used to check the equality of two operands. In C language, it is used to assign a result of an expression or constant value to a variable. The following shows examples of assignment statements:
