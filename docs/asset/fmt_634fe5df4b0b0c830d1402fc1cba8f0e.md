
我们已经看到如何在 ECMAScript 中定义构造函数，以及如何向对象添加成员变量。通常，我们还想定义成员函数。因为函数在 ECMAScript 中被视为一等公民，所以这似乎变得非常容易。

来自 `arguments` 数组：

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

`arguments` 数组可以根据参数的类型或数量来重载函数的行为。例如，假设我们让 `sum()` 接收一个可选的一元参数，后面跟着一个数字列表，允许我们如下所示调用它：

```javascript
print(sum(1, 2, 3, 4, 5, 6));
print(sum(square, 1, 2, 3, 4, 5, 6));
```

以下是我们可以实现 `sum()` 以支持这种方式：

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

如果我们提供一个函数作为第一个参数，该函数将被应用于每个数字加到求和之前；否则，我们使用恒等函数 `function(x) { return x; }`。

对于 C++ 程序员来说，ECMAScript 最难以接受的方面可能是它与 C++、`C#`、`Java`、`Simula` 和 `Smalltalk` 不同，这些都是基于类的。ECMAScript 并没有提供类概念，而是提供了更底层的机制，让我们能够实现相同的的结果。

让我们在 ECMAScript 中实现类的第一个机制是构造函数。构造函数是一个可以使用 `new` 操作符调用的函数。例如，我们有一个用于 `Shape` 对象的构造函数：

```javascript
function Shape(x, y) {
  this.x = x;
  this.y = y;
}
```

`Shape` 构造函数有两个参数，并根据传递给构造函数的值初始化新对象的 `x` 和 `y` 属性（成员变量）。`this` 关键字指向正在被创建的对象。在 ECMAScript 中，对象本质上是属性的集合；属性可以任何时候添加、删除或修改。属性在第一次被设置时创建，当我们在构造函数中为 `this.x` 和 `this.y` 赋值时，`x` 和 `y` 属性就因此创建了。

C++ 和 Java 开发者的一个常见错误是在访问对象属性时忘记使用 `this` 关键字。在前面的示例中，这不太可能发生，因为像 `x = x` 这样的语句看起来非常可疑，但在其他示例中，这将导致创建意外的全局变量。

要实例化一个 `Shape`，我们如下使用 `new` 操作符：

```javascript
var shape = new Shape(10, 20);
```

如果我们对 `shape` 变量使用 `typeof` 操作符，我们得到的类型类型是 `Object` 而不是 `Shape`。如果我们想判断一个对象是否是使用 `Shape` 构造函数创建的，我们可以使用 `instanceof` 操作符：

```javascript
var array = new Array(100);
array instanceof Shape;      // 返回 false
```

```javascript
var shape = new Shape(10, 20);
shape instanceof Shape;      // 返回 true
```

ECMAScript 不会执行任何函数作为构造函数的服务。然而，如果该对象不是函数，那么将其作为构造函数调用是没有意义的。相反，构造函数可以作为普通函数调用，但这也很少有意义。ECMAScript 提供了内置构造函数，让我们能够实例化基础对象类型，特别是 `Array`、`Date` 和 `RegExp`。其他构造函数转换原始数据类型，允许我们创建存储原始值的对象。使用 `valueOf()` 成员函数可以让我们检索到存储在对象中的原始值。例如：

```javascript
var boolObj = new Boolean(true);
typeof boolObj; // 返回 "object"

var boolVal = boolObj.valueOf();
typeof boolVal; // 返回 "boolean"
```

# 图 22.1. 全局对象的内置属性

| 常量 | 描述 |
| :--- | :--- |
| `NaN` | IEEE 754 非数字 (NaN) 值 |
| `Infinity` | 正无穷大 (+∞) |
| `undefined` | 未初始化变量的默认值 |

| 函数 | 描述 |
| :--- | :--- |
| `print(x)` | 在控制台上打印值 |
| `eval(str)` | 执行 ECMAScript 程序 |
| `parseInt(str, base)` | 将字符串转换为整数 |
| `parseFloat(str)` | 将字符串转换为浮点数 |
| `isNaN(n)` | 如果 n 是 NaN 则返回 true |
| `isFinite(n)` | 如果 n 是除 NaN、+∞ 或 -∞ 以外的数字，则返回 true |
| `decodeURI(str)` | 将 8 位编码的 URI 转换为 Unicode |
| `decodeURIComponent(str)` | 将 8 位编码的组件转换为 Unicode |
| `encodeURI(str)` | 将 Unicode URI 转换为 8 位编码 |
| `encodeURIComponent(str)` | 将 Unicode 组件转换为 ECMAScript 标准指定的 8 位编码 |

