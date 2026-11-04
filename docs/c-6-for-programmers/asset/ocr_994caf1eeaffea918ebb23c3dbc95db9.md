resents both the merge symbol and the decision symbol as diamonds. The merge symbol joins multiple flows of activity into one. In this diagram, the merge symbol joins the transitions from the initial state and from the action state, so they both flow into the decision that determines whether the loop should begin (or continue) executing.

![](bbox=[0.2, 0.27, 0.85, 0.52])

Fig. 5.6 | while iteration statement UML activity diagram.

The decision and merge symbols can be distinguished by the number of “incoming” and “outgoing” transition arrows. A decision symbol has one transition arrow pointing to the diamond and two or more pointing out from it to indicate possible transitions from that point. In addition, each transition arrow pointing out of a decision symbol has a guard condition next to it. A merge symbol has two or more transition arrows pointing to the diamond and only one pointing from the diamond, to indicate multiple activity flows merging to continue the activity. None of the transition arrows associated with a merge symbol has a guard condition.

Figure 5.6 clearly shows the iteration of the while statement discussed earlier in this section. The transition arrow emerging from the action state points back to the merge, from which program flow transitions back to the decision that’s tested at the beginning of each iteration of the loop. The loop continues executing until the guard condition product > 100 becomes true. Then the while statement exits (reaches its final state), and control passes to the next statement in sequence in the app.

# 5.7 Counter-Controlled Iteration

Consider the following problem statement:

A class of 10 students took a quiz. The grades (integers in the range 0 to 100) for this quiz are available to you. Determine the class average on the quiz.

The class average is equal to the sum of the grades divided by the number of students. The app must input each grade, keep track of the total of all grades entered, perform the averaging calculation and print the result.

We use counter-controlled iteration to input the grades one at a time. In this example, iteration terminates when the counter exceeds 10.