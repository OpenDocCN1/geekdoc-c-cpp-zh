```
1  Initialize total to zero
2  Initialize counter to zero

4  Prompt the user to enter the first grade
5  Input the first grade (possibly the sentinel)

7  While the user has not yet entered the sentinel
8      Add this grade into the running total
9      Add one to the grade counter
10     Prompt the user to enter the next grade
11     Input the next grade (possibly the sentinel)

13  If the counter is not equal to zero
14     Set the average to the total divided by the counter
15     Print the total of the grades for all students in the class
16     Print the class average
17  else
18     Print "No grades were entered"
```

**Fig. 4.11**  |  Class average problem pseudocode algorithm with sentinel-controlled repetition.

![](bbox=[0.16, 0.5, 0.215, 0.551])

> **Error-Prevention Tip 4.3**
> 
> When performing division by an expression whose value could be zero, explicitly test for this possibility and handle it appropriately in your program (such as by printing an error message) rather than allowing the fatal error to occur. We say more about dealing with these kinds of errors when we discuss exception handling.

The pseudocode in Fig. 4.11 solves the more general class average problem. This algorithm required only two levels of refinement. Sometimes more levels are necessary.

![](bbox=[0.16, 0.646, 0.215, 0.71])

> **Software Engineering Observation 4.6**
> 
> Terminate the top-down, stepwise refinement process when the pseudocode algorithm is specified in sufficient detail for you to be able to convert the pseudocode to C++. Typically, implementing the C++ program is then straightforward.

![](bbox=[0.16, 0.728, 0.215, 0.793])

> **Software Engineering Observation 4.7**
> 
> Many experienced programmers write programs without ever using program development tools like pseudocode. These programmers feel that the ultimate goal is to solve the problem on a computer and that writing pseudocode merely delays the production of final outputs. Although this method might work for simple and familiar problems, it can lead to serious difficulties in long, complex projects.

# Implementing Sentinel-Controlled Repetition in Class GradeBook

Figures 4.12–4.13 show class GradeBook containing member function determineClass-Average that implements the pseudocode algorithm of Fig. 4.11 (this class is demonstrated in Fig. 14.14). Although each grade entered is an integer, the averaging calculation is likely to produce a number with a decimal point—in other words, a real number or float-