| 类 (构造函数) | 描述 |
| :--- | :--- |
| `Object` | 提供所有对象通用的功能 |
| `Function` | 封装一个 ECMAScript 函数 |
| `Array` | 表示可伸缩的项向量 |
| `String` | 存储 Unicode 字符串 |
| `Boolean` | 存储布尔值 (true 或 false) |
| `Number` | 存储浮点数 |
| `Date` | 存储日期和时间 |
| `RegExp` | 提供正则表达式匹配 |
| `Error` | 错误类型的基类型 |
| `EvalError` | 错误使用 eval() 时抛出 |
| `RangeError` | 数值超出合法范围时抛出 |
| `ReferenceError` | 尝试访问未定义变量时抛出 |
| `SyntaxError` | 被 eval() 检测到语法错误时抛出 |
| `TypeError` | 当参数类型错误时抛出 |
| `URIError` | 解析失败时抛出 |
| `Math` | 提供数学常量和函数 |

我们已经看到如何在 ECMAScript 中定义构造函数，以及如何向对象添加成员变量。通常，我们还想定义成员函数。因为函数在 ECMAScript 中被视为一等公民，所以这似乎变得非常容易。这里有一个新版本的 Shape 构造函数，包含了成员函数：

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

通过这种方法，每个 Shape 实例都有自己的 manPos 和 translate 属性。这些属性对于所有 Shape 实例应该是相同的；因此最好只存储一次，而不是在每个实例中。ECMAScript 通过使用原型来实现这一点。原型是一个作为其他对象的回退的对象，提供了一组初始属性。这种方法的一个优势是可以随时更改原型对象，更改会立即反映在所有使用该原型创建的对象中。

```javascript
var shape = new Shape(10, 20);
shape.translate(100, 100);
print(shape.x + ", " + shape.y + " (" + shape.hattanPos() + ")");
```

在基于类的语言（如 C++ 和 Java）中，我们可以使用类继承来创建特殊对象。例如，我们会定义一个 Shape 类并派生 Triangle、Square 和 Circle。在 ECMAScript 中，可以使用原型实现类似的效果。以下示例展示了如何定义既是 Shape 实例又是 Circle 对象：

```javascript
Shape.prototype.area = function() { return 0 };

function Circle(x, y, radius) {
  Shape.call(this, x, y);
  this.radius = radius;
}

Circle.prototype = new Shape();
Circle.prototype.area = function() {
  return Math.PI * this.radius;
};
```

我们首先定义一个 `Shape` 构造函数并与其关联一个 `area()` 函数，该函数始终返回 0。然后我们定义一个 `Circle` 构造函数，它使用所有函数对象（包括构造函数）定义的 `call()` 函数调用基类构造函数，并添加了 `radius` 属性。在构造函数外部，我们将 `Circle` 的原型设置为 `Shape` 对象，并用 `Circle` 特有的实现覆盖了 `Shape` 的 `area()` 函数。这于于 C++ 代码：

代码视图：

```cpp
class Shape {
public:
  Shape(double x, double y) {
    this->x = x;
    this->y = y;
  }

  virtual double area() const { return 0; }

  double x;
  double y;
};

class Circle : public Shape {
public:
  Circle(double x, double y, double radius)
    : Shape(x, y) {
    this->radius = radius;
  }

  double area() const { return M_PI * radius * radius; }

  double radius;
};
```

`instanceof` 运算符通过遍历原型链来确定调用了哪些构造函数。结果是，子类的实例也被认为是基类的实例：

```javascript
var circle = new Circle(0, 0, 50);
circle instanceof Circle; // 返回 true
circle instanceof Shape; // 返回 true
circle instanceof Object; // 返回 true
circle instanceof Array; // 返回 false
```

到此我们对 ECMAScript 的简要介绍就结束。在接下来的章节中，我们将展示如何将这种语言与 C++/Qt 应用结合使用，为终端用户提供更多的灵活性和定制性，或者仅仅是为了加速开发过程。

