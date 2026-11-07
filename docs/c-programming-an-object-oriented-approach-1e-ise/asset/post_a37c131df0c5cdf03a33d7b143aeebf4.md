
![](img/d68f6199646ca63591a6d8419e0ed4ba_555_0.png)

Figure 11.28 Sequence diagram for the registrar project

is created by the *course* object, and the schedule object is created by the *student* object. The *registrar*, *course*, and *student* objects are created by *main*. We show the case for one single student and one single course to make the diagram simpler.

## Programs

Program 11.32 is the interface file. Program 11.33 is the implementation file.

### Program 11.32 File courseRoster.h

```cpp
/**********************************************************************
 * The interface file for the class CourseRoster                       *
 **********************************************************************/
#ifndef COURSEROSTER_H
#define COURSEROSTER_H
6  #include <string>
7  #include <iostream>
8  #include <cassert>
9  using namespace std;
10
11 // Class Definition
12 class CourseRoster
13 {
14   private:
15     int size;
16     string* stdNames;
17   public:
18     CourseRoster ();
19     ~CourseRoster();
20     void addStudent (string studentName);
21     void print () const;
22 };
23 #endif
```

### Program 11.33 File courseRoster.cpp

```cpp
1 /*************************************************************
2  * The implementation file for class CourseRoster            *
3  *************************************************************/
4 #include "courseRoster.h"
5
6 // Constructor
7 CourseRoster :: CourseRoster ()
8  :size (0)
9 {
10     stdNames = new string [20];
11 }
12 // Destructor
13 CourseRoster :: ~CourseRoster ()
14 {
15     delete [] stdNames;
16 }
17 // Definition of addStudent function
18 void CourseRoster :: addStudent (string studentName)
19 {
20     stdNames [size] = studentName;
21     size++;
}
// Definition of print function
void CourseRoster::print() const
{
    cout << "List of Students" << endl;
    for (int i = 0; i < size; i++)
    {
        cout << stdNames[i] << endl;
    }
    cout << endl;
}
```

## Class Course

Program 11.34 is the interface file. Program 11.35 is the implementation file.

### Program 11.34 File course.h

```cpp
/************************************************************
 * The interface file for the class Course                 *
 ************************************************************/
#ifndef COURSE_H
#define COURSE_H
#include <cassert>
#include <string>
#include <iostream>
#include "courseRoster.h"
using namespace std;

// Class Definition
class Course
{
private:
    string name;
    int units;
    CourseRoster* roster;
public:
    Course (string name, int units);
    ~Course();
    string getName() const;
    CourseRoster* getRoster() const;
    void addStudent (string name);
    void print () const;
};
#endif
```

### Program 11.35 File course.cpp

```cpp
/*****************************************************
 * The implementation file for the class Course
 *****************************************************/
#include "course.h"

// Constructor
Course :: Course (string nm, int ut)
: name (nm), units (ut)
{
    roster = new CourseRoster;
}
// Destructor
Course :: ~Course ()
{
}
// Definition of getName function
string Course :: getName() const
{
    return name;
}
// Definition of addStudent function
void Course :: addStudent (string name)
{
    roster -> addStudent (name);
}
// Definition of getRoster function
CourseRoster* Course :: getRoster () const
{
    return roster;
}
// Definition of print function
void Course :: print () const
{
    cout << "Course Name: " << name << endl;
    cout << "Number of Units: " << units << endl;
    roster -> print ();
}
```

## StudentSchedule Class

Program 11.36 is the interface file.

### Program 11.36 File studentSchedule.h

```cpp
/*************************************************************
 * The interface file for the class StudentSchedule           *
 *************************************************************/
#ifndef STUDENTSCHEDULE_H
#define STUDENTSCHEDULE_H
#include <string>
#include <iostream>
#include <cassert>
using namespace std;

// Class Definition
class StudentSchedule
{
   private:
      int size;
      string* courseNames;
   public:
      StudentSchedule ();
      ~StudentSchedule();
      void addCourse (string course);
      void print () const;
};
#endif
```

Program 11.37 is the implementation file.

### Program 11.37 File studentSchedule.cpp

```cpp
/*************************************************************
 * The implementation file for the class StudentSchedule     *
 *************************************************************/
#include "studentSchedule.h"

// Constructor
StudentSchedule :: StudentSchedule ()
:size (0)
{
   courseNames = new string [5];
}
// Destructor
StudentSchedule :: ~StudentSchedule()
{
    delete[] courseNames;
}
// Definition of addCourse function
void StudentSchedule::addCourse (string name)
{
    courseNames[size] = name;
    size++;
}
// Definition of print function
void StudentSchedule::print () const
{
    cout << "List of Courses" << endl;
    for (int i = 0; i < size; i++)
    {
        cout << courseNames[i] << endl;
    }
    cout << endl;
}
```

Program 11.38 is the interface file.

### Program 11.38 File student.h

```cpp
/************************************************************
 * The interface file for the class Student                 *
 ************************************************************/
#ifndef STUDENT_H
#define STUDENT_H
#include <cassert>
#include <string>
#include <iostream>
#include "studentSchedule.h"
using namespace std;

// Class Definition
class Student
{
private:
    string name;
    StudentSchedule* schedule;
public:
    Student (string name);
    ~Student();
    string getName () const;
    StudentSchedule* getSchedule () const;
    void addCourse (string name);
    void print () const;
};
#endif
```

Program 11.39 is the implementation file.

### Program 11.39 File student.cpp

```cpp
/************************************************************
 * The implementation file for the class Student             *
 ************************************************************/
#include "student.h"

// Constructor
Student :: Student (string nm)
: name (nm)
{
    schedule = new StudentSchedule;
}
// Destructor
Student :: ~Student ()
{
}
// Definition of getName function
string Student :: getName () const
{
    return name;
}
// Definition of getSchedule function
StudentSchedule* Student :: getSchedule () const
{
    return schedule;
}
// Definition of addCourse function
void Student :: addCourse (string name)
{
    schedule -> addCourse (name);
}
// Definition of print function
void Student :: print () const
{
    cout << "Student name: " << name << endl;
    schedule -> print();
}
```

### Program 11.40 File registrar.h

```cpp
/************************************************************
 * The interface file for the class Registrar                 *
 ************************************************************/
#ifndef REGISTRAR_H
#define REGISTRAR_H
#include "course.h"
#include "student.h"

// Class Definition
class Registrar
{
   public:
      Registrar();
      ~Registrar();
      void enroll (Student student, Course course);
};
#endif
```

Program 11.40 is the interface file.
Program 11.41 is the implementation file.
Program 11.42 is the application file. Note that the application creates one registrar object. In Chapter 20, we learn how to control the Registrar object so that it is unique.

### Program 11.41 File registrar.cpp

```cpp
/************************************************************
 * The implementation file for the class Registrar           *
 ************************************************************/
#include "registrar.h"

// Constructor
Registrar :: Registrar ()
{
}
// Destructor
Registrar :: ~Registrar ()
{
}
// Enroll function
void Registrar :: enroll (Student student, Course course)
{
   (course.getRoster ()) -> addStudent (student.getName());
   (student.getSchedule()) -> addCourse (course.getName());
}
```
