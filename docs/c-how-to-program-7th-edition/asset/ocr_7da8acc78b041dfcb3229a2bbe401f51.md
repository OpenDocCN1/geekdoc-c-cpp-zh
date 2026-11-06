**Common Programming Error 4.1**  
*Using a keyword as an identifier is a syntax error.*

**Common Programming Error 4.2**  
*Spelling a keyword with any uppercase letters is a syntax error. All of C++’s keywords contain only lowercase letters.*

# Summary of Control Statements in C++

C++ has only three kinds of control structures, which from this point forward we refer to as control statements: the sequence statement, selection statements (three types—if, if…else and switch) and repetition statements (three types—while, for and do…while). Each program combines as many of these control statements as is appropriate for the algorithm the program implements. We can model each control statement as an activity diagram with an initial state and a final state that represent a control statement’s entry point and exit point, respectively. These single-entry/single-exit control statements make it easy to build programs—control statements are attached to one another by connecting the exit point of one to the entry point of the next. This is similar to the way a child stacks building blocks, so we call this control-statement stacking. We’ll learn shortly that there is only one other way to connect control statements—called control-statement nesting, in which one control statement is contained inside another. Thus, algorithms in C++ programs are constructed from only three kinds of control statements, combined in only two ways.

**Software Engineering Observation 4.1**  
*Any C++ program we’ll ever build can be constructed from only seven different types of control statements (sequence, if, if…else, switch, while, do…while and for) combined in only two ways (control-statement stacking and control-statement nesting).*

# 4.5 if Selection Statement

Programs use selection statements to choose among alternative courses of action. For example, suppose the passing grade on an exam is 60. The pseudocode statement

> If student’s grade is greater than or equal to 60  
> &emsp;&emsp;&emsp;&emsp;Print “Passed”

determines whether the condition “student’s grade is greater than or equal to 60” is true or false. If the condition is true, “Passed” is printed and the next pseudocode statement in order is “performed” (remember that pseudocode is not a real programming language). If the condition is false, the print statement is ignored and the next pseudocode statement in order is performed. The indentation of the second line is optional, but it’s recommended because it emphasizes the inherent structure of structured programs.

**Good Programming Practice 4.1**  
*Consistently applying reasonable indentation conventions throughout your programs greatly improves program readability. We suggest three blank lines between statements. Some people prefer using tabs, but these can vary across editors, causing a program written on one editor to align differently when used with another.*