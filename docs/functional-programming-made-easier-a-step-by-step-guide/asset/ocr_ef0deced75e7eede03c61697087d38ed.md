② Removed Ordering(..) and compare.

# 7.20. Creating Our Own Typeclass

Let’s imagine that we have some things we’d like to encode as CSV (Comma-Separated Values).

A very efficient way to do this is to create a Typeclass. Let’s call it ToCSV with a single Method called toCSV.

First though, let’s make a new file called Ch7b.purs under the src directory with the following:

```
module Ch7b where

import Prelude

import Effect (Effect)
import Effect.Console (log)

test :: Effect Unit
test = do
  log "placeholder" ①
```

① We’re going to delete this line shortly. It’s only here to keep the compiler happy for now.

And change Main.purs to be:

```
module Main where

import Prelude
import Effect (Effect)

import Ch7b as Ch7b ①

main :: Effect Unit
main = Ch7b.test ②
```

① Change import from a to b.

② Call b’s test function.

Now, go ahead and write the Typeclass for ToCSV before moving on. If you get stuck, check out the Hint section.