# ### Flowcharts

A flowchart is a *graphical representation* of an algorithm or of a portion of an algorithm. Flowcharts are drawn using certain special-purpose symbols such as *rectangles*, *diamonds*, *rounded rectangles*, and *small circles*; these symbols are connected by arrows called flowlines.

Like pseudocode, flowcharts are useful for developing and representing algorithms, although pseudocode is preferred by most programmers. Flowcharts clearly show how control structures operate; that's what we use them for in this text.

Consider the flowchart for the sequence structure in Fig. 3.1. We use the rectangle symbol, also called the action symbol, to indicate any type of action including a calculation or an input/output operation. The flowlines in the figure indicate the *order* in which the actions are performed—first, grade is added to total, then 1 is added to counter. C allows us to have as many actions as we want in a sequence structure. As we'll soon see, *anywhere a single action may be placed, we may place several actions in sequence.*

![](bbox=[0.31, 0.405, 0.765, 0.595])

**Fig. 3.1** | Flowcharting C's sequence structure.

When drawing a flowchart that represents a complete algorithm, the first symbol we use is a rounded rectangle symbol containing the word *“Begin.”* The last symbol is a rounded rectangle containing the word *“End.”* When drawing only a *portion* of an algorithm as in Fig. 3.1, we omit the rounded rectangle symbols in favor of using small circle symbols, also called connector symbols.

Perhaps the most important flowcharting symbol is the diamond symbol, also called the decision symbol, which indicates that a *decision* is to be made. We'll discuss the diamond symbol in the next section.

# ### Selection Statements in C

C provides three types of selection structures in the form of statements. The `if` selection statement (Section 3.5) either *selects* (performs) an action if a condition is *true* or *skips* the action if the condition is *false*. The `if...else` selection statement (Section 3.6) performs an action if a condition is *true* and performs a different action if the condition is *false*. The `switch` selection statement (discussed in Chapter 4) performs one of *many* different actions, depending on the value of an expression. The `if` statement is called a single-selection statement because it selects or ignores a single action. The `if...else` statement is called a double-selection statement because it selects between two different actions. The `switch` statement is called a multiple-selection statement because it selects among many different actions.