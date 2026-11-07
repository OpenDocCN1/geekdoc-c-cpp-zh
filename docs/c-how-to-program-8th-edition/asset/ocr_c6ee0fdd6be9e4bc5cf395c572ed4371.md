decision. This diagram also introduces the UML’s **merge symbol**, which joins two flows of activity into one flow of activity. The UML represents both the merge symbol and the decision symbol as diamonds. In this diagram, the merge symbol joins the transitions from the initial state and the action state, so they both flow into the decision that determines whether the loop should begin (or continue) executing. The decision and merge symbols can be distinguished by the number of “incoming” and “outgoing” transition arrows. A decision symbol has one transition arrow pointing to the diamond and two or more transition arrows pointing out from the diamond to indicate possible transitions from that point. In addition, each transition arrow pointing out of a decision symbol has a guard condition next to it. A merge symbol has two or more transition arrows pointing to the diamond and only one transition arrow pointing from the diamond, to indicate multiple activity flows merging to continue the activity. Unlike the decision symbol, the merge symbol does not have a counterpart in C++ code.

![](bbox=[0.143, 0.356, 0.857, 0.591])

**Fig. 4.6**  |  *while* repetition statement UML activity diagram.

The diagram of Fig. 4.6 clearly shows the repetition of the while statement discussed earlier in this section. The transition arrow emerging from the action state points to the merge, which transitions back to the decision that’s tested each time the loop until the guard condition product > 100 becomes true. Then the while statement exits (reaches its final state) and control passes to the next statement in sequence in the program.

**Performance Tip 4.3**

*A small performance improvement for code that executes many times in a loop can result in substantial overall performance improvement.*

# 4.8 Formulating Algorithms: Counter-Controlled Repetition

To illustrate how programmers develop algorithms, this section and Section 4.9 solve two variations of a class average problem. Consider the following problem statement:

*A class of ten students took a quiz. The grades (0 to 100) for this quiz are available to you. Calculate and display the total of the grades and the class average.*