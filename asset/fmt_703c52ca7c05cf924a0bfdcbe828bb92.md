
`document.getElementById("daysLeft").innerHTML = "45-<span>Days</span>";`

更改 `innerHTML` 属性的值会覆盖所选对象中当前包含任何内容，因此在重写文档中已存在的元素内容时，你应该小心。

Hector 为他的页面设置了以下包含日期和时间的 `div` 元素：

```html
<div id="dateNow">11/23/2017 12:45:12 p.m.</div>
```

使用 `innerHTML` 属性将此 div 元素的内容更改为字符串 "m/d/yr -h:m:s"。注意，你将用返回当前日期和时间的计算值来替换此字符串。

## 使用 JavaScript 编写 HTML 代码：

- 1. 如果你在上一节课后休息了，请确保在编辑器中打开了 `script.js` 文件。
- 2. 在注释区域的 `+` 行正下方插入以下代码：

```javascript
// Display the current date and time +/
document.getElementById("dateNow").innerHTML = "m/d/yr />h:m:s";
```

`innerHTML` 属性只能应用于代表文档内元素的对象。

务必使 Id 值的文本与 HTML 文件中的 Id 值匹配，包括大小写字母。

### 提示

# HTML 690 HTML 和 CSS | 第 9 节 开始学习 JavaScript

图 9-14 高出了新添加的代码。

## 图 9-14 更改元素内 HTML 代码的值

```javascript
/* 引用 ID 属性为 "dateNow" 的元素 */
/* 显示当前日期和时间 */
document.getElementById("dateNow").innerHTML = "m/d/y <br> + h:m:s";
/*为元素内的 HTML 代码设置新值 */
```

- 3. 保存对文件的更改，然后在浏览器中重新加载 `tny_clock.html` 文件。

图 9-15 显示了通过重写 `innerHTML` 属性值所写入的内容。

## 图 9-15 修改后的日期和时间内容

当前时间
m/d/y
h:m:s

使用 JavaScript 写入的内容

图 9-16 列出了其他可修改页面元素内容的 JavaScript 属性和方法。

# 第 9 节 开始学习 JavaScript | HTML 和 CSS HTML 691

图 9-16 插入内容的属性和方法

| 属性或方法 | 描述 |
| --- | --- |
| `element.innerHTML` | 返回元素内的 HTML 代码 |
| `element.outerHTML` | 返回元素内的 HTML 代码以及元素本身的 HTML 代码 |
| `element.textContent` | 返回元素内定义的文本，忽略 HTML 标签 |
| `element.insertAdjacentHTML(position, text)` | 在指定位置插入由 text 元素定义的 HTML 内容，其中 position 为之一：'beforebegin'（在元素开始标签之前）、'afterbegin'（在元素开始标签之后）、'beforeend'（在元素结束标签之前）或'afterEnd'（在元素结束标签之后） |

如果页面仅包含文本而没有 HTML 标记，你可以使用 `textContent` 属性修改其内容。在 `try.html` 文件中，Hector 将倒计时值放置在以下元素中：

```html
<div><span id="days">%s</span></div>
<div><span id="hours">%s</span></div>
<div><span id="mins">%s</span></div>
<div><span id="secs">%s</span></div>
```

使用 `textContent` 属性将天、小时、分钟、秒改为字符串 "dd", "hh", "mm", "ss"。

## 使用 JavaScript 写入文本：

- 1. 返回编辑器中的 `try.js` 文件。
- 2. 在文件底部插入以下代码：

图 9-17 新添加的代码。

```javascript
/* 显示当前日期和时间 */
document.getElementById("now").innerHTML = "m/d/y/>h:m:s";
/* 显示距离跨年夜的剩余 */
document.getElementById("days").textContent = "dd";
document.getElementById("hours").textContent = "hh";
document.getElementById("mins").textContent = "mm";
document.getElementById("secs").textContent = "ss";
```

| 引用元素 | 属性 | 新文本内容 |
| --- | --- | --- |
| ID 为 "days", "hours", "mins" 和 "secs" | 元素内的 | 元素 |

# HTML 692 HTML 和 CSS | 第 9 节 开始学习 JavaScript

- 3. 保存对文件的更改，然后在浏览器中重新加载 `tny_clock.html` 文件。
图 9-18 显示了用于倒计时的占位文本。

