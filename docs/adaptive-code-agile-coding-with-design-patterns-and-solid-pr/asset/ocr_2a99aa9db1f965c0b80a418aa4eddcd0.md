# Chapter 5: Testing [NEW]

Unit testing is a non-negotiable prerequisite to any software project. Closely related to refactoring, the two practices work in unison to produce adaptive code. Without the safety net of unit tests, refactoring is prone to error; without refactoring, code becomes unwieldy, rigid, and hard to comprehend. This chapter takes an example of unit testing from humble beginnings and expands it to use more advanced—but practical—features such as fluent assertions, test-driven development, and mocking.

# Chapter 6: Refactoring [NEW]

To refactor is to improve the design of code after it has been written. This chapter gives examples of real-world refactors that improve the readability and maintainability of source code. Code must have tests so that it can be safely refactored, but this chapter also covers how to add tests to existing code so that it can be safely refactored.

# Part III: SOLID code

This chapter builds on the foundations laid in Part II. Each chapter is devoted to examining one principle of SOLID. The emphasis in these chapters is on practical examples for implementing the principles, rather than solely on the theory of why they are important. By placing each example in a real-world context, the chapters in this part of the book clearly demonstrate the utility of SOLID.

# Chapter 7: The single responsibility principle

This chapter shows how to implement the single responsibility principle in practice by using the Decorator and Adapter patterns. The outcome of applying the principle is an increase in the number of classes and a decrease in the size of those classes. The chapter shows that, in contrast with monolithic classes that provide extensive features, these smaller classes are more directed and focused on solving only a small part of a larger problem. It is in their aggregation that these classes then become more than the sum of their parts.

# Chapter 8: The open/closed principle

The open/closed principle (OCP) is simply stated, but it can have a significant impact on code. It is responsible for ensuring that code that follows the SOLID principles is only appended to and never edited. This chapter also discusses the concept of predicted variation in relation to OCP and explores how it can help developers identify extension points for further adaptability.