# 5.2.1 Printing a message inside while loop: An example

As an example, let us write a program to print a message Loops made simple five times on a computer screen. One method to get this output is to write the statement: printf("Loops made simple\\n"); five times in the program. However, this will then be a hard-coded program where the number of times the message would appear will always be five. Let us design a code which can print the message for any k number of times, instead of hard coding to five. Also, study of loops is all about avoiding repetitive effort of writing the same line again and again in the code. The approach is simply unrealistic if we want to print a message say 1000 times. Hence, instead of typing the same printf() statement multiple times we shall write it only once and put it in the loop so that it is executed multiple times.

We can put the printf() statement in the loop as shown below:

```
while(<condition>) {
printf("Loops made simple\\n");
<code to control the condition>
}
```

while loop will repeat the execution of printf() statement as long as the condition is evaluated as true. Hence, we need to design a condition such that the condition is evaluated as true for the first five iterations and becomes false later on as we need to print the message only five times on the screen.

To design such a condition, we maintain a counter variable say i with an initial value of 1.

```
int i = 1;
```

Each time the operation is performed, we increment the value of i by 1. This will ensure that we always store the count of times printf() is executed in the variable i. This means that any iteration of while loop can determine the progress by looking at the value of variable i. To clarify further, when value of i is 2, it will imply that the operation is executed two times, when value of i is 3, it will imply that the operation is performed three times and so on. In general, when the value of i is k, we can say that operation is performed k times. Here, we need to perform the operation 5 times, i.e., we need to print a message for values of variable i = 1, 2, 3, 4, 5, or once i crosses 5 the loop shall terminate. In other words, the loop must continue till i is <= 5. Hence, i<=5 is the condition for while loop to run as shown below:

```
while(i<=5){
printf("Loops made simple\\n");
i++; /*increment value of i in each iteration*/
}
```

The following is the full source code to print the message Loops made simple five times on the computer screen:

```
#include<stdio.h>
void main()
{
    int i=1;
```