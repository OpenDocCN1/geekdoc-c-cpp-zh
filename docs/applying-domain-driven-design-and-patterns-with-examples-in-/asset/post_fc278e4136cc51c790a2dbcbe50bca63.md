
By the way, you shouldn't ask the customer if you should use TDD or not, at least not if you're asking for more payment/time/whatever at the same time. He will just tell you to do it right instead. When considering the project from start to finish, if using TDD incurs no extra cost, I believe you should just go ahead. The customer will be happy afterward when he gets the quality he expects.

## Note

Let's for a moment skip TDD and focus only on automatic tests.

A colleague of mine has been *extremely* skeptical of the need for automatic unit tests (created before or after real code). He told me that during his two-decade career, automatic unit tests would not have helped him once. However, I think he changed his mind a bit recently. We were working together on a project where he wrote a COM component in C++ and I wrote tests as specifications and as just tests. When we were done, the customer changed one thing in the requirements. My colleague made a small change, but the tests caught a bug that occurred just four times in 1,000 executions. The bug was found after only seconds of testing, compared to hours if it had been done manually. And if it had been done manually, the bug would most probably not have been found at all, but would have shown itself during production.

## The TDD Flow

Now I have tried to get you motivated to start with TDD, so let's have a closer look at how the process flows. (We'll get back to this in [Chapter 3](#) when we will investigate it in a bit more depth with a real world demo.) Assuming you have a decent idea about the requirements, the flow goes like this:

- First of all, you start writing a test. You make the test fail meaningfully so that you can be sure that the test is testing what you think. This is a simple and important rule, but even so, I have skipped over it several times and that is just asking for trouble.
- The second step is to write the simplest possible code that makes the test pass.
- The third step is to refactor if necessary, because you identify code that smells (for example, code duplication), and then you start all over again, adding another test.

If we use NUnit lingo, the first step should give you a red light/bar, and the second step should give you a green light/bar.

I mentioned refactoring previously and as the third step in the general process of TDD, and I think I should briefly explain the term a bit more.

## Refactoring

Continuous learning was something we heard about in school all the time. It's very much true in the case of refactoring [Fowler R] refactoring to get a better model, for example.

Refactoring is about making small, well-known changes step by step in order to improve the design of existing code. That is, to improve its maintainability without changing its observed behavior. Another way to say it is to change how, not what.

In a nutshell, what refactoring does is to take you from smelly code to nice code. It's as simple as that.

So you don't have to come up with a perfect design up-front. That is good news, because it can't be done anyway.

## Why Use Refactoring?

None of us have any trouble in recognizing smelly code. What might be more troublesome is to know when to fix it. As I see it, you should deal with the problem as soon as it arises. You should use refactoring because without continuous maintenance of your code, it will start to degenerate and crumble.

## Note

Mark Burhop said the following: "A good friend keeps a list of Software Development Laws. One goes something like "Code, left untouched, will develop bugs.""

Let's use the analogy of your home. Problems you choose to ignore, such as fixing windows, repairing the roof, painting the woodwork, and so on—ignored problems like these will grow in time. That's an immutable law. So sooner or later your house will fall to bits, and at that point it's worthless. Nobody wants that situation, right?

Software is different because it's not built of organic material and won't become affected from weather and wind if not changed. Still, we intuitively have a feeling for what's happening over time with software when refactoring isn't applied during bug fixes and when the software is extended.

## How Should I Use Refactoring?

Refactoring can be used in all phases of the application lifecycle; for instance, during development of the first version of an application. But just assume we don't use refactoring, but an up-front, traditional design heavy process instead (now often referred to as Big Design Up-Front, BDUF). We will spend quite a lot of time on initial detailed design, creating loads of detailed UML diagrams, but as a result we will expect the development to go very smoothly and quickly. Even assuming that it does, there is still a risk that the code will be, well, smelly.

Instead, let's say we just accept the fact that we can't get it right up front the first time. In this case, a slightly different approach is to move some of the effort from initial detailed design over to development instead (and of course all development, especially in this case, *is design*) and to be prepared for doing refactoring continuously when we learn more. Learning more is exactly what we do during development, and as I see it, this approach results in higher quality code.

So instead of doing too much guessing, we do more learning and proofing!

## Note

I was probably overly positive to BDUF so as to not distract you from the point that I was after regarding smell code. Doing a lot of guesswork on day one will often lead to wasted time because it is just guesswork.

My friend Jimmy Ekbäck commented on this by saying, "BDUF can be even worse than wasted time because of incorrect guesses. BDUF can also lead to self-fulfilled prophecies."

## Refactoring + TDD = True

In order to be able to use refactoring in a safe way, you *must* carry out extensive tests. If you don't, you will introduce bugs and/or you will prioritize, not making any changes simply for the sake of maintainability, because the risk of introducing bugs is just too large. And when you stop making changes because of maintainability, your code has slowly started to degrade.

## Note

You will find much more coverage, with focus on hands-on examples, about both TDD and Refactoring in [Chapter 3](Chapter 3).

It's a good idea to use TDD and refactoring for bugfixing also. First expose the bug with a red test, then solve the bug so you get green, and then refactor.

## Which Ingredient or a Combination?

Again, I'm sure many of you are wondering which way to go. For instance, should you focus on up-front design or TDD?

As I see it, you can mix up-front design and TDD successfully. For example, set up some up-front architecture, work with Domain-Driven Design, and for each piece of behavior build it with TDD (including refactoring). Then go back to your architecture and change it in accordance with what you have learned. Then work with Domain-Driven Design, and continue like that.

A good starting point for learning more about continuous integration is a paper written by Martin Fowler and Matthew Foemmel called "Continuous Integration" [Fowler/Foemmel CI].

Thanks, Claudio! Now let's move on to some operational aspects.

![](img/89fb3513cb9b6343875aadbfd042005d_63_0.png)

![](img/89fb3513cb9b6343875aadbfd042005d_63_1.png)

## Note

If you have the possibility of using *Aspect-Oriented Programming (AOP)*, it might not take more than a few minutes to add tracing afterward. We will discuss AOP quite a lot in Chapter 10, "Design Techniques to Embrace."

## Tracing in Place

If you have a working tracing solution in place, you know how efficient it might be to find and solve the problem instead. The days-long delay is gone, and you are on the way to tracking down the problem in minutes.

So it's important to be careful and not think "You Aren't Going to Need It" (YAGNI) too often when it comes to operational mechanisms. Using YAGNI often will cost too much when it comes to adding the mechanism if (or rather when) you will need it. Remember, the idea with YAGNI is that the cost of adding something is pretty much the same now and later, in which case you can always wait until you really need it. When the cost is low now and high later, and there's a good chance you will need it, you should make a different decision.

## Some Examples of Operational Mechanisms

Here I have listed a short number of operational mechanisms that can be considered for most enterprise scale applications:

- **Tracing**

  As we just discussed, it's nice to be able to listen to what is going on at the same time as users run scenarios in the system. This is not only a very efficient solution for tracking down bugs, but it can be used for investigating where the bottlenecks are located, for example.

- **Logging**

  Errors, warnings, and information messages must be logged. This is extremely important for investigating problems after they have occurred. We can't expect the users to write down the exact messages for us. It might also be that we want to collect information that we don't want to show to the users.

- **Config**

  Have you had to recompile old applications just because the database server was switched to a new machine with a new name? I have. Of course, that kind of information should be configurable and depending on the application, this might be the case for loads of information.

- **Performance monitoring**
