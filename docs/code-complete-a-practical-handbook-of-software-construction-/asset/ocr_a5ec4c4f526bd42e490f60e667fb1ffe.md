+   - Rewrite the code to use a status variable (in Section 17.3)
+   - Use guard clauses to exit a routine and make the nominal path through the code clearer (in Section 17.1)
+   - Use exceptions (Section 8.4)
+   - Redesign deeply nested code entirely (this section)

# 19.5 A Programming Foundation: Structured Programming

The term “structured programming” originated in a landmark paper, “Structured Programming,” presented by Edsger Dijkstra at the 1969 NATO conference on software engineering (Dijkstra 1969). By the time structured programming came and went, the term “structured” had been applied to every software-development activity, including structured analysis, structured design, and structured goofing off. The various structured methodologies weren’t joined by any common thread except that they were all created at a time when the word “structured” gave them extra cachet.

The core of structured programming is the simple idea that a program should use only one-in, one-out control constructs (also called single-entry, single-exit control constructs). A one-in, one-out control construct is a block of code that has only one place it can start and only one place it can end. It has no other entries or exits. Structured programming isn’t the same as structured, top-down design. It applies only at the detailed coding level.

A structured program progresses in an orderly, disciplined way, rather than jumping around unpredictably. You can read it from top to bottom, and it executes in much the same way. Less disciplined approaches result in source code that provides a less meaningful, less readable picture of how a program executes in the machine. Less readability means less understanding and, ultimately, lower program quality.

The central concepts of structured programming are still useful today and apply to considerations in using break, continue, throw, catch, return, and other topics.

# The Three Components of Structured Programming

The next few sections describe the three constructs that constitute the core of structured programming.

# Sequence

A sequence is a set of statements executed in order. Typical sequential statements include assignments and calls to routines. Here are two examples:

> Cross-Reference For details on using sequences, see Chapter 14, “Organizing Straight-Line Code.”