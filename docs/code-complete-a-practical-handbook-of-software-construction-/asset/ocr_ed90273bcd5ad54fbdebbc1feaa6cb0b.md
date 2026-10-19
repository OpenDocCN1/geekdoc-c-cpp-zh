Cross-Reference For details on iteration, see Section 34.8, "Iterate, Repeatedly, Again and Again," later in this chapter.

Low-level processes matter, too. If you follow the process of writing pseudocode and then filling in the code around the pseudocode, you reap the benefits of designing from the top down. You’re also guaranteed to have comments in the code without having to put them in later.

Observing large processes and small processes means pausing to pay attention to how you create software. It’s time well spent. Saying that “code is what matters; you have to focus on how good the code is, not some abstract process” is shortsighted and ignores mountains of experimental and practical evidence to the contrary. Software development is a creative exercise. If you don’t understand the creative process, you’re not getting the most out of the primary tool you use to create software—your brain. A bad process wastes your brain cycles. A good process leverages them to maximum advantage.

# 34.3 Write Programs for People First, Computers Second

*your program* n. A maze of non sequiturs littered with clever-clever tricks and irrelevant comments. Compare MY PROGRAM.

*my program* n. A gem of algoristic precision, offering the most sublime balance between compact, efficient coding on the one hand and fully commented legibility for posterity on the other. Compare YOUR PROGRAM.

—Stan Kelly-Bootle

Another theme that runs throughout this book is an emphasis on code readability. Communication with other people is the motivation behind the quest for the Holy Grail of self-documenting code.

The computer doesn’t care whether your code is readable. It’s better at reading binary machine instructions than it is at reading high-level-language statements. You write readable code because it helps other people to read your code. Readability has a positive effect on all these aspects of a program:

+   - Comprehensibility
+   - Reviewability
+   - Error rate
+   - Debugging
+   - Modifiability
+   - Development time—a consequence of all of the above
+   - External quality—a consequence of all of the above