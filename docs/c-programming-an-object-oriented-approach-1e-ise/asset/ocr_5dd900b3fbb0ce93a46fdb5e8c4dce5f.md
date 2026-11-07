# Program 8.12  The application file for Student class (Continued)

```
```cpp
// Declaration of an array of Students using default constructors
Student students[5];
// Instantiation of five objects using parameter constructors
students[0] = Student("George", 82);
students[1] = Student("John", 73);
students[2] = Student("Luci", 91);
students[3] = Student("Mary", 72);
students[4] = Student("Sue", 65);
// Printing students' name, score, and grade
for (int i = 0; i < 5; i++)
{
    students[i].print();
}
return 0;
}
```
```

The following shows the separate compilation and running of the application program for creating and displaying students’ information.

```
```text
c++ -c students.cpp                 // Compilation of implementation file
c++ -c app.cpp                      // Compilation of application file
c++ -o application student.o app.o  // Linking of two compiled object files
application                         // Running the executable file

Run:
George        82        B
John          73        C
Luci          91        A
Mary          72        C
Sue           65        D
```
```

Although the approach may look more involved and uses more lines of code, it has the advantage that when the *Student* class is created, it can be used by any professor just by downloading the interface and the implementation. Each professor can customize her own application based on her need.

# 8.3 MULTIDIMENSIONAL ARRAYS

Some applications require that a set of values be arranged in a *multidimensional array*. The most common are two-dimensional arrays, but we may occasionally encounter three-dimensional arrays.

# 8.3.1 Two-Dimensional Arrays

A *two-dimensional array* defines a structured data type in which two indices are used to define the location of elements in rows and columns. The first index defines the row; the second index defines the column. Figure 8.13 shows a two-dimensional array, named *scores*, with five rows and three columns.