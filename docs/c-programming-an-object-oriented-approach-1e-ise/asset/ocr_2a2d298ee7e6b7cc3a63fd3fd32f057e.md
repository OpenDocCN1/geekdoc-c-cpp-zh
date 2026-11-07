# Program 19.15   Handling a set of integers (Continued)

```
    48   iter2--;
    50   cout << "Element before 20: " << *iter2 << endl;
    51   return 0;
    52 }
    Run:
    Printing set elements from smallest to largest.
      12 18 20 24 47 52 53 77 87 92 98

    Printing set elements from largest to smallest.
      98 92 87 77 53 52 47 24 20 18 12

    Element after 52: 53
    Element before 20: 18
```

operator for the Student class so we can list students according to their student identifica-
tion (Program 19.16, Program 19.17, and Program 19.18).
    Program 19.16 shows the interface file for the Student set.

# Program 19.16   The interface file (student.h)

```
    1  /************************************************************
    2   * The interface file for the Student class                  *
    3   ************************************************************/
    4  #ifndef STUDENT_H
    5  #define STUDENT_H
    6  #include <string>
    7  #include <set>
    8  #include <iostream>
    9  #include <iomanip>
    10 using namespace std;
    11
    12 class Student
    13 {
    14    private:
    15        int identity ;
    16        string name;
    17        double gpa;
    18    public:
    19        Student(int identity, string name, double gpa);
    20        ~Student();
    21        void print() const;
    22        bool friend operator<(const Student& left, const Student& right);
    23 };
    24 #endif
```