The following statements illustrate how to use variables of type string to read the names of the input/output files during program execution and open those files:

```
```cpp
ifstream infile;
string fileName;

cout << "Enter the input file name: ";
cin >> fileName;

infile.open(fileName.c_str());    //open the input file
```
```

Of course, you must also include the header file string in the program. The output file has similar conventions.

# # Parallel Arrays

Two (or more) arrays are called **parallel** if their corresponding components hold related information.

Suppose you need to keep track of students’ course grades, together with their ID numbers, so that their grades can be posted at the end of the semester. Further, suppose that there is a maximum of 50 students in a class and their IDs are 5 digits long. Because there may be 50 students, you need 50 variables to store the students’ IDs and 50 variables to store their grades. You can declare two arrays: studentId of type int and courseGrade of type char. Each array has 50 components. Furthermore, studentId[0] and courseGrade[0] will store the ID and course grade of the first student, studentId[1] and courseGrade[1] will store the ID and course grade of the second student, and so on.

The statements:

```
```
int studentId[50];
char courseGrade[50];
```
```

declare these two arrays.

Suppose you need to input data into these arrays, and the data is provided in a file in the following form:

```
```
studentId courseGrade
```
```

For example, a sample data set is:

```
```
23456 A
86723 B
22356 C
32733 B
11892 D
.
.
.
```
```

Suppose that the input file is opened using the ifstream variable infile. Because the size of each array is 50, a maximum of 50 elements can be stored into each array. Moreover, it is possible that there may be fewer than 50 students in the class. Therefore,