## 2. 应用脚本

- ECMAScript 语言概述
- 使用脚本扩展 Qt 应用
- 使用脚本实现 GUI 扩展
- 通过脚本实现自动化

脚本是用解释型语言编写的程序，用于扩展现有系统的功能。某些脚本作为独立应用程序运行，而另一些则嵌入应用程序中执行。Qt 包含了 QtScript，该模块可以使用 ECMAScript（JavaScript 的标准版本）使 Qt 应用脚本化。该模块是对早期 Trolltech Qt Script for Applications (QSA) 的完全重写，并对 ECMAScript 第 3 版提供了完全支持。

ECMAScript 是 Ecma International 标准化的官方名称。它是 JavaScript (Mozilla)、JScript (Microsoft) 和 ActionScript (Adobe) 的基础。尽管该语言的语法在表面与 C++ 和 Java 相似，但底层概念有着本质区别，使其与其他大多数面向对象的编程语言区分开来。在本章的第一节中，我们将快速回顾 ECMAScript 语言，并展示如何使用 Qt 运行 ECMAScript 代码。如果你已经熟悉 JavaScript 或任何其他基于 ECMAScript 的语言，可以直接跳过本节。

在第二节中，我们将看到如何为 Qt 应用添加脚本支持。这使得用户能够在应用程序已提供的功能之外添加自己的功能。这种方法也经常用于更方便用户支持；技术人员可以通过脚本的形式提供错误修复程序和解决方案。

在第三节中，我们将展示如何开发使用 Qt Designer 创建的 GUI 前端和表。这种技术对于不喜欢与 C++ 开发相关的“编译、链接、运行”循环并偏好脚本方法的开发者来说非常有吸引力。它还让具有 JavaScript 经验的用户设计完全功能的 GUI 界面，无需学习 C++。

在最后一节中，我们将展示如何开发依赖 C++ 组件作为处理部分的脚本。这可以使用任意 C++ 和 C++/Qt 组件完成，这些组件不需要为了脚本化而专门设计。当多个程序需要使用相同的基础组件编写时，或者当我们希望让非 C++ 程序员能够使用 C++ 功能时，这种方法特别有用。

### ECMAScript 语言概述

本节对 ECMAScript 语言进行了简要介绍，以便你理解本章其他部分的代码片段，并开始编写自己的脚本。Mozilla 基金的网站 http://developer.mozilla.org/en/docs/Core_JavaScript_1.5_Guide 提供了更完整的教程，David Flanagan 的《JavaScript: The Definitive Guide》(O'Reilly, 2006) 也既作为教程也作为参考资料。官方 ECMAScript 规范在线地址为 http://www.ecmainternational.org/publications/standards/Ecma-262。

ECMAScript 定义了五种原始类型：Undefined、Null、Boolean、Number 和 String。Undefined 和 Null 分别是未定义和空的特殊类型。Boolean 类型包含两个值：true 和 false。Number 类型存储浮点数。String 类型存储 Unicode 字符串。变量还可以存储对象和函数，对应于 Object 和 Function 数据类型。例如：

```javascript
var x = new Array(10); // 返回 "object"
typeof x;
x = print; // 返回 "function"
typeof x;
```

`typeof` 运算符返回与变量关联的数据类型的小写字符串表示。与 Java 类似，ECMAScript 区分了原始类型和对象类型。原始类型的行为类似于 C++ 的值类型（如 int 和 QString），它们在不使用 `new` 运算符的情况下创建，并按值复制。相比之下，对象类型必须使用 `new` 运算符创建，且这些类型的变量只存储指向对象的引用（指针）。使用 `new` 分配对象时，我们不需要担心释放它们的内存，因为垃圾回收器会自动完成工作。

如果在不使用 `var` 关键字声明变量的情况下给变量赋值，该变量将作为全局变量创建。如果我们尝试读取不存在的变量的值，将得到 ReferenceError 异常。我们可以使用 `try...catch` 语句捕获异常，如下：

```javascript
try {
  print(y);
} catch (e) {
  print(e.name + ": " + e.message);
}
```

如果变量 y 不存在，控制台将打印消息 "ReferenceError: y is not defined"。
