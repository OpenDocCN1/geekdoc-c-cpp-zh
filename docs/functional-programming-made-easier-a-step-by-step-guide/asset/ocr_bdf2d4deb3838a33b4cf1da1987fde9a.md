```
const isEven = n => n % 2 === 0;
const upperLower = n => {
  if (isEven(n)) return String.prototype.toUpperCase;
  else return String.prototype.toLowerCase;
};

console.log(upperLower(0).apply("this should be output in uppercase"));
console.log(upperLower(1).apply("THIS SHOULD BE OUTPUT IN LOWERCASE"));
```

① If n is even then we return a Function to convert strings to uppercase. Otherwise, we return a Function to convert strings to lowercase.

Let’s see how we’d write this in PureScript:

```
module Main where

import Prelude

import Data.String.Common (toLower, toUpper)
import Effect (Effect)
import Effect.Console (log)

isEven :: Int -> Boolean
isEven n = n `mod` 2 == 0

upperLower :: Int -> (String -> String)
upperLower n = if isEven n then toUpper else toLower

main :: Effect Unit
main = do
  log $ upperLower 0 "this should be output in uppercase"
  log $ upperLower 1 "THIS SHOULD BE OUTPUT IN LOWERCASE"
```

Once again, the PureScript example will not completely make sense to you yet but we’re only concerned with how it contrasts with Javascript.

It’s also possible that you are not familiar with Javascript either and in that case, the best you can hope to discern from these two examples is that the syntax in PureScript is far less dense than in Javascript.

You may also notice that there’s a lot more overhead in PureScript because we have to import libraries. In this particular example, Javascript has all of the Functions we need already built-in. This is not always the case.

If you’ve spent any time working with Javascript, you’re well aware of how complicated adding libraries