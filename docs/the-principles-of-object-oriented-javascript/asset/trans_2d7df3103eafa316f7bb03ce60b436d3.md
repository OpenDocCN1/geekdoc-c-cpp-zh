

## 5

## 继承

![](img/dcf53336af93733d4dab8829d31ceb8e_85_0.png)

学习如何创建对象是理解面向对象编程的第一步。第二步是理解继承。在传统的面向对象语言中，类从其他类继承属性。然而在 JavaScript 中，继承可以在没有类式结构定义关系的对象之间发生。这种继承的机制是你已经熟悉的：原型。

### 原型链和 Object.prototype

JavaScript 的内置继承方法称为原型链，或原型继承。正如你在第 4 章中学到的，原型属性会自动在对象实例上可用，这是一种继承形式。对象实例从原型继承属性。因为

原型本身也是一个对象，它有自己的原型并从中继承属性。这就是原型链：一个对象从其原型继承，而该原型又从其原型继承，以此类推。

所有对象，包括你自己定义的，除非另有说明，否则都会自动从 Object.prototype 继承（本章后面会讨论）。更具体地说，所有对象都从 Object.prototype 继承。任何通过对象字面量定义的对象，其 [[Prototype]] 都被设置为 Object.prototype，这意味着它从 Object.prototype 继承属性，就像本例中的 book 一样：

```
var book = {
	title: "The Principles of Object-Oriented JavaScript"
};

var prototype = Object.getPrototypeOf(book);

console.log(prototype === Object.prototype); // true
```

这里，book 的原型等于 Object.prototype。无需额外代码即可实现，因为这是创建新对象的默认行为。这种关系意味着 book 自动获得来自 Object.prototype 的方法。

### 从 Object.prototype 继承的方法

- hasOwnProperty() 判断是否存在具有给定名称的自身属性
- propertyIsEnumerable() 判断自身属性是否可枚举
- isPrototypeOf() 判断该对象是否为另一个对象的原型
- valueOf() 返回对象的数值表示
- toString() 返回对象的字符串表示

这五种方法通过继承出现在所有对象上。后两种在你需要让对象在 JavaScript 中一致工作时很重要，有时你可能想自己定义它们。

### valueOf()

每当运算符作用于对象时，就会调用 valueOf() 方法。默认情况下，valueOf() 只是返回对象实例。原始包装类型重写了 valueOf()，使其对 String 返回字符串，对 Boolean 返回布尔值，对 Number 返回数字。同样，Date 对象的 valueOf() 方法返回以毫秒为单位的纪元时间（就像 Date.prototype.getTime() 一样）。这就是允许你编写比较日期的代码的原因，例如：

```
var now = new Date();
var earlier = new Date(2010, 1, 1);

console.log(now > earlier);      // true
```

在这个例子中，now 是一个代表当前时间的 Date，而 earlier 是一个过去的固定日期。当使用大于运算符 (>) 时，在比较执行之前会先在两个对象上调用 valueOf() 方法。你甚至可以从一个日期中减去另一个日期并得到纪元时间差，这也是因为 valueOf()。

如果你希望对象与运算符一起使用，你可以随时定义自己的 valueOf() 方法。如果你确实定义了 valueOf() 方法，请记住，你并没有改变运算符的工作方式，只是改变了与运算符默认行为一起使用的值。

### toString()

当 valueOf() 返回引用值而不是原始值时，会调用 toString() 方法作为后备。它也在 JavaScript 期望字符串时隐式地对原始值调用。例如，当字符串用作加法运算符的一个操作数时，另一个操作数会自动转换为字符串。如果另一个操作数是原始值，它会被转换为字符串表示（例如，true 变成 "true"），但如果它是引用值，则会调用 valueOf()。如果 valueOf() 返回引用值，则会调用 toString() 并使用返回的值。例如：

```
var book = {
  title: "The Principles of Object-Oriented JavaScript"
};

var message = "Book = " + book;
console.log(message);      // "Book = [object Object]"
```

这段代码通过将 "Book = " 与 book 组合来构造字符串。由于 book 是一个对象，因此会调用它的 toString() 方法。该方法继承自 Object.prototype，并在大多数 JavaScript 引擎中返回默认的 "[object Object]"。如果你对该值满意，就无需更改对象的 toString() 方法。然而，有时定义自己的 toString() 方法很有用，这样字符串转换会返回更有信息量的值。假设，例如，你希望之前的脚本记录书籍的标题：

```
var book = {
    title: "The Principles of Object-Oriented JavaScript",
    toString: function() {
        return "[Book " + this.title + "]"
    }
};

var message = "Book = " + book;

// "Book = [Book The Principles of Object-Oriented JavaScript]"
console.log(message);
```

这段代码为 book 定义了一个自定义的 toString() 方法，它返回的值比继承版本更有用。你通常不需要担心定义自定义 toString() 方法，但知道在必要时可以这样做是好的。

### 修改 Object.prototype

所有对象默认都从 Object.prototype 继承，因此对 Object.prototype 的更改会影响所有对象。这是一个非常危险的情况。第 4 章建议你不要修改内置对象原型，而对 Object.prototype 这一建议更是加倍。看看会发生什么：

```
Object.prototype.add = function(value) {
    return this + value;
};

var book = {
    title: "The Principles of Object-Oriented JavaScript"
};

console.log(book.add(5));        // "[object Object]5"
console.log("title".add("end"));  // "titleend"

// in a web browser
console.log(document.add(true));  // "[object HTMLDocument]true"
console.log(window.add(5));       // "[object Window]true"
```

Object.create() 方法接受两个参数。第一个参数是用于新对象 [[Prototype]] 的对象。可选的第二个参数是属性描述符对象，其格式与 Object.defineProperties() 使用的格式相同（参见第 3 章）。考虑以下内容：

```
var book = {
  title: "The Principles of Object-Oriented JavaScript"
};

// is the same as

var book = Object.create(Object.prototype, {
  title: {
    configurable: true,
    enumerable: true,
    value: "The Principles of Object-Oriented JavaScript",
    writable: true
  }
});
```

这段代码中的两个声明在效果上是相同的。第一个声明使用对象字面量定义一个具有单个属性 title 的对象。该对象自动从 Object.prototype 继承，并且该属性默认设置为可配置、可枚举和可写。第二个声明采取相同的步骤，但使用 Object.create() 显式执行。每个声明产生的 book 对象行为完全相同。但你可能永远不会直接编写从 Object.prototype 继承的代码，因为你默认就会得到它。从其他对象继承更有趣：

```
var person1 = {
  name: "Nicholas",
  sayName: function() {
    console.log(this.name);
  }
};

var person2 = Object.create(person1, {
  name: {
    configurable: true,
    enumerable: true,
    value: "Greg",
    writable: true
  }
});

person1.sayName(); // outputs "Nicholas"
person2.sayName(); // outputs "Greg"
```

