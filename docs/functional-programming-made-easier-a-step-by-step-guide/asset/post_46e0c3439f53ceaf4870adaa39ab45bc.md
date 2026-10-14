
I’ll give you a hint, we replaced `Int` with `Semiring` to make it work for ANY Element. How about now? Can you see any other hardcoded Type?

That’s right. The collection, i.e. the `List`, can also be Abstracted. What constraint can we put on the collection to make more general?

This Chapter is about `Foldable`, and we’ve been restricting our code to `List`, but there are many other `Foldable` Data Structures, e.g. `Array` or trees, etc.

Add the following lines to your test code in anticipation of being able to `sum` over `Arrays`:

```
log $ show $ sum [1, 2, 3] ❶
log $ show $ sum [1.0, 2.0, 3.0] ❷
```

+   ❶ Prints `6`.
+   ❷ Prints `6.0`.

So try to modify our Function to work with ANY `Foldable` Type. Then see how you did by advancing to the next section.

## 11.24. Code for `sum` using `Foldable`

```
sum :: ∀ f a. Foldable f => Semiring a => f a -> a
sum = foldl (+) zero
```

❶ We added the `Foldable f` Constraint where `f` is our foldable Type, e.g. `List`, `Array`, etc.

This final version of `sum` is as flexible as we can make it. We’ve abstracted both the Data Structure AND the Elements.

We could create a Tree and make it `Foldable` and then if the Tree holds a `Semiring`, we could call `sum` on it and it would just work with no additional effort on our part. This is the real power of Typeclasses.

And if we can, maybe we should.

## 11.25. Using `sum` with `Tree`

This is a Recursive Definition because the `Tree` Type is on both the left and right-hand side of the equal sign.

`Leaf` is the base-case. It’s what terminates the Recursion.

`Node` is the recursive case.

These mirror the way base-cases and recursive cases work in Recursive Functions. Our base-case, terminates the Recursion.

Now, all we have to do is make our Tree `Foldable`. Easier said than done though.

There are a number of things we must first decide before we make it `Foldable`. Are we going to favor, the left or right side when we encounter a `Node`? And, are we going to traverse the `Tree`, Depth-first or Breath-first.

We didn’t have to make these decisions for `List` since there’s only one way to traverse a `List`, i.e. from head to tail. But a `Tree` is a structure that can be traversed a few different ways.

To make our code easier, let’s make an executive decision and choose **Depth-first**.

Often times, it’s worth stopping and creating a simple example of your Data Structure to help you develop your code. Here’s a simple `Tree`:

![](img/8c0e9b687c62642e828ccb5481e11313_396_0.png)

Let’s see how our `sum` function is affected by favoring the *Left*:

```
0 + 5 + (-1) + 14 + 99 = 117
```

If now if we favor the *Right* we’ll get:

```
0 + 99 + 14 + (-1) + 5 = 117
```

Notice the result is the same. So using `sum` to help us decide which side to favor doesn’t help us much.

We also need to remember that we’re writing the `Foldable` instance for all functions, not just `sum`. So we need to consider the best way to traverse it so it works well for all `Foldable` operations, e.g. Subtraction. With Subtraction, the results will NOT be the same.

But, we didn’t specify anything special about this Binary Tree. It’s just a Binary Tree. It’s not balanced or sorted. So we cannot make any decisions based on that information.

So, let’s make another executive decision and just choose *Left*.

Now that we’ve decided on how to traverse, we’re ready to code the `Foldable` instance for `Tree`. Consult

In all 3 cases, we pass all Parameters except the final one. That allows us to simply compose these functions since they’re both waiting for a single parameter.

Now that our Tree is Foldable, we can call sum on it when it’s a is a Semiring like our test Tree:

```
(Node (Node (Leaf 5) (Node (Leaf (-1)) (Leaf 14))) (Leaf 99))
```

## 11.29. Improving on Foldable for Tree

If we wanted to support favoring the Right side and/or Breath-first traversals, then we could use newtype to make new Types that have the appropriate behaviors and their own toList and Foldable instances.

We could even make our own Typeclass, called ToList to make that process easier.

We won’t delve into this too deeply at this point, but for grins here’s the implementation for Left and Right favoring for Depth-first ONLY, since I’m too lazy to write the Breadth-first traversal code.

Here is the full implementation for those interested:

```
```haskell
data Tree a = Leaf a | Node (Tree a) (Tree a)

class ToList f where ❶
  toList :: ∀ a. f a -> List a

newtype RightFirstTree a = RightFirstTree (Tree a) ❷
newtype LeftFirstTree a = LeftFirstTree (Tree a)

instance toListRightFirstTree :: ToList RightFirstTree where
  toList (RightFirstTree (Leaf x)) = singleton x
  toList (RightFirstTree (Node lt rt)) =
    toList (RightFirstTree rt) <> toList (RightFirstTree lt) ❸ ❺

instance toListLeftFirstTree :: ToList LeftFirstTree where
  toList (LeftFirstTree (Leaf x)) = singleton x
  toList (LeftFirstTree (Node lt rt)) =
    toList (LeftFirstTree lt) <> toList (LeftFirstTree rt) ❹ ❺

instance foldableRightFirstTree :: Foldable RightFirstTree where
  foldr f acc = foldr f acc <<< toList
  foldl f acc = foldl f acc <<< toList
  foldMap f = foldMap f <<< toList

instance foldableLeftFirstTree :: Foldable LeftFirstTree where
  foldr f acc = foldr f acc <<< toList
  foldl f acc = foldl f acc <<< toList
  foldMap f = foldMap f <<< toList
```
```

+   1. The `ToList` class to distinguish the traversal over a non-List structure.
+   2. We wrap `Tree` in these speciality Types that have definitive traversals.
+   3. `rt` is prepended to `lt` for a Right-favoring traversal.
+   4. `lt` is prepended to `rt` for a Left-favoring traversal.
+   5. We have to rewrap the Left and Right `Trees` in the `newtype` before we can Recurse. We could’ve derived a `Newtype` instance and used `wrap` instead.

Notice that we no longer need a `Foldable` instance for `Tree` or our standalone `toList` helper function. Also, our test code should change slightly:

# Chapter 12. Functors

We’re going to finally delve into Functors a very powerful Abstraction pilfered from Category Theory in Mathematics. We won’t delve too much into the Category Theory here, but will primarily concentrate on the motivations for using this Abstraction to help solve Programming problems.

But before we do, I want to lay down a bit of groundwork that will hopefully take us all the way through Applicatives and Monads.

## 12.1. Defining ADTs

When we define an Algebraic Data Type (ADT) such as Maybe, we have an idea of what that Type represents. We’ve been talking about Maybe being the Type that holds the result a computation that can potentially fail:

```
data Maybe a = Nothing | Just a
```

But at this point, all we have is our Intention. We haven’t specified how it’s to be used. Once we start adding Typeclass Instances, our intention becomes more explicit:

```
data Maybe a = Nothing | Just a
derive instance eqMaybe :: Eq (Maybe a)
derive instance ordMaybe :: Ord (Maybe a) ①
```

① This derivation along with the initial Type definition will determine how Maybes will sort. Nothings will be smaller than Justs since they are defined first.

Every time we implement another Typeclass instance, we are cementing the Type’s behaviors, choosing one possible behavior over all others. That doesn’t mean we couldn’t write code to sort Maybe where Just is sorted before Nothing despite the Ord derivation. But the whole point of Ord is to dictate the behavior when comparing values of a Type.

We could also decide not to derive Ord for our Type burdening those who use it to write a lot of boilerplate code to do common functionality:

```
compareMaybe :: ∀ a. Maybe a -> Maybe a -> Boolean
```

But this would be short-sighted and difficult to maintain. It might work for small codebases, but it certainly doesn’t scale or work well with multiple projects, especially, if compareMaybe is different between projects.

Now, imagine we want to compute the following Mathematical equation:
