```
import Prelude (Unit, show, discard, (==), ($)) ①

import Data.Eq (class Eq) ②
import Effect (Effect) ③
import Effect.Console (log) ③
```

① Some things we’ll need from Prelude. Remember, discard is implicitly used in the do syntax (more on this later in the book).

② We need to import the Eq Typeclass. Note the class keyword.

③ These imports are for our debugging code, viz. the test function.

Edit your Main.purs to look like:

```
module Main where

import Prelude
import Effect (Effect)

import Ch7a as Ch7a ①

main :: Effect Unit
main = Ch7a.test ②
```

① Change from Ch5 to Ch7a.

② Change from Ch5.test to Ch7a.test.

Add the following Function to test our code in Ch7a.purs:

```
test :: Effect Unit
test = do
  log $ show $ Just 5 == Just 5 -- COMPILER ERROR!! ①
  log $ show $ Just 5 == Just 2 ②
  log $ show $ Just 5 == Nothing ③
  log $ show $ Nothing == Just 5 ④
  log $ show $ Nothing == (Nothing :: Maybe Unit) ⑤ ⑥
```

① Prints true.

② Prints false.

③ Prints false.

④ Prints false.