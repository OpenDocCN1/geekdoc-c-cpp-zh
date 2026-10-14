Next, we’ll write the Bind Instance.

We’ll start with the definition:

```
instance bindReader :: Bind (Reader r) where
```

And then the left-hand side of bind:

```
instance bindReader :: Bind (Reader r) where
  bind (Reader fx) f = ???
```

We’ve destructured Reader to unwrap fx, which is a Function, which, when called with an r, will return a Value.

Now we add our, all too familiar, pattern:

```
instance bindReader :: Bind (Reader r) where
  bind (Reader fx) f = Reader \r -> ???
```

This is where things get difficult. So, let’s go slowly through building a strategy for how to attack this problem.

First, we’ll need to get the Value from fx by passing it r. Then we can apply that result to f. But unlike the mapping Functions in Functor or Apply, our f is a Monadic Function, i.e. it returns an Reader r b not b.

So, we’re probably going to have a Type mismatch problem, i.e. a Reader inside of another Reader instead of just a Reader.

There are 2 approaches for moving forward. The first is to just code up what we know we need to do and see what complaints the compiler makes and figure out what to do afterwards. This approach is risky since the compiler won’t always be helpful.

The second approach is to write out all the Types and figure out how to code it from that. This is less risky and will always work, but requires a bit more effort.

If the first approach fails us, then we’ll be forced to use the second approach.

So, let’s be lazy and start with the first approach and if we have to, we can always fallback to the second.

We know we have to call f with the Value fx r. So, we’ll write just that and hope the compiler error can help us: