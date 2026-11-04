# CHAPTER 27

# Diagnostics and Instrumentation

# IN THIS CHAPTER

+   - Ensuring Code Quality 1364
+   - Instrumentation 1378
+   - Controlling Processes 1386

Writing high-quality software should be a no-brainer. It's also common wisdom that catching bugs early during development is beneficial to reduce cost and user frustration. Luckily, .NET comes armed with a whole series of tools, built in to the framework and otherwise, that help the developer achieve those goals.

In this chapter, we focus on code quality from different angles. To start, we look at various development-time tools and techniques that help keep up a high-quality standard. Those include code analysis and FxCop, various Visual Studio tools, and simple but effective techniques such as writing code with asserts. Starting from .NET 4, code contracts extend upon such tools, allowing developers to write down, analyze, and enforce conditions the code should obey.

One thing we don't cover here is the extended tooling available in Visual Studio to do test-driven development (TDD). Although I'm a firm believer in taking such an approach, having some continuous monitoring of potential code regressions and code coverage, we simply don't have the space to do the subject justice. (You can find any numbers of books devoted to TDD and the use of Visual Studio tools to achieve this.)

Being able to catch problems early is one thing, but there will always be cases where deployed and running software needs to be checked for mishaps and debugged accordingly. Various classes that can be found in the System.Diagnostics namespace help to build better code that's instrumented to make such production analysis easier to accomplish. In particular, we talk about event logging,