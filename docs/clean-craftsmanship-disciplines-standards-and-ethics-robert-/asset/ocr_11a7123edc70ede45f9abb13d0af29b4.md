humans are not good at doing two things at once. If we focus on writing a failing test, it’s not likely to be a well-written test. If we focus on writing production code that passes the test, it is not likely to be good production code. If we focus on the behavior we want, we will not be focusing on the structure we want.

Don’t fool yourself. You cannot do both at once. It is hard enough to get code to behave the way you want it to. It is too hard to write it to behave *and* have the right structure. Thus, we follow Kent Beck’s advice:

> > *First make it work. Then make it right.*

Therefore, we add a new law to the three laws of TDD: the law of refactoring. First you write a small amount of failing test code. Then you write a small amount of passing production code. Then you clean up the mess you just made.

The traffic light gets a new color: red → green → refactor ([Figure 2.1](#figure-2-1)).

![](bbox=[0.26, 0.432, 0.68, 0.646])

**Figure 2.1** Red → green → refactor

You’ve likely heard of refactoring, and as I said earlier, we’ll be spending a great deal of time on it in coming chapters. For now, let me dispel a few myths and misconceptions:

+   - Refactoring is a constant activity. Every time around the TDD cycle, you clean things up.