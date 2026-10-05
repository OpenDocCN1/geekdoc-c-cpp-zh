# 510 Introduction to C++

reads the data of a student, saves it to the corresponding members of an object, and displays it on the screen. The typical practice is to put the class declaration in a header file, which is usually named the same as the name of the class. The implementation of the member functions is placed in one or more code files that make #include the header file. Separating the class declaration from the implementation makes the code easier to read and maintain. Let's see the two files:

```
// student.h
#ifndef STUDENT_H
#define STUDENT_H

#include <string>

class Student {
private:
    int code;
public:
    std::string name;
    float grd;

    void set(int c) {code = c};
    void show();
};
endif
```

and then include that file in the source file.

```
// student.cpp
#include <iostream> // Example 17.1
#include "student.h"
using std::cin;
using std::cout;

void Student::show() {
    cout << "N:" << name << "C:" << code << "G:" << grd << '\n';
}

int main() {
    int code;
    Student s; /* s is an object of the class Student. It is not necessary to add the word class. */

    cout << "Name: ";
    getline(cin, s.name);

    cout << "Grade: ";
    cin >> s.grd;

    cout << "Code: ";
    cin >> code;
    s.set(code);
    s.show();
    return 0;
}
```