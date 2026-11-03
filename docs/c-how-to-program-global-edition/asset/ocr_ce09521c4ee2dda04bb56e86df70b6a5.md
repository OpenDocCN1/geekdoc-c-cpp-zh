in Chapter 5—when we discuss the scope of variables—how this practice helps you eliminate errors.

# 3.9 Formulating Algorithms with Top-Down, Stepwise Refinement Case Study 2: Sentinel-Controlled Iteration

Let’s generalize the class-average problem. Consider the following problem:

*Develop a class-averaging program that will process an arbitrary number of grades each time the program is run.*

In the first class-average example, the number of grades (10) was known in advance. In this example, no indication is given of how many grades are to be entered. The program must process an arbitrary number of grades. How can the program determine when to stop the input of grades? How will it know when to calculate and print the class average?

One way to solve this problem is to use a special value called the sentinel value (also called a signal value, a dummy value, or a flag value) to indicate “end of data entry.” The user types grades until all legitimate grades have been entered. The user then types the sentinel value to indicate “the last grade has been entered.” Sentinel-controlled iteration is often called indefinite iteration because the number of iterations isn’t known before the loop begins executing.

Clearly, the sentinel value must be chosen so that it cannot be confused with an acceptable input value. Because grades on a quiz are normally nonnegative integers, −1 is an acceptable sentinel value for this problem. Thus, a run of the class-average program might process a stream of inputs such as 95, 96, 75, 74, 89 and −1. The program would then compute and print the class average for the grades 95, 96, 75, 74, and 89 (−1 would be the sentinel value, so it should not enter into the averaging calculation).

# Top-Down, Stepwise Refinement

We approach the class-average program with a technique called top-down, stepwise refinement, a technique that’s essential to the development of well-structured programs. We begin with a pseudocode representation of the top:

*Determine the class average for the quiz*

+   Initialize variables
+   Input, sum, and count the quiz grades
+   Calculate and print the class average

Here, only the sequence structure has been used—the steps listed are to be executed in order, one after the other.

> **Software Engineering Observation 3.2**
> 
> *Each refinement, as well as the top itself, is a complete specification of the algorithm; only the level of detail varies.*

![](bbox=[0.22, 0.92, 0.28, 0.98])