# **Figure 9**
**The Software Development Process**

![](bbox=[0.12, 0.11, 0.25, 0.51])

A method is *unambiguous* when there are precise instructions for what to do at each step and where to go next. There is no room for guesswork or creativity. A method is *executable* when each step can be carried out in practice. Had we asked to use the actual interest rate that will be charged in years to come, and not a fixed rate of 5 percent per year, our method would not have been executable, because there is no way for anyone to know what that interest rate will be. A method is *terminating* if it will eventually come to an end. In our example, it requires a bit of thought to see that the method will not go on forever. With every step, the balance goes up by at least $500, so eventually it must reach $20,000.
A sequence of steps that is unambiguous, executable, and terminating is called an **algorithm**. We have found an algorithm to solve our investment problem, and thus we can find the solution by programming a computer. The existence of an algorithm is an essential prerequisite for programming a task. You need to first discover and describe an algorithm for the task that you want to solve before you start programming (see Figure 9).

![](bbox=[0.7, 0.26, 0.9, 0.47])

*An algorithm is a recipe for finding a solution.*

> An algorithm for solving a problem is a sequence of steps that is unambiguous, executable, and terminating.

![](bbox=[0.12, 0.67, 0.25, 0.73])

20. Suppose the interest rate was 20 percent. How long would it take for the investment to double?

21. Suppose your cell phone carrier charges you $29.95 for up to 300 minutes of calls, and $0.45 for each additional minute, plus 12.5 percent taxes and fees. Give an algorithm to compute the monthly charge from a given number of minutes.

22. Consider the following pseudocode for finding the most attractive photo from a sequence of photos:

```
**Pick the first photo and call it "the best so far".**
**For each photo in the sequence**
  **If it is more attractive than the "best so far"**
    **Discard "the best so far".**
    **Call this photo "the best so far".**
**The photo called "the best so far" is the most attractive photo in the sequence.**
```

Is this an algorithm that will find the most attractive photo?