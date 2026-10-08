In the preceding syntax, each user-defined function is identified by its name. The naming convention of the function is similar to that of a variable in C language. The only difference is that in functions, a parenthesis set is suffixed after the name. The function also has a data type; the data type here refers to the type of data the function will return back to the caller function. If the function only returns control but no value, then the data type is defined as void. The parameters are optional, but in case they are present, they refer to the input that will be accepted by the function. Each parameter has its own data type. These parameters are known as formal parameters, and are local to the function and do not exists outside the function. The declaration statement refers to the definition of variables used in the function. The executable statements are the ones that will be executed once a call to a function is made. Program 1 illustrates a C program that uses function to find the factorial of a given positive number:

▸ Program 1

```
```
/* Program to illustrate user-defined function */
/* Prototype of function factorial */
/* It takes an integer-value as input */
/* Returns a long integer value as output */
long factorial(int);
#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_number;
    long l_result;
    /* Input Data */
    printf("Enter a number : ");
    scanf("%d", &i_number);
    /* Check if number is greater than 0 */
    if(i_number > 0)
    {
        /* Call function factorial */
        l_result = factorial(i_number);
        /* Print the value of factorial */
        printf("Factorial of %d is %ld\n", i_number, l_result);
    }
    else
        printf("The number entered is zero or negative\n");
    return;
}
/* End of function main */
/* Function to calculate factorial of a positive number greater than 0 */
long factorial(int i_number)
{
    long l_result=1;
    int i_ctr;
    for(i_ctr= 1; i_ctr <= i_number; i_ctr++)
    {
        l_result = l_result * i_ctr;
    }
    return(l_result);
}
/* End of function factorial */
```
```