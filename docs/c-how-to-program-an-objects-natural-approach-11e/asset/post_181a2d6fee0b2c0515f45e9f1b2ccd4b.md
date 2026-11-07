
sions in which all the operand types are identical. To ensure this, the compiler performs an operation called **promotion** (also called **implicit conversion**) on selected operands. In an expression containing values of data types `double` and `int`, C++ promotes any `int` operands to `double` values. So in line 32, C++ promotes a temporary copy of gradeCounter’s value to type `double`, then performs the division.

## 3.9.5 Formatting Floating-Point Numbers

Figure 3.2’s formatting features are introduced here briefly. Chapter 19 explains them in depth. In Chapter 4, we’ll introduce C++20’s new text-formatting features that can express the formatting we show here more concisely.

### Parameterized Stream Manipulator `setprecision`

Line 37’s call to `setprecision`—`setprecision(2)`—indicates that floating-point values should be output with two digits of **precision** to the right of the decimal point (e.g., 92.37). `setprecision` is a **parameterized stream manipulator** because it requires an argument (in this case, 2) to perform its task. Programs that use parameterized stream manipulators must include the header `<iomanip>` (line 4).

### Nonparameterized Stream Manipulator `fixed`

The **non-parameterized stream manipulator `fixed`** (line 37) does not require an argument and indicates that floating-point values should be output in **fixed-point format**. This is opposed to **scientific notation**³, which displays a number from 1.0 up to, but not including, 10.0 multiplied by a power of 10. So, in scientific notation, the value 3,100.0 is displayed as 3.1e+03 (that is, 3.1 × 10³). This format is useful for displaying very large or very small values (that is, values with negative exponents).

Fixed-point formatting forces a floating-point number to display without scientific notation. Fixed-point formatting also forces the decimal point and trailing zeros to print, even if the value is a whole-number amount, such as 88.00. Without the fixed-point formatting option, 88.00 prints as 88 without the trailing zeros and decimal point.

Stream manipulators `setprecision` and `fixed` perform **sticky settings**—all floating-point values formatted in your program will use those settings until you change them. Chapter 19 shows how to capture the stream format settings before applying sticky settings, so you can restore the original format settings later.

### Rounding Floating-Point Numbers

When the stream manipulators `fixed` and `setprecision` are used, the formatted value is **rounded** to the number of decimal positions specified by the current precision. The value in memory remains unaltered. For the precision 2, 87.946 and 67.543 would be rounded to 87.95 and 67.54, respectively.⁴

Lines 37 and 38 of Fig. 3.2 output the class average rounded to the nearest hundredth, with exactly two digits to the right of the decimal point. The three grades entered during the program’s execution in Fig. 3.2 total 257, which yields the average 85.666… and displays the rounded value 85.67.

- 3. Formatting using scientific notation is discussed further in Chapter 19.
- 4. In Fig. 3.2, if you do not specify `setprecision` and `fixed`, C++ uses four digits of precision by default. If you specify only `fixed`, C++ uses six digits of precision.

## Checkpoint

- 1. *(True/False)* Any value may be used as a sentinel value.  
  **Answer:** False. You must choose a sentinel value that cannot be confused with an acceptable input value.

- 2. *(Fill-in)* For arithmetic on fundamental types, the compiler knows how to evaluate only expressions in which all the operand types are identical. To ensure this, the compiler performs an operation called ________ (also called ________) on selected operands.  
  **Answer:** promotion, implicit conversion.

- 3. *(Code)* Write a program segment that reads an arbitrary number of integer Fahrenheit temperatures from the user and calculates their average. Assume the user enters at least one temperature and temperatures are in the range −212 to 212. Display the average.  
  **Answer:**

  ```
  double total{0.0};
  int counter{0};

  cout << "Enter a temperature or 9999 to quit: ";
  int temperature;
  cin >> temperature;

  while (temperature != 9999) {
      total = total + temperature;
      counter = counter + 1;

      cout << "Enter a temperature or 9999 to quit: ";
      cin >> temperature;
  }

  double average{total / counter};
  cout << "Average temperature is: " << average << "\n";
  ```

  ```
  Enter a temperature or 9999 to quit: 12
  Enter a temperature or 9999 to quit: -22
  Enter a temperature or 9999 to quit: 17
  Enter a temperature or 9999 to quit: 9999
  Average temperature is: 2.33333
  ```

## 3.10 Formulating Algorithms: Nested Control Statements

We’ve seen that control statements can be stacked on top of one another (in sequence). In this case study, we examine nesting one control statement within another—the other structured way control statements can be connected.

### 3.10.1 Problem Statement

Consider the following problem statement:

> A college offers a course that prepares students for the state licensing exam for real estate brokers. Last year, 10 students who completed this course took the exam. The college wants to know how well its students did on the exam. You’ve been asked to write a program to summarize the results. You’ve been given a list of these 10 students. Next to each name is a 1 if the student passed the exam or a 2 if the student failed.
>
> Your program should analyze the results of the exam as follows:
>
> - 1. Input each test result (i.e., a 1 or a 2). Display “Enter result” on the screen each time the program requests another test result.
> - 2. Count the number of test results of each type.
> - 3. Display a summary of the test results, indicating the number of students who passed and the number who failed.
> - 4. If more than eight students pass, print “Bonus to instructor!”

**Problem Statement Observations**

After reading the problem statement carefully, we make the following observations:

- 1. The program must process test results for 10 students. We can use counter-controlled iteration because we know the number of test results in advance.
- 2. Each time the program reads a test result, it must determine whether it’s a 1 or a 2. We test for a 1 in our algorithm. If the number is not a 1, we assume it’s a 2. (Exercise 3.10 considers the consequences of this assumption.)
- 3. Two counters are used to keep track of the exam results—one to count the number of students who passed the exam and the other to count the number who failed.
- 4. After the program has processed all the results, it must decide whether more than eight students passed the exam.

### 3.10.2 Top-Down, Stepwise Refinement: Pseudocode Representation of the Top

Let’s proceed with top-down, stepwise refinement. We begin with a pseudocode representation of the top:

```
analyze exam results and decide whether a bonus should be paid
```

Once again, the top is a complete representation of the program, but we’ll likely need several refinements before the pseudocode can evolve naturally into a C++ program.

### 3.10.3 Top-Down, Stepwise Refinement: First Refinement

Our first refinement is

```
initialize variables
input the 10 exam results, and count passes and failures
print a summary of the exam results and decide whether a bonus should be paid
```

Here, too, though we have a complete representation of the entire program, further refinement is necessary. We now commit to specific variables. We need counters to record the passes and failures, a counter to control the looping process, and a variable to store the user input. We do not need to initialize the variable that stores the user input because its value is read from the user during each loop iteration.

### 3.10.4 Top-Down, Stepwise Refinement: Second Refinement

The pseudocode statement

```
initialize variables
```

can be refined as follows:

```
initialize passes to zero
initialize failures to zero
initialize student counter to one
```

Notice that only the counters are initialized at the start of the algorithm.

The pseudocode statement

```
input the 10 exam results, and count passes and failures
```

requires a loop that successively inputs the result of each exam. We know in advance that there are precisely 10 exam results, so counter-controlled looping is appropriate. Inside the loop (i.e., nested within the loop), a double-selection structure will determine whether each exam result is a pass or a failure, then increment the appropriate counter. The preceding pseudocode statement can be refined as follows:

```
while student counter is less than or equal to 10
    prompt the user to enter the next exam result
    input the next exam result

    if the student passed
        add one to passes
    else
        add one to failures

    add one to student counter
```

We use blank lines to isolate the nested *if…else* statement, which improves readability.

The pseudocode statement

```
print a summary of the exam results and decide whether a bonus should be paid
```

can be refined as follows:

```
print the number of passes
print the number of failures
if more than eight students passed
    print “Bonus to instructor!”
```

### 3.10.5 Complete Second Refinement of the Pseudocode

Here we show the complete second refinement. This pseudocode is now sufficiently refined for conversion to C++.

```
1  initialize passes to zero
2  initialize failures to zero
3  initialize student counter to one
4
```
