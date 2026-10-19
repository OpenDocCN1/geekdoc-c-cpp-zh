data, losing important changes, a possessed editor that saves programs incorrectly—you name it. This is “programming by superstition.”

If you have a problem with a program you’ve written, it’s your fault. It’s not the computer’s fault, and it’s not the compiler’s fault. The program doesn’t do something different every time. It didn’t write itself; you wrote it, so take responsibility for it.

![](bbox=[0.11, 0.23, 0.2, 0.31])

Even if an error at first appears not to be your fault, it’s strongly in your interest to assume that it is. That assumption helps you debug. It’s hard enough to find a defect in your code when you’re looking for it; it’s even harder when you assume your code is error-free. Assuming the error is your fault also improves your credibility. If you claim that an error arose from someone else’s code, other programmers will believe that you have checked out the problem carefully. If you assume the error is yours, you avoid the embarrassment of having to recant publicly later when you find out that it was your defect after all.

# 23.2 Finding a Defect

Debugging consists of finding the defect and fixing it. Finding the defect—and understanding it—is usually 90 percent of the work.

Fortunately, you don’t have to make a pact with Satan to find an approach to debugging that’s better than random guessing. Debugging by thinking about the problem is much more effective and interesting than debugging with an eye of a newt and the dust of a frog’s ear.

Suppose you were asked to solve a murder mystery. Which would be more interesting: going door to door throughout the county, checking every person’s alibi for the night of October 17, or finding a few clues and deducing the murderer’s identity? Most people would rather deduce the person’s identity, and most programmers find the intellectual approach to debugging more satisfying. Even better, the effective programmers who debug in one-twentieth the time used by the ineffective programmers aren’t randomly guessing about how to fix the program. They’re using the scientific method—that is, the process of discovery and demonstration necessary for scientific investigation.

# The Scientific Method of Debugging

Here are the steps you go through when you use the classic scientific method:

+   1. Gather data through repeatable experiments.
+   2. Form a hypothesis that accounts for the relevant data.
+   3. Design an experiment to prove or disprove the hypothesis.