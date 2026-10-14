
Applicative.

But this is a Chapter on Monads. And so you might be wondering what does our `SideEffect` Typeclass have to do with Monads?

## 18.4. We Created a `Monad` and More

It turns out that our `SideEffect` class is nearly the `Monad` class from PureScript. In PureScript, the Monad has been factored out into 2 Typeclasses, `Bind` and `Monad`, whereas in Haskell it’s in a single Typeclass.

Here’s our `SideEffect` class for reference:

```
class Applicative f <= SideEffect f where
  applySideEffect :: ∀ a b. f a -> (a -> f b) -> f b
```

And here are `Bind` and `Monad`:

```
class Apply m <= Bind m where
  bind :: ∀ a b. m a -> (a -> m b) -> m b

infixl 1 bind as >>>=

class (Applicative m, Bind m) <= Monad m
```

> ❶ `bind` is equivalent to `applySideEffect`. This should be obvious when you change the `f` Type Parameter to `m` in `SideEffect`.
> 
> ❷ The `>>>=` Operator Alias is for `bind`.
> 
> ❸ No methods for `Monad`. Just implied laws that the programmer must verify.

Notice the use of the Polymorphic Parameter, `m`. That’s because we’re usually thinking in the context of `Monad`, as opposed to `Functor`, when we use these.

One thing to note here is that `Bind` has `Apply` as its Superclass. It doesn’t need `pure` to do it’s job. But `Monad`, on the other hand, absolutely needs it for the same reason we created `makeDebuggable`. It lets us work with Pure Functions. This is why `Monad` has `Applicative` as its Superclass, since `Applicative` implements `pure`.

Next, let’s step back and think about what `Monad` gives us. It basically allows us to compose Functions of the following form:

```
a -> m b
```

Functions of this type are commonly referred to as *Monadic Functions* or *Effectful Functions*. Basically, Function with Side-effects.

But how does `bind` accomplish this kind of composition, especially since it's more akin to Function Application than Function Composition?

Well, remember when we rewrote `composeDebuggable` in terms of `applyDebuggable`?

```
composeDebuggable
  :: ∀ b c d
  . (c -> Debuggable d)
  -> (b -> Debuggable c)
  -> (b -> Debuggable d)
composeDebuggable g f x = f x `applyDebuggable` g
```

But `applyDebuggable` is just `bind` specialized for `Debuggable`.

So let's write the general version of `composeDebuggable` that leverages `bind` to allow us to compose Monadic Functions.

We're going to call it `composeKleisli` for reasons that will become apparent once we talk about the *Kleisli Category*:

```
composeKleisli
  :: ∀ a b c m
  . Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f x = f x >>= g

infixr 5 composeKleisli as >>= ①
```

① This is the Operator Alias for `composeKleisli` and is commonly referred to as the *Fish Operator.*

So `bind`, Monadic Function Application, lets us write `composeKleisli` for `Monads`, just like `$`, Pure Function Application, lets us write `compose` for `Functions`:

```
```haskell
compose
  :: ∀ a b c
  .  (b -> c)
  -> (a -> b)
  -> (a -> c)
compose g f x        = g $ f x

composeKleisli
  :: ∀ a b c m
  .  Monad m
  => (b -> m c)
  -> (a -> m b)
  -> (a -> m c)
composeKleisli g f x  = g =<< f x
```
```

> ① This is normally written as `g (f x)`. By using `$`, it’s easier to see the similarities between the 2 Functions.

> ② I’m using the flipped `bind` operator to help show how `$` and `bind` work similarly in implementing composition.

The implementations are analogous where `g $ f x` is the analogy of `g =<< f x`.

To sum things up, with `Bind` and `Monad`, we have a way of composing and calling Monadic Functions, i.e. Functions that return Side-effects along with their Pure results. And with `pure` from `Applicative`, we have a way to lift a Pure Function into a Monadic one, so it can operate along side of other Monadic Functions.

At its most basic level, the Monad lets us do Function Application and indirectly Function Composition of Monadic Functions.

That’s it. Nothing magical. Nothing complicated. Just very useful and very powerful, as we shall soon see.

## 18.5. An Alternative Monad Implementation

We’re going to look at another equally valid way to implement `Monads`. It’s more in line with the way Mathematician’s see it. And in some languages, `Monad` is implemented in this way. This implementation is Isomorphic to what’s done in PureScript and Haskell.

Let’s look back at `Bind`:

```
```haskell
class Apply m <= Bind m where
  bind :: ∀ a b. m a -> (a -> m b) -> m b
```
```

Since `Apply` is the Superclass of `Bind`, that means that `Bind` is a `Functor`, which means that `Monad` is also a

Functor since Applicative is one of its Superclasses:

```
class (Applicative m, Bind m) <= Monad m
```

Let’s pretend, for a moment, that the Bind Typeclass does NOT exist. We’d still like to have a bind Function but not as a Method of a Typeclass.

We know that a Monad is Functor, so let’s try to write bind as a helper Function, that leverages map:

```
bind :: ∀ a b m. Functor m => m a -> (a -> m b) -> m b
bind x f = map f x --- COMPILER ERROR!!
```

1 m must at least be a Functor since we’re using map.

Attempting to write bind in terms of map gives us the following compiler error:

![](img/8c0e9b687c62642e828ccb5481e11313_676_0.png)

The error talks about m0 b1 and b1 not matching. If it’s not clear what the problem is, then it’s time to write out our Types:

```
map :: (a -> b) -> m a -> m b
f :: a -> m b
map f :: m a -> m (m b)
map f x :: m (m b)
```

1 Our Functor, usually signified with f, is our Monad, m. So this Type Signature has m in it to make things easier.

2 Here’s where things go wrong. map expects a Function with Type a -> b but we gave it a Function with Type a -> m b.

③ This final Type doesn’t match our bind Type Signature.

Here we wound up with an m b where we only wanted a b. Look back at the error message. That’s exactly what the compiler was complaining about.

So now, what do we need to fix this?

We need a Function, which I’ll call join, that does the following:

```
join :: ∀ a m. m (m a) -> m a
```

This basically flattens out one of the Monad Contexts. In fact, in other Functional Languages, e.g. Scala, this Function is called flatten. But in PureScript and Haskell it’s called join.

So, instead of implementing a Bind Typeclass, we could implement a Typeclass that has join as its Member:

```
class Apply m <= Join m where
  join :: ∀ a. m (m a) -> m a ①
```

① I’ve dropped m from ∀ in the Type Signature since it can now be found in the Typeclass definition.

Our alternative Monad definition uses Join instead of Bind:

```
class (Applicative m, Join m) <= Monad ①
```

① Join instead of Bind.

And now we can fix our bind Function:

```
bind :: ∀ a b m. Join m => m a -> (a -> m b) -> m b ①
bind x f = join $ map f x ②
```

① Now it has to at least be a Join since we’re using join.

② We use join after map has left us with doubly nested m’s. It will flatten out one of the m’s.

When this approach is taken for Monad, bind is typically called flatMap, which should be apparent from its implementation:

```
flatMap :: ∀ a b m. Monad m => m a -> (a -> m b) -> m b ①
flatMap x f = flatten $ map f x ②
```

① bind has been renamed to flatMap.

② join has been renamed to flatten.

I've included this alternative view on Monad in case you take what you've learned here to languages that use flatMap or if you watch Functional Programming talks in Scala.

## 18.6. Back to PureScript's Monad Implementation

We saw in the previous section a Function join that was used to implement an alternative, but Isomorphic, version of Monad. And if it's Isomorphic, we should be able to write join in terms of things from our Monad implementation, i.e. the PureScript one.

Let's look at the Type Signature for join:

```
join :: ∀ a m. Bind m => m (m a) -> m a ①
```

① In the PureScript implementation, m needs to be at least a Bind.

Now, let's write the code:

```
join :: ∀ a m. Bind m => m (m a) -> m a
join x = ???
```

What things from our Bind or Monad implementation can we use to accomplish join's task?

We know that m is a Bind, which means we COULD use bind or >>= . To see if bind will work for us, let's look to it's definition:

```
class Apply m <= Bind m where
  bind :: ∀ a b. m a -> (a -> m b) -> m b
```

Notice how bind MUST break into its first Parameter, m a, to get at the a before it can call the Function, a -> m b.

This will get rid of one layer of Context, i.e. m. So far this looks promising since we want join to remove a layer of Context.

So, let's try using bind to see if it works for us:

```
join :: ∀ a m. Bind m => m (m a) -> m a
join x = x >>= ??? ①
```
