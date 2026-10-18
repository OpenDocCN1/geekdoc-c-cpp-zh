# DISPLAY 7.14 Two-Dimensional Array *(part 1 of 3)*

```
```cpp
1  //Reads quiz scores for each student into the two-dimensional array grade (but
2  //the input code is not shown in this display). Computes the average score
3  //for each student and the average score for each quiz. Displays the quiz scores
4  //and the averages.
5  #include <iostream>
6  #include <iomanip>
7  const int NUMBER_STUDENTS = 4, NUMBER_QUIZZES = 3;
8
9  void computeStAve(const int grade[][NUMBER_QUIZZES], double stAve[]);
10 //Precondition: Global constants NUMBER_STUDENTS and NUMBER_QUIZZES
11 //are the dimensions of the array grade. Each of the indexed variables
12 //grade[stNum - 1, quizNum - 1] contains the score for student stNum on quiz
13 //quizNum.
14 //Postcondition: Each stAve[stNum - 1] contains the average for student
15 //number stNum.
16
17 void computeQuizAve(const int grade[][NUMBER_QUIZZES], double quizAve[]);
18 //Precondition: Global constants NUMBER_STUDENTS and NUMBER_QUIZZES
19 //are the dimensions of the array grade. Each of the indexed variables
20 //grade[stNum - 1, quizNum - 1] contains the score for student stNum on quiz
21 //quizNum.
22 //Postcondition: Each quizAve[quizNum - 1] contains the average for quiz number
23 //quizNum.
24
25 void display(const int grade[][NUMBER_QUIZZES],
26              const double stAve[], const double quizAve[]);
27 //Precondition: Global constants NUMBER_STUDENTS and NUMBER_QUIZZES are the
28 //dimensions of the array grade. Each of the indexed variables grade[stNum - 1,
29 //quizNum - 1] contains the score for student stNum on quiz quizNum. Each
30 //stAve[stNum - 1] contains the average for student stNum. Each
31 //quizAve[quizNum - 1] contains the average for quiz number quizNum.
32 //Postcondition: All the data in grade, stAve, and quizAve has been output.
33
34 int main( )
35 {
36     using namespace std;
37     int grade[NUMBER_STUDENTS][NUMBER_QUIZZES];
38     double stAve[NUMBER_STUDENTS];
39     double quizAve[NUMBER_QUIZZES];
40
    <The code for filling the array grade goes here, but is not shown.>
```
```

*(continued)*