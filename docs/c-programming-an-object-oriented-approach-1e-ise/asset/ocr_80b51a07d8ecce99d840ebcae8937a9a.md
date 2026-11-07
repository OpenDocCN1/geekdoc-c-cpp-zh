# **Program 9.17**  Implementation file (Continued)

```
```cpp
105    cout << right << students[i].score;
106    cout << setw (10) << right << students[i].grade;
107    cout << fixed << setw (20) << right << setprecision (2);
108    cout << showpoint << showpos;
109    cout << students[i].deviation << endl;
110 }
111 cout << "Average score: " << fixed << setw (4);
112 cout << setprecision (2) << averageScore << endl;
113 cout << "Standard Deviation: " << standardDeviation;
114 }
```
```

# **Program 9.18**  Application file

```
```cpp
1  /********************************************************************
2   * The application program is very simple. The user instantiates    *
3   * an object of the class and passes the number of students and     *
4   * name of the input file where the scores are stored.              *
5   * Everything is done by the constructor of the class.              *
6   ********************************************************************/
7  #include "course.h"
8
9  int main ( )
10 {
11     // Instantiation of the Course object
12     Course course (10, "scores.dat");
13     return 0;
14 }
```
```

**Run:**

| Identity | Score | Grade | Deviation |
|---|---:|:---:|---:|
| 1000 | 88 | B | +3.20 |
| 1001 | 100 | A | +15.20 |
| 1002 | 92 | A | +7.20 |
| 1003 | 77 | C | -7.80 |
| 1004 | 54 | F | -30.80 |
| 1005 | 82 | B | -2.80 |
| 1006 | 67 | D | -17.80 |
| 1007 | 95 | A | +10.20 |
| 1008 | 93 | A | +8.20 |
| 1009 | 100 | A | +15.20 |

Average score: +84.80

Standard Deviation: +4.51