# 4.6.2 Adding Nondeterminism, Conditions, and Backtracking

A pure functional language supports only deterministic computation. This means that the application of a function to a given set of arguments always produces the same value. However, some problems, such as flipping a coin, are underspecified, in that their solutions come from a set of values that need only satisfy some constraints. In the case of a coin toss, a definite value is returned, but it will be either heads or tails. Curry supports such nondeterminism by allowing a set of equations for a function to be tried in no particular order. For example, the choice operator ? is defined with two equations:

```
x ? y = x
x ? y = y
```

When ? is applied to some operands, Curry, unlike Haskell, does not automatically try the first equation that appears in the definition, which would always return the first operand. Moreover, if one equation fails during execution, another equation in the set is then tried, although that won’t happen in this particular example. Thus, a nondeterministic function for flipping a coin can be defined using ?:

```
flipCoin = 0 ? 1
```

In Section 4.5.4, we showed some Prolog rules for sorting a list that generated permutations of a list until one of them satisfied the constraint of being sorted. This sorting strategy was clear and simple but suffered the woeful inefficiency of generating permutations of the list until one of them satisfied the sorted predicate. A similar, but more efficient, strategy can be used to define functions to sort a list in Curry.

Working top-down, we define two functions, sorted and permutation, such that the application:

```
sorted (permutation xs)
```

returns a sorted list of the elements in xs. Obviously, if the list returned by a call of permutation is not sorted, the computation must somehow backtrack and try another call of the function, until it produces a sorted list. The strategy used here exploits Curry’s support for nondeterminism and backtracking to produce a simple implementation.

The function sorted expects a list as an argument and returns a sorted list of the same elements. The first two equations in its definition specify the results for an empty list and a list of one element:

```
sorted [] = []
sorted [x] = [x]
```

The third equation handles the case of a list of two or more elements. In this case, the equation includes a condition (specified by the code to the right of the | symbol) that permits evaluation of its right side only if the first element in the list is less than or equal to the second element:

```
sorted (x:y:ys) | x <= y
              = x : sorted(y:ys)
```

As you can see, this function will succeed and return a sorted list just when it receives a permutation of the list that happens to be sorted. However, it fails as soon as the first two elements of the list argument are out of order.