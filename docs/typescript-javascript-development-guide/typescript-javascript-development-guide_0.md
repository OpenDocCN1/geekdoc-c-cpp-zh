
# TypeScript：JavaScript 开发指南

![](img/00001.jpeg)

保留所有权利

打开终端，执行下方提供的命令：

```bash
$ curl http://npmjs.org/install.sh | sh
$ npm --version
1.1.70
```

在一步中，安装 TypeScript 的 `npm` 软件包，这应该在命令行中全局执行。可以使用以下命令执行此操作：

```bash
$ npm install -g typescript
$ npm view typescript version
npm http GET https://registry.npmjs.org/typescript
npm http 304 https://registry.npmjs.org/typescript
0.8.1-1
```

确保你使用的是最新版本的浏览器，例如 `Chrome`。任何文本编辑器都是适用的，例如 Sublime 文本编辑器。

## Hello World 示例

现在我们已经准备好了编程环境，可以开始编程了。我们将从创建 Hello world 示例开始。记住 TypeScript 是 `ES5` 的超集，它拥有更多 `ES6` 的特性。TypeScript 也会编译成 `JavaScript`。

我们要创建一个 `index.html` 文件，然后将其引用到外部文件。以下是 `index.html` 文件的代码：

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>This is TypeScript</title>
</head>
<body>
  <script src="hello.ts"></script>
</body>
</html>
```

如上述代码所示，我们将文件中的代码引用到了 `hello.ts` 文件。这是在 `<script src="hello.ts"></script>` 这一行完成的。文件后缀 `.ts` 意味着这是一个 TypeScript 文件。

现在，创建一个新文件并命名为 `hello.ts`。应在文件中添加以下行代码：

```javascript
alert('hello world, this is TypeScript!');
```

之后，启动命令行，然后导航到 `hello.ts` 文件所在的文件夹。执行以下命令编译文件：

```bash
tsc hello.ts
```

TypeScript 中的 `tsc` 命令代表 TypeScript 编译器，它将生成一个名为 `hello.js` 的新文件。通过文件后缀，我们将 TypeScript 转换为 JavaScript 文件。

## 第 3 章：类型注解

该功能在 TypeScript 中是可选的，允许我们在 TypeScript 程序中表达并实现类型注解。我们需要通过创建一个计算矩形面积的程序来演示这一点。只需打开文本编辑器并创建一个名为 `area.ts` 的新文件。在文件中添加以下代码：

```typescript
function area(shape: string, width: number, height: number) {
  var area = width * height;
  return "The shape is " + shape + " having an area of " + area + " cm squared.";
}

document.body.innerHTML = area("rectangle", 20, 15);
```

接下来，打开 `index.html` 文件并将脚本源从 `type.ts` 改为 `area.ts`。打开终端，然后执行以下命令以编译整个内容：

```bash
tsc area.ts
```

消息将与矩形的面积一起显示。正如你可能已经注意到的，类型注解被传递给函数的参数，它们用于指示函数支持的参数类型。在上面的示例中，参数 `shape` 是一个字符串，而参数 `length` 和 `width` 是数字。

你必须知道，类型注解（Type annotations）和其他 TypeScript 特性在编译期间都是强制执行的。如果向这些参数传递了其他类型的值，编译器将显示编译时错误。在处理大型应用程序时，这是一个非常好的主意。

我们需要演示在我们的情况下是如何检测到错误的。考虑下面的代码：

```typescript
function area(shape: string, width: number, height: number) {
    var area = width * height;
    return "The shape is " + shape + " having an area of " + area + " cm squared.";
}

document.body.innerHTML = area("rectangle", "width", 15); // width 类型错误
```

在上面的示例中，`width` 被作为字符串传递，这是错误的。编译器期望 `width` 应该是一个数字。编译上面的程序后，你将得到以下错误：

```bash
$ tsc type.ts
type.ts(6,26): Supplied parameters do not match any signature of call target
```

这就是你得到的错误类型。

然而，你可能注意到，尽管由于类型不匹配产生了警告，但这并没有阻止 TypeScript 文件的编译并生成 JavaScript 文件。

如上面的示例所示，很清楚注解被用于记录函数或变量意图执行的操作。假设你有一个函数，它期望只传递一个参数，且该参数应该是字符串类型。一旦向它传递一个数组，会发生什么？考虑下面的示例：

```typescript
function welcome(name: string) {
    return "Hello, " + name;
}

var user = [0, 1, 2];

document.body.innerHTML = wlecome(user);
```

一旦你重新编译上述代码，你将得到以下错误：

```text
welcome.ts(7,26): Supplied parameters do not match any signature of call target
```

同样，你可以尝试从 `welcome` 调用中移除所有参数。TypeScript 编译器将警告你传递了意料数量的参数。

## 第 4 章：接口（Interfaces）

我们需要通过扩展之前的示例来实现一个接口，该接口将形状描述为一个具有可选 `color` 属性的对象。

创建一个新文件，并命名为 `interface.ts`。打开 `index.html` 文件，然后修改使其脚本源为 `interface.js`。将以下代码添加到 `interface.ts` 文件：

```typescript
interface Shape {
    name: string;
    width: number;
    height: number;
    color?: string;
}

function area(shape : Shape) {
    var area = shape.width * shape.height;
    return "The shape is " + shape.name + " having an area of " + area + " cm squared";
}

console.log( area( {name: "rectangle", width: 20, height: 15} ) );
console.log( area( {name: "square", width: 20, height: 25, color: "blue"} ) );
```

接口是赋予对象类型的名称。我们可以声明接口，并同时在类型注解中使用它。

一旦你编译 `interface.js` 文件，你将不会得到任何错误。为了让它产生错误，我们在 `interface.js` 文件中添加一行新代码，包含一个没有 `name` 属性的形状，然后在浏览器的控制台中观察结果。将下面的代码添加到 `interface.js` 文件中：

```typescript
console.log( area( {width: 20, height: 15} ) );
```

然后你可以运行 `tsc interface.js` 命令来编译文件中的代码。将输出一个错误，但目前不要担心它。刷新你的浏览器，然后观察控制台给你的结果。文本和矩形的面积将形成控制台上的输出。箭头应该如下所示：

```text
interface.ts(26,13): Supplied parameters do not match any signature of call target:
Could not apply type 'Shape' to argument 1, which is of type '{ width: number; height: number; }'
```

上述错误的结果是因为传递给函数 `area()` 的对象不符合名为 `shape` 的接口，因为它需要一个 `name` 属性。

考虑下面的代码，它展示了如何在 TypeScript 中使用接口：

```typescript
interface Person {
    fName: string;
    lName: string;
}

function welcome(person: Person) {
    return "Hello, " + person.fName + " " + person.lName;
}

var user = { fName: "Jane", lName: "User" };

document.body.innerHTML = welcome(user);
```

## 第 5 章：函数表达式（Function Expressions）

理解 `this` 的作用域是挑战性的。TypeScript 支持使用箭头函数，这使其变得更简单。注意下面的示例：

```typescript
var shape = {
    name: "rectangle",
    width: 20,
    height: 15
};

function area(shape) {
    var area = shape.width * shape.height;
    return "The shape is " + shape.name + " having an area of " + area + " cm squared";
}

console.log(area(shape));

var shape = {
    name: "square",
    width: 20,
    height: 25,
    color: "blue"
};

function area(shape) {
    var area = shape.width * shape.height;
    return "The shape is " + shape.name + " having an area of " + area + " cm squared";
}

console.log(area(shape));
```

```javascript
this.becomeOld = function() {
    _this.age++;  // 使用已经捕获的 this
}
}

var person = new Person(1);

setTimeout(person.becomeOld, 1000);

setTimeout(function() { console.log(person.age); }, 2000); // 2
```

由于我们使用的是 TypeScript，可以通过结合类和箭头函数来使用更简洁的语法。下方的示例代码所示：

```typescript
class Person {
    constructor(public age:number) {}

    becomeOld = () => {
        this.age++;
    }
}

var person = new Person(1);

setTimeout(person.becomeOld, 1000);

setTimeout(function() { console.log(person.age); }, 2000); // 2
```

然而，你应该知道，只有当你打算将函数交给其他个人以进行调用时，才应该使用箭头函数。如下所示：

```javascript
var becomeOld = person.becomeOld;

// 这稍后会被其他人调用：

becomeOld();
```

如果你是自己调用它，应该像下面所示执行：

```javascript
person.becomeOld();
```

然后 `this` 对象将成为正确的调用上下文。

在大多数情况下，库会使用对象 `this` 来传递当前正在迭代的对象。如果你需要访问库传递的 `this`，甚至是你的周围变量，你可以像像没有箭头函数的情况下那样使用一个临时变量。下方的代码所示：

```javascript
let _self = this;

