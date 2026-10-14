# # Chapter 15. Coding More Functors

As always, it’s good to take the time to code the things we’ve just learned for ourselves. It’s easy to fool ourselves that we understand something when we first learn it. But trying to implement what we’ve just learned is a great way to both let us know at what level we actually did learn it and to help deepen that understanding.

Return to the project that you’ve been coding in and create a file called `Ch15.purs` and add the following:

```
```purescript
module Ch15 where

import Prelude ❶

import Effect (Effect)
import Effect.Console (log)

test :: Effect Unit
test = do
  log "placeholder" ❷
```
```

❶ We’re not rewriting anything from Prelude in this Chapter, so we can just import everything from Prelude.

❷ We’ll delete this soon enough. It’s just here to keep the compiler happy.

Next, change your `Main` module to import `Ch15` and call its `test` function:

```
```purescript
module Main where

import Prelude
import Effect (Effect)

import Ch15 as Ch15

main :: Effect Unit
main = Ch15.test
```
```

If you run:

```
```shell
npx spago run
```
```

you should see it build and print: