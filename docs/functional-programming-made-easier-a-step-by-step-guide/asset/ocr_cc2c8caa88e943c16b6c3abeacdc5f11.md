to the new `List`.

# 5.41. Writing `zip`

`zip` will take 2 `Lists` and zip them into a single `List` where each element of the output `List` is a `Tuple` containing the first `List`'s element in the first position and the second `List`'s in the second position.

One important thing to note is that the shortest `List` dictates when `zip` stops.

Consult `Pursuit` for more information.

Add the following to your test code:

```
```purescript
log $ show $ zip (1 : 2 : 3 : Nil) ("a" : "b" : "c" : "d" : "e" : Nil)
log $ show $ zip ("a" : "b" : "c" : "d" : "e" : Nil) (1 : 2 : 3 : Nil)
log $ show $ zip (Nil :: List Unit) (1 : 2 : Nil)
```
```

+   1. Prints `((Tuple 1 "a") : (Tuple 2 "b") : (Tuple 3 "c") : Nil)`.
+   2. Prints `((Tuple "a" 1) : (Tuple "b" 2) : (Tuple "c" 3) : Nil)`.
+   3. Explicitly specify our empty `List` Type.
+   4. Prints `Nil`.

Try to write `zip` without looking further.

# 5.41.1. Code for `zip`

Starting with the Type Signature:

```
```purescript
zip :: ∀ a b. List a -> List b -> List (Tuple a b)
```
```

Take a minute to look at the signature. Notice how we have to define both `a` and `b`, viz. `∀ a b`. That’s because a `Tuple` can take 2 different Types. So our `Lists` don’t have to be the same Type. They *can* be the same, but do not have to be.

`∀ a b` says that `a` and `b` can be any Type, which means they can both be `Int`, for example. But the fact that they are named differently means that they are independent and can be different Types just like they are in our test code.

Next, we write the base-case (there are 2):