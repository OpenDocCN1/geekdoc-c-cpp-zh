

```js
{
  type: "apply",
  operator: {type: "word", name: ">"},
  args: [
    {type: "word", name: "x"},
    {type: "value", value: 5}
  ]
}
```

我们描述一个函数 parseExpression，它接收一个字符串作为输入，并返回一个对象，其中包含字符串开头处表达式的数据结构，以及解析完该表达式后字符串剩余的部分。在解析子表达式时，你可以再次调用这个函数，并将剩余文本作为参数表达式传给它。这段文本可能包含更多参数，或包含结束参数列表的右括号。

下面是解析器的第一部分：

```js
function parseExpression(program) {
  program = skipSpace(program);
  let match, expr;
  if (match = /^"([^"]*)"/.exec(program)) {
    expr = {type: "value", value: match[1]};
  } else if (match = /^\d+\b/.exec(program)) {
    expr = {type: "value", value: Number(match[0])};
  } else if (match = /^[^\s(),#]+/.exec(program)) {
    expr = {type: "word", name: match[0]};
  } else {
    throw new SyntaxError("Unexpected syntax: " + program);
  }
  return parseApply(expr, program.slice(match[0].length));
}

function skipSpace(string) {
  let first = string.search(/\S/);
  if (first == -1) return "";
  return string.slice(first);
}
```

## 求值器

求值器用于运行程序的语法树。给它一个语法树和一个将名称与值关联起来的作用域对象，它就会求值该树所表示的表达式，并返回由此产生的值。

```js
const specialForms = Object.create(null);
function evaluate(expr, scope) {
  if (expr.type === "value") {
    return expr.value;
  } else if (expr.type === "word") {
    if (expr.name in scope) {
      return scope[expr.name];
    } else {
      throw new ReferenceError(
        `Undefined binding: ${expr.name}`);
    }
  } else if (expr.type === "apply") {
    let {operator, args} = expr;
    if (operator.type === "word" &&
        operator.name in specialForms) {
      return specialForms[operator.name](expr.args, scope);
    } else {
      let op = evaluate(operator, scope);
      if (typeof op === "function") {
        return op(...args.map(arg => evaluate(arg, scope)));
      } else {
        throw new TypeError("Applying a non-function.");
      }
    }
  }
}
```

求值器包含针对每种表达式类型的代码。字面值表达式返回其值。对于单词，检查它是否在作用域中定义；如果已定义，则返回该绑定的值。如果它是特殊形式，则不进行任何求值；相反，它把参数表达式连同作用域一起传给处理该形式的函数。如果是普通调用，则求值运算符，判断它是否为函数，并用求值后的参数调用它。用普通 JavaScript 函数值表示 Egg 的函数值。求值的递归结构与解析器的结构相似，二者都映射语言的结构。你可以把解析器与求值器合并，在解析过程中进行求值，但将它们分开能更清晰地呈现程序。实现 Egg 所需的全部内容就这些。

## 特殊形式

specialForms 对象描述了 Egg 中独特的语法。它将单词与处理此类形式的函数关联起来。它目前是空的。让我们添加 if。

```js
specialForms.if = (args, scope) => {
  if (args.length != 3) {
    throw new SyntaxError("Wrong number of args to if");
  } else if (evaluate(args[0], scope) !== false) {
    return evaluate(args[1], scope);
  } else {
    return evaluate(args[2], scope);
  }
};
```

Egg 的 if 构造期望三个参数。它求值第一个参数，如果值不是 false，就求值第二个参数。否则，它求值第三个参数。if 形式看起来更像 JavaScript 的三元 ?: 运算符，而不是 JavaScript 的 if。它是一个表达式，而不是语句，并会产生一个值，即第二个或第三个参数的结果。Egg 在对待条件值的方式上也与 JavaScript 不同。它不会把零或空字符串之类的东西视为 false，只把确切的 false 值视为假。函数的所有参数都会在函数被调用之前求值。

```js
specialForms.while = (args, scope) => {
  if (args.length != 2) {
    throw new SyntaxError("Wrong number of args to while");
  }
  while (evaluate(args[0], scope) !== false) {
    evaluate(args[1], scope);
  }
  // Since undefined does not exist in Egg, we return false,
  // for lack of a meaningful result.
  return false;
};
```

