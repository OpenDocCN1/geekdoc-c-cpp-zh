
do...while evaluates the loop-continuation test immediately. A for statement executes its increment expression, then tests the loop-continuation condition.

## Section 4.9 Logical Operators
- Logical operators && (logical AND), || (logical OR) and ! (logical NOT, or logical negation) may be used to form complex conditions by combining simple conditions.
- The && (logical AND; p. 153) operator evaluates to true if and only if both of its operands are true.
- C evaluates all expressions that include relational operators, equality operators, and/or logical operators to 0 or 1. Although C sets a true value to 1, it accepts any nonzero value as true.
- The || (logical OR; p. 153) operator evaluates to true if either or both of its operands are true.
- The && operator has higher precedence than ||. Both operators group from left-to-right.
- Operators && or || use short-circuit evaluation, terminating as soon as the condition is known to be false or true.
- C provides the ! (logical negation; p. 153) operator to enable you to “reverse” the meaning of a condition. Unlike the binary operators && and ||, which combine two conditions, the unary logical negation operator has only a single condition as an operand.
- The logical negation operator is placed before a condition when we’re interested in choosing a path of execution if the original condition (without the logical negation operator) is false.

## Section 4.10 Confusing Equality (==) and Assignment (=) Operators
- Programmers often accidentally swap the operators == and =. Statements with these errors ordinarily compile correctly, allowing programs to run to completion while likely generating incorrect results through runtime logic errors.
- In a condition like 7 == x, if you accidentally replace == with =, the compiler will report a syntax error. Only a variable name can be placed on the left-hand side of an assignment.
- Variable names are said to be lvalues (for “left values”; p. 158) because they can be used on the left side of an assignment operator.
- Constants are said to be rvalues (for “right values”; p. 158) because they can be used only on the right side of an assignment operator. lvalues can also be used as rvalues, but not vice versa.

## Self-Review Exercises
### 4.1 Fill-In the blanks in each of the following statements.
- a) In counter-controlled iteration, a(n) ____ is used to count the number of times a group of instructions should be repeated.
- b) The ____ statement, when executed in an iteration statement, causes the next iteration of the loop to be performed immediately.
- c) The ____ statement, when executed in an iteration statement or a switch, causes an immediate exit from the statement.
- d) The ____ is used to test a particular variable or expression for each of the constant integral values it may assume.

### 4.2 State whether the following are true or false. If the answer is false, explain why.
- a) The default case is required in the switch selection statement.
- b) The break statement is required in a switch statement’s default case.
- c) The expression (x > y && a < b) is true if either x > y is true or a < b is true.
- d) An expression containing the `||` operator is *true* if either or both of its operands are *true*.

### 4.3 Write a statement or a set of statements to accomplish each of the following tasks:
- a) Sum the odd integers between 1 and 99 using a `for` statement. Use the integer variables `sum` and `count`.
- b) Print the value `333.546372` in a field width of 15 characters with precisions of 1, 2, 3, 4 and 5. Left-align the output. What are the five values that print?
- c) Calculate the value of 2.5 raised to the power of 3 using the `pow` function. Print the result with a precision of 2 in a field width of 10 positions. What is the value that prints?
- d) Print the integers from 1 to 20 using a `while` loop and the counter variable `x`. Print only five integers per line. [*Hint*: Use the calculation x % 5. When this is 0, print a newline character, otherwise print a tab character.]
- e) Repeat Exercise 4.3(d) using a `for` statement.

### 4.4 Find the error in each of the following code segments and explain how to correct it:
```c
a) x = 1;
   while (x <= 10);
       ++x;
   }
```
```c
b) for (double y = .1; y != 1.0; y += .1) {
       printf("%f\n", y);
   }
```
```c
c) switch (n) {
       case 1:
           puts("The number is 1");
       case 2:
           puts("The number is 2");
           break;
       default:
           puts("The number is not 1 or 2");
           break;
   }
```
d) The following code should print the values 1 to 10.
```c
n = 1;
while (n < 10) {
    printf("%d ", n++);
}
```

