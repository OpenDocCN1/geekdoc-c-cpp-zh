```
h :: Int -> Tuple String Int
h = g `composeDebuggable` f
```

This looks very close to our Pure version, h':

```
h' :: Int -> Int
h' = g `compose` f ①
```

① I chose not use <<< to make the similarity even more obvious.

composeDebuggable now lets us compose these Side-effect Functions, but it's only limited to ones that return Tuple String Int. At this point, writing a more general compose Function is very difficult and maybe impossible. Or it's possible, but so complex that it's inconvenient to use.

But no matter, we've got a good solution for these kinds of Functions, which means we can compose them.

But our world is filled with lots and lots of Pure Functions. And we cannot use compose or composeDebuggable to compose a Pure Function with our Side-effect one. It sure would be nice if we could compose Pure Functions with our Side-effect ones.

# 18.1.2. Composing Side-effect Function with Pure Ones

Let's write a Function that converts a Pure Function into a Side-effect one. This will let us compose all the Pure Functions in the world with our Side-effect ones.

We'll call it makeFuncDebuggable. First the Type Signature:

```
makeFuncDebuggable :: ∀ a b. (a -> b) -> (a -> Tuple String b) ①
```

① Implicit, Right-Associative Parentheses added.

makeFuncDebuggable will lift our Function into one that has a Side-effect, i.e. it takes a Function that normally returns a Pure Value, b, and makes it return a Side-effect Value, Tuple String b.

Next, we'll write the implementation:

```
makeFuncDebuggable :: ∀ a b. (a -> b) -> a -> Tuple String b ①
makeFuncDebuggable f x = Tuple "" (f x)
```

① Removed redundant Parentheses.

Notice how we use an empty String so that NOTHING is added to the log. This should make you think of mempty from Monoid, since composeDebuggable uses the Semigroup Operator, <>, to combine the