Use the following to test your code:

```
log "___________________________"
log $ show $ runPredicate (Predicate odd) $ 10
log $ show $ runPredicate (Predicate odd) $ 11
```

1 Helpful for delimiting our output since they're all Booleans.

2 Prints false.

3 Prints true.

Give it a try before reading on.

# 15.5. Code for runPredicate

Let's write the Type Signature first:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
```

We take a Predicate a and a value a and return the result of that Predicate.

Notice that runPredicate is general, i.e. it will work with any Predicate. This is why we use the Polymorphic Parameter a.

Next, we write the function:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
runPredicate (Predicate f) x = ???
```

1 We destructure Predicate using Pattern Matching to extract or unwrap the function.

Next, we simply just call that function:

```
runPredicate :: ∀ a. Predicate a -> a -> Boolean
runPredicate (Predicate f) x = f x
```

# 15.6. Writing Contravariant Instance for Predicate

We are now ready to write the Contravariant Instance.

First, add the following code to your test code: