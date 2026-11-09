
![](img/5a907eb39993e80f28c82efc2e4632b3_159_0.png)

有关更多字符串和数字方法的列表，请参见 W3Schools 网站 www.w3schools.com/js/js_number_methods.asp 和 www.w3schools.com/js/js_string_methods.asp。

## 提醒用户并提示其输入

向用户显示消息并收集输入，是 JavaScript 提供的交互性的开端。尽管如今已有更复杂的技术，但 `alert()` 方法和 `prompt()` 方法是显示带有消息的弹出框并提示用户输入的简单方式。

创建警告或提示的语法是：在括号内用引号写入文本，调用该方法，如下所示：

```
alert("You have mail!");
prompt("What do you want for dinner?");
```

图 9-6 展示了由 `alert()` 方法创建的警告弹出框，以及由 `prompt()` 方法创建的用于用户输入的提示框。

![](img/5a907eb39993e80f28c82efc2e4632b3_159_1.png)

**图 9-6：** JavaScript 警告弹出框和用户提示。

## 用函数为代码命名

函数是一种将 JavaScript 语句分组的方式，并为这组语句命名，以便通过函数名轻松引用。这些语句通常被分在一起，因为它们实现特定的编码目标。你可以通过只写函数名来重复使用这些语句，而不必一遍又一遍地重写语句。函数可以防止重复，并使代码更易于维护。

我小时候，每个星期六早上，母亲都会让我刷牙、叠衣服、用吸尘器打扫房间，还要修剪草坪。最终，母亲厌倦了一遍又一遍地重复同一份清单，于是把家务清单写在纸上，给它起名为“周六家务”，并贴在冰箱上。函数为一组语句命名，就像“周六家务”是我那份家务清单的名字一样。

函数使用 `function` 一词定义一次，后面跟函数名，然后是一组放在花括号内的语句。这称为*函数声明*。函数中的语句只有在通过名称调用函数时才会执行。在下面的示例中，我声明了一个名为 `greeting` 的函数，它使用 `prompt()` 方法询问你的姓名，返回你输入的姓名并将其存储在名为 `name` 的变量中，然后使用 `alert()` 方法显示一条包含 name 变量的消息：

```javascript
function greeting() {
    var name=prompt("What is your name?");
    alert("Welcome to this website " + name);
}

greeting();
greeting();
```

在函数声明下方，我调用了该函数两次，因此会触发两次询问我姓名的提示，这些姓名存储在变量 name 中，并会显示两条消息，欢迎变量 name 中的值访问本网站。

![](img/5a907eb39993e80f28c82efc2e4632b3_160_0.png)

“+”运算符用于将字符串与其他字符串、值或变量连接（合并）起来。

函数可以接收输入，称为*参数*，以帮助函数运行，并可在函数完成时返回一个值。写完家务清单后，每个星期六早上，母亲会说“Nik，做周六家务”，等我哥哥年龄足够大时，她会说“Neel，做周六家务”。如果家务清单是函数声明，“周六家务”是函数名，那么“Nik”和“Neel”就是参数。最后，在我完成后，我会让母亲知道家务已经完成，就像函数返回值一样。

在下面的示例中，我声明了一个名为 `amountdue` 的函数，它接收 `price` 和 `quantity` 作为参数。该函数在被调用时计算小计，加上应付税款，然后返回总计。函数 `amountdue(10,3)` 返回 31.05。

```javascript
function amountdue(price, quantity) {
    var subtotal=price * quantity;

    var tax = 1.05;
    var total = subtotal + tax;
    return total;
}

alert("The amount due is $" + amountdue(10,3));
```

![](img/5a907eb39993e80f28c82efc2e4632b3_160_1.png)

每个左圆括号都有一个右圆括号，每个左花括号都有一个右花括号，每个左双引号都有一个右双引号。你能在上面的示例中找到所有成对的左右符号吗？

## 将 JavaScript 添加到网页

将 JavaScript 添加到网页的两种方式是：

- 使用 script 标签将 JavaScript 代码嵌入 HTML 文件。
- 使用 script 标签从 HTML 文件链接到单独的 JavaScript 文件。

要将 JavaScript 代码嵌入 HTML 文件，请使用一个开始和结束 `<script>` 标签，并在两个标签之间编写 JavaScript 语句，如下例所示：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Embedded JavaScript</title>
    <script>
      alert("This is embedded JavaScript");
    </script>
  </head>
  <body>
    <h1>Example of embedded JavaScript</h1>
  </body>
