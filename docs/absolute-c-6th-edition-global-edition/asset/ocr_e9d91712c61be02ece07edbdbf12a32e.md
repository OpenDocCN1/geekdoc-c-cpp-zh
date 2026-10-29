# EXAMPLE: (continued)

and so forth. The array quizAve will be used to record the average score for each quiz. For example, the program will set quizAve[0] equal to the average of all the student scores for quiz 1, quizAve[1] will record the average score for quiz 2, and so forth. Display 5.11 illustrates the relationship between the arrays grade, stAve, and quizAve. This display shows some sample data for the array grade. These data, in turn, determine the values that the program stores in stAve and in quizAve. Display 5.12 also shows these values, which the program computes for stAve and quizAve.

The complete program for filling the array grade and then computing and displaying both the student averages and the quiz averages is shown in Display 5.10. In that program we have declared array dimensions as global named constants. Since the procedures are particular to this program and cannot be reused elsewhere, we have used these globally defined constants in the procedure bodies, rather than having parameters for the size of the array dimensions. Since it is routine, the display does not show the code that fills the array.

# Display 5.10 Two-Dimensional Array (part 1 of 3)

```
1 //Reads quiz scores for each student into the two-dimensional array
2 //grade (but the input code is not shown in this display).
3 //Computes the average score for each student and the average score
4 //for each quiz. Displays the quiz scores and the averages.
5 #include <iostream>
6 #include <iomanip>
7 using namespace std;
8 const int NUMBER_STUDENTS = 4, NUMBER_QUIZZES = 3;
9 void computeStAve(const int grade[][NUMBER_QUIZZES], double stAve[]);
10 //Precondition: Global constants NUMBER_STUDENTS and NUMBER_QUIZZES
11 //are the dimensions of the array grade. Each of the indexed variables
12 //grade[stNum-1, quizNum-1] contains the score for student stNum on
13 //quiz quizNum.
14 //Postcondition: Each stAve[stNum-1] contains the average for student
15 //number stNum.
16 void computeQuizAve(const int grade[][NUMBER_QUIZZES],
17 double quizAve[]);
18 //Precondition: Global constants NUMBER_STUDENTS and NUMBER_QUIZZES
19 //are the dimensions of the array grade. Each of the indexed variables
20 //grade[stNum-1, quizNum-1] contains the score for student stNum on
21 //quiz quizNum.
22 //Postcondition: Each quizAve[quizNum-1] contains the average for
23 //quiz numbered quizNum.
```