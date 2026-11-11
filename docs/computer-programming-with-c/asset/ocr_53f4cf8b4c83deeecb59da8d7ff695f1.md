![](bbox=[0.245, 0.111, 0.733, 0.339])

Remember, we are in a scope of object s1, and hence, the members m1, m2, and m3 of the mark sheet of student object s1 will be taken as input from the user due to this statement.

Similarly, the statement

```
s2.inputStud();
```

will accept roll_no, name and marks of object s2 as input from the user. Assuming the sample input values, state of objects s1 and s2 is as shown in Figure 11.50.

The statement

```
s1.outputStud();
```

invokes outputStud() method to print the details of student s1 on computer screen. Before printing the data, it calculates total marks of the student, using the statement

```
total = marks.m1+marks.m2+marks.m3;
```

Note that, we have directly accessed private members m1, m2 and m3 of class MarkSheet in the scope of method outputStud(). This is possible because we have created class Student as a friend class of class MarkSheet as seen in the code. The function prints the value of members roll_no, name, and total and also invokes printMarks() of MarkSheet class to print the individual marks obtained by the student. Similarly, the statement

```
s2.outputStud();
```

prints the details of Student object s2 on computer screen

> > **NOTES**
> >
> > We have invoked the functions `inputMarks()` and `printMarks()` of class MarkSheet from class Student. We know that the functions of class MarkSheet must be invoked using its object. Hence both the functions are invoked using object `marks` (which is a member of class Student) as shown below
> >
> > ```cpp
> > marks.inputMarks();
> > marks.printMarks();
> > ```