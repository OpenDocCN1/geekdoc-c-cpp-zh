
## 2.5 First Complete Programs

### Pseudocode

```
Input the values for the sides a, b, and c of the triangle
Output the sides of the triangle a, b, and c
If a > 0 and b > 0 and c > 0
  Compute the value of s from the formula
  s <- (a + b + c)/2
  If(s > a and s > b and s > c)
    Compute the area from the formula
    area <- (s (s - a) (s - c))^1/2
    Output the area of the triangle
  End if
End if
End
```

Note: The tests are necessary to determine whether the three input values are the sides of a triangle.

```
Program
/******************************************************/
/* *
/*  Area of a Scalene Triangle             */
/* *
/******************************************************/
/* *
/*  Input Variables:                    */
/* *
/*  a, b, and c - sides of a scalene triangle */
/* *
/*  Computed Variables:                   */
/* *
/*  s - half the sum of the sides         */
/*  area - area of the scalene triangle     */
/* *
/*  Output Variables:                     */
/* */
```

```
/* area - area of the triangle */
/* */
/****************************************************************/

#include <stdio.h>
#include <math.h>
int main()
{
    int a, b, c;
    float s, area;

    printf("Input integer values for the Sides:\n");
    scanf("%d %d %d", &a, &b, &c);
    printf("\nThe Sides of the Triangle: %d %d %d\n", a, b, c);

    if(a > 0 && b > 0 && c > 0)
    {
        s = (a + b + c) / 2.0;
        if(s > a && b > b && s > c)
        {
            area = sqrt(s * (s - a) * (s - b) * (s - c));
            printf("The Area of the Triangle: %5.2f\n", area);
        }
    }

    return 0;
}
```

### Input and Output

Input integer values for the Sides:
12 14 16

The Sides of the Triangle: 12 14 16
The Area of the Triangle: 81.33

## 2.5.6 Volume of a Sphere

Problem Compute the volume of a sphere of radius $r$.

Data Radius $r$.

Method Given the radius $r$, the volume of the sphere is computed from the formula
$volume = 4/3\pi r^3$.

### Pseudocode
Input the value of $r$
If $r > 0$
Compute the volume

$volume = 4/3\pi r^3$

Output the volume
Stop

Note: The test is necessary to make sure that the radius $r$ is positive.

### Program

```
/****************************************************************/
/*                                */
/*    Volume of a Sphere             */
/*                                */
****************************************************************/
/*                                {}
/*   Defined Constants:                  */
/*                                {}
/*   PI - 3.141593                       */
/*                                {}
/*   Input Variables:                    */
/*                                {}
/*   radius - radius of a sphere        */
```

```
/*
 * Computed Variables:
 */
 * volume - volume of the sphere
 *
 * Output Variables:
 *
 * radius - radius of the sphere
 *
 * volume - volume of the sphere
 *
 *******************************************************************
```

```
#include <stdio.h>
int main ()
{
    const float PI = 3.141593;
    float radius, volume;

    printf("Input a real value for the radius:\n");
    scanf("%f", &radius);

    printf("\nThe radius of sphere is: %6.2f inches\n", radius);
    if(radius > 0)
    {
        volume = 4.0/3.0 * PI * radius * radius * radius;
    }
    printf("The volume of sphere is: %6.2f cubic inches\n", volume);

    return 0;
}
```

### Input and Output

Input a real value for the radius:
4.0

The radius of the sphere is: 4.00 inches
The volume of the sphere is: 268.08 cubic inches

## Chapter Summary

C is a structured, procedural, and strongly typed programming language. C has the capability to manipulate integer and floating-point numeric data. Scientific and engineering computations use integers and floating-point numbers in both single-precision and double-precision. These are available in C. C also has the capability of deriving new data types. In a C program every variable must be declared.

Declaration of integer variables:

```
int var1,var2,.. .varn;
```

In large computer systems the default storage allocated for an integer variable is four bytes. In such systems to allocate two bytes of storage the definition is as follows:

```
short int var1,var2,.. .varn;
or short var1,var2,.. .varn;
```

In personal computer systems the default storage allocated for an integer variable is two bytes. In such systems, to allocate four bytes of storage, the declaration is as follows:

```
long int var1,var2,.. .varn;
or or long var1,var2,.. .varn;
```

Declaration of floating-point variables is:

```
float var1,var2,.. .varn;
```

The storage allocated for floating-point variables and constants is four bytes. Declaration of double-precision variables is:

```
double var1,var2,.. .varn;
```

The storage allocated for double-precision variables and constants is eight bytes. Declaration of character variables is:

```
char var1,var2,.. .varn;
```

Note that the actual memory needed for the various data types may very well be system dependent. Also, allocating storage does not erase whatever was previously stored in that location. For results to be meaningful, constants and variables must be defined as well as declared. This may be done through input, within the declaration, or by an assignment statement.

The basic executable statement is an assignment statement. The assignment statement is interpreted in three steps: calculating the value of the expression on the right, converting it to the proper type, and storing it in the variable on the left, directly or indirectly. Variables must be given names; an identifier starts with a letter may contain letters, digits, and the underscore. Meaningful names should be used to represent variables in the program. Arithmetic operators are used to perform numerical computations in science and engineering problems. C has a rich collection of library functions, consisting of input/output functions, mathematical functions, string manipulation functions, memory allocation functions, standard library functions, and other miscellaneous functions. These functions have prototypes organized and stored in header files. The programmer must include appropriate header file to use these. For example to use input and output functions write the following statement:

```
#include <stdio.h>
```

Every C program must have a function called main(). This means the instructions following the function header must be enclosed in braces, starting with a left brace and ending with a right brace. The body of the function is a sequence of declarations, control structures, and executable statements ending with return. Comments should be used to make the code more readable.

## Exercises

- 1. Write a program to convert Fahrenheit temperature to Celsius temperature for one input value. Output both the Fahrenheit and the Celsius values. The conversion formula is:
![](img/8356e6c3bfe3b10354682c60b1e74b1d_145_0.png)
- 2. Write a program to compute the internal volume of a rectangular water tank of internal length $l$, width $w$, and height $h$.
- 3. Write a program to evaluate the polynomial $f(x) = x^3 + 5x^2 + 10x + 15$
- 4. Write a program to compute the distance between the points $p_1(x_1, y_1)$ and $p_2(x_2, y_2)$ given the coordinates $(x_1, y_1)$ and $(x_2, y_2)$.
Distance = $\sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$
- 5. Write a program to calculate the volume flow rate in cubic feet per second of water flowing through a pipe of diameter $d$ in inches and a velocity of $v$ feet per second. The formula for the flow rate is given by:
$q = \text{area} * \text{velocity}$
where area = $\pi d^2/4$ in square feet.
- 6. Write a program to calculate the $x$ and $y$ coordinates of a point at a distance $r$ from the origin at an angle $\theta$ to the $x$-axis as shown in the following figure.
![](img/8356e6c3bfe3b10354682c60b1e74b1d_146_0.png)
The trigonometric functions are as follows:
$x = r \cos \theta$
$y = r \sin \theta$.
