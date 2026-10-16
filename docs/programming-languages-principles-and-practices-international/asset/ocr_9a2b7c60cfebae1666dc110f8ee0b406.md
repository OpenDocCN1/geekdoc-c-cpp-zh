# 4.1 Logic and Logic Programs

Before you can learn about logic programming, you need to know a little bit about mathematical logic. The kind of logic used in logic programming is the first-order predicate calculus, which is a way of formally expressing logical statements, that is, statements that are either true or false.

# EXAMPLE 1

The following English statements are logical statements:

+   - 0 is a natural number.
+   - 2 is a natural number.
+   - For all x, if x is a natural number, then so is the successor of x.
+   - 21 is a natural number.

A translation into predicate calculus is as follows:

+   - natural(0).
+   - natural(2).
+   - For all x, natural(x) → natural(successor(x)).
+   - natural(21).

Among these logical statements, the first and third statements can be viewed as axioms for the natural numbers: statements that are assumed to be true and from which all true statements about natural numbers can be proved. Indeed, the second statement can be proved from these axioms, since 2 = successor(successor(0)) and natural(0) → natural(successor(0)) → natural(successor(successor(0))). The fourth statement, on the other hand, cannot be proved from the axioms and so can be assumed to be false.

First-order predicate calculus classifies the different parts of such statements as follows:

+   1. Constants. These are usually numbers or names. Sometimes they are called atoms, since they cannot be broken down into subparts. In Example 1, 0 is a constant.
+   2. Predicates. These are names for functions that are true or false, like Boolean functions in a program. Predicates can take a number of arguments. In Example 1, the predicate natural takes one argument.
+   3. Functions. First-order predicate calculus distinguishes between functions that are true or false—these are the predicates—and all other functions, like successor in Example 1, which represent non-Boolean values.
+   4. Variables That Stand for as yet Unspecified Quantities. In Example 1, x is a variable.
+   5. Connectives. These include the operations and, or, and not, just like the operations on Boolean data in programming languages. Additional connectives in predicate calculus are implication, signified by →, and equivalence, indicated by ↔. These are not really new operations: a → b means that b is true whenever a is true. This is equivalent to the statement b or not a. Also a ↔ b means the same as (a → b) and (b → a).