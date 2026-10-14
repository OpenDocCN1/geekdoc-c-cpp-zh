```
}
void read_student_p(struct student student2)
{
gets(student2.name);
scanf("%d",&student2.marks);
```

# Explanation

+   1. The function read_student reads values in structures and returns the structure.

+   2. The function print_student takes the structure variable as input and prints the content in the structure.

+   3. The function read_student_p reads the data in the structure similarly to

read_student. It takes the structure student as an argument and puts the data in the structure. Since the data of a member of the structure is modified, you need not pass the structure as a pointer even though structure members are modified. Here you are not modifying the structure, but you are modifying the structure members through the structure.

# Self Assessment Questions

7. We cannot write a function that returns the structure. (True/False) 8. We can modify a member of the structure by passing the structure as a ________.

# 10.4 Arrays of Structures

We can use structures to describe the format of a number of related variables. For example, in analyzing the marks obtained by a class of students, we may use a template to describe student name and marks obtained in various