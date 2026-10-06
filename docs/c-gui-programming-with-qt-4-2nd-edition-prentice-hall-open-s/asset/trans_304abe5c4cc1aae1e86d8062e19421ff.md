
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

# 2. 应用脚本

![](img/5a524abdf0b0d58fa99d30abb4463611_848_0.png)

- ECMAScript 语言概述
- 使用脚本扩展 Qt 应用
- 使用脚本实现 GUI 扩展
- 通过脚本实现自动化

脚本是用解释型语言编写的程序，用于扩展现有系统的功能。某些脚本作为独立应用程序运行，而另一些则嵌入应用程序中执行。Qt 包含了 QtScript，该模块可以使用 ECMAScript（JavaScript 的标准版本）使 Qt 应用脚本化。该模块是对早期 Trolltech Qt Script for Applications (QSA) 的完全重写，并对 ECMAScript 第 3 版提供了完全支持。

ECMAScript 是 Ecma International 标准化的官方名称。它是 JavaScript (Mozilla)、JScript (Microsoft) 和 ActionScript (Adobe) 的基础。尽管该语言的语法在表面与 C++ 和 Java 相似，但底层概念有着本质区别，使其与其他大多数面向对象的编程语言区分开来。在本章的第一节中，我们将快速回顾 ECMAScript 语言，并展示如何使用 Qt 运行 ECMAScript 代码。如果你已经熟悉 JavaScript 或任何其他基于 ECMAScript 的语言，可以直接跳过本节。

在第二节中，我们将看到如何为 Qt 应用添加脚本支持。这使得用户能够在应用程序已提供的功能之外添加自己的功能。这种方法也经常用于更方便用户支持；技术人员可以通过脚本的形式提供错误修复程序和解决方案。

在第三节中，我们将展示如何开发使用 Qt Designer 创建的 GUI 前端和表。这种技术对于不喜欢与 C++ 开发相关的“编译、链接、运行”循环并偏好脚本方法的开发者来说非常有吸引力。它还让具有 JavaScript 经验的用户设计完全功能的 GUI 界面，无需学习 C++。

在最后一节中，我们将展示如何开发依赖 C++ 组件作为处理部分的脚本。这可以使用任意 C++ 和 C++/Qt 组件完成，这些组件不需要为了脚本化而专门设计。当多个程序需要使用相同的基础组件编写时，或者当我们希望让非 C++ 程序员能够使用 C++ 功能时，这种方法特别有用。

# ECMAScript 语言概述

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

如果未定义的变量会对我们的程序造成混乱，因此定义但持有未定义常量的变量在用 `var` 声明变量时会提供默认值。要测试未定义，我们可以使用严格比较运算符 `===` 或 `!==`。例如：

```javascript
var x;
...
var y = 0;
if (x !== undefined)
  y = x;
```

ECMAScript 中也提供了熟悉的 `==` 和 `!=` 比较运算符，与 `===` 和 `!==` 不同，当所比较的值类型不同时，它们有时会返回 true。例如，`24 == "24"` 和 `null == undefined` 返回 true。
```
