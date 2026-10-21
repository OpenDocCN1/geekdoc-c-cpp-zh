

```js
console.log(person1.hasOwnProperty("sayName"));    // true
console.log(person1.isPrototypeOf(person2));    // true
console.log(person2.hasOwnProperty("sayName"));    // false
```

这段代码创建了一个对象 person1，它具有 name 属性和 sayName() 方法。person2 对象继承自 person1，因此它继承了 name 和 sayName()。然而，person2 是通过 Object.create() 定义的，这也为 person2 定义了一个自身的 name 属性。这个自身属性会遮蔽同名原型属性，并在其位置被使用。因此，person1.sayName() 输出 "Nicholas"，而 person2.sayName() 输出 "Greg"。请记住，sayName() 仍然只存在于 person1 上，并且被 person2 继承。

在这个示例中，person2 的继承链比 person1 的更长。person2 对象继承自 person1 对象，而 person1 对象继承自 Object.prototype。参见图 5-1。

![](img/dcf53336af93733d4dab8829d31ceb8e_91_0.png)

图 5-1：person2 的原型链包括 person1 和 Object.prototype。

当在一个对象上访问属性时，JavaScript 引擎会进行搜索过程。如果属性在实例上找到（即它是自身属性），则使用该属性值。如果属性未在实例上找到，搜索会继续在 [[Prototype]] 上进行。如果属性仍未找到，搜索会继续到该对象的 [[Prototype]]，依此类推，直到链的末尾。链通常以 Object.prototype 结束，其 [[Prototype]] 设置为 null。

你也可以通过 Object.create() 创建具有 null [[Prototype]] 的对象，例如：

```js
var nakedObject = Object.create(null);
console.log("toString" in nakedObject); // false
console.log("valueOf" in nakedObject); // false
```

这个示例中的 nakedObject 是一个没有原型链的对象。这意味着内置方法如 toString() 和 valueOf() 并不存在于该对象上。实际上，这个对象是一个完全空白的画布，没有预定义的属性，这使其非常适合创建查找哈希，而无需担心潜在的命名冲突或继承的属性名。这种对象没有太多其他用途，你也不能像它继承自 Object.prototype 一样使用它。例如，任何时候你在 nakedObject 上使用运算符，你只会得到类似“Cannot convert object to primitive value.”的错误。尽管如此，JavaScript 语言中可以创建原型-less 对象，这是一个有趣的怪癖。

## 构造函数继承

JavaScript 中的对象继承也是构造函数继承的基础。回顾第 4 章，几乎每个函数都有一个可以修改或替换的 prototype 属性。该 prototype 属性会自动分配为一个继承自 Object.prototype 的新通用对象，并且有一个名为 constructor 的单一自身属性。实际上，JavaScript 引擎在幕后为你做了以下操作：

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

因此，无需做任何额外操作，这段代码就会将构造函数的 prototype 属性设置为一个继承自 Object.prototype 的对象，这意味着 YourConstructor 的任何实例也继承自 Object.prototype。YourConstructor 是 Object 的子类型，而 Object 是 YourConstructor 的超类型。

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

在这个版本的代码中，Square.prototype 被一个继承自 Rectangle.prototype 的新对象覆盖，并且 Rectangle 构造函数从未被调用。这意味着你不再需要担心因不带参数调用构造函数而导致错误。否则，这段代码的行为与之前的代码完全相同。原型链保持完整，因此 Square 的所有实例都继承自 Rectangle.prototype，并且构造函数在同一步骤中被恢复。

**NOTE** 始终确保在向其添加属性之前覆盖原型，否则在覆盖发生时你将丢失添加的方法。

## 构造函数窃取

由于 JavaScript 中的继承是通过原型链实现的，因此你不需要调用对象的超类型构造函数。如果你确实想从子类型构造函数中调用超类型构造函数，那么你需要利用 JavaScript 函数的工作方式。

在第 2 章中，你学习了 call() 和 apply() 方法，它们允许函数使用不同的 this 值被调用。这正是构造函数窃取的工作方式。你只需使用 call() 或 apply() 从子类型构造函数中调用超类型构造函数，并传入新创建的对象。实际上，你窃取了超类型构造函数用于自己的对象，如此示例所示：

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

Square 构造函数调用 Rectangle 构造函数并传入 this 以及两次 size（一次用于 length，一次用于 width）。这样做会在新对象上创建 length 和 width 属性，并使它们都等于 size。这是避免重新定义你想要继承的构造函数中的属性的方法。你可以在应用超类型构造函数之后添加新属性或覆盖现有属性。

这种两步过程在需要在自定义类型之间实现继承时很有用。你总是需要修改构造函数的原型，并且你可能还需要从子类型构造函数内部调用超类型构造函数。通常，你会修改原型以实现方法继承，并使用构造函数窃取来实现属性。这种方法通常被称为伪经典继承，因为它模仿了基于类的语言中的经典继承。

## 访问超类型方法

在之前的示例中，Square 类型有自己的 toString() 方法，它遮蔽了原型上的 toString()。在子类型中用新功能覆盖超类型方法是很常见的，但如果仍想访问超类型方法怎么办？在其他语言中，你可能可以说 super.toString()，但 JavaScript 没有类似的东西。相反，你可以直接在超类型的原型上访问该方法，并使用 call() 或 apply() 在子类型对象上执行该方法。例如：

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

在这个版本的代码中，Square.prototype.toString() 通过使用 call() 调用 Rectangle.prototype.toString()。该方法只需在返回结果文本之前将 "Rectangle" 替换为 "Square"。这种方法对于如此简单的操作来说可能显得有点冗长，但它是访问超类型方法的唯一方式。

