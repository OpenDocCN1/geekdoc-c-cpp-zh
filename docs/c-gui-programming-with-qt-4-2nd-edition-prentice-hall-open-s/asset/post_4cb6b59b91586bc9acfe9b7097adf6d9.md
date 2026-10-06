
it from the arguments array:

```javascript
function sum()
{
  var unaryFunc = arguments[0];
  var result = 0;
  for (var i = 1; i < arguments.length; ++i) {
    result += unaryFunc(arguments[i]);
  }
  return result;
}
```

The arguments array can be used to overload the behavior of functions based on the types of the arguments or on their number. For example, suppose that we want to let sum() take an optional unary argument followed by a list of numbers, allowing us to invoke it as follows:

```javascript
print(sum(1, 2, 3, 4, 5, 6));
print(sum(square, 1, 2, 3, 4, 5, 6));
```

Here's how we can implement sum() to support this:

```javascript
function sum()
{
  var unaryFunc = function(x) { return x; };
  var i = 0;

  if (typeof arguments[0] == "function") {
    unaryFunc = arguments[0];
    i = 1;
  }

  var result = 0;
  while (i < arguments.length) {
    result += unaryFunc(arguments[i++]);
  }
  return result;
}
```

If we supply a function as the first argument, that function is applied to each number before it is added to the sum; otherwise, we use the identity function function(x) { return x; }

For C++ programmers, arguably the most difficult aspect of ECMAScript is its apart from C++, C#, Java, Simula, and Smalltalk, which are all class-based. Instead of a class concept, ECMAScript provides us with lower-level mechanisms that let us achieve the same results.

The first mechanism that lets us implement classes in ECMAScript is that of a constructor. A constructor is a function that can be invoked using the new operator. For example, we have a constructor for Shape object:

```javascript
function Shape(x, y) {
  this.x = x;
  this.y = y;
}
```

The Shape constructor has two parameters and initializes the new object's x and y properties (member variables) based on the values passed to the constructor. The this keyword refers to the object being created. In ECMAScript, an object is essentially a collection of properties; properties can be added, removed, or modified at any time. A property is created the first time it is set, when we assign to this.x and this.y in the constructor, the x and y properties are created as a result.

A common mistake for C++ and Java developers is to forget the this keyword when accessing object properties. In the preceding example, this would have been unlikely, because a statement such as x = x would have looked very suspicious, but in other examples this would have led to the creation of spurious global variables.

To instantiate a Shape, we use the new operator as follows:

```javascript
var shape = new Shape(10, 20);
```

If we use the typeof operator on the shape variable, we obtain Object, not Shape, as the data type. If we want to determine whether an object has been created using the Shape constructor, we can use the instanceof operator:

```javascript
var array = new Array(100);
array instanceof Shape;      // returns false
```

```javascript
var shape = new Shape(10, 20);
shape instanceof Shape;      // returns true
```

ECMAScript does not perform any function service as a constructor. However, if the function this object, it doesn't make sense to invoke it as a constructor. Conversely, a constructor can be invoked as a plain function, but again this rarely makes sense. ECMAScript provides built-in constructors that let us instantiate fundamental object types, notably Array, Date, RegExp. Other constructors convert the primitive data types, allowing us to create objects that store primitive values. Using the valueOf() member function lets us retrieve the primitive value stored in the object. For example:

```javascript
var boolObj = new Boolean(true);
typeof boolObj; // returns "object"

var boolVal = boolObj.valueOf();
typeof boolVal; // returns "boolean"
```

Figure 22.1 lists the built-in global constants, functions, and objects provided by ECMAScript. In the next section, we will see how to supplement this functionality with additional, application-specific components written in C++.

# Figure 22.1. Built-in properties of the global object

| Constants | Description |
| :--- | :--- |
| NaN | IEEE 754 Not-a-Number (NaN) value |
| Infinity | Positive infinity (+∞) |
| undefined | Default value for uninitialized variables |

| Functions | Description |
| :--- | :--- |
| print(x) | Prints a value on the console |
| eval(str) | Executes an ECMAScript program |
| parseInt(str, base) | Converts a string to an integer |
| parseFloat(str) | Converts a string to a floating-point value |
| isNaN(n) | Returns true if n is NaN |
| isFinite(n) | Returns true if n is a number other than NaN, +∞, or -∞ |
| decodeURI(str) | Converts 8-bit-encoded URI to Unicode |
| decodeURIComponent(str) | Converts 8-bit-encoded component to Unicode |
| encodeURI(str) | Converts a Unicode URI to 8-bit-encoded |
| encodeURIComponent(str) | Converts a Unicode component to 8-bit-encoded specified by the ECMAScript standard. |

| Classes (Constructors) | Description |
| :--- | :--- |
| Object | Provides functionality common to all objects |
| Function | Encapsulates an ECMAScript function |
| Array | Represents a resizable vector of items |
| String | Stores a Unicode string |
| Boolean | Stores a Boolean value (true or false) |
| Number | Stores a floating-point number |
| Date | Stores a date and time |
| RegExp | Provides regular expression matching |
| Error | Base type for error types |
| EvalError | Raised using eval() wrongly |
| RangeError | Raised when numeric value is outside the legal range |
| ReferenceError | Raised when trying to access undefined variable |
| SyntaxError | Raised when syntax error is detected by eval() |
| TypeError | Raised when argument is the wrong type |
| URIError | Raised when parsing fails |
| Math | Provides mathematical constants and functions |

We have seen how to define a constructor in ECMAScript and how to add member variables to the object. Normally, we also want to define member functions. Because functions are treated as first-class citizens in ECMAScript, this turns out to be surprisingly easy. Here's a new version of the Shape constructor, this time with member functions:

```javascript
function Shape(x, y) {
  this.x = x;
  this.y = y;

  this.hattanPos = function() {
    return Math.abs(this.x) + Math.abs(this.y);
  };
  this.translate = function(dx, dy) {
    this.x += dx;
    this.y += dy;
  };
}
```

We can then invoke the member functions using the .dot operator:

```javascript
var shape = new Shape(10, 20);
shape.translate(100, 100);
print(shape.x + ", " + shape.y + " (" + shape.hattanPos() + ")");
```

With this approach, each Shape instance has its own manPos and translate properties. These properties should be identical for all Shape instances; it is desirable to store them only once rather than in every instance. ECMAScript lets us achieve this by using a prototype. A prototype is an object that serves as a fallback for other objects, providing an initial set of properties. One advantage of this approach is that it is possible to change the prototype object at any time and the changes are immediately reflected in all objects that were created with that prototype.

```javascript
function Shape(x, y) {
  this.x = x;
  this.y = y;
}

Shape.prototype.hattanPos = function() {
  return Math.abs(this.x) + Math.abs(this.y);
};

Shape.prototype.translate = function(dx, dy) {
  this.x += dx;
  this.y += dy;
};
```

In this version of Shape, we create the manPos and translate properties outside the constructor, as properties of the Shape.prototype object. When we instantiate a Shape, the newly created object has an internal pointer back to Shape.prototype. Whenever we retrieve the value of a property that doesn't exist in our Shape object, the property is looked up in the prototype as a fallback. Thus, the Shape prototype is the ideal place to put member functions, which should be shared by all Shape instances.

It might be tempting to put all sorts of properties that we want to share between instances in the prototype, similar to C++s static member variables or Java's class functions. This idiom works for read-only properties (including members) because the prototype acts as a fallback when we retrieve the value of a property. However, it doesn't work as expected when we want to assign a new value to the shared variable; instead, a fresh variable is created directly in the Shape object, shadowing any property of the same name in the prototype. This asymmetry between read and write access to a variable is a frequent source of confusion for novice ECMAScript programmers.

In class-based languages like C++ and Java, we can use class inheritance to create specialized objects. For example, we would define a Shape class and derive Triangle, Square, and Circle from Shape. In ECMAScript, a similar effect can be achieved using prototypes. The following example shows how to define Circle objects that are also Shape instances:
