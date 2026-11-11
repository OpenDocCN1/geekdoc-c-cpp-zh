
```javascript
};
```

无需构建对象来保存迭代状态，生成器会立即存储其局部状态，并且每次都会产出。这个 yield 表达式只能直接发生在生成器函数内部，而不能发生在你在其中设置的内层函数中。生成器在产出时会保存。这是它的局部环境以及它产出的位置。异步函数是一种特殊的生成器。它在被调用时创建一个 Promise，该 Promise 在函数完成时解决，在抛出异常时拒绝。每当它产出一个 Promise，该 Promise 的结果就会成为 await 表达式的结果。

### 事件循环

异步程序一项接一项地执行。每个片段可能启动若干操作，并安排代码在操作完成或失败时执行。在这些片段之间，程序什么都不做，等待下一个操作。因此，你不能由安排回调的代码来调用回调。如果你在函数内部调用 setTimeout，那么在该回调函数被调用之前，这个函数就已经返回了。异步特性发生在其空的函数调用栈上。由于每个回调都从空栈开始，当异常发生时，你的 catch 处理器不会在栈上。

```javascript
try {
setTimeout(() => {
throw new Error("Woosh");
}, 20);
} catch (_) {
// This will not run
console.log("Caught");
}
```

无论超时或传入请求等事件如何发生，JavaScript 环境一次只运行一个程序。当无事可做时，循环停止。但当事件到来时，它们会被附加到队列中，其代码会一个接一个地执行。由于两件事不会同时运行，运行缓慢的代码可能会阻碍其他事件的处理。下面的示例设置了一个超时，但还会一直停留到超时设定时间之后，从而使超时延迟。

```javascript
let start = Date.now();
setTimeout(() => {
console.log("Timeout ran at", Date.now() - start);
}, 20);
while (Date.now() < start + 50) {}
```

```javascript
console.log("Wasted time until", Date.now() - start);
// → Wasted time until 50
// → Timeout ran at 55
```

Promise 会作为新事件被解决或拒绝。即使一个 Promise 已经解决，等待它也会让你的回调在当前脚本完成后运行，而不是立即运行。

```javascript
Promise.resolve("Done").then(console.log);
console.log("Me first!");
// → Me first!
// → Done
```

### 异步错误

当你同步运行程序时，除了程序自身产生的变化外，不会有其他给定的变化发生。但运行异步程序时，就是另一回事了。它们在执行过程中可能包含其他代码可以利用的间隙。下面是一个示例。我们乌鸦最喜欢做的事情之一，是统计每年村里孵化的雏鸡数量。巢把这一计数保存在它们的存储球中。下面的代码试图统计特定年份每个巢的计数：

```javascript
function anyStorage(nest, source, name) {
  if (source == nest.name) return storage(nest, name);
  else return routeRequest(nest, source, "storage", name);
}

async function chicks(nest, year) {
  let list = "";
  await Promise.all(network(nest).map(async name => {
    list += `${name}: ${
      await anyStorage(nest, name, `chicks in ${year}`)
    }\n`;
  }));
  return list;
}
```

`async name =>` 语法表明，将 `async` 一词放在箭头函数前面也可以使箭头函数变为异步。该代码对巢集合运行异步箭头函数，构建一个 Promise 数组，并利用 Promise.all 在返回它们创建的列表之前等待。但它有问题。它会返回一行输出，列出响应最慢的巢。你知道为什么吗？问题出在 `+=` 运算符：它在语句开始执行时获取列表的当前值，并在等待结束时将列表绑定设置为该值加上添加的字符串。但在语句开始和结束之间，存在一个异步间隙。map 表达式最先运行，此时你还不能向列表添加任何内容，因此每个 `+=` 运算符都从空字符串开始，并在其检索存储完成时结束。和往常一样，计算新值是一个无错误的过程，而不是转换现有值。

```javascript
async function chicks(nest, year) {
  let lines = network(nest).map(async name => {
    return name + ": " +
      await anyStorage(nest, name, `chicks in ${year}`);
  });
  return (await Promise.all(lines)).join("\n");
}
```

错误很容易发生，尤其是在使用 await 时，你应该知道代码中的间隙在哪里。

### 总结

本章我们学习了异步编程的全部内容。异步编程让程序能够表达对长时间运行操作的等待，而不会在整个操作过程中给程序造成问题。JavaScript 环境通常通过回调（在操作结束时被调用的函数）来使用这种编程风格。我们也简要讨论了事件循环。事件循环为这类回调制定计划，使它们在合适的时候一个接一个地被调用，以避免重叠。

### 练习

编写一个 JavaScript 程序，将异步函数转换为返回 Promise 的函数。

### 解决方案

**HTML 代码：**

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Convert an asynchronous function to return a promise</title>
</head>
<body>

</body>
</html>
```

**JavaScript 代码：**

```javascript
//#source https://bit.ly/2newfJ2
const promisify = func => (...args) =>
  new Promise((resolve, reject) =>
    func(...args, (err, result) => (err ? reject(err) : resolve(result)))
  );
const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(() => console.log('Hi!')); // Promise resolves after 2s
```

## 第 13 章：解析

开发自己的编程语言相对容易，而且非常令人兴奋。本章将教你如何构建自己的语言。我们将创建一种名为 Egg 的编程语言。一种小而简单的语言依然强大到足以表达任何可想象的计算。它支持纯抽象和确定的函数。

### 解析

编程语言最引人注目的部分是记法或语法。解析器是一个读取文本并提供数据结构的程序，该结构反映文本中程序的结构。如果文本无法构成有效程序，解析器会指出错误。我们的语言将具有精确且统一的语法。Egg 中的所有内容都是表达式。表达式可以是绑定名、数字、字符串或应用。使用“应用”表示函数调用以及 if 或 while 等结构。

为保持解析器简单，Egg 中的字符串不支持反斜杠转义。字符串是由非双引号字符组成的序列，并用双引号括起来。名称绑定可以包含任何不是空白且在语法中没有特殊含义的字符。在 JavaScript 中编写应用时，在表达式后放置圆括号，并在括号内放入任意数量的参数，以逗号分隔。

```javascript
do(define(x, 10),
if(>(x, 5),
  print("large"),
  print("small")))
```

Egg 语言的一致性意味着 JavaScript 中的运算符（如 >）在此语言中称为绑定，使用方式与其他函数类似。而且语法中完全没有块的概念，因此需要一种结构来表示连续运行多个事物。解析器用来定义程序的数据结构包含表达式对象。每个对象包含一个 type 属性，表示它是什么类型的表达式，以及若干其他属性来确定其内容。类型为 "value" 的表达式表示字符串或数字。它们的 value 属性由它们所代表的字符串或数字值组成。对标识符（名称）使用类型为 "word" 的表达式。这类对象包含一个 name 属性，以字符串形式保存标识符的名称。然后 "apply" 表达式表示应用。它们包含一个 operator 属性，引用被应用的表达式，以及一个 args 属性，保存参数表达式数组。

新程序中的 >(x, 5) 部分会像这样：
