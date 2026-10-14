
# 12.4. Higher-kinded Types

We talked about how values are grouped by Type and how Types are grouped by Kinds, e.g. `Maybe`'s Kind Signature is:

```
Maybe :: Type -> Type
```

`Maybe` takes a `Type` and returns a `Type`. Unlike `Int`:

```
Int :: Type
```

`Int` is just a `Type`. And `Either` takes 2 Types:

```
Either :: Type -> Type -> Type
```

If you like, you can get the Kinds of Types in the PureScript REPL:

```
```text
$ npx spago repl

> import Data.Either
> :k Either
Type -> Type -> Type
> ^D
See ya!
()
$
```
```

❶ `:k` is short for `:kind`.

❷ Control-D to exit the REPL.

`Maybe` and `Either` look like functions and we can conceptualize them as such. They are in fact *Type Constructors*, which is analogous to *Data Constructors*, which are functions.

> Any Type Constructor that takes 1 or more Parameters is a High-kinded Type.

`Int` is not a Higher-kinded Type like `Maybe` and `Either` since it takes NO Type Parameters.

We can draw analogies between the *Value Space* and *Type Space* in our programs:

| Value | 10 :: Int |
| Function | f :: Int -> Int |
| Type | Int :: Type |
| Higher-kinded Type | Maybe :: Type -> Type |

Notice the parallelism between Value and Type. Also, the parallelism between Function and Higher-kinded Type.

# 12.5. Functions with Simple Types

When we work with Simple Types, i.e. not Higher-kinded, we can write functions like:

```
f :: ∀ a b. a -> b
g :: ∀ b c. b -> c
h :: ∀ c d. c -> d
```

and then compose them:

```
hgf :: ∀ a d. a -> d
hgf = h <<< g <<< f
```

In Mathematics, functions map from the Domain to the Codomain. The Domain and Codomain are Sets whose elements are values:

![](img/8c0e9b687c62642e828ccb5481e11313_410_0.png)

We say that a function maps elements in the Domain to elements in the Codomain.

But in Programming, our Domain and Codomain are Types and the elements are the Inhabitants of those Types:

![](img/8c0e9b687c62642e828ccb5481e11313_410_1.png)

Here we show the composition of f, g and h and their mappings from the Set of Type a to Type b and so forth. The inhabitants of Type a are the elements of the Type a Set.

And this image also holds true for repeated Function Application:

```
fgh :: ∀ a d. a -> d
fgh x = h $ g $ f x
```

Function Composition and Function Application are the bread of butter of Functional Programming. We are able to leverage smaller things to solve bigger problems, e.g. use Atoms to make Molecules.

Notice how all of our Types so far are Simple Types like Int, String, Number, etc. But what happens when we consider the case of failure, e.g. what if g could fail:

```
g :: ∀ b c. b -> Maybe c -- returns a Higher-kinded Type
```

We can compose it with f without issue:

```
gf :: ∀ a c. a -> Maybe c
gf = f <<< g
```

And we can do Function Application with it too:

```
fg :: ∀ a c. a -> Maybe c
fg x = g $ f x
```

But what happens when we want to Compose or Apply h?

The problem is h takes a c not a Maybe c. We could always rewrite h or make a specialized version of h that takes a Maybe, but that just opens up a can of worms. Our h function works with Simple Types but not with Higher-kinded Types.

Functors and Monads solve these problems. We will cover the solutions to this seemingly simple problem in great detail in this and the next few Chapters. And along the way, we will discover the real power of these concepts.

These concepts are too often skimmed over in other texts or introduced far too early. We’ve taken hundreds of pages to get here with the hope that you’re comfortable with the underlying concepts before delving into these Abstractions. And, hopefully, you are now able to concentrate on just the concepts at hand.

These Abstractions will make up a large percentage of your Functional Programming experience and so they are worth taking slowly to make sure you get a good, solid understanding.

# 12.6. Functors to the Rescue

We introduced the notion of Contexts earlier and in our recent example, c is in the Context of Maybe:

```
g :: ∀ b c. b -> Maybe c
```

Our conundrum was how to apply h to the output of g. Let’s write a function to help us apply h to a Maybe c.

First, we’ll start with the Type Signature:

```
applyH :: (c -> d) -> Maybe c -> ???
```

What do we put for the final Type of our function? We may lean toward making it d to match what we did when g could not fail. But when we try that, we get stuck:

```
applyH :: (c -> d) -> Maybe c -> d
applyH h Nothing = ???
```

We cannot magically produce a value for the Nothing case. We need to short-circuit the computation and return Nothing. That means our final result must be Maybe d:

```
applyH :: (c -> d) -> Maybe c -> Maybe d
applyH _ Nothing = Nothing
```

Next, we can write the Just case:

```
applyH :: (c -> d) -> Maybe c -> Maybe d
applyH _ Nothing = Nothing
applyH h (Just x) = ???
```

We could replace the ??? with 2 possible values. First is Nothing, but then our function wouldn’t provide the promised functionality of applying h to the value in the Maybe Context. It simply would always throw away all data and always return Nothing. We might as well just replace h with const Nothing.

So, there’s only one reasonable implementation:

```
applyH :: (c -> d) -> Maybe c -> Maybe d
applyH _ Nothing = Nothing
applyH h (Just x) = Just $ h x
```

This is great. So now we can rewrite our Function Application example from the previous section:

```
fgh :: ∀ a d. a -> Maybe d
fgh x = applyH h $ g $ f x
```

But what if we wanted g to also return a reason for the failure:

```
g :: ∀ b c. b -> Either String c
```

Now we have to write another function to apply h that works with Either String. Bells should be going off in your head at this point. This is going to be a problem for ALL Higher-kinded Types.

We would like to solve this problem in a more general fashion and, as it turns out, Category Theory gives us just the right solution, the Functor.

Here’s the definition of a Functor in PureScript:

```
class Functor f where ①
  map :: ∀ a b. (a -> b) -> f a -> f b ②

infixl 4 map as <$> ③
```

① When we used NonEmpty, it used f in its Type Signature. That stood for Functor and we use the same variable name here. This is common in PureScript and Haskell. Another use of f as a Type Parameter is for Foldable. But typically when you see f it represents a Functor.

② Notice how f is a Higher-kinded Type here since it takes a Single Type Parameter, which means it has the Kind Type -> Type.

③ Mapping over Functors is so common that there’s an Operator Alias for it. Notice how it mirrors the Function Application Operator, $. Also, realize our applyH is just the map Method for Maybe where f is Maybe.

The map Method allows us to Apply the function a -> b to the a within the Context of f and modify it WITHOUT changing the Context. This is an important point. When we examine the Functor Laws, we’ll see why this is true.

It’s unfortunate that the function is called map since this is an overloaded term, e.g. Maps are key/value stores and functions map from the Domain to the Codomain. So while the function is called map, many times we say map over, e.g. we want to map f over the List.

Let’s write the Functor instance for Maybe:

```
```haskell
instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
  map f (Just x) = Just $ f x
```
```

Does that look familiar? `map` is a generalized solution to our specific one that we tried to solve with `applyH`.

Now let’s use this to rewrite our Function Application example:

```
```haskell
fgh :: ∀ a d. a -> Maybe d
fgh x = h <$> g $ f x
```
```

Contrast that with the pure version, i.e. no Higher-kinded Types:

```
```haskell
fgh :: ∀ a d. a -> d
fgh x = h $ g $ f x
```
```

The only difference is that `$` is replaced with `<$>`.

# 12.7. Two Perspectives of `map`

Look carefully at the `map` Type Signature:

```
```haskell
class Functor f where
  map :: ∀ a b. (a -> b) -> f a -> f b
```
```

We can interpret this function as taking a function from `a` to `b` and a value `a` in some Context `f` and returning a `b` in that same Context.

Another way to state this is that the function `a -> b` is *lifted* into the Context and applied. You will hear the term *lift* a lot when talking about Functors.

Now, let’s take that same Type Signature and add the implied Parentheses as we’ve done before:

```
```haskell
class Functor f where
  map :: ∀ a b. (a -> b) -> (f a -> f b)
```
```

Now, how might we interpret this?

We can say that `map` *lifts* the function into the Functor, i.e. we take a function that operates on Simple Types (also referred to as Pure Values) and lifts it to work on Functor Types.
