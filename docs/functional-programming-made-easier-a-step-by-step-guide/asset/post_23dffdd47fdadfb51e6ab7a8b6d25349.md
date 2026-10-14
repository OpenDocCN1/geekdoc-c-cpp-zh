
That should inform us on how to write this. So give it a try.

### 5.5.2. Code for const

```purescript
const :: ∀ a b. a -> b -> a
const x _ = x
```

- 1. We don’t care about the second Parameter, hence the `_`, and we just return the first Parameter.

If it’s not obvious how this is useful, maybe a simple example will help:

```purescript
filter (\n -> n > 2) [1, 2, 3]  -- [3]
filter (const true) [1, 2, 3]  -- [1, 2, 3]
```

- 1. The Predicate to filter, which is a Lambda Function, takes a single Parameter that is `n` and returns a Boolean, which tells `filter` whether to keep the element in the resulting Array.
- 2. Here `const true` is the Predicate, which when passed an element from the Array will ignore it (since it’s the second Parameter to `const`) and just return `true` (the first Parameter to `const`).

Notice how `const true` is a Partial Application of the `const` Function, i.e. we haven’t quite given it all of its Parameters. By partially applying, we are effectively "baking" in the constant value that we want this Function to return. Remember that `const` will ignore its second Parameter and always return its first.

> Think of `const` as a Constant Function not a constant value. `const true` is a Constant Function whereas `true` is a Constant Value.

Your module should now look like this:

```purescript
module Ch5 where

import Prelude (Unit, show)

import Effect (Effect)
import Effect.Console (log)

flip :: ∀ a b c. (a -> b -> c) -> b -> a -> c
flip f x y = f y x

const :: ∀ a b. a -> b -> a
const x _ = x

test :: Effect Unit
test = do
  log (show (flip const 1 2))
```

And when run should still print 2, assuming we wrote `const` correctly since now our test code is using our `const` and not Prelude’s.

## 5.6. The Apply Operator (`$`)

There’s a really helpful Operator that is often used in idiomatic PureScript, `$`. While this Operator is very easy to implement (we’ll do so shortly), it’s very powerful in reducing coding noise by eliminating Parentheses.

Let’s look at our test Function:

```purescript
test :: Effect Unit
test = do
  log (show (flip const 1 2)) ①
```

① It would be nice to reduce these Parentheses.

With the Apply Operator we can remove all Parentheses from that line of code:

```purescript
test :: Effect Unit
test = do
  log $ show $ flip const 1 2 ①
```

① Equivalent statement to the one with Parentheses.

We can think of `$` as adding a Begin Parenthesis at the point where the `$` is and an End Parenthesis at the end of the line.

For now, let’s write the Function:

```purescript
apply :: ∀ a b. (a -> b) -> a -> b
apply f x = f x
```

Well, that was pretty trivial.

Next, try to write the Operator.

### 5.7.1. Hint for (`$`)

Most likely, when you read the last sentence of the previous section, you were stumped. I know I would be. Even though we’ve talked about operators and we’ve looked at how they were defined, we’ve never **created** our own operators.

This is why doing exercises is so important. It forces you to really understand things.

So here’s a quick refresher on how to create an Operator:

- 1. Decide what the associativity is going to be for your infix Operator and use one of the following accordingly:
  - 1. `infixl` (Left-Associative).
  - 2. `infixr` (Right-Associative).
  - 3. `infix` (Non-Associative).
- 2. Decide the precedence (Higher gets done first).

Here’s an example of a fictitious Operator `!!!` that’s Right-Associative and has a Precedence of `3`:

```purescript
infixr 3 notReal as !!!
```

Now see if you can write the Operator for `apply` that’s Right-Associative with Precedence 0. (These choices will become apparent soon enough.)

### 5.7.2. Code for (`$`)

Here is the code for `apply` and its Operator:

```purescript
apply :: ∀ a b. (a -> b) -> a -> b
apply f x = f x

infixr 0 apply as $
```

You may be wondering how we knew what to choose for Associativity and Precedence. For this Operator, it’s a very simple process, which is not true for all Operators.

If we think about the Precedence of Parentheses, it would be 9 because it has the highest Precedence and therefore gets evaluated first.

Let’s return to our code with Parentheses:

```purescript
test :: Effect Unit
test = do
  log (show (flip const 1 2))
```

We are saying that we want everything in the Parentheses to happen first. This implies that we want the result of the Parenthetical to be applied to `log` last.

So if we’re going to represent that application with our new Operator, `$`, we want its Precedence to be last, this way everything to the right of the `$` gets evaluated first as if it were surrounded by Parentheses.

That’s why it has the Precedence of 0 and why we can use it in place of Parentheses.

When considering the Associativity for this Operator, we need to remember how the Operator was defined. We said that it would be the equivalent of adding a Begin Parenthesis where the `$` is specified and an End Parenthesis at the end of the line.

That tells us that repeated use of the Operator on the same line of code should work like its Parenthetical Equivalent, which has Parentheses collecting at the end of the line:

```purescript
log $ show $ flip const 1 2  -- log (show (flip const 1 2))
```

Right-Associativity associates to the right, which means that the Parentheses collect on the Right. And that’s exactly what we have here, which is why we picked `infixr`.

Now change your test code to use `$` and rerun it. It should still print 2.

## 5.8. Writing the Apply Flipped Operator (`#`)

There’s another very helpful Operator in PureScript, `#`. But it’s a little more difficult to understand why, so let’s look at an example:

```purescript
f x =
  step3 (step2 (step1 x))
```

Here we have a Function that performs 3 Functions, `step1`, `step2` and `step3` in that order. But the order in which we write these, from left to right, feels inside-out when compared to the order of execution. The inside Parenthetical gets executed first, then the next Parenthetical and finally `step3` is called with the result.

So let’s rewrite it using our newly minted Operator, `$`:

```purescript
f x =
  step3 $ step2 $ step1 x
```

It’s not inside-out anymore, but since we read code from left to right, it feels backwards. `step1` is called then `step2` then `step3`. Execution is right to left.

Many times, we like to think about things as a sequence of operations. Written out in English, this would be "Take `x` and apply it to `step1` and then take that result and apply it to `step2` and then finally apply that result to `step3`."

It’s just a different way of thinking and it would be nice if we could code that way when it makes the most sense.

Well, we can with the flipped version of the `$` Operator, viz. `#`:

```purescript
f x = x
  # step1
  # step2
  # step3
```

This code reads like our English sentence above does. And since we read code from top to bottom, the steps are in the order they’re applied.

Now, before continuing, write `applyFlipped` and its Operator, `#`.

### 5.8.1. Code for `applyFlipped` and (`#`)

Looking first at the signature:

```purescript
applyFlipped :: ∀ a b. a -> (a -> b) -> b
```

we can see that it lives up to its name. Its Type Signature is just a flipped version of `apply`’s Type Signature, which means we can use `flip` on `apply` to write this Function:

```purescript
applyFlipped :: ∀ a b. a -> (a -> b) -> b
applyFlipped = flip apply
```

If this implementation isn’t clear enough, take a look at the manually written version:

```purescript
applyFlipped :: ∀ a b. a -> (a -> b) -> b
applyFlipped x f = f x
```

Next, we turn our attention to the Operator Precedence and Associativity.

Let’s look back at our example usage of `#`:

```purescript
f x = x
  # step1
  # step2
  # step3
```

Since we want this to apply `x` to `step1` first then `step2`, etc., we should add the Parentheses to reflect that fact:

```purescript
f x = (((x
  # step1)
  # step2)
  # step3)
```

> ① Notice how Parentheses collect on the left.

This informs us that we want to use `infixl` for Left-Associativity.

To determine Precedence, let’s look once again at our example usage of `#`:

```purescript
f x = x
  # step1
  # step2
  # step3
```

> ① Imagine for a minute that our `x` is a more complex computation, e.g. `x + 10`.

If we were to replace `x` with `x + 10`, we’d want that computation to happen **before** we apply it to `step1`:

```purescript
f x = (x + 10)
  # step1
  # step2
  # step3
```
