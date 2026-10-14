# 5.37.1. Code for dropWhile

First things, first:

```
dropWhile :: ∀ a. (a -> Boolean) -> List a -> List a
```

Next, the base-case:

```
dropWhile :: ∀ a. (a -> Boolean) -> List a -> List a
dropWhile _ Nil = Nil
```

Finally, the recursive case:

```
dropWhile :: ∀ a. (a -> Boolean) -> List a -> List a
dropWhile _ Nil      = Nil
dropWhile pred l@(x : xs) = if pred x then dropWhile pred xs else l ①
```

① If x passes the Predicate then discard it and continue dropping with the tail, xs. Otherwise, we return the FULL List, l. Notice the l@ syntax. This creates a variable for the FULL List and then proceeds to destructure it using Pattern Matching into x and xs.

Turns out that dropWhile is Tail Recursive, unlike takeWhile.

# 5.38. Writing takeEnd

takeEnd does what take does, but at the end of the List. This makes it a bit more complicated.

Add the following to your tests:

```
log $ show $ takeEnd 3 (1 : 2 : 3 : 4 : 5 : 6 : Nil) ①
log $ show $ takeEnd 10 (1 : Nil) ②
```

① Prints (4 : 5 : 6 : Nil)

② Prints (1 : Nil)

Try to write takeEnd before moving on.

# 5.38.1. Hint for takeEnd

You may think about writing takeEnd as: