
If the variable grade is greater than or equal to 90, all four conditions will be true, but only the puts statement after the first test will be executed. After that puts is executed, the else part of the “outer” if...else statement is skipped.

You may write the preceding if statement as

```c
if ( grade >= 90 ) {
    puts( "A" );
} // end if
else if ( grade >= 80 ) {
    puts( "B" );
} // end else if
else if ( grade >= 70 ) {
    puts( "C" );
} // end else if
else if ( grade >= 60 ) {
    puts( "D" );
} // end else if
else {
    puts( "F" );
} // end else
```

As far as the C compiler is concerned, both forms are equivalent. The latter form is popular because it avoids the deep indentation of the code to the right. Such indentation often leaves little room on a line, forcing lines to be split and decreasing program readability.

The if selection statement expects only one statement in its body—if you have only one statement in the if’s body, you do not need to enclose it in braces. To include several statements in the body of an if, you must enclose the set of statements in braces ({ and }). A set of statements contained within a pair of braces is called a compound statement or a block.

![](img/d0d3b7423c2d9e5650be79209ea1885d_109_0.png)

### Software Engineering Observation 3.1

*A compound statement can be placed anywhere in a program that a single statement can be placed.*

The following example includes a compound statement in the else part of an if...else statement.

```c
if ( grade >= 60 ) {
    puts( "Passed." );
} // end if
else {
    puts( "Failed." );
    puts( "You must take this course again." );
} // end else
```

In this case, if grade is less than 60, the program executes both puts statements in the body of the else and prints

```
Failed.
You must take this course again.
```

The braces surrounding the two statements in the else clause are important. Without them, the statement

```c
puts( "You must take this course again." );
```

would be outside the body of the else part of the if and would execute regardless of whether the grade was less than 60, so even a passing student would have to take the course again!

> **Error-Prevention Tip 3.2**
> Always include your control statements' bodies in braces ({ and }), even if those bodies contain only a single statement. This solves the "dangling-else" problem, which we discuss in Exercises 3.30–3.31.

A syntax error is caught by the compiler. A logic error has its effect at execution time. A fatal logic error causes a program to fail and terminate prematurely. A nonfatal logic error allows a program to continue executing but to produce incorrect results.

Just as a compound statement can be placed anywhere a single statement can be placed, it's also possible to have no statement at all, i.e., the empty statement. The empty statement is represented by placing a semicolon (;) where a statement would normally be.

> **Common Programming Error 3.1**
> Placing a semicolon after the condition in an if statement as in if ( grade >= 60 ); leads to a logic error in single-selection if statements and a syntax error in double-selection if statements.

> **Error-Prevention Tip 3.3**
> Typing the beginning and ending braces of compound statements before typing the individual statements within the braces helps avoid omitting one or both of the braces, preventing syntax errors and logic errors (where both braces are indeed required).

## 3.7 The while Iteration Statement

An iteration statement (also called a repetition statement or loop) allows you to specify that an action is to be repeated while some condition remains true. The pseudocode statement

> While there are more items on my shopping list
> Purchase next item and cross it off my list

describes the iteration that occurs during a shopping trip. The condition, "there are more items on my shopping list" may be true or false. If it's true, then the action, "Purchase next item and cross it off my list" is performed. This action will be performed repeatedly while the condition remains true. The statement(s) contained in the while iteration statement constitute the body of the while. The while statement body may be a single statement or a compound statement. Eventually, the condition will become false (when the last item on the shopping list has been purchased and crossed off the list). At this point, the iteration terminates, and the first pseudocode statement after the iteration structure is executed.

> **Common Programming Error 3.2**
> Not providing in the body of a while statement an action that eventually causes the condition in the while to become false. Normally, such an iteration structure will never terminate—an error called an "infinite loop."

> **Common Programming Error 3.3**
> *Spelling a keyword (such as while or if) with any uppercase letters (as in, While or If) is a compilation error. Remember C is case sensitive and keywords contain only lowercase letters.*

As an example of a while statement, consider a program segment designed to find the first power of 3 larger than 100. The integer variable product has been initialized to 3. When the following code finishes executing, product will contain the desired answer:

```c
product = 3;
while ( product <= 100 ) {
    product = 3 * product;
}
```

The flowchart of Fig. 3.4 illustrates the flow of control in the preceding while iteration statement. Once again, note that (besides small circles and arrows) the flowchart contains only a rectangle symbol and a diamond symbol. The flowchart clearly shows the iteration. The flowline emerging from the rectangle wraps back to the decision, which is tested each time through the loop until the decision eventually becomes false. At this point, the while statement is exited and control passes to the next statement in the program.

![](img/d0d3b7423c2d9e5650be79209ea1885d_111_0.png)

**Fig. 3.4** | Flowcharting the while iteration statement.

When the while statement is entered, the value of product is 3. The variable product is repeatedly multiplied by 3, taking on the values 9, 27 and 81 successively. When product becomes 243, the condition in the while statement, product <= 100, becomes false. This terminates the iteration, and the final value of product is 243. Program execution continues with the next statement after the while.

## 3.8 Formulating Algorithms Case Study 1: Counter-Controlled Iteration

To illustrate how algorithms are developed, we solve several variations of a class-averaging problem. Consider the following problem statement:

> *A class of ten students took a quiz. The grades (integers in the range 0 to 100) for this quiz are available to you. Determine the class average on the quiz.*

The class average is equal to the sum of the grades divided by the number of students. The algorithm for solving this problem on a computer must input each of the grades, perform the averaging calculation, and print the result.

Let’s use pseudocode to list the actions to execute and specify the order in which these actions should execute. We use counter-controlled iteration to input the grades one at a time. This technique uses a variable called a counter to specify the number of times a set of statements should execute. In this example, iteration terminates when the counter exceeds 10. In this case study we simply present the pseudocode algorithm (Fig. 3.5) and the corresponding C program (Fig. 3.6). In the next case study we show how pseudocode algorithms are developed. Counter-controlled iteration is often called definite iteration because the number of iterations is known before the loop begins executing.

- 1. Set total to zero
- 2. Set grade counter to one
- 3. While grade counter is less than or equal to ten
  - Input the next grade
  - Add the grade into the total
  - Add one to the grade counter
- 4. Set the class average to the total divided by ten
- 5. Print the class average

**Fig. 3.5** | Pseudocode algorithm that uses counter-controlled iteration to solve the class-average problem.

```c
// Fig. 3.6: fig03_06.c
// Class average program with counter-controlled iteration.
#include <stdio.h>

// function main begins program execution
int main( void )
{
    unsigned int counter; // number of grades to be entered next
    int grade; // grade value
    int total; // sum of grades entered by user
    int average; // average of grades

    // initialization phase
    total = 0; // initialize total
    counter = 1; // initialize loop counter

    // processing phase
    while ( counter <= 10 ) { // loop 10 times
        printf( "%s", "Enter grade: " ); // prompt for input
        scanf( "%d", &grade ); // read grade from user
        total = total + grade; // add grade to total
        counter = counter + 1; // increment counter
    } // end while
```

**Fig. 3.6** | Class-average problem with counter-controlled iteration. (Part 1 of 2.)