## 图 9-18 修改后的文本内容

![](img/bf90ebf56b5f948b05e7a26851204c31_709_0.png)

注意如果你要在文本内容中插入 HTML 代码，必须使用 `innerHTML`。`textContent` 属性仅适用于纯文本。

## 使用 document.write() 写入内容

向网页文档写入 HTML 内容的另一种方法是使用以下方法：

```
document.write(text)
```

其中 *text* 是内容的文本。`document.write()` 方法通常与嵌入脚本一起使用，在浏览器加载时直接写入内容。例如，下面的代码使用嵌入脚本向页面页头写入一个 H1 标题。

```html
<header>
  <script>
    document.write("<h1>Welcome to Tulsa!</h1>");
  </script>
</header>
```

注意，如果在此 HTML 文件完全加载后应用此方法，它将覆盖文档中所有的 HTML 内容，用 `document.write()` 指定的替换 HTML 代码。如果你想在页面由浏览器加载后修改，你应该只使用 `innerHTML` 或 `textContent` 属性。

# 变量的操作

由于你在 `innerHTML` 属性中使用了特定的文本字符串，你的脚本所做的并不比直接在网页中输入 HTML 代码所做的多多少。JavaScript 在与变量结合使用时变得强大且有用得多。变量是程序中一个命名的条目，用于存储数据值（如数字或文本）或对象，作为 浏览器或浏览器窗口的一部分。变量之所以有用，是因为它们可以存储脚本某部分创建的信息并在其他地方使用它。

## 声明变量

通过以下关键字声明变量，将变量引入脚本：

```
var variable = value;
```

```javascript
currentDay = "May 3, 2018";
```

你不需要为变量提供初始值。你可以让变量的值保持为未定义（undefined），如下面的命令所示，该命令声明了 `currentDay` 变量但没有提供值：

```
currentDay =;
```

你可以通过在逗号分隔的列表中输入变量名来声明多个变量。以下语句声明了名为 `currentMonth` 和 `currentYear` 的两个变量，并分别为它们赋值为 "May" 和 2018。

```javascript
currentMonth = "May", currentYear = 2018;
```

JavaScript 对变量实施了以下限制：

-   第一个字符必须是字母或下划线字符 (_)。
-   其余字符可以是字母、数字或下划线。
-   变量名不能包含空格。
-   你不能使用 JavaScript 语言本身的一部分名称；例如，你不能将变量命名为 "document" 或window" 或 "textContent"。

与 JavaScript 的其他部分一样，变量名对大小写敏感。变量名 `currentday` 和 `currentDate` 代表两个不同的变量。一个常见的错误是忘记这个重要事实，并在变量名中交替使用大写和小写字母。

变量声明后，可以通过给以下命令分配新值来更改它的值：

```
variable = value;
```

其中 `variable` 是变量名，`value` 是分配给变量的新值。因此，"May 4, 2018"：

```javascript
currentDay = "May 4, 2018";
```

使用变量的优点之一是你可以在程序过程中多次更改它们的值，通常是为了响应网页中的用户操作。

![](img/bf90ebf56b5f948b05e7a26851204c31_710_0.png)

# 变量与数据类型

JavaScript 变量可以存储不同类型的信息，称为变量的数据类型。JavaScript 支持以下数据类型：

-   数值 (numeric)
-   字符串 (text string)
-   布尔值 (Boolean)
-   对象 (object)
-   空 (null)

数值可以是任何数字，例如 13、22.5 或 3.14159。数字也可以用科学计数法表示，例如用 5.12 表示 5.1 × 10³ (510)。如果你想在 `currentYear` 变量中存储值 2018，可以运行命令：

```javascript
currentYear = 2018;
```

提示
如果你将数字包含在双引号或单引号内，JavaScript 将其视为字符串。

字符串是任何被双引号或单引号包裹的字符组。以下语句在 `currentMonth` 变量中显示文本 "May"。

```javascript
currentMonth = "May";
```

布尔值表示陈述的真假。只有两种可能的布尔值：true（真）或 false（假）。例如，以下语句将 `isMay` 变量设置为 true，将 `isApril` 变量的值设置为 false：

```javascript
var isMay = true, isApril = false;
```

布尔值通常用于必须对不同条件做出不同响应的程序。上述引用的示例可能用于测试当前月份是否为 5 月的程序。如果值设置为 true，程序的运行方式将与设置为 false 时不同。请注意，如果没有给布尔值赋值，它将被解释为值为 false。

表示对象的变量可以用来简化代码，从而消除重写逻辑和有时复杂的对象的需求。因此，接下来的 `dateVar` 将存储 ID 为 `dateNow` 的文档元素的引用。

```javascript
var dateVar = document.getElementById("dateNow");
```

最后，`null` 值表示尚未为变量分配任何值。这可以通过显式地为变量分配关键字 `null` 来完成，如语句所示：

```javascript
var currentDate = null;
```

或者通过简单地声明变量而不赋值来隐式地完成。

# JavaScript 与弱类型语言

在 JavaScript 中，变量的数据类型可以根据其使用的上下文发生变化。在以下两个语句中，`currentMonth` 开始是一个初始值为 4 的数值变量，但随后变成一个包含文本 "May" 的字符串：

```javascript
var currentMonth = 4;
currentMonth = "May";
```

像 JavaScript 这样的编程语言，其变量没有严格绑定到特定的数据类型，被称为**弱类型编程语言**；与之相对的强类型语言则强制程序员显式地插入变量的数据类型。在强类型语言中，代码将导致错误，因为不允许变量从一种数据类型切换到另一种。

虽然强类型语言看起来限制性得多，但它具有标记错误（例如可能发生的错误）的优点。

## 使用变量

创建变量后，你可以在代码中使用它。例如，以下语句使用 `dateVar` 在页面上显示日期：

```javascript
dateNow.innerHTML = dateVar;
```

# 教程 9 JavaScript 入门 | HTML 和 CSS HTML 697

# 图 9-19 创建 Date 对象

![](img/bf90ebf56b5f948b05e7a26851204c31_714_0.png)

```
/* Store the current date and time */
var currentDate = new Date("May 23, 2018 14:35:05");
```

接下来，你应用 JavaScript 的 Date 方法来从此 Date 对象中提取信息。

# 应用 Date 方法

JavaScript 日期存储为数值值，该数值等于指定日期与 1970 年 1 月 1 日午夜之间的毫秒数。例如，2018 年 5 月 23 日下午 2:35:05 的 Date 对象有一个隐藏值，等于 1,527,104,050,000 毫秒。坦率地说，你不需要直接处理这个值！图 9-20 描述了一些用于从 Date 对象中提取信息的 JavaScript 方法。

# 图 9-20 Date 对象的方法

| Date | 方法 | 描述 | 结果 |
| :--- | :--- | :--- | :--- |
| var thisDay = Date("May 23, 2018 14:35:05"); | thisDay.getSeconds() | 秒 | 5 |
| | thisDay.getMinutes() | 分 | 35 |
| | thisDay.getHours() | 小时 | 14 |
| | thisDay.getDate() | 月中的几 | 23 |
| | thisDay.getMonth() | 月份，一月 = 0，二月 = 1， | 4 |
| | thisDay.getFullYear() | 年 | 2018 |
| | thisDay.getDay() | 星期几，星期日 = 0，星期一 = 1， | 3 |
| | thisDay.toLocaleString() | 使用常规的日期文本 | "5/23/2018" |
| | thisDay.toLocaleTimeString() | 使用常规的时间文本 | "2:35:05 PM" |

Hector 想要在页眉中显示日期并在单独的行创建两个变量。以下 `dateString` 变量将存储日期对象部分的文本字符串，而 `timeString` 变量将存储时间部分的文本字符串。

```
var date = currentDate.toLocaleDateString();
var time = currentDate.toLocaleTimeString();
```

`toLocaleString` 和 `toLocaleTimeString` 都根据渲染日期和时间的本地配置返回文本。因此，在美国，这些变量将使用文本 "5/23/2018" 和 "2:35:05 PM"。其他具有不同区域设置的国家将使用这些日期和时间的不同文本表示。

Copyright 2018 Cengage Learning. 版权所有。不得全部或部分复制、扫描或复制。WCN 02-200-203

* 11/3/18 22:44

# HTML 698 HTML 和 CSS | 教程 9 JavaScript 入门

日期时间变量可以使用 `dateNow` 元素的 `innerHTML` 属性来更改插入到元素中的代码：

```javascript
document.getElementById("dateNow").innerHTML = dateStr + "<br />" + timeStr;
```