另一个基本构件是 do，它从上到下依次求值其参数。它的值是最后一个参数的值。

```js
specialForms.do = (args, scope) => {
  let value = false;
  for (let arg of args) {
    value = evaluate(arg, scope);
  }
  return value;
};
```

要创建绑定并赋予新值，我们需要一个称为 define 的形式。它期望第一个参数是一个单词，第二个参数是一个表达式，该表达式产生要赋给该单词的值。因为 define 是一个表达式，所以它必须返回一个值。我们将返回被赋的值（类似 JavaScript 的 = 运算符）。

```js
specialForms.define = (args, scope) => {
  if (args.length != 2 || args[0].type != "word") {
    throw new SyntaxError("Incorrect use of define");
  }
  let value = evaluate(args[1], scope);
  scope[args[0].name] = value;
  return value;
};
```

## 环境

evaluate 接收的作用域是一个对象，其属性名对应绑定名。它们的值对应那些绑定所绑定的值。下面是一个表示全局作用域的对象示例。为了能够使用前面描述的 if 构造，布尔值必须可访问。由于只有两个布尔值，你只需将两个名称分别绑定到 true 和 false 值并使用它们。

```js
const topScope = Object.create(null);
topScope.true = true;
topScope.false = false;
```

现在我们可以求值一个对布尔值取反的简单表达式。

```js
let prog = parse(`if(true, false, true)`);
console.log(evaluate(prog, topScope));
// → false
```

为了提供基本的算术和比较运算符，让我们把函数值添加到作用域中。我们将在一个循环中对几个运算符函数使用 Function 构造器，而不是逐个写出来。

```js
for (let op of ["+", "-", "*", "/", "==", "<", ">"]) {
  topScope[op] = Function("a, b", `return a ${op} b;`);
}
```

我们将把 console.log 包装在一个函数中以输出值，并将其称为 print。

```js
topScope.print = value => {
  console.log(value);
  return value;
};
```

这提供了足够的基础工具，可用来编写简单程序，并在新的作用域中解析和运行它们：

```js
function run(program) {
  return evaluate(parse(program), Object.create(topScope));
}
```

对象原型链将表示嵌套作用域，允许我们添加绑定而不改变顶层作用域。

```js
run(`
do(define(total, 0),
define(count, 1),
while(<(count, 11),
do(define(total, +(total, count)),
define(count, +(count, 1)))),
print(total))
`);
// → 55
```

这个程序计算 1 到 10 的数字之和，如 Egg 中所示。

## 函数

没有函数的编程语言非常糟糕，尽管添加函数很容易：把最后一个参数用作函数体，并把此前的每个参数用作函数的参数名。

```js
specialForms.fun = (args, scope) => {
  if (!args.length) {
    throw new SyntaxError("Functions need a body");
  }
  let body = args[args.length - 1];
  let params = args.slice(0, args.length - 1).map(expr => {
    if (expr.type != "word") {
      throw new SyntaxError("Parameter names must be words");
    }
    return expr.name;
  });
  return function() {
    if (arguments.length != params.length) {
      throw new TypeError("Wrong number of arguments");
    }
    let localScope = Object.create(scope);
    for (let i = 0; i < arguments.length; i++) {
      localScope[params[i]] = arguments[i];
    }
    return evaluate(body, localScope);
  };
};
```

Egg 函数有自己的局部作用域。由 fun 形式创建的函数会创建这个局部作用域，并向其中添加参数绑定。然后它在这个作用域中求值函数体并返回结果。

```js
run(`
do(define(plusOne, fun(a, +(a, 1))),
print(plusOne(10)))
`);
// → 11

run(`
do(define(pow, fun(base, exp,
  if(==(exp, 0),
    1,
    *(base, pow(base, -(exp, 1))))),
print(pow(2, 10))
`);
// → 1024
```

## 总结

本章我们涵盖了解析、函数、特殊形式和求值器。记法（即语法）是编程中非常重要的一个方面。解析器读取文本并产生一个数据结构，该结构表示文本中程序的结构。如果文本没有形成有效程序，解析器将发出错误信号。

## 练习

编写一个 JavaScript 函数来计算正整数的因数。

## 解答

