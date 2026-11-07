been entered. Sentinel-controlled repetition is often called **indefinite repetition** because the number of repetitions is *not* known before the loop begins executing.

The sentinel value must be chosen so that it’s not confused with an acceptable input value. Grades are normally nonnegative integers, so −1 is an acceptable sentinel value. Thus, a run of the program might process inputs such as 95, 96, 75, 74, 89 and −1. The program would then print the class average for the grades 95, 96, 75, 74 and 89. Since −1 is the sentinel value, it should not enter into the averaging calculation.

# Developing the Pseudocode Algorithm with Top-Down, Stepwise Refinement: The Top and First Refinement

We approach the class average program with a technique called **top-down, stepwise refinement**, a technique that’s helpful to the development of well-structured programs. We begin with a pseudocode representation of the **top**—a single statement that conveys the overall function of the program:

```
Determine the class average for the quiz for an arbitrary number of students
```

The top is, in effect, a *complete* representation of a program. Unfortunately, the top (as in this case) rarely conveys sufficient detail from which to write a program. So, now we begin the refinement process. We divide the top into a series of smaller tasks and list these in the order in which they need to be performed. This results in the following **first refinement**.

+   - Initialize variables
+   - Input, sum and count the quiz grades
+   - Calculate and print the total of all student grades and the class average

This refinement uses only the sequence structure—the steps execute in order.

![](bbox=[0.129, 0.567, 0.189, 0.617])

> **Software Engineering Observation 4.4**
> 
> Each refinement, as well as the top itself, is a complete specification of the algorithm; only the level of detail varies.

![](bbox=[0.129, 0.638, 0.189, 0.685])

> **Software Engineering Observation 4.5**
> 
> Many programs can be divided logically into three phases; an initialization phase that initializes the program variables, a processing phase that inputs data values and adjusts program variables (such as counters and totals) accordingly, and a termination phase that calculates and outputs the final results.

# Proceeding to the Second Refinement

The preceding *Software Engineering Observation* is often all you need for the first refinement in the top-down process. In the **second refinement**, we commit to specific variables. In this example, we need a running total of the numbers, a count of how many numbers have been processed, a variable to receive the value of each grade as it’s entered by the user and a variable to hold the calculated average. The pseudocode statement

```
Initialize variables
```

can be refined as follows:

+   - Initialize total to zero
+   - Initialize counter to zero