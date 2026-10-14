# 22.2. Working with the Aff Monad

While Effect is the Monad that our program ultimately runs in, there’s another more powerful effects Monad called Aff, which is a Monad for Asynchronous Effects.

To get any real work done, we’re going to rely heavily on Aff. If we want to run HTTP requests while handling user input from the Browser, we’re going to use Aff.

On the backend, if we’re running in Node, we’re going to want to handle multiple requests at a time, which means we’re going to run our request handlers in Aff.

Learning how to work within Aff and its ancillary services is imperative to building an application of any level of complexity.

So let’s start that process by looking at how we can read a File in an Asynchronous way:

```
import Prelude

import Effect (Effect)
import Effect.Aff (Aff, launchAff_)
import Effect.Class.Console (log) ①
import Node.Encoding (Encoding(..))
import Node.FS.Aff (readTextFile) ②

readAFile :: Aff Unit ③
readAFile = do
  text <- readTextFile ASCII "test.txt"
  log text

test :: Effect Unit
test = launchAff_ readAFile ④
```

① We’re importing a different version of log here. This version will work in Effect and any Monad that has a MonadEffect Instance. It turns out that Aff has such an instance meaning we can also call log in Aff.

② We need to add node-fs-aff to our spago.dhall file to import this module.

③ We are running in the Aff Monad.

④ launchAff_ is one of many ways of running Asynchronous processes, in this case, readAFile.

This code uses a different Node library that allows us to easily work with files in the Aff Monad without having to deal with Callback, which makes our coding much easier.

But, this particular library will throw exceptions and crash your program if it receives an error. In the above code, if test.txt doesn’t exist, this will crash.