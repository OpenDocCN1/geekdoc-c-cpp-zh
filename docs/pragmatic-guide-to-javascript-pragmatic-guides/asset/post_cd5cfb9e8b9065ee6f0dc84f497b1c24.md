
### 1 Dynamically Selecting a Method/Property

Often you find yourself wanting to call one of two methods (functions associated with an object) depending on the situation. Or instead of functions to call, this could be about reading, or writing, to one of two possible properties (variables associated with an object). The code for this would look something like what follows:

```
if (condition) {
    myObj.method1(someArg);
} else {
    myObj.method2(someArg);
}
```

JavaScript offers a simple syntax for dynamically selecting methods and properties, all relying on the square brackets ([]) operator. You see, JavaScript has two interchangeable syntaxes for member access (that is a common dynamic language trait):

```
obj[expressionResultingInMemberName] == obj.memberName
```

If you’ve ever plucked a value from an Array cell using its integer index, you’ve already used the square brackets operator for dynamic member selection! This is because Array objects have properties named after their numerical indices (plus the length property). However, in this case, JavaScript won’t let you use the dot operator (.) for direct access. myArray.0 is invalid syntax (too bad, that would have made a good nerd trick).

Here’s why using the square brackets operator ([]) is more powerful than dot notation: you can put anything in between the brackets to obtain the name of the member (property or method) that you want to access. Common cases include literals, variables holding the member name, name composition expressions (mostly string concatenations), and quick if/then choices in the form of a ternary operator (condition ? valueIfTrue : valueIfFalse). It’ll all be turned into a string first and then used to look up the member you want to use.

In JavaScript, functions are objects too and can be referenced like any other value. When an expression results in a function, you can call it by using parentheses, possibly with arguments, just like you would on a function you’re calling straight by its name.

Note that if the arguments you want to pass to the method vary depending on which technique you select, using parentheses may quickly become too cluttered for easy reading. In that case, going for a regular if/else structure is a wiser move.

#### Use the square brackets ([]) operator.

```
object['propertyName']  // => object.propertyName
object['methodName'](arg1)  // => object.methodName(arg1)
```

#### Toggle behavior.

```
// Call show() or hide(), depending on shouldBeVisible
// Avoid "heavy" animations on IE to favor immediate reflow
// (assumes we've got a properly set isIE variable)
element[shouldBeVisible ? 'show' : 'hide']();
```

#### Compose method names.

```
element[(enable ? 'add' : 'remove') + 'ClassName']('enabled');
```

#### Try this example code in any window.

```
var love = { firstName: 'Élodie', lastName: 'Porteneuve' };
var useFirstName = true;
alert(love[useFirstName ? 'firstName' : 'lastName']); // => "Élodie"
```

### 2 Achieving Code Privacy with the Module Pattern

The more JavaScript there is in your codebase, the more your global scope may get “polluted” with numerous functions and variables that would actually be better kept private to whatever set of code uses it. With this comes the risk of name collision, with one script unintentionally overwriting another’s identifiers. This leads to bugs.

We need to be able to create self-contained, opaque batches of JavaScript code, which would expose only selected identifiers, if any, to the outside world. Indeed, this is a major requirement for “programming in the large,” being able to bring in frameworks and libraries in any page without risking a clash. This is what the module pattern is for.

The whole idea of the module pattern is to create a private scope for var-declared identifiers and functions, a scope that only functions defined inside it can access. To make some of these definitions accessible to the outside world, our enclosing function has two choices. It may return an object with these selected values as properties (see the facing page); we just need to assign that returned object to a variable in the outside scope. Another way is to pass the enclosing function a scope object that it writes properties to (to make these global, you’d simply pass window).

In JavaScript, identifiers first used with the var declaring keyword are local. (They belong to the function currently defined.) Identifiers first used without var are global. (They’re grafted onto the current default scope, which most of the time means the global window object.)

In a few specific circumstances, the current default scope will not actually be global, so there are ways to execute code in a context where non-var identifiers will not leak into the global namespace—but that is a bit outside the scope of this task.

Technically, you do not have to name your “public properties” exactly like your private identifiers. Indeed, you could define public methods on the fly in the returned object literal using anonymous functions. But such practices would result in code that is more obscure (or misleading) to read and—perhaps more importantly—to debug. As a rule of thumb, whenever possible, try to define your functions using named function expressions:

```
function myFunctionName(...) { ... }
```

#### Use vars inside anonymous functions.

```
(function() {
  var privateField = 42;

  function innerFunc() {
    notSoPrivate = 43;
    return notSoPrivate;
  }

  alert(privateField); // => 42
  innerFunc();
  alert(notSoPrivate); // => 43 (ouch!)
})();
alert(typeof privateField); // => undefined
alert(notSoPrivate); // => 43 (ouch!)
```

#### Try this example: "private properties."

```
var obj = (function() {
  var privateField = 42;
  var publicField = 'foobar';

  function processInternals() { alert('Internal stuff: ' + privateField); }

  function run() {
    processInternals();
    alert('Still private stuff: ' + privateField);
    alert('Public stuff: ' + publicField);
  }

  return {
    publicField: publicField,
    run: run
  };
})();

obj.run() // three alerts: Internal, still private, public
obj.publicField // foobar
obj.processInternals() // Undefined
obj.privateField // Undefined
```

#### Declare parameters (name arguments).

```javascript
function repeat(rant, times) {
    while (--times >= 0)
        alert(rant);
}
repeat('IE6 must die!', 5); // => 5 alert boxes in a row
```

#### Grab arguments (however many).

```javascript
function repeat(times) {
    while (--times >= 0) {
        for (var index = 1, len = arguments.length; index < len; ++index) {
            alert(arguments[index]);
        }
    }
}
repeat(2, 'IE6 must die!', 'So should IE7...'); // => 4 alert boxes
```

#### Take optional arguments with default values.

```javascript
function repeat(times, rant) {
    if (undefined === rant) {
        rant = 'IE6 must die!';
    }
    while (--times >= 0) {
        alert(rant);
    }
}
repeat(3); // => 3 IE6 alert boxes
repeat(3, 'So should IE7...'); // => 3 IE7 alert boxes
```

#### Use a literal object for pseudo-named arguments.

```javascript
function repeat(options) {
    options = options || {};
    for (var opt in (repeat.defaultOptions || {})) {
        if (!(opt in options)) {
            options[opt] = repeat.defaultOptions[opt];
        }
    }
    for (var index = 0; index < options.times; ++index) {
        alert(options.rant);
    }
}
repeat.defaultOptions = { times: 2, rant: 'IE6 must die!' };

repeat(); // 2 IE6 alert boxes
repeat({ times: 3 }); // 3 IE6 alert boxes
repeat({ times: 2, rant: 'Flash must die!' }); // 2 Flash alert boxes
```

## Part II

### The DOM, Events, and Timers
