# 184 CHAPTER 5 Recursion as a Problem-Solving Technique

You now must establish that

property is true for an arbitrary k ⇒ property is true for k + 1

**Inductive hypothesis.** Assume that the property is true for n = k. That is, assume that factorial(k) = k × (k - 1) × (k - 2) × ... × 1

**Inductive conclusion.** Show that the property is true for n = k + 1. That is, you must show that fact(k + 1) returns the value

```
(k + 1) × k × (k - 1) × (k - 2) × ... 2 × 1
```

By definition of the function, fact(k + 1) returns the value

```
(k + 1) × factorial(k)
```

But by the inductive hypothesis, fact(k) returns the value

```
k × (k - 1) × (k - 2) × ... 2 × 1
```

Thus, fact(k + 1) returns the value

```
(k + 1) × k × (k - 1) × (k - 2) × ... 2 × 1
```

which is what you needed to show that for an arbitrary k ⇒ property is true for k + 1
The inductive proof is thus complete.

# 5.4.2 The Cost of Towers of Hanoi

In Chapter 2, you saw the following solution to the Towers of Hanoi problem:

```
solveTowers(count, source, destination, spare)
if (count is 1)
    make a disk directly from source to destination
else
    solveTowers(count - 1, source, spare, destination)
    solveTowers(1, source, destination, spare)
    solveTowers(count - 1, spare, destination, source)
```

We now pose the following question: If you began with N disks, how many moves does Towers make to solve the problem?
M(N) be the number of moves made starting with N disks. When N = 1, the answer is easy:

```
moves(1) = 1
```

When N > 1, the value of moves(N) is not so apparent. An inspection of the solveTowers algorithm, reveals three recursive calls. Therefore, if you know how many moves solveTowers made starting with N - 1 disks, you could figure out how many it made starting with N disks; that is,

```
moves(N) = moves(N-1) + moves(1) + moves(N)
```