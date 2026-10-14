
Since the compiler knows how to call `Just` and `Nothing`, when you pass them, they will always pass the current way to call them and since you're using `Just` and `Nothing`, that code will never be dead code eliminated.

This rule holds for all PureScript Functions including your own.

## 26.2. FFIs and Effect

For Javascript Functions that perform real-world Effects, we need to make sure we create the Javascript code properly.

Another very important thing to keep in mind is that it's not always obvious when a Javascript Function is performing real-world Effects. Sometimes you have to really investigate.

For example, here's the Node API definition for `resolve`:

```
path.resolve([...paths])
Added in: v0.3.4

- ...paths <string> A sequence of paths or path segments
- Returns: <string>

The path.resolve() method resolves a sequence of paths or path segments into an absolute path.

The given sequence of paths is processed from right to left, with each subsequent path prepended until an absolute path is constructed. For instance, given the sequence of path segments: /foo, /bar, baz, calling path.resolve('/foo', '/bar', 'baz') would return /bar/baz because 'baz' is not an absolute path but '/bar' + '/' + 'baz' is.

If, after processing all given path segments, an absolute path has not yet been generated, the current working directory is used.

The resulting path is normalized and trailing slashes are removed unless the path is resolved to the root directory.

Zero-length path segments are ignored.

If no path segments are passed, path.resolve() will return the absolute path of the current working directory.
```

Reading through this, it's not clear whether this Function is doing any real-world Effects. But the following worries me:

```
The path.resolve() method resolves a sequence of paths or path segments into an absolute path.
```

How does it figure out an absolute path from a relative one without consulting the Operating System for the Current Directory. If it does, then that would warrant an Effect in PureScript. Or I may just be interpreting this wrong.

My gut is telling me that this probably is going to need to run in Effect, but the following bit of documentation slightly further down the page from the previous seals the deal:

```
If, after processing all given path segments, an absolute path has not yet been generated, the current working directory is used.
```

That's all we need to know. It has to call the Operating System to find out what the "current working directory" is and therefore is NOT Pure.

Here's how we'd write the Javascript code so this can run in Effect:

```
const path = require('path');

exports.resolveImpl = (paths, path_) => {
  return () => path.resolve.apply(this, paths.concat(path_)); ① ②
};
```

① Effects return Javascript FUNCTIONS not results.

② Concatenate the paths together to conform to resolve's terrible interface.

There's a lot to unpack here. The first thing to note is that resolve takes any number of arguments:

```
path.resolve([...paths])
```

We can't do this in PureScript. Good thing too. This is such a terrible interface to understand because of this. It turns out that the paths are processed from RIGHT to LEFT.

This means that the LAST path will be the path that you're trying to resolve using the leftmost paths. That's why this Function takes 2 Parameters, paths and path.

Here's the corresponding PureScript code:

```
foreign import resolveImpl
  :: Fn2 (Array FilePath) FilePath (Effect FilePath) ①

resolve:: Array FilePath -> FilePath -> Effect FilePath ①
resolve paths path = runFn2 resolveImpl paths path
```

① Remember that this runs in the Effect Monad.

And then some test code to use this:

```
test :: Effect Unit
test = do
  path <- resolve [ "/foo", "/bar" ] "baz" ① ②
  log path
```

① Remember, resolve runs in Effect so we need to extract the result from the Monad.

② This is the example given in the Node API documentation for resolve. This way we'll know for sure that our code is working.

When we run this we get:

```
/bar/baz
```

This is exactly what the Node API documentation example says that we should get back from this call.

Let's return to something I glossed over, but is an important thing to understand.

Code that runs in Effect returns Javascript Functions:

```
const path = require('path');

exports.resolveImpl = (paths, path_) => {
  return () => path.resolve.apply(this, paths.concat(path_)); ①
};
```

① Returning a Function since resolveImpl runs in Effect.

Do remember writing runReaderT and runWriterT, etc. for their respective Monads?

Well, there is no run Function for Effect. It's run by the compiler generated code. And now we can see that main returns a Javascript Function since its Type is Effect Unit.

We can think of Effect as a set of instructions of what should be run at some point after our program runs. When our programs run, it calls our main, which does not execute our program, but, instead, purely generates an extremely complex set of instructions to be run later in the form of a single, massive, Javascript Function.

This is how we can stay in the Pure Functional world while still effecting the outside world. We create code in the Pure world that generates instructions to be run later in the Impure world.

## 26.3. FFIs and Aff

There are 2 ways to call a Javascript Function Asynchronously. The hard way and the easy way.

Let's start with the easy way. Here's how we can call our resolve Javascript Function Asynchronously:

```
import Effect.Aff (Aff, launchAff_, makeAff, nonCanceler)
import Effect.Class (liftEffect)
import Effect.Class.Console (log)

test :: Effect Unit
test = launchAff_ do
  aPath <- liftEffect $ resolve [ "/foo", "/bar" ] "baz"
  log aPath
```

① We're running in Aff thanks to launchAff_

② We convert resolve from an Effect to an Aff via liftEffect since we're running in Aff.

This case was really easy. But what if our Javascript Function takes a long time to complete and, therefore, has a Callback because we cannot afford to block the current thread.

This was not the case with resolve since it's a very fast Function even if it calls the Operating System for the current working directory.

But, readTextFile from Node's fs module is not fast. It could take a very long time, in computer time, to read a file. So, it needs a Callback.

But we don't want a Callback like we have in Node.FS.Async and we'd like to run it in Aff not Effect.

While this is the hard way, relatively speaking, we can do all of this nicely with a neat little Function from Effect.Aff.Compat called fromEffectFnAff.

Here's how we'd write our Javascript code:

```
exports._readTextFile = path => (onError, onSuccess) => {
  fs.readFile(path, { encoding: 'UTF-8' }, (err, data) =>
    err ? onError(err) : onSuccess(data));
  return (cancelError, onCancelerError, onCancelerSuccess) =>
    onCancelerSuccess();
};
```

There's a lot of code to look at here. So let's dissect it one piece at a time.

```
exports._readTextFile = path => (onError, onSuccess) =>
```

First, _readTextFile is an alternative naming convention for Javascript Functions similar to readTextFileImpl. I think I like this convention better.

Second, _readTextFile takes a path to read. It returns a Function that expects 2 Parameters, which are both Callback Functions.

onError is to be called when an error occurs in the Asynchronous operation. It will be called with the Javascript Error, which has an equivalent Type in Effect.Exception.

onSuccess is to be called passing the result when it succeeds.

We can see this in the next line of code:

```
fs.readFile(path, { encoding: 'UTF-8' }, (err, data) =>
  err ? onError(err) : onSuccess(data));
```

On this line, we call Node's readFile with the path and an Encoding of UTF-8. The final Parameter is the Callback.

The Callback takes 2 Parameters. If the first Parameter isn't undefined or null, then an error occurred and onError is called with that error.

If the first Parameter doesn't have a value, then the second Parameter will have the file data in it and onSuccess is called passing the file data.

Here's the final line of code:

```
return (cancelError, onCancelError, onCancelSuccess) =>
  onCancelSuccess();
```

_readTextFile returns a Canceler Function. This Function will be called by the Fiber Manager if we've been canceled.

The first Parameter to this Function, cancelError, is the Error passed in from whatever canceled us. In an earlier Chapter, we called killFiber to cancel:

```
kill :: ∀ a. Fiber a -> Aff Unit
kill = killFiber (error "Killing you softly...") ①
```

① killFiber takes an Error. This will be passed to the Canceler.
