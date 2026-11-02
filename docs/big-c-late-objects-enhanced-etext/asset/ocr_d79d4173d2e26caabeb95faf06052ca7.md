+   • **E11.18** Recursively generate all ways in which a vector can be split up into a sequence of nonempty subvectors. For example, if you are given the vector `{1, 7, 2, 9}`, return the following vectors of vectors:
+   
+     `{{1}, {7}, {2}, {9}}, {{1, 7}, {2}, {9}}, {{1}, {7, 2}, {9}}, {{1}, {7}, {2, 9}}, {{1, 7, 2}, {9}}, {{1, 7}, {2, 9}}, {{1}, {7, 2, 9}}, {{1, 7, 2, 9}}}`
+   
+     *Hint:* First generate all subvectors of the vector with the last element removed. The last element can either be a subsequence of length 1, or it can be added to the last subsequence.

+   • **E11.19** Given a vector of integers, recursively find all vectors of elements of a whose sum is a given integer n.

+   • **E11.20** Suppose you want to climb a staircase with n steps and you can take either one or two steps at a time. Recursively enumerate all paths. For example, if n is 5, the possible paths are:
+   
+     `{1, 2, 3, 4, 5}, {1, 3, 4, 5}, {1, 2, 4, 5}, {1, 2, 3, 5}, {1, 4, 5}`

+   • **E11.21** Repeat Exercise E11.20, where the climber can take up to k steps at a time.

+   • **E11.22** Given an integer price, list all possible ways of paying for it with $100, $20, $5, and $1 bills, using recursion. Don’t list duplicates.

+   • **E11.23** Extend the expression evaluator in Section 11.5 so that it can handle the `%` operator as well as a “raise to a power” operator `^`. For example, `2 ^ 3` should evaluate to 8. As in mathematics, raising to a power should bind more strongly than multiplication:
+   
+     `5 * 2 ^ 3` is 40.

+   • **E11.24** The backtracking algorithm will work for any problem whose partial solutions can be examined and extended. Provide a class

```
```cpp
class PartialSolution
{
public:
    virtual int examine() const;
    virtual vector<PartialSolution*> extend() const;
    virtual void print() const;
    PartialSolution* solve() const;
};
```
```

and a derived class EightQueensPartialSolution.

+   • **E11.25** Refine the program for solving the eight queens problem so that rotations and reflections of previously displayed solutions are not shown. Your program should display twelve unique solutions.

+   • **E11.26** Refine the program for solving the eight queens problem so that the solutions are written to an HTML file, using tables with black and white background for the board and the Unicode character `♛` (`\u2655`) for the white queen.

+   • **E11.27** Generalize the program for solving the eight queens problem to the n queens problem. Your program should prompt for the value of n and display the solutions.

+   • **E11.28** Using backtracking, write a program that solves summation puzzles in which each letter should be replaced by a digit, such as
+   
+     `send + more = money`