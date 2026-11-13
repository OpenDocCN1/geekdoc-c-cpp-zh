```
{
    int i, n;
    printf("\n Enter the number of students : ");
    scanf("%d", &n);
    for(i=0;i<n;i++)
    {
        ptr_stud[i] = (struct student *)malloc(sizeof(struct student));
        printf("\n Enter the data for student %d ", i+1);
        printf("\n ROLL NO. : ");
        scanf("%d", &ptr_stud[i]->roll_no);
        printf("\n NAME : ");
        gets(ptr_stud[i]->name);
        printf("\n COURSE : ");
        gets(ptr_stud[i]->course);
        printf("\n FEES : ");
        scanf("%f", &ptr_stud[i]->fees);
    }
    printf("\n DETAILS OF STUDENTS");
    for(i=0;i<n;i++)
    {
        printf("\n ROLL NO. = %d", ptr_stud[i]->roll_no);
        printf("\n NAME = %s", ptr_stud[i]->name);
        printf("\n COURSE = %s", ptr_stud[i]->course);
        printf("\n FEES = %f", ptr_stud[i]->fees);
    }
    return 0;
}
```

```
Output
Enter the number of students : 1
Enter the data for student 1
ROLL NO. : 01
NAME : Rahul
COURSE : BCA
FEES : 45000
DETAILS OF STUDENTS
ROLL NO. = 01
NAME = Rahul
COURSE = BCA
FEES = 45000
```

# 8. Write a program that passes a pointer to a structure to a function.

```
#include <stdio.h>
#include <conio.h>
#include <alloc.h>
struct student
{
    int r_no;
    char name[20];
    char course[20];
    int fees;
};
void display (struct student *);
main()
{
    struct student *ptr;
    ptr = (struct student *)malloc(sizeof(struct student));
    printf("\n Enter the data for the student ");
    printf("\n ROLL NO. : ");
    scanf("%d", &ptr->r_no);
```