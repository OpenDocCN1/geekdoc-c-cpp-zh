In this example, sayNameForAll() accepts one parameter that is used as a label to the output value. The function is then called three times. Notice that there are no parentheses after the function name because it is accessed as an object rather than as code to execute. The first function call uses the global this and passes in the parameter "global" to output "global:Michael". The same function is called two more times, once each for person1 and person2. Because the call() method is being used, you don't need to add the function directly onto each object—you explicitly specify the value of this instead of letting the JavaScript engine do it automatically.

# The apply() Method

The second function method you can use to manipulate this is apply(). The apply() method works exactly the same as call() except that it accepts only two parameters: the value for this and an array or array-like object of parameters to pass to the function (that means you can use an arguments object as the second parameter). So, instead of individually naming each parameter using call(), you can easily pass arrays to apply() as the second argument. Otherwise, call() and apply() behave identically. This example shows the apply() method in action:

```
```javascript
function sayNameForAll(label) {
  console.log(label + ":" + this.name);
}

var person1 = {
  name: "Nicholas"
};

var person2 = {
  name: "Greg"
};

var name = "Michael";

sayNameForAll.apply(this, ["global"]); // outputs "global:Michael"
sayNameForAll.apply(person1, ["person1"]); // outputs "person1:Nicholas"
sayNameForAll.apply(person2, ["person2"]); // outputs "person2:Greg"
```
```

This code takes the previous example and replaces call() with apply(); the result is exactly the same. The method you use typically depends on the type of data you have. If you already have an array of data, use apply(); if you just have individual variables, use call().