</html>
```

`<script>` 标签可以放在开始和结束 `<head>` 标签内，如上所示，也可以放在开始和结束 `<body>` 标签内。选择其中一种方式而不是另一种方式会有一些性能优势，你可以在 http://stackoverflow.com/questions/436411/where-is-the-best-place-to-put-script-tags-in-html-markup 阅读更多内容。

`<script>` 标签也用于链接到单独的 JavaScript 文件，这是推荐的方式。`<script>` 标签包括：

- 一个 `type` 属性，对于 JavaScript，它始终设置为等于 `"text/javascript"`。
- 一个 `src` 属性，它设置为等于 JavaScript 文件的位置。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Linking to a separate JavaScript file</title>
    <script type="text/javascript" src="script.js"></script>
  </head>
  <body>
    <h1>Linking to a separate JavaScript file</h1>
  </body>
</html>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_162_0.png)

无论代码是嵌入在标签之间，还是使用 `src` 属性链接到单独的文件，`<script>` 标签都有开始和结束标签。

## 编写你的第一个 JavaScript 程序

使用 Codecademy 网站在线练习 JavaScript。Codecademy 是一个创建于 2011 年的免费网站，让任何人都可以直接在浏览器中学习编程，而无需安装或下载任何软件。按照以下步骤练习你在本章学到的所有标签（以及一些其他内容）：

- 1. **打开浏览器，访问** `www.dummies.com/go/codingfd`，**并点击指向 Codecademy 的链接。**
- 2. **登录你的 Codecademy 账户。** 注册相关讨论见第 3 章。创建账户可以让你在工作时保存进度，但这是可选的。
- 3. **导航到并点击“Programming 入门”（Getting Started with Programming）。**
- 4. **背景信息显示在网站的左上部分，说明显示在网站的左下部分。**
- 5. **在主编码窗口中完成说明。**
- 6. **完成说明后，点击 Save and Submit Code 按钮。**

如果你正确遵循了说明，会出现一个绿色对勾，并且你会进入下一个练习。如果你的代码中存在错误，会出现警告并给出建议的修复方法。如果你遇到问题，或者有无法修复的错误，请点击链接、使用 Q&A 论坛，或在 Twitter 上发推给我 @nikhilgabraham，并包含话题标签 #codingFD。

## 使用 API

尽管 API（*应用程序编程接口*）已经存在了几十年，但随着我们听到更多关于其使用的讨论和推广，这个术语在过去几年中变得流行起来。*使用 Facebook API！为什么 Craigslist 没有 API？* Stripe 的全部业务就是让开发者使用其支付 API 在线接受付款。

许多人使用 API 这个术语，但很少有人理解它的含义。本节将帮助阐明 API 能做什么以及如何使用它们。

## API 能做什么？

API 允许程序 A 访问另一个独立程序 B 的部分功能。程序 B 通过允许程序 A 以结构化、可预测、有文档记录的方式提出数据请求来授予访问权限，而程序 B 以结构化、可预测、有文档记录的方式响应该数据请求，如下所示（参见图 9-7）：

- **它是结构化的**，因为请求中的字段和响应中的数据遵循易于阅读的标准化格式。例如，Yahoo Weather API 的数据响应包含以下选定的结构化数据字段：

```json
"location": {
    "city": "New York",
    "region": "NY"
},
"units": {
    "temperature": "F"
},
"forecast": [
    {
        "date": "29 Oct 2014",
        "high": "68",
        "low": "48",
        "text": "PM Showers"
    }
]
```

访问 `http://developer.yahoo.com/weather/` 可查看完整的 Yahoo Weather API 响应。

- **它是可预测的**，因为请求中必须包含和可以包含的字段是预先指定的，并且对成功请求的响应将始终包含相同的字段类型。

- **它是有文档记录的**，因为 API 有详细说明。任何更改通常都会通过网站、社交媒体、电子邮件进行传达，而且即使在 API 更改之后，通常也会有一段向后兼容期，在此期间旧的 API 请求仍会收到响应。例如，当 Google Maps 发布其 API 的第 3 版时，第 2 版仍在一段宽限期内继续运行。

![](img/5a907eb39993e80f28c82efc2e4632b3_163_0.png)

**图 9-7：** API 允许两个独立的程序相互通信。

