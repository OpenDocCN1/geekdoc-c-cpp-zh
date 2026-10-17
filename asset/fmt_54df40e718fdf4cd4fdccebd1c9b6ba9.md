
要运行一个函数，你必须调用它。如果函数有任何参数，参数的初始值会在调用函数时进行设置。调用函数并运行其包含的命令的通用表达式为：

```
function_name(parameter values)
```

其中 `function_name` 是函数名，`parameter values` 是与函数参数匹配的逗号分隔的值列表。如果函数没有使用参数，请按如下所示留空参数值：

```javascript
function_name()
```

例如，调用之前描述的 `showDay()` 函数，使用字符串 `"11/3/2017"` 作为日期，并将 `"24:45:12 p.m."` 作为 `timeStr` 参数的值，你需要运行以下代码：

```javascript
showDay("24:45:12 p.m.");
```

结果是将以下 HTML 代码写入 `dateNode` 中：

```
11/3/2017<br>24:45:12 p.m.
```

参数值也可以赋值。以下代码使用存储在 `text1` 和 `text2` 变量中的值调用 `showDay()`：

```javascript
var text1="11/3/2017";
var text2="24:45:12 p.m.";
showDay(text1,text2);
```

结果是将相同的代码写入 `dateNode` 元素的 `innerHTML` 属性中。其巨大优势之一是它们可以使用不同的值反复调用，以实现不同的结果。另一个优势是，函数可以将长且复杂的脚本拆分为可管理的块。将经常使用的函数包含在单独的 JavaScript 文件也是良好的编程习惯，这样整个网站的脚本都可以访问并使用它们。通过添加调用行来执行 `runClock()` 函数。

## 调用 runClock()

- 1. 在 `runClock()` 的正上方，插入以下命令：

`/* 用于创建和运行倒计时钟的函数 */`

`runClock();`

- 2. 将你的代码与图 9-3 进行对比，该图高亮了运行 `runClock()` 函数的代码。

![](img/bf90ebf56b5f948b05e7a26851204c31_733_0.png)

- 3. 保存文件的更改，然后在浏览器中重新加载 `tiny_clock.html`。验证页面再次显示当前日期和时间，并计算到元旦的间隔。

## 创建一个返回值的函数

你创建 `runClock()` 函数是为了执行写入 HTML 代码的操作。函数的另一个用途是返回一个计算后的值。要让函数返回一个，必须以 `return` 语句结束，如下：

```javascript
function_name(parameters) {
    return value;
}
```

其中 `value` 是函数返回的计算值。例如，以下 `calArea()` 函数返回矩形的面积：

```javascript
function calArea(length, width) {
    var area = length * width;
    return area;
}
```

你可以像这样调用并获取返回值：

```javascript
var result = calArea(5, 10);
```

在上面的例子中，`result` 变量将存储函数返回的 50。另一个是返回字符串的例子：

```javascript
function getGreeting(name) {
    return "Hello, " + name;
}
var message = getGreeting("Alice");
```

在这个例子中，`message` 变量将存储 `"Hello, Alice"`。

## 函数与作用域

在函数内部定义的变量是该函数作用域内的。例如：

```javascript
var x = 10;
function myFunction() {
    var y = 20;
    console.log(x + y);
}
myFunction();
console.log(y); // 这会报错，因为 y 是局部变量
```

函数也可以访问全局变量。例如：

```javascript
function myFunction() {
    var z = 30;
}
myFunction();
console.log(z); // 这会报错，因为 z 是函数内部的
```

在函数外部定义的变量是全局作用域的。例如：

```javascript
var timer;
function startTimer() {
    timer = setInterval(function() {
        console.log("Tick");
    }, 1000);
}
startTimer();
clearInterval(timer);
```

## 定时命令

你已经完成了倒计时钟所需的函数，但页面是静态的，只有重新加载时才会变化。你想让钟不断更新，以便显示当前时间和到元旦剩余的时间。JavaScript 提供了两种方法：延迟命令和间隔命令。

### 使用延迟命令

延迟命令是在指定时间后运行的 JavaScript 命令。延迟使用 `setTimeout` 方法定义：

```javascript
setTimeout(command, delay);
```

其中 `command` 是 JavaScript 命令，`delay` 是浏览器运行命令前的毫秒数。命令必须放在引号中。例如，在 5 秒后运行 `runClock()` 函数的延迟：

```javascript
setTimeout(function() {
    runClock();
}, 5000);
```

在 JavaScript 程序中，你可能需要取消一个延迟命令。当其他用户不再运行该命令时，这是必要的。延迟命令使用以下语句取消：

```javascript
clearTimeout(timeout);
```

浏览器可以处理的延迟命令数量没有限制。为了区分不同的延迟命令，你为每个命令分配一个唯一的标识：

```javascript
var timeout = setTimeout(function() {
    runClock();
}, 5000);
```

其中 `timeout` 是存储延迟命令 ID 的变量。在你为命令分配了 ID 后，可以使用以下 `clearTimeout()` 方法取消它：

```javascript
clearTimeout(timeout);
```

其中 `timeout` 是存储命令 ID 的变量。

### 按指定间隔运行命令

运行 JavaScript 命令是使用间隔命令，它指示浏览器按照指定的间隔反复运行命令。间隔命令应用以下 `setInterval` 方法：

```javascript
setInterval(command, interval);
```

其中 `interval` 是命令再次运行之前的间隔时间（毫秒）。间隔命令通过使用以下语句停止：

```javascript
clearInterval(intervalID);
```

使用间隔命令时，你可能同时有多个间隔命令在运行。为了区分不同的间隔命令，你按如下所示将 ID 存储在变量中：

```javascript
var intervalID = setInterval(function() {
    runClock();
}, 1000);
```

其中 `intervalID` 是存储间隔命令 ID 的变量。

# 教程 9 JavaScript 入门 | HTML 和 CSS

通过应用以 `timeID` 为参数值的 `setInterval` 方法来停止时间间隔命令：

```
clearInterval(timeID);
```

需要记住的一点是，关于 `setTimeout()` 和 `setInterval()` 方法：浏览器在处理完稍后运行命令的请求后，并不会停止。相反，浏览器会继续处理脚本中的后续命令。例如，你可能会尝试使用以下结构以 50 毫秒的间隔运行三个函数：

```
setTimeout("function1()", 50);
setTimeout("function2()", 50);
setTimeout("function3()", 50);
```

然而，浏览器会同时运行这三个函数。为了让每个函数之间有约 50 毫秒的间隔运行函数，你需要使用三个不同的延迟时间，如下：

```
setTimeout("function1()", 50);
setTimeout("function2()", 100);
setTimeout("function3()", 150);
```

在这种情况下，用户的浏览器将在 50 毫秒后运行第一个函数，50 毫秒后运行第二个函数，在另一个 50 毫秒后运行第三个函数。

# 运行定时命令

- 若要在延迟后运行命令，使用方法 `timeID = setTimeout("command", delay)`，其中 `command` 是要运行的命令，`delay` 是毫秒单位的延迟时间，`timeID` 是存储与定时命令关联 ID 的变量。
- 若要按间隔重复命令，使用方法 `timeID = setInterval("command", interval)`，其中 `interval` 是重复命令的时间（单位为毫秒）。
- 若要取消特定的定时命令，使用方法 `clearInterval(timeID)`，其中 `timeID` 是定时命令的 ID。
- 若要清除所有定时命令，使用以下方法：`clearInterval()`
- 若要取消重复命令，使用方法 `clearInterval(timeID)`，其中 `timeID` 是重复命令的 ID。
- 若要清除所有重复命令，使用以下方法 `clearInterval()`

# HTML 720 HTML 和 CSS | 教程 9 JavaScript 入门

使用 `setInterval()` 方法反复运行 `runClock()` 函数。由于函数应该每秒运行一次，请使用命令将间隔长度设置为 1000 毫秒：

```
setInterval("runClock()", 1000);
```

现在将此内容添加到 `try_script.js` 文件中。

## 每秒运行一次 runClock() 函数

- 1. 回到编辑器中的 `try_script.js` 文件，在 `runClock()` 命令正下方插入以下内容：

图 9-8 显示了用于定时间隔命令运行的代码。

图 9-38 重复 `runClock()` 函数

```
/* 执行该函数以运行并显示倒计时钟 */
runClock();
setInterval("runClock()", 1000);
```

![](img/bf90ebf56b5f948b05e7a26851204c31_737_0.png)

- 2. 保存文件更改并在浏览器中重新加载 `try_clock.html`。
- 3. 验证随着跨年派对（New Year's Eve Bash）日期的接近，每秒时间值和倒计时值都会发生变化。

你已经完成了新年派对的倒计时钟。Hector 将继续开发活动网站，并在有任何新项目或疑虑时与你联系。

# 使用数值控制 JavaScript 的工作

当你使用 JavaScript 进行数学计算时，你会遇到需要处理数值本身属性的情况。JavaScript 提供了几种方法，允许你检查数字的属性性，并指定它们在网页上的显示方式。

## 处理非法操作

某些数学运算返回的结果不是数值。例如，你不能将一个数字除以字符串。像 `"5/a"` 这样的表达式会返回 `"Not A Number"`，这是 JavaScript 表示非法操作的方式（该操作应仅涉及数值），但你可以使用以下 `isNaN()` 函数检查该错误是否存在：

```
isNaN(value)
```

其中 `value` 是你想要测试是否为数值的变量或值。如果值不是数值，`isNaN()` 返回 `true`，否则返回 `false`。`isNaN` 函数是定位代码中非数值视为数值处理的非法操作的方法之一。

