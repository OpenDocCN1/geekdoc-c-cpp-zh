# 5.10 Formulating Algorithms: Sentinel-Controlled Iteration 201

### Common Programming Error 5.4
Assuming that integer division rounds (rather than truncates) can lead to incorrect results.
For example, $7+4$, which yields 1.75 in conventional arithmetic, truncates to 1 in integer arithmetic, rather than rounding to 2.

![](bbox=[0.148, 0.108, 0.218, 0.153])

# 5.10 Formulating Algorithms: Sentinel-Controlled Iteration

Let us generalize Section 5.9's class-average problem. Consider the following problem:
Develop a class-averaging app that processes grades for an arbitrary number of students each time it runs.

In the previous class-example, the problem statement specified the number of students, so the number of grades (10) was known. In this example, no indication of how many grades the user will enter before stop the program's execution. The program must process an *number* of grades. How can we determine when to stop the input of grades? How will it know to calculate and print the class average?

One way to solve this is to use a special sentinel value (also called a signal value, a dummy value or a flag value) to indicate "end of data." The user enters until all grades have been entered. The user then types the sentinel value to indicate that no more grades will be entered. Sentinel-controlled iteration is often called indefinite iteration because the number of iterations is not known before the loop begins. Clearly, a sentinel value must be chosen that it cannot be confused with an acceptable value. Grades on a quality average so -1 is not an acceptable value for this problem. Thus, a run of the class-averaging program might process a sequence of inputs such as 95, 96, 75, 74, 89 and -1. The program would then compute and print the class average for the grades 95, 96, 75, 74 and 89; since -1 is the sentinel value, it should *not* enter into the averaging process.

# 5.10.1 Top-Down, Stepwise Refinement: The Top and First Refinement

We approach this class-average program with a technique top-down, stepwise refinement, which is essential to the development of well-structured programs. We begin with a pseudocode representation of the top—a statement that conveys the overall purpose of the program:

> Determine the class average for the quiz

The top is, in effect, a complete representation of a program. Unfortunately, the top rarely conveys specific detail from how to write a C# app. So we begin the refinement process. We divide the top into smaller sets of tasks and list them in the order in they'll be performed. This results in the following first refinement:

+   - Initialize variables
- Input, sum and count the quiz grades
- Calculate and print the class average

This refinement uses only the sequence structure—the steps listed should execute in order, one after the other.