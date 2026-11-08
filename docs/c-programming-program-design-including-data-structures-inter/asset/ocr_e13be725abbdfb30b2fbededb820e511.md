```
```cpp
int testScore;
int programmingScore;
double GPA;
};
```
```

```
```cpp
//variables
studentType newStudent;
studentType student;
```
```

Suppose you want to initialize the member GPA of newStudent to 0.0. The following statement accomplishes this task:

```
```cpp
newStudent.GPA = 0.0;
```
```

Similarly, the statements:

```
```cpp
newStudent.firstName = "John";
newStudent.lastName = "Brown";
```
```

store "John" in the member firstName and "Brown" in the member lastName of newStudent.

After the preceding three assignment statements execute, newStudent is as shown in Figure 9-2.

![](bbox=[0.123, 0.482, 0.951, 0.703])

**FIGURE 9-2** struct newStudent

The statement:

```
```cpp
cin >> newStudent.firstName;
```
```