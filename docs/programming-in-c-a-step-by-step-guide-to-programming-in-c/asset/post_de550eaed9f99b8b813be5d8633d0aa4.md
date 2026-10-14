
```
float price;
};
```

```
struct book_bank book1, book2, book3;
```

It is also allowed to combine both the template declaration and variables declaration in one statement.

```
struct book_bank
{
char title[20];
char author[15];
int pages;
float price;
} book1, book2, book3;
```

## General format of a Structure Definition:

The general format of a structure definition is as follows:

```
struct tag_name
{
data_type member1;
data_type member2;
-----
};
```

In defining a structure you may note the following syntax:

+ 1. The template is terminated with a semicolon.
+ 2. While the entire declaration is considered as a statement, each member
is declared independently for its name and type in a separate statement inside the template.

3. The tag name such as tag_name can be used to declare structure variables of its type, later in the program.

## Giving values to Members:

Structure members need to be linked to the structure variables in order to make them meaningful members. The link between a member and a variable is established using the member operator ‘.’ which is also known as ‘dot operator’ or ‘period operator’.

Here is how we would assign values to the members of book1.

```
strcpy(book1.title,"BASIC");
```

```
strcpy(book1.author,"Balagurusamy");
```

```
book1.pages = 250;
```

```
book1.price = 28.50;
```

We can also give the values through the keyboard.

```
gets(book1.title);
```

```
gets(book1.author);
```

```
printf("%d",book1.pages);
```

```
printf("%f",book1.price);
```

## Structure Initialization: void main()

```
{
```

```
struct st_record
```

```
{
```

```
char name[20];
```

```
int weight;
```

float height;

};

static struct st_record student1 = {"Suresh", 60, 180.75}; static struct st_record student2 = {"Umesh", 53, 170.60}; }

## Program 10.1: To print the date of joining of a person

```c
#include<conio.h>

#include<stdio.h>

struct personal
{
char name[30];
int day;
int month;
int year;
float salary;
};

void main()
{
struct personal p;
printf("Enter the name:\n");
gets(p.name);
printf("Enter the day of joining:\n");
scanf("%d",&p.day);
printf("Enter the month of joining:\n");
scanf("%d",&p.month);
```

```
printf("Enter the year of joining:\n");
scanf("%d",&p.year);
printf("Enter the salary:\n");
scanf("%f", & p.salary);
printf("\nName:",p.name);
printf("\nDate of joining:%d %d %d",p.day,p.month,p.year);
printf("Salary:",p.salary);
getch();
}
```

## Comparison of structure variables

Two variables of same structure type can be compared in the same way as ordinary variables. If **person1** and **person2** belong to the same structure, then the following operations are valid:

| Operation | Meaning |
|---|---|
| **person1 = person2** | Assign **person2** to **person1** |
| **person1 == person2** | Compare all members of **person1** and **person2** and return 1 if they are equal, 0 otherwise. |
| **person1 != person2** | Return 1 if all the members are not equal, 0 otherwise |

## Program 10.2: To Compare structure variables

```
#include <stdio.h>
#include<conio.h>
struct stclass{
```

```c
int number;
char name[20];
float marks;
};

void main(){
int x;
static struct stclass student1 = {111,"Rao",72.50};
static struct stclass student2 = {222,"Reddy",67.00};
struct stclass student3;
student3 = student2;

x=((student3.number == student2.number) && (student3.marks == student2.marks))? 1:0;
if(x == 1)
{
printf("\nStudent2 and Student3 are same");
printf("%d\t %s\t %f\t",student3.number,student3.name,student3.marks);
}
else
{
printf("\nStudent2 and student3 are different");
}
getch();
}
```

## Self Assessment Questions

1. A __________ is a convenient tool for handling a group of logically related data items.

2. We can declare structure variables using the tag name anywhere in the program. (True/False)

3. __________ is a method for packing data of different types.

4. If person1 and person2 are variables of the same type structure then the expression person1>person2 is valid. (True/False)

5. __________ is a method for packing data of different types.

6. The link between a member and a variable is established using the member operator __________.

## 10.3 Structures and Functions

We can write programs with structures by using modular programming. We can write a function that returns the structure. While writing the function, you should indicate the type of structure that is returned by the function. The **return** statement should return the structure using a variable. It is to pass a structure as an argument. We can modify a member of the structure by passing the structure as an argument. The changes in the member made by the function are retained in the called module. This is not against the principle of call by value because we are not modifying the structure variable, but are instead modifying the members of the structure.

## Program 10.3: To illustrate the concept of structures and functions

```
struct student
{
char name[30];
float marks;
};
main ()
{
struct student student1;
student1 = read_student ();
print_student( student1);
read_student_p(student1);
print_student (student1);
}
struct student read_student()
{
struct student student2;
gets(student2.name);
scanf("%d",&student2.marks);
return (student2);
}
void print_student (struct student student2)
{
printf( "name is %s\n", student2.name);
printf( "marks are%d\n", student2.marks);
```

```
}
void read_student_p(struct student student2)
{
gets(student2.name);
scanf("%d",&student2.marks);
```

## Explanation

+ 1. The function read_student reads values in structures and returns the structure.
+ 2. The function print_student takes the structure variable as input and prints the content in the structure.
+ 3. The function read_student_p reads the data in the structure similarly to read_student. It takes the structure student as an argument and puts the data in the structure. Since the data of a member of the structure is modified, you need not pass the structure as a pointer even though structure members are modified. Here you are not modifying the structure, but you are modifying the structure members through the structure.

## Self Assessment Questions

7. We cannot write a function that returns the structure. (True/False)

8. We can modify a member of the structure by passing the structure as a __________.

## 10.4 Arrays of Structures

We can use structures to describe the format of a number of related variables. For example, in analyzing the marks obtained by a class of students, we may use a template to describe student name and marks obtained in various subjects and then declare all the students as structure variables. In such cases, we may declare an array of structures, each element of the array representing a structure variable. e.g, `struct stclass student[100];` defines an array called student, that consists of 100 elements. Each element is defined to be of the type struct stclass. Consider the following declaration:

```
```c
struct marks
{
    int subject1;
    int subject2;
    int subject3;
};

main()
{
    static struct marks student[3] = {{45,68,81},{75,53,69},{57,36,71}};
}
```
```

This declares the student as an array of three elements student[0], student[1] and student[2] and initializes their members as follows: student[0].subject1 = 45; student[0].subject2 = 68; ........ student[2].subject3 = 71;

## Program 10.4: To process employee details using structures

```
```c
#include <conio.h>
#include <stdio.h>

struct employee
{
```

```
int empno;
char name[30];
int basic;
int hra;
};
void main()
{
int i,j,n,net[50];
float avg;
employee e[50];
printf("\nEnter the number of employees:");
scanf("%d", &n);
printf("\nEnter Empno.\tName\tBasic\tHra of each employee:\n"); for(i=0;i<n;i++)
{
scanf("%d",&e[i].empno);
gets(e[i].name);
scanf("%d",&e[i].basic);
scanf("%d",&e[i].hra);
net[i]= e[i].basic+e[i].hra;
avg=avg+net[i];
avg=avg/n;
printf("\nEmpno.\tName\tNetpay\n");
for(i=0;i<n;i++)
{
```
