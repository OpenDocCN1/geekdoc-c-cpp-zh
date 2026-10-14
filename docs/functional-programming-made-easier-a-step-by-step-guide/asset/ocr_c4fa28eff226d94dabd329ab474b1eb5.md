+   5. The code we wrote that the compiler is complaining about.
+   6. The actual Type we want.

What we want is `Reader r b` but we have `Reader r (Reader r b)`, i.e. the `b` part in what we want has a `Reader r b` in it instead. This is exactly what the compiler was trying to tell us earlier. It found a `Reader r0 b1` where a `b1` should be. It’s obvious now, but only after we wrote out all of the Types. It figures.

How do we fix this? We have a `Reader` inside of another `Reader`, or more generally a `Monad` inside another `Monad`.

Do you remember `join`? What does join do?

Here’s the definition for `join`:

```
join :: ∀ a m. Bind m => m (m a) -> m a
join x = x >>= identity
```

This may be a bit too abstract. So let’s replace `m` with `Reader r` in the Type Signature:

```
join :: ∀ a. (Reader r) ((Reader r) a) -> (Reader r) a
```

And we’ll remove the extra Parentheses and replace `a` with `b` to better match our situation:

```
join :: ∀ b. Reader r (Reader r b) -> Reader r b
```

This will take our `Reader r (Reader r b)`, i.e. the Type our code returns, and give us `Reader r b`, i.e. the Type we ultimately want. That should work.

So let’s add join as the final step in our code:

```
instance bindReader :: Bind (Reader r) where
  bind (Reader fx) f = join $ Reader \\r -> f $ fx r
```

And now the compiler is happy. But we won’t be. It’s probably not obvious why, but I’ve made this mistake way too many times and I want to save you the headache.

It’s possible to write a Function that makes the compiler happy, but that doesn’t mean that we’ll be. For example, here’s a Function that makes the compiler happy: