```
```javascript
// Array filling
var arrayOut = [7, 7, 7];    // NOTE: fillArray sees all zeros!
var length = winRTClass.arrayOut(); // On return, arrayOut = [0, 1, 2]

// Array returning
a = winRTClass.returnArray();    // a = [1, 2, 3]

// Pass a collection and have its elements modified
var localSettings = Windows.Storage.ApplicationData.current.localSettings;
localSettings.values["Key1"] = "Value1";
winRTClass.passAndModifyCollection(localSettings.values);
// On return, localSettings.values has 2 key/value pairs in it

// Call overloaded method
winRTClass.someMethod(5);       // Actually calls SomeMethod(String) passing "5"

// Consume the automatically implemented event
s = function (v) { console.log(v.target); };
winRTClass.addEventListener("autoevent", f, false);
s = winRTClass.raiseAutoEvent(7);

// Consume the manually implemented event
winRTClass.addEventListener("manualEvent", f, false);
s = winRTClass.raiseManualEvent(8);

// Invoke asynchronous method supporting progress, cancelation, & error handling
var promise = winRTClass.doSomethingAsync();
promise.then(
    function (result) { console.log("Async op complete: " + result); },
    function (error) { console.log("Async op error: " + error); },
    function (progress) {
        console.log("Async op progress: " + progress);
        //if (progress == 30) promise.cancel();    // To test cancelation
    }
);
```
```