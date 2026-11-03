If there are two different types in an expression then both will convert to better type.In an assignment statement, final result of calculation will be converted to the type of the variable which will hold the result of the calculation (ex. the variable “count” in the assignment count=i+1;)

For example if you add two values from int and float type and assign it to a double type variable, result will be double.

# Using loops in an example -

# Write a program – To accept scores of a person and calculate sum of them and their average and print them.

```
```c
#include<stdio.h>
#include<conio.h>
main()
{
int count=0;
float num=0,sum=0,avg=0;
printf(\u0022Enter score (-1 to stop): \u0022);
scanf(\u0022%f\u0022,&num);
while(num>=0)
{
sum=sum+num;
count++;
printf(\u0022Enter score (-1 to stop): \u0022);
scanf(\u0022%f\u0022,&num);
}
avg=sum/count;
printf(\u0022\\nAverage=%f\u0022,avg);
printf(\u0022\\nSum=%f\\n\u0022,sum);
system(\u0022pause\u0022);
}
```
```

This example we get first number and then enter the loop. We will stay inside loop until user enters a value smaller than 0. If user enters a value lower than 0 we will interpret it as STOP receiving scores.

# Here are the output results of a sample run:

Enter score (-1 to stop): 12
Enter score (-1 to stop): 14