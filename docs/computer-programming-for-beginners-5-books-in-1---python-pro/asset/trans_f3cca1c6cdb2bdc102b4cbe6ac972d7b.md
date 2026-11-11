
异常的影响是一种不同类型的控制流。这表明你的代码可能有不同的副作用，但异常可能阻止它们发生。下面是一些糟糕的银行代码：

```
const accounts = {
a: 100,
b: 0,
c: 20
};
function getAccount() {
let accountName = prompt("Enter an account name");
if (!accounts.hasOwnProperty(accountName)) {
throw new Error(`No such account: ${accountName}`);
}
return accountName;
}
function transfer(from, amount) {
if (accounts[from] < amount) return;
accounts[from] -= amount;
accounts[getAccount()] += amount;
}
```

transfer 函数用于从指定账户向另一个账户发送特定金额的钱，同时要求输入另一个账户的名称。如果输入错误的账户名，getAccount 会输出异常。如果钱已从第一个账户转出，然后程序在钱转入另一个账户之前输出异常，钱就会消失。解决这个问题，利用 finally 代码块。如下所示：

```
function transfer(from, amount) {
if (accounts[from] < amount) return;
let progress = 0;
try {
accounts[from] -= amount;
progress = 1;
accounts[getAccount()] += amount;
progress = 2;
} finally {
if (progress === 1) {
accounts[from] += amount;
}
}
}
```

### 选择性捕获

当异常一路到达代码块底部而未被处理时，它由环境处理。无效用法，例如在 null 上查找属性、引用不存在的绑定或调用非函数，将导致抛出异常。这些异常可以被捕获。JavaScript 不支持选择性捕获异常。下面是一个示例，它尝试持续调用 promptDirection，直到其提供有效答案：

```
for (;;) {
  try {
    let dir = promptDirection("Where?"); // ← typo!
    console.log("You select ", dir);
    break;
  } catch (e) {
    console.log("Invalid direction. Try again.");
  }
}
```

for (;;) 结构用于构建一个无法自行终止的循环。当获得有效方向时，你可以跳出循环，但拼写错误的 promptDirection 会输出未定义变量错误。如果你想捕获特定类型的异常，请在 catch 块中检查你拥有的异常是否是你想要的异常，并重新抛出它。让我们描述一种新的错误类型，并利用 instanceof 来识别它。

```
class InputError extends Error {}
function promptDirection(question) {
  let result = prompt(question);
  if (result.toLowerCase() == "left") return "L";
  if (result.toLowerCase() == "right") return "R";
  throw new InputError("Invalid direction: " + result);
}
```

新的错误类扩展了 Error。它没有定义自己的构造函数，而是继承 Error 构造函数，该构造函数期望一个字符串消息，我们可以借此识别它。

现在循环可以更仔细地捕获这些异常。

```
for (;;) {
  try {
    let dir = promptDirection("Where?");
    console.log("You chose ", dir);
    break;
  } catch (e) {
    if (e instanceof InputError) {
      console.log("Invalid direction. Try again.");
    } else {
      throw e;
    }
  }
}
```

### 总结

本章讨论调试。编程的一个重要部分是识别和修复错误。有时，你可以在本地解决问题。你可以使用特殊返回值或异常来跟踪它们。

### 练习

修复下面有问题的代码并指出问题：

```
for(var I=0; I > 5; I++) {
    console.log(i)
}
```

### 解答

![](img/239ff1e8a63502805c86c4dfbd71509a_738_0.png)

问题——循环内的条件不正确。

## 第10章：正则表达式

编程概念和工具以杂乱无章的方式发展，但它们的成功表明了一项出色的技术。在本章中，我们将讨论正则表达式。它们用于定义字符串数据中的模式。它们是一种小而不同的语言，是 JavaScript 以及其他语言的一部分。

### 创建正则表达式

正则表达式通过 RegExp 构造函数构造，或通过用正斜杠（/）字符包围模式来写为字面量值。

```
let re1 = new RegExp("ABC");
let re2 = /ABC/;
```

这两个正则表达式对象代表相同的模式。使用 RegExp 构造函数时，将模式写成普通字符串，以便反斜杠的规则适用。

第二种表示法对反斜杠的处理不同；必须在任何正斜杠前放置反斜杠，因为模式出现在斜杠字符之间。

### 测试匹配

正则表达式对象包含多个方法，其中之一是 test。当你传入一个字符串时，它返回一个布尔值，判断字符串是否包含表达式中模式的匹配项。

