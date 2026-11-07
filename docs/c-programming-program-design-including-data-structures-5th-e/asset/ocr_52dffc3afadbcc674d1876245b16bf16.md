The `structVariableName.memberName` is just like any other variable. For example, `newStudent.courseGrade` is a variable of type `char`, `newStudent.firstName` is a string variable, and so on. As a result, you can do just about anything with `struct` members that you normally do with variables. You can, for example, use them in assignment statements or input/output (where permitted) statements.

In C++, the dot (`.`) is an operator called the **member access operator**.

Suppose you want to initialize the member GPA of `newStudent` to `0.0`. The following statement accomplishes this task:

```
newStudent.GPA = 0.0;
```

Similarly, the statements:

```
newStudent.firstName = "John";
newStudent.lastName = "Brown";
```

store `"John"` in the member `firstName` and `"Brown"` in the member `lastName` of `newStudent`.

After the preceding three assignment statements execute, `newStudent` is as shown in Figure 10-2.

![](bbox=[0.204, 0.482, 1.0, 0.701])

**FIGURE 10-2** *struct* `newStudent`

The statement:

```
cin >> newStudent.firstName;
```

reads the next string from the standard input device and stores it in:

```
newStudent.firstName
```

The statement:

```
cin >> newStudent.testScore >> newStudent.programmingScore;
```