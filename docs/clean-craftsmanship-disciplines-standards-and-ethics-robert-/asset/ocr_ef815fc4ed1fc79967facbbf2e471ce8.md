production of complex documents whose accuracy, at the level of individual symbols, is critical.

Accountants and programmers may not want to admit it, but they are of a kind. And the discipline of the older profession should be well observed by the younger.

As you will see in what follows, TDD *is* double-entry bookkeeping. It is the same discipline, executed for the same purpose, and delivering the same results. Everything is said twice, in complementary accounts that must be kept in balance by keeping the tests passing.

# ## The Three Laws of TDD

Before we get to the three laws, we have some preliminaries to cover.

The essence of TDD entails the discipline to do the following:

+   1. Create a test suite that enables refactoring and is trusted to the extent that passage implies deployability. That is, if the test suite passes, the system can be deployed.
+   2. Create production code that is decoupled enough to be testable and refactorable.
+   3. Create an extremely short-cycle feedback loop that maintains the task of writing programs with a stable rhythm and productivity.
+   4. Create tests and production code that are sufficiently decoupled from each other so as to allow convenient maintenance of both, without the impediment of replicating changes between the two.

The discipline of TDD is embodied within three entirely arbitrary laws. The proof that these laws are arbitrary is that the essence can be achieved by very different means. In particular, Kent Beck’s test && commit || revert (TCR) discipline. Although TCR is entirely different from TDD, it achieves precisely the same essential goals.

The three laws of TDD are the basic foundation of the discipline. Following them is very hard, especially at first. Following them also requires some skill and knowledge that is hard to come by. If you try to follow these laws