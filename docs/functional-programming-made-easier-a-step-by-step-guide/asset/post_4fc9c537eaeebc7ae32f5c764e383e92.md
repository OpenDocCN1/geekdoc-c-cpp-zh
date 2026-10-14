
![](img/8c0e9b687c62642e828ccb5481e11313_942_0.png)

If you remember, we saw this same issue when we were coding ReaderT. We’ve used <#>, which is map, which requires at least a Functor. So we need to add a Functor Constraint for m:

```
instance functorStateT :: Functor m => Functor (StateT s m) where
  map f (StateT mg) =
    StateT \s -> mg s <#> \(Tuple x s') -> Tuple (f x) s'
```

Notice that we only constrain m as much as we need for the instance code to compile. We could just make it a Monad and it would still work. But, the limited approach is better since it tells us what is required by the instance implementation and in our case, we’ve only used map and so a Functor Constraint is sufficient.

Next thing to code is the Apply Instance. Go as far as you can before reading more.

We’ll start with the instance definition:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
```

We’ve proactively added the same Functor Constraint that we have in our Functor Instance since it’s our Superclass.

And now we’ll code the left-hand side of the equal sign:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = ???
```

We have named fmf and fmx as such to remind us that we are dealing with Functions that return a Function in a Monad and a Value in a Monad, respectively.

Now we can add our common pattern to create a StateT:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> ???
```

And this is usually where we have to stop and think.

Since the Types here are more complex than for `map`, let’s write the specialized Type Signature for `apply`. Go ahead and write out the Type Signature specialized for `StateT` before reading on.

Here’s the Type Signature specialized for `StateT`:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply :: ∀ a b. StateT s m (a -> b) -> StateT s m a -> StateT s m b
  apply (StateT fmf) (StateT fmx) = StateT \s -> ???
```

Now, write out the Types for `fmf` and `fmx` before reading on.

Here are the Types:

```
fmf :: s -> m (Tuple (a -> b) s)
fmx :: s -> m (Tuple a s)
```

❶ Don’t forget that `fmf`, once called, will return a Function, albeit inside of a `Tuple` that’s inside of a `Monad`.

In `apply`, we always work with the lefthand Parameter first, i.e. `fmf` and then work with the right-hand side next.

Keeping that in mind along with all the Types, go ahead and see if you can finish this before reading the solution.

The next step is to call `fmf` and destructure the `Tuple` to get at the mapping Function:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s -> fmf s ???
```

And now we’ll need to `map` to a `Lambda` like we did in our `map` implementation:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
  apply (StateT fmf) (StateT fmx) = StateT \s ->
    fmf s <#> \(Tuple f s') -> ???
```

And now we do the same thing for `fmx`:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
    apply (StateT fmf) (StateT fmx) = StateT \s ->
        fmf s <#> \(Tuple f s') -> fmx s <#> \(Tuple x s'') -> ???
```

And finally, we can put everything back together:

```
instance applyStateT :: Functor m => Apply (StateT s m) where
    -- COMPILER ERROR!!
    apply (StateT fmf) (StateT fmx) = StateT \s ->
        fmf s <#> \(Tuple f s') -> fmx s <#> \(Tuple x s'') -> Tuple (f x) s''
```

Here’s the error the compiler’s giving us:

![](img/8c0e9b687c62642e828ccb5481e11313_944_0.png)

Can you see what’s wrong?

If not, then look closely at the part that’s underlined. The compiler is seeing an m3, or what we called m, and it wants a Tuple t1.

Does that help?

I’m not sure about you, but it’s not totally clear to me. Sometimes when this happens, I read a bit further into the error message:

```
while trying to match type m3 (Tuple b4 s5)
    with type Tuple t1 s5
```

This is a little more helpful. The underlined part’s Type is supposed to be m (Tuple b s). It’s a b and not an a here because we’ve applied f to x. So, the compiler’s Type m3 (Tuple b4 s5) seems to correspond to the Type the underlined part is supposed to be.

So, we can conclude that the Type the compiler found is Tuple t1 s5 instead. But where?

It certainly isn’t the code that’s underlined. We know that’s got to be a Monad since we’re mapping.

This error message isn’t helpful. At this point, there’s a few options we have at our disposal.

We can write out the Types of our code by hand. And this will work as we’ve seen so many times in the past.

Or we can let the compiler help us with those Types.

Since we’ve written out Types by hand before, I’m going to show you a technique using Type Holes that I use from time to time when I’m too lazy to figure out complex Types in my head.

### 21.2. Type Holes and Undefined

Type Holes are a great tool for determining Types when you cannot figure out a Type or they are overly complex.

The problem with Type Holes is that your code must compile before the compiler will evaluate the Type Holes. This is unfortunate, since many times we’re trying to code something and the compiler is complaining that our Types don’t match, which is the very time we will need Type Holes to work.

So, we have a chicken and egg problem. We cannot get our code to compile because the Types don’t match and we cannot figure out the Types using Type Holes since our code doesn’t compile.

What we need is a way to easily get our code to compile so we can get Type help using Type Holes. But how?

We’d like to be able to type something like:

```
myFunctionThatWontCompile = someMagicalThingThatWillCompile
```

We need something that will compile no matter where we put it. And that thing is called undefined. It’s in a library called purescript-undefined and here’s its Type Signature:

```
undefined :: ∀ a. a
```

This function will produce an a out of thin air. Actually, it doesn’t. It can’t. No function can. But this is its Type Definition.

At this point, you’re probably wondering how you can write such a Function in PureScript. The answer is you cannot.

And now, your next question is probably how did the library authors write this then. And the answer is that they wrote it in Javascript.

We haven’t delved into how to write Javascript code that can be called from PureScript just yet, we’ll do that in the Beyond Section of the book, but it is possible.

Here’s the PureScript code:

```
module Undefined where

foreign import undefined :: forall anything. anything
```

Now, I know I said you cannot write this in PureScript and yet here it is written in PureScript. But it’s using a foreign import which means that it expects to get this definition from Javascript. That’s what foreign means in PureScript (much more in the Beyond Section of this book).

And for the impatient, here’s the Javascript code it uses:

```
"use strict";

exports.undefined = undefined
```

undefined will almost always crash your program, but that’s okay. We’re not going to run our program with undefined in it, unless we forget to remove it.

We only want it to make the compiler happy. Since it returns an a (or anything), it will unify with ANY Type the compiler is looking for. This breaks the chicken and egg cycle and allows the compiler to evaluate our Type Holes.

To use undefined, we’ll need to edit our spago.dhall file:

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "arrays"
  , "bifunctors"
  , "console"
  , "contravariant"
  , "control"
  , "effect"
  , "either"
  , "foldable-traversable"
  , "integers"
  , "lists"
  , "maybe"
  , "newtype"
  , "nonempty"
  , "prelude"
  , "profunctor"
  , "psci-support"
  , "strings"
  , "tuples"
  , "undefined" ①
  , "unfoldable"
  , "unicode"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① Added undefined. I added it here because I like to keep my libraries in alpha order.

Then comment out the apply code TEMPORARILY so that our code will build with NO errors, save your file and then run:

```
npx spago build
```

This will install and build the new library and your program. We commented out the bad code so we wouldn’t get any errors.

We’ll ignore this warning for obvious reasons:
