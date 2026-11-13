Note Of all the operators ->, ., (, ) and [] have the highest priority. This is evident from the following statement stud1.fees++ will be interpreted as (stud1.fees)++.

# 5.1.5 Copying and Comparing Structures

We can assign a structure to another structure of the same type. For example, if we have two structure variables stud1 and stud2 of type struct student given as

![](bbox=[0.1, 0.24, 0.4, 0.41])

# Figure 5.3 Values of structure variables

```
struct student stud1 = {01, "Rahul", "BCA", 45000};
struct student stud2;
```

Then to assign one structure variable to another, we will write

```
stud2 = stud1;
```

This statement initializes the members of stud2 with the values of members of stud1. Therefore, now the values of stud1 and stud2 can be given as shown in Fig. 5.3.

C does not permit comparison of one structure variable with another. However, individual members of one structure can be compared with individual members of another structure. When we compare one structure member with another structure's member, the comparison will behave like any other ordinary variable comparison.

> **Programming Tip**
> An error will be generated if you try to compare two structure variables.

For example, to compare the fees of two students, we will write
if(stud1.fees > stud2.fees) //to check if fees of stud1 is greater than stud2

# PROGRAMMING EXAMPLES

+   1. Write a program using structures to read and display the information about a student.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    struct student
    {
        int roll_no;
        char name[80];
        float fees;
        char DOB[80];
    };
    struct student stud1;
    clrscr();
    printf("\n Enter the roll number : ");
    scanf("%d", &stud1.roll_no);
    printf("\n Enter the name : ");
    scanf("%s", stud1.name);
    printf("\n Enter the fees : ");
    scanf("%f", &stud1.fees);
    printf("\n Enter the DOB : ");
    scanf("%s", stud1.DOB);
    printf("\n ******************STUDENT'S DETAILS *******");
    printf("\n Roll No. = %d, stud1.roll_no);
    printf("\n NAME = %s, stud1.name);
    printf("\n FEES = %f, stud1.fees);
}
```