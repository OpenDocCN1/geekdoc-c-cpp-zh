At this point, It’s probably a good idea to run the tests again to make sure that we didn’t break anything. Chances are pretty slim since we just changed Types and the compiler is our test for those kinds of changes.

Another point worth making is that our final Type Signatures look scary. But, we didn’t just write these scary Type Signatures the first time. We initially wrote simple ones and as we generalized, we rewrote them over and over until they were more complex. But you saw the process. It’s not magic. And it’s not hard. It’s just many incremental changes from a concrete version of the code to a very abstract version.

So, when you see these kinds of Type Signatures in the wild, don’t panic. If there are Constraints that you don’t know, then go learn them. And if there are Types you’re not familiar with, then go become familiar. Because that’s all it takes as you have now witnessed.

And because we understand both our Types and Classes we used in our Constraints, we can easily justify every part of our Type Signatures, for example, in some:

```
some :: V a f m
  . Unfoldable f
  => Alt m
  => Applicative m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (NonEmpty f a)
```

① An Unfoldable. This is because we used none in many.

② Because we call many and it uses <|>.

③ Because we call many and it uses pure.

④ Because we need to break the infinite loop with defer.

⑤ cons-like Function, which means we expect our Unfoldable to be a list-like structure.

⑥ The original Applicative of a’s that we’re going to leverage to produce a new Applicative. With Parsers, this is a single Parser that we’ll use over and over again as needed.

⑦ Our new Applicative that produces a NonEmpty list-like structure. With Parsers, this is a Parser that will produce a list-like result when the Parser is run.

If we were to look upon this Type Signature for the first time, we might find it intimidating. And it will be if we don’t understand Unfoldable or Lazy, for example. But since we do, we can look at each line one at a time and understand, albeit slowly, what this Type Signature means. And sometimes, we’ll need to look at the implementation of a Function to get the kind of insight as we were able to provide above for some.

For complex Type Signatures like this one, this process may take quite a bit of time, so make sure to set your expectations accordingly. Don’t beat yourself up for taking 20 minutes or more to understand one. Understanding complex things takes time and practice. The more you do it, the faster you’ll get.