
Now, we’re going to call `fullName` with one Parameter at a time but only AFTER that Parameter has been passed through our validation function, `errIfMissing`.

Unfortunately, `errIfMissing` returns an `Either String String` but `fullName` expects `Strings` as Parameters:

```
fullName :: String -> String -> String -> String
```

But we can map `fullName` over `Either String String` since the second Parameter of `Either String String` is `String`.

So, let’s at least do that for the first parameter to see where that takes us:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
  ???
```

> We map `fullName` over `Either String String`, which will result in a Partially Applied Function in a Context, viz. `Either`.

We’re not done yet. This doesn’t compile and for good reason. The Types don’t match:

```
fullName <$> (first `errIfMissing` "First name must exist")
  :: Either String (String -> String -> String)
```

At this point, we now have a Partially Applied function in a Context, viz. `Either`. Notice that it’s waiting for 2 more `Strings`, i.e `middle` and `last`.

This is where `Applicatives` shine.

So let’s use `<*>` to pass `middle` and `last` to our enclosed function, but first we’ll pass those values through our validation function, `errIfMissing`:

```
fullNameEither :: Maybe String -> Maybe String -> Maybe String
             -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
          <*> (middle `errIfMissing` "Middle name must exist")
          <*> (last `errIfMissing` "Last name must exist")
```

This approach is far better than our previous one. We kept our simple function simple and leveraged it from our validating version. Our validation logic is also factored out into a helper function.

Here’s our final implementation:

```
errIfMissing :: Maybe String -> String -> Either String String
errIfMissing Nothing err = Left err
errIfMissing (Just s) _ = Right s

fullName :: String -> String -> String -> String
fullName first middle last = first <> " " <> middle <> " " <> last

fullNameEither :: Maybe String -> Maybe String -> Maybe String -> Either String String
fullNameEither first middle last =
  fullName <$> (first `errIfMissing` "First name must exist")
           <*> (middle `errIfMissing` "Middle name must exist")
           <*> (last `errIfMissing` "Last name must exist")
```

## 16.9. Applicative Effects

In an earlier Chapter, Semantics was discussed regarding Types, in particular, what exactly does it mean to use Maybe or Either. We concluded that Maybe’s Implicit Behavior was to short-circuit. That’s because it was dictated by the Type’s structure.

In contrast, Either also short-circuits but the Type didn’t dictate that behavior, but instead was a conscious choice, which is why we called it an Explicit Behavior.

While I prefer the more nuanced look at these attributes of our Types, they tend to get lumped into a single term, Effects. The trouble with this term is that it’s poorly defined and overloaded. I suspect this is for historical reasons.

In the early days of Haskell, for example, they had no way of doing Effects. They literally could only do pure function calls. Effects were solved by using Monads, which strangely enough existed in the language before Applicatives.

And since all Monads are Applicatives, and many Functors can be made into both Applicatives and Monads, there became a need to identify the "effect" of the Maybe Monad, which is to short-circuit.

So be careful when it’s used to make sure to understand whether they’re talking about the behavior of a Type or a real-world side-effect, e.g. writing data to a database.

Keeping this in mind, let’s look at another example of using Applicatives to combine a list of Effects. Let’s imagine we map a function over a List of values and that function returns an Applicative, e.g. a Maybe.

Since the function returns a Maybe, we can safely conclude that that function could fail. And now we want to get a final result from that List by combining the results into a single result of success or failure. We’d also like to be able to do the same with Either.

But instead of writing it just for success and failure Applicatives, we’re going to write a general combining function called combineList.

Here’s its Type Signature:

```
combineList :: ∀ a f. Applicative f => List (f a) -> f (List a)
```

In the case where f is Maybe, we’ll get a Maybe (List a).

And if f is Either a then we’ll get an Either a(List b).

Realize that the "effect" of Maybe and Either are to short-circuit. Other Applicatives could have different "effects".

But with Maybe, we’d expect that if there are any errors in our List, i.e. Nothing, that we’ll get a final result of an error, i.e. Nothing.

And the same with Either. If there’s a single error in the list, i.e. Left, we’ll get a Left.

Let’s remind ourselves of Maybe’s Apply Instance:

```
instance applyMaybe :: Apply Maybe where
  apply (Just f) x = f <$> x
  apply Nothing _ = Nothing ①
