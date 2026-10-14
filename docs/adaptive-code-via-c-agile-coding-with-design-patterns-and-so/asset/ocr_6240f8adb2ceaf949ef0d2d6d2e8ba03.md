# Chapter 4. Unit testing and refactoring

# After completing this chapter, you will be able to

+   - Define unit testing and refactoring and explain why both are very useful techniques.
+   - Understand how unit testing and refactoring are intrinsically linked.
+   - Write code in a test-first fashion, focusing on implementing only that which the tests require.
+   - Refactor production code to improve its overall design.
+   - Recognize overspecified unit tests and refactor them.

This chapter focuses on two different techniques that are current programming best practices: unit testing and refactoring.

Unit testing is the discipline of writing code that tests other code. Unit tests themselves, being source code, can be compiled and executed. As each unit test runs, it reports the test’s success or failure with a simple true or false, often a green or a red visual indicator. If all of the unit tests pass, the production code that they test is considered to possibly be working. If even a single unit test fails—out of possibly thousands—the production code overall is deemed to certainly be broken.

Refactoring is the process of incrementally improving the design of existing code. It is analogous to writing various drafts of code, much like I have written various drafts of this book. By acknowledging that we developers rarely get things right the first time, refactoring frees us to do the simplest thing first and gradually, through incremental improvements, arrive at a better solution later.

The freedom to refactor with impunity is made possible by unit testing. When you unit test as early as possible in the process—that is, before you write any production code—you create a safety net to catch any subsequent errors when you refactor code. If a unit test transitions from a passing state to a failing state, you know that the last change you made is responsible for breaking the code. The process of writing unit tests and then refactoring toward better design is an upward spiral whereby the code quality increases while you simultaneously make progress with implementing new features.

# Unit testing

To some degree, unit testing should be considered a mandatory part of every programmer’s daily discipline. For some developers, the ideal situation is when production code—the code that forms the basis of the software product—is entirely the result of the tests that were written to verify the application’s behavior. Later in this chapter, you will learn how this can be achieved through test-driven development, but bear in mind that the aim is to be pragmatic rather than purist: it is surely better to ship something and accept some prudent technical debt than it is to be late for the sake of writing more unit tests. That said, every project is unique in its tolerance for timeliness versus completeness.

There are some recognized unit testing patterns and guidelines that will result in repeatable success. These patterns and guidelines are no longer new but expected, tried, and tested. The arrangement and naming of unit tests and, most of all, how to ensure the testability of the code are all primary concerns. If these concerns are neglected, unit tests will no longer be synchronized with the code that they test, test failures will be tolerated, and the safety net will wither and break.