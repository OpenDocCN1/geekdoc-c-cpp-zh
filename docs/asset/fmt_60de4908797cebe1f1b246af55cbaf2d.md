
## JavaScript 数字

对于那些熟悉其他语言中双精度（`doubles`）/浮点数（`float`）的人来说，需要知道 JavaScript 的浮点数存在精度问题。

```javascript
0.1 + 0.2 // 0.30000000000000004
```

使用 `big.js` 来解决这个问题。

JavaScript 的安全整数范围是 `Number.MAX_SAFE_INTEGER`。

```javascript
Number.MAX_SAFE_INTEGER // 900719925474091
```

以下是关于 JavaScript 数字的你应该注意的关键信息。

JavaScript 只有一种数字类型。它是一个双精度 64 位数字（`Number`）。下面讨论它的局限性以及推荐的解决方案。

对于那些熟悉其他语言中双精度（`doubles`）/浮点数（`float`）的人来说，需要知道 JavaScript 的浮点数存在精度问题。

```javascript
0.1 + 0.2 // 0.30000000000000004
```

使用 `big.js` 来解决这个问题。

JavaScript 的安全整数范围是 `Number.MAX_SAFE_INTEGER`。

```javascript
Number.MAX_SAFE_INTEGER // 900719925474091
```

对于超出安全范围的整数，计算可能会丢失精度：

```javascript
Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2 // false
```

```javascript
console.log(Number.MAX_SAFE_INTEGER + 1); // 900719925474092
console.log(Number.MAX_SAFE_INTEGER + 2); // 900719925474092
```

使用 `big.js` 用于财务计算（例如金额）。

安装非常简单：

```bash
npm install big.js
```

快速使用示例：

```javascript
import { Big } from 'big.js';

const foo = new Big('1.1111111111111111');
const bar = foo.plus('0.1111111111111111');

console.log(bar.toString()); // 1.2222222222222222
```

```javascript
import * as deepEqual from "deep-equal";
console.log(deepEqual({a:123},{a:123})); // True
```

除了字面量外，JavaScript 中的任何对象（包括函数、数组、正则等）都是引用。这意味着以下几点：

```javascript
var foo = {};
var bar = foo; // bar 是同一个对象的引用

foo.baz = 123;
console.log(bar.baz); // 123
```

```javascript
var foo = {};
var bar = foo; // bar 是一个引用
var baz = {}; // baz 是一个不同于 `foo` 的“新对象”

console.log(foo === bar); // true
console.log(foo === baz); // false
```

事实是，你需要处理这二者。只需用 `==` 检查其中之一即可。

```javascript
// 假设你正在执行 `foo.bar == undefined`，其中 bar 可能是以下之一：
console.log(undefined == undefined); // true
console.log(null == undefined); // true
console.log(@ == undefined); // false
console.log('\' == undefined); // false
console.log(false == undefined); // false
```

推荐使用 `== null` 来检查 `undefined` 或 `null`。你通常并不想区分这二者。

```typescript
function foo(arg: string | null | undefined) {
  if (arg != null) {
    // arg 必须是字符串，因为 `!=` 规则排除了 null 和 undefined。
  }
}
```

记得我应该教你如何使用 `== null` 吗？当然，你要这样做（因为我刚说了 ^）。

不要将其用于根层级的东西。在严格模式（`strict mode`）下，如果你使用 `foo` 且它是 `undefined`，你会得到一个 `ReferenceError` 异常，整个调用栈都会回溯。

所以，要在全局层级检查变量是否已定义，通常使用 `typeof`：

```javascript
if (typeof someglobal !== 'undefined') {
  // someglobal 现在可以安全使用了
  console.log(someglobal);
}
```

在函数内部对 `this` 关键字的任何访问实际上取决于函数是如何被调用的。这通常被称为“调用上下文”（`calling context`）。

这是一个示例：

```javascript
function foo() {
  console.log(this);
}

foo(); // 打印全局对象，例如浏览器中的 `window`
let bar = {
  foo
}
bar.foo(); // 打印 `bar`，因为 `foo` 是在 `bar` 上被调用的
```

所以请注意你对 `this` 的使用。如果你想断开类中 `this` 与调用上下文的连接，请使用箭头函数（`arrow function`），稍后会介绍。

JavaScript 有的最棒的特性就是闭包。JavaScript 中的函数可以访问在外部作用域定义的任何变量。用示例解释闭包是最好的：

```javascript
function outerFunction(arg) {
  var variableInOuterFunction = arg;

  function bar() {
    console.log(variableInOuterFunction); // 访问外部作用域的变量
  }

  // 调用本地函数以证明它有访问 arg 的权限
  bar();
}

outerFunction("hello closure"); // 打印 hello closure!
```

你可以看到内部函数可以访问外部作用域的变量（`variableInOuterFunction`）。外部函数中的变量被内部函数捕获（或绑定）了。这里使用的术语是 **闭包**（`closure`）。这个概念本身足够简单且直观。

现在是很棒的部分：**即使在外部函数返回后，内部函数仍然可以访问外部作用域的变量**。这是因为变量仍然绑定在内部函数中，而不依赖于外部函数。再次看一个示例：

```javascript
function outerFunction(arg) {
  var variableInOuterFunction = arg;
  return function() {
    console.log(variableInOuterFunction);
  }
}
```

var innerFunction = outerFunction("hello closure!");

```javascript
// 注意 outerFunction 已经返回
innerFunction(); // 打印 closure!
```

### 为什么它很棒

```javascript
function createCounter() {
  let val = 0;
  return {
    increment() { val++ },
    getVal() { return val }
  }
}
```

```javascript
let counter = createCounter();
counter.increment();
console.log(counter.getVal()); // 1
counter.increment();
console.log(counter.getVal()); // 2
```

在高级层面上，这也是让像 Node.js 这样的成为可能的原因（如果你现在脑子里还没转通，不用担心。它会会的）：

```javascript
// 说明该概念的伪代码
server.on(function(req, res) {
  loadData(req.id).then(function(data) {
    // 'res' 已被闭包并在之后可用
    res.send(data);
  });
});
```

在任何编程语言中处理数字时，你都需要意识到该语言处理数字的特殊性。以下是关于 JavaScript 数字的你应该注意的关键信息。

JavaScript 只有一种数字类型。它是一个双精度 64 位数字（`Number`）。下面讨论它的局限性以及推荐的解决方案。

对于那些熟悉其他语言中双精度（`doubles`）/浮点数（`float`）的人来说，需要知道 JavaScript 的浮点数存在精度问题。

```javascript
0.1 + 0.2 // 0.30000000000000004
```

使用 `big.js` 来解决这个问题。

JavaScript 的安全整数范围是 `Number.MAX_SAFE_INTEGER`。

```javascript
Number.MAX_SAFE_INTEGER // 900719925474091
```

对于超出安全范围的整数，计算可能会丢失精度：

```javascript
Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2 // false
```

```javascript
console.log(Number.MAX_SAFE_INTEGER + 1); // 900719925474092
console.log(Number.MAX_SAFE_INTEGER + 2); // 900719925474092
```

使用 `big.js` 用于财务计算（例如金额）。

安装非常简单：

```bash
npm install big.js
```

快速使用示例：

```javascript
import { Big } from 'big.js';

const foo = new Big('1.1111111111111111');
const bar = foo.plus('0.1111111111111111');

console.log(bar.toString()); // 1.2222222222222222
```

你可以手动使用这些 Infinity 值，或者像下面所示通过 `Number` 类的静态成员来使用：

```javascript
console.log(Number.POSITIVE_INFINITY === Infinity); // true
console.log(Number.NEGATIVE_INFINITY === -Infinity); // true
```

幸运的是，比较运算符 (`<` / `>`) 在无穷值上的工作是可靠的：

```javascript
console.log(Infinity > 1); // true
console.log(-Infinity < -1); // true
```

`Number` 可以的最小非零值通过静态 `Number.MIN_VALUE` 提供：

```javascript
console.log(Number.MIN_VALUE); // 5e-324
```

比 `MIN_VALUE` 更小的值（“下溢值”）会被转换为 0。

```javascript
console.log(Number.MIN_VALUE / 10); // 0
```

> 进一步的直觉：就像大于 `Number.MAX_VALUE` 的值会被限制为 `INFINITY` 一样，小于 `Number.MIN_VALUE` 的值会被限制为 0。

TypeScript 的主要卖点之一是它允许你在当前的（ES3 和 ES5 级别的）JavaScript 引擎（如当前的浏览器和 Node.js）中使用 ES6 及更高版本的特性。在这里深入探讨为什么这些特性有用，以及这些特性在 TypeScript 中是如何实现的。

注意：并不是所有这些特性都计划立即添加到 JavaScript 中，但它们为你的代码组织和维护提供了巨大的实用性。另外注意，你可以自由忽略任何对你的项目没有意义的结构，尽管你最终会使用其中大部分的 ;)

在 JavaScript 中将类作为一等公民项之所以重要，是因为：

- 1. 类提供了一种实用的结构抽象。
- 2. 为开发者提供了一种统一的方式来使用类，而不是让每个框架（`emberjs`, `reactjs` 等）都搞自己的版本。
- 3. 面向对象的 JavaScript 开发者已经熟悉类了。

最后，JavaScript 开发者可以使用 `class`。这里我们有一个名为 `Point` 的基础类：

```typescript
class Point {
  x: number;
  y: number;
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
  add(point: Point) {
    return new Point(this.x + point.x, this.y + point.y);
  }
}

var p1 = new Point(0, 10);
var p2 = new Point(10, 20);
var p3 = p1.add(p2); // {x:10,y:30}
```

这个 `Point` 类在生成 ES5 输出时会生成以下 JavaScript：

```javascript
var Point = (function () {
  function Point(x, y) {
    this.x = x;
    this.y = y;
  }
  Point.prototype.add = function (point) {
    return new Point(this.x + point.x, this.y + point.y);
  };
  return Point;
})();
```

作为一种一等语言结构，这现在是一种相当符合传统的传统的 JavaScript 类模式。

TypeScript 中的类（与其他语言一样）支持使用 `extends` 关键字进行单继承，如下所示：

```typescript
class Point3D extends Point {
  z: number;
  constructor(x: number, y: number, z: number) {
    super(x, y);
    this.z = z;
  }
  add(point: Point3D) {
    var point2D = super.add(point);
    return new Point3D(point2D.x, point2D.y, this.z + point.z);
  }
}
```

如果你在类中有一个构造函数，你必须在构造函数中调用父类构造函数（TypeScript 会向你指出这一点）。这确保了需要设置的内容被设置。在调用 `super` 之后，你可以在构造函数中添加任何你想做的额外操作（在这里我们添加了另一个成员 `z`）。

注意你可以轻松地重写父类成员函数（这里我们重写了 `add`），并在成员函数中使用父类的功能（使用 `super` 语法）。

TypeScript 类支持由类的所有实例共享的静态属性。放置（以及访问）这些内容的自然地方是类本身，下面是 TypeScript 的实现方式：

```typescript
class Something {
  static instances = 0;
  constructor() {
    Something.instances++;
  }
}
```

```javascript
var s1 = new Something();
var s2 = new Something();
console.log(Something.instances); // 2
```

你可以拥有静态成员也可以拥有静态函数。

## 访问修饰符 (Access Modifiers)

TypeScript 支持 `public`、`private` 和 `protected` 访问修饰符，它们决定了类成员的可访问性，如下所示：

| 位置 | public | protected | private |
| --- | --- | --- | --- |
| 类 | yes | yes | yes |
| 类子类 | yes | yes | no |
| 类实例 | yes | no | no |

如果没有指定访问修饰符，它默认是 `public`，这符合 JavaScript 的便利性。
注意在运行时（在生成的 JS 中）这些是没有意义的，但如果你错误地使用它们，将给你产生编译时错误。下面展示了每个的示例：

```typescript
class FooBase {

  public x: number;

  private y: number;

  protected z: number;

}

// 对实例的影响

var foo = new FooBase();

foo.x; // okay

foo.y; // ERROR : private

foo.z; // ERROR : protected
```
