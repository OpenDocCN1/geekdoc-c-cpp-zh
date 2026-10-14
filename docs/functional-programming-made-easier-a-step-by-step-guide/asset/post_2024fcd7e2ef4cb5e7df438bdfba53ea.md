
## Chapter 5. Basic Coding in PureScript

Reading a book can lull us into the false sense that we understand what we’ve read. This happens to me, especially in programming. We understand it as it’s being explained, but we haven’t fully understood it until we’ve utilized it.

So that’s what the exercises are for. And if you’re like me and tend to skip exercises in books, please do not. There’s more to these exercises than meets the eye.

Many concepts will get introduced in the exercises. Many commonly used library Functions will also be introduced during this process. You will also learn how to program, and more important, think in a Functional way using PureScript.

### 5.1. Prelude

`Prelude` is library of commonly used Functions that nearly every program will use. Unlike Haskell, you have to explicitly `import` this module into your code:

```
```purescript
import Prelude
```
```

When you import a module like this, *all* exported Functions get imported into your module’s global namespace. This can be problematic if they collide with Functions from other modules.

Let’s assume that we have a module called `AnotherModule` that exports `identity` and `doSomething`. If we import as follows and then try to use `identity`:

```
```purescript
import Prelude
import AnotherModule

id = identity   -- COMPILER ERROR!!
```
```

The compiler will complain that `identity` is ambiguous:

```
module Ch5 where

import Prelude
import AnotherModule

id = identity
    identity :: Int

    Conflicting definitions are in scope for value identity from the following modules:

    AnotherModule
    Prelude
    PureScript(ScopeConflict)

Peek Problem  No quick fixes available
```

We can fix this by *selectively importing*:

```
import Prelude
import AnotherModule (doSomething) ①

id = identity
```

① Import AnotherModule but ONLY include doSomething.

Or we can decide to use identity from AnotherModule but we want everything else from Prelude:

```
import Prelude hiding (identity) ①
import AnotherModule (identity, doSomething) ②

id = identity
```

① Import Prelude while *hiding* identity, i.e. do not import it.

② Explicitly specify the import of identity and doSomething from AnotherModule.

> It is considered good practice to *explicitly* specify all Functions that are imported from modules. In small programs, you can get away with not doing this, but as your codebase grows, it becomes increasingly difficult to determine where Functions have been imported from. The only exception to this rule is Prelude.

But what if we want to use Prelude’s identity sometimes and AnotherModule’s other times?

```
module Ch5 where ①

import Prelude (Unit) ②

import Effect (Effect) ③
import Effect.Console (log)

test :: Effect Unit ③
test = do ③
  log "test" ④
```

① We define and name our module.

② We are only importing the Unit Type because we're going to be writing our own versions of many of the Prelude Functions here and we don't want name collisions.

③ Don't worry about these lines. We will eventually get to them when we talk about Effects.

④ This logs the String test to the console. We'll delete this later.

Now to run this program in Node, we can open the Terminal in VSCode by typing Ctrl+` and then typing:

```
npx spago run
```

Our program should print out the String test.

We are now ready to start coding.

### 5.3. Pursuit

Since we are going to writing a lot of Functions that already exist in the Prelude library, we should get used to looking up Function definitions.

There is a website for doing this called Pursuit. It can be found on the web at https://pursuit.purescript.org/. When you're there, you can search for Functions using the Search field.

Before you code any of the Functions in the Chapter, please first consult Pursuit to find its Type Signature and what it's supposed to do.

Let's look for flip by typing the name of the Function and hitting Enter:

![](img/8c0e9b687c62642e828ccb5481e11313_146_0.png)

You should see the following definition:

## Search results

### `flip`

```
```purescript
flip :: forall a b c. (a -> b -> c) -> b -> a -> c
```
```

Flips the order of the arguments to a function of two arguments.

```
```purescript
flip const 1 2 = const 2 1 = 2
```
```

This Function’s Type Signature is:

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
```
```

I’ve used `∀` instead of `forall` as shown in `Pursuit`.

We want to understand what this Function does and sometimes we’ll get a nice example (other times not):

```
```purescript
flip const 1 2 = const 2 1 = 2
```
```

Unfortunately, we don’t know what `const` does just yet so this is marginally helpful. It says that calling `flip` on the Function `const` (whatever that does) with Parameters `1` and `2` is the same as calling `const` with those Parameters reversed. It also shows the result of the `const` call being `2`.

Another thing to notice is both the package and module where `flip` can be found. The package is `purescript-prelude` and the module is `Data.Function`.

### 5.4. Writing `flip`

Sometimes a Function’s Parameters are in the wrong order for how we’d like to use them. This is where `flip` comes in. Try to code `flip` in the `Ch5` module and then write the following line into your `test` Function:

```
```purescript
log (show (flip const 1 2))
```
```

Also. delete the line:

```
log "test"
```

Your module should look like:

```
module Ch5 where

import Prelude (Unit, show, const) ① ②

import Effect (Effect)
import Effect.Console (log)

test :: Effect Unit
test = do
  log (show (flip const 1 2)) ③
```

① We need the show Function from Prelude to turn the Int we’ll ultimately get from the flip const call into a String that we can pass to log.

② We also need const for now. Ultimately, we’ll write this Function and so we’ll need to remove this once we get there.

③ Here’s our test code.

Now all you have to do is write the flip Function. Please try to do so without looking ahead. Once you’re done or if you get stuck continue on.

#### 5.4.1. Hint for flip

Let’s take a look at the details of the Type Signature for flip:

```
flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
```

It tells us that flip takes a Function of 2 Parameters (a and b returning c), a Parameter of Type b, Parameter of Type a and returns a value of Type c.

Our first step is to name these Parameters:

```
flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
flip f x y = ???
```

See if that helps you write the Function now.

#### 5.4.2. Code for `flip`

Here’s the code for `flip`:

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
flip f x y = f y x
```
```

❶ We call f with the original Parameter order flipped.

We can test this by running our program:

```
```bash
npx spago run
```
```

It should print out 2.

#### 5.4.3. Alternative Coding for `flip`

What would have happened if `flip`’s Type Signature had the redundant Parentheses added:

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> (b -> a -> c)
```
```

Now it takes a single Function and returns a Function. Since Type Signatures are Right-Associative, these Parentheses are implied, but seeing them changes how we think about the Function.

How might you have written it differently if you saw this version of the Type Signature?

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> (b -> a -> c)
flip f = \x y -> f y x
```
```

❶ We return a Lambda Function.

Remember, when we talked about Lambda Functions, we talked about moving Parameters across the equals sign? Well, here’s a case where we’ve done exactly that.

By the way, it turns out that our first version of `flip` is idiomatic PureScript. But it’s good to see other ways of writing and thinking about `flip`.

Just for fun, here’s another way that’s also valid:

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> b -> (a -> c)
flip f x = \y -> f y x
```
```

❶ The redundant Parentheses are specified differently here.

❷ Takes a Function and a Parameter of Type b and returns a Function of 1 Parameter.

By the way, all 3 versions are equivalent:

```
```purescript
flip f = \\ x y -> f y x
flip f x = \\y -> f y x
flip f x y = f y x
```
```

As are the Type Signatures:

```
```purescript
flip :: ∀ a b c. (a -> b -> c) -> (b -> a -> c)
flip :: ∀ a b c. (a -> b -> c) -> b -> (a -> c)
flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
```

If this is still confusing, go back and read the section on Lambda Functions.

### 5.5. Writing const

Before reading on, look up `const` on Pursuit and see if you can figure out what it does and how it might be used.

`const` is used when you’re calling a Function that needs a Function to perform an operation but that operation never varies. Instead, it’s always returns a **constant** value.

Before you write `const`, remember to remove it from the `Prelude` import:

```
```purescript
import Prelude (Unit, show) ❶
```
```

❶ Remove const from the list of Functions imported from Prelude since we’re writing our own.

So now, you’re ready to write `const`.

#### 5.5.1. Hint for const

Look at `const`’s Type Signature:

```
```purescript
const :: ∀ a b. a -> b -> a
```
```

We can see that the first Parameter, a, is returned and the second Parameter b is ignored.
