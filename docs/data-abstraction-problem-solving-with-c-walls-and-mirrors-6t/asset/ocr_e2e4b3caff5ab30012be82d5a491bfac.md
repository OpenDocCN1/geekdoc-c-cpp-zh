# Prerequisites

+   - Appendix A Review of C++ Fundamentals
+   - Chapter 1 Data Abstraction: The Walls

What are the specific characteristics of good solutions? How can you construct good solutions? This appendix provides some answers to these very difficult questions.

The programming themes that we will discuss should be familiar to you. However, the novice programmer usually does not truly appreciate their importance. After the first course in programming, many students still simply want to “get the thing to run.” The discussion that follows should help you realize just how important these themes really are.

People read programs, too

One of the most widespread misconceptions held by novice programmers is that a computer program is “read” only by a computer. As a consequence, they tend to consider only whether the computer is able to “understand” the program—that is, does the program compile, execute, and produce the correct output? The truth is, of course, that other people often must read and modify programs. In a typical programming environment, many individuals share a program. One person may write a program, which other people use in conjunction with other programs written by other people, and a year later, a different person may modify the program. It is therefore essential that you take great care to design a program that is easy to read and understand.

Key programming themes

You should always keep in mind the following seven themes of programming: modularity, style, modifiability, ease of use, fail-safe programming, debugging, and testing.

# B.1 Modularity

Modularity facilitates programming

As this book continually emphasizes, you should strive for modularity in all phases of the problem-solving process, beginning with the initial design of a solution. Many programming tasks become more difficult as the size and complexity of a program grows. Modularity slows the rate at which the level of difficulty grows. More specifically, modularity has a favorable impact on the following aspects of programming:

+   - **Constructing the program.** The primary difference between a small modular program and a large modular program is simply the number of modules each contains. Because the modules are independent, writing one large modular program is not very different from writing many small, independent programs, although the interrelationships among modules make the design much more complicated. On the other hand, working on a large nonmodular program is more like working on many interrelated programs simultaneously. Modularity also permits team programming, in which several programmers work independently on their own modules before combining them into one program.

Modularity isolates errors

+   - **Debugging the program.** Debugging a large program can be a monstrous task. Imagine that you try a 10,000-line program and eventually get it to compile. Neither of these tasks would be much fun. Now imagine that you execute your program, and after a few hundred lines of output, you notice an incorrect number. You should anticipate spending the next day or so tracing through the intricacies of your program before discovering a problem such as an array index that is too large. A great advantage of modularity is that the task of debugging a large program is reduced to one of debugging many small programs. When you begin to code a module, you should be almost certain that all other modules coded so far are correct. That is, before you consider a module finished, you should test it extensively, but separately and in context with the other modules, by calling it with actual arguments carefully chosen to induce all possible behaviors of the modules. If this testing is done thoroughly, you can feel fairly sure that any problem is a result of an error in the last module added. *Modularity isolates errors.*