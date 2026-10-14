```
```purescript
main :: Effect Unit
main = do
  shutdown <- HTTPure.serve port router
  $ log $ "Server up running on port: " <> show port
  pure unit
```
```

This should run so give it a try. Once it runs, you will have to kill the server with `Ctrl-C`.

Next, we can write the `Handler` for `SIGINT`. This is the signal that the OS sends to your program when you type `Ctrl-C`. But, how do we figure out how to do this?

Well, the first place I’d look is to see how `Node` handles SIGINT. To do that, we can use Google. Go ahead and search Google and see what you find.

I searched Google for the term `node SIGINT` and found:

![](bbox=[0.146, 0.391, 0.855, 0.513])

When I click on that I get a big list of API Functions. So I search the page, via `Cmd-F` or `Ctrl-F` on Windows, for `SIGINT` and I find the example code:

```
```javascript
// Begin reading from stdin so the process does not exit.
process.stdin.resume();

process.on('SIGINT', () => {
  console.log('Received SIGINT. Press Control-D to exit.');
});

// Using a single function to handle multiple signals
function handle(signal) {
  console.log(`Received ${signal}`);
}

process.on('SIGINT', handle);
process.on('SIGTERM', handle);
```
```

Unfortunately, this `on` function isn’t something that I’d expect to be duplicated in PureScript. But just for fun, I’ll check `Pursuit` for `on`.