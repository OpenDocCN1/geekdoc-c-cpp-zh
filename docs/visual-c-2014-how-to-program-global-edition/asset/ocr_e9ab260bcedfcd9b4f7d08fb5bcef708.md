# 5.9 Formulating Algorithms: Counter-Controlled Iteration

![](bbox=[0.223, 0.107, 0.773, 0.333])

**Fig. 5.7** | while iteration statement UML activity diagram.

next to it. A merge symbol has two or more transition arrows pointing to the diamond and only one pointing from the diamond, to indicate multiple activity flows merging to continue the activity. None of the transition arrows associated with a merge symbol has a guard condition.

5.7 clearly shows the iteration of the while statement discussed earlier in this section. The transition arrow emerging from the action state points back to the merge, from which program flows back to the decision that tested at the beginning of each iteration. The loop continues until the guard condition product > 100 becomes *true*. The while iteration statement exits (reaches its final state), and control passes to the next sequence in the app.

# 5.9 Formulating Algorithms: Counter-Controlled Iteration

To illustrate how algorithms are developed, we solve two variations of a problem that averages student grades. Consider the following problem statement:

> A class of 10 students took a quiz. The grades (integers in the range 0 to 100) for this quiz are available to you. Determine the class average on the quiz.

The class average is equal to the sum of the grades divided by the number of students. The algorithm for solving this problem on a computer must input each grade, keep track of the total of all grades entered, perform the averaging calculation and produce the result.

# 5.9.1 Pseudocode Algorithm with Counter-Controlled Iteration

Let's use pseudocode to list the actions to execute and specify the order in which they should execute. We use counter-controlled iteration to input the grade one at a time. This technique uses a variable counter (or control variable) to control the number of times a set of statements we execute. Counter-controlled iteration is often called definite iteration, because the number of iterations is known before the loop begins executing. In this example, iteration terminates when the counter exceeds 100. This section presents a fully developed pseudocode algorithm (Fig. 5.8) and a corresponding C# app (Fig. 5.9)