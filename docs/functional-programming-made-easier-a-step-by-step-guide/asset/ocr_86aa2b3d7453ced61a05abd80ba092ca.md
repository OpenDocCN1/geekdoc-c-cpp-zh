When the compiler looked at the first Parameter of our call to `many`, it found a `Parser`, `p`, but expected a `Function`. That’s because we added the `cons` Parameter to `many` but forget to add it to our call.

Let’s fix that now:

```
some :: ∀ e a f
     . Unfoldable f
     => (a -> f a -> f a)
     -> Parser e a
     -> Parser e (f a)
some cons p = cons <$> p <*> defer \\_ -> many cons p ①
```

> ① Added `cons` as `many`’s first Parameter.

Now, the compiler is making a similar complaint about `many`, which we’ll fix in a similar way:

```
many' :: ∀ e. Parser e Char -> Parser e String
many' p = fromCharArray <$> many (:) p ①
```

> ① Added the `(:)` Operator as our cons-like Function.

We might as well fix `some'` before the compiler complains about it too:

```
some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <$> some (:) p ①
```

> ① Added the `(:)` Operator as our cons-like Function.

At this point we could stop, but stepping back and looking over the code we’ve written, we can see that `some` will never return an empty `Unfoldable` since it’s supposed to parse 1 or more.

How can we change it to reflect this restriction?

Do you remember `NonEmpty`? Here’s it’s definition:

```
data NonEmpty f a = NonEmpty a (f a)
```

We can use this on `some` but NOT `many` since it can be empty, since `many` is 0 or more. This means that when `many` calls `some`, we’ll have to convert the `NonEmpty` that we get back to something that can be empty.

Okay, so one problem at a time. Let’s first modify `some` to return `NonEmpty`: