
In the PureScript library, there are 2 functions, foldMapDefaultR and foldMapDefaultL which effectively is the above code.

And as it turns out, the authors of the Array Foldable Typeclass chose to be Right-Associative, while the authors of List chose Left-Associative.

While this is unfortunate, it’s possible to convert between a List and an Array, so we can choose which one we want. We also can explicitly call foldMapDefaultR on Lists. But these non-default solutions cannot benefit from Typeclasses.

So, let’s pick Left-Associative to match the library author’s choice:

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f l          = foldl (\acc x -> acc <> f x) mempty l ①
```

① We cannot write in Point-free when using Pattern Matching.

## 10.5. Rewriting length with Folds

Since foldl and foldr pass State, we can recode the Tail Recursive version of length using Fold. Before we do, let’s revisit that version of length:

```
length :: ∀ a. List a -> Int
length l = go 0 l where ①
  go :: ∀ a. Int -> List a -> Int ①
  go acc Nil      = acc
  go acc (x : xs) = go (acc + 1) xs ②
```

① The first Parameter is our State, which is the current count and it starts at 0.

② Each iteration we add 1 to our count.

We have to determine 2 things to use foldl or foldr. First, what’s the State and its initial value. In this case, it’s a count of the number of elements in the List and its Initial Value is 0.

And the second thing to determine is what operation will we do each iteration. In this case, we’ll simply add 1 to our count.

The last thing to determine is if Associativity matters to us. Since our operation is +, which is Commutative, i.e. order does NOT matter, we do not care about Associativity.

So we could choose either `foldl` or `foldr` and our results would be the same:

```
(((1 + 1) + 1) + 1) = (1 + (1 + (1 + 1)))
```

But there is one more factor to consider. Here is our implementation of `Foldable` for `List`:

```
instance foldableList :: Foldable List where
  foldr _ acc Nil      = acc
  foldr f acc (x : xs) = f x (foldr f acc xs)
  foldl _ acc Nil      = acc
  foldl f acc (x : xs) = foldl f (f acc x) xs
  foldMap _ Nil        = mempty
  foldMap f l          = foldl (\acc x -> acc <> f x) mempty l
```

Compare the implementation of `foldr` to `foldl` and see if you find a reason to use one over the other.

If you cannot see why one would be preferred over the other, see if one is more efficient than the other.

It turns out that `foldl` is more efficient than `foldr` since `foldl` is Tail Recursive, whereas `foldr` is not. So we’ll choose that to rewrite `length` using `foldl`:

```
length :: ∀ a. List a -> Int
length = foldl (\count _ -> count + 1) 0 ①
```

① Since we don’t care what the value is from the `List`, we ignore it with `_`.

```
```haskell
reverse :: List ~> List
reverse Nil = Nil
reverse ol = go Nil ol where
  go rl Nil     = rl
  go rl (x : xs) = go (x : rl) xs
```
```

Go ahead and rewrite this by using either `foldl` or `foldr`, which ever makes the most sense. Then continue reading.

## 11.2. Code for `reverse`

First thing to decide before we begin coding is what is the State for `reverse`. Looking at our Tail Recursive version, we see that we’re passing `rl`, i.e the reversed `List`, to our `go` function. We can also see that the Initial State is `Nil`, i.e. it’s the value we initially pass to `go`.

We should use `foldl` since it’s Tail Recursive and therefore more efficient, not to mention that we’re rewriting a Tail Recursive function and we’d like to keep it that way:

```
```haskell
import Data.List (List(..), (:), foldl)

reverse :: List ~> List
reverse = foldl (\rl x -> x : rl) Nil
```
```

- 1. We could’ve imported `foldl` from `Data.Foldable` as well. `Data.List` re-exports `foldl` from `Data.Foldable`.
- 2. The Initial State is `Nil` and at each iteration we add to the head of `rl` and return that as our modified State.
- 3. This is written in Point-free form where the `List` is unnamed.

## 11.3. Writing `max`

Let’s take a side tour and code up the `max` function. It takes 2 values and returns the maximum of the two.

Add the following to your test code:

```
```haskell
log $ show $ max (-1) 99
log $ show $ max "aa" "z"
```
```

- 1. Prints `99`.
- 2. Prints `"z"`.

Also, add discard and negate to your Prelude import list. We need discard since we’re adding multiple lines to our test code using the do syntax (more on this later, I promise) and we need negate for our −1.

Remember, we normally do not need to worry about these imports when writing normal code but since we’re recoding functions from Prelude, we’re being very careful about our imports.

Another possible way we could handle imports from Prelude is to use hiding to EXCLUDE things that we’re overriding, e.g.:

```
import Prelude hiding (max)
```

But if we did that, you’d learn a lot less about the different functions and where they come from. Keep in mind, you’ll simply import Prelude with NO import list in your production code.

Go ahead and code up max before moving on the Hint section.

# 11.4. Hint for max

You probably got stumped by the test code. You have to write a function that will work with Ints and Strings. But how?

I’m going to show you a little trick. Write the function WITHOUT the Type Signature. Then once your function compiles, you’ll get a compiler warning that will suggest what Type Signature you should use. That suggested Type Signature will tell you how.

Give it another try and see what you get.

# 11.5. Code for max

We’re going to follow the approach suggested in the Hint section.

We can code this using an if expression or with Guards. Let’s do it with Guards:

```
import Prelude (Unit, show, negate, discard, otherwise, type (~>), ($), (>))

max x y | x > y      = x   -- COMPILER WARNING!!
        | otherwise = y
```

1 Had to add > and otherwise. Remember, otherwise is just defined to be true.

Now we get the following compiler warning:

![](img/8c0e9b687c62642e828ccb5481e11313_377_0.png)

We can see that we need constrain a to have an Ord instance. That’s because the operator >, which is an Operator Alias for greaterThan, calls compare from the Ord Typeclass.

This is how max can work for Ints and Strings:

```
import Prelude (class Ord, Unit, show, negate, discard, otherwise,
    type (~>), ($), (>)) ①

max :: ∀ a. Ord a => a -> a -> a ②
max x y | x > y     = x
        | otherwise = y
```

① We had to import the Ord class. Note the class keyword.

② The Type Signature as suggested by the compiler warning message.

# 11.6. Writing findMax

Armed with our max function, we can now write a function to find the maximum value of a List. We’ve not written this before, so we’ll first write it as regular Recursive function.

Let’s make the first Parameter to findMax a default value so we don’t have to return a Maybe.

Add the following line to your test code:

```
log $ show $ findMax 0 (37 : 311 : -1 : 2 : 84 : Nil) ①
log $ show $ findMax "" ("a" : "bbb" : "c" : Nil) ②
```

① Prints 311.

② Prints "c".

Try to code findMax before moving forward.

## 11.7. Code for `findMax`

Since we wrote `max` to help us write `findMax`, we can look to `max`’s Type Signature for clues on what Constraints we’ll need. We can see that if `max` requires values to have an `Ord` instance, then we’ll need the same Constraint, i.e. if we want to call `max` with elements from our `List`:

```
```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
```
```

The first Parameter is the default value, just in case our `List` is empty.

Next, we write the base-case:

```
```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
findMax mx Nil = mx
```
```

We return either the default value if the initial `List` is empty or whatever the current maximum value is if we’ve just exhausted our `List`.

Finally, we code the recursive case:

```
```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
findMax mx Nil = mx
findMax mx (x : xs) = findMax (max x mx) xs
```
```

Tail Recursive call.

We recurse with the tail of the `List` and the `max` of our current maximum (which is initially our default value) and the head of our `List`.

## 11.8. Improving `findMax`

Let’s examine our test code for `findMax`:

```
```haskell
log $ show $ findMax 0 (37 : 311 : -1 : 2 : 84 : Nil)
```
```

What would happen if we didn’t use `0` as our default value? What if we change the default value to `999` and run our tests. What did you think you’d get? Go ahead and try it.

If you changed your test and ran it, you’d see that you get `999` since it’s larger than anything in the `List`. Not ideal.

We cannot trust our caller to pick the right default value. This function’s design is flawed. How can we fix
