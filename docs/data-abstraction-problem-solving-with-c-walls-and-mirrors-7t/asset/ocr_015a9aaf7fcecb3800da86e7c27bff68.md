You can make precedence and association rules unnecessary by placing parentheses around each pair of operands together with their operator, thereby avoiding any ambiguity. A grammar for the language of all fully parenthesized infix expressions is

```
```
<infix> = <identifier> | (<infix> <operator> <infix>)
<operator> = + | - | * | /
<identifier> = a | b | ... | z
```
```

Although the grammar is simple, the language is rather inconvenient for programmers.

Therefore, most programming languages support a definition of algebraic expressions that includes both precedence rules for the operators and rules of association so that fully parenthesized expressions are not required. However, the grammars for defining such languages are more involved and the algorithms for recognizing and evaluating their expressions are more difficult than those you have seen in this section. Programming Problem 8 at the end of this chapter describes such a grammar without left-to-right association rules and asks you to write a recognition algorithm. Programming Problem 8 at the end of Chapter 6 presents a nonrecursive evaluation algorithm for algebraic expressions that use both precedence and left-to-right association rules.

# ## 5.3 Backtracking

This section considers an organized way to make successive guesses at a solution. If a particular guess leads to a dead end, you back up to that guess and replace it with a different guess. This strategy of retracing steps in reverse order and then trying a new sequence of steps is called backtracking. You can combine recursion and backtracking to solve the following problem.

# ### 5.3.1 Searching for an Airline Route

This example will introduce you to a general type of search problem. In this particular problem, you must find a path from some point of origin to some destination point. We shall solve this problem by using recursion. In the next chapter, we will solve it again without recursion.

The High Planes Airline Company (HPAir) wants a program to process customer requests to fly from some origin city to some destination city. So that we can focus on recursion, we will simplify the problem: For each customer request, just indicate whether a sequence of HPAir flights from the origin city to the destination city exists.

Imagine three input text files that specify all of the flight information for the airline as follows:

+   * The names of cities that HPAir serves
+   * Pairs of city names, each pair representing the origin and destination of one of HPAir's flights
+   * Pairs of city names, each pair representing a request to fly from some origin to some destination

The program should then produce output such as

```
```
Request is to fly from Providence to San Francisco.
HPAir flies from Providence to San Francisco.

Request is to fly from Philadelphia to Albuquerque.
Sorry. HPAir does not fly from Philadelphia to Albuquerque.

Request is to fly from Salt Lake City to Paris.
Sorry. HPAir does not serve Paris.
```
```