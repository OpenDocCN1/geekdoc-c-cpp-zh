
scanf("%d", &i_first);
printf("\nEnter second number: ");
scanf("%d", &i_second);
/* Call function swap */
swap(&i_first, &i_second);
/* Print new values */
printf("\nNew value of first number is %d.\n", i_first);
printf("\nNew value of second number is %d.\n", i_second);
return;
} /* End of function main */

**Output:**

Enter first number: 75

Enter second number: 50

New value of first number is 50

New value of second number is 75.

It can be seen in Program 6 that we have defined a function called swap that takes two pointer variable as parameter. The function swap does not return any value to the function main. The job of the function swap is to interchange the values of the variables i_first and i_second used in the function main. Figure 10 illustrates the stack frame of the function main and the function swap:

![](img/5d422ba7108ffdf64376be51eaf0c459_187_0.png)

It can be seen in Figure 10 that when the operating system calls the function main, two local variables of the function main are created in the memory. When the call to function swap is made within the function main, a total of three local variables, namely, i_first, i_second, and i_temp, are created in the memory. The variables i_first and i_second in the function swap are assigned values 0x2000 and 0x2006. These values are the address of variables used in the function main. When the function swap is processed, we dereference these address values and swap the actual contents in the function main. Figure 11 illustrates the final swapping of values:

![](img/5d422ba7108ffdf64376be51eaf0c459_188_0.png)

A programmer has to be cautious while using pass-by-address mechanism, as a slight problem in the logic of the program can crash the working program or give unwanted results. The next section discusses a concept of recursion in functions.

## 8.6 Recursive Function

Recursion is one of the major concepts of structured programming in C language. A function that calls itself repeatedly based on some condition is called a recursive function. This simply means that one of the executable statements within the function designed is a call to itself. Recursion is used to split a complex problem into a single simplest possible solution. The recursive function thus can only give us the simplest possible solution. Most of the problems that are iterative in nature can be solved through recursion. However, iteration and recursion are still two different entities. Program 7 illustrates a recursive function that calculates the value of a number raised to its power:

### ▶ Program 7

```c
/* Program to illustrate recursive function */
#include <stdio.h>
/* Beginning of function raistopower */
int raisetopower(int i_number, int i_power)
{
if(i_power == 0)
    return (1);
else
    return (i_number * raisetopower(i_number, i_power - 1));
}
/* End of function raisetopower */
/* Beginning of function main */
main()
{
/* Declare local variables */
int i_number, i_power, i_result;
/* Accept value from user */
printf("\nEnter the number: ");
scanf("%d", &i_number);
printf("\nEnter the power: ");
scanf("%d", &i_power);
/* Check if power is positive or not */
if(i_power > 0)
{
/* Call function raisetopower */
i_result = raisetopower(i_number, i_power);
printf("\nThe number %d raised to the power of %d is %d.\n",
       i_number, i_power, i_result);
}
else
    printf("\nCalculation for negative power is not performed.\n");
return;
}
/* End of function main */
```

### Output 1:

Enter the number: 3

Enter the power: 2

The number 3 raised to the power of 2 is 9.

### Output 2:

Enter the number: -5

Enter the power: 3

The number -5 raised to the power of 3 is -125.

### Output 3:

Enter the number: 9

Enter the power: -2

Calculation for negative power is not performed.

It can be seen in Program 7 that we have defined a function called raisetopower that takes two integer parameter values as an input from the function main. It also returns an integer value back to the function main. The job of this function is to calculate the value of an integer number raised to its power. The function raisetopower is a recursive function. Observe the last statement of the function, that is, `return (i_number * raisetopower(i_number, i_power - 1));`. In this statement, a call is again made to function raisetopower. Figure 12 illustrates how the function recursion works for Program 7:

![](img/5d422ba7108ffdf64376be51eaf0c459_190_0.png)

**Figure 12: Recursive Function Call**

It can be seen in the Figure 12 that the one call of the function raisetopower within the function main recursively generates additional two calls. It can be seen that we are not able to return any value back to the calling functions until the call number 3 is processed. Once the function call number 3 receives value 1, its execution is completed. Similarly, the function call 2 receives value 3, and finally, the function call number 1 receives value 9 that is assigned to the variable i_result. The symbol shown in Figure 12 indicates that after returning the values, the function is removed from the stack.

Recursive functions can be effectively used to solve problems where the solution is expressed in terms of applying the same solution repeatedly. The use of recursive function also reduces the size of the program code and the program looks simpler. The only disadvantage of the recursive function is the memory requirement. With every call, the memory contents of the recursive function are replicated. A user should begin with the iterative solutions of a program first and then try to convert them to recursive solution.

The next section discusses a concept called command line arguments.

## 8.7 **Command-Line Arguments**

Throughout this book, you will observe that all executable C programs have a function main. The function main is an entry point of the program and is invoked by the environment (operating system) in which the program is executed. We have already mentioned that a function can accept parameters from the calling function. The same is true for the function main also. The function main can also accept parameters: the parameters accepted are generally input through the environment. These parameters are commonly known as command-line arguments. To pass the command-line arguments to the function main, the program needs to be run from the command prompt of an operating system.

Till now we have defined the function main using the syntax `main()` or `int main()`; to use command-line arguments, we need to use the syntax as follows:

`int main(int argc, char *argv[])`

In the preceding syntax, the parameters argc is an integer variable that refers to the number of command-line arguments passed. The minimum value of argc is always 1, and generally refers to the name of the program. The parameter argv is an array of character pointers (concept discussed in detail in Chapter 9). Program 8 illustrates the use of the command-line arguments;

### **Program 8**

```c
/* Program to illustrate command line arguments */
#include <stdio.h>
#include <string.h>

/* Beginning of function main */
main(int argc, char *argv[]) 
{ 
    /* Declare local variables */
    int i_octr, i_length, i_maxlength;
    int i_strindex = 1;

    /* Check number of command line arguments */
    if(argc > 1) 
    { 
        /* Find maximum length string */
        i_maxlength = strlen(argv[1]);
        
        for(i_octr = 2; i_octr <= argc; i_octr++)
        {
            i_length = strlen(argv[i_octr]);
            
            if(i_length >= i_maxlength)
            { 
                i_maxlength = i_length;
                i_strindex = i_octr;
            }
        }
    }
    
    /* Print the last string with maximum length */
    printf("The string %s is the longest.\n", argv[i_strindex]);
    return 0;
}
```

It can be seen in Program 8 that we have used the command-line arguments in the function main. The program checks the length of the strings provided as command-line arguments to identify the string that has maximum length. In case the list has more than one string that has maximum length, then the last string in the sequence is considered to have the maximum length. Observe that we have not provided any output for this program. Program 8 will not run from any Integrated Development Environment (IDE) directly, but has to executed from the command prompt. Figure 13 shows the syntax of executing the program on Disk Operating System (DOS) as well as Linux/UNIX environment along with the output that will be generated:

![](img/5d422ba7108ffdf64376be51eaf0c459_192_0.png)

It can be seen in Figure 13 that we have typed the name of the executable file (prog8_8.exe in case of DOS and prog8_8.o in case of Linux/UNIX) along with some names. All these names along with the name of the executable program are the contents of parameter argv. In case of DOS environment, argv[0] stores value *prog8_8.exe*, argv[1] stores value *navya*, and so on. The last value stored in argv[5] is *vidita*. The value of parameter in DOS environment is equal to 6. In case of Linux/UNIX environment, the value of argc is equal to 4 and the contents of the parameter argv also differ, as can be seen in Figure 13.
