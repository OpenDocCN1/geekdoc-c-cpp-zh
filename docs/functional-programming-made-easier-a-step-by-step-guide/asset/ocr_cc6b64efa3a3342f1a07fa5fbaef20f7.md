# # Chapter 5. Basic Coding in PureScript

Reading a book can lull us into the false sense that we understand what we’ve read. This happens to me, especially in programming. We understand it as it’s being explained, but we haven’t fully understood it until we’ve utilized it.

So that’s what the exercises are for. And if you’re like me and tend to skip exercises in books, please do not. There’s more to these exercises than meets the eye.

Many concepts will get introduced in the exercises. Many commonly used library Functions will also be introduced during this process. You will also learn how to program, and more important, think in a Functional way using PureScript.

# ## 5.1. Prelude

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