另一个非法操作是将数字除以 0，这会返回 `Infinity` 值，表示计算结果大于 JavaScript 支持的数值。对于结果小于最小值的运算，也会生成 `Infinity` 值。JavaScript 学习处理的是大约在 $1.8 \times 10^{-308}$ 和 $1.8 \times 10^{308}$ 之间的值。任何超出这些界限的操作（例如尝试将数字除以 0），你都可以使用函数检查此结果：

## isFiniteValues

> 提示
>
> 报告运行时错误或逻辑错误的程序可能存在数据值不匹配，你可以使用 `isNaN()` 和 `isFinite()` 来确定值的状态。

其中 `value` 是你想要测试是否为有限的值。如果该值是有限的，`isNaN()` 函数和 `isFinite()` 函数将返回一个布尔值。

# 教程 9 JavaScript 入门 | HTML 和 CSS HTML 721

# 定义数字

当 JavaScript 显示数字时，`toFixed()` 方法限制了位数。注意 `toFixed()` 会对值进行舍入而不是截断。

# 转换数字和文本

有时你可能需要将字符串转换为数字，反之亦然。将字符串转换为数字的一种方法是使用 `+` 运算符。例如，以下代码使用 `+` 拼接字符串：

```
testString = "123";
testNumber = testString + ""; // 数值字符串
```

将字符串转换为数字，可以使用任何非 `+` 的算术运算符。结果是一个数字。

```
testString = "123";
testNumber = testString*1; // 数值
```

# HTML 720 HTML 和 CSS | JavaScript JavaScript 入门

另一种转换文本值的方法是使用以下 `parseInt()` 函数，它可以从文本中提取整数值：

```
parseInt(text)
```

其中 `text` 是你想要从中提取整数值的字符串或变量。`parseInt()` 函数从文本中提取整数，并忽略非数字字符。如果文本字符串不是以整数开头，函数返回 `NaN`；如果文本字符串不包含数字。以下是 `parseInt()` 方法的一些示例值：

```
parseInt("120 lbs"); // 返回 120
parseInt("120abc"); // 返回 120
parseInt("weight equals 120 lbs"); // 返回 NaN
```

![](img/bf90ebf56b5f948b05e7a26851204c31_739_0.png)

图 9-39 总结了处理数值的 JavaScript 函数和方法。

| 数值函数 | 说明 |
| --- | --- |
| isFinite(value) | 指明值是否为有限实数 |
| NaN(value) | 指明值是否为数字 |
| parseFloat(string) | 从文本字符串中提取第一个数值 |
| parseInt(string) | 从文本字符串中提取第一个整数值 |
| 数值方法 | 说明 |
| --- | --- |
| value.toFixed(n) | 返回以指数计数法表示数值的字符串，小数点后有 n 位数字 |
| value.toFixed(n) | 返回保留到 n 位小数的数值字符串 |
| value.toPrecision(n) | 返回小数点左侧或右侧 n 位有效数字的数值字符串 |

图 9-39

你不需要在代码中使用 `parseInt()` 或其他数值方法。此时，你可以打开任何文件或应用程序。

# 教程 9 JavaScript 入门 | HTML 和 CSS

## HTML 723

## 解决问题：修复常见的编程错误

当你开始编写 JavaScript 程序时：

- **变量名拼写错误：** 例如，如果你将变量命名为 `ListPrice`，那么拼写错误或大小写不正确——例如 `listprice`、`ListPrice` 或 `list_price`——将导致程序无法正常运行。
- **括号或大括号不匹配：** 下述代码会导致错误，因为函数缺少大括号：

```
function Area(width, height) {
  var size = width+height;
}
```

- **引号不匹配：** 如果 JavaScript 将文本字符串视为对象或值，就会导致错误。下面的代码会导致错误，因为第一个变量名缺少了双引号：

```javascript
var firstName = "Sean"
var lastName = "Lee";
```

- **缺少引号：** 当你使用 `+` 符号组合多个文本字符串时，可能会忘记给所有文本字符串加引号。例如，该代码由于 `<br />` 标签周围缺少引号而产生错误。

```javascript
document.write("MidWest Student Union" + <br />);
```

随着经验的增加，你将能够识别这些类型的错误，使调试程序变得更加容易。

## 节 9.3 快速检查

1. 使用自增运算符提供命令将 `thisDay` 变量的值加 1。
2. 使用赋值运算符重写以下命令：

`income = taxes;`

3. 提供一个表达式，返回 `dailyIncome` 的值并向上舍入到下一个整数。
4. 圆的面积为 $\pi*r^2$，其中 $r$ 是圆半径。提供一个 JavaScript 表达式，返回半径存储在变量 `radius` 中的圆的面积。
5. 提供代码创建一个名为 `calcArea()` 的函数，该函数根据给定的半径返回圆面积。
6. 提供命令调用 `calcArea()`，使用值 15 作为圆半径并将结果存储在名为 `finalArea` 的变量中。
7. 局部作用域和全局变量之间的区别是什么？
8. 提供在 5 秒后运行 `init()` 函数的命令。`init()` 函数没有参数值。
