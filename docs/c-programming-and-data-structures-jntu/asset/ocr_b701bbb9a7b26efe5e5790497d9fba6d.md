C language does not permit the initialization of individual structure members within template. The initialization must be done only in the declaration of the actual variables.

# 12.5 COMPARISON OF STRUCTURE VARIABLES

Two variables of the same structure type can be compared the same way as ordinary variables. If person1 and person2 belong to the same structure, then the following operations are valid:

| Operation | Meaning |
|---|---|
| person1 = person2 | Assign person2 to person1. |
| person1 == person2 | Compare all members of person1 and person2 and return 1 if they are equal, 0 otherwise. |
| person1 != person2 | Return 1 if all the members are not equal, 0 otherwise. |

Note that not all compilers support these operations. For example, Microsoft C version does not permit any logical operations on structure variables. In such cases, individual members can be compared using logical operators.

# Example 12.2

Write a program to illustrate the comparison of structure variables.

The program shown in Fig. 12.2 illustrates how a structure variable can be copied into another of the same type. It also performs memberwise comparison to decide whether two structure variables are identical.

# 12.6 ARRAYS OF STRUCTURES

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