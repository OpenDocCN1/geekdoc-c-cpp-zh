the prototype is also an object, it has its own prototype and inherits properties from that. This is the prototype chain: An object inherits from its prototype, while that prototype in turn inherits from its prototype, and so on.

All objects, including those you define yourself, automatically inherit from Object.prototype unless you specify otherwise (discussed later in this chapter). More specifically, all objects inherit from Object.prototype. Any object defined via an object literal has its [[Prototype]] set to Object.prototype, meaning that it inherits properties from Object.prototype, just like book in this example:

```
```javascript
var book = {
		title: "The Principles of Object-Oriented JavaScript"
	};

var prototype = Object.getPrototypeOf(book);

console.log(prototype === Object.prototype); // true
```
```

Here, book has a prototype equal to Object.prototype. No additional code was necessary to make this happen, as this is the default behavior when new objects are created. This relationship means that book automatically receives methods from Object.prototype.

# **Methods Inherited from Object.prototype**

+   - hasOwnProperty() Determines whether an own property with the given name exists
+   - propertyIsEnumerable() Determines whether an own property is enumerable
+   - isPrototypeOf() Determines whether the object is the prototype of another
+   - valueOf() Returns the value representation of the object
+   - toString() Returns a string representation of the object

These five methods appear on all objects through inheritance. The last two are important when you need to make objects work consistently in JavaScript, and sometimes you might want to define them yourself.