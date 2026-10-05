
# Output is shown in Output 8.9.

```
Enter the details of the Student[1]:
Name :sachin
Reg No:10243
Year :1
Branch:CSE
Want to continue? (YES/NO:1/0) 1
Enter the details of the Student[2]:
Name :guvi
Reg No:12561
Year :2
Branch:ECE
Want to continue? (YES/NO:1/0) 1
Enter the details of the Student[3]:
Name :Schway
Reg No:25416
Year :3
Branch:Civil
Want to continue? (YES/NO:1/0) 1
Enter the details of the Student[4]:
Name :Sourav
Reg No:10254
Year :2
Branch:Mechanical
Want to continue? (YES/NO:1/0) 0
Details of the students are...
```

# 8.1.6. Passing structures to functions

Passing an ordinary variable or an array to a method is what we generally do. Having discussed about the Powerful Structures, the reader should raise a question, 'How to pass an entire structure to the method for calculation purposes?' For example, passing an array of structures to a method which is defined to find out the total marks and average marks of every student.

Passing a structure to a method is not very complicated. It is simple.

Just need the name of the structure variable in the function call.

Suppose we have

- a structure named 'Cricket'
- players[11] as its variable (Array of structures) and
- a method kriketers () meant for dealing with the player’s records.

# Output 8.10 for Program 8.10

| NAME | YEAR | BRANCH |
| :--- | :--- | :--- |
| sachin | 1 | CSE |
| guvi | 2 | ECE |
| Schway | 3 | Civil |
| Sourav | 2 | Mechanical |

# STRUCTURES AND UNIONS 133

Passing the structure Cricket to kriketers () is done via a function call as, kriketers (players);
How to declare the method then?
`<return_type> (struct Cricket []);`
Function/ Method definition is done in traditional format.

```
<return_type> <function_name>(parameters)
{
---function body—
}
```

The program 8.11 given below would throw more light on this concept.

