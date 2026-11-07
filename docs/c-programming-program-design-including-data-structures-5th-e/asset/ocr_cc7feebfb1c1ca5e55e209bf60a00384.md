copies the contents of `newStudent` into `student`. After this assignment statement executes, the values of `student` are as shown in Figure 10-4.

![](bbox=[0.204, 0.173, 0.889, 0.393])

**FIGURE 10-4** `student` after `student = newStudent`

In fact, the assignment statement:

```
student = newStudent;
```

is equivalent to the following statements:

```
student.firstName = newStudent.firstName;
student.lastName = newStudent.lastName;
student.courseGrade = newStudent.courseGrade;
student.testScore = newStudent.testScore;
student.programmingScore = newStudent.programmingScore;
student.GPA = newStudent.GPA;
```

# Comparison (Relational Operators)

To compare `struct` variables, you compare them member-wise. As with an array, no aggregate relational operations are performed on a `struct`. For example, suppose that `newStudent` and `student` are declared as shown earlier. Furthermore, suppose that you want to see whether `student` and `newStudent` refer to the same student. Now `newStudent` and `student` refer to the same student if they have the same first name and the same last name. To compare the values of `student` and `newStudent`, you must compare them member-wise, as follows:

```
if (student.firstName == newStudent.firstName &&
    student.lastName == newStudent.lastName)
.
.
.
```