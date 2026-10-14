We can conceptualize main as if it returns the Effect Monad to the PureScript runtime code, which will then execute it.

This is how we can code in Pure Functions and still affect the outside world. We’re never calling random in our code. We only build a Monad, i.e. Effect, that will process the result of such a call:

```
main :: Effect Unit
main = do
  n <- random
  log $ show n
```

Here random isn’t a Function. It’s a Monad, or more precisely, it’s an Effect Number, i.e. a Monadic Value that will bind to n in main:

```
main :: Effect Unit
main = random >>= \n -> log $ show n
```

The bind for Effect is not coded in PureScript. It’s code that the compiler will generate, i.e. imperative non-Pure code. But at that point it’s out of our hands.

We did our jobs as PureScript programmers, i.e. to combine Monads, and, therefore, Functions, to build a program that WHEN run will process the data given to it. We did this with Pure Functional code.

main is like any other Monad, a complex combination of Functions to be run at a later time. That later time is when we execute the Javascript code that the compiler generated.

Like random, all Browser APIs run in the Effect Monad, e.g. to get the Browser Window:

```
import Web.HTML (window)

window :: Effect Window
```

And to get the current Browser location:

```
import Web.HTML.Window (location)

location :: Window -> Effect Location
```

And to get the href from that location as a String: