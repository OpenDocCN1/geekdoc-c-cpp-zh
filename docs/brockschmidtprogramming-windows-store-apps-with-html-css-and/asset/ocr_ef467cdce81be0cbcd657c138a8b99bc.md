+   - To support cancellation, the `WinJS.Promise` constructor also takes an optional second argument: a function to call if the promise's `cancel` method is called. Here you halt whatever operation is underway. The full `calculateIntegerSum` function of scenario 8, for example (again, it's in `default.js`), has a simple function to set a `_cancel` variable that the iteration loop checks before calling its next `setImmediate`.

# ## Originating Errors with WinJS.Promise.WrapError

In Chapter 3 we learned about handling async errors as a consumer of promises and the role of the `done` method vs. `then`. When originating a promise, we need to make sure that we cooperate with how all that works.

When implementing an async function, you must handle two error different error conditions. One is obvious: you encounter something within the operation that causes it to fail, such as a network timeout, a buffer overrun, the inability to access a resource, and so on. In these cases you call the error dispatcher (the second argument given to your initialization function by the `WinJS.Promise` constructor), passing an error object that describes the problem. That error object is typically created with `WinJS.ErrorFromName` (using `new`), using an error name and a message, but this is not a strict requirement. `WinJS.xhr`, for example, passes the request object directly to the error handler as that object contains much richer information already.

```
```js
if (false /* replace with any necessary error check -- we don't have any here */) {
    errorDispatch(new WinJS.ErrorFromName("calculateIntegerSum (scenario 7)", "error occurred"));
}
```
```

The other error condition is more interesting. What happens when a function that normally returns a promise encounters a problem such that it cannot create its usual promise? It can't just return `null`, because that would make it very difficult to chain promises together. What it needs to do instead is return a promise that *already* contains an error, meaning that it will immediately call any error handlers give to it `then`.

For this purpose, WinJS has a special function `WinJS.Promise.wrapError` whose argument is an error object (again typically a `WinJS.ErrorFromName`). `wrapError` creates a promise that has no fulfillment value and will never call a completed handler. It will only pass its error to any error handler if you call `then`. Still, this `then` function must yet return a promise itself; in this case it returns a promise whose fulfillment value is the error object.

For example, if `calculateIntegerSum` receives `max` or `step` arguments that are less than 1, it has to fail and can just return a promise from `wrapError` (see `default.js`):