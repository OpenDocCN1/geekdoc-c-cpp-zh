
```
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f = State \s -> fx s # \(Tuple x s') -> ???
```
```

Now, we can call f on x, which is the whole point of bind:

```
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> f x -- COMPILER ERROR!
```
```

We’re not surprised by the compiler error because we remember that f is a Monadic Function, which means we’ll need to call runState on f x. We also remember that we’ll need to pass the new State, s', to runState as its second Parameter:

```
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s' ???
```
```

And now we destructure the runState result, which is a Tuple:

```
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s'
      # \(Tuple y s') -> ???
```
```

And now we can finish by putting it all back together:

```
```haskell
instance bindState :: Bind (State s) where
  bind (State fx) f =
    State \s -> fx s # \(Tuple x s') -> runState (f x) s'
      # \(Tuple y s'') -> Tuple y s'' ❶
```
```

❶ What happened here?

Looking at the last Lambda, \(Tuple y s'') -> Tuple y s'', we can see that it’s just identity.

Looks that I got a bit carried away here. We were done when we added runState. So, let’s roll things back a bit:

```
instance bindState :: Bind (State s) where
    bind (State fx) f =
        State \s -> fx s # \(Tuple x s') -> runState (f x) s'
```

And last, but not least, we have the Monad Instance:

```
instance monadState :: Monad (State s)
```

Here's what we've written for State:

```
newtype State s a = State (s -> Tuple a s)

instance functorState :: Functor (State s) where
    map f (State fx) = State \s -> fx s # \(Tuple x s') -> Tuple (f x) s'

instance applyState :: Apply (State s) where
    apply (State ff) (State fx) = State \s -> ff s # \(Tuple g s') -> fx s'
        # \(Tuple x s'') -> Tuple (g x) s''

instance applicativeState :: Applicative (State s) where
    pure x = State \s -> Tuple x s

instance bindState :: Bind (State s) where
    bind (State fx) f =
        State \s -> fx s # \(Tuple x s') -> runState (f x) s'

instance monadState :: Monad (State s)
```

And, not surprisingly, there isn't much code here. A lot of thinking went into coding a little bit of code.

But we're not quite done yet. We still need to write the State API:

```
get :: ∀ s. State s s
put :: ∀ s. s -> State s Unit
modify :: ∀ s. (s -> s) -> State s s
modify_ :: ∀ s. (s -> s) -> State s Unit
```

Here get will retrieve the current State and put will replace the current State.

modify will modify the current State using a Function that takes the old State and returns the new State. modify also returns the new State, whereas, modify_ will do the same as modify but returns Unit instead.

In practice, modify_ is used more often since it doesn’t require a void in a do block and we rarely need the new State back. But, when we do, modify will save us a call to get.

Let’s start with get:

```
get :: ∀ s. State s s
get = ???
```

We need to return a State, so we’ll use our pattern:

```
get :: ∀ s. State s s
get = State \s -> ???
```

And now, all we have to do is return the State UNCHANGED in both slots of the Tuple, since the resulting Pure Computation is the State:

```
get :: ∀ s. State s s
get = State \s -> Tuple s s
```

Here the first s of the Tuple is the Pure Computational result and the second s is the Monadic Computational result. This is just like ask in Reader.

Now, we’ll code put:

```
put :: ∀ s. s -> State s Unit
put s = ???
```

This will be a bit trickier. put gets a new State, s, that’s going to replace whatever State that is passed to it. So, we’re going to start with the pattern we always use to return a State, but, in this case, we’re going to throw away the Parameter, which we usually call s:

```
put :: ∀ s. s -> State s Unit
put s = State \_ -> ??? ①
```

① _ is normally called s but we don’t care about the value of the old State, since we’re replacing it.

And now, we can return the new State, s, and unit wrapped up in a Tuple:

```
put :: ∀ s. s -> State s Unit
put s = State \_ -> Tuple unit s ①
```

① unit is the Pure Computational result and s is the Monadic Computational result.

Can you think of why the return type is State s Unit? What else could we have used instead of Unit?

We could have used an Int, which means we’d returned Tuple 0 s instead of Tuple unit s. But there’s no reason for the 0 or any Int Value for that matter.

Unit here works for 2 reasons. First, it’s a don’t-care Value and second, it has a Discard Instance, which means when we use put in a do block, we won’t have to use void to discard the Value returned.

Now we’ll write modify:

```
modify :: ∀ s. (s -> s) -> State s s
modify f = ???
```

And we need to return a State, so we’ll add our pattern:

```
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> ???
```

Remember that f is used to modify the State by applying it to s. So let’s add that returning the new State as both the Pure Computation and the Monadic one:

```
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> Tuple (f s) (f s)
```

Okay, so, I’m probably being a bit picky here, but I hate the duplication of code. You can stop here if you want but I want to go one step further:

```
modify :: ∀ s. (s -> s) -> State s s
modify f = State \s -> let ns = f s in Tuple ns ns ①
```

① ns is our new State.

Notice the use of the let expression to avoid duplication of code. I’m not sure if the PureScript compiler would have optimized the duplication out in the previous step, so the safe bet is to not have it in the first place.

Now modify_ should be easy. We can copy modify’s implementation making sure to change it to return unit as the Pure Computation:

```
modify_ :: ∀ s. (s -> s) -> State s Unit
modify_ f = State \s -> Tuple unit (f s)
```

Here’s the parallel computation diagram for State:

![](img/8c0e9b687c62642e828ccb5481e11313_744_0.png)

In the diagram, get reads the current Monadic Computation’s result and makes it available to the Pure Computation channel. put, on the other hand, takes a Value and replaces the Monadic Computation with it.

## 18.22. Using State as a Monadic Validation

Earlier we considered making Validation a Monad but ran into problems writing bind. But now that we have the State Monad, we should be able to use it to collect errors. So let’s give it a try.

We’ll start with our example before we starting using Validation example:

```
errIfMissing :: Maybe String -> String -> Either String String
errIfMissing Nothing err = Left err
errIfMissing (Just s) _ = Right s

fullName :: String -> String -> String -> String
fullName first middle last = first <> " " <> middle <> " " <> last

fullNameEither :: Maybe String -> Maybe String -> Maybe String
                -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
           <*> (middle `errIfMissing` "Middle name must exist")
           <*> (last `errIfMissing` "Last name must exist")
```

Take a moment to review this.

And if you remember, we rewrote fullNameEither to use do notation:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String
                -> Either String String
fullNameEither first middle last = do
  f <- errIfMissing first "First name must exist"
  m <- errIfMissing middle "Middle name must exist"
  l <- errIfMissing last "Last name must exist"
  pure $ fullName f m l
```

But both versions of fullNameEither stop at the first error since they're using Either, which Short-circuits. That's why we're going to use State instead of Either.

Let's rewrite errIfMissing so it uses State instead of Either. We'll start with its Type Signature:

```
errIfMissing :: Maybe String -> String -> State ???
```

Now we have to figure out what Type Parameters we're going to need for State. Let's pick Array String as our State, i.e. the first Type Parameter in the State Type Constructor. This way we can collect our errors in an Array:

```
errIfMissing :: Maybe String -> String -> State (Array String) ???
```

By looking at our Either implementation, we see that it returned a String in the success case. So let's try that for our Pure Computation result Type:
