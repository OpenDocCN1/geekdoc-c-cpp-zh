```
(algebra-2 ' (+ (* 3 (+ x 1)) -3))
(* 3 x)
```

At this point we can see how it may be possible to extend such a system to simplify large classes of algebraic expressions.

# Exercise 4.2: Term ordering

According to the predicate expr?, an expression that is explicitly a number is less than any expression that is not explicitly a number.

+   a. In algebra-2 how does the ordering on expressions imposed by the commutative laws make the numerical simplification rules effective?

+   b. Suppose that the commutative laws did not force an ordering. How would we have to express the numerical simplification rules? Explain why numerical simplification would become very expensive.

# Exercise 4.3: Sorting efficiency

The ordering in the commutative laws evolves an $n^2$ bubble sort on the terms of a sum and the factors of a product. This can get pretty bad if there are many terms, as in a serious algebra problem. Is there some way in this system to make a more efficient sort? If not, why not? If so, how would you arrange it?

# Exercise 4.4: Collecting terms

The system we have described does not collect like terms. For example:

```
(algebra-2 ' (+ (* 4 x) (* 3 x))
(+ (* 3 x) (* 4 x))
```