## Answers to Self-Review Exercises
### 4.1
a) control variable or counter. b) `continue`. c) `break`. d) `switch` selection statement.

### 4.2 See the answers below:
- a) **False.** The default case is optional. If no default action is needed, then there's no need for a default case.
- b) **False.** The break statement is used to exit the switch statement. The break statement is not required in *any* case.
- c) **False.** Both of the relational expressions must be *true* for the entire expression to be *true* when using the && operator.
- d) **True.**

### 4.3 See the answers below:
```c
a) int sum = 0;
   for (int count = 1; count <= 99; count += 2) {
       sum += count;
   }

b) printf("%-15.1f\n", 333.546372); // prints 333.5
   printf("%-15.2f\n", 333.546372); // prints 333.55
   printf("%-15.3f\n", 333.546372); // prints 333.546
   printf("%-15.4f\n", 333.546372); // prints 333.5464
   printf("%-15.5f\n", 333.546372); // prints 333.54637

c) printf("%10.2f\n", pow(2.5, 3)); // prints 15.63
```
```c
d) int x = 1;

   while (x <= 20) {
       printf("%d", x);
       if (x % 5 == 0) {
           puts("");
       }
       else {
           printf("%s", "\t");
       }
       ++x;
   }
```
or
```c
int x = 1;
while (x <= 20) {
    if (x % 5 == 0) {
        printf("%d\n", x++);
    }
    else {
        printf("%d\t", x++);
    }
}
```
or
```c
int x = 0;
while (++x <= 20) {
    if (x % 5 == 0) {
        printf("%d\n", x);
    }
    else {
        printf("%d\t", x);
    }
}
```
```c
e) for (int x = 1; x <= 20; ++x) {
    printf("%d", x);
    if (x % 5 == 0) {
        puts("");
    }
    else {
        printf("%s", "\t");
    }
}
```
or
```c
for (int x = 1; x <= 20; ++x) {
    if (x % 5 == 0) {
        printf("%d\n", x);
    }
    else {
        printf("%d\t", x);
    }
}
```
- 4.4 a) Error: The semicolon after the while header causes an infinite loop.
  Correction: Replace the semicolon with a { or remove both the ; and the }.
- b) Error: Using a floating-point number to control a for iteration statement.
  Correction: Use an integer, and perform the proper calculation to get the values you desire.
```c
for (int y = 1; y != 10; ++y) {
    printf("%f\n", (float) y / 10);
}
```
- c) Error: Missing break statement in the statements for the first case.
  Correction: Add a break statement at the end of the statements for the first case. This is not necessarily an error if you want the statement of case 2: to execute every time the case 1: statement executes.
d) Error: Improper relational operator used in the while iteration-continuation condition.
Correction: Use `<=` rather than `<`.

## Exercises
### 4.5 Find the error in each of the following. *(Note: There may be more than one error.)*
- a)
```c
For (x = 100, x >= 1, ++x) {
    printf("%d\n", x);
}
```
- b) The following code should print whether a given integer is odd or even:
```c
switch (value % 2) {
    case 0:
        puts("Even integer");
    case 1:
        puts("Odd integer");
}
```
- c) The following code should input an integer and a character and print them. Assume the user types as input 100 A.
```c
scanf("%d", &intVal);
charVal = getchar();
printf("Integer: %d\nCharacter: %c\n", intVal, charVal);
```
- d)
```c
for (x = .000001; x == .0001; x += .000001) {
    printf("%.7f\n", x);
}
```
- e) The following code should output the odd integers from 999 to 1:
```c
for (x = 999; x >= 1; x += 2) {
    printf("%d\n", x);
}
```
- f) The following code should output the even integers from 2 to 100:
```c
counter = 2;
Do {
    if (counter % 2 == 0) {
        printf("%d\n", counter);
    }
    counter += 2;
} While (counter < 100);
```
- g) The following code should sum the integers from 100 to 150 (assume total is initialized to 0):
```c
for (x = 100; x <= 150; ++x) {
    total += x;
}
```