```

① Applying a Nothing to anything will result in Nothing.

From this code, it should be easy to see that if we combine a List of Maybes with <*>, we’ll get a final result of Nothing if any of the elements of that List are Nothing. This is Maybe’s short-circuit "effect" in action.

Now we’ll finish writing combineList. First, the base case:

```
combineList :: ∀ a f. Applicative f => List (f a) -> f (List a)
combineList Nil = pure Nil
```

If given an empty List, we simply wrap it up in the Context, using pure.

Next, we write the recursive case:

```
```haskell
combineList :: ∀ a f. Applicative f => List (f a)
combineList Nil       = pure Nil
combineList (x : xs)  = Cons <$> x <**> combineList xs
```
```

Cons is a Data Constructor that takes a value and a List and produces a List.

Remember, we have a List of values of Type a that are in some Context, f. So we cannot pass them directly to Cons but must use <$> and <**>.

If this is still a brain bender, let’s look at the recursive case one step at a time. Pay close attention to the Types:

```
```haskell
Cons :: ∀ a. a -> List a -> List a
```
```

Here Cons takes a value and a List and produces a List, after placing that value at the head.

Next step:

```
```haskell
x :: f a
Cons <$> x :: f (List a -> List a)
```
```

Once we mapped Cons over the Applicative, x, we’re stuck with a function in a Context. That means it’s time to break out apply, <**>:

```
```haskell
combineList xs :: f (List a)
Cons <$> x <**> combineList xs :: f (List a)
```
```

And finally, we’re applying combineList xs to the function in the Context resulting in a List a in Context f.

Let’s see how our new function works. First with Maybe:

```
```haskell
import Data.List (fromFoldable)

combineList (fromFoldable [Just 1, Just 2, Just 3])
  -- (Just (1 : 2 : 3 : Nil))
combineList (fromFoldable [Just 1, Nothing, Just 3])
  -- Nothing
```
```

We import a helper function to convert any Foldable to a List. This is convenient since the syntax for an Array is simpler than for List.

Notice that a single Nothing in the List, short-circuits and produces Nothing.

Just in case this still seems like Black Magic, we’re going to look at a simpler version of this example one step at a time.

Here’s our function:

```
combineList :: ∀ a f. Applicative f => List (f a) -> f (List a)
combineList Nil      = pure Nil ①
combineList (x : xs) = Cons <$> x <*> combineList xs ②
```

We’re going to do Algebraic Substitution and Function Application to see how each step of the computation process works:

```
combineList (fromFoldable [Just 1, Just 2])                 -- Given
combineList (Just 1 : Just 2 : Nil)                         -- Apply fromFoldable
Cons <$> Just 1 <*> combineList (Just 2 : Nil)              -- Substitute into ②
Just (Cons 1) <*> combineList (Just 2 : Nil)                -- Apply $<>
Just (Cons 1) <*> (Cons <$> Just 2 <*> combineList Nil)     -- Substitute into ②
Just (Cons 1) <*> (Just (Cons 2) <*> combineList Nil)       -- Apply $<>
Just (Cons 1) <*> (Just (Cons 2) <*> pure Nil)              -- Substitute into ①
Just (Cons 1) <*> (Just (Cons 2 Nil))                       -- Apply <*>
Just (Cons 1 (Cons 2 Nil))                                  -- Apply <*>
Just (1 : 2 : Nil)                                          -- Rewrite with :
```

Now let’s look at Either:

```
import Data.List (fromFoldable)

combineList (fromFoldable [Right 1, Right 2, Right 3])
  -- (Right (1 : 2 : 3 : Nil))
combineList (fromFoldable [Right 1, Left "err", Right 3, Left "err2"])
  -- (Left "err")
```

And we see that the FIRST Left short-circuited to produce Left "err". The rest of the List was effectively ignored.

It’s important to understand that it was still processed since PureScript is a Strict language. In Haskell, a Lazy language, this would NOT be the true making Haskell more efficient in this case.
