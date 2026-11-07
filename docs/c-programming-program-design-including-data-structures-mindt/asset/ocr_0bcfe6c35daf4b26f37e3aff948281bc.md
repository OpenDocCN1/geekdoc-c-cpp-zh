In fact, the assignment statement:

```
```cpp
student = newStudent;
```
```

is equivalent to the following statements:

```
```cpp
student.firstName = newStudent.firstName;
student.lastName = newStudent.lastName;
student.courseGrade = newStudent.courseGrade;
student.testScore = newStudent.testScore;
student.programmingScore = newStudent.programmingScore;
student.GPA = newStudent.GPA;
```
```

# Comparison (Relational Operators)

To compare `struct` variables, you compare them member-wise. As with an array, no aggregate relational operations are performed on a `struct`. For example, suppose that `newStudent` and `student` are declared as shown earlier. Furthermore, suppose that you want to see whether `student` and `newStudent` refer to the same student. Now `newStudent` and `student` refer to the same student if they have the same first name and the same last name. To compare the values of `student` and `newStudent`, you must compare them member-wise, as follows:

```
```cpp
if (student.firstName == newStudent.firstName &&
    student.lastName == newStudent.lastName)
```
```

+   - .
+   - .
+   - .

Although you can use an assignment statement to copy the contents of one `struct` into another `struct` of the same type, you cannot use relational operators on `struct` variables. Therefore, the following would be illegal:

```
```cpp
if (student == newStudent)    //illegal
```
```

+   - .
+   - .

# Input/Output

No aggregate input/output operations are allowed on a `struct` variable. Data in a `struct` variable must be read one member at a time. Similarly, the contents of a `struct` variable must be written one member at a time.

We have seen how to read data into a `struct` variable. Let us now see how to output a `struct` variable. The statement: