
```cpp
if (effect == "Plain") {
  painter.setPen(Qt::NoPen);
} else if (effect == "Outline") {
  QPen pen(Qt::black);
  pen.setWidthF(2.5);
  painter.setPen(pen);
} else if (effect == "Shadow") {
  QPainter path(Qt::darkGray);
  painter.setBrush(brush);
  path.addText((size.width() - metrics.width(text)) / 2 + 3,
  (size.height() - metrics.descent()) + 3, myFont,
  text);
  painter.drawPath(path);
  painter.setBrush(brush);
}
```

对于 `Plain` 效果，不需要轮廓。对于 `Outline` 效果，我们忽略原始画笔，并创建了一个宽度为 2.5 像素的自定义黑色画笔。对于 `Shadow` 效果，我们需要先画阴影，这样文本就可以画在上面。

```cpp
QPainterPath path;
path.addText((size.width() - metrics.width(text)) / 2,
              size.height()) - metrics.descent(), myFont, text);
    painter.drawPath(path);

    return pixmap;
}
```

现在我们已经为每个文本效果正确设置了画笔和画刷，在 `Shadow` 效果情况下我们已经画好了阴影。我们现在准备好渲染文本了。文本水平居中，并且绘制在距离 `pixmap` 底部足够的位置，为下降字母（descenders）留出空间。

```cpp
Q_EXPORT_PLUGIN2(basiceffectplugin, BasicEffectsPlugin)
```

在 `.cpp` 文件的末尾，我们使用 `Q_EXPORT_PLUGIN2()` 宏让插件对 Qt 可用。

`.pro` 文件与我们在本章之前用于青铜风格插件的使用的类似（第 493 页）：

```
TEMPLATE = lib
CONFIG += plugin
HEADERS = ../textart/textartinterface.h \
    basiceffectsplugin.h
SOURCES = basiceffectsplugin.cpp
DESTDIR = ../textart/plugins
```

如果本节激发了你对应用程序插件的兴趣，你可能会喜欢提供的 Plug & Paint 示例。该应用程序支持三种不同的接口，并包含一个列出可用插件和接口的有用插件对话框。

# 2 应用程序脚本

![](img/5a24abdf0b0d58fa99d30abb4463611_834_0.png)

语言概述

- 使用脚本扩展 Qt
- 使用脚本实现 GUI

脚本是用解释型语言编写的程序，用于扩展现有系统的功能。某些脚本作为独立程序运行，而另一些则嵌入应用程序中执行。从 4.3 版本开始，Qt 包含了 `QtScript` 模块，它可以使用 ECMAScript（JavaScript 的标准化版本）来使 Qt 应用程序可脚本化。

在本章的第一节中，我们将快速回顾 ECMAScript 语言，并展示如何使用 Qt 运行 ECMAScript 代码。如果你已经熟悉 JavaScript 或任何其他基于 ECMAScript 的语言，可以直接跳过本节。

在第二节中，我们将介绍如何为 Qt 应用程序添加脚本支持。这使得用户能够在应用程序现有功能之外添加自己的功能。这种方法也经常用于便于支持用户；技术人员可以以脚本的形式提供错误修复和解决方案。

在第三节中，我们将展示如何通过结合 ECMAScript 代码和使用 `Qt Designer` 创建的表单来开发 GUI 前端。这种技术对于不喜欢 C++ 相关的“编译、链接、运行”循环的开发者来说非常有吸引力。它还让具有 JavaScript 经验的用户无需学习 C++ 就能设计功能完整的 GUI 界面。

在上一节中，我们将展示如何开发依赖 C++ 组件作为其处理部分的脚本。这可以使用任意的 C++ 和 C++/Qt 组件来实现，这些组件不需要在设计时考虑可脚本性。这种方法在多个程序需要使用相同的基础组件编写时，或者当我们希望让非 C++ 程序员也能使用 C++ 功能时，显得尤为有用。

## ECMAScript 语言概述

本节对 ECMAScript 语言进行简要介绍，以便你理解本章节后续介绍的代码段，并开始编写自己的脚本。Mozilla 基金会网站提供了更完整的教程：

http://developer.mozilla.org/en/docs/Core_JavaScript_1_5_Guide，此外推荐 David Flanagan 的《JavaScript: The Definitive Guide》(O'Reilly, 2006)，既可以作为教程，也可以作为参考资料。官方的 ECMAScript 规范在线位于：

http://www.ecmainternational.org/publications/standards/Ecma-262.htm。

基础的 ECMAScript 控制结构——`if` 语句、`for` 循环和 `while` 循环与 C++ 和 Java 相同。ECMAScript 还提供了或多或相同的赋值、关系和算术运算符。ECMAScript 字符串支持使用 `+` 进行拼接以及使用 `+=` 进行追加。

为了感受 ECMAScript 的语法，我们将从学习以下程序开始，该程序会打印小于 1000 的所有质数的列表：

```
const MAX = 1000;
var isPrime = new Array(MAX);

for (var i = 2; i < MAX; ++i)
  isPrime[i] = true;

for (var i = 2; i < MAX; ++i) {
  if (isPrime[i]) {
    for (var j = i; j < MAX; ++j)
      isPrime[i * j] = false;
  }
}

for (var i = 2; i < MAX; ++i) {
  if (isPrime[i])
    print(i);
};
```

从 C++ 程序员的角度来看，ECMAScript 最显著的特征可能是变量没有显式类型；声明变量只需要 `var` 关键字。只读变量使用 `const` 声明，而不是 `main()` 函数。前一个程序的另一个值得注意的特征是，位于任何函数之外的代码会立即执行，从文件顶部开始一直运行到底部。

与 C++ 不同，语句末尾的分号在 ECMAScript 中通常是可选的。通过简单的规则，解释器可以自己插入遗漏的分号。尽管如此，我们仍建议自己手动使用分号，以避免不悦的意外。

要运行上述内容，我们可以使用 Qt 的 `examples/script/qscript` 目录下的 `qscript` 解释器。如果用文件名作为命令行参数调用解释器，则该文件被视为 ECMAScript 并执行；否则，将启动交互式会话。

如果在使用 `var` 声明变量时不提供初始值，则默认值为 `undefined`，这是一个类型为 `Undefined` 的特殊值。我们稍后后可以使用赋值运算符 (`=`) 为变量分配任何类型的值。考虑以下示例：

```
var x;
typeof x; // 返回 "undefined"

x = null;
typeof x; // 返回 "null"

x = true;
typeof x; // 返回 "boolean"

x = 5;
typeof x; // 返回 "number"

x = "Hello";
typeof x; // 返回 "string"
```

`typeof` 运算符返回与变量存储的值相关的数据类型的小写字符串表示。ECMAScript 定义了五种原始数据类型：`Undefined`、`Null`、`Boolean`、`Number` 和 `String`。`Undefined` 和 `Null` 分别是 `undefined` 和 `null` 常量的特殊类型。`Boolean` 类型包含两个值：`true` 和 `false`。`Number` 类型存储浮点数。`String` 类型存储 Unicode 字符串。

变量也可以存储对象和函数，对应于 `Object` 和 `Function` 数据类型。例如：

```
var x = new Array(10); // 返回 "object"
typeof x;
x = print; // 返回 "function"
typeof x;
```

与 Java 类似，ECMAScript 区分原始数据类型和对象类型。原始数据类型的行为类似于 C++ 值类型（如 `int` 和 `QString`），它们不通过 `new` 运算符创建，并且按值拷贝。相比之下，对象类型必须使用 `new` 运算符创建，且这些类型的变量只存储指向对象的引用（指针）。当使用 `new` 分配对象时，我们不需要担心释放它们的内存，因为垃圾回收器会自动完成工作。

如果在不先使用 `var` 关键字声明的情况下给变量赋值，该变量将被创建为全局变量。如果我们尝试读取不存在的变量的值，将得到 `ReferenceError` 异常。我们可以使用 `try...catch` 语句捕获异常，如下：

```
try {
  print(y);
} catch (e) {
  print(e.name + ": " + e.message);
}
```

如果变量 `y` 不存在，控制台将打印消息 "ReferenceError: y is not defined"。

如果未定义的变量会对我们的程序造成混乱，那么已定义但持有 `undefined` 常量的变量也是如此——在使用 `var` 声明变量时会提供默认值。为了测试是否为 `undefined`，我们可以使用严格比较运算符 `===` 或 `!==`。例如：

```
var x;
...
var y = 0;
if (x === undefined) {
  print("x is undefined");
}
if (y !== undefined) {
  print("y is not undefined");
}
```

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

对于 C++ 程序员来说，ECMAScript 最难以接受的方面可能是它与 C++、C#、Java、Simula 和 Smalltalk 不同，这些都是基于类的。ECMAScript 并没有提供类概念，而是提供了更底层的机制，让我们能够实现相同的的结果。

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

图 22.1 列出了 ECMAScript 提供的内置全局常量、函数和对象。在下一节中，我们将看到如何用用 C++ 编写的额外特定应用程序组件来补充此功能。

# 图 22.1. 全局对象的内置属性

| 常量 | 描述 |

| :--- | :--- |

| NaN | IEEE 754 非数字 (NaN) 值 |

| Infinity | 正无穷大 (+∞) |

| undefined | 未初始化变量的默认值 |

| 函数 | 描述 |

| :--- | :--- |

| print(x) | 在控制台上打印值 |

| eval(str) | 执行 ECMAScript 程序 |

| parseInt(str, base) | 将字符串转换为整数 |

| parseFloat(str) | 将字符串转换为浮点数 |

| isNaN(n) | 如果 n 是 NaN 则返回 true |

| isFinite(n) | 如果 n 是除 NaN、+∞ 或 -∞ 以外的数字，则返回 true |

| decodeURI(str) | 将 8 位编码的 URI 转换为 Unicode |

| decodeURIComponent(str) | 将 8 位编码的组件转换为 Unicode |

| encodeURI(str) | 将 Unicode URI 转换为 8 位编码 |

| encodeURIComponent(str) | 将 Unicode 组件转换为 ECMAScript 标准指定的 8 位编码 |

| 类 (构造函数) | 描述 |

| :--- | :--- |

| Object | 提供所有对象通用的功能 |

| Function | 封装一个 ECMAScript 函数 |

| Array | 表示可伸缩的项向量 |

| String | 存储 Unicode 字符串 |

| Boolean | 存储布尔值 (true 或 false) |

| Number | 存储浮点数 |

| Date | 存储日期和时间 |

| RegExp | 提供正则表达式匹配 |

| Error | 错误类型的基类型 |

| EvalError | 错误使用 eval() 时抛出 |

| RangeError | 数值超出合法范围时抛出 |

| ReferenceError | 尝试访问未定义变量时抛出 |

| SyntaxError | 被 eval() 检测到语法错误时抛出 |

| TypeError | 当参数类型错误时抛出 |

| URIError | 解析失败时抛出 |

| Math | 提供数学常量和函数 |
