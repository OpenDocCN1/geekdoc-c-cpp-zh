# 5.3.1 Formalization of the Heavy Hitter Problem

The Heavy Hitter Problem can be formalized in HOL4 by modeling the sample set of elements and the data stream as lists (Halali, Hasan & Tahar, 2012). Then we model a function, freq, that returns the frequency of an element in a list.

# Definition 5.9

```
|- ∀ L e. freq e L =
(LENGTH (FILTER (λ r.r = e) L)) / (LENGTH L)
```

where LENGTH returns the length of a list, and FILTER returns a filtered list out of its argument list with elements that satisfy the given condition. The above function will be required later, to report the list of the α-heavy hitter elements. Next, we model another function, HeavyHitter_lst, which takes as parameters two lists and a real value and returns the list of heavy hitters corresponding to the algorithm of heavy hitter problem.

# Definition 5.10

```
|- ∀ L M α. HeavyHitter_lst L M α =
FILTER (λ r. α <= (freq (EL r L) M)) L
```

So far, the formalization has been based on deterministic functions. We now introduce the randomness in our models using appropriate random variables and our probabilistic analysis of the algorithm for the heavy hitter problem would be based upon the characteristics of these random variables. In our analysis, we need a Bernoulli variable X, with outcomes 1 or 0. In order to formalize this random behavior, we have to define a probability space that has the set {0, 1} as its space and power set, POW {0, 1}, as the events space and the probability measure will be a new function that returns pr if the set in parameter implements the fact that f(x), which refers to our random variable in this case, is equal to 1, and returns 1 - pr otherwise. The corresponding probability measure is defined in HOL4 as follows:

# Definition 5.11

```
|- ∀ g pr. mu g pr =
(λ a.if (a = X|g x = 1) then pr else (1 - pr))
```