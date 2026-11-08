```
```c
fclose(fp1);
fp2=fopen("kiran.txt","w");
if(fp2==NULL)
{
    printf("file can not be open");
}
else
{
    while(fscanf(fp1,"%s %s %d %d",&name,&desig,&age,&basic)!=EOF)
    {
        fprintf(fp2,"%s %s %d %d\n",name,desig,&age,&basic);
    }
}
fclose(fp2);
getch();
}
```
```

**Output**

Sri  RegionalManager  46  70000

# 76. Write a C program to read name and marks of n number of students from user and store them in a file.

```
```c
#include <stdio.h>
int main()
{
    char name[50];
    int marks, i, num;

    printf("Enter number of students: ");
    scanf("%d", &num);

    FILE *fptr;
    fptr = (fopen("C:\\student.txt", "w"));
    if(fptr == NULL)
    {
        printf("Error!");
        exit(1);
    }

    for(i = 0; i < num; ++i)
    {
        printf("For student%d\nEnter name: ", i+1);
        scanf("%s", name);

        printf("Enter marks: ");
        scanf("%d", &marks);
        fprintf(fptr,"\nName: %s \nMarks=%d \n", name, marks);
    }
    fclose(fptr);
    return 0;
}
```
```