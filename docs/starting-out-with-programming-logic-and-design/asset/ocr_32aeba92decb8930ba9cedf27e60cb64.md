# 5.6 Nested Loops 219

The simulated clock example brings up a few points about nested loops:

+   - An inner loop goes through all of its iterations for every single iteration of an outer loop.
- Inner loops complete their iterations faster than outer loops.
- To get the total number of iterations of a nested loop, multiply the number of iterations of all loops.

Program 5-20 shows another example in pseudocode. It is a program that a teacher might use to get the average of each student's test scores. The statement in line 13 gets the number of tests per student. The For loop that begins in line 20 iterates for each student. The nested loop, in line 27 through 31, iterates for each test score.

# Program 5-20

```
// This program averages test scores. It asks the user for the
// number of students and the number of test scores per student.
Declare Integer numStudents
Declare Integer numTestScores
Declare Integer total
Declare Integer student
Declare Integer testNum
Declare Real score
Declare Real average

// Get the number of students.
Display "How many students do you have?"
Input numStudents

// Get the number of test scores per student.
Display "How many test scores per student?"
Input numTestScores

// Determine each student's average test score.
For student = 1 To numStudents
// Initialize an accumulator for test scores.
Set total = 0

// Get the student's test scores.
Display "Student number ", student
Display ""
For testNum = 1 To numTestScores
Display "Enter test number ", testNum, ":"
Input score
Set total = total + score
// Calculate the average test score for this student.
Set average = total / numTestScores
// Display the average.
Display "The average for student ", student, " is ", average
Display
End For
```