![](bbox=[0.19, 0.06, 0.81, 0.27])

According to the error message, the case that’s missing is (Cons Nil _). So let’s add it:

```
concat :: ∀ a. List (List a) -> List a
concat Nil = Nil
concat (Nil : xss) = ??? ①
concat ((x : xs) : xss) = x : concat (xs : xss)
```

① This is the case when we’ve exhausted the head List. This is also the case where we encounter an empty List in our List of Lists like our last List in our test code.

Once we’ve depleted the head List and processed all its elements, it will be empty and we can just throw it away and continue with the rest of the Lists:

```
concat :: ∀ a. List (List a) -> List a
concat Nil = Nil
concat (Nil : xss) = concat xss ①
concat ((x : xs) : xss) = x : concat (xs : xss)
```

① We continue concat-ing with the remainder of the List of Lists.

# 5.28. Writing filter

When I first learned about Functional Javascript, I learned about 3 Functions, map, reduce and filter. filter is one of those Functions that cannot be done without being able to pass a Function as an Argument to another Function.

Non-Functional Languages like Java could not do this for a very long time and so this Function seemed so magical because I was never able to write a Function like filter. I always had to write a for-loop.

But this is not the case in Functional Languages since we have Higher-Ordered Functions, i.e. Functions that take or return Functions.

filter takes a Predicate Function to KEEP or filter-in elements when the Predicate returns true. Take the