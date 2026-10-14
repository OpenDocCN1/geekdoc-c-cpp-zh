
bimap:

```
rmap :: ∀ f a b c. Bifunctor f => (b -> c) -> f a b -> f a c
rmap = bimap identity ①
```

① Written in Point-free notation where the function is unnamed.

Now we can write lmap’s Type Signature:

```
lmap :: ∀ f a b c. Bifunctor f => (a -> c) -> f a b -> f c b ①
```

① Notice the function a -> c maps over the LEFT Type Parameter and takes a f a b and turns it into a f c b.

And finally, we write the implementation for lmap leveraging bimap:

```
lmap :: ∀ f a b c. Bifunctor f => (a -> c) -> f a b -> f c b
lmap f = bimap f identity ①
```

① This could’ve been written Point-free by using flip, but in this case, it would make the code more verbose. For the curious, the Point-free version is: lmap = flip bimap identity.

Now we’re ready to start writing the instance for Either. We’ll start by writing its Type definition:

```
data Either a b = Left a | Right b ①
```

① Either’s Kind is Type -> Type -> Type

Next, let’s write the instance definition:

```
instance bifunctorEither :: Bifunctor Either where ①
```

① Either’s Kind Signature matches f’s in the Bifunctor Typeclass, so we can just specify it without any Type Parameters.

And now, let’s add the implementation for the Left case:

```
instance bifunctorEither :: Bifunctor Either where
  bimap f _ (Left err)  = Left $ f err ①
```

① In this case, we don’t care about the RIGHT mapping function. This is because Either is a Sum Type (Coproduct). We will care when we write bimap for Product Types.

And finally, we code the Right case:

```
instance biFunctorEither :: Bifunctor Either where
  bimap f _ (Left err)  = Left $ f err
  bimap _ g (Right x)   = Right $ g x ①
```

① In this case, we don’t care about the LEFT mapping function.

## 13.12. Writing Bifunctor Instance for Tuple

Unlike Either, Tuple is a Product Type, i.e. both of its Type Parameters are present at the same time. So keep this in mind while coding its Bifunctor Instance.

Here’s the test code that you should add:

```
log $ show $ rmap (_ * 2) $ Tuple 80 40 ①
log $ show $ lmap (_ / 2) $ Tuple 80 40 ②
log $ show $ bimap (_ / 2) (_ * 2) $ Tuple 80 40 ③
```

① Prints (Tuple 80 80).

② Prints (Tuple 40 40).

③ Prints (Tuple 40 80).

Notice that we didn’t run into any of the problems that we did with our Either test code. That’s because Tuple is a Product Type and both of its Type Parameters are present in all of its Inhabitants. The compiler can know full well that a and b are both Ints.

Now based on what we’ve done earlier, writing Bifunctor for Tuple should go pretty smoothly. After you’ve written it, continue on.

## 13.13. Code for Bifunctor Instance for Tuple

First we write the instance definition:

```
instance biFunctorTuple :: Bifunctor Tuple where
```

And finally, we write the bimap Method:

```
instance bifunctorTuple :: Bifunctor Tuple where
  bimap f g (Tuple x y) = Tuple (f x) (g y) ①
```

## 13.16. Validating the Bifunctor Laws

Now, we’re ready to validate the `Bifunctor` laws. When we did this for `Functor`, we used code. This time we’re going to use Algebraic Substitution.

Let’s review the laws:

```
bimap identity identity = identity        [Identity]
bimap (g1 <<< f1) (g2 <<< f2) =
        bimap g1 g2 <<< bimap f1 f2        [Composition]
```

Put into words, the `Identity` law states that if you `bimap` using `identity` on both the right and the left, it has the same affect as just using the `identity` function. And the `Composition` law states that composing 2 functions on both sides is equivalent to `bimapping` with one function set and then composing with `bimapping` with the other.

Let’s validate that our `Tuple` implementation is a law-abiding `Bifunctor`:

```
instance bifunctorTuple :: Bifunctor Tuple where
  bimap f g (Tuple x y) = Tuple (f x) (g y)
```

We’re going to substitute starting on the left-hand side and then the right until the two sides are equal, which proves that we’re law-abiding.

Let’s start with the `Identity` law:

```
bimap identity identity (Tuple x y)
                       = identity (Tuple x y) -- Given
Tuple (identity x) (identity y)
                       = identity (Tuple x y) -- Subst into
Tuple x y = identity (Tuple x y)          -- Function application
Tuple x y = Tuple x y                      -- Function application
```

Next the `Composition` law:

```
bimap (g1 <<< f1) (g2 <<< f2) (Tuple x y)
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Given
Tuple (g1 <<< f1 $ x) (g2 <<< f2 $ y)
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Subst into ❶
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Compose equivalence
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 (bimap f1 f2 (Tuple x y)) — Compose equivalence
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 (Tuple (f1 x) (f2 y)) — Subst into ❶
Tuple (g1 (f1 x)) (g2 (f2 y))
    = Tuple (g1 (f1 x)) (g2 (f2 y)) — Subst into ❶
```

# Chapter 14. More Functors

So far, we’ve only considered Functors that contained Values. But technically, a Function is a Value. So can a Functor contain a Function?

Of course, it can and these sorts of Functors are some of the most powerful and useful Functors we will use. But before we delve into Functors of Functions, let’s do a quick recap of Functors of Values.

## 14.1. Functors of Values

Here are some generic Product Types with 1 and 2 Parameters:

```
newtype PV1 a = PV1 a
data PV2 a b = PV2 a b
```

Writing their Functor Instances is pretty mechanical:

```
instance functorPV1 :: Functor PV1 where
  map f (PV1 x) = PV1 (f x)

instance functorPV2 :: Functor (PV2 a) where
  map f (PV2 x y) = PV2 x (f y)
```

Notice how we use the function, f. We immediately apply it to the Values to produce new Values within the Context. This is an important distinction that will be more apparent when those Values are Functions.

Here are some generic Sum Types with 1 or 2 Parameters:

```
data SV1 a = Nought | SV1 a
data SV2 a b = Nada | SV2A a | SV2B b
```

And writing the Functor Instances for these is equally mechanical:

```
instance functorSV1 :: Functor SV1 where
    map _ Nought = Nought
    map f (SV1 x) = SV1 (f x)

instance functorSV2 :: Functor (SV2 a) where
    map _ Nada = Nada
    map _ (SV2A x) = SV2A x
    map f (SV2B y) = SV2B (f y)
```

Once again, we apply the function f immediately to the Values.

## 14.2. Functors of Functions

But what happens when we have the following Type:

```
newtype F1 a = F1 (Int -> a)
```

How do we write the Functor Instance for F1? Let's give it a try:

```
instance functorF1 :: Functor F1 where
    map f (F1 g) = F1 (???) ①
```

① We need to combine f and g somehow.

How do we combine functions? Well, usually through Composition, but it really depends. We also have to make sure that Types match. So, let's look at the Types in detail.

First, our mapping function's Type Signature:

```
f :: a -> b
```

Nothing special here. This is the standard Type Signature for any Functor's mapping function.

Next, let's add F1 Function's Type, g:

```
f :: a -> b
g :: Int -> a
```

And finally, let's add the composition of f and g:

```
f :: a -> b
g :: Int -> a
g <<< f --- COMPILER ERROR!! ①
f <<< g :: Int -> b ②
```

① Cannot compose this way since the Types don’t match.

② This is a clue that composition will probably give us what we want since Int -> b is the resulting Type Signature that we’re expecting after we call map on F1.

Looks like f <<< g is our answer since it gives us the correct Type Signature. Just for fun, let’s return to our attempt to the write F1’s Functor and look at this from another perspective:

```
instance functorF1 :: Functor F1 where
  map f (F1 g) = F1 (???)
```

In place of the ???, we need a function that takes Ints and returns bs. If we start with g which takes Ints and returns a’s, we can use f to convert those a’s into a b’s, which is exactly the return Type we’re looking for.

This also shows us that we can compose the two functions using f to convert the output of g to get the desired Type:

```
instance functorF1 :: Functor F1 where
  map f (F1 g) = F1 (f <<< g)
```

Notice that when we map over Types that have Functions instead of Values, we don’t apply the Function to the Value. Instead, we compose the Functions. This is an important distinction that we should keep in mind moving forward.

Let’s try another:

```
newtype C1 a = C1 (a -> Int)
```

This is pretty similar to our F1 with the only difference being that C1 contains a Function whose Type Signature is backwards from F1.

But no matter, we should write the Functor next:

```
instance functorC1 :: Functor C1 where
  map f (C1 g) = C1 (f <<< g) -- COMPILER ERROR!!
```
