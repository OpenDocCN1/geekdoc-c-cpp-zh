
Suppose we need to be able to determine whether a given symbol is in a given list. A straightforward Prolog description of this is

```prolog
member(Element, [Element | _]).
member(Element, [_ | List]) :- member(Element, List).
```

The underscore indicates an "anonymous" variable; it is used to mean that we do not care what instantiation it might get from unification. The first statement in the previous example succeeds if Element is the head of the list, either initially or after several recursions through the second statement. The second statement succeeds if Element is in the tail of the list. Consider the following traced examples:

```prolog
trace.
member(a, [b, c, d]).
(1) 1 Call: member(a, [b, c, d])?
(2) 2 Call: member(a, [c, d])?
(3) 3 Call: member(a, [d])?
(4) 4 Call: member(a, [])?
(4) 4 Fail: member(a, [])
(3) 3 Fail: member(a, [d])
(2) 2 Fail: member(a, [c, d])
(1) 1 Fail: member(a, [b, c, d])
no
```

```prolog
member(a, [b, a, c]).
(1) 1 Call: member(a, [b, a, c])?
(2) 2 Call: member(a, [a, c])?
(2) 2 Exit: member(a, [a, c])
(1) 1 Exit: member(a, [b, a, c])
yes
```

## 16.7 Deficiencies of Prolog

Although Prolog is a useful tool, it is neither a pure nor a perfect logic programming language. This section describes some of the problems with Prolog.

### 16.7.1 Resolution Order Control

Prolog, for reasons of efficiency, allows the user to control the ordering of pattern matching during resolution. In a pure logic programming environment, the order of attempted matches that take place during resolution is nondeterministic, and all matches could be attempted concurrently. However, because Prolog always matches in the same order, starting at the beginning of the database and at the left end of a given goal, the user can profoundly affect efficiency by ordering the database statements to optimize a particular application. For example, if the user knows that certain rules are much more likely to succeed than others during a particular “execution,” then the program can be made more efficient by placing those rules at the beginning of the database.

In addition to allowing the user to control database and subgoal ordering, Prolog, in another concession to efficiency, allows some explicit control of backtracking. This is done with the cut operator, which is specified by an exclamation point (!). The cut operator is actually a goal, not an operator. As a goal, it always succeeds immediately, but it cannot be resatisfied through backtracking. Thus, a side effect of the cut is that subgoals to its left in a compound goal also cannot be resatisfied through backtracking. For example, in the goal

```prolog
a, b, !, c, d.
```

If both a and b succeed but c fails, the whole goal fails. This goal would be used if it were known that whenever c fails, it is a waste of time to resatisfy b or a.

The purpose of the cut then is to allow the user to make programs more efficient by telling the system when it should not attempt to resatisfy subgoals that presumably could not result in a complete proof.

As an example of the use of the cut operator, consider the member rules from Section 16.6.7, which are:

```prolog
member(Element, [Element | _]).
member(Element, [_ | List]) :- member(Element, List).
```

If the list argument to member represents a set, then it can be satisfied only once (sets contain no duplicate elements). Therefore, if member is used as a subgoal in a multiple subgoal goal statement, there can be a problem. The problem is that if member succeeds but the next subgoal fails, backtracking will attempt to resatisfy member by constructing a prior match. But because the list argument to member has only one copy of the element to begin with, member cannot be resatisfied again, which eventually causes the whole goal to fail, in spite of any additional attempts to resatisfy member. For example, consider the goal:

```prolog
dem_candidate(X) :- member(X, democrats), tests(X).
```

This goal determines whether a given person is a democrat and is a good candidate to run for a particular position. The tests subgoal checks a variety of characteristics of the given democrat to determine the suitability of the person for the position. If the set of democrats has no duplicates, then we do not want to back up to the member subgoal if the tests subgoal fails, because member will search all of the other democrats but fail, because there are no duplicates. The second attempt of member subgoal will be a waste of computation time. The solution to this inefficiency is to add a right side to the first statement of the member definition, with the cut operator as the sole element, as in

```prolog
member(Element, [Element | _]) :- !.
```

Backtracking will not attempt to resatisfy member but instead will cause the entire subgoal to fail.

Cut is particularly useful in a programming strategy in Prolog called generate-and-test. In programs that use the generate-and-test strategy, the goal consists of subgoals that generate potential solutions, which are then checked by later “test” subgoals. Rejected solutions require backtracking to “generator” subgoals, which generate new potential solutions. As an example of a generate-and-test program, consider the following, which appears in Clocksin and Mellish (2003):

```prolog
divide(N1, N2, Result) :- is_integer(Result),
    Product1 is Result * N2,
    Product2 is (Result + 1) * N2,
    Product1 =< N1, Product2 > N1, !.
```

This program performs integer division, using addition and multiplication. Because most Prolog systems provide division as an operator, this program actually is not useful, other than to illustrate a simple generate-and-test program.

The predicate `is_integer` succeeds as long as its parameter can be instantiated to some nonnegative integer. If its argument is not instantiated, `is_integer` instantiates it to the value 0. If the argument is instantiated to an integer, `is_integer` instantiates it to the next larger integer value.

So, in `divide`, `is_integer` is the generator subgoal. It generates elements of the sequence 0, 1, 2, ..., one each time it is satisfied. All of the other subgoals are the testing subgoals—they check to determine whether the value produced by `is_integer` is, in fact, the quotient of the first two parameters, `N1` and `N2`. The purpose of the cut as the last subgoal is simple: It prevents `divide` from ever trying to find an alternative solution once it has found the solution. Although `is_integer` can generate a huge number of candidates, only one is the solution, so the cut here prevents useless attempts to produce secondary solutions.

Use of the cut operator has been compared to the use of the goto in imperative languages (van Emden, 1980). Although it is sometimes needed, it is possible to abuse it. Indeed, it is sometimes used to make logic programs have a control flow that is inspired by imperative programming styles.

The ability to tamper with control flow in a Prolog program is a deficiency, because it is directly detrimental to one of the important advantages of logic programming—that programs do not specify how solutions are to be found. Rather, they simply specify what the solution should look like. This design makes programs easier to write and easier to read. They are not cluttered with the details of how the solutions are to be determined and, in particular, the precise order in which the computations are done to produce the solution. So, while logic programming requires no control flow directions, Prolog programs frequently use them, mostly for the sake of efficiency.

### 16.7.2 The Closed-World Assumption

The nature of Prolog's resolution sometimes creates misleading results. The only truths, as far as Prolog is concerned, are those that can be proved using its database. It has no knowledge of the world other than its database. When the system receives a query and the database does not have information to prove the query absolutely, the query is assumed to be false. Prolog can prove that a given goal is true, but it cannot prove that a given goal is false. It simply assumes that, because it cannot prove a goal true, the goal must be false. In essence, Prolog is a true/fail system, rather than a true/false system.

Actually, the closed-world assumption should not be at all foreign to you—our judicial system operates the same way. Suspects are innocent until proven guilty. They need not be proven innocent. If a trial cannot prove a person guilty, he or she is considered innocent.

The problem of the closed-world assumption is related to the negation problem, which is discussed in the following subsection.

### 16.7.3 The Negation Problem

Another problem with Prolog is its difficulty with negation. Consider the following database of two facts and a relationship:

```prolog
parent(bill, jake).
parent(bill, shelley).
sibling(X, Y) :- (parent(M, X), parent(M, Y)).
```

Now, suppose we typed the query

```prolog
sibling(X, Y).
```

Prolog will respond with

```
X = jake
Y = jake
```

Thus, Prolog “thinks” Jake is a sibling of himself. This happens because the system first instantiates M with bill and X with jake to make the first subgoal, parent(M, X), true. It then starts at the beginning of the database again to match the second subgoal, parent(M, Y), and arrives at the instantiations of M with bill and Y with jake. Because the two subgoals are satisfied independently, with both matchings starting at the database’s beginning, the shown response appears. To avoid this result, X must be specified to be a sibling of Y only if they have the same parents and they are not the same. Unfortunately, stating that they are not equal is not straightforward in Prolog, as we will discuss. The most exacting method would require adding a fact for every pair of atoms, stating that they were not the same. This, of course, causes the database to become very large, for there is often far more negative information than
