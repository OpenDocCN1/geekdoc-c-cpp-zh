```
function (error) {
});
```

I don't know about you, but I really get lost in all the )'s and )'s (unless I try hard to remember my LISP class in college), and it's hard to see which error function applies to which async call. And just imagine throwing a few progress handlers in as well!

Chaining promises solves all of this with the small tradeoff of needing to declare a few extra temp variables outside the chain for any variables that need to be shared amongst the various completed handlers. Each completed handler in the chain again returns the promise for the next operation, and each link is a call to then except for a final call to done to terminate the chain. This allows you to indent all the async calls only once, and it has the effect of propagating errors down the chain, as any intermediate promise that's in the error state will be passed through to the end of the chain very quickly. This allows you to have only a single error handler at the end:

```
captureUI.captureFileAsync(Windows.Media.Capture.CameraCaptureUIMode.photo)
.then(function (capturedFileTemp) {
    //...
    return local.createFolderAsync("HereMyAm", ...);
})
.then(function (myFolder) {
    //...
    return capturedFile.copyAsync(myFolder, newName);
})
.done(function (newFile) {
},
    function (error) {
})
```

To my eyes (and my aging brain), this is a much cleaner code structure—and it's therefore easier to debug and maintain. If you like, you can even end the chain with done(null, errorHandler), as we did in Chapter 2:

```
captureUI.captureFileAsync(Windows.Media.Capture.CameraCaptureUIMode.photo)
//...
.then(function (newFile) {
})
.done(null, function (error) {
})
```

Remember, though, that if you need to pass a promise for the whole chain elsewhere, as to a setPromise method, you'll use then throughout.

# Error Handling in Promise Chains: then vs. done

This brings us to why we have both then and done and to why done is used at the end of a chain as well as for single async operations. To begin with, then returns another promise, thereby allowing chaining, whereas done returns undefined, so it always occurs at the end of a chain. Second, if an exception occurs within one async operation's then method and there's no error handler at that level,