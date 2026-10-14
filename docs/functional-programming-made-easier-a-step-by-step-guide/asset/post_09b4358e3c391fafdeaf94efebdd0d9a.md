
```
composeKleisli
  :: V a b c m
  · Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f = \x -> f x >>= g
```

x moved from the right side of the equation to the left as the first argument of the Lambda.

Let’s write `composeKleisli` in infixed notation and change the function names so they don’t collide with the Associativity Law to make it easier to work with:

```
composeKleisli s r   = \x -> r x >>= s
s `composeKleisli` r = \x -> r x >>= s
s      >=>           r = \x -> r x >>= s
```

Our strategy here is to substitute the above implementation for `composeKleisli` into the Associativity Laws to get the equivalent law for `bind`:

```
(f >=> g) >=> h = f >=> (g >=> h)        [Associativity]
```

We’ll do that by working from left to right:

```
(f >=> g) >=> h                         = f >=> (g >=> h)
(\x -> g x >>= f) >=> h                 = f >=> (g >=> h)
\y -> h y >>= (\x -> g x >>= f)          = f >=> (g >=> h)
\y -> h y >>= (\x -> g x >>= f)          = f >=> (\x -> h x >>= g)
\y -> h y >>= (\x -> g x >>= f)          = \y -> (\x -> h x >>= g) y >>= f
```

+   1. The Associativity Law using Kleisli Composition.
+   2. Substitute `f >=> g` into `s >=> r = \x -> r x >>= s`, where `f` binds to `s` and `g` binds to `r`.
+   3. Substitute `(\x -> g x >>= f) >=> h` into `s >=> r = \y -> r y >>= s`, where `(\x -> g x >>= f)` binds to `s` and `h` binds to `r`. To avoid name confusion, `x` was renamed to `y` in the Kleisli Composition formula.
+   4. Now on the right side, substitute `g >=> h` into `s >=> r = \x -> r x >>= s`, where `g` binds to `s` and `h` binds to `r`.
+   5. Substitute `f >=> (\x -> h x >>= g)` into `s >=> r = \y -> r y >>= s`, where `f` binds to `s` and `(\x -> h x >>= g)` binds to `r`. To avoid name confusion, `x` was renamed to `y` in the Kleisli Composition formula.

At this point, we simply reduce the equation at each step:

```
\y -> h y >>= (\x -> g x >>= f) = \y -> (\x -> h x >>= g) y >>= f ①
h y >>= (\x -> g x >>= f)          = (\x -> h x >>= g) y >>= f      ②
h y >>= (\x -> g x >>= f)          = (h y >>= g) >>= f             ③
m >>= (\x -> g x >>= f)            = (m >>= g) >>= f              ④
```

① The last substitution step for reference.

② Eliminate \y -> on both sides.

③ Apply y to the Lambda on the right side binding y to x.

④ Substitute m for h y. This will be the Monadic Value we start with when doing our binds.

The final equation is the Associativity Law for Monads but written with bind instead of Kleisli Composition:

```
(m >>= g) >>= f = m >>= (\x -> g x >>= f)      [Associativity] ①
```

① Flipped the equation from above.

Now, we can put our implementation for bind through this formula to prove it’s Associative. But, we only care about the second Value of the Tuple. We’ve already determined that our Strings, the first Value of the Tuple, will be combined in an Associative way thanks to the Associativity of <>.

So, let’s write a degenerate version of our bind to isolate just the second Value of the Tuple. This will help reduce the noise:

```
-- ORIGINAL
instance bindDebuggable :: Bind Debuggable where
    bind (Debuggable (Tuple s x)) f =
        let (Debuggable (Tuple s' r)) = f x
        Debuggable $ Tuple (s <> s') r

-- DEGENERATE VERSION to isolate the second Value of the Tuple
instance bindDebuggable :: Bind Debuggable where
    bind (Debuggable x) f = f x
```

If the degenerate version is Associative then our original version will be too.

Here are the assumptions that we’ll be working with to put our degenerate bind through the Associativity Law:

```
Debuggable y >>= h = h x ❶
v :: a ❷
w :: b
z :: c
m = Debuggable v :: Debuggable a ❸
g :: a -> Debuggable b ❹
f :: b -> Debuggable c ❺
```

❶ Our degenerate version of `bind` written infixed and with the variables renamed to avoid confusion.

❷ `v`, `w` and `z` are just some working Values specified here with their Types.

❸ We’re going to start with `Debuggable v` as our starting Monadic Value for the `bind`.

❹ `g` is a Monadic Function of the form `a -> m b`, where the Type `m` is the Monad, `Debuggable`, not to be confused with our Monadic Value, `m`.

❺ `f` is also a Monadic Function of the form `b -> m c`.

Now we start with the left side of the law:

```
(m >>= g) >>= f ❶
(Debuggable v >>= g) >>= f ❷
g v >>= f ❸
Debuggable w >>= f ❹
f w ❺
Debuggable z ❻
```

❶ Left side of Associativity Law.

❷ Substitute using `m = Debuggable v`.

❸ Substitute `Debuggable v >>= g` into `Debuggable y >>= h = h y`, where `v` binds to `y` and `g` binds to `h`.

❹ Apply `g` to `v`. Remember that `w` is of Type `b`.

❺ Substitute `Debuggable w >>= f` into `Debuggable y >>= h = h y`, where `w` binds to `y` and `f` binds to `h`.

❻ Apply `f` to `w`. Remember that `z` is of Type `c`.

And we do the same with the right side of the law:

```
m >>= (\x -> g x >>= f)
Debuggable v >>= (\x -> g x >>= f)
(\x -> g x >>= f) v
g v >>= f
Debuggable w >>= f
f w
Debuggable z
```

① Right side of Associativity Law.

② Substitute using m = Debuggable v.

③ Substitute Debuggable v >>= (\x -> g x >>= f) into Debuggable y >>= h = h y, where v binds to y and (\x -> g x >>= f) binds to h.

④ Apply (\x -> g x >>= f) to v, where v binds to x.

⑤ Apply g to v. Remember that w is of Type b.

⑥ Substitute Debuggable w >>= f into Debuggable y >>= h = h y, where w binds to y and f binds to h.

⑦ Apply f to w. Remember that z is of Type c.

Since substituting our bind implementation into both sides of the Associativity Laws resulted in Debuggable z, we know that our degenerate implementation of bind is Associative, which means our original version of bind is also Associative.

## 18.10. Monad Instance for Maybe

Now that we’ve discovered the Monad, let’s use it. And, as always, Maybe is a great place to start.

For reference, here’s the Maybe implementation up to and including Applicative:

```
data Maybe a = Nothing | Just a

instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
  map f (Just x) = Just $ f x

instance applyMaybe :: Apply Maybe where
  apply Nothing _ = Nothing
  apply (Just f) x = f <$> x

instance applicativeMaybe :: Applicative Maybe where
  pure = Just
```

① Don’t forget that f returns a Maybe b. That’s why this code looks so simple.

That may seem too easy. In fact, it is that easy. And, as it turns out, it was easier to write this than it was to write the Applicative Instance. This is a common pattern. And once we learn about ap, writing Applicative Instances will get easy too.

And now for the easiest part, coding the Monad Instance:

```
instance monadMaybe :: Monad Maybe
```

While that was super simple, it comes at a cost. By creating the Monad Instance, we’re promising users of our Type that we’ve giving them a law abiding Monad Instance, which means we need to do the work of proving that we have.

First, we start with the Monad Laws:

```
pure >>= g = g                         [Left Identity (Kleisli)]
f >>= pure = f                         [Right Identity (Kleisli)]
(f >>= g) >>= h = f >>= (g >>= h)      [Associativity (Kleisli)]
(m >>= g) >>= f = m >>= (\x -> g x >>= f)  [Associativity (Bind)]
```

I’ve include both the Kleisli Composition version along with the Bind version of the Associativity Law, where >>= is Monadic Function Composition and >>= is Monadic Function Application.

Remember, a Monadic Function (or Effectful Function) has the Type Signature of a -> m b, where a Pure Function has a -> b.

To prove we have a proper Monad, we’ll want to use the Bind versions of the laws, since our code is for bind. But we’ll first need to convert the Left and Right Identity Laws from Kleisli Composition to bind.

To do this, we’ll need the implementation of composeKleisli, which is written using bind, i.e. >>=:

```
composeKleisli
  :: ∀ a b c m
  . Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f = \x -> f x >>= g ①
```

① Written using a Lambda to keep it easier to convert our laws to use bind.

Once again, we’ll rewrite composeKleisli implementation using infixed notation and with renamed
