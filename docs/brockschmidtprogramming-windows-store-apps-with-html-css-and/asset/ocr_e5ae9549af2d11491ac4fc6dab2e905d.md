![](bbox=[0.13, 0.07, 0.93, 0.24])

Again, when a promise already knows its results, it can synchronously pass them to whatever completed handler it received through `then`. Here a promise is nothing more than an extra layer that delivers results through a callback rather than directly from a function. For pre-existing results, in other words, a promise is pure overhead. You can see this by placing another `console.log` call after `promise.then`, and you'll see that the `{}` result is logged before `promise.then` returns.

All this is implemented in scenario 1 of the Promises example.

# # Example #2: An Empty Async Promise

While using promises with known values seems like a way to waste memory and CPU cycles for the sheer joy of it, promises become much more interesting when those values are obtained asynchronously.

Let's change the earlier `EmptyPromise` class to do this. Instead of calling the completed handler right away, we'll do that after a timeout.

```
~~~javascript
var EmptyPromise = function () {
    this._value = {};
    this.then = function (completedHandler) {
        //Simulate async work with a timeout so that we return before calling completedHandler
        setTimeout(completedHandler, 100, this._value);
    }
}
~~~
```

With the same consumer code as before, and suitable `console.log` calls, we'll see that `promise.then` returns before the completed handler is called. Here's the output:

```
~~~
promise created
returned from promise.then
{}
~~~
```

Indeed, all the synchronous code that follows `promise.then` will execute before the completed handler is called. This is because `setTimeout` has to wait for the app to yield the UI thread, even if that's much longer than the timeout period itself. So, if I do something synchronously obnoxious in the consumer code like the following, as in scenario 2 of the Promises example:

```
~~~javascript
var promise = doSomethingForNothing();
console.log('promise created');
~~~
```