```
```c
printf("Enter next number:\n");
scanf("%d",&number);
}
printf("Result of addition is %d",s);
}
```
```

# **Output**

```
Enter a number:
10
Enter next number:
20
Enter next number:
30
Enter next number:
40
Enter next number:
0
Result of addition is 100
```

# **SCRATCH PAD**

We accept the value of the variable number at each iteration of the while loop as seen in the code. Each value of the variable number which is read by the program is added to the value of variable s which represents the sum of the numbers entered by the user so far. The while loop terminates when the user inputs the value zero which represents the end of incoming data.

# **Solved Example 5.12**

Write a program to print Floyd’s triangle. The program should read the number of rows as input from the user and print the Floyd’s triangle which is given as below (The below triangle is drawn assuming the height as 5.):

```
1
2      3
4      5      6
7      8      9      10
11     12     13     14     15
```

```
```c
#include<stdio.h>
void main()
{
int i,j,r,value=1;
printf("Enter the number of rows:");
scanf("%d",&r);
    for(i=0 ; i<=r-1 ; i++)
```
```