```c
#include<stdio.h>
#include<conio.h>

struct student
{
    char s_name[30];
    long int s_regno;
    int year_of_study;
    char branch[10];
    int marks[3];
}
var[5];
void avg_function(struct student [], int);
{
    int index=0,yesno,i,j;
    do {
        printf("nEnter the details of the Student[%d]:\n",index+1);
        printf("Name :%s",var[index].s_name);
        printf("\nReg :%d",scanf("%d",&var[index].s_regno));
        printf("\nYear :%d",scanf("%d",&var[index].year_of_study));
        printf("\nBranch :%s",scanf("%s",var[index].branch));
        for (j=0;j<3;j++) {
            printf("\nMark %d",j+1);scanf("%d",&var[index].marks[j]);
        }
        printf(
        Want to continue? (YES/NO: 1/0)",scanf("%d",&yesno);
        index++;
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_144_0.png)

# 134

# C-SIMPLER

avg_function(var,index);
getch();

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_145_0.png)

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_145_1.png)

```c
void avg_function(struct student obj[], int index)
{
    int i,total_marks=0,avg,j;
    for (i=0;i<index;i++) {
        for (j=0;j<3;j++) {
            total_marks+=obj[i].marks[j];
        }
        printf("\nThe total of Student %d is %d out of 300\n", i+1,total_marks);
        printf("\nThe average of Student %d is %d\n", i+1, total_marks/3);
        total_marks=0;
    }
}
```

# Program 8.11 Passing Structure to Functions

On executing the Program 8.11, we are confronted with the output as shown below in Output 8.11.

```
Enter the details of the Student[1]:
Name :Rahul
Reg No:3225
Year :3
Branch:Civil
Mark 1:86
Mark 2:68
Mark 3:79
Want to continue? (YES/NO: 1/0) 1
Enter the details of the Student[2]:
Name :Dravid
Reg No:3226
Year :4
Branch:CSE
Mark 1:98
Mark 2:87
Mark 3:76
Want to continue? (YES/NO: 1/0) 1
Enter the details of the Student[3]:
Name :Sourav
Reg No:3227
Year :3
Branch:ECE
Mark 1:68
Mark 2:87
Mark 3:89
```

| NAME | REGNO | YEAR | BRANCH | MARK1 | MARK2 | MARK3 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Rahul | 3225 | 3 | Civil | 86 | 68 | 79 |
| Dravid | 3226 | 4 | CSE | 98 | 87 | 76 |
| sourav | 3227 | 3 | ECE | 68 | 87 | 89 |

total of student 1 is 233 out of 300
The average of student 1 is 77
total of student 2 is 261 out of 300
The average of student 2 is 87
total of student 3 is 244 out of 300
The average of student 3 is 81

Output 8.11

# 8.1.7. Nested structures

Meaning, Structure within another Structure. Those who have come across Database Management Systems (DBMS) would be aware of composite attributes. Date of Birth (DOB) attribute is an instance of this. As it can be observed from DOB, it has parts (mm/dd/yyyy). Unfortunately, if we have to use anywhere while coding, we don't have the flexibility of using built-in data type like 'date'. There comes the use of structures and nested structures.

We can define a structure 'Date' with following variables:

1. int day
2. int month
3. int year

Another structure named Student will have the following statement.
Struct Date obj; where obj is an instance of the structure 'Date'.
Accessing day, month, year via obj:
var.obj.day;
var.obj.month;
var.obj.year;
where var is the variable for the structure 'Student'.

Program 8.12 given below explain the concept.

```c
#include <stdio.h>
#include <conio.h>
struct Date {
    int day;
    int month;
    int year;
}
struct student {
    char s_name[30];
    long int s_regno;
    int year_of_study;
    char branch[10];
    int marks[3];
    // Nested Structure: 'Date' inside 'student'
    struct Date obj;

void main() {
    printf("\n Enter the details of the Student\n");
    printf("\nName: %s");scanf("%s", &var.s_name);
    printf("\nReg No: %ld");scanf("%ld", &var.s_regno);
    printf("\nYear: %d");scanf("%d", &var.year_of_study);
    printf("\nBranch: %s");scanf("%s", &var.branch);
    printf("\nDOB: %d/%d/%d");scanf("%d/%d/%d", &var.obj.day, &var.obj.month, &var.obj.year);
    printf("\nThe details are...\n");
    printf("\nName: %s", var.s_name);
    printf("\nReg No: %ld", var.s_regno);
    printf("\nYear: %d", var.year_of_study);
    printf("\nBranch: %s", var.branch);
    printf("\nDOB: %d/%d/%d", var.obj.day, var.obj.month, var.obj.year);
    getch();
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_147_0.png)

# Program 8.12 Nested Structures

# STRUCTURES AND UNIONS

Output of Program 8.12 is shown in Output 8.12.

```
Enter the details of the Student
Name :michael
Reg No:3226
Year :3
Branch:Biotech
DOB:21/1/1989
The details are...
Name :michael
Reg No:3226
Year :3
Branch:Biotech
DOB:21/1/1989
```

Output 8.12

# 8.2. UNIONS

Yet another User defined data type is Union! Syntactically there’s no big difference between these and Structures. But with respect to memory allocations, there is a huge difference to be noted.

We can store information in one field at a time in a Union data type. We can leave it as such imagine unions as a chunk of memory Once a new value is written into it, the old value will be wiped out or erased completely.

The major difference between structures and unions is given in Table 8.1:

| Structures | Unions |
| :--- | :--- |
| Size of a Structure is equal to Sum of the sizes of its individual variables. | The size of a union is equal to the size of its largest data member. |
| Example, | Example, |
| struct s | union s |
| int a; | int a; |
| char b; | char b; |
| }; | }; |
| Size = 5 bytes (theoretically) | Size = 4 bytes (Size of integer) |

Table 8.1 Difference between structures and unions

# 8.2.1. Accessing union fields

To access the fields of a union, we use the dot operator(.) just as we would for a structure. When a value is assigned to one member, the other member(s) gets wiped out since they share the same memory.

Program 8.13 explains Union Concept.

```c
#include <stdio.h>
union data {
char a;
int x;
float f;
} myData;
void main() {
    int mode = 1;
    myData.a = 'A';
    printf("Here is the Data: %c\n%d\n%f\n", myData.a, myData.x, myData.f);
    mode = 2;
    printf("Here is the Data: %c\n%d\n%f\n", myData.a, myData.x, myData.f);
    if (mode == 1) {
        printf("The float is being used\n");
    } else if (mode == 2) {
        printf("The int is being used\n");
    } else if (mode == 3) {
        printf("The char is being used\n");
    }
    getch();
}
```

> Union has 3 variables. Of which only one can be in memory at a time

| Size of this |
| :--- |
| Union: 4 bytes |

| char variable is used. Neither int float can be used |
| --- |
| int in use |

> Printing the other variables(x,f) would print simple garbage

> Printing char and float variables would throw garbage values!

# Program 8.13 Union program
