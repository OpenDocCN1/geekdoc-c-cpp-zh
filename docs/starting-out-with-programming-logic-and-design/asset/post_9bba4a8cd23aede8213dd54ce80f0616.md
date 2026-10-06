
# Chapter 5 Repetition Structures

Figure 5-21 Flowchart for a clock simulator

![](img/c939132f78787c7f339c6977b3fc8c85_242_0.png)

## 5.6 Nested Loops

The simulated clock example brings up a few points about nested loops:

- An inner loop goes through all of its iterations for every single iteration of an outer loop.
- Inner loops complete their iterations faster than outer loops.
- To get the total number of iterations of a nested loop, multiply the number of iterations of all loops.

Program 5-20 shows another example in pseudocode. It is a program that a teacher might use to get the average of each student's test scores. The statement in line 13 gets the number of tests per student. The For loop that begins in line 20 iterates for each student. The nested loop, in line 27 through 31, iterates for each test score.

## Program 5-20

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

## Program Output (with Input Shown in Bold)

How many students do you have?
3 [Enter]
How many test scores per student?
3 [Enter]

```
Student number 1
-----------------
Enter test number 1:
100 [Enter]
Enter test number 2:
95 [Enter]
Enter test number 3:
90 [Enter]
The average for student number 1 is 95.0
```

```
Student number 2
-----------------
Enter test number 1:
80 [Enter]
Enter test number 2:
81 [Enter]
Enter test number 3:
82 [Enter]
The average for student number 2 is 81.0
```

```
Student number 3
-----------------
Enter test number 1:
75 [Enter]
Enter test number 2:
85 [Enter]
Enter test number 3:
80 [Enter]
The average for student number 3 is 80.0
```

## Review Questions

### Multiple Choice

- 1. A ________controlled loop uses a true/false condition to control the number of times that it repeats.
  a. Boolean
  b. condition
  c. decision
  d. count

- 2. A ________controlled loop repeats a specific number of times.
  a. Boolean
  b. condition
  c. decision
  d. count

- 3. Each repetition of a loop is known as a(n) _________.
  a. cycle
  b. revolution
  c. orbit
  d. iteration

- 4. The While loop is a ________ type of loop.
  a. pretest
  b. posttest
  c. prequalified
  d. post iterative

- 5. The Do-While loop is a ________ type of loop.
  a. pretest
  b. posttest
  c. prequalified
  d. post iterative

- 6. The For loop is a ________ type of loop.
  a. pretest
  b. posttest
  c. prequalified
  d. post iterative

- 7. A(n) ________ loop has no way of ending and repeats until the program is interrupted.
  a. indeterminate
  b. interminable
  c. infinite
  d. timeless

- 8. A ________ loop always executes at least once.
  a. pretest
  b. posttest
  c. condition-controlled
  d. count-controlled

- 9. A(n) ________ variable keeps a running total.
  a. sentinel
  b. sum
  c. total
  d. accumulator

- 10. A(n) ________ is a special value that signals when there are no more items from a list of items to be processed. This value cannot be mistaken as an item from the list.
  a. sentinel
  b. flag
  c. signal
  d. accumulator

### True or False

A condition-controlled loop always repeats a specific number of times.

- 1. The While loop is a pretest loop.
2. The Do-While loop is a pretest loop.
3. You should not write code that modifies the contents of the counter variable in the body of a For loop.
4. You cannot display the contents of the counter variable in the body of a loop.
5. It is not possible to increment a counter variable by value other than 1.
6. The following statement declares the variable x: Set x = x - 1.
7. It is not necessary to initialize accumulator variables.
8. In a nested loop, the inner loop goes through all of its iterations for every iteration of the outer loop.
9. To calculate the total number of iterations of a nested loop, add the number of iterations of all loops.

### Short Answer

- 1. Why should you indent the statements in the body of a loop?
2. Describe the difference between pretest loops and posttest loops.
3. What is a condition-controlled loop?
4. What is a count-controlled loop?
5. What actions do count-controlled loops typically perform using the counter variable?
6. What is an infinite loop? Write the code for one.
7. A For loop looks like what other loop?
8. Why is it critical to initialize accumulator variables?
9. What is the advantage of using a sentinel?
10. Why must the value chosen for sentinel be carefully selected?

### Algorithm Workbench

- 1. Design a loop that lets the user enter a number. The number should be multiplied by 10 and stored in a variable named product. The loop should iterate as long as product contains a value less than 100.
2. Design a Do-While loop that asks the user to enter two numbers. The numbers should be added and displayed. The loop should ask the user whether they wish to perform the operation again; if so, the loop should repeat; otherwise, it terminates.
3. Design a For loop that displays the following set of numbers: 0, 10, 20, 30, 40, ..., 100.
4. Design a loop that asks the user to enter a number. The loop should iterate 10 times and keep a running total of the numbers entered.
5. Design a For loop that calculates the total of the following series of numbers: 30 + 29 + 28 + ... + 1.
6. Design a nested loop that displays 10 rows of characters. There should be 15 characters in each row.
7. Convert the While loop to a Do-While loop:
   Declare Integer x = 1
   While x > 0
       Display "Enter a number."
       Input x
8. Convert the Do-While loop in the following code to a While loop:
   Declare String sure
   Do
       Display "Are you sure you want to quit?"
       Input sure
   While sure != "Y" AND sure != "y"
9. Convert the While loop to a For loop:
   Declare Integer count = 0
   While count < 50
       Display "The count is ", count
       Set count = count + 1
10. Convert the For loop to a While loop:
    Declare Integer count
    For count = 1 To 50
        Display count

### Debugging Exercises

- 1. Find the error in the following pseudocode:
   Declare Boolean finished = False
   Declare Integer value, cube
   While NOT finished
       Display "Enter a value to be cubed."
       Input value
       Set cube = value^3
       Display value, " cubed is ", cube
- 2. The programmer intended the following pseudocode to display the numbers 1 through 60, and then display the message "Time’s up!" It will not function as intended, however. Find the error.
   Declare Integer counter = 1
   Const Integer TIME_LIMIT = 60
   ```
   While counter < TIME_LIMIT
       Display counter
       Set counter = counter + 1
   End While
   Display "Time's up!"
   ```
- 3. The programmer intended the following pseudocode to get sum of five sets of numbers, calculate the sum of each set, and calculate the sum of all the numbers entered. It will not function as intended, however. find the error.

### Programming Exercises

- 1. **Bug Collector**: A bug collects bugs every day for seven days. Design a program that keeps a running total of the number of bugs collected during the seven days. The loop should ask for the number of bugs collected for each day, and when the loop is finished, the program should display the number of bugs collected.
- 2. **Calories Burned**: Running on a particular treadmill will burn 3.9 calories per minute. Design a program that uses a loop to display the number of calories burned after 10, 15, 20, 25, and 30 minutes.
- 3. **Budget Analysis**: Design a program that asks the user to enter the amount he or she has budget. A loop should prompt the user to enter each of or or her expenses for the month, and keep a running total. When the loop finishes, the program should display the amount that is over or under budget.
- 4. **Sum of Numbers**: Design a program with a loop that asks the user to enter a set of positive numbers. The user should enter a negative number to signal the end of the series. After all the positive numbers have been entered, the program should display their sum.

![](img/c939132f78787c7f339c6977b3fc8c85_248_0.png)
