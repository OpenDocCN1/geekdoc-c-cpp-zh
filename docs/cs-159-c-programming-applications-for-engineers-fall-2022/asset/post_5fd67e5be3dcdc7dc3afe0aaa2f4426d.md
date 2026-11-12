

| Possible Observation | Reason why this may occur? |
| :--- | :--- |
| No problem, program works as expected. | Going beyond the limits of the array and into memory that is NOT reserved for the purpose of the array MAY NOT be reserved for any other purpose. |
| Program executes, but results are unexpected. | Going beyond the limits of the array and into memory that is NOT reserved for the purpose of the array MAY be reserved for any other purpose and multiple edits to the same memory may leave an unexpected value being stored. |
| Program crashes. | Going beyond the limits of the array and attempting to access memory that DOES NOT exist or that the program does not have the ability to access. |

## Examples of exceeding the defined limits of an array

```c
int x[5] = {8, 4, 5, 2, 3};
```

| 8 | 4 | 5 | 2 | 3 |
| 0 | 1 | 2 | 3 | 4 |

## Arrays and Functions (Inter-Function Communication)

Arrays are going to be of limited use to us if they are confined only to the function in which they are declared. There are two approaches for sharing data in an array with a user-defined function, we can either send an element, or the entire array.

## Within each method we must understand the following:

- How the function declaration, function call, and function definition change in terms of syntax.
- Whether the values being passed are by value or by address and if a method other than the default can be used.

## Passing Individual Elements

You can pass individual elements to a function like any other variable, as long as the array element type matches the function parameter type, it can be successfully passed to a function.

```c
#define SIZE 5
int calcFactorial(int);
int main(void)
{
   int num = 8;
   int data[SIZE] = { 2, 4, 6, 3, 5};
   printf("Result: %d\n", calcFactorial(num) );
   printf("Result: %d\n", calcFactorial(data[2]));
   return(0);
}
int calcFactorial(int x)
{
   int xFact = 1;
   while(x > 1)
   {
      xFact *= x--;
   }
   return(xFact);
}
```

## Example: Given an initialized integer array, print the square of each integer in the array.

```c
#define ARRAYSIZE 5
void print_square(int);
int main(void)
{
    int lcv;
    int base[ARRAYSIZE] = {3, 7, 2, 4, 5};
    for(lcv = 0; lcv < ARRAYSIZE; lcv++)
    {
        print_square(base[lcv]);
    }
    printf("\n");
    return(0);
}
void print_square(int x)
{
    printf("%d squared = %d\n", x, x * x);
}
```

## Observation from the previous program:

- When passing a single element of an array to a function you must specify the name of the array followed by the specific index of the value being passed in between the [ ] braces.

## Review Pass By Value

- Recall if we pass a single variable to a function that it is only a copy of the variable's value that is sent to the function such that changes to this copy does not change the variable back in the calling function.
- How is a single element of an array passed to a function? The first example that follows demonstrates the pass by value technique as demonstrated in chapter 4. The second example attempts to demonstrate whether a single element of an array is passed by value or by address.
- Should x[1] be 24 in the final print statement then we would conclude that the element was passed by value.
- Should x[1] be 3 in the final print statement then we would conclude that the element was passed by address.

```c
void passTest(int);
int main(void)
{
    int x = 32;
    printf("Before x = %d\n", x);
    passTest(x);
    printf("After x = %d\n", x);
    return(0);
}
void passTest(int g)
{
    printf("Before g = %d\n", g);
    g = g / 8;
    printf("After g = %d\n", g);
}
```

```c
void passTest(int);
int main(void)
{
    int x[3] = {16, 24, 32};
    printf("Before x[1] = %d\n", x[1]);
    passTest(x[1]);
    printf("After x[1] = %d\n", x[1]);
    return 0;
}
void passTest(int g)
{
    printf("Before g = %d\n", g);
    g = g / 8;
    printf("After g = %d\n", g);
}
```

Output of program above:

From the output you can see that a single element of an array is treated the same as a single variable being passed to a function, that is, a single element of an array is passed by value.

- Is it possible to make use of pass by address with individual elements of an array?

## Example: Swap two elements of an array by passing them both by address to a function.

```c
#define SIZE 10
void swapValues(int *, int *);
void main(void)
{
 int x[SIZE] = {3, 4, 5, 1, 2, 9, 8, 7, 6, 0};
 printf("x[4] = %d x[5] = %d\n", x[4], x[5]);
 swapValues(&x[4], &x[5]);
 printf("x[4] = %d x[5] = %d\n", x[4], x[5]);
 return 0;
}
void swapValues(int *ax, int *ay)
{
 int temp;
 temp = *ax;
 *ax = *ay;
 *ay = temp;
}
```

## Example: Passing the x[1] element by address.

```c
#include <stdio.h>
void passTest(int *);
void main(void)
{
 int x[3] = {16, 24, 32};
 printf("Before x[1] = %d\n", x[1]);
 passTest(&x[1]);
 printf("After x[1] = %d\n", x[1]);
 return 0;
}
void passTest(int *g)
{
 printf("Before g = %d\n", *g);
 *g = *g / 8;
 printf("After g = %d\n", *g);
}
```

## Passing the Whole Array

What if we have an array of size 10 and we need to pass all 10 elements to a function?

## Option #1, Pass Every Element

```c
void fun(int, int, int, int, int, int, int, int, int, int);
```

## Option #2, Pass Entire Array

```c
void fun(int []);
```

There is more here in terms of syntax and an end result that may be surprising when it comes to our conclusion regarding the passing technique used.

| | |
| - | - |
| `#include <stdio.h><br>void passTest(int []);<br>int main(void)<br>{<br>   int x[3] = {16, 24, 32};<br>   printf("Before x[1] = %d\n", x[1]);<br>   passTest(x);<br>   printf("After x[1] = %d\n", x[1]);<br>   return(0);<br>}` | `When passing the whole array to a function you only need to list the name of the array.` |
| `void passTest(int y[])<br>{<br>   printf("Before y[1] = %d\n", y[1]);<br>   y[1] = y[1] / 8;<br>   printf("After y[1] = %d\n", y[1]);<br>}` | `DO NOT include any of the following:<br>* The square braces as seen in the function declaration and definition.<br>* The size of the array as used in the array declaration.<br>* The data type of the array. When have we ever listed the type of a parameter in a function call?` |
| | `Output of program on left:` |
| | `Conclusion – Whole arrays are passed by address.` |

- Consider this: if arrays were passed by value then this requires a complete duplication of memory necessary to store the copy of the array. This would be a very inefficient use of memory. Rather than passing a copy of the array the language passes the address of the array. Is it even possible to pass a whole array by value? No.
- No & operator in the user-defined function call as in chapter 4? The name of an array already references a memory address!
- Which memory address is represented by the name of an array? Arrays only track where they begin in memory and not where they end!
- What does an index value represent? The index value provided is added to the address represented by the name of the array to locate the desired element inside of the array. The index essentially serves as an offset from where the array begins in the memory of the computer.

```c
void getData(int b[])
{
    int lcv;
    printf("Enter integer data set now -> ");
    for(lcv = 0; lcv < ARRAYSIZE; lcv++)
    {
        scanf("%d", &b[lcv]);
    }
}
```

Example: Calculate the average of the values in a 50-element integer array:

```c
#include <stdio.h>
#define ARRAYSIZE 50
float average (int []);
void getData(int []);
int main (void)
{
    int base [ARRAYSIZE];
    float avg;
    getData (base);
    avg = average (base);
    printf("The average = %.2f\n", avg);
    return(0);
}
```

```c
float average(int b[])
{
    int lcv;
    float avg = 0.0;
    for(lcv = 0; lcv < ARRAYSIZE; lcv++)
    {
        avg += b[lcv];
    }
    avg = avg / ARRAYSIZE;
    return(avg);
}
```

What would be the result of the print statement below if it were inserted into the main function ?

```c
printf("%d\n", base);
```

Why are index range violations possible?

- The address represented by the name of the array is added to the specified index to calculate a new memory address. This address may be beyond that memory specifically allocated for the array.

