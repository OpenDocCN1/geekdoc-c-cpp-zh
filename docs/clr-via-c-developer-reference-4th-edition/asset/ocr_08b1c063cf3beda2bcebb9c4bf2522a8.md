The following JavaScript code demonstrates how to access all of the previous WinRT components and features.

```
function () {
  // Make accessing the namespace more convenient in the code
  var winRTComps = Intel.WinRTComponents;

  // NOTE: The JavaScript VM projects WinRT APIs via camel casing
  // Access WinRT type's static method & property
  var s = winRTComps.staticMethod(null); // NOTE: JavaScript "null" here
  var struct = { index: 123, as: "Jeff", aenum: winRTComps.WinRTEnum.notnone };
  winRTComps.WinRTClass.staticProperty = struct;
  s = winRTComps.WinRTClass.staticProperty; // Read it back

  // If the method has out parameters, then they return the value
  // and are returned as an object's properties
  var s = winRTComps.WinRTClass.outParameters();
  var name = s.value; // Return value
  var struct = s.x; // an 'out' parameter
  var year = s.year; // another 'out' parameter

  // Construct an instance of the WinRT component
  var winRTClass = new winRTComps.WinRTClass(null);
  s = winRTClass.toString(); // Call ToString()

  // Demonstrate throw and catch
  try {
    winRTClass.throwingMethod();
  } catch (err) {
}

  // Array parsing
  var a = [1, 2, 3, 4, 5];
  var sum = winRTClass.passArray(a);

  // Array filling
  var arrayOut = [7, 7, 7]; // NOTE: fillArray sees all zeros!
  var length = winRTClass.fill(arrayOut); // On return, arrayOut = [0, 1, 2]

  // Array returning
  a = winRTClass.returnArray(); // a = [1, 2, 3]

  // Pass a collection and it has elements modified
  var localSettings = Windows.Storage.ApplicationData.current.localSettings;
  localSettings.values["Key1"] = "Value1";
  winRTClass.passAndModify(localSettings.values);
  // On return, localSettings.values has 2 key/value pairs in it

  // Call overloaded method
  winRTClass.someMethod(String); // Actually calls someMethod(""

  // Consume the automatically implemented event
  var f = function (v) { return v.target };
  winRTClass.addEventListener("autoevent", f, false);
  s = winRTClass.raiseEvent(7);
```