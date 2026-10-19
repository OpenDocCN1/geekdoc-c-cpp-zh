# Chapter 23

# Debugging

# Contents

+   - 23.1 Overview of Debugging Issues: page 535
+   - 23.2 Finding a Defect: page 540
+   - 23.3 Fixing a Defect: page 550
+   - 23.4 Psychological Considerations in Debugging: page 554
+   - 23.5 Debugging Tools—Obvious and Not-So-Obvious: page 556

# Related Topics

+   - The software-quality landscape: Chapter 20
+   - Developer testing: Chapter 22
+   - Refactoring: Chapter 24

> Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.
> —Brian W. Kernighan

Debugging is the process of identifying the root cause of an error and correcting it. It contrasts with testing, which is the process of detecting the error initially. On some projects, debugging occupies as much as 50 percent of the total development time. For many programmers, debugging is the hardest part of programming.

Debugging doesn’t have to be the hardest part. If you follow the advice in this book, you’ll have fewer errors to debug. Most of the defects you’ll have will be minor oversights and typos, easily found by looking at a source-code listing or stepping through the code in a debugger. For the remaining harder bugs, this chapter describes how to make debugging much easier than it usually is.

# 23.1 Overview of Debugging Issues

The late Rear Admiral Grace Hopper, co-inventor of COBOL, always said that the word “bug” in software dated back to the first large-scale digital computer, the Mark I (IEEE 1992). Programmers traced a circuit malfunction to the presence of a large moth that had found its way into the computer, and from that time on, computer problems were blamed on “bugs.” Outside software, the word “bug” dates back at least to Thomas Edison, who is quoted as using it as early as 1878 (Tenner 1997).

The word “bug” is a cute word and conjures up images like this one: