The top is, in effect, a complete representation of a program. Unfortunately, the top rarely conveys sufficient detail from which to write a Java program. So we now begin the refinement process. We divide the top into a series of smaller tasks and list these in the order in which they’ll be performed. This results in the following first refinement:

+   Initialize variables
+   Input, sum and count the quiz grades
+   Calculate and print the class average

This refinement uses only the sequence structure—the steps listed should execute in order, one after the other.

# Software Engineering Observation 4.2

Each refinement, as well as the top itself, is a complete specification of the algorithm—only the level of detail varies.

# Software Engineering Observation 4.3

Many programs can be divided logically into three phases: an initialization phase that initializes the variables; a processing phase that inputs data values and adjusts program variables accordingly; and a termination phase that calculates and outputs the final results.

# Proceeding to the Second Refinement

The preceding Software Engineering Observation is often all you need for the first refinement in the top-down process. To proceed to the next level of refinement—that is, the second refinement—we commit to specific variables. In this example, we need a running total of the numbers, a count of how many numbers have been processed, a variable to receive the value of each grade as it’s input by the user and a variable to hold the calculated average. The pseudocode statement

Initialize variables

can be refined as follows:

+   Initialize total to zero
+   Initialize counter to zero

Only the variables total and counter need to be initialized before they’re used. The variables average and grade (for the calculated average and the user input, respectively) need not be initialized, because their values will be replaced as they’re calculated or input.

The pseudocode statement

Input, sum and count the quiz grades

requires a repetition structure (i.e., a loop) that successively inputs each grade. We do not know in advance how many grades are to be processed, so we’ll use sentinel-controlled repetition. The user enters grades one at a time. After entering the last grade, the user enters the sentinel value. The program tests for the sentinel value after each grade is input and terminates the loop when the user enters the sentinel value. The second refinement of the preceding pseudocode statement is then