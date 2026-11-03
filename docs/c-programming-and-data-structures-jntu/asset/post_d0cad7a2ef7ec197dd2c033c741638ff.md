
It is also allowed to combine both the template declaration and variables declaration in one statement.

The declaration

```
struct book_bank
{
  char title[20];
  char author[15];
  int pages;
  float price;
} book1, book2, book3;
```

is valid. The use of tag name is optional. For example,

```
struct
{
  ........
  ........
} book1, book2, book3;
```

declares book1, book2, and book3 as structure variables representing three books, but does not include a tag name for later use in declarations.

Normally, structure definitions appear at the beginning of the program file, before any variables or functions are defined. They may also appear before the main, along with macro definitions, such as #define. In such cases, the definition is global and can be used by other functions as well.

## 12.3 GIVING VALUES TO MEMBERS

We can assign values to the members of a structure in a number of ways. As mentioned earlier, the members themselves are not variables. They should be linked to the structure variables in order to make them meaningful members. For example, the word title, has no meaning whereas the phrase 'title of book3' has a meaning. The link between a member and a variable is established using the member operator '.' which is also known as 'dot operator' or 'period operator'. For example,

```
book1.price
```

is the variable representing the price of book1 and can be treated like any other ordinary variable. Here is how we would assign values to the members of book1:

```
strcpy(book1.title, "BASIC");
strcpy(book1.author, "Balagurusamy");
book1.pages = 250;
book1.price = 28.50;
```

We can also use scanf to give the values through the keyboard.

```
scanf("%s\n", book1.title);
scanf("%d\n", &book1.pages);
```

are valid input statements.

## 12.6 C Programming and Data Structures

Structure definition along with the program is shown in Fig. 12.1. The scanf and printf functions illustrate how the member operator '.' is used to link the structure members to the structure variables. The variable name with a period and the member name is used like an ordinary variable.

### Example 12.1

```
```c
/* DEFINING AND ASSIGNING VALUES TO STRUCTURE MEMBERS */
struct personal
{
    char name[20];
    int day;
    char month[10];
    int year;
    float salary;
};

main()
{
    struct personal person;
    printf("Input Values\n");
    scanf("%s %d %s %d %f",
           &person.name,
           &person.day,
           &person.month,
           &person.year,
           &person.salary);
    printf("%s %s %d %.2f\n",
           person.name,
           person.day,
           person.month,
           person.year,
           person.salary);
}
```
```

Input Values
M.L. Goel 10 January 1945 4500.00
M.L. Goel 10 January 1945 4500.00

![](img/65953ea584e494f3d396b2252cb5ea53_336_0.png)

Like any other data type, a structure variable can be initialized. However, a structure must be declared as static if it is to be initialized inside a function (similar to arrays).

Note: This condition is not applicable to ANSI compilers. The ANSI standard permits initialization of structure variables with auto storage class. We could therefore delete the word static when using ANSI compilers. However, the use of the keyword static in the programs would enable us to run them under both the old and ANSI standard compilers.

```
main()
{
    static struct
    {
        int weight;
        float height;
    }
    student = {60, 180.75};
    ....
    ....
}
```

This assigns the value 60 to student.weight and 180.75 to student.height. There is a one-to-one correspondence between the members and their initializing values.

A lot of variation is possible in initializing a structure. The following statements initialize two structure variables. Here, it is essential to use a tag name.

```
main()
{
    struct st_record
    {
        int  weight;
        float height;
    };
    static struct st_record student1 = {60, 180.75};
    static struct st_record student2 = {53, 170.60};
    ....
    ....
}
```

Another method is to initialize a structure variable outside the function as shown below:

```
struct st_record  /* No static word */
{
    int  weight;
    float height;
} student1 = {60, 180.75};
main()
{
    static struct st_record student2 = {53, 170.60};
    ....
    ....
}
```

C language does not permit the initialization of individual structure members within template. The initialization must be done only in the declaration of the actual variables.

## 12.5 COMPARISON OF STRUCTURE VARIABLES

Two variables of the same structure type can be compared the same way as ordinary variables. If person1 and person2 belong to the same structure, then the following operations are valid:

| Operation | Meaning |
|---|---|
| person1 = person2 | Assign person2 to person1. |
| person1 == person2 | Compare all members of person1 and person2 and return 1 if they are equal, 0 otherwise. |
| person1 != person2 | Return 1 if all the members are not equal, 0 otherwise. |

Note that not all compilers support these operations. For example, Microsoft C version does not permit any logical operations on structure variables. In such cases, individual members can be compared using logical operators.

### Example 12.2

Write a program to illustrate the comparison of structure variables.

The program shown in Fig. 12.2 illustrates how a structure variable can be copied into another of the same type. It also performs memberwise comparison to decide whether two structure variables are identical.

## 12.6 ARRAYS OF STRUCTURES

We use structures to describe the format of a number of related variables. For example, in analysing the marks obtained by a class of students, we may use a template to describe student name and marks obtained in various subjects and then declare all the students as structure variables. In such cases, we may declare an array of structures, each element of the array representing a structure variable. For example,

```
struct class student[100];
```

defines an array called student, that consists of 100 elements. Each element is defined to be of the type struct class. Consider the following declaration:

```
struct marks
{
    int subject1;
    int subject2;
    int subject3;
};
main()
{
    static struct marks student[3] = {
        {45,68,81}, {75,53,69}, {57,36,71}};
```

## Structures and Unions 12.9

This declares the student as an array of three elements student[0], student[1], and student[2] and initializes their members as follows:

```
student[0].subject1 = 45;
student[0].subject2 = 68;
.....
student[2].subject3 = 71;
```

```
Program
/* COMPARISON OF STRUCTURE VARIABLES */
struct class {
int number;
char name[20];
float marks;
};
main()
{
int x;
static struct class student1 = {111,"RAO",72.50};
static struct class student2 = {222,"Reddy",67.00};
struct class student3;
student3 = student2;
x = ((student3.number == student2.number) && (student3.marks == student2.marks)) ? 1 : 0;
if(x == 1)
{
printf("\nstudent2 and student3 are same\n");
printf("%d %s %f\n", student3.number, student3.name, student3.marks);
}
else
{
printf("\nstudent2 and student3 are different\n");
}
Output
student2 and student3 are same
222 Reddy 67.000000
```

![](img/65953ea584e494f3d396b2252cb5ea53_339_0.png)

Note that the array is declared just as it would have been, with any other array. Since student is an array, we use the usual array-accessing methods to access individual elements and then the member operator to access individual members.

An array of structures is stored inside the memory in the same way as a multi-dimensional array. The array student actually looks as shown in Fig. 12.3.

### Example 12.3

For the **student** array discussed above, write a program to calculate the subjectwise and studentwise totals and store them as a part of the structure.

|  |  |
|---|---|
| student[0].subject1 | 45 |
| . subject2 | 68 |
| . subject3 | 81 |
| student[1].subject1 | 75 |
| . subject2 | 53 |
| . subject3 | 69 |
| student[2].subject1 | 57 |
| . subject2 | 36 |
| . subject3 | 71 |

**Fig. 12.3** *The array student inside memory*

The program is shown in Fig. 12.4. We have declared a four-member structure, the fourth one for keeping the student-totals. We have also declared an array total to keep the subject-totals and the grand-total. The grand-total is given by **total.total**. Note that a member name can be any valid C name and can be the same as an existing structure variable name. The linked name **total.total** represents the **total** member of the structure variable total.

```
Program
/*------------------------------------------------------------*/
/* ARRAYS OF STRUCTURES */
/*------------------------------------------------------------*/
struct marks
{
 int sub1;
 int sub2;
 int sub3;
 int total;
};
main()
{
 int i;
 static struct marks student[3] = { {45,67,81,0},
 {75,53,69,0},
 {57,36,71,0}};
 static struct marks total;
 for(i = 0; i <= 2; i++)
 {
 student[i].total = student[i].sub1 +
 student[i].sub2 +
 student[i].sub3;
 total.sub1 = total.sub1 + student[i].sub1;
 total.sub2 = total.sub2 + student[i].sub2;
