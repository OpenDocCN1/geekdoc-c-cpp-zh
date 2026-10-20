
![](img/009e962758dcc71dbc43a493362e6dc0_175_0.png)

![](img/009e962758dcc71dbc43a493362e6dc0_175_1.png)

Fig. 4.20 | Lines fanning from a corner.

![](img/009e962758dcc71dbc43a493362e6dc0_175_2.png)

![](img/009e962758dcc71dbc43a493362e6dc0_175_3.png)

Fig. 4.21 | Line art with loops and drawLine.

## 4.15 Wrap-Up

This chapter presented basic problem solving for building classes and developing methods for these classes. We demonstrated how to construct an algorithm (i.e., an approach to solving a problem), then how to refine the algorithm through several phases of pseudocode development, resulting in Java code that can be executed as part of a method. The chapter showed how to use top-down, stepwise refinement to plan out the specific actions that a method must perform and the order in which the method must perform these actions.

Only three types of control structures—sequence, selection and repetition—are needed to develop any problem-solving algorithm. Specifically, this chapter demonstrated the if single-selection statement, the if...else double-selection statement and the while repetition statement. These are some of the building blocks used to construct solutions to many problems. We used control-statement stacking to total and compute the average of a set of student grades with counter- and sentinel-controlled repetition, and we used control-statement nesting to analyze and make decisions based on a set of exam results. We introduced Java’s compound assignment operators and its increment and decrement operators. Finally, we discussed Java’s primitive types. In Chapter 5, we continue our discussion of control statements, introducing the for, do...while and switch statements.

## Summary

### Section 4.1 Introduction

- Before writing a program to solve a problem, you must have a thorough understanding of the problem and a carefully planned approach to solving it. You must also understand the building blocks that are available and employ proven program-construction techniques.

### Section 4.2 Algorithms

- Any computing problem can be solved by executing a series of actions (p. 103) in a specific order.
- A procedure for solving a problem in terms of the actions to execute and the order in which they execute is called an algorithm (p. 103).
- Specifying the order in which statements execute in a program is called program control (p. 104).

### Section 4.3 Pseudocode

- Pseudocode (p. 104) is an informal language that helps you develop algorithms without having to worry about the strict details of Java language syntax.
- Pseudocode is similar to everyday English—it’s convenient and user friendly, but it’s not an actual computer programming language.
- Pseudocode helps you “think out” a program before attempting to write it in a programming language, such as Java.
- Carefully prepared pseudocode can easily be converted to a corresponding Java program.

### Section 4.4 Control Structures

- Normally, statements in a program are executed one after the other in the order in which they’re written. This process is called sequential execution (p. 104).
- Various Java statements enable you to specify that the next statement to execute is not necessarily the next one in sequence. This is called transfer of control (p. 104).
- Böhm and Jacopini demonstrated that all programs could be written in terms of only three control structures (p. 105)—the sequence structure, the selection structure and the repetition structure.
- The term “control structures” comes from the field of computer science. The *Java Language Specification* refers to “control structures” as “control statements” (p. 104).
- The sequence structure is built into Java. Unless directed otherwise, the computer executes Java statements one after the other in the order in which they’re written—that is, in sequence.
- Anywhere a single action may be placed, several actions may be placed in sequence.
- Activity diagrams (p. 105) are part of the UML. An activity diagram models the workflow (p. 105; also called the activity) of a portion of a software system.
- Activity diagrams are composed of symbols (p. 105)—such as action-state symbols, diamonds and small circles—that are connected by transition arrows, which represent the flow of the activity.
- Action states (p. 105) contain action expressions that specify particular actions to perform.
- The arrows in an activity diagram represent transitions, which indicate the order in which the actions represented by the action states occur.
- The solid circle located at the top of an activity diagram represents the activity’s initial state (p. 105)—the beginning of the workflow before the program performs the modeled actions.
- The solid circle surrounded by a hollow circle that appears at the bottom of the diagram represents the final state (p. 106)—the end of the workflow after the program performs its actions.
- Rectangles with their upper-right corners folded over are UML notes (p. 106)—explanatory remarks that describe the purpose of symbols in the diagram.
- Java has three types of selection statements (p. 106).
- The if single-selection statement (p. 106) selects or ignores one or more actions.
- The if...else double-selection statement selects between two actions or groups of actions.
- The switch statement is called a multiple-selection statement (p. 106) because it selects among many different actions or groups of actions.
- Java provides the while, do...while and for repetition (looping) statements that enable programs to perform statements repeatedly as long as a loop-continuation condition remains true.
- The while and for statements perform the action(s) in their bodies zero or more times—if the loop-continuation condition (p. 106) is initially false, the action(s) will not execute. The do...while statement performs the action(s) in its body one or more times.
- The words if, else, switch, while, do and for are Java keywords. Keywords cannot be used as identifiers, such as variable names.
- Every program is formed by combining as many sequence, selection and repetition statements (p. 106) as is appropriate for the algorithm the program implements.
- Single-entry/single-exit control statements (p. 106) are attached to one another by connecting the exit point of one to the entry point of the next. This is known as control-statement stacking.
- A control statement may also be nested (p. 106) inside another control statement.

### Section 4.5 if Single-Selection Statement

- Programs use selection statements to choose among alternative courses of action.
- The single-selection if statement’s activity diagram contains the diamond symbol, which indicates that a decision is to be made. The workflow follows a path determined by the symbol’s associated guard conditions (p. 107). If a guard condition is true, the workflow enters the action state to which the corresponding transition arrow points.
- The if statement is a single-entry/single-exit control statement.

### Section 4.6 if...else Double-Selection Statement

- The if single-selection statement performs an indicated action only when the condition is true.
- The if...else double-selection statement (p. 106) performs one action when the condition is true and a different action when the condition is false.
- The conditional operator (?:) is Java’s only ternary operator—it takes three operands. Together, the operands and the ?: symbol form a conditional expression (p. 108).
- A program can test multiple cases with nested if...else statements (p. 109).
- The Java compiler associates an else with the immediately preceding if unless told to do otherwise by the placement of braces.
- The if statement expects one statement in its body. To include several statements in the body of an if (or the body of an else for an if...else statement), enclose the statements in braces.
- A block (p. 111) of statements can be placed anywhere that a single statement can be placed.
- A logic error (p. 111) has its effect at execution time. A fatal logic error (p. 111) causes a program to fail and terminate prematurely. A nonfatal logic error (p. 111) allows a program to continue executing, but causes the program to produce incorrect results.
- Just as a block can be placed anywhere a single statement can be placed, you can also use an empty statement, represented by placing a semicolon (;) where a statement would normally be.

### Section 4.7 while Repetition Statement

- The while repetition statement (p. 112) allows you to specify that a program should repeat an action while some condition remains true.
