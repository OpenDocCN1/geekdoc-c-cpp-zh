The class average is equal to the sum of the grades divided by the number of students. The algorithm for solving this problem on a computer must input each of the grades, calculate the average and print the result.

# Pseudocode Algorithm with Counter-Controlled Repetition

Let’s use pseudocode to list the actions to execute and specify the order in which these actions should occur. We use **counter-controlled repetition** to input the grades one at a time. This technique uses a variable called a **counter** to control the number of times a group of statements will execute (also known as the number of **iterations** of the loop).

Counter-controlled repetition is often called **definite repetition** because the number of repetitions is known *before* the loop begins executing. In this example, repetition terminates when the counter exceeds 10. This section presents a fully developed pseudocode algorithm (Fig. 4.7) and a version of class GradeBook (Fig. 4.8–Fig. 4.9) that implements the algorithm in a C++ member function. The section then presents an application (Fig. 4.10) that demonstrates the algorithm in action. In Section 4.9 we demonstrate how to use pseudocode to develop such an algorithm from scratch.

![](bbox=[0.159, 0.407, 0.217, 0.453])

> **Software Engineering Observation 4.3**
> 
> *Experience has shown that the most difficult part of solving a problem on a computer is developing the algorithm for the solution. The process of producing a working C++ program from the algorithm is typically straightforward.*

```
```text
 1  Set total to zero
 2  Set grade counter to one
 3
 4  While grade counter is less than or equal to ten
 5      Prompt the user to enter the next grade
 6      Input the next grade
 7      Add the grade into the total
 8      Add one to the grade counter
 9
10  Set the class average to the total divided by ten
11  Print the total of the grades for all students in the class
12  Print the class average
```
```

**Fig. 4.7**  Pseudocode for solving the class average problem with counter-controlled repetition.

Note the references in the pseudocode algorithm of Fig. 4.7 to a total and a counter. A **total** is a variable used to accumulate the sum of several values. A **counter** is a variable used to count—in this case, the grade counter indicates which of the 10 grades is about to be entered by the user. Variables used to store totals are normally initialized to zero before being used in a program; otherwise, the sum would include the previous value stored in the total’s memory location.

# Enhancing GradeBook Validation

Let’s consider an enhancement we made to class GradeBook. In Fig. 3.16, our setCourseName member function validated the course name by testing whether the course name’s