```
console.log(/abc/.test("abcde"));
// → true
console.log(/abc/.test("abxde"));
// → false
```

一个仅包含非特殊字符的正则表达式表示一个字符序列。如果 ABC 出现在字符串中的任何位置，当我们运行 test 时，test 将返回 true。

### 字符集

正则表达式使我们能够描述复杂的模式。如果你想在正则表达式中匹配任意数字，请将一组字符放在方括号之间。以下表达式匹配每个包含数字的字符串：

```
console.log(/[0123456789]/.test("in 1992"));
// → true
console.log(/[0-9]/.test("in 1992"));
// → true
```

方括号内两个字符之间的连字符（-）用于指定一个字符范围，该范围由字符的 Unicode 编号决定。从 0 到 9 的字符按此顺序彼此相邻（编码 48 到 57），因此 [0-9] 覆盖所有这些字符并匹配任意数字。常见字符组有内置快捷方式。数字就是这样一个组：`\d` 与 [0-9] 含义相同。

- `\d` 任意数字字符
- `\w` 一个字母数字字符（“单词字符”）
- `\s` 任意空白字符（空格、制表符、换行符及类似字符）
- `\D` 非数字字符
- `\W` 非字母数字字符
- `\S` 非空白字符
- `.` 除换行符外的任意字符

因此，用下面的表达式匹配像 01-30-2003 15:20 这样的日期和时间格式：

```
let dateTime = /\d\d-\d\d-\d\d\d\d \d\d:\d\d/;
console.log(dateTime.test("01-30-2003 15:20"));
// → true
console.log(dateTime.test("30-jan-2003 15:20"));
// → false
```

这些反斜杠代码也可以在方括号内使用。例如，`[\d.]` 匹配任意数字或句点字符；句点没有特殊含义，其他特殊字符（如 +）也是如此。

```
let notBinary = /^[^01]*/;
console.log(notBinary.test("1100100010100110"));
// → false
console.log(notBinary.test("1100100010200110"));
// → true
```

### 重复模式的部分

现在你已经很好地理解了如何匹配单个数字。如果你想匹配一个完整数字或一连串更多数字，请在正则表达式中的元素后紧跟一个加号（+）。这表示该元素可以重复不止一次；`/\d+/` 匹配一个或多个数字字符。

```
console.log(/\d+/.test("123"));
// → true
console.log(/\d+/.test(""));
// → false
console.log(/\d*/.test("123"));
// → true
console.log(/\d*/.test(""));
// → true
```

星号（*）使模式能够匹配零次出现。在下面的示例中，允许 `u` 字符出现，但未找到该字符时模式也能匹配。

```
let neighbor = /neighbour/;
console.log(neighbor.test("neighbour"));
// → true
console.log(neighbor.test("neighbor"));
// → true
```

要确定某个模式元素应出现特定次数，请使用花括号，在元素后插入 `{4}`。如果你希望它恰好出现四次，请使用 `{4}`。像 `{2,4}` 这样的范围表示该元素必须至少出现两次、至多出现四次。下面是日期和时间模式的另一个版本，它允许日、月和小时为一位数或两位数。

```
let dateTime = /\d{1,2}-\d{1,2}-\d{4} \d{1,2}:\d{2}/;
console.log(dateTime.test("01-30-2003 8:45"));
// → true
```

### 分组子表达式

如果你想一次对一个或多个元素使用像 * 或 + 这样的运算符，请使用圆括号。就运算符而言，正则表达式中用圆括号括起来的部分算作单个元素。

```
let cartoonCrying = /boo+(hoo+)+/i;
console.log(cartoonCrying.test("Boohooohooohooo"));
// → true
```

第一个和第二个 + 字符仅适用于 'boo' 和 'hoo' 中的第二个 'o'。第三个 + 适用于整个组 (hoo+)，匹配该组的一次或多次出现。示例中表达式末尾的 i 用于不区分大小写，使其能够匹配输入字符串中的大写 B，尽管模式完全是小写。

### 匹配和组

test 方法是测试正则表达式的最佳方式；它只判断是否匹配。正则表达式还有一个 exec（执行）方法，如果找不到匹配，它将返回 null；否则返回一个包含匹配相关数据的对象。

```
let match = /\d+/.exec("one two 100");
console.log(match);
// → ["100"]
console.log(match.index);
```
