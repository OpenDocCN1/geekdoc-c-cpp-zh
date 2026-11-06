
## 4.9.5 Input Validation

Any time a program receives input from the user, various problems might occur. For example, in line 15 of **Fig. 4.10**:

```cpp
cin >> grade; // input next grade
```

we assume that the user will enter an integer grade in the range 0 to 100. However, the user could enter an integer less than 0, an integer greater than 100, an integer outside the range of values that can be stored in an `int` variable, a number containing a decimal point, or a value containing letters or special symbols that’s not even an integer.

To ensure that inputs are valid, industrial-strength programs must test for all possible erroneous cases. A program that inputs grades should validate the grades by using **range checking** to ensure that they’re values from 0 to 100. You can then ask the user to reenter any value that’s out of range. If a program requires inputs from a specific set of values (e.g., nonsequential product codes), you can ensure that each input matches a value in the set.

## 4.10 Formulating Algorithms: Sentinel-Controlled Iteration

Let’s generalize **Section 4.9**’s class-average problem. Consider the following problem:

- *Develop a class-averaging program that processes grades for an arbitrary number of students each time it’s run.*

In the previous class-average example, the problem statement specified the number of students, so the number of grades (10) was known in advance. In this example, no indication is given of how many grades the user will enter during the program’s execution. The program must process an *arbitrary* number of grades. How can it determine when to stop the input of grades? How will it know when to calculate and print the class average?

One way to solve this problem is to use a special value called a **sentinel value** (also called a **signal value**, a **dummy value** or a **flag value**) to indicate “end of data entry.” The user enters grades until all legitimate grades have been entered. The user then types the sentinel value to indicate that no more grades will be entered. **Sentinel-controlled iteration** is often called **indefinite iteration** because the number of iterations is *not* known before the loop begins executing.

Clearly, a sentinel value must be chosen that cannot be confused with an acceptable input value. Grades on a quiz are nonnegative integers, so −1 is an acceptable sentinel value for this problem. Thus, a run of the class-averaging program might process a stream of inputs such as 95, 96, 75, 74, 89 and −1. The program would then compute and print the class average for the grades 95, 96, 75, 74 and 89; since −1 is the sentinel value, it should *not* enter into the averaging calculation.

### 4.10.1 Top-Down, Stepwise Refinement: The Top and First Refinement

We approach this class-averaging program with a technique called **top-down, stepwise refinement**, which is essential to the development of well-structured programs. We begin with a pseudocode representation of the **top**—a single statement that conveys the overall function of the program:

```text
Determine the class average for the quiz
```

The top is, in effect, a *complete* representation of a program. Unfortunately, the top rarely conveys sufficient detail from which to write a C++ program. So we now begin the refinement process. We divide the top into a series of smaller tasks and list these in the order in which they’ll be performed. This results in the following **first refinement**:

```text
Initialize variables

Input, sum and count the quiz grades
Calculate and print the class average
```

This refinement uses only the *sequence* structure—the steps listed should execute in order, one after the other.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_443_0.png)

### Software Engineering Observation 4.2

*Each refinement, as well as the top itself, is a complete specification of the algorithm—only the level of detail varies.*

### 4.10.2 Proceeding to the Second Refinement

The preceding Software Engineering Observation is often all you need for the first refinement in the top-down process. To proceed to the next level of refinement—that is, the **second refinement**—we commit to specific variables. In this example, we need a running total of the numbers, a count of how many numbers have been processed, a variable to receive the value of each grade as it’s entered by the user and a variable to hold the calculated average. The pseudocode statement

```text
Initialize variables
```

can be refined as follows:

```text
Initialize total to zero
Initialize counter to zero
```

Only the variables *total* and *counter* need to be initialized before they’re used. The variables *average* and *grade* (for the calculated average and the user input, respectively) need not be initialized, because their values will be replaced as they’re calculated or input.

The pseudocode statement

```text
Input, sum and count the quiz grades
```

requires *iteration* to successively input each grade. We do not know in advance how many grades will be entered, so we’ll use sentinel-controlled iteration. The user enters grades one at a time. After entering the last grade, the user enters the sentinel value. The program tests for the sentinel value after each grade is input and terminates the loop when the user enters the sentinel value. The second refinement of the preceding pseudocode statement is then:

```text
Prompt the user to enter the first grade
Input the first grade (possibly the sentinel)
While the user has not yet entered the sentinel
    Add this grade into the running total
    Add one to the grade counter
    Prompt the user to enter the next grade
    Input the next grade (possibly the sentinel)
```

We simply indent the statements under the *While* to show that they belong to the *While*. Again, pseudocode is only an informal program development aid.

The pseudocode statement

```text
Calculate and print the class average
```

can be refined as follows:

```text
If the counter is not equal to zero
    Set the average to the total divided by the counter
    Print the average
else
    Print "No grades were entered"
```

We’re careful here to test for the possibility of *division by zero*—a logic *error* that, if undetected, would cause the program to fail or produce invalid output. The complete second refinement of the pseudocode for the class-average problem is shown in **Fig. 4.11**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_446_0.png)

### Error-Prevention Tip 4.3

According to the C++ standard, the result of division by zero in floating-point arithmetic is undefined. When performing division (`/`) or remainder (`%`) calculations in which the right operand could be zero, test for this and handle it (e.g., display an error message) rather than allowing the calculation to proceed.

```text
1  Initialize total to zero
2  Initialize counter to zero
3
4  Prompt the user to enter the first grade
5  Input the first grade (possibly the sentinel)
6
7  While the user has not yet entered the sentinel
8      Add this grade into the running total
9      Add one to the grade counter
10     Prompt the user to enter the next grade
11     Input the next grade (possibly the sentinel)
12
13 If the counter is not equal to zero
14     Set the average to the total divided by the counter
15     Print the average
16 else
17     Print “No grades were entered”
```

**Fig. 4.11** Class-averaging pseudocode algorithm with sentinel-controlled iteration.

In **Fig. 4.9** and **Fig. 4.11**, we included blank lines and indentation in the pseudocode to make it more readable. The blank lines separate the algorithms into their phases and set off control statements; the indentation emphasizes the bodies of the control statements.

The pseudocode algorithm in **Fig. 4.11** solves the more general class-average problem. This algorithm was developed after two refinements. Sometimes more are needed.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_448_0.png)

### Software Engineering Observation 4.3

Terminate the top-down, stepwise refinement process when you've specified the pseudocode algorithm in sufficient detail for you to convert the pseudocode to C++.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_448_1.png)

### Software Engineering Observation 4.4

Some programmers do not use program development tools like pseudocode. They feel that their ultimate goal is to solve the problem on a computer and that writing pseudocode merely delays the production of final outputs. Although this may work for simple and familiar problems, it can lead to serious errors and delays in large, complex projects.
