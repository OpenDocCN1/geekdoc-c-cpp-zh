In this example level and GPA are variables while junior, senior, Aminus, and Bplus are constants.

# 4.2.3 Multiway Structures

There is a special statement equivalent to the if-else...if-else...if...else...else. This can be used when all of the conditions check for values of the same variable, and those values may be 1, 2, 3, etc. This is usually used with assigned codes. The structure is called a case structure. In C it can be implemented by a switch statement.
The following example shows the use of if-else to implement a case structure:

```
int student_code;

scanf("%d", &student_code);

printf("The student code = %d\n", student_code);
if (student_code == 1)
{
    printf("The student is a freshman.\\n")
}
else if (student_code == 2)
{
    printf("The student is a sophomore.\\n")
}
else if (student_code == 3)
{
    printf("The student is a junior.\\n")
}
else if (student_code == 4)
{
    printf("The student is a senior.\\n")
}
else
{
    printf("The student is unclassified.\\n")
}
```

If the student_code matches the code specified in a conditional branch, only statements in the corresponding branch are executed. If the student_code does