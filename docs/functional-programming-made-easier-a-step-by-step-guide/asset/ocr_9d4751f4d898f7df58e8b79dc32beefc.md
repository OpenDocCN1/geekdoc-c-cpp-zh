```
zip :: ∀ a b. List a -> List b -> List (Tuple a b)
zip Nil _ = Nil
zip _ Nil = Nil
```

If either List is empty, then there’s nothing to zip.

And finally, the recursive case:

```
zip :: ∀ a b. List a -> List b -> List (Tuple a b)
zip Nil _           = Nil
zip _ Nil           = Nil
zip (x : xs) (y : ys) = Tuple x y : zip xs ys ①
```

① Take the head off of both lists and wrap it up in a Tuple, which we put on the head of the zipped tails.

# 5.42. Writing unzip

unzip is the inverse of zip. You should be able to take the output of zip and apply it to unzip and get your original Lists back, albeit in a Tuple, assuming you started with Lists of the same size. That’s because zip will truncate the longer of the 2 Lists.

Add the following to your test code:

```
log $ show $ unzip (Tuple 1 "a" : Tuple 2 "b" : Tuple 3 "c" : Nil) ①
log $ show $ unzip (Tuple "a" 1 : Tuple "b" 2 : Tuple "c" 3 : Nil) ②
log $ show $ unzip (Nil :: List (Tuple Unit Unit)) ③ ④
```

① Prints (Tuple (1 : 2 : 3 : Nil) ("a" : "b" : "c" : Nil)).

② Prints (Tuple ("a" : "b" : "c" : Nil) (1 : 2 : 3 : Nil)).

③ Explicitly specified the Type of our empty List. Notice that unzip is expecting a List of Tuples. We don’t care about the underlying Types since our List is empty and so we simply specify Unit.

④ Prints (Tuple Nil Nil).

Consult Pursuit for the Type Signature and further examples then try to write unzip before reading on.

# 5.42.1. Code for unzip

First, the Type Signature and the single base-case: