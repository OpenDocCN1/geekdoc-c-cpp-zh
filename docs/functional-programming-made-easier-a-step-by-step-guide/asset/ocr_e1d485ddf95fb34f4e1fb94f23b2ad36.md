# Chapter 25. Coding With Ajax and JSON

Return to the project that you’ve been coding in and create a file called Ch25a.purs and add the following:

```
module Ch25a where

import Prelude ①

import Effect (Effect)
import Effect.Class.Console (log) ②

test :: Effect Unit
test = do
  log "placeholder" ③
```

① Once again we are not writing anything from Prelude so we’ll just import all of it.

② We’re now using this version of log so we can use it in Effect and Aff.

③ We’ll delete this soon enough. It’s just here to keep the compiler happy.

Next, change your Main module to import Ch25a and call its test Function:

```
module Main where

import Prelude
import Effect (Effect)

import Ch25a as Ch25a

main :: Effect Unit
main = Ch25a.test
```

If you run:

```
npx spago run
```

you should see it build and print:

```
[info] Build succeeded.
placeholder
```