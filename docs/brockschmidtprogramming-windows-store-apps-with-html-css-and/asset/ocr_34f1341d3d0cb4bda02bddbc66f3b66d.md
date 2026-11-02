![](bbox=[0.15, 0.08, 0.92, 0.38])

The nesting and chaining constructs that we saw in Chapter 3 can accommodate this need equally, but let's take a closer look at both.

# Nesting Promises

One way to perform sequential async operations is to nest the calls that start each operation within the completed handler of the previous one. This actually doesn't require anything special where the promises are concerned.

To see this, let's expand upon that bit of UI-thread-blocking code from Example #2 that did a bunch of counting and turn it into an async operation—see scenario 5 of the Promises example:

```
function calculateIntegerSum(max, step) {
    return new IntegerSummationPromise(max, step);
}

var IntegerSummationPromise = function (max, step) {
    this._sum = null; //null means we haven't started the operation
    this._cancel = false;
    
    //Error conditions
    if (max < 1 || step < 1) {
        return null;
    }
    
    //Handler lists
    this._cList = [];
    this._eList = [];
    this._pList = [];
    
    this._then = function (completedHandler, errorHandler, progressHandler) {
        //Save handlers in their respective arrays
        completedHandler && this._cList.push(completedHandler);
```