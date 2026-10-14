
② Here empty is the analogy of mempty in Monoid.

Let’s write a few instances of Plus:

```
instance plusList :: Plus List where
    empty = Nil

instance plusArray :: Plus Array where
    empty = []

instance plusMaybe :: Plus Maybe where
    empty = Nothing
```

With List and Array, these empty values are like the Empty Set, which doesn’t change the original Set when applying a UNION operation, i.e. <|> from Alt.

And with Maybe, Nothing doesn’t change the choice result since we don’t choose Nothing unless we have no other choice.

These act exactly like mempty does from Monoid, i.e. they are Identity Values.

But what about Either?

```
instance plusEither :: Plus (Either a) where
    empty = ??? ①
```

① We need some empty value here that will work with ALL Either a’s.

Here we are stuck. You might think that we could simply constrain b to be a Monoid and then write the following:

```
-- COMPILER ERROR!!
instance plusEither :: Monoid b => Plus (Either a) where
    empty = Right mempty
```

We cannot write an empty value for every possible Either a since the second Type Parameter of Either, which is b, cannot be constrained since it’s not part of the instance definition.

You might think that we could just define it:

```
-- COMPILER ERROR!!
instance plusEither :: ∀ b. Monoid b => Plus (Either a) where
  empty = Right mempty
```

But unfortunately, ∀ b is not allowed here and even if it was, there’s no way to tell the compiler that the b we’re referring to here is the second Type Parameter of Either.

So it is IMPOSSIBLE to write an instance of Plus for Either.

This is the first time we’ve encountered such a limitation. But as we move on to higher and higher levels of abstraction, we will encounter situations where writing an instance for our Types either doesn’t make sense or break laws or produces undesirable results or simply cannot be done.

# 16.19. Plus Laws

And of course, there are laws:

```
empty <|> x = x          [Left Identity]
x <|> empty = x          [Right Identity]
f <$> empty = empty      [Annihilation]
```

The 2 Identity Laws are identical to the Monoid laws.

And the Annihilation Law tells us that mapping has NO affect on the Empty Value, which is evidenced by Maybe’s empty being Nothing, which when mapped over, produces Nothing.

# 16.20. Alternative Functor

We combine Applicative with Plus (a Subclass of Alt) to produce the Alternative Functor:

```
class (Applicative f, Plus f) <= Alternative f
```

Notice that there are no Typeclass Methods. An Alternative has all the methods of Applicative AND Plus and NO Methods unique to itself.

Alternative has a complex hierarchy. So here’s a diagram to help cement it in our minds:

![](img/8c0e9b687c62642e828ccb5481e11313_586_0.png)

A canonical use of Alternative is in Parsers. We’re going to write an Applicative Parser in the next Chapter and we’ll then expand that Parser to be Monadic one once we learn about Monads.

But for now, imagine that the functions num and words are Parsers and that Parser is an Applicative Parser that has an Alternative instance.

Then here’s how we could use Alternative:

```
data Token
  = Word String
  | Num Int
  | WordNum String Int

wordOrNum :: Parser Token
wordOrNum = Num <$> num <|> Word <$> word ①

wordAndNum :: Parser Token
wordAndNum = WordNum <$> word <*> num ②
```

① Since num and word are Applicative Functors, we need to map our Data Constructors over them.

② We use <*> since WordNum takes 2 Parameters.

wordOrNum will first try to parse for a number and if and only if that fails, it will then try to parse a word.

wordAndNum will parse a word and then immediately parse a number, e.g. abc123.

Don’t worry if these Parser functions are a bit obtuse. One of the exercises in the next Chapter is to build an

This coding Chapter is going to differ from earlier ones. You’re going to code like all the exercise Chapters, but sometimes we’ll code together when the going gets rough.

# 17.1. Writing `Applicative` Instance for `Maybe`

Create the `Maybe` Type from scratch providing all of the prerequisites for Applicative:

+   - Define the Type
+   - Create a `Show` Instance using `genericShow` (for our test code)
+   - Create a `Functor` Instance
+   - Create an `Apply` Instance
+   - Create an `Applicative` Instance

We’ve already done some of this before, but do yourself a favor and don’t look back at your old code. Write this from scratch for practice. The more times you write this the better.

Here’s the test code that you can now replace the placeholder test code with:

```
log $ show $ (+) <$> Just 21 <*> Just 21 ❶
log $ show $ (*) <$> pure 2 <*> (pure 21 :: Maybe Int) ❷ ❸
log $ show $ pure (+) <*> Just 17 <*> Just 25 ❹
```

+   ❶ Prints `(Just 42)`.
+   
+   ❷ Prints `(Just 42)`.
+   
+   ❸ The compiler has no way to know which `pure` we’re using here. So we let it know by telling it that one of the `pure` calls is a `Maybe`. It’ll be able to figure out the other from that.
+   
+   ❹ Prints `(Just 42)`.

So go ahead and write the code using the above 5-step plan before reading on.

# 17.2. Code for `Applicative` Instance for `Maybe`

We start out by creating the Type:

```
data Maybe a = Nothing | Just a
```

Then deriving `Generic` so we can use `genericShow`:

```
```haskell
import Data.Generic.Rep (class Generic) ❶

data Maybe a = Nothing | Just a
derive instance genericMaybe :: Generic (Maybe a) _ ❷
```
```

+   ❶ We need to import the `Generic` class, hence the `class` keyword.
+   
+   ❷ Derive `Generic`.

Next, we write the `Show` instance:

```
```haskell
import Data.Show.Generic (genericShow) ❶

instance showMaybe :: Show a => Show (Maybe a) where
  show = genericShow
```
```

+   ❶ We need to import `genericShow`.

And then the `Functor` instance:

```
```haskell
instance functorMaybe :: Functor Maybe where
  map f (Just x) = Just $ f x
  map _ Nothing = Nothing
```
```

At this point, we are embarking on new territory. So let’s write the `Apply`, one line at a time:

```
```haskell
instance applyMaybe :: Apply Maybe where
```
```

Remember, that `Apply`'s Type Parameter is of Kind `Type -> Type`, which is why we specify `Maybe` instead of `Maybe a`.

Next, we’ll write the `Just` case:

```
```haskell
instance applyMaybe :: Apply Maybe where
  apply (Just f) x = f <$> x
```
```

We only unwrap (or destructure) the first Parameter to gain access the Function, `f` so we can apply it. Once we do, we leverage `map`’s code, which will handle 2 cases for us. The first case `<$>` handles is where the second Parameter, `x` is `Just x`. And the other case is when `x` is `Nothing`.

By leveraging map, we don’t have worry about those cases here. That means we only have 1 more case to consider and that’s when the first parameter is `Nothing`:

```
instance applyMaybe :: Apply Maybe where
  apply (Just f) x     = f <$> x
  apply Nothing _      = Nothing
```

We cannot apply a Function we don’t have, so we all we can do is return Nothing. This is in keeping with the Semantics of Maybe.

Next, we’ll write the Applicative Instance one line at a time:

```
instance applicativeMaybe :: Applicative Maybe where
```

We use Maybe here and not Maybe a for the same reasons we did for Apply.

And since Applicative only has a single Method, pure, we only need to write that. But before we do, let’s think about what pure should be.

Remember, that pure takes a Pure Value or a Pure Function (which technically is a Value) and wraps it in the Context. This is helpful when we want to use it with Functions that expect values in a particular Context, e.g. <*> expects this.

So we have to options for implementing pure. We could make pure return Nothing or Just x (where x is our Pure Value). If we were to pick Nothing, we would NEVER be able to use Pure Values with Contextual ones since we would annihilate the value. That’s a hugely undesirable limitation.

Also, if we use Nothing, we’d break the Identity Laws for Applicative, which if we think about, is in place so we don’t do something destructive like use Nothing.

So the only reasonable, law-abiding and useful option is to use Just:

```
instance applicativeMaybe :: Applicative Maybe where
  pure = Just ①
```

① Written in Point-free Notation.

Test your code to see if it prints out the expected results.

# 17.3. Writing Applicative Instance for Either

We’re going to write the Applicative Instance for Either in exactly the same way we did with Maybe except our test code is going to verify the Applicative Laws (which include the Apply Laws). So we’ll need to add the Eq instance to Either.

But instead of writing Eq and Functor, we’re going to derive it and let the compiler do some work for us.
