```
```javascript
errorHandler && this.__eList.push(errorHandler);
progressHandler && this.__pList.push(progressHandler);
var that = this;

function iterate(args) {
  for (var i = args.start; i < args.end; i++) {
    that.__sum += 1;
  }

  if (i >= max) {
    //Complete...dispatch results to completed handlers
    that.__cList.forEach(function (handler) {
      handler(that.__sum);
    });
  } else {
    //Dispatch intermediate results to progress handlers
    that.__pList.forEach(function (handler) {
      handler(that.__sum);
    });

    //Do the next cycle
    setImmediate(iterate, { start: args.end, end: Math.min(args.end + step, max) });
  }
}

//Only start the operation on the first call then
if (this.__sum === null) {
  this.__sum = 0;
  setImmediate(iterate, { start: 0, end: Math.min(step, max) });
};
this.cancel = function () {
  this.__cancel = true;
}
}
```
```

The IntegerSummationPromise class here is structurally similar to the XhrPromise class in scenario 4 to support multiple handlers and cancellation. Its asynchronous nature comes from using setImmediate to break up its computational cycles (meaning that it's still running on the UI thread; we'd have to use a web worker to run on a separate thread).

To make sequential async operations interesting, let's say we get our inputs for calculateIntegerSum from the following function (completely contrived, of course, with a promise that doesn't support multiple handlers):

```
```javascript
function getDesiredCount() {
  return new NumberPromise();
}
```
```

```
```javascript
var NumberPromise = function () {
  this.__value = 5000;
  this.then = function (completedHandler) {
```
```