thing.each(function() {
    console.log(_self); // 这是你的词法作用域值
    console.log(this); // 这是库传递的值
});
```

## 第 6 章：类

在 TypeScript 中，有具有公共（public）或私有（private）访问权限的类。在 TypeScript 中，类的用法与 ES6 相同。创建一个新文件并命名为 `class.ts`。在类中添加以下代码：

```typescript
class Shape {
    area: number;
    color: string;
    constructor ( name: string, width: number, height: number ) {
        this.area = width * height;
        this.color = "red";
    };
    shoutit() {
        return "The object is" + this.color + " " + this.name + " having an area of " + this.area + " cm squared.";
    }
}

var square = new Shape("square", 20, 20);

console.log( square.shoutit() );
console.log( 'Area of Object: ' + square.area );
console.log( 'Name of Object: ' + square.name );
console.log( 'Color of Object: ' + square.color );
console.log( 'Width of Object: ' + square.width );
console.log( 'Height of Object: ' + square.height );
```

我们在上例示例中的对象有两个属性，即 `area` 和 `color`。我们还实现了一个构造函数和 `shoutit()` 方法。我们的构造函数参数的作用域局限于构造函数。由于由于，在浏览器和编译器中都会观察到错误，如下：

```text
class.ts(12,42): The 'name' property does not exist on the value of type 'Shape'
class.ts(20,40): The 'name' property does not exist on the value of type 'Shape'
class.ts(22,41): The 'width' property does not exist on the value of type 'Shape'
class.ts(23,42): The 'height' property does not exist on the value of type 'Shape'
```

TypeScript 支持 `public` 和 `private` 访问修饰符。对于公共成员，我们可以从任何地方访问它们，而对于私有成员，我们只能在内部访问它们。在 JavaScript 中，没有可以用于强制私有化的功能，这就是为什么它在编译期间强制执行，并提醒开发者他们将其设置为私有的意图。

我们需要为构造函数参数 `name` 添加公共访问修饰符，然后为成员即 `color` 添加私有访问修饰符。一旦在构造函数的参数上添加了访问修饰符，它将自动成为具有该访问修饰符的类成员。考虑下面的示例：

```typescript
...
private color: string;
...
constructor ( public name: string, width: number, height: number ) {
...
```

考虑下方的 ES 6 类：

```javascript
class Monster {
    constructor(name, initPosition) {
        this.name = name;
        this.initPosition = initPosition;
    }
}
```

在 TypeScript 中，有具有公共或私有访问权限的类。在 TypeScript 中，类的用法与 ES6 相同。创建一个新文件并命名为 `class.ts`。在类中添加以下代码：



```typescript
class Shape {
    area: number;
    color: string;
    constructor ( name: string, width: number, height: number ) {
        this.area = width * height;
        this.color = "red";
    };
    shoutit() {
        return "The object is" + this.color + " " + this.name + " having an area of " + this.area + " cm squared.";
    }
}

var square = new Shape("square", 20, 20);

console.log( square.shoutit() );
console.log( 'Area of Object: ' + square.area );
console.log( 'Name of Object: ' + square.name );
console.log( 'Color of Object: ' + square.color );
console.log( 'Width of Object: ' + square.width );
console.log( 'Height of Object: ' + square.height );
```

我们在上例示例中的对象有两个属性，即 `area` 和 `color`。我们还实现了一个构造函数和 `shoutit()` 方法。我们的构造函数参数的作用域局限于构造函数。由于由于，在浏览器和编译器中都会观察到错误，如下：

```text
class.ts(12,42): The 'name' property does not exist on the value of type 'Shape'
class.ts(20,40): The 'name' property does not exist on the value of type 'Shape'
class.ts(22,41): The 'width' property does not exist on the value of type 'Shape'
class.ts(23,42): The 'height' property does not exist on the value of type 'Shape'
```

TypeScript 支持 `public` 和 `private` 访问修饰符。对于公共成员，我们可以从任何地方访问它们，而对于私有成员，我们只能在内部访问它们。在 JavaScript 中，没有可以用于强制私有化的功能，这就是为什么它在编译期间强制执行，并提醒开发者他们将其设置为私有的意图。

我们需要为构造函数参数 `name` 添加公共访问修饰符，然后为成员即 `color` 添加私有访问修饰符。一旦在构造函数的参数上添加了访问修饰符，它将自动成为具有该访问修饰符的类成员。考虑下面的示例：

```typescript
...
private color: string;
...
constructor ( public name: string, width: number, height: number ) {
...
```

在 TypeScript 中，支持访问修饰符，这些修饰符控制了访问变量的方式。变量可以通过类的实例直接访问，也可以在子类中被访问。以下是三种类型的访问修饰符：

1. `public`：在任何地方都可以通过实例进行访问。
2. `private`：在类外部无法访问。
3. `protected`：在子类中可以访问，但不能直接通过实例访问。

你应该意识到，这对你的程序没有多大影响，但如果你尝试在运行时访问它们，它们将给你返回一些错误。考虑下面的示例，它展示了如何进行操作：

```typescript
class ClassBase {
   public a: number;
   private b: number;
   protected c: number;
}

// 对实例的影响
var myVar = new ClassBase();

foo.a; // okay
foo.b; // ERROR : private
foo.c; // ERROR : protected

// 对子类的影响
class ClassChild extends ClassBase {
   constructor() {
      super();
      this.a; // okay
      this.b; // ERROR: private
      this.c; // okay
   }
}
```

如你所知，上述修饰符同样适用于成员属性和成员函数。

### 使用构造函数定义

类中的成员可以如下所示进行初始化：

```typescript
class MyClass {
   x: number;
   constructor(x:number) {
      this.x = x;
   }
}
```

这是 TypeScript 中一个非常常见的场景，人们只需在成员前加上访问修饰符，它就会类中自动声明，然后从你的构造函数中复制。通过此，我们之前的示例可以写如下所示：

```typescript
class MyClass {
   constructor(public x:number) {
   }
}
```

### 属性初始化

这是 TypeScript 支持的一个非常重要的特性。你可以在构造函数之外初始化类的任何成员，这对于提供默认值很有用。考虑下面的示例：

```typescript
class MyClass {
   members = [];  // 直接初始化
   add(x) {
      this.members.push(x);
   }
}
```

### 剩余参数

此功能允许在函数接受多个参数，然后以数组的形式获取这些参数。可以像下面的示例所示：

```typescript
Function allFunction(first, second, ...rest) {
   console.log(rest);
}

allFunction ('sample', 'bar'); // []
allFunction ('sample', 'bar', 'bas', 'qux'); // ['bas','qux']
```

## 第 7 章 - 解构

解构意味着分解结构。TypeScript 支持以下类型的解构：

1. 对象解构
2. 数组解构

为了方便起见，可以将解构视为结构化的逆过程。下面的示例展示了在 JavaScript 中如何进行结构化：

```javascript
var myVar = {
   bar: {
      bas: 789
   }
};
```

由于 JavaScript 对结构化的支持，创建新对象的过程将有些困难。通过解构，我们获得了获取特定源数据的同等便利性。

### 对象解构

通过解构，人们可以在单行内完成原本需要多行代码的工作。考虑下面的示例：

```javascript
var rectangle = { a: 0, b: 10, height: 20 };
var {a, b, height} = rectangle;
console.log(a, b, height);
```

如果我们不使用解构，`a`、`b` 和 `height` 将被单独选取。也可以通过解构从结构中获取深层数据。下面的代码最好地说明了如何做到这一点：

```javascript
var foo = { bas: 123 };
var {bas} = foo; // 相当于 bas = foo.bas
```

### 数组解构

`const` 是 TypeScript 和 ES6 引入的新特性。通过它，人们可以使变量不可不可变的。这在运行时和文档方面都有很好的作用。要使用它，只需将关键字 `var` 替换为 `const`。考虑下面的代码：

```typescript
const maximumRows = 10;
if (a > maximumRows) {
// 低可读性
```

在 TypeScript 中，使用 `const` 比其他语言的情况要容易得多。它帮助我们避免魔法字面量，是提高可读性的良好实践。

### `const` 的初始化

必须完成 `const` 声明。此外，在创建常量之后，它们变得不可变，所以如果你尝试给它们分配新值，你将得到编译错误。考虑下面的代码：

```typescript
const myConst = 123;
myConst = 540; // ERROR: 赋值左侧不能为常量
```

如上所示，尝试这样做会导致注释中提到的编译错误。

### 块级作用域

`const` 只是像 `let` 一样具有作用域的块。下面的代码最好地描述了这一点：

```typescript
const myConst = 123;
if (true) {
   const myConst = 500; // 允许，因为新变量限于此 if 块
}
```

### 深层不可变性

就你而言，我们可以在对象字面量使用 `const`，以保护变量的引用。然而，你仍然可以修改对象的属性。如下代码所示：

```typescript
const myConst = { bar: 123 };
myConst.bar = 500; // 允许的
console.log(myConst); // { bar: 500 }
```

## 第 8 章 - `for...of`

`for...of` 并不遍历数组的元素，这是 JavaScript 初学者经常遇到的一个问题。它遍历对象的键。考虑下面的示例，它最好描述了这一点：

```javascript
var myArray = [7, 2, 5];
for (var item in myArray) {
   console.log(item); // 0,1,2
}
```

在上面的示例中，尽管我们期望得到 7, 2, 5，但得到的是索引 0、1、2。这就是为什么引入了 `for...of`。考虑下面的示例，它将遍历数组元素并输出预期的结果：

```javascript
var myArray = [7, 2, 5];
for (var item of myArray) {
   console.log(item); // 7,2,5
}
```

上面的示例输出的是预期的结果而不是索引。同样，在 TypeScript 中，人们可以使用 `for...of` 逐字符遍历字符串。如下代码所示：

```typescript
var hi = "are you the one looking for me?";
for (var char of hi) {
   console.log(char); // are you the one looking for me?
}
```

### JS 生成

对于预 ES6，TypeScript 总是生成标准的 `for (var i = 0; i < list.length; i++)`。我们之前的示例将生成以下内容：

```javascript
var myArray = [7, 2, 5];
for (var item of myArray) {
   console.log(item);
}
// 将变为
for (var _j = 0; _j < myArray.length; _j++) {
   var item = myArray[_j];
   console.log(item);
}
```

如上面的示例所示，使用 `for...of` 将使意图更清晰，并减少你编写的代码量，以及创建的变量数量。

### 局限性

对于那些目标不是 ES6 或以上版本的人，生成的代码将假设对象存在 `length` 属性，并且可以通过数字进行索引。这意味着在旧版 JS 引擎中，它仅支持数组和字符串。

如果 TypeScript 发现你既没有使用数组也没有使用字符串，你将得到一个错误。考虑下面提供的示例，它很好地描述了这一点：

```typescript
let artParagraphs = document.querySelectorAll("article > p");

// Error: Nodelist is not an array type or a string type

for (let par of artParagraphs) {
   par.classList.add("read");
}
```

从上面的演示可以清楚看出，`for…of` 应该只用于数组或字符串对象。

## 第 9 章 - 迭代器（Iterators）

迭代器（Iterator）是一种主要用于面向对象编程语言的特性。它是一个对象，用于实现以下类型的接口：

```typescript
interface Iterator<T> {
  next(value?: any): IteratorResult<T>;
  return?(value?: any): IteratorResult<T>;
  throw?(e?: any): IteratorResult<T>;
}
```

该接口允许我们从对象的集合或序列中检索特定值。想象一种情况：你有一个帧（frame）对象，它包含了我们的帧所包含的组件列表。通过迭代器接口，我们可以像下面的代码所示，从帧对象中检索组件：

```typescript
'use strict';

class Component {
  constructor (public name: string) {}
}

class Frame implements Iterator<Component> {
  private point = 0;
  constructor(public name: string, public components: Component[]) {}
  public next(): IteratorResult<Component> {
    if (this.point < this.components.length) {
      return {
        done: false,
        value: this.components[this.point++]
      }
    } else {
      return {
        done: true
      }
    }
  }
}

let fr = new Frame("Door", [new Component("top"), new Component("bottom"), new Component("left"), new Component("right")]);
let iteratorResult_1 = fr.next(); //{ done: false, value: Component { name: 'top' } }
let iteratorResult_2 = fr.next(); //{ done: false, value: Component { name: 'bottom' } }
let iteratorResult_3 = fr.next(); //{ done: false, value: Component { name: 'left' } }
let iteratorResult_4 = fr.next(); //{ done: false, value: Component { name: 'right' } }
let iteratorResult_5 = fr.next(); //{ done: true }

// 我们可以通过 value 属性来访问迭代结果的值：
let component = iteratorResult_1.value; //Component { name: 'top' }
```

你必须知道，迭代器本身并不是 TypeScript 的一项特性，这意味着代码在不显式实现迭代器和 `iteratorResult` 的情况下也可以运行。然而，为了代码的一致性，使用这些 ES6 接口特性对我们是有好处的。

考虑下面的代码，它展示了如何实现：

```typescript
class Frame implements Iterable<Component> {
  constructor(public name: string, public components: Component[]) {}
  [Symbol.iterator]() {
    let p = 0;
    let components = this.components;
    return {
      next(): IteratorResult<Component> {
        if (p < components.length) {
          return {
            done: false,
            value: components[p++]
          }
        } else {
          return {
            done: true
          }
        }
      }
    }
  }
}

let fr = new Frame("Door", [new Component("top"), new Component("bottom"), new Component("left"), new Component("right")]);
for (let cmp of frame) {
  console.log(cmp);
}
```

迭代器不能遍历一个有限的值。一个很好的例子是斐波那契数列。这在下面的代码中体现得最清楚：



```typescript
class Fibonacci implements IterableIterator<number> {
  protected fbn1 = 0;
  protected fbn2 = 1;
  constructor(protected maxValue?: number) {}
  public next(): IteratorResult<number> {
    let current = this.fbn1;
    this.fbn1 = this.fbn2;
    this.fbn2 = current + this.fbn1;
    if (this.maxValue && current <= this.maxValue) {
      return {
        done: false,
        value: current
      }
    }
    return {
      done: true
    }
  }
  [Symbol.iterator](): IterableIterator<number> {
    return this;
  }
}

let fib = new Fibonacci();
fib.next() // done: false, value: 0
fib.next() // done: false, value: 1
fib.next() // done: false, value: 1
fib.next() // done: false, value: 2
fib.next() // done: false, value: 3
let fibMax50 = new Fibonacci(50);
console.log(Array.from(fibMax50)); // [ 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ]
let fibMax21 = new Fibonacci(21);
for(let num of fibMax21) {
  console.log(num); //将打印 0 到 21 的斐波那契数列
}
```

## 第 11 章 - 展开运算符（Spread Operator）

该运算符用于展开数组对象。

### 应用（Apply）

该运算符用于将数组展开到函数参数中。过去，人们期望使用 `Function.prototype.apply` 函数。如下代码所示：

```javascript
function myFunction(a, b, c) { }
var args = [0, 1, 2];
myFunction.apply(null, args);
```

为了实现这一点，我们可以在参数前加上 `…`，如下所示：

```javascript
function myFunction(a, b, c) { }
var args = [0, 1, 2];
myFunction(...args);
```

### 解构（Destructuring）

你已经见过它如何在解构中被使用了，如下所示：

```javascript
var [a, b, ...remaining] = [1, 2, 3, 4];
console.log(a, b, remaining); // 1, 2, [3,4]
```

这种设计的初衷是为了让人们轻松捕获解构时剩余的数组元素。

### 数组赋值

展开运算符允许你将一个已经展开的数组放入另一个数组中。考虑下面的示例，它展示了如何实现这一点：

```javascript
var list = [5, 6];
list = [...list, 7, 8];
console.log(list); // [5,6,7,8]
```

## 第 12 章 - 枚举（Enums）

枚举为我们提供了一种组织具有相关值集合的方法。除了 JavaScript 之外，其他编程语言都提供了枚举数据类型。TypeScript 支持这一点。在 TypeScript 中，可以像下面所示声明枚举：

```typescript
enum Card {
   Clubs,
   Spades,
   Diamonds,
   Hearts
}

// 示例用法
var card = Card.Clubs;

// 安全性
card = "It is not a member of the card suit"; // 错误：string 无法赋值给类型 `CardSuit`
```

### 枚举与数字

TypeScript 中的枚举是基于数字的。这意味着我们可以为 TypeScript 中的枚举实例分配数字，这适用于任何与数字兼容的类型。下面的代码描述了如何实现这一点：

```typescript
enum Color {
   Red,
   Green,
   Blue
}

var color = Color.Red;
color = 0; // 这等于 Color.Red
```

### 枚举与字符串

我们想知道枚举生成的 JavaScript 是什么样的。考虑下面的 TypeScript 示例：

```typescript
enum MyEnum {
   False,
   True,
   Unknown
}
```

从上面的 TypeScript 代码将生成以下 JavaScript 代码：

```javascript
var MyEnum;
(function (MyEnum) {
   MyEnum [MyEnum ["False"] = 0] = "False";
   MyEnum [MyEnum ["True"] = 1] = "True";
   MyEnum [MyEnum ["Unknown"] = 2] = "Unknown";
})( MyEnum || (MyEnum = {}));
```

变量 `MyEnum` 可以用于将字符串版本的枚举转换为数字版本，或者将数字版本的枚举转换为字符串版本。下面的代码描述了这一点：

```typescript
enum MyEnum {
   False,
   True,
   Unknown
}

console.log(MyEnum [0]); // "False"
console.log(MyEnum ["False"]); // 0
console.log(MyEnum [MyEnum.False]); // "False" 因为 `MyEnum.False == 0`
```

我们也可以更改与枚举关联的数字。默认设置是枚举从 0 开始，随后每次递增 1。考虑下面的代码：

```typescript
enum Color {
   Red,      // 0
   Green,    // 1
   Blue      // 2
}
```

可以通过特定的赋值来更改特定枚举关联的数字。下面的示例从 3 开始，然后继续递增：

```typescript
enum Color {
   LightRed = 3,  // 3
   DarkGreen,     // 4
   LightBlue      // 5
}
```

你还需要知道枚举是开放的。考虑下面由枚举生成的 JavaScript 代码：

```javascript
var MyEnum;
(function (MyEnum) {
   MyEnum [MyEnum ["False"] = 0] = "False";
   MyEnum [MyEnum ["True"] = 1] = "True";
   MyEnum [MyEnum ["Unknown"] = 2] = "Unknown";
})( MyEnum || (MyEnum = {}));
```

枚举定义可以跨越多个文件。考虑下面的示例，其中我们展开了 `Color` 的定义以获取两个块：

```typescript
enum Color {
   Red,
   Green,
   Blue
}

enum Color {
   LightRed = 3,
   DarkGreen,
   LightBlue
}
```

### 作为标志（Flags）的枚举

标志为我们提供了使用枚举的卓越能力。考虑下面的示例：

```typescript
enum Animal {
   None            = 0,
   PossesClaws     = 1 << 0,
   Flying          = 1 << 1,
   ConsumesFish    = 1 << 2,
   Endangered      = 1 << 3
}
```

在上述情况下，我们需要通过移动 1 来获取位运算符。考虑下面的示例：

```typescript
enum Animal {
   None        = 0,
   PossesClaws = 1 << 0,
   Flies       = 1 << 1,
}

function printAbilities(animal) {
   var animFlags = animal.flags;
   if (animFlags & Animal.PossesClaws) {
      console.log('The animal has claws');
   }
   if (animFlags & Animal.Flies) {
      console.log('The animal can fly');
   }
   if (animFlags == Animal.None) {
      console.log('nothing');
   }
}

var animal = { flags: Animal.None };
printAbilities(animal); // nothing
animal.flags |= Animal.PossesClaws;
printAbilities(animal); // The animal has claws
animal.flags &= ~Animal.PossesClaws;
printAbilities(animal); // The animal has claws
```

The spread operator can allow you to place an array which has been expanded into another array. Consider the example given below, which demonstrates how this can be done:

```javascript
var list = [5, 6];
list = [...list, 7, 8];
console.log(list); // [5,6,7,8]
```

# Chapter 12 - Enums

An enum provides us with a way to organize collections having related values. Other programming languages provide us with an enum data type except JavaScript. This is supported in TypeScript. In TypeScript, an enum can be declared as shown below:

```typescript
enum Card {
   Clubs,
   Spades,
   Diamonds,
   Hearts
}

// A sample usage
var card = Card.Clubs;

// Safety
card = "It is not a member of the card suit"; // Error: string is not assignable to type `CardSuit`
```

### Enums and Numbers

Enums in TypeScript are number-based. This indicates that we can assign numbers to an instance of an enum in TypeScript. The same applies to any type that is compatible with numbers. The code below describes how this can be done:

```typescript
enum Color {
   Red,
   Green,
   Blue
}

var color = Color.Red;
color = 0; // This is the same as Color.Red
```

### Enums and Strings

We want to know what kind of JavaScript is produced by enums. Consider the following TypeScript example:

```typescript
enum MyEnum {
   False,
   True,
   Unknown
}
```

The following JavaScript code will be generated from the TypeScript code above:

```javascript
var MyEnum;
(function (MyEnum) {
   MyEnum [MyEnum ["False"] = 0] = "False";
   MyEnum [MyEnum ["True"] = 1] = "True";
   MyEnum [MyEnum ["Unknown"] = 2] = "Unknown";
})( MyEnum || (MyEnum = {}));
```

The variable `MyEnum` can be used to convert a string version of an enum into a number, or a number version of an enum into a string. The following code describes this:

```typescript
enum MyEnum {
   False,
   True,
   Unknown
}

console.log(MyEnum [0]); // "False"
console.log(MyEnum ["False"]); // 0
console.log(MyEnum [MyEnum.False]); // "False" because `MyEnum.False == 0`
```

It is also possible to change the number associated with an enum. The default setting is that enums start at 0, and each subsequent increment is automatically made in intervals of 1. Consider the following code:

```typescript
enum Color {
   Red,      // 0
   Green,    // 1
   Blue      // 2
}
```

The number associated with a specific enum can be automatically changed by assigning a value to it. The following example starts at 3 and then increments from there:

```typescript
enum Color {
   LightRed = 3,  // 3
   DarkGreen,     // 4
   LightBlue      // 5
}
```

You also have to know that enums are open-ended. Consider the following JavaScript code generated from an enum:

```javascript
var MyEnum;
(function (MyEnum) {
   MyEnum [MyEnum ["False"] = 0] = "False";
   MyEnum [MyEnum ["True"] = 1] = "True";
   MyEnum [MyEnum ["Unknown"] = 2] = "Unknown";
})( MyEnum || (MyEnum = {}));
```



枚举定义可以分布在多个文件中。下面的示例将`Color`的定义拆分为两个代码块：

```typescript
enum Color {
   Red,
   Green,
   Blue
}

enum Color {
   LightRed = 3,
   DarkGreen,
   LightBlue
}
```

### 将枚举用作标志

标志为使用枚举提供了出色的能力。请看下面的示例：

```typescript
enum Animal {
   None            = 0,
   PossesClaws      = 1 << 0,
   Flying          = 1 << 1,
   ConsumesFish    = 1 << 2,
   Endangered      = 1 << 3
}
```

在上面的示例中，我们需要通过移动`1`的位置来获取位运算符。请看下面的示例：

```typescript
enum Animal {
   None            = 0,
   PossesClaws      = 1 << 0,
   Flies           = 1 << 1,
}

function printAbilities(animal) {
   var animFlags = animal.flags;
   if (animFlags & Animal.PossesClaws) {
      console.log('The animal has claws');
   }
   if (animFlags & Animal.Flies) {
      console.log('The animal can fly');
   }
   if (animFlags == Animal.None) {
      console.log('nothing');
   }
}

var animal = { flags: Animal.None };
printAbilities(animal); // nothing
animal.flags |= Animal.PossesClaws;
printAbilities(animal); // The animal has claws
animal.flags &= ~Animal.PossesClaws;
printAbilities(animal); // The animal has claws
```

然而，如果变量名已经被周围的作用域占用，则会生成一个新的变量名，如下方的代码所示：

```javascript
var myVar = '123';

if (true) {
    let myVar = 123;
}

// will become //

var myVar = '123';

if (true) {
    var _myVar = 123; // 它已经被重命名了
}
```

### `let`闭包

考虑下面这段简单的 JavaScript 代码：

```javascript
var functions = [];

// 创建一组函数
for (var j = 0; j < 3; j++) {
    functions.push(function() {
        console.log(j);
    })
}

// 调用它们
for (var k = 0; k < 3; k++) {
    functions[k]();
}
```

在大多数面试题中，你会被问到上述 JavaScript 文件中的日志输出。尽管大多数人期望答案是`0, 2, 3`，但真正的答案是`3`。原因是这三个函数都使用了外部作用域中的变量`j`，而当我们执行它们时，变量`j`的值将是`3`。这构成了第一个循环的终止条件。

解决这个问题的方法是为每次迭代创建一个变量，并且该变量应该专门用于对应循环中的迭代。如你所知，可以通过创建一个新函数并立即执行它来为变量创建一个新的作用域。代码如下：

```javascript
var functions = [];

// 创建一组函数
for (var j = 0; j < 3; j++) {
    (function() {
        var local = j;
        functions.push(function() {
            console.log(local);
        })
    })();
}

// 调用它们
for (var k = 0; k < 3; k++) {
    funcs[k]();
}
```

一旦使用`let`关键字而不是`var`关键字，就会为每次循环迭代创建一个唯一的变量。

## 结论

我们已经得出了本指南的结论。`TypeScript`是一种始终编译为 JavaScript 的编程语言。该语言是开源的，由微软开发和维护。它非常适合支持静态类型和面向对象编程等特性的应用开发。这两个特性是使其适用于开发大型应用程序的主要特征。

该语言支持类型注解，这对于维护程序中的缩进非常有帮助。缩进通常能确保程序具有良好的可读性。你需要记住，`TypeScript`是`JavaScript`的超集，这意味着任何`JavaScript`代码也是`TypeScript`代码。这就是为什么`TypeScript`始终编译为`JavaScript`的原因。要开始使用`TypeScript`编程，你必须先准备好环境。对于 Windows 用户，你只需要安装 Visual Studio，然后下载并安装必要的插件就可以开始编程了。

如果你在使用任何其他平台，则需要依赖名为`npm`的 Node 包。确保你已经有一个文本编辑器和浏览器。一旦你安装了`TypeScript`的`npm`包，就可以开始编写你的`TypeScript`程序了。
