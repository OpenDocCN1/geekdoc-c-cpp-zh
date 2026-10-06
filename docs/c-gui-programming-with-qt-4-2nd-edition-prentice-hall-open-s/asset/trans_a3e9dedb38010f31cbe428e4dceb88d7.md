
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
