However, at the point that `getDesiredCount.then` returns, we haven't even started `calculateIntegerSum` yet. This means that whatever promise is returned from `getDesiredCount.then` is some other intermediary promise. This intermediary has its own `then` method and can receive its own completed, error, and progress handlers. But instead of waiting directly for some arbitrary asynchronous operation to finish, this intermediate promise is instead waiting on the results of the completed handler given to `getDesiredCount.then`. That is, the intermediate promise is a child or subsidiary of the promise that created it, such that it can manage its relationship on the parent's completed handler.

Looking back at the code from scenario 5 in the last section, you'll see that none of our `then` implementations return anything (and are thus incomplete according to the spec). So what would it take to make it right?

Simplifying the matter for the moment by not supporting multiple calls to `then`, a promise class such as `NumberPromise` would look something like this:

```
~~~
var NumberPromise = function () {
    this._value = 1000;
    this.then = function (completedHandler) {
        setTimeout(valueAvailable, 100, this._value);
        var that = this;

        function valueAvailable(value) {
            var retVal = completedHandler(value);
            that._innerPromise.complete(retVal);
        }

        var retVal = new InnerPromise();
        this._innerPromise = retVal;
        return retVal;
    }
}
~~~
```

Here, `then` creates an instance of a promise to which we pass whatever our completed handler gives us. That extra `InnerPromise.complete` method is the private communication channel through which we tell that inner promise that it can fulfill itself now, which means it calls whatever completed handlers it received in its own `then`.

So `InnerPromise` might start to look something like this (this is not complete):

```
~~~
var InnerPromise = function (value) {
    this._value = value;
    this._completedHandler = null;
    var that = this;

    //Internal helper
    this._callComplete = function (value) {
        that._completedHandler && that._completedHandler(value);
    }

    this.then = function (completedHandler) {
~~~
```