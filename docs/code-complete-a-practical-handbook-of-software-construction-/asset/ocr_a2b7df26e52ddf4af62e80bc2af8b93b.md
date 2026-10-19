Pseudocode makes changes easier. A few lines of pseudocode are easier to change than a page of code. Would you rather change a line on a blueprint or rip out a wall and nail in the two-by-fours somewhere else? The effects aren’t as physically dramatic in software, but the principle of changing the product when it’s most malleable is the same. One of the keys to the success of a project is to catch errors at the “least-value stage,” the stage at which the least effort has been invested. Much less has been invested at the pseudocode stage than after full coding, testing, and debugging, so it makes economic sense to catch the errors early.

Pseudocode minimizes commenting effort. In the typical coding scenario, you write the code and add comments afterward. In the PPP, the pseudocode statements become the comments, so it actually takes more work to remove the comments than to leave them in.

Pseudocode is easier to maintain than other forms of design documentation. With other approaches, design is separated from the code, and when one changes, the two fall out of agreement. With the PPP, the pseudocode statements become comments in the code. As long as the inline comments are maintained, the pseudocode’s documentation of the design will be accurate.

![](bbox=[0.138, 0.441, 0.213, 0.506])

As a tool for detailed design, pseudocode is hard to beat. One survey found that programmers prefer pseudocode for the way it eases construction in a programming language, for its ability to help them detect insufficiently detailed designs, and for the ease of documentation and ease of modification it provides (Ramsey, Atwood, and Van Doren 1983). Pseudocode isn’t the only tool for detailed design, but pseudocode and the PPP are useful tools to have in your programmer’s toolbox. Try them. The next section shows you how.

# 9.3 Constructing Routines by Using the PPP

This section describes the activities involved in constructing a routine, namely these:

+   - Design the routine.
+   - Code the routine.
+   - Check the code.
+   - Clean up loose ends.
+   - Repeat as needed.

# Design the Routine

Once you’ve identified a class’s routines, the first step in constructing any of the class’s more complicated routines is to design it. Suppose that you want to write a routine to