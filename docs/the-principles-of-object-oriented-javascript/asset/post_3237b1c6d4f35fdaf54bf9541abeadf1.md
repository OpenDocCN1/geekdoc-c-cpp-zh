
```js
console.log(person1.hasOwnProperty("sayName"));    // true
console.log(person1.isPrototypeOf(person2));    // true
console.log(person2.hasOwnProperty("sayName"));    // false
```

This code creates an object, person1, with a name property and a sayName() method. The person2 object inherits from person1, so it inherits both name and sayName(). However, person2 is defined via Object.create(), which also defines an own name property for person2. This own property shadows the prototype property of the same name and is used in its place. So, person1.sayName() outputs "Nicholas", while person2.sayName() outputs "Greg". Keep in mind that sayName() still exists only on person1 and is being inherited by person2.

The inheritance chain in this example is longer for person2 than it is for person1. The person2 object inherits from the person1 object, and the person1 object inherits from Object.prototype. See Figure 5-1.

![](img/dcf53336af93733d4dab8829d31ceb8e_91_0.png)

Figure 5-1: The prototype chain for person2 includes person1 and Object.prototype.

When a property is accessed on an object, the JavaScript engine goes through a search process. If the property is found on the instance (that is, if it’s an own property), that property value is used. If the property is not found on the instance, the search continues on [[Prototype]]. If the property is still not found, the search continues to that object’s [[Prototype]], and so on until the end of the chain is reached. That chain usually ends with Object.prototype, whose [[Prototype]] is set to null.

You can also create objects with a null [[Prototype]] via Object.create(), such as:

```js
var nakedObject = Object.create(null);
console.log("toString" in nakedObject); // false
console.log("valueOf" in nakedObject); // false
```

The nakedObject in this example is an object with no prototype chain. That means built-in methods such as toString() and valueOf() aren’t present on the object. In effect, this object is a completely blank slate with no predefined properties, which makes it perfect for creating a lookup hash without potential naming collisions or inherited property names. There aren’t many other uses for an object like this, and you can’t use it as if it were inheriting from Object.prototype. For example, any time you use an operator on nakedObject, you’ll just get an error along the lines of “Cannot convert object to primitive value.” Still, it’s an interesting quirk of the JavaScript language that you can create a prototype-less object.

## Constructor Inheritance

Object inheritance in JavaScript is also the basis of constructor inheritance. Recall from Chapter 4 that almost every function has a prototype property that can be modified or replaced. That prototype property is automatically assigned to be a new generic object that inherits from Object.prototype and has a single own property called constructor. In effect, the JavaScript engine does the following for you:

```js
// you write this
function YourConstructor() {
  // initialization
}

// JavaScript engine does this for you behind the scenes
YourConstructor.prototype = Object.create(Object.prototype, {
  constructor: {
    configurable: true,
    enumerable: true,
    value: YourConstructor,
    writable: true
  }
});
```

So without doing anything extra, this code sets the constructor's prototype property to an object that inherits from Object.prototype, which means any instances of YourConstructor also inherit from Object.prototype. YourConstructor is a subtype of Object, and Object is a supertype of YourConstructor.

```js
// inherits from Rectangle
function Square(size) {
	this.length = size;
	this.width = size;
}

Square.prototype = Object.create(Rectangle.prototype, {
	constructor: {
		configurable: true,
		enumerable: true,
		value: Square,
		writable: true
	}
});

Square.prototype.toString = function() {
	return "[Square " + this.length + "x" + this.width + "]";
};
```

In this version of the code, Square.prototype is overwritten with a new object that inherits from Rectangle.prototype, and the Rectangle constructor is never called. That means you don't need to worry about causing an error by calling the constructor without arguments anymore. Otherwise, this code behaves exactly the same as the previous code. The prototype chain remains intact, so all instances of Square inherit from Rectangle.prototype and the constructor is restored in the same step.

**NOTE** Always make sure that you overwrite the prototype before adding properties to it, or you will lose the added methods when the overwrite happens.

## Constructor Stealing

Because inheritance is accomplished through prototype chains in JavaScript, you don't need to call an object's supertype constructor. If you do want to call the supertype constructor from the subtype constructor, then you need to take advantage of how JavaScript functions work.

In Chapter 2, you learned about the call() and apply() methods, which allow functions to be called with a different this value. That's exactly how constructor stealing works. You simply call the supertype constructor from the subtype constructor using either call() or apply() to pass in the newly created object. In effect, you're stealing the supertype constructor for your own object, as in this example:

```js
function Rectangle(length, width) {
	this.length = length;
	this.width = width;
}
```

```js
Rectangle.prototype.getArea = function() {
    return this.length * this.width;
};

Rectangle.prototype.toString = function() {
    return "[Rectangle " + this.length + "x" + this.width + "]";
};

// inherits from Rectangle
function Square(size) {
    Rectangle.call(this, size, size);
    // optional: add new properties or override existing ones here
}

Square.prototype = Object.create(Rectangle.prototype, {
    constructor: {
        configurable: true,
        enumerable: true,
        value: Square,
        writable: true
    }
});

Square.prototype.toString = function() {
    return "[Square " + this.length + "x" + this.width + "]";
};

var square = new Square(6);

console.log(square.length);      // 6
console.log(square.width);        // 6
console.log(square.getArea());    // 36
```

The Square constructor calls the Rectangle constructor and passes in this as well as size two times (once for length and once for width). Doing so creates the length and width properties on the new object and makes each equal to size. This is the way to avoid redefining properties from a constructor from which you want to inherit. You can add new properties or override existing ones after applying the supertype constructor.

This two-step process is useful when you need to accomplish inheritance between custom types. You'll always need to modify a constructor's prototype, and you may also need to call the supertype constructor from within the subtype constructor. Generally, you'll modify the prototype for method inheritance and use constructor stealing for properties. This approach is typically referred to as pseudoclassical inheritance because it mimics classical inheritance from class-based languages.

## Accessing Supertype Methods

In the previous example, the Square type has its own toString() method that shadows toString() on the prototype. It is fairly common to override supertype methods with new functionality in the subtype, but what if you still want to access the supertype method? In other languages, you might be able to say super.toString(), but JavaScript doesn’t have anything similar. Instead, you can directly access the method on the supertype’s prototype and use either call() or apply() to execute the method on the subtype object. For example:

```js
function Rectangle(length, width) {
  this.length = length;
  this.width = width;
}
```

```js
Rectangle.prototype.getArea = function() {
  return this.length * this.width;
};
```

```js
Rectangle.prototype.toString = function() {
  return "[Rectangle " + this.length + "x" + this.width + "]";
};
```

```js
// inherits from Rectangle
function Square(size) {
  Rectangle.call(this, size, size);
}
```

```js
Square.prototype = Object.create(Rectangle.prototype, {
  constructor: {
    configurable: true,
    enumerable: true,
    value: Square,
    writable: true
  }
});
```

```js
// call the supertype method
Square.prototype.toString = function() {
  var text = Rectangle.prototype.toString.call(this);
  return text.replace("Rectangle", "Square");
};
```

In this version of the code, Square.prototype.toString() calls Rectangle.prototype.toString() by using call(). The method just needs to replace "Rectangle" with "Square" before returning the resulting text. This approach may seem a bit verbose for such a simple operation, but it is the only way to access a supertype's method.
