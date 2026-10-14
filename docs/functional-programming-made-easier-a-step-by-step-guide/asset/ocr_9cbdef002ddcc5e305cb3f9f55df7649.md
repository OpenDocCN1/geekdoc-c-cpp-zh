```
```haskell
add :: a -> a -> a
```
```

Takes 2 Parameters NOT 3.

Yet, we have 3 Parameters in our `add` function. If you remember from earlier, we can move variables across the equal sign. Let’s do that and see how we really only have 2 Parameters:

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g = \\x -> f x + g x
```
```

Equivalent to the original `add` function above but now with only 2 Parameters on the left-hand side.

Now we only have 2 Parameters. The original way of coding this is far cleaner, but writing the Lambda version was just to remind us how it really works.

And the next line of code:

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \\_ -> zero
```
```

The Identity for `add` is `zero` and it appears to be an Infinite Loop since it has `zero` on both sides of the equal sign. But it’s not.

The left-hand side `zero` is the `zero` for `Semiring (a -> b)`, i.e. `zero` for functions.

The right-hand side `zero` is the `zero` for `Semiring b`, i.e. zero for b, whatever Type b happens to be.

This may seem confusing at first, but remember, the whole right-hand side of `zero` is of Type a (see the Typeclass definition), which here is `(a -> b)`. This means that the Expression, `\\_ -> zero`, takes an a (which it ignores) and returns a b, in this case `zero`. This shows that the right-hand `zero` is b’s `zero`. And so there’s no Infinite Loop here.

And the remaining lines of code:

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \\_ -> zero
  mul f g x = f x * g x
  one = \\_ -> one
```
```

`mul` and `one` are analogous to `add` and `zero`, whereas `one` is the Identity for `mul`.