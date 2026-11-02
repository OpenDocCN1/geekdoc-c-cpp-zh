4. Click OK to save the changes.

You’ll no longer receive warnings on scanf (or any other functions that Microsoft has deprecated for similar reasons). For industrial-strength coding, disabling the warnings is discouraged. We’ll say more about how to use scanf_s and printf_s in a later Secure C Coding Guidelines section.

# Summary

# Section 3.1 Introduction

+   - Before writing a program to solve a particular problem, you must have a thorough understanding of the problem and a carefully planned approach to solving the problem.

# Section 3.2 Algorithms

+   - The solution to any computing problem involves executing a series of actions in a specific order (p. 102).
+   - A procedure (p. 102) for solving a problem in terms of the actions (p. 102) to be executed, and the order in which these actions are to be executed, is called an algorithm (p. 102).
+   - The order in which actions are to be executed is important.

# Section 3.3 Pseudocode

+   - **Pseudocode** (p. 102) is an artificial and informal language that helps you develop algorithms.
+   - Pseudocode is similar to everyday English; it’s not an actual computer programming language.
+   - Pseudocode programs help you “think out” a program.
+   - Pseudocode consists purely of “characters”; you may type pseudocode using a text editor.
+   - Carefully prepared pseudocode programs may be converted easily to corresponding C programs.
+   - Pseudocode consists only of action statements.

# Section 3.4 Control Structures

+   - Normally, statements in a program execute one after the other in the order in which they’re written. This is called sequential execution (p. 103).
+   - Various C statements enable you to specify that the next statement to execute may be other than the next one in sequence. This is called transfer of control (p. 103).
+   - Structured programming has become almost synonymous with **“goto elimination”** (p. 103).
+   - Structured programs are clearer, easier to debug and modify and more likely to be bug free.
+   - All programs can be written in terms of sequence, selection and iteration control structures (p. 103).
+   - Unless directed otherwise, the computer automatically executes C statements in sequence.
+   - A flowchart (p. 104) is a graphical representation of an algorithm. Flowcharts are drawn using rectangles, diamonds, rounded rectangles and small circles, connected by arrows called flow-lines (p. 104).
+   - The rectangle (action) symbol (p. 104) indicates any type of action including a calculation or an input/output operation.
+   - Flowlines indicate the order in which the actions are performed.
+   - When drawing a flowchart that represents a complete algorithm, we use as the first symbol a rounded rectangle containing the word “Begin.” We use as the last symbol a rounded rectangle