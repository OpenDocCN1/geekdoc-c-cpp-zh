
The flowchart clearly shows the iteration—the flowline emerging from the rectangle points back to the flowline entering the decision. The loop tests the condition in the diamond during each iteration until the condition eventually becomes *false*. At this point, the `while` statement exits and control continues with the next statement in sequence.

### Self Check

- 1. (Program Segment) The `while` statement program segment in this section finds the first power of 3 larger than 100. Rewrite this program segment so that it will find the first power of 2 greater than or equal to 1024, leaving it in product.
  Answer: See below.

  ```c
  int product = 2;

  while (product < 1024) {
      product = 2 * product;
  }
  ```

- 2. (Fill-in-the-Blank) An action in a `while` statement's body must eventually cause the condition to become *false*; otherwise, the loop will never terminate. This is a logic error called a(n) ________.
  Answer: infinite loop.

## 3.8 Formulating Algorithms Case Study 1: Counter-Controlled Iteration

To illustrate how algorithms are developed, we solve two variations of a class-averaging problem in this section and the next. Consider the following problem statement:

> *A class of ten students took a quiz. The grades (integers in the range 0 to 100) for this quiz are available to you. Determine the class average on the quiz.*

The class average is the sum of the grades divided by the number of students. The algorithm to solve this problem must input the grades, then calculate and display the class average.

### Pseudocode for the Class-Average Problem

Let's use pseudocode to list the actions to execute and specify the order in which they should execute. We use counter-controlled iteration to input the grades one at a time. This technique uses a variable called a counter to specify the number of times a set of statements should execute. In this example, we know that ten students took a quiz, so we need to input 10 grades. Iteration terminates when the counter exceeds 10. In this case study, we simply present the final pseudocode algorithm (Fig. 3.1) and the corresponding C program (Fig. 3.2). In the next case study, we show how to develop pseudocode algorithms. Counter-controlled iteration is often called definite iteration because the number of iterations is known before the loop begins executing.

```
1  Set total to zero
2  Set grade counter to one
3
4  While grade counter is less than or equal to ten
5      Input the next grade
6      Add the grade into the total
7      Add one to the grade counter
8
9  Set the class average to the total divided by ten
10 Print the class average
```

**Fig. 3.1** | Pseudocode algorithm that uses counter-controlled iteration to solve the class-average problem.

```
1  // fig03_02.c
2  // Class average program with counter-controlled iteration.
3  #include <stdio.h>
4
5  // function main begins program execution
6  int main(void) {
7      // initialization phase
8      int total = 0; // initialize total of grades to 0
9      int counter = 1; // number of the grade to be entered next
10
11     // processing phase
12     while (counter <= 10) { // loop 10 times
13         printf("%s", "Enter grade: "); // prompt for input
14         int grade = 0; // grade counter
15         scanf("%d", &grade); // read grade from user
16         total = total + grade; // add grade to total
17         counter = counter + 1; // increment counter
18     } // end while
19
20     // termination phase
21     int average = total / 10; // integer division
22     printf("Class average is %d\n", average); // display result
23 } // end function main
```

```
Enter grade: 98
Enter grade: 76
Enter grade: 71
Enter grade: 87
Enter grade: 83
Enter grade: 90
Enter grade: 57
Enter grade: 79
Enter grade: 82
Enter grade: 94
Class average is 81
```

**Fig. 3.2** | Class-average problem with counter-controlled iteration.

A total is a variable (line 8) used to accumulate the sum of a series of values. A counter is a variable (line 9) used to count—in this case, to count the number of grades entered. Variables for totals should be initialized to zero; otherwise, the sum would include the previous value stored in the total's memory location. You should initialize all counters and totals. Counters typically are initialized to zero or one, depending on their use—we'll present examples of each. An uninitialized variable contains a "garbage" value—the value last stored in the memory location reserved for that variable. If a counter or total isn't initialized, the results of your program will be incorrect. These are examples of logic errors.

![](img/43d318ad505997c339a3ea78d716d162_154_0.png)

The average was 81 in the preceding sample execution, but the sum of the grades we input was 817. Of course, 817 divided by 10 should yield 81.7—a number with a decimal point. The next section shows how to deal with such floating-point numbers.

### Self Check

- 1. *(Fill-in-the-Blank)* Counter-controlled iteration is often called ________ iteration because the number of iterations is known before the loop begins executing.
  **Answer:** definite.

- 2. *(True/False)* Variables used to store totals should be initialized to one before being used in a program; otherwise, the sum would include the previous value stored in the total's memory location.
  **Answer:** *False.* Actually, variables used to store totals should be initialized to *zero* before being used in a program; otherwise, the sum would include the previous value stored in the total's memory location.

## 3.9 Formulating Algorithms with Top-Down, Stepwise Refinement Case Study 2: Sentinel-Controlled Iteration

Let's generalize the class-average problem. Consider the following problem:

> *Develop a class-averaging program that will process an arbitrary number of grades each time the program is run.*

In the first class-average example, we knew there were 10 grades in advance. In this example, no indication is given of how many grades the user might input. The program must process an *arbitrary* number of grades. How can the program determine when to stop inputting grades? How will it know when to calculate and print the class average?

### Sentinel Values

One way is to use a sentinel value to indicate "end of data entry." A sentinel value also is called a signal value, a dummy value, or a flag value. The user types grades until all legitimate grades have been entered. The user then types the sentinel value to indicate "the last grade has been entered." Sentinel-controlled iteration is often called indefinite iteration because the number of iterations isn't known before the loop begins executing.

requires an iteration structure that successively inputs each grade. Because we do not know how many grades are to be processed, we'll use sentinel-controlled iteration. The user will enter legitimate grades one at a time. After entering the last legitimate grade, the user will type the sentinel value. The program will test for this value after each grade is input and will terminate the loop when the sentinel is entered. The refinement of the preceding pseudocode statement is then

```
Input the first grade (possibly the sentinel)
While the user has not as yet entered the sentinel
    Add this grade into the running total
    Add one to the grade counter
    Input the next grade (possibly the sentinel)
```

In pseudocode, we do not use braces around the set of statements that form a loop's body. We simply indent the body statements under the while. Again, pseudocode is an informal program-development aid.

The pseudocode statement

```
Calculate and print the class average
```

may be refined as follows:

```
If the counter is not equal to zero
    Set the average to the total divided by the counter
    Print the average
else
    Print "No grades were entered"
```

We're being careful here to test for the possibility of division by zero—a fatal error ⊗ ERR that, if undetected, would cause the program to fail (often called “crashing”). You should explicitly test for this case and handle it appropriately in your program, such as by printing an error message, rather than allowing the fatal error to occur.

### Complete Second Refinement

The complete second refinement is shown in Fig. 3.3. We include some blank lines in the pseudocode for readability.

| Line | Pseudocode |
|------|------------|
| 1 | Initialize total to zero |
| 2 | Initialize counter to zero |
| 3 |  |
| 4 | Input the first grade (possibly the sentinel) |
| 5 | While the user has not as yet entered the sentinel |
| 6 | Add this grade into the running total |
| 7 | Add one to the grade counter |
| 8 | Input the next grade (possibly the sentinel) |

Fig. 3.3 | Pseudocode algorithm that uses sentinel-controlled iteration to solve the class-average problem. (Part 1 of 2.)
