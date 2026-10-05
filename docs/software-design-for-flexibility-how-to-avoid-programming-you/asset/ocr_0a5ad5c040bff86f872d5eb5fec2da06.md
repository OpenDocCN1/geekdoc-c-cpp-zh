The constructor make-prime-number requires that its argument be prime, as determined by slow-prime?: the only objects that can be tagged by this constructor are prime numbers.

(make-prime-number 4)
;Ill-formed data for prime-number: 4

# 3.5.2 Relationships between predicates

The sets that we can define with abstract predicates can be related to one another. For example, the primes are a subset of the positive integers. The even integers, and the odd integers are subsets of the integers. This is important because any operation that is applicable to an integer is applicable to any element of any subset, but there are operations that can be applied to all elements of an enclosing subset. For example, the even integers can be halved without leaving a remainder, but that is not true of the full integers.

When we define prime-number?, we effectively defined a set of objects. But that set has no relation to the set defined by exact-integer?

```
(exact-integer? (make-prime-number 2))
#f
```

We would like these sets to be properly related, which is done by adding some metadata to the predicates themselves:

```
(set-predicate<= prime-number? exact-integer?)
```

This procedure set-predicate<= modifies the metadata of its argument predicates to indicate that the set defined by the first argument is a (non-strict) subset of the set defined by the second argument. In our case, the set defined by prime-number? is declared to be a subset of the set defined by exact-integer?. Once this is done, exact-integer? will recognize our objects:

```
(exact-integer? (make-prime-number 2))
#f
```

# 3.5.3 Predicates are dispatch keys