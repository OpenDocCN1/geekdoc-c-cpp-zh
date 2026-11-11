by ordering the database statements to optimize a particular application. For example, if the user knows that certain rules are much more likely to succeed than others during a particular “execution,” then the program can be made more efficient by placing those rules at the beginning of the database.

In addition to allowing the user to control database and subgoal ordering, Prolog, in another concession to efficiency, allows some explicit control of backtracking. This is done with the cut operator, which is specified by an exclamation point (!). The cut operator is actually a goal, not an operator. As a goal, it always succeeds immediately, but it cannot be resatisfied through backtracking. Thus, a side effect of the cut is that subgoals to its left in a compound goal also cannot be resatisfied through backtracking. For example, in the goal

```
a, b, !, c, d.
```

if both a and b succeed but c fails, the whole goal fails. This goal would be used if it were known that whenever c fails, it is a waste of time to resatisfy b or a.

The purpose of the cut then is to allow the user to make programs more efficient by telling the system when it should not attempt to resatisfy subgoals that presumably could not result in a complete proof.

As an example of the use of the cut operator, consider the member rules from Section 16.6.7, which are:

```
member(Element, [Element | _]).
member(Element, [_ | List]) :- member(Element, List).
```

If the list argument to member represents a set, then it can be satisfied only once (sets contain no duplicate elements). Therefore, if member is used as a subgoal in a multiple subgoal goal statement, there can be a problem. The problem is that if member succeeds but the next subgoal fails, backtracking will attempt to resatisfy member by constructing a prior match. But because the list argument to member has only one copy of the element to begin with, member cannot be resatisfied again, which eventually causes the whole goal to fail, in spite of any additional attempts to resatisfy member. For example, consider the goal:

```
dem_candidate(X) :- member(X, democrats), tests(X).
```

This goal determines whether a given person is a democrat and is a good candidate to run for a particular position. The tests subgoal checks a variety of characteristics of the given democrat to determine the suitability of the person for the position. If the set of democrats has no duplicates, then we do not want to back up to the member subgoal if the tests subgoal fails, because member will search all of the other democrats but fail, because there are no duplicates. The second attempt of member subgoal will be a waste of computation time. The solution to this inefficiency is to add a right side to the first statement of the member definition, with the cut operator as the sole element, as in