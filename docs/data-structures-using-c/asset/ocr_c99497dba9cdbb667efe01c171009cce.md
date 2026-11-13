# User-defined Data Types

Suppose we want to maintain a record of 100 students with the following fields in each record: roll number, name of student, and percentage of marks of the students. Then we use the C++ class as follows:

```
```cpp
class Student
{
private:
    int roll;
    char name[20];
    float percentage;
public:
    void GetRecord();
    void PrintRecord();
    void SearchRecord();
}
```
```

Class, structure, and union are the user-defined data types in C++.

# 1.3.3 Data Object

A data object represents a container for data values—a place where data values may be stored and later retrieved. A data object is characterized by a set of attributes, one of the most important of which is its data type. The attributes determine the number and type of values that the data object may contain and also determine the logical organization of these values.

A data object is nothing but a set of elements, say D. The data object 'alphabets' can be defined as D = {A, B, ..., Z, a, b, ..., z} and the data object 'integers' as D = {..., -3, -2, -1, 0, 1, 2, 3, ...}. The data object set may be finite or infinite.

A data object is a run-time instance of data structures. It is the run-time grouping of one or more data pieces. Some of the data objects that exist during program execution are programmer-defined, such as variables, constants, arrays, and files. The programmer explicitly creates and manipulates these data objects through declarations and statements in the program. System-defined data objects are ordinarily generated automatically as needed during program execution without explicit specification by the programmer.

# 1.3.4 Data Structure

Data structures refer to data and representation of data objects within a program, that is, the implementation of structured relationships. A data structure is a collection of atomic and composite data types into a set with defined relationships. By structure, we mean a set of rules that holds the data together. In other words, if we take a combination of data types and fit them into a structure such that we can define the relating rules, we can have data structures that consist of other data structures too.