# 06
Sequence Control in C

# OBJECTIVES

+   - Explain Decision Structure

**W**e have mentioned in Chapter 1 of this book that a program is always executed in a sequence from top to bottom. The statements are executed one after the other sequentially in the order that they appear in a C program. The compiler by default transfers the control to the next statement once the execution of current statement is finished. In practical scenario, this sequential flow does not work. We at times need to change the sequence of execution based on certain conditions, or may need to execute certain set of statements repeatedly. In this chapter, we will learn about a control structure used to alter the flow of execution. This control structures is called a decision structure. We will also discuss about different variants of the decision structure and see how to use them in a program.

# 6.1
Decision Structure

The decision structure of C language is used to make selections. Selection allows us to choose option from two or more options available within the program. In C language, decision structures allow us to perform predefined actions based on the results of one or more conditions. C language provides two types of selection statements, called two-way selection and multiway selection. The next section discusses about the two-way selection.

# • The Two-Way Selection

A two-way selection in C language represents a conditional statement that can be evaluated as true or false by the compiler. The true answer leads to the execution of one or more action statements. In case of answer being false, the other set of action statements is executed. A general flowchart of the two-way selection is shown in Figure 1:

![](bbox=[0.33, 0.71, 0.71, 0.83])

▲ Figure 1: Flowchart of a Two-Way Selection