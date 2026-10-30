This is how the test setup should read. There is far more clarity in what you can expect from the system under test. Look back again at the original Arrange section of this test and see how it compares. The details of mock setup—implementation details—cloud the intent of the code. Look at the placement of the parameterized values: 200m and "Trading Account". They are lost within the noise of mock initialization. With the use of the Builder pattern, the tests now have far more clarity of intent.

Tip Another advantage of the Builder pattern is that it leads to more declarative tests. No test should ever have a cyclomatic complexity greater than 1, meaning that tests should be completely linear with no branching. An if statement or a for, foreach, or while loop will cause the cyclomatic complexity of a test to exceed 1. The Builder pattern helps with this by converting imperative construction and initialization to declarative.

# Writing tests first

What has been presented so far in this chapter are the merits of unit testing with a test-driven development (TDD) approach. But is this, strictly speaking, test-driven development? Software development is fraught with overloaded terms whose meaning is subjective or shifts over time. Consider the word "service," for example. That means a multitude of different things in different situations. This book alone uses the term in a number of different contexts. And context is the key. Without context, there is no basis for discussion, no environment in which debate can exist.

TDD might not necessarily be a subjective term, but its meaning has shifted. The modern standards and practices that are upheld as "software engineering" have trickled through the industry, and their meaning has been distorted or mistaken.

# What is TDD?

Test-driven development has a purist and a pragmatist interpretation. Even those terms are loaded: a purist never yields from his or her myopic, idealistic vision of how things ought to be; the pragmatist is a maverick who cuts corners and dilutes the code in the name of delivery. Of course, both of these descriptions are hyperbolic caricatures.

The "purist" idea of TDD is that it is a design tool—that developers should approach the keyboard without forethought of the production code they might implement. Instead, they are the proverbial blank slates, prepared to discover their design as they progress. This progress is guided by writing failing unit tests.

The "pragmatic" idea of TDD is that developers write the unit tests first. The distinction is subtle. With purist TDD, there are more constraints to the process. The goal of both TDD styles is the same: generate production code that has been verified as meeting requirements with unit tests. However, pragmatic TDD has fewer rules governing how to achieve this goal. With pragmatic TDD, the only rule is this: write tests first.