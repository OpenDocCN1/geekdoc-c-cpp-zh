

## 以下是 JavaScript 引擎中实际发生的事情：

```
// what the JavaScript engine does
var name = "Nicholas";
var temp = new String(name);
temp.last = "Zakas";
temp = null;                     // temporary object destroyed

var temp = new String(name);
console.log(temp.last);          // undefined
temp = null;
```

代码实际上并不是为字符串分配新属性，而是在一个临时对象上创建新属性，然后该临时对象被销毁。当你稍后尝试访问该属性时，会临时创建一个不同的对象，而新属性在该对象上并不存在。尽管针对原始值会自动创建引用值，但当 instanceof 检查这些类型的值时，结果是 false：

```
var name = "Nicholas";
var count = 10;
var found = false;

console.log(name instanceof String);   // false
console.log(count instanceof Number);  // false
console.log(found instanceof Boolean); // false
```

instanceof 运算符返回 false，是因为临时对象只在读取值时才会创建。由于 instanceof 实际上不读取任何内容，因此不会创建临时对象，它告诉我们这些值不是原始包装类型的实例。你可以手动创建原始包装类型，但会产生一些副作用：

```
var name = new String("Nicholas");
var count = new Number(10);
var found = new Boolean(false);

console.log(typeof name);   // "object"
console.log(typeof count);  // "object"
console.log(typeof found);  // "object"
```

如你所见，创建原始包装类型的实例只会创建另一个对象，这意味着 typeof 无法识别你想要存储的数据类型。

此外，你不能像使用原始值那样使用 String、Number 和 Boolean 对象。例如，以下代码使用了一个 Boolean 对象。该 Boolean 对象为 false，但 console.log("Found") 仍然执行，因为在条件语句中，对象始终被视为 true。对象表示 false 并不重要；它是一个对象，所以计算结果为 true。

```
var found = new Boolean(false);

if (found) {
    console.log("Found");    // this executes
}
```

手动实例化原始包装器在其他方面也可能令人困惑，因此除非你发现这样做有意义的特殊情况，否则应避免这样做。大多数情况下，使用原始包装对象而不是原始值只会导致错误。

## 总结

虽然 JavaScript 没有类，但它有类型。每个变量或数据片段都与特定的原始类型或引用类型相关联。五种原始类型（字符串、数字、布尔值、null 和 undefined）表示直接存储在给定上下文的变量对象中的简单值。你可以使用 typeof 来识别原始类型，但 null 除外，必须直接与特殊值 null 进行比较。

引用类型是 JavaScript 中最接近类的东西，对象是引用类型的实例。你可以使用 new 运算符或引用字面量创建新对象。你主要通过点表示法访问属性和方法，但也可以使用方括号表示法。函数是 JavaScript 中的对象，你可以使用 typeof 运算符识别它们。对于任何其他引用类型的对象，你应该使用 instanceof 与构造函数来识别。

为了使原始值看起来更像引用，JavaScript 提供了三种原始包装类型：String、Number 和 Boolean。JavaScript 在后台创建这些对象，以便你可以像对待普通对象一样对待原始值，但使用它们的语句一旦执行完毕，临时对象就会被销毁。尽管你可以创建自己的原始包装器实例，但最好不要这样做，因为这可能会令人困惑。

## 2

## 函数

![](img/dcf53336af93733d4dab8829d31ceb8e_37_0.png)

如第 1 章所讨论的，函数实际上是 JavaScript 中的对象。函数的一个决定性特征——使它区别于任何其他对象——是存在一个名为 [[Call]] 的*内部属性*。内部属性不能通过代码访问，而是定义代码执行时的行为。ECMAScript 为 JavaScript 中的对象定义了多个内部属性，这些内部属性用双方括号表示法表示。

[[Call]] 属性是函数独有的，表示该对象可以被执行。由于只有函数具有此属性，ECMAScript 将 typeof 运算符定义为对任何具有 [[Call]] 属性的对象返回 "function"。这在过去导致了一些混淆，因为一些浏览器也对正则表达式包含了 [[Call]] 属性，因此它们被错误地识别为函数。现在所有浏览器的行为都是一致的，因此 typeof 不再将正则表达式识别为函数。

本章讨论在 JavaScript 中定义和执行函数的各种方式。因为函数是对象，所以它们的行为与其他语言中的函数不同，而这种行为对于深入理解 JavaScript 至关重要。

### 声明与表达式

实际上有两种函数字面量形式。第一种是函数声明，以 function 关键字开头，后面紧跟函数名称。函数内容用大括号括起来，如下所示：

```
function add(num1, num2) {
    return num1 + num2;
}
```

第二种形式是函数表达式，它不需要在 function 后面有名称。这些函数被视为匿名函数，因为函数对象本身没有名称。相反，函数表达式通常通过变量或属性来引用，如下面的表达式所示：

```
var add = function(num1, num2) {
    return num1 + num2;
};
```

这段代码实际上将一个函数值赋给了变量 add。函数表达式与函数声明几乎相同，只是缺少名称和末尾的分号。赋值表达式通常以分号结尾，就像你赋值任何其他值一样。

尽管这两种形式非常相似，但它们的区别非常重要。函数声明在代码执行时会被提升到上下文的顶部（无论是声明所在的函数还是全局作用域）。这意味着你实际上可以在代码中使用函数之后再定义它，而不会产生错误。例如：

```
var result = add(5, 5);

function add(num1, num2) {
    return num1 + num2;
}
```

这段代码看起来可能会导致错误，但实际上运行良好。这是因为 JavaScript 引擎将函数声明提升到顶部，并实际上执行代码，就好像代码是这样写的：

```
// how the JavaScript engine interprets the code
function add(num1, num2) {
    return num1 + num2;
}

var result = add(5, 5);
```

函数提升只发生在函数声明上，因为函数名称是事先已知的。另一方面，函数表达式不能被提升，因为这些函数只能通过变量来引用。所以以下代码会导致错误：

```
// error!
var result = add(5, 5);

var add = function(num1, num2) {
    return num1 + num2;
};
```

只要始终在使用函数之前定义它们，你既可以使用函数声明，也可以使用函数表达式。

### 函数作为值

由于 JavaScript 拥有一等函数，你可以像使用任何其他对象一样使用它们。你可以将它们赋值给变量、添加到对象中、作为参数传递给其他函数，并从函数中返回它们。基本上，你可以在任何使用其他引用值的地方使用函数。这使得 JavaScript 函数异常强大。考虑以下示例：

```
① function sayHi() {
    console.log("Hi!");
}

sayHi();      // outputs "Hi!"

② var sayHi2 = sayHi;

sayHi2();     // outputs "Hi!"
```

