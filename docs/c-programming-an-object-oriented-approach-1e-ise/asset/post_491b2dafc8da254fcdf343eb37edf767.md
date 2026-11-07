
In line 22 of Program 16.15, we take the address of a variable of type int, interpret it as a pointer to character, and write its contents, as characters, to the file. We do the same in line 23, but the variable is of type double.

In line 35, we take the address of a variable of type int, interpret the location reserved in memory as a pointer to character, and store characters extracted from the file in it. We do the same in line 36, but the location is of type double.

Note that in both cases (reading and writing), we interpret the address of a fundamental data type as a pointer to characters.

## Conversion of User-Defined Objects

The conversion can be performed because an object of a fundamental data type is stored in memory as a sequence of bits (or bytes). The only thing we must do is change the read/write function to access a variable of type class instead of a variable of a fundamental data type.

When reading, we need an empty object (created from a default constructor) to be filled by characters from the file. When we write, we need a filled object (created from the parameter constructor) to be changed to characters and written to the file as shown below:

```cpp
istream& read (reinterpret_cast <char*> (&object), sizeof (class))
ostream& write (reinterpret_cast <char*> (&object), sizeof (class))
```

We can create a class representing information about a student (identity, name, and GPA) and write the instances of the class to a file and then read the instances from the file. We show the interface, implementation, and the application files next. Program 16.16 shows the interface file.

### Program 16.16 File student.h

```cpp
/**********************************************************
 * The program defines the interface file for the Student class
 * to be used to store student records in a binary file
 **********************************************************/
#ifndef STUDENT_H
#define STUDENT_H
#include <iostream>
#include <fstream>
#include <cassert>
#include <iomanip>
#include <cstring>
#include <string>
using namespace std;

class Student
{
private:
   int stdId;
   char stdName [20];
   double stdGpa;
public:
    Student(int, const string&, double);
    Student();
    ~Student();
    int getId() const;
    string getName() const;
    double getGpa() const;
};
#endif
```

Program 16.17 shows the implementation file for the student class. Note that we use the accessor functions to get the value of the data members, but we could have overloaded the insertion operator for the class.

### Program 16.17 File student.cpp

```cpp
/******************************************************
 * The implementation file for Student class
 ******************************************************/
#include "student.h"

// Parameter Constructor
Student::Student(int id, const string& name, double gpa)
: stdId(id), stdGpa(gpa)
{
    strcpy(stdName, name.c_str());
    if (stdId < 1 || stdId > 99)
    {
        cout << "Identity is out of range. Program aborted.";
        assert(false);
    }
    if (stdGpa < 0.0 || stdGpa > 4.0)
    {
        cout << "The gpa value is out of range. Program aborted.";
        assert(false);
    }
}

// Default Constructor
Student::Student()
{
}

// Destructor
Student::~Student()
{
}

// Accessor function
int Student :: getId() const
{
    return stdId;
}

// Accessor function
string Student :: getName() const
{
    return stdName;
}

// Accessor function
double Student :: getGpa() const
{
    return stdGpa;
}
```

Program 16.18 shows the application file for writing and reading objects to a file. We first change several objects to binary data and write them to the file. We then open the same file and read student objects one after another.

### Program 16.18 File app.cpp

```cpp
/**************************************************************
* The application file to write students record to a binary   *
* file and then read the records sequentially                  *
**************************************************************/
#include "student.h"

int main()
{
    // Opening File.dat for binary output
    fstream stdStrm1;
    stdStrm1.open ("File.dat", ios :: binary | ios :: out);
    if (!stdStrm1.is_open())
    {
        cout << "File.dat cannot be opened for writing!";
        assert (false);
    }

    // Instantiation of five objects
    Student std1 (1, "John", 3.91);
    Student std2 (2, "Mary", 3.82);
    Student std3 (3, "Lucie", 4.00);
    Student std4 (4, "Edward", 3.71);
    Student std5 (5, "Richard", 3.85);

    // Writing the five objects to the binary file and close it
    stdStrm1.write(reinterpret_cast<char*>( &std1), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std2), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std3), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std4), sizeof(Student));
    stdStrm1.write(reinterpret_cast<char*>( &std5), sizeof(Student));
    stdStrm1.close();

    // Opening file.dat for input
    fstream stdStrm2;
    stdStrm2.open("File.dat", ios :: binary | ios :: in);
    if (!stdStrm2.is_open())
    {
        cout << "File.dat cannot be opened for reading!";
        assert (false);
    }

    // Read Student objects, display them, and close the File.data
    cout << left << setw (4) << "ID" << " ";
    cout << setw (15) << left << "Name" << " ";
    cout << setw (4) << "GPA" << endl;

    Student std;
    for (int i = 0; i < 5; i++)
    {
        stdStrm2.read(reinterpret_cast<char*>( &std), sizeof(Student));
        cout << setw (4) << std.getId() << " ";
        cout << setw (15) << left << std.getName() << " ";
        cout << fixed << setw (4) << setprecision (2) << std.getGpa();
        cout << endl;
    }

    stdStrm2.close();
    return 0;
}
```

| ID | Name    | GPA |
|---:|---------|----:|
| 1  | John    | 3.91 |
| 2  | Mary    | 3.82 |
| 3  | Lucie   | 4.00 |
| 4  | Edward  | 3.71 |
| 5  | Richard | 3.85 |

## Random Access

We can also read from or write to binary files randomly. In other words, instead of reading the record of all students, we can read the record of a specific student using her identity. However, this involves two precautions.

First, we must be sure that all of the objects stored in the file are of the same size so we can use the `seekg()` and `seekp()` functions. In the case of the object with only data members of fundamental data types, the size of each object is the sum of the size of its data members. In the case of the `Student` class, the size of array representing the name is also fixed.

Second, we must use some precautions to find the location of the object, given some information about it. For example, we can use the identity of a student in the previous example to find the location of the Student object using:

```cpp
seekg ((id − 1) * sizeof (Student))
```

But if the identity does not start from 1, we must transform the identity to the student record number.

## 16.4 STRING STREAMS

String streams use three classes: *istringstream*, *ostringstream*, and *stringstream*. These classes are used to input data from or output data to strings. They are inherited, respectively, from *istream*, *ostream*, and *iostream*. With a couple of exceptions, all member functions discussed in their superclasses can be used in these classes and can add more classes. String stream classes are defined in the `<sstream>` header file, which must be included in our program when we use them.

> To use string streams, we need the `<sstream>` header file.

The source or destination of string streams is different from that of console streams or file streams. In console streams, the source or destination is a physical device outside the program. In file streams, the source or destination is a file, an entity that exists outside the program. In string streams, the source or destination is in fact a string inside the program itself. In other words, we read from an existing string in the program; we write to a string in the program. For the sake of clarity, in the figures we use in this section, we show the source or sink as a string outside the program, but we must remember that it is part of the program.

We cannot open or close these streams because the source or sink entities connected to these streams are not external; they are created and destroyed inside our programs. For this reason, there are no *open()* or *close()* functions for these streams.

> The *open()* and *close()* functions are not defined for string streams.

### 16.4.1 Instantiation

Similar to file streams, each string stream is instantiated using constructors. We show the constructors for the *istringstream*, *ostringstream*, and *stringstream* classes in Table 16.11; we show the default values for the open modes.

Each constructor instantiates an object of type *istringstream*, *ostringstream*, or *stringstream* and connects the object to the string object defined as the first parameter. Note that a string object must be included, but it can be a null string.
