```
```haskell
log $ show $ parse' threeChars "A" ❶
```
```

❶ Prints `(Left EOF)`.

Go ahead and run that. You should see how it returns our EOF error. That’s because it ran out of data when processing the String. The Parser would consume 3 characters but the String only had 1.

Now what if I asked you to write a Function that consumes 10 characters? Would you write the following:

```
```haskell
tenChars :: ∀ e. Parser e String
tenChars = (\c1 c2 c3 c4 c5 c6 c7 c8 c9 c10 ->
  fromCharArray [c1, c2, c3, c4, c5, c6, c7, c8, c9, c10])
  <$> char <*> char <*> char <*> char <*> char <*> char
  <*> char <*> char <*> char <*> char
```
```

I should hope not or at least you’d question your sanity after you had. I know I am questioning mine as I type this.

What we really need is a better mechanism for taking our Parser, char, and making it consume a specific number of characters.

But how? First of all, let’s look at my insane implementation for tenChars. Notice we have 10 instances of char and we keep applying them to each other. Can you remember what we’ve seen that does this?

If you said Traversable, then kudos to you. If not, don’t worry, I didn’t think of using Traversal either. I cheated and looked at what was done in Haskell’s parsec library.

So, the first thing that we’ll need is a way to duplicate the Parser in an Array. This can be accomplished with a Function called replicate from Data.Array.

The next thing we’ll need to do is to run sequence over it to apply the parser over and over again.

Let’s refresh our memories regarding the Traversable Typeclass:

```
```haskell
class (Functor t, Foldable t) <= Traversable t where
  traverse :: ∀ a b m. Applicative m => (a -> m b) -> t a -> m (t b)
  sequence :: ∀ a m. Applicative m => t (m a) -> m (t a)
```
```

In our usage case, t is Array and m is our Parser e, which is an Applicative.

So we want a Parser, which we’ll call count, that takes a count and a Parser that parses an a and produces a new Parser that produces Array a, i.e a bunch of a’s.

Go ahead and just write the Type Signature for count before reading on.