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