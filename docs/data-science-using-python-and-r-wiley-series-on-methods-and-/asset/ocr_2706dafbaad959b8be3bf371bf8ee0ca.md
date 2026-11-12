# 14.2 A SIMPLE EXAMPLE OF ASSOCIATION RULE MINING

We begin with a simple example. Suppose that a local farmer has set up a roadside vegetable stand and is offering the following items for sale: {asparagus, beans, broccoli, corn, green peppers, squash, and tomatoes}. Denote this set of items as I.

One by one, customers pull over, pick up a basket, and purchase various combinations of these items, subsets of I.

Let D be the set of transactions represented in Table 14.1, where each transaction T in D represents a set of items contained in I.

Suppose that we have a particular set of items A (e.g. beans and squash) and another set of items B (e.g. asparagus). Then, define an association rule as follows:

> An association rule takes the form:
> 
> if A then B (i.e. A => B).
> 
> where the antecedent A and the consequent B are proper subsets of I, and A and B are mutually exclusive.

This definition would exclude trivial rules such as if beans and squash, then beans.

| Transaction | Items Purchased |
| :--- | :--- |
| 1 | Broccoli, green peppers, corn |
| 2 | Asparagus, squash, corn |
| 3 | Corn, tomatoes, beans, squash |
| 4 | Green peppers, corn, tomatoes, beans |
| 5 | Beans, asparagus, broccoli |
| 6 | Squash, asparagus, beans, tomatoes |
| 7 | Tomatoes, corn |
| 8 | Broccoli, tomatoes, green peppers |
| 9 | Squash, asparagus, beans |
| 10 | Beans, corn |
| 11 | Green peppers, broccoli, beans, squash |
| 12 | Asparagus, beans, squash |
| 13 | Squash, corn, asparagus, beans |
| 14 | Corn, green peppers, tomatoes, beans, broccoli |

# 14.3 SUPPORT, CONFIDENCE, AND LIFT

Measures of goodness of an association rule include support, confidence, and lift. The support for a particular association rule A => B is the proportion of transactions in D that contain